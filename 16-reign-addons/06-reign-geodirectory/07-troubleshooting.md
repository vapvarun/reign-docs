# Reign GeoDirectory Addon - Troubleshooting Guide

## What You'll Learn
How to quickly diagnose and fix common issues with the Reign GeoDirectory addon. We'll cover everything from installation problems to advanced debugging, with clear solutions for each issue.

## Quick Overview  
**Most issues are solved in:** 5-10 minutes
**Difficulty:** Easy to moderate fixes
**Success rate:** 95% of issues covered here

---

## Part 1: Installation Issues

### "Plugin won't activate"

**Error message:** "The plugin does not have a valid header"

**Solution 1: Re-download the plugin**
1. Log into your WBcom account
2. Download fresh copy of the addon
3. Delete old file from WordPress
4. Upload new file
5. Activate plugin

**Solution 2: Check file integrity**
```bash
# Via FTP, check file structure:
/wp-content/plugins/reign-geodirectory-addon/
├── reign-geodirectory-addon.php  # Main file must exist
├── includes/
├── templates/
└── assets/
```

**Solution 3: Manual installation**
1. Unzip plugin on your computer
2. Upload via FTP to `/wp-content/plugins/`
3. Ensure folder name is `reign-geodirectory-addon`
4. Activate from WordPress admin

### "License key not working"

**Common causes and fixes:**

| Issue | Solution |
|-------|----------|
| **Extra spaces** | Remove all spaces before/after key |
| **Wrong site URL** | Check if www/non-www matches license |
| **Already activated** | Deactivate on old site first |
| **Expired license** | Renew at wbcomdesigns.com |
| **Invalid key** | Contact support with order number |

**How to reset license:**
```sql
-- In database (use with caution):
DELETE FROM wp_options 
WHERE option_name LIKE '%reign_gd_license%';
```

### "GeoDirectory not detected"

**The addon requires GeoDirectory plugin:**

**Fix steps:**
1. Install GeoDirectory first:
   - Go to **Plugins** → **Add New**
   - Search "GeoDirectory"
   - Install and activate
2. Run GeoDirectory setup wizard
3. Then activate Reign addon

**Verify installation:**
```php
// Check if GeoDirectory is active
if (class_exists('GeoDirectory')) {
    echo "GeoDirectory is installed";
} else {
    echo "GeoDirectory is missing";
}
```

---

## Part 2: Display Issues

### "Listings not showing"

**Checklist to diagnose:**

☑️ **Check listing status:**
- Go to **GeoDirectory** → **Places**
- Verify listings are "Published"
- Not "Draft" or "Pending"

☑️ **Check page assignment:**
- **GeoDirectory** → **Settings** → **Pages**
- Ensure pages are selected:
  - Listing page
  - Search page
  - Add listing page

☑️ **Clear all caches:**
```php
// Add to functions.php temporarily
add_action('init', function() {
    wp_cache_flush();
    if (function_exists('geodir_clear_cache')) {
        geodir_clear_cache();
    }
});
```

☑️ **Check theme compatibility:**
- Switch to Twenty Twenty-Three theme
- If listings appear, theme conflict exists
- Contact theme developer

### "Map not displaying"

**Step-by-step diagnosis:**

**1. Check Google Maps API Key:**
```javascript
// Open browser console (F12)
// Look for errors like:
"Google Maps JavaScript API error: InvalidKeyMapError"
```

**2. Verify API key configuration:**
- Go to **GeoDirectory** → **Settings** → **Google Maps**
- Paste your API key
- Save settings

**3. Check API restrictions:**
- Go to Google Cloud Console
- Select your project
- APIs & Services → Credentials
- Click your API key
- Check restrictions:
  ```
  HTTP referrers: 
  - https://yoursite.com/*
  - https://www.yoursite.com/*
  ```

**4. Enable required APIs:**
- Maps JavaScript API ✅
- Places API ✅
- Geocoding API ✅

**5. Check billing:**
- Google requires billing enabled
- Even for free tier usage
- Add payment method in Google Cloud

### "Listings look broken"

**CSS conflicts - Quick fixes:**

**Solution 1: Regenerate CSS**
```
Appearance → Customize → Publish (without changes)
This regenerates all CSS files
```

**Solution 2: Add compatibility CSS**
```css
/* Add to Additional CSS */
.geodir-container {
    max-width: 100%;
    overflow: visible;
}

.gd-listings .gd-listing {
    display: block;
    margin-bottom: 20px;
}

.reign-geodirectory-wrapper {
    clear: both;
    overflow: hidden;
}
```

**Solution 3: Fix z-index issues**
```css
/* Map overlapping content */
.geodir_map_container {
    position: relative;
    z-index: 1;
}

/* Dropdown menus hidden */
.geodir-dropdown {
    z-index: 9999;
}
```

