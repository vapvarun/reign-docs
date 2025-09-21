# Reign TutorLMS Addon - Troubleshooting Guide

## Overview

This comprehensive troubleshooting guide addresses common issues with Reign TutorLMS Addon v2.0.0, including social integration problems, AJAX functionality issues, context detection failures, and performance optimization solutions.

---

## Part 1: Installation and Activation Issues

### Plugin Installation Problems

#### Issue: "Plugin could not be activated because it triggered a fatal error"

**Symptoms:**
- White screen after activation
- Fatal error message
- Plugin fails to activate

**Solutions:**

1. **Check PHP Version Compatibility**
   ```bash
   # Check current PHP version
   php -v
   ```
   - **Requirement**: PHP 7.4 or higher
   - **Recommended**: PHP 8.0+

2. **Verify Required Dependencies**
   ```yaml
   Required Plugins:
   - TutorLMS: Active and updated
   - Reign Theme: Active and updated

   Optional Dependencies:
   - BuddyPress: For profile integration
   - PeepSo: For PeepSo integration
   ```

3. **Memory Limit Issues**
   ```php
   // Add to wp-config.php
   ini_set('memory_limit', '256M');
   define('WP_MEMORY_LIMIT', '256M');
   ```

4. **Plugin Conflict Resolution**
   ```yaml
   Testing Process:
   1. Deactivate all plugins except TutorLMS and Reign
   2. Activate Reign TutorLMS Addon
   3. Reactivate plugins one by one
   4. Identify conflicting plugin
   ```

#### Issue: "License activation failed"

**Solutions:**

1. **Verify License Key Format**
   ```
   Correct Format: XXXX-XXXX-XXXX-XXXX
   Common Issues:
   - Extra spaces before/after
   - Missing hyphens
   - Wrong case (should be uppercase)
   ```

2. **Check Domain Configuration**
   ```yaml
   Common Domain Issues:
   - www vs non-www mismatch
   - HTTP vs HTTPS mismatch
   - Subdomain vs main domain
   - Development vs production URLs
   ```

3. **License Server Connection**
   ```bash
   # Test connection to license server
   curl -I https://wbcomdesigns.com/
   ```

---

## Part 2: Social Integration Issues

### BuddyPress Integration Problems

#### Issue: "My Courses" tab not appearing in profiles

**Diagnostic Steps:**

1. **Verify BuddyPress Activation**
   ```php
   // Check if BuddyPress is active
   if (function_exists('bp_is_active')) {
       echo "BuddyPress is active";
   } else {
       echo "BuddyPress is not active";
   }
   ```

2. **Check Profile Component**
   ```yaml
   BuddyPress Settings:
   - Go to Settings → BuddyPress → Components
   - Ensure "User Profiles" is enabled
   - Check "Activity Streams" is enabled
   ```

3. **Template Compatibility**
   ```php
   // Check if theme supports BuddyPress
   if (bp_is_theme_compat_active()) {
       echo "Theme compatibility mode is active";
   }
   ```

**Solutions:**

1. **Force Tab Registration**
   ```php
   // Add to functions.php for testing
   function force_reign_tutor_bp_tab() {
       if (function_exists('bp_core_new_nav_item')) {
           bp_core_new_nav_item(array(
               'name' => 'My Courses',
               'slug' => 'courses',
               'position' => 30,
               'default_subnav_slug' => 'enrolled'
           ));
       }
   }
   add_action('bp_setup_nav', 'force_reign_tutor_bp_tab', 100);
   ```

2. **Clear BuddyPress Cache**
   ```php
   // Clear BuddyPress navigation cache
   wp_cache_flush();
   bp_core_clear_cache();
   ```

3. **Check User Roles and Capabilities**
   ```php
   // Verify current user can access profiles
   if (bp_is_my_profile() || bp_current_user_can('bp_view', bp_displayed_user_id())) {
       echo "User has profile access";
   }
   ```

#### Issue: Course activities not showing in activity stream

**Solutions:**

1. **Activity Component Check**
   ```yaml
   BuddyPress Settings:
   - Ensure "Activity Streams" component is active
   - Check activity types are not filtered out
   ```

2. **Manual Activity Test**
   ```php
   // Test activity creation manually
   if (function_exists('bp_activity_add')) {
       bp_activity_add(array(
           'user_id' => get_current_user_id(),
           'type' => 'tutor_course_test',
           'action' => 'Testing TutorLMS activity integration',
           'component' => 'tutor'
       ));
   }
   ```

