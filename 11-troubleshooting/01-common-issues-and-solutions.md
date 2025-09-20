# Common Issues and Solutions

## Overview

This comprehensive guide addresses the most common issues users face with Reign theme and provides step-by-step solutions.

## Installation Issues

### Theme Won't Activate

**Error:** "The package could not be installed"

**Solutions:**
1. **Check PHP Version**
   ```
   Minimum: PHP 7.4
   Recommended: PHP 8.1+
   ```

2. **Increase Memory Limit**
   ```php
   define('WP_MEMORY_LIMIT', '256M');
   ```

3. **File Permissions**
   ```
   Folders: 755
   Files: 644
   ```

4. **Upload via FTP**
   - Extract reign-theme.zip
   - Upload to /wp-content/themes/
   - Activate from WordPress admin

### License Key Not Working

**Issue:** License key shows as invalid

**Solutions:**
1. **Verify Purchase Source**
   - Must be from WBcom Designs
   - NOT from ThemeForest
   - Check email for license key

2. **Check License Status**
   - Login to WBcom Designs account
   - Verify license is active
   - Check activation limit

3. **Clear License Cache**
   ```sql
   DELETE FROM wp_options
   WHERE option_name LIKE '%reign_license%';
   ```

## Display Issues

### Header Not Showing Correctly

**Problem:** Header layout broken or missing

**Solutions:**

1. **Verify Header Version**
   - Customize → Header → Layout
   - Select from v1, v2, v3, or v4
   - Save and refresh

2. **Clear All Caches**
   - Browser cache (Ctrl+F5)
   - Plugin cache
   - Server cache
   - CDN cache

3. **Check Menu Assignment**
   - Appearance → Menus
   - Assign to Primary Menu location
   - Save menu

4. **Disable Plugins**
   - Test with all plugins disabled
   - Enable one by one to find conflict

### Sidebar Missing or Wrong Position

**Issue:** Sidebar not displaying where expected

**Fix:**

1. **Check Global Settings**
   ```
   Customize → General → Site Layout → Sidebar Layout
   ```

2. **Page-Specific Override**
   - Edit page/post
   - Check Page Attributes
   - Select sidebar option

3. **Add Widgets**
   - Appearance → Widgets
   - Add widgets to sidebar area
   - Save and refresh

### Footer Not Appearing

**Problem:** Footer widgets or copyright missing

**Solutions:**

1. **Enable Footer**
   ```
   Customize → Footer → Enable Footer
   ```

2. **Add Footer Widgets**
   - Appearance → Widgets
   - Add to Footer Widget Areas
   - Configure widget settings

3. **Check Template**
   - Verify page template includes footer
   - Check for `get_footer()` in template

## BuddyPress Issues

### Activity Stream Not Loading

**Issue:** Blank activity stream or loading error

**Solutions:**

1. **Check Component Status**
   - Settings → BuddyPress → Components
   - Enable Activity Streams
   - Save settings