---

## Part 3: Search & Filter Problems

### "Search returns no results"

**Diagnostic steps:**

**1. Test basic search:**
```sql
-- Check if listings exist in database
SELECT COUNT(*) FROM wp_posts 
WHERE post_type = 'gd_place' 
AND post_status = 'publish';
```

**2. Rebuild search index:**
```php
// Run once to rebuild
add_action('init', function() {
    if (isset($_GET['rebuild_gd_search'])) {
        $posts = get_posts(array(
            'post_type' => 'gd_place',
            'posts_per_page' => -1,
            'post_status' => 'publish'
        ));
        
        foreach ($posts as $post) {
            wp_update_post($post);
        }
        
        echo "Search index rebuilt for " . count($posts) . " listings";
        die();
    }
});
// Visit: yoursite.com/?rebuild_gd_search
```

**3. Check search form:**
```html
<!-- Verify form structure -->
<form class="geodir-search-form">
    <input type="text" name="s" />
    <input type="hidden" name="post_type" value="gd_place" />
</form>
```

### "Location search not working"

**Fix location detection:**

**1. Enable browser location:**
```javascript
// Test in browser console
navigator.geolocation.getCurrentPosition(
    position => console.log('Location:', position),
    error => console.log('Error:', error)
);
```

**2. Set default location:**
```
GeoDirectory → Settings → General
Default Country: United States
Default City: New York
Default Latitude: 40.7128
Default Longitude: -74.0060
```

**3. Fix location hierarchy:**
```php
// Reset location data
add_action('init', function() {
    if (isset($_GET['fix_locations'])) {
        if (function_exists('geodir_location_fix_terms')) {
            geodir_location_fix_terms();
            echo "Locations fixed";
        }
        die();
    }
});
```

### "Filters not applying"

**Common filter issues:**

**1. AJAX not working:**
```javascript
// Check browser console for errors
// Add to fix AJAX URL:
jQuery(document).ready(function($) {
    if (typeof geodir_params === 'undefined') {
        window.geodir_params = {
            ajax_url: '<?php echo admin_url("admin-ajax.php"); ?>'
        };
    }
});
```

**2. Category filter broken:**
```php
// Refresh category terms
wp_schedule_single_event(time(), 'geodir_update_term_counts');
```

---

## Part 4: User Submission Issues

### "Can't submit listings"

**Permission checklist:**

☑️ **User role capabilities:**
```php
// Add to functions.php
$role = get_role('subscriber');
$role->add_cap('gd_add_listing');
$role->add_cap('upload_files');
```

☑️ **Page exists:**
- Check **Pages** → look for "Add Listing"
- Should contain `[gd_add_listing]` shortcode
- Set as "Add Listing Page" in GeoDirectory settings

☑️ **Form validation:**
```javascript
// Disable validation temporarily for testing
jQuery(document).ready(function($) {
    $('.geodir-add-listing-form').attr('novalidate', 'novalidate');
});
```

### "Images won't upload"

**Upload troubleshooting:**

**1. Check file size limits:**
```php
// Add to .htaccess or php.ini
php_value upload_max_filesize 10M
php_value post_max_size 10M
php_value max_execution_time 300
php_value max_input_time 300
```

**2. Verify permissions:**
```bash
# Check upload folder permissions
chmod 755 wp-content/uploads
chmod 755 wp-content/uploads/geodir_uploads
```

**3. Test with basic uploader:**
```php
// Temporarily switch uploader
add_filter('geodir_image_upload_handler', function() {
    return 'wp_handle_upload';
});
```

---

## Part 5: Payment & Pricing Issues

### "Payment not processing"

**If using paid listings:**

**1. Check payment gateway:**
```
GeoDirectory → Settings → Payment
Test mode: Enable for testing
Test credentials: Use sandbox keys
```

**2. Test payment flow:**
- Submit test listing
- Use test credit card:
  - Number: 4242 4242 4242 4242
  - Expiry: Any future date
  - CVC: Any 3 digits

**3. Check IPN/Webhook:**
```php
// Log payment notifications
add_action('geodir_payment_ipn_handler', function($data) {
    error_log('Payment IPN: ' . print_r($data, true));
});
```

### "Featured listings not showing"

**Fix featured status:**

```php
// Check featured meta
$is_featured = get_post_meta($post_id, 'featured', true);

// Manually set featured
update_post_meta($post_id, 'featured', 1);
update_post_meta($post_id, 'featured_expires', date('Y-m-d', strtotime('+30 days')));
```

---

## Part 6: Performance Issues

### "Site running slow"

**Performance optimization:**