### PeepSo Integration Problems

#### Issue: Courses not displaying in PeepSo profiles

**Diagnostic Steps:**

1. **Verify PeepSo Installation**
   ```php
   // Check PeepSo activation
   if (class_exists('PeepSo')) {
       echo "PeepSo version: " . PeepSo::PLUGIN_VERSION;
   }
   ```

2. **Check Profile Segment Registration**
   ```php
   // Debug profile segments
   $segments = PeepSoProfileShortcode::get_instance()->get_segments();
   var_dump($segments);
   ```

**Solutions:**

1. **Manual Profile Integration**
   ```php
   // Force PeepSo profile integration
   function force_peepso_courses_tab($tabs) {
       $tabs['courses'] = array(
           'label' => __('Courses', 'reign-tutorlms-addon'),
           'icon' => 'ps-icon-education'
       );
       return $tabs;
   }
   add_filter('peepso_navigation_profile', 'force_peepso_courses_tab', 10, 1);
   ```

2. **Profile Widget Reset**
   ```php
   // Reset PeepSo profile widgets
   delete_option('peepso_profile_widgets');
   ```

---

## Part 3: AJAX and JavaScript Issues

### AJAX Progress Updates Not Working

#### Issue: Progress bars not updating in real-time

**Diagnostic Steps:**

1. **Check Browser Console**
   ```javascript
   // Open browser console (F12) and look for:
   // - JavaScript errors
   // - Failed AJAX requests
   // - Network connectivity issues
   ```

2. **Verify AJAX Configuration**
   ```javascript
   // Check if AJAX variables are loaded
   console.log(reign_tutor_ajax);
   // Should output object with ajax_url, nonce, etc.
   ```

3. **Test AJAX Endpoint**
   ```bash
   # Test AJAX endpoint directly
   curl -X POST "https://yoursite.com/wp-admin/admin-ajax.php" \
        -d "action=reign_tutor_update_progress&nonce=NONCE_VALUE"
   ```

**Solutions:**

1. **Script Loading Issues**
   ```php
   // Ensure scripts are loaded correctly
   function debug_reign_tutor_scripts() {
       global $wp_scripts;
       if (isset($wp_scripts->registered['reign-tutor-ajax'])) {
           echo "AJAX script is registered";
       } else {
           echo "AJAX script NOT registered";
       }
   }
   add_action('wp_footer', 'debug_reign_tutor_scripts');
   ```

2. **Nonce Verification Issues**
   ```php
   // Debug nonce verification
   function debug_ajax_nonce() {
       if (isset($_POST['nonce'])) {
           $verified = wp_verify_nonce($_POST['nonce'], 'reign_tutor_ajax_nonce');
           error_log('Nonce verification: ' . ($verified ? 'PASSED' : 'FAILED'));
       }
   }
   add_action('wp_ajax_reign_tutor_update_progress', 'debug_ajax_nonce', 1);
   ```

3. **JavaScript Conflict Resolution**
   ```javascript
   // Check for jQuery conflicts
   jQuery(document).ready(function($) {
       if (typeof $ === 'undefined') {
           console.error('jQuery is not loaded');
       } else {
           console.log('jQuery version:', $.fn.jquery);
       }
   });
   ```

#### Issue: Course filtering not working

**Solutions:**

1. **Filter Query Debug**
   ```php
   // Debug filter queries
   function debug_course_filter_query($query_args, $filters) {
       error_log('Filter Query Args: ' . print_r($query_args, true));
       error_log('Applied Filters: ' . print_r($filters, true));
       return $query_args;
   }
   add_filter('reign_tutor_filter_query_args', 'debug_course_filter_query', 10, 2);
   ```

2. **AJAX Response Testing**
   ```javascript
   // Test AJAX filter response
   jQuery.ajax({
       url: reign_tutor_ajax.ajax_url,
       method: 'POST',
       data: {
           action: 'reign_tutor_filter_courses',
           nonce: reign_tutor_ajax.nonce,
           course_status: 'enrolled'
       },
       success: function(response) {
           console.log('Filter response:', response);
       },
       error: function(xhr, status, error) {
           console.error('Filter error:', error);
       }
   });
   ```

---

## Part 4: Context Detection Issues

### User Context Not Detected Correctly

#### Issue: Wrong courses showing for profile visitors vs owners

**Diagnostic Steps:**