2. **Permalinks Reset**
   - Settings → Permalinks
   - Click Save Changes (don't change anything)
   - Clears rewrite rules

3. **Database Tables**
   ```sql
   -- Check if tables exist
   SHOW TABLES LIKE 'wp_bp_%';
   ```

### Member Directory Empty

**Problem:** No members showing in directory

**Fix:**

1. **Check Privacy Settings**
   - BuddyPress settings
   - Member directory visibility
   - Registration settings

2. **Sync Users**
   ```php
   // Force member sync
   bp_core_signup_user($user_id);
   ```

3. **Clear BuddyPress Cache**
   - Clear transients
   - Reset member count

### Groups Not Working

**Issue:** Can't create or view groups

**Solutions:**

1. **Enable Groups Component**
   - Settings → BuddyPress → Components
   - Check "User Groups"
   - Save changes

2. **Check Permissions**
   - Who can create groups?
   - Group creation settings
   - User capabilities

## WooCommerce Problems

### Products Not Showing

**Issue:** Shop page empty or 404

**Solutions:**

1. **Set Shop Page**
   - WooCommerce → Settings → Products
   - Select shop page
   - Save changes

2. **Flush Permalinks**
   - Settings → Permalinks
   - Save without changes

3. **Check Product Visibility**
   - Edit products
   - Check catalog visibility
   - Ensure published status

### Cart Not Updating

**Problem:** Ajax cart not working

**Fix:**

1. **Check Ajax Settings**
   ```
   WooCommerce → Settings → Products
   Enable AJAX add to cart
   ```

2. **JavaScript Errors**
   - Open browser console
   - Check for JS errors
   - Resolve conflicts

3. **Clear Cart Sessions**
   ```sql
   DELETE FROM wp_options
   WHERE option_name LIKE '_wc_session_%';
   ```

### Checkout Errors

**Issue:** Can't complete checkout

**Solutions:**

1. **SSL Certificate**
   - Ensure HTTPS is working
   - Force SSL on checkout

2. **Payment Gateway**
   - Verify gateway settings
   - Check API credentials
   - Test in sandbox mode

3. **Required Fields**
   - Check field validation
   - Ensure all required fields present

## Performance Issues

### Site Loading Slowly

**Problem:** Pages take long to load

**Solutions:**

1. **Enable Smart Performance Mode**
   ```
   Customize → General → Site Performance
   Enable all optimizations
   ```

2. **Image Optimization**
   - Compress images
   - Use WebP format
   - Enable lazy loading

3. **Plugin Audit**
   - Deactivate unused plugins
   - Use Query Monitor
   - Find slow queries

4. **Hosting Upgrade**
   - Check PHP version (8.1+)
   - Increase resources
   - Consider better hosting

### High Memory Usage

**Issue:** Memory exhausted errors

**Fix:**

1. **Increase PHP Memory**
   ```php
   define('WP_MEMORY_LIMIT', '512M');
   define('WP_MAX_MEMORY_LIMIT', '512M');
   ```

2. **Optimize Queries**
   - Limit posts per page
   - Reduce widget queries
   - Use caching

3. **Check Plugins**
   - Memory-intensive plugins
   - Deactivate and test
   - Find alternatives

## Styling Problems

### Custom CSS Not Working

**Issue:** CSS changes not appearing

**Solutions:**

1. **Specificity Issues**
   ```css
   /* Use more specific selectors */
   body .site-header .logo {
       /* styles */
   }

   /* Or use !important sparingly */
   .logo {
       color: red !important;
   }
   ```

2. **Cache Issues**
   - Clear all caches
   - Hard refresh (Ctrl+F5)
   - Check CDN cache

3. **Syntax Errors**
   - Validate CSS
   - Check for typos
   - Use browser inspector

### Colors Not Changing

**Problem:** Color settings not applying

**Fix:**

1. **Check Priority**
   - Child theme CSS
   - Plugin styles
   - Inline styles

2. **Clear Customizer Cache**
   ```sql
   DELETE FROM wp_options
   WHERE option_name LIKE 'theme_mods_%';
   ```

3. **Regenerate CSS**
   - Save Customizer settings
   - Clear cache
   - Check file permissions

## Mobile Issues

### Mobile Menu Not Working

**Issue:** Hamburger menu not opening

**Solutions:**

1. **Check JavaScript**
   - Console errors
   - jQuery conflicts
   - Script loading order

2. **Menu Assignment**
   - Appearance → Menus
   - Mobile Menu location
   - Separate mobile menu

3. **CSS Conflicts**
   ```css
   /* Force display */
   .mobile-menu {
       display: block !important;
       z-index: 99999;
   }
   ```

### Responsive Layout Broken

**Problem:** Layout not adapting to screen size

**Fix:**

1. **Viewport Meta Tag**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1">
   ```

2. **CSS Media Queries**
   - Check breakpoints
   - Test all screen sizes
   - Update responsive CSS

3. **Disable Desktop Mode**
   - Mobile browser settings
   - Request mobile site

## Update Issues

### Can't Update Theme

**Issue:** Update notification but can't update

**Solutions:**

1. **Activate License**
   - Reign Settings → License
   - Enter valid license key
   - Activate license

2. **Manual Update**
   - Download latest version
   - Upload via FTP
   - Or use WordPress updater

3. **Check Permissions**
   - File/folder permissions
   - WordPress file ownership
   - FTP credentials

### Lost Customizations After Update

**Problem:** Settings reset after update

**Fix:**

1. **Use Child Theme**
   - Download child theme
   - Activate child theme
   - Move customizations

2. **Backup Settings**
   ```sql
   -- Backup customizer settings
   SELECT * FROM wp_options
   WHERE option_name LIKE 'theme_mods_%';
   ```

3. **Export/Import**
   - Use Customizer export plugin
   - Save settings before update
   - Import after update

## Debug Mode

### Enable WordPress Debug

**Add to wp-config.php:**
```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('SCRIPT_DEBUG', true);
```

### Check Error Logs

**Locations:**
- `/wp-content/debug.log`
- Server error logs
- PHP error logs
- Browser console

## Getting Help

### Before Contacting Support

1. **Check Documentation**
   - Read relevant guides
   - Search documentation
   - Check FAQs

2. **Test Basic Solutions**
   - Clear cache
   - Disable plugins
   - Switch to default theme

3. **Gather Information**
   - WordPress version
   - Theme version
   - PHP version
   - Error messages
   - Steps to reproduce

### Contact Support

**Support Channels:**
- **Support Portal:** WBcom Designs account
- **Documentation:** https://docs.wbcomdesigns.com
- **Community:** Facebook group
- **Email:** support@wbcomdesigns.com

**Include in Support Request:**
- License key
- Site URL
- Issue description
- Screenshots
- Error messages
- What you've tried