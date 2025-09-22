# Reign Dokan Addon - Troubleshooting Guide

## 🆘 Quick Fix Your Marketplace Issues

Don't worry! Most issues can be fixed in minutes. This guide helps you solve common problems quickly without needing technical support. We'll walk through solutions step-by-step.

---

## 🔴 Installation Problems

### "Plugin Won't Activate" Error

**What you see:**
```
Plugin could not be activated because it triggered a fatal error.
```

**Quick Fix (90% Success Rate):**

1. **✅ Check Your Setup**
   - Is Reign Theme active? (Not just installed)
   - Is Dokan plugin activated?
   - Is WooCommerce running?

   **Missing something?** Install in this order: WooCommerce → Dokan → Reign Theme → Reign Dokan Addon

2. **Enable Debug Mode**
   ```php
   // In wp-config.php
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   define('WP_DEBUG_DISPLAY', false);
   ```

3. **Check Error Log**
   ```
   /wp-content/debug.log
   ```

### Issue: License Activation (If Applicable)

If using a licensed version:

1. **Verify License Key**
   - Login to WBcom Designs account
   - Copy exact license key
   - Remove any spaces

2. **Contact Support**
   - Email: support@wbcomdesigns.com
   - Include order ID and site URL

---

## 🔍 Display & Layout Issues

### Shortcodes Show as Text (Not Working)

**What's happening:**
- You see `[rda_dokan_vendors]` as plain text
- Vendor listings don't appear
- Pages show shortcode instead of content

**5-Minute Fix:**

1. **🔌 Check Plugin Status**
   - Go to Plugins page
   - Look for "Reign Dokan Addon"
   - Make sure it says "Deactivate" (meaning it's active)

2. **👥 Verify You Have Vendors**
   - Go to Dokan → Vendors
   - Do you have at least 1 approved vendor?
   - No vendors = Nothing to display!

3. **🧪 Test with Simple Shortcode**
   ```
   [rda_dokan_vendors]
   ```
   If this works, your other shortcodes will too!

### Store Pages Look Plain/Ugly

**What's wrong:**
- Vendor stores don't have beautiful Reign design
- Headers missing or plain
- Layout looks like basic Dokan

**Quick Solutions:**

1. **🧹 Clear All Caches (Fixes 70% of Issues)**
   - Browser: Press `Ctrl+F5` (Windows) or `Cmd+Shift+R` (Mac)
   - WordPress: Deactivate cache plugins temporarily
   - Hosting: Clear server cache in hosting panel

2. **Verify Theme Active**
   ```php
   $theme = wp_get_theme();
   echo $theme->get('Name'); // Should be "Reign"
   ```

3. **Check Template Loading**
   ```php
   // Add to functions.php temporarily for debugging
   add_filter('dokan_locate_template', function($template, $name) {
       error_log('Loading template: ' . $name . ' from: ' . $template);
       return $template;
   }, 10, 2);
   ```

### Issue: Settings Not Applying

**Symptoms:**
- Customizer changes not visible
- Store header not showing despite settings

**Solutions:**

1. **Save Settings Again**
   - Go to Appearance → Customize → Dokan Settings
   - Make any change and click "Publish"

2. **Check Setting Values**
   ```php
   // Check if settings are saved
   $header_enabled = get_theme_mod('reign_dokan_store_header_location');
   var_dump($header_enabled);
   ```

3. **Clear Customizer Cache**
   - Visit Appearance → Customize
   - Click "Publish" without making changes

## BuddyPress Integration Issues

### Issue: Store Tab Not Showing in Profiles

**Symptoms:**
- BuddyPress profiles missing store tab
- Vendor features not visible

**Solutions:**

1. **Verify BuddyPress is Active**
   - Check Plugins page
   - Ensure BuddyPress is activated

2. **Check User is Vendor**
   ```php
   $user_id = bp_displayed_user_id();
   $is_seller = get_user_meta($user_id, 'dokan_enable_selling', true);
   var_dump($is_seller); // Should be 'yes'
   ```

3. **Clear BuddyPress Cache**
   - Clear all caches
   - Visit Settings → Permalinks → Save

### Issue: Favorite Products Not Working

**Solutions:**

1. **Check BuddyPress Active**
2. **Verify User is Logged In**
3. **Clear Browser Cache**

## Performance Issues

### Issue: Slow Store Loading

**Solutions:**

1. **Use Caching Plugin**
   - Install WP Rocket, W3 Total Cache, or similar
   - Configure page caching

2. **Optimize Images**
   - Compress store banners and product images
   - Use appropriate image sizes

3. **Limit Shortcode Results**
   ```
   [rda_dokan_vendors count="6"]  // Instead of high numbers
   [rda_dokan_store_listing per_page="12"]  // Reasonable pagination
   ```

### Issue: Memory Issues

**Solutions:**

1. **Check Memory Limit**
   ```php
   echo 'Memory limit: ' . ini_get('memory_limit');
   echo 'Peak usage: ' . number_format(memory_get_peak_usage() / 1024 / 1024, 2) . ' MB';
   ```

2. **Increase Memory (if needed)**
   ```php
   // In wp-config.php
   define('WP_MEMORY_LIMIT', '256M');
   ```

## Plugin Conflicts

### Issue: Conflict with Other Plugins

**Common Conflicts:**
- Cache plugins
- Security plugins
- Other marketplace plugins
- Page builders

**Solutions:**

1. **Test Plugin Conflicts**
   - Deactivate all non-essential plugins
   - Test if issue resolves
   - Reactivate plugins one by one to identify conflict

2. **Common Conflict Fixes**
   - Exclude store pages from cache
   - Whitelist Dokan endpoints in security plugins
   - Check for duplicate marketplace functionality

## Debug and Diagnostics

### Enable Debug Mode

```php
// In wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

### Check Plugin Status

```php
// Verify addon is loaded
if (function_exists('reign_dokan_addon')) {
    echo 'Reign Dokan Addon is loaded';
} else {
    echo 'Addon not found';
}
```

### Test Shortcode Registration

```php
// Check if shortcodes are registered
global $shortcode_tags;
var_dump(isset($shortcode_tags['rda_dokan_vendors']));
var_dump(isset($shortcode_tags['rda_dokan_store_listing']));
```

## Getting Help

### Before Contacting Support

1. **Gather Information**
   - WordPress version
   - Reign theme version
   - Dokan version
   - Plugin version
   - Error messages (if any)

2. **Test Basic Functionality**
   - Try shortcodes on test page
   - Check if Dokan works without addon
   - Verify theme settings are accessible

### Contact Support

**Support Channels:**
- Email: support@wbcomdesigns.com
- Include detailed description of issue
- Provide steps to reproduce
- Share relevant error messages

## Quick Reference

### Essential Checks
1. ✅ Reign Theme active
2. ✅ Dokan installed and configured
3. ✅ WooCommerce active
4. ✅ Reign Dokan Addon activated
5. ✅ Test shortcodes work
6. ✅ Settings accessible in Customizer

### Quick Fixes
- Clear all caches
- Resave permalinks
- Republish Customizer settings
- Deactivate/reactivate plugin

## Next Steps

- [FAQ](08-faq.md) - Frequently asked questions
- [Developer Guide](05-developer-guide.md) - Advanced customization
- [Configuration Guide](03-configuration.md) - Settings reference

---

*Troubleshooting guide verified against Reign Dokan Addon v3.5.4*