1. **User Context Debug**
   ```php
   // Add debug output for context detection
   function debug_user_context($context, $profile_user_id, $current_user_id) {
       error_log("Context Debug - Detected: {$context}, Profile User: {$profile_user_id}, Current User: {$current_user_id}");
       return $context;
   }
   add_filter('reign_tutor_user_context', 'debug_user_context', 10, 3);
   ```

2. **Profile URL Analysis**
   ```php
   // Check profile URL structure
   function debug_profile_urls() {
       if (function_exists('bp_displayed_user_id')) {
           $profile_user = bp_displayed_user_id();
           $current_user = get_current_user_id();
           error_log("Profile User: {$profile_user}, Current User: {$current_user}");
       }
   }
   add_action('wp', 'debug_profile_urls');
   ```

**Solutions:**

1. **Force Context Detection**
   ```php
   // Override context detection for testing
   function force_context_detection($context, $profile_user_id, $current_user_id) {
       // Force specific context for debugging
       if ($profile_user_id === $current_user_id) {
           return 'profile_owner';
       } else {
           return 'visitor';
       }
   }
   add_filter('reign_tutor_user_context', 'force_context_detection', 999, 3);
   ```

2. **Session and Cache Issues**
   ```php
   // Clear user-related caches
   function clear_user_context_cache() {
       if (function_exists('wp_cache_delete')) {
           wp_cache_delete('user_context_' . get_current_user_id(), 'reign_tutor');
       }
   }
   add_action('wp_login', 'clear_user_context_cache');
   add_action('wp_logout', 'clear_user_context_cache');
   ```

---

## Part 5: Performance Issues

### Slow Course Loading

#### Issue: Course grids taking too long to load

**Diagnostic Steps:**

1. **Query Performance Analysis**
   ```php
   // Enable WordPress query debugging
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   define('SAVEQUERIES', true);

   // Check slow queries
   function log_slow_queries() {
       global $wpdb;
       if ($wpdb->queries) {
           foreach ($wpdb->queries as $query) {
               if ($query[1] > 0.1) { // Queries taking more than 0.1 seconds
                   error_log('Slow Query: ' . $query[0] . ' (' . $query[1] . 's)');
               }
           }
       }
   }
   add_action('wp_footer', 'log_slow_queries');
   ```

2. **Image Loading Performance**
   ```php
   // Check image sizes and optimization
   function debug_image_performance() {
       $upload_dir = wp_upload_dir();
       $total_size = 0;

       // Calculate total image sizes
       // Implementation depends on specific requirements
   }
   ```

**Solutions:**

1. **Query Optimization**
   ```php
   // Optimize course queries
   function optimize_course_queries($query_args, $shortcode_args) {
       // Add query optimization
       $query_args['no_found_rows'] = true; // Skip counting total posts if not needed
       $query_args['update_post_meta_cache'] = false; // Skip meta cache if not needed
       $query_args['update_post_term_cache'] = false; // Skip term cache if not needed

       return $query_args;
   }
   add_filter('reign_tutor_course_query_args', 'optimize_course_queries', 10, 2);
   ```

2. **Implement Caching**
   ```php
   // Add course data caching
   function cache_course_data($courses, $args) {
       $cache_key = 'reign_tutor_courses_' . md5(serialize($args));
       $cached_data = wp_cache_get($cache_key, 'reign_tutor');

       if (false === $cached_data) {
           // Cache for 15 minutes
           wp_cache_set($cache_key, $courses, 'reign_tutor', 900);
       }

       return $courses;
   }
   add_filter('reign_tutor_course_data', 'cache_course_data', 10, 2);
   ```

3. **Image Optimization**
   ```php
   // Lazy load course images
   function add_lazy_loading_to_course_images($content) {
       // Add loading="lazy" to course images
       $content = str_replace('<img ', '<img loading="lazy" ', $content);
       return $content;
   }
   add_filter('reign_tutor_course_card_content', 'add_lazy_loading_to_course_images');
   ```

---

## Part 6: Styling and Display Issues

### CSS and Layout Problems

#### Issue: Course cards not displaying correctly

**Common Causes:**
- Theme CSS conflicts
- Missing CSS files
- Responsive breakpoint issues
- Custom CSS overrides

**Solutions:**

1. **CSS Conflict Resolution**
   ```css
   /* Add CSS specificity to override theme styles */
   .reign-tutor-courses-grid .reign-tutor-course-card {
       /* Use !important sparingly */
       display: flex !important;
       flex-direction: column !important;
   }
   ```

2. **Force CSS Loading**
   ```php
   // Ensure CSS is loaded
   function force_reign_tutor_css() {
       wp_enqueue_style(
           'reign-tutor-public',
           plugin_dir_url(__FILE__) . 'assets/css/public.css',
           array(),
           '2.0.0'
       );
   }
   add_action('wp_enqueue_scripts', 'force_reign_tutor_css', 999);
   ```

3. **Mobile Responsiveness Issues**
   ```css
   /* Fix mobile layout issues */
   @media (max-width: 768px) {
       .reign-tutor-courses-grid {
           grid-template-columns: 1fr !important;
           gap: 16px !important;
       }

       .reign-tutor-course-card {
           margin-bottom: 20px !important;
       }
   }
   ```

#### Issue: Progress bars not displaying correctly

**Solutions:**

1. **Progress Bar CSS Fix**
   ```css
   /* Ensure progress bars have proper styling */
   .reign-tutor-progress-bar {
       width: 100%;
       height: 8px;
       background-color: #f0f0f0;
       border-radius: 4px;
       overflow: hidden;
       position: relative;
   }

   .reign-tutor-progress-bar .progress-fill {
       height: 100%;
       background: linear-gradient(90deg, #007cba 0%, #005a87 100%);
       transition: width 0.8s ease-in-out;
       width: 0%; /* Start at 0 and animate */
   }
   ```

2. **JavaScript Animation Fix**
   ```javascript
   // Fix progress bar animation
   function animateProgressBar(element, targetWidth) {
       jQuery(element).find('.progress-fill').animate({
           width: targetWidth + '%'
       }, 800, 'easeOutCubic');
   }
   ```

---

## Part 7: Security Issues

### Permission and Access Problems

#### Issue: Users seeing courses they shouldn't access

**Solutions:**

1. **Capability Checks**
   ```php
   // Add proper capability checks
   function check_course_access($is_visible, $course_id, $user_id, $context) {
       // Check if user has permission to view course
       if (!current_user_can('read_post', $course_id)) {
           return false;
       }

       // Check enrollment status for private courses
       if ('private' === get_post_status($course_id)) {
           if (!tutor_utils()->is_enrolled($course_id, $user_id)) {
               return false;
           }
       }

       return $is_visible;
   }
   add_filter('reign_tutor_course_visibility', 'check_course_access', 10, 4);
   ```

2. **Privacy Settings Enforcement**
   ```php
   // Enforce privacy settings
   function enforce_course_privacy($courses, $user_id, $context) {
       if ($context !== 'profile_owner') {
           // Filter out private courses for visitors
           $courses = array_filter($courses, function($course) use ($user_id) {
               $privacy = get_user_meta($course->instructor_id, 'course_privacy_setting', true);
               return ($privacy !== 'private');
           });
       }

       return $courses;
   }
   add_filter('reign_tutor_user_courses', 'enforce_course_privacy', 10, 3);
   ```

---

## Part 8: Database and Data Issues

### Data Inconsistency Problems

#### Issue: Course progress not syncing correctly

**Solutions:**

1. **Progress Data Repair**
   ```php
   // Repair progress data
   function repair_course_progress() {
       global $wpdb;

       // Get all enrollments
       $enrollments = $wpdb->get_results("
           SELECT user_id, course_id
           FROM {$wpdb->prefix}tutor_enrollments
           WHERE status = 'completed'
       ");

       foreach ($enrollments as $enrollment) {
           // Recalculate progress
           $progress = tutor_utils()->get_course_completed_percent(
               $enrollment->course_id,
               $enrollment->user_id
           );

           // Update progress meta
           update_user_meta(
               $enrollment->user_id,
               "_course_progress_{$enrollment->course_id}",
               $progress
           );
       }
   }
   ```

2. **Database Cleanup**
   ```php
   // Clean up orphaned data
   function cleanup_orphaned_course_data() {
       global $wpdb;

       // Remove progress data for deleted courses
       $wpdb->query("
           DELETE pm FROM {$wpdb->usermeta} pm
           LEFT JOIN {$wpdb->posts} p ON pm.meta_key LIKE CONCAT('_course_progress_', p.ID)
           WHERE pm.meta_key LIKE '_course_progress_%'
           AND p.ID IS NULL
       ");
   }
   ```

---

## Part 9: Common Error Messages

### Error: "Call to undefined function tutor_utils()"

**Cause:** TutorLMS plugin not loaded or activated

**Solution:**
```php
// Check TutorLMS availability before using functions
if (function_exists('tutor_utils')) {
    $courses = tutor_utils()->get_enrolled_courses_by_user($user_id);
} else {
    // Fallback or error handling
    error_log('TutorLMS plugin not available');
}
```

### Error: "Maximum execution time exceeded"

**Cause:** Large datasets or inefficient queries

**Solutions:**
1. **Increase PHP limits**
   ```php
   // In wp-config.php
   ini_set('max_execution_time', 300);
   ini_set('memory_limit', '512M');
   ```

2. **Optimize queries**
   ```php
   // Use pagination for large datasets
   $args = array(
       'posts_per_page' => 20, // Limit results
       'paged' => get_query_var('paged', 1)
   );
   ```

### Error: "Headers already sent"

**Cause:** Output before AJAX responses

**Solution:**
```php
// Ensure clean AJAX responses
function clean_ajax_response() {
    // Clear any previous output
    if (ob_get_length()) {
        ob_clean();
    }

    // Your AJAX code here
    wp_send_json_success($data);
}
```

---

## Part 10: Debugging Tools and Utilities

### Debug Mode Activation

```php
// Add to wp-config.php for debugging
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('SCRIPT_DEBUG', true);

// TutorLMS specific debugging
define('TUTOR_DEBUG', true);

// Reign TutorLMS addon debugging
define('REIGN_TUTOR_DEBUG', true);
```

### Custom Debug Functions

```php
/**
 * Debug helper functions
 */
function reign_tutor_debug($message, $data = null) {
    if (defined('REIGN_TUTOR_DEBUG') && REIGN_TUTOR_DEBUG) {
        $debug_message = '[Reign TutorLMS] ' . $message;

        if ($data !== null) {
            $debug_message .= ' | Data: ' . print_r($data, true);
        }

        error_log($debug_message);
    }
}

function reign_tutor_var_dump($var, $label = '') {
    if (defined('REIGN_TUTOR_DEBUG') && REIGN_TUTOR_DEBUG) {
        echo '<pre style="background: #f0f0f0; padding: 10px; margin: 10px; border: 1px solid #ccc;">';
        if ($label) {
            echo '<strong>' . $label . ':</strong><br>';
        }
        var_dump($var);
        echo '</pre>';
    }
}
```

---

## Emergency Recovery Procedures

### Complete Plugin Reset

If all else fails, follow these steps:

1. **Backup Database**
   ```bash
   mysqldump -u username -p database_name > backup.sql
   ```

2. **Deactivate Plugin**
   ```php
   // Via database if admin not accessible
   UPDATE wp_options
   SET option_value = ''
   WHERE option_name = 'active_plugins';
   ```

3. **Clear All Caches**
   ```php
   // Clear all WordPress caches
   wp_cache_flush();

   // Clear object cache
   if (function_exists('wp_cache_delete_group')) {
       wp_cache_delete_group('reign_tutor');
   }
   ```

4. **Reset Plugin Options**
   ```php
   // Remove plugin options
   delete_option('reign_tutor_settings');
   delete_option('reign_tutor_version');

   // Remove user meta
   delete_metadata('user', 0, '_reign_tutor_preferences', '', true);
   ```

5. **Reinstall Plugin**
   - Download fresh copy from WBcom
   - Upload and activate
   - Reconfigure settings

---

## Getting Additional Help

### Support Channels

**WBcom Support:**
- 📧 Email: support@wbcomdesigns.com
- 🎫 Support Portal: wbcomdesigns.com/support/
- 📚 Documentation: docs.wbcomdesigns.com
- 💬 Community: facebook.com/groups/wbcom

**Before Contacting Support:**

1. **Gather System Information**
   ```
   WordPress Version: ___
   TutorLMS Version: ___
   Reign Theme Version: ___
   Reign TutorLMS Addon Version: ___
   PHP Version: ___
   Active Plugins: List all active plugins
   ```

2. **Document the Issue**
   - Exact error messages
   - Steps to reproduce
   - Screenshots/screen recordings
   - Browser console errors
   - Server error logs

3. **Temporary Access**
   - Be prepared to provide temporary admin access
   - Use plugins like "Temporary Login Without Password"
   - Ensure you have recent backups

---

**Next Steps:**
- [FAQ](08-faq.md) - Frequently asked questions
- [Developer Guide](05-developer-guide.md) - Advanced customization
- [Configuration Guide](03-configuration.md) - Settings optimization

**Critical Issues:**
For urgent issues affecting live sites, contact emergency support at urgent@wbcomdesigns.com with "URGENT" in the subject line.