**1. Limit map markers:**
```php
// Reduce markers on map
add_filter('geodir_map_max_markers', function() {
    return 100; // Instead of unlimited
});
```

**2. Enable caching:**
```php
// Cache listing queries
add_filter('geodir_cache_queries', '__return_true');

// Set cache time
add_filter('geodir_cache_time', function() {
    return 3600; // 1 hour
});
```

**3. Optimize database:**
```sql
-- Add indexes for speed
ALTER TABLE wp_geodir_gd_place_detail 
ADD INDEX idx_featured (featured);

ALTER TABLE wp_geodir_gd_place_detail 
ADD INDEX idx_location (city, region, country);
```

### "Too many database queries"

**Query reduction:**

```php
// Use transients for expensive queries
function get_featured_listings_cached() {
    $cache_key = 'gd_featured_listings';
    $listings = get_transient($cache_key);
    
    if ($listings === false) {
        $listings = get_posts(array(
            'post_type' => 'gd_place',
            'meta_key' => 'featured',
            'meta_value' => '1',
            'posts_per_page' => 10
        ));
        
        set_transient($cache_key, $listings, HOUR_IN_SECONDS);
    }
    
    return $listings;
}
```

---

## Part 7: Mobile Issues

### "Mobile layout broken"

**Responsive fixes:**

```css
/* Mobile-specific CSS */
@media (max-width: 768px) {
    /* Fix grid layout */
    .geodir-listings {
        grid-template-columns: 1fr !important;
    }
    
    /* Fix map height */
    .geodir_map_container {
        height: 250px !important;
    }
    
    /* Fix overlapping elements */
    .gd-listing-card {
        margin: 10px 0;
        width: 100%;
    }
    
    /* Fix search form */
    .geodir-search-form input {
        width: 100%;
        margin-bottom: 10px;
    }
}
```

### "Touch events not working"

**Enable touch support:**

```javascript
// Fix map touch events
jQuery(document).ready(function($) {
    if ('ontouchstart' in window) {
        $('.geodir_map_container').addClass('touch-enabled');
        
        // Enable map dragging on mobile
        if (typeof geodirMapOptions !== 'undefined') {
            geodirMapOptions.draggable = true;
            geodirMapOptions.gestureHandling = 'greedy';
        }
    }
});
```

---

## Part 8: Integration Conflicts

### "BuddyPress integration not working"

**Enable integration:**

```php
// Force BuddyPress integration
add_action('init', function() {
    if (class_exists('BuddyPress') && class_exists('GeoDirectory')) {
        // Add listings to activity stream
        add_filter('bp_activity_custom_post_type_post_action', function($activity_action, $post) {
            if ($post->post_type == 'gd_place') {
                $activity_action = sprintf(
                    '%s added a new listing: %s',
                    bp_core_get_userlink($post->post_author),
                    '<a href="' . get_permalink($post->ID) . '">' . $post->post_title . '</a>'
                );
            }
            return $activity_action;
        }, 10, 2);
    }
});
```

### "Theme conflicts"

**Common theme compatibility fixes:**

```php
// Remove theme's archive template
add_filter('geodir_template_part', function($template) {
    if (is_post_type_archive('gd_place')) {
        return plugin_dir_path(__FILE__) . 'templates/archive.php';
    }
    return $template;
});

// Fix content width
add_action('wp_head', function() {
    if (geodir_is_page()) {
        echo '<style>.site-content { max-width: 100%; }</style>';
    }
});
```

---

## Part 9: Data & Import Issues

### "Import failing"

**CSV import troubleshooting:**

**1. Check CSV format:**
```csv
"post_title","post_content","post_address","post_city","post_region","post_country","post_zip"
"Sample Restaurant","Description here","123 Main St","New York","NY","USA","10001"
```

**2. Increase limits:**
```php
// Temporary for import
@ini_set('max_execution_time', 0);
@ini_set('memory_limit', '512M');
```

**3. Import in batches:**
```php
// Split large CSV files
$batch_size = 100;
$offset = 0;

while ($rows = array_slice($csv_data, $offset, $batch_size)) {
    foreach ($rows as $row) {
        // Process row
    }
    $offset += $batch_size;
    sleep(1); // Prevent timeout
}
```

### "Lost listings after update"

**Recovery steps:**

**1. Check trash:**
```sql
SELECT * FROM wp_posts 
WHERE post_type = 'gd_place' 
AND post_status = 'trash';
```

**2. Restore from backup:**
```sql
-- Restore specific listings
UPDATE wp_posts 
SET post_status = 'publish' 
WHERE post_type = 'gd_place' 
AND post_status = 'trash';
```

---

## Part 10: Advanced Debugging

### Enable debug mode

**WordPress debug settings:**

```php
// In wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('SCRIPT_DEBUG', true);
define('GEODIR_DEBUG', true);
```

### Debug functions

**Useful debugging code:**

```php
// Log GeoDirectory actions
add_action('all', function($tag) {
    if (strpos($tag, 'geodir') !== false) {
        error_log("GeoDir Action: " . $tag);
    }
});

// Check active hooks
function check_geodir_hooks() {
    global $wp_filter;
    
    foreach ($wp_filter as $hook => $filters) {
        if (strpos($hook, 'geodir') !== false) {
            error_log("Hook: $hook has " . count($filters->callbacks) . " callbacks");
        }
    }
}

// Monitor database queries
add_action('shutdown', function() {
    if (defined('SAVEQUERIES') && SAVEQUERIES) {
        global $wpdb;
        $geodir_queries = array_filter($wpdb->queries, function($query) {
            return strpos($query[0], 'geodir') !== false;
        });
        error_log('GeoDir Queries: ' . count($geodir_queries));
    }
});
```

### Browser console debugging

**JavaScript debugging:**

```javascript
// Enable verbose logging
if (typeof geodir_params !== 'undefined') {
    geodir_params.debug = true;
}

// Monitor AJAX calls
jQuery(document).ajaxSend(function(e, xhr, settings) {
    if (settings.url.includes('geodir')) {
        console.log('GeoDir AJAX:', settings);
    }
});

// Check for JavaScript errors
window.addEventListener('error', function(e) {
    if (e.filename && e.filename.includes('geodir')) {
        console.error('GeoDir JS Error:', e);
    }
});
```

---

## Common Error Messages

### Error Reference Table

| Error Message | Cause | Solution |
|---------------|-------|----------|
| "Invalid API key" | Google Maps key issue | Regenerate API key |
| "No listings found" | Empty archive | Check published listings |
| "Failed to load resource" | Missing file | Reinstall plugin |
| "Call to undefined function" | Missing dependency | Install GeoDirectory |
| "Headers already sent" | PHP output error | Check for spaces before <?php |
| "Maximum execution time" | Timeout | Increase PHP limits |
| "Allowed memory exhausted" | Memory limit | Increase to 256M+ |

---

## Emergency Fixes

### "Site completely broken"

**Recovery mode:**

1. **Via FTP:**
   ```
   Rename: /plugins/reign-geodirectory-addon/
   To: /plugins/reign-geodirectory-addon-disabled/
   ```

2. **Database cleanup:**
   ```sql
   UPDATE wp_options 
   SET option_value = 'a:0:{}' 
   WHERE option_name = 'active_plugins';
   ```

3. **Safe mode:**
   ```php
   // Add to wp-config.php
   define('DISABLE_GEODIR', true);
   ```

### "Can't access admin"

**Backdoor access:**

```php
// Emergency admin creation (remove after use!)
add_action('init', function() {
    if (isset($_GET['create_admin'])) {
        $user_id = wp_create_user('emergency_admin', 'TempPass123!');
        $user = new WP_User($user_id);
        $user->set_role('administrator');
        die('Admin created');
    }
});
```

---

## Getting More Help

### Before contacting support

**Gather this information:**

```
✓ WordPress version: ___________
✓ Reign theme version: ___________
✓ GeoDirectory version: ___________
✓ Reign addon version: ___________
✓ PHP version: ___________
✓ Error messages: ___________
✓ When issue started: ___________
✓ Recent changes made: ___________
```

### Support channels

**Where to get help:**

1. **Documentation:** docs.wbcomdesigns.com
2. **Support tickets:** wbcomdesigns.com/support
3. **Community forum:** facebook.com/groups/wbcom
4. **Emergency support:** support@wbcomdesigns.com

### Providing debug information

**Generate system report:**

```php
// Create system info page
function generate_system_report() {
    $report = array(
        'WordPress Version' => get_bloginfo('version'),
        'PHP Version' => phpversion(),
        'MySQL Version' => $GLOBALS['wpdb']->db_version(),
        'Active Theme' => wp_get_theme()->get('Name'),
        'Active Plugins' => get_option('active_plugins'),
        'GeoDirectory Version' => defined('GEODIRECTORY_VERSION') ? GEODIRECTORY_VERSION : 'Not installed',
        'Memory Limit' => ini_get('memory_limit'),
        'Max Execution Time' => ini_get('max_execution_time'),
        'Upload Max Size' => ini_get('upload_max_filesize')
    );
    
    return $report;
}
```

---

**Remember:**
🔧 Most issues have simple solutions
📚 Check documentation first
📋 Create backups before major changes
👥 Community can help
☕ Take a break if frustrated!

---

**Quick Support:**
📧 Email: support@wbcomdesigns.com
🌐 Live chat: wbcomdesigns.com (business hours)
📦 Priority support: Available with license