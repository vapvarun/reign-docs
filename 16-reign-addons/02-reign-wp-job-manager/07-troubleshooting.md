# Reign WP Job Manager Addon - Troubleshooting Guide

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
   - Confirm WP Job Manager is installed and activated
   - Check WordPress version (5.8+)

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
   echo home_url(); // Should match licensed domain
   ```

3. **Deactivate Other Sites**
   - Visit My Account > Licenses
   - Deactivate unused sites
   - Reactivate on current site

## Display Issues

### Issue: Job Listings Not Showing

**Symptoms:**
- Empty job listings page
- Shortcode not rendering
- 404 errors

**Solutions:**

1. **Check Post Status**
   ```sql
   SELECT post_status, COUNT(*) 
   FROM wp_posts 
   WHERE post_type = 'job_listing' 
   GROUP BY post_status;
   ```

2. **Verify Permalinks**
   ```
   Settings > Permalinks > Save Changes
   ```

3. **Check Shortcode Usage**
   ```php
   // Correct usage
   [jobs]
   
   // With parameters
   [jobs per_page="12" show_filters="true"]
   ```

4. **Debug Query**
   ```php
   add_action('pre_get_posts', function($query) {
       if ($query->get('post_type') === 'job_listing') {
           var_dump($query->request);
       }
   });
   ```

### Issue: Layout Broken

**Symptoms:**
- Misaligned elements
- Missing styles
- Responsive issues

**Solutions:**

1. **Clear Cache**
   - Browser cache (Ctrl+F5)
   - WordPress cache plugins
   - CDN cache
   - Server cache

2. **Regenerate CSS**
   ```
   Appearance > Customize > Publish (without changes)
   ```

3. **Check for CSS Conflicts**
   ```css
   /* Add to Additional CSS */
   .job_listings {
       clear: both !important;
       width: 100% !important;
   }
   ```

4. **Verify Theme Compatibility**
   ```php
   $theme = wp_get_theme();
   echo $theme->get('Name'); // Should be "Reign"
   echo $theme->get('Version'); // Should be 7.0+
   ```

### Issue: Maps Not Loading

**Solutions:**

1. **Check Google Maps API Key**
   ```
   Job Listings > Settings > Google Maps API Key
   ```

2. **Verify API Restrictions**
   - Check Google Cloud Console
   - Verify domain restrictions
   - Check API quotas

3. **Debug JavaScript**
   ```javascript
   console.log(typeof google);
   console.log(google.maps);
   ```

## Functionality Issues

### Issue: Job Application Not Working

**Symptoms:**
- Application form not showing
- Emails not sending
- Application errors

**Solutions:**

1. **Check Application Method**
   ```php
   $method = get_the_job_application_method();
   echo 'Application method: ' . $method;
   ```

2. **Test Email Delivery**
   ```php
   wp_mail('test@example.com', 'Test', 'Test message');
   ```

3. **Configure SMTP**
   ```php
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

### Issue: Search/Filter Not Working

**Solutions:**

1. **Check AJAX Handler**
   ```javascript
   console.log(reign_job_vars);
   console.log(reign_job_vars.ajax_url);
   ```

2. **Verify Nonce**
   ```php
   wp_localize_script('reign-job-script', 'reign_job_vars', array(
       'ajax_url' => admin_url('admin-ajax.php'),
       'nonce' => wp_create_nonce('reign_job_nonce')
   ));
   ```

3. **Debug AJAX Request**
   ```javascript
   jQuery(document).ajaxError(function(event, xhr, settings, error) {
       console.error('AJAX Error:', error);
       console.log('URL:', settings.url);
       console.log('Data:', settings.data);
   });
   ```

## Performance Issues

### Issue: Slow Page Load

**Diagnosis:**
```php
add_action('wp_footer', function() {
    echo '<!-- Page generated in ' . timer_stop() . ' seconds -->';
    echo '<!-- Queries: ' . get_num_queries() . ' -->';
});
```

**Solutions:**

1. **Optimize Queries**
   ```php
   // Reduce posts per page
   add_filter('job_manager_get_listings_args', function($args) {
       $args['posts_per_page'] = 10;
       return $args;
   });
   ```

2. **Implement Caching**
   ```php
   // Cache job listings
   $cache_key = 'reign_jobs_' . md5(serialize($_GET));
   $jobs = get_transient($cache_key);
   
   if (!$jobs) {
       $jobs = new WP_Query($args);
       set_transient($cache_key, $jobs, HOUR_IN_SECONDS);
   }
   ```

3. **Lazy Load Images**
   ```html
   <img data-src="image.jpg" class="lazy-load" />
   ```

### Issue: High Memory Usage

**Solutions:**

1. **Increase Memory Limit**
   ```php
   // In wp-config.php
   define('WP_MEMORY_LIMIT', '256M');
   define('WP_MAX_MEMORY_LIMIT', '512M');
   ```

2. **Optimize Image Sizes**
   ```php
   add_filter('job_manager_company_logo_size', function() {
       return array(150, 150);
   });
   ```

## Compatibility Issues

### Issue: Plugin Conflicts

**Common Conflicts:**
- Other job board plugins
- Page builders
- Cache plugins
- Security plugins

**Solutions:**

1. **Identify Conflicts**
   - Deactivate all plugins except required
   - Reactivate one by one
   - Test after each activation

2. **Fix JavaScript Conflicts**
   ```javascript
   jQuery.noConflict();
   (function($) {
       // Your code here
   })(jQuery);
   ```

3. **Resolve CSS Conflicts**
   ```css
   /* Increase specificity */
   .reign-theme .job-listings {
       /* Your styles */
   }
   ```

### Issue: Theme Compatibility

**Solutions:**

1. **Check Theme Functions**
   ```php
   if (!function_exists('reign_get_theme_version')) {
       // Theme function missing
       function reign_get_theme_version() {
           return wp_get_theme()->get('Version');
       }
   }
   ```

2. **Add Theme Support**
   ```php
   add_theme_support('job-manager-templates');
   add_theme_support('wc-product-gallery-zoom');
   ```

## Database Issues

### Issue: Missing Job Meta

**Solutions:**

1. **Check Meta Keys**
   ```sql
   SELECT DISTINCT meta_key 
   FROM wp_postmeta 
   WHERE post_id IN (
       SELECT ID FROM wp_posts 
       WHERE post_type = 'job_listing'
   );
   ```

2. **Repair Missing Meta**
   ```php
   $jobs = get_posts(array(
       'post_type' => 'job_listing',
       'posts_per_page' => -1
   ));
   
   foreach ($jobs as $job) {
       if (!get_post_meta($job->ID, '_job_location', true)) {
           update_post_meta($job->ID, '_job_location', '');
       }
   }
   ```

## Debug Tools

### Enable Debug Mode

```php
// Complete debug configuration
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('SCRIPT_DEBUG', true);
define('SAVEQUERIES', true);

// Reign Job specific
define('REIGN_JOB_DEBUG', true);
```

### Debug Functions

```php
/**
 * Debug helper functions
 */
function reign_job_debug($data, $label = '') {
    if (defined('REIGN_JOB_DEBUG') && REIGN_JOB_DEBUG) {
        error_log($label . ': ' . print_r($data, true));
    }
}

// Usage
reign_job_debug($_POST, 'Form submission');
reign_job_debug($job_query->request, 'SQL Query');
```

### JavaScript Debugging

```javascript
// Debug mode
window.REIGN_JOB_DEBUG = true;

if (window.REIGN_JOB_DEBUG) {
    console.log('Jobs loaded:', $('.job_listing').length);
    console.log('Filters:', $('.job-filter').serialize());
}
```

## Getting Help

### Before Contacting Support

1. **Gather Information**
   ```php
   // System information
   echo 'WordPress: ' . get_bloginfo('version') . "\n";
   echo 'PHP: ' . phpversion() . "\n";
   echo 'Theme: ' . wp_get_theme()->get('Version') . "\n";
   echo 'WP Job Manager: ' . JOB_MANAGER_VERSION . "\n";
   echo 'Reign Job Manager: ' . REIGN_JOB_VERSION . "\n";
   ```

2. **Check Error Logs**
   - WordPress debug.log
   - PHP error log
   - Browser console
   - Server error log

3. **Test in Safe Mode**
   - Default theme
   - Minimal plugins
   - No custom code

### Contact Support

**Support Channels:**
- Email: support@wbcomdesigns.com
- Forum: wbcomdesigns.com/support
- Documentation: docs.wbcomdesigns.com

**Include in Support Request:**
- License key
- Site URL
- Steps to reproduce
- Error messages
- System information
- Debug log excerpt

## Common Error Messages

### "No jobs found"
**Fix:** Check job post status and visibility settings

### "Application method is not valid"
**Fix:** Configure application method in job settings

### "Google Maps API error"
**Fix:** Verify API key and enable required APIs

### "Permission denied"
**Fix:** Check user roles and capabilities

### "Invalid nonce"
**Fix:** Clear cache and check for plugin conflicts

## Next Steps

- [FAQ](08-faq.md) - Frequently asked questions
- [Configuration Guide](03-configuration.md) - Settings reference
- [Developer Guide](05-developer-guide.md) - Advanced solutions