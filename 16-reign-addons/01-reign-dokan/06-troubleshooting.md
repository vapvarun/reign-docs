# Reign Dokan Addon - Troubleshooting Guide

## Common Installation Issues

### Issue: Plugin Activation Failed

**Error Message:**
```
Plugin could not be activated because it triggered a fatal error.
```

**Solutions:**

1. **Check PHP Version**
   ```php
   <?php phpinfo(); ?>
   // Requires PHP 7.4 or higher
   ```

2. **Verify Dependencies**
   - Ensure Reign Theme is active
   - Confirm Dokan is installed and activated
   - Check WooCommerce is active

3. **Enable Debug Mode**
   ```php
   // In wp-config.php
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   define('WP_DEBUG_DISPLAY', false);
   ```

4. **Check Error Log**
   ```
   /wp-content/debug.log
   ```

### Issue: License Activation Failed

**Error Messages:**
- "Invalid license key"
- "License key expired"
- "Site limit exceeded"

**Solutions:**

1. **Verify License Key**
   - Login to WBcom Designs account
   - Copy exact license key
   - Remove any spaces

2. **Check Site URL**
   ```php
   // License is tied to site URL
   echo home_url(); // Should match licensed domain
   ```

3. **Deactivate Other Sites**
   - Visit My Account > Licenses
   - Deactivate unused sites
   - Reactivate on current site

4. **Contact Support**
   - Email: support@wbcomdesigns.com
   - Include order ID and site URL

## Display Issues

### Issue: Store Layout Broken

**Symptoms:**
- Misaligned elements
- Missing styles
- Broken grid layout

**Solutions:**

1. **Clear Cache**
   ```bash
   # Clear all caches
   - Browser cache (Ctrl+F5)
   - WordPress cache plugins
   - CDN cache
   - Server cache
   ```

2. **Regenerate CSS**
   ```
   Appearance > Customize > Publish (without changes)
   ```

3. **Check Theme Compatibility**
   ```php
   // Verify theme version
   $theme = wp_get_theme();
   echo $theme->get('Version'); // Should be 7.0+
   ```

4. **Fix CSS Conflicts**
   ```css
   /* Add to Additional CSS */
   .dokan-store-wrap {
       clear: both !important;
       width: 100% !important;
   }
   ```

### Issue: Store Banner Not Showing

**Solutions:**

1. **Check Image Upload**
   ```php
   // Verify upload directory permissions
   $upload_dir = wp_upload_dir();
   echo 'Upload path: ' . $upload_dir['path'];
   // Should be writable (755 or 775)
   ```

2. **Verify Image Dimensions**
   - Minimum: 1200x300px
   - Maximum file size: 2MB
   - Format: JPG, PNG

3. **Database Check**
   ```sql
   SELECT meta_value 
   FROM wp_usermeta 
   WHERE user_id = [vendor_id] 
   AND meta_key = 'dokan_banner';
   ```

### Issue: Products Not Displaying

**Solutions:**

1. **Check Vendor Status**
   ```php
   $vendor = dokan()->vendor->get($vendor_id);
   var_dump($vendor->is_enabled()); // Should be true
   ```

2. **Verify Product Visibility**
   ```sql
   SELECT post_status, post_author 
   FROM wp_posts 
   WHERE post_type = 'product' 
   AND post_author = [vendor_id];
   ```

3. **Fix Query Issues**
   ```php
   add_filter('dokan_store_products_query', function($query) {
       $query['post_status'] = 'publish';
       return $query;
   });
   ```

## Functionality Issues

### Issue: Vendor Dashboard Access Denied

**Solutions:**

1. **Check User Role**
   ```php
   $user = wp_get_current_user();
   var_dump($user->roles); // Should include 'seller'
   ```

2. **Verify Capabilities**
   ```php
   if (current_user_can('dokandar')) {
       echo 'Has vendor capabilities';
   }
   ```

3. **Reset User Roles**
   ```php
   $user = new WP_User($vendor_id);
   $user->remove_role('subscriber');
   $user->add_role('seller');
   ```

### Issue: Widgets Not Appearing

**Solutions:**

1. **Check Widget Registration**
   ```php
   global $wp_registered_widgets;
   print_r(array_keys($wp_registered_widgets));
   ```

2. **Verify Widget Areas**
   ```php
   global $wp_registered_sidebars;
   print_r($wp_registered_sidebars);
   ```

3. **Fix Widget Display**
   ```php
   // Force widget display
   add_filter('sidebars_widgets', function($sidebars) {
       // Check if widgets are assigned
       return $sidebars;
   });
   ```

## Performance Issues

### Issue: Slow Store Loading

**Diagnosis:**
```php
// Add to functions.php temporarily
add_action('wp_footer', function() {
    echo '<!-- Page generated in ' . timer_stop() . ' seconds -->';
    echo '<!-- Queries: ' . get_num_queries() . ' -->';
});
```

**Solutions:**

1. **Optimize Database**
   ```sql
   -- Add indexes
   ALTER TABLE wp_usermeta 
   ADD INDEX idx_dokan_meta (meta_key(20));
   
   -- Optimize tables
   OPTIMIZE TABLE wp_posts, wp_postmeta, wp_usermeta;
   ```

2. **Implement Caching**
   ```php
   // Cache vendor data
   function get_cached_vendor($vendor_id) {
       $cache_key = 'vendor_data_' . $vendor_id;
       $data = wp_cache_get($cache_key);
       
       if (!$data) {
           $data = dokan()->vendor->get($vendor_id);
           wp_cache_set($cache_key, $data, '', 3600);
       }
       
       return $data;
   }
   ```

3. **Reduce Queries**
   ```php
   // Batch load vendor meta
   function load_vendor_meta($vendor_ids) {
       global $wpdb;
       
       $query = "SELECT user_id, meta_key, meta_value 
                FROM {$wpdb->usermeta} 
                WHERE user_id IN (" . implode(',', $vendor_ids) . ")
                AND meta_key LIKE 'dokan_%'";
       
       return $wpdb->get_results($query);
   }
   ```

### Issue: High Memory Usage

**Solutions:**

1. **Increase Memory Limit**
   ```php
   // In wp-config.php
   define('WP_MEMORY_LIMIT', '256M');
   define('WP_MAX_MEMORY_LIMIT', '512M');
   ```

2. **Optimize Image Loading**
   ```php
   // Use appropriate image sizes
   add_filter('dokan_store_banner_size', function() {
       return array(1200, 300);
   });
   ```

3. **Limit Query Results**
   ```php
   add_filter('dokan_store_products_per_page', function() {
       return 12; // Reduce from default
   });
   ```

## Compatibility Issues

### Issue: Conflict with Other Plugins

**Common Conflicts:**
- Cache plugins
- Security plugins
- Other marketplace plugins
- Page builders

**Solutions:**

1. **Identify Conflicts**
   ```php
   // Deactivate all plugins except required
   // Reactivate one by one
   ```

2. **Fix JavaScript Conflicts**
   ```javascript
   // Use no-conflict mode
   jQuery.noConflict();
   (function($) {
       // Your code here
   })(jQuery);
   ```

3. **Resolve CSS Conflicts**
   ```css
   /* Increase specificity */
   .reign-theme .dokan-store-wrap {
       /* Your styles */
   }
   ```

### Issue: Theme Compatibility

**Solutions:**

1. **Check Theme Support**
   ```php
   // Verify Reign theme functions
   if (function_exists('reign_get_theme_version')) {
       echo reign_get_theme_version();
   }
   ```

2. **Add Compatibility Layer**
   ```php
   // Add theme support
   add_theme_support('dokan');
   add_theme_support('woocommerce');
   ```

## Email Issues

### Issue: Vendor Emails Not Sending

**Solutions:**

1. **Check Email Settings**
   ```php
   // Test WordPress email
   wp_mail('test@example.com', 'Test', 'Test message');
   ```

2. **Configure SMTP**
   ```php
   // Use SMTP plugin or add to functions.php
   add_action('phpmailer_init', function($phpmailer) {
       $phpmailer->isSMTP();
       $phpmailer->Host = 'smtp.gmail.com';
       $phpmailer->SMTPAuth = true;
       $phpmailer->Port = 587;
       $phpmailer->Username = 'your-email@gmail.com';
       $phpmailer->Password = 'your-password';
       $phpmailer->SMTPSecure = 'tls';
   });
   ```

3. **Debug Email Issues**
   ```php
   // Enable email debugging
   add_action('wp_mail_failed', function($error) {
       error_log('Email error: ' . print_r($error, true));
   });
   ```

## Database Issues

### Issue: Missing Database Tables

**Solutions:**

1. **Check Tables**
   ```sql
   SHOW TABLES LIKE '%dokan%';
   ```

2. **Recreate Tables**
   ```php
   // Trigger Dokan table creation
   dokan()->activate();
   ```

3. **Manual Table Creation**
   ```sql
   -- If needed, create manually
   CREATE TABLE IF NOT EXISTS wp_dokan_vendor_balance (
       id bigint(20) NOT NULL AUTO_INCREMENT,
       vendor_id bigint(20) NOT NULL,
       -- other columns
       PRIMARY KEY (id)
   );
   ```

## Debug Tools

### Enable Debug Logging

```php
// Complete debug configuration
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('SCRIPT_DEBUG', true);
define('SAVEQUERIES', true);

// Reign Dokan specific
define('REIGN_DOKAN_DEBUG', true);
```

### Query Monitor

```php
// Install Query Monitor plugin
// Check for:
- Slow queries
- PHP errors
- HTTP requests
- Hooks and actions
```

### Browser Console

```javascript
// Check for JavaScript errors
console.log('Reign Dokan loaded:', typeof ReignDokan !== 'undefined');

// Debug AJAX requests
jQuery(document).ajaxError(function(event, xhr, settings, error) {
    console.error('AJAX Error:', error, settings.url);
});
```

## Getting Help

### Before Contacting Support

1. **Gather Information**
   - WordPress version
   - Theme version
   - Plugin versions
   - PHP version
   - Error messages
   - Debug log

2. **Create System Report**
   ```php
   // System information
   echo 'WordPress: ' . get_bloginfo('version') . "\n";
   echo 'PHP: ' . phpversion() . "\n";
   echo 'Theme: ' . wp_get_theme()->get('Version') . "\n";
   echo 'Dokan: ' . DOKAN_PLUGIN_VERSION . "\n";
   echo 'Reign Dokan: ' . REIGN_DOKAN_VERSION . "\n";
   ```

### Contact Support

**Support Channels:**
- Email: support@wbcomdesigns.com
- Forum: wbcomdesigns.com/support
- Documentation: docs.wbcomdesigns.com

**Include in Support Request:**
- License key
- Site URL
- Steps to reproduce
- Screenshots/videos
- System report
- Debug log excerpt

## Next Steps

- [FAQ](07-faq.md) - Frequently asked questions
- [Developer Guide](05-developer-guide.md) - Advanced solutions
- [Configuration Guide](03-configuration.md) - Settings reference