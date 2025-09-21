# Reign WC Vendors Addon - Troubleshooting Guide

## How to Use This Guide
Find your issue below and follow the solutions step by step. We start with the easiest fixes first, then move to more advanced solutions.

---

## 🔴 Critical Issues

### "Plugin won't activate at all"

**Error: "Plugin could not be activated because it triggered a fatal error"**

**Solution 1: Check Requirements**
```
Required:
✅ PHP 7.2 or higher
✅ WordPress 5.0+
✅ WooCommerce 3.0+
✅ WC Vendors (free version)
✅ Reign Theme
```

How to check:
1. Go to **Tools** → **Site Health** → **Info**
2. Check PHP version under "Server"
3. Check WordPress version under "WordPress"

**Solution 2: Check Plugin Order**

Activate in this exact order:
1. WooCommerce
2. WC Vendors Marketplace
3. Reign Theme
4. Reign WC Vendors Addon

**Solution 3: Check Error Log**
```php
// Add to wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```
Then check `/wp-content/debug.log`

---

### "White screen after activation"

**Emergency Recovery:**

1. **Via FTP/File Manager:**
   - Navigate to `/wp-content/plugins/`
   - Rename `reign-wc-vendors/` to `reign-wc-vendors-disabled/`
   - Site should load now
   
2. **Find the issue:**
   - Check error log
   - Increase PHP memory limit
   - Disable other plugins one by one

3. **Fix memory issues:**
```php
// Add to wp-config.php
define('WP_MEMORY_LIMIT', '256M');
define('WP_MAX_MEMORY_LIMIT', '512M');
```

---

## 🛍️ Vendor Store Issues

### "Vendor stores show 404 error"

**Solution 1: Refresh Permalinks**
1. Go to **Settings** → **Permalinks**
2. Don't change anything
3. Click **Save Changes**
4. Test vendor stores again

**Solution 2: Check Store Base URL**
1. Go to **WC Vendors** → **Settings** → **Display**
2. Look for "Vendor Store URL Base"
3. Should be something like: `vendors` or `stores`
4. Save and refresh permalinks again

**Solution 3: Check .htaccess**
```apache
# Should contain:
<IfModule mod_rewrite.c>
RewriteEngine On
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
</IfModule>
```

---

### "Store layout looks broken"

**Solution 1: Clear All Caches**
```
1. Browser: Ctrl+F5 (Windows) or Cmd+Shift+R (Mac)
2. Plugin cache: WP Rocket/W3 Total Cache → Clear Cache
3. CDN: Cloudflare → Purge Everything
4. Theme cache: Appearance → Customize → Publish
```

**Solution 2: Check Theme Compatibility**
1. Temporarily switch to Reign parent theme
2. If it works, issue is in child theme
3. Check child theme's functions.php for conflicts

**Solution 3: Regenerate CSS**
1. Go to **Appearance** → **Customize**
2. Change any color slightly
3. **Publish**
4. Change it back
5. **Publish** again

---

### "Vendor products not showing"

**Solution 1: Check Product Status**
1. Go to **Products** → **All Products**
2. Filter by vendor (top dropdown)
3. Check if products are "Published"
4. Not "Draft" or "Pending Review"

**Solution 2: Check Vendor Permissions**
1. Go to **WC Vendors** → **Settings** → **Capabilities**
2. Ensure vendors can:
   - ✅ Submit products
   - ✅ Edit products
   - ✅ Publish products (if trusted)

**Solution 3: Check Product Visibility**
```sql
-- Run this query to check hidden products
SELECT post_title, post_status, post_author 
FROM wp_posts 
WHERE post_type = 'product' 
AND post_author = [vendor_user_id];
```

---

## 👥 Vendor Dashboard Problems

### "Vendors can't access dashboard"

**Solution 1: Check User Role**
1. Go to **Users** → Find vendor
2. Click **Edit**
3. Role should be "Vendor" or "Pending Vendor"
4. If not, change it and **Update User**

**Solution 2: Check Dashboard Page**
1. Go to **Pages**
2. Find "Vendor Dashboard" page
3. Make sure it contains: `[wcv_vendor_dashboard]`
4. Make sure it's **Published**
5. Check URL matches settings

**Solution 3: Fix Capabilities**
```php
// Temporarily add to functions.php
add_action('init', function() {
    $role = get_role('vendor');
    if ($role) {
        $role->add_cap('read');
        $role->add_cap('edit_products');
        $role->add_cap('delete_products');
        $role->add_cap('manage_product');
        $role->add_cap('view_woocommerce_reports');
    }
});
```

---

### "Dashboard showing wrong data"

**Solution 1: Clear Transients**
```php
// Run once via functions.php
add_action('init', function() {
    if (isset($_GET['clear_vendor_cache'])) {
        global $wpdb;
        $wpdb->query("DELETE FROM {$wpdb->options} WHERE option_name LIKE '_transient_wcv_%'");
        echo 'Vendor cache cleared';
        exit;
    }
});
// Then visit: yoursite.com?clear_vendor_cache=1
```

**Solution 2: Recalculate Stats**
1. Go to **WooCommerce** → **Status** → **Tools**
2. Run "Regenerate product lookup tables"
3. Run "Clear transients"

---

## 💰 Commission & Payment Issues

### "Commissions not calculating"

**Solution 1: Check Settings**
1. Go to **WC Vendors** → **Settings** → **Commission**
2. Make sure commission is set (not 0%)
3. Check "Commission Type" is selected
4. Save settings

**Solution 2: Check Order Status**
- Commissions only calculate on "Completed" orders
- Not on "Processing" or "Pending"
- Complete a test order to verify

**Solution 3: Manually Trigger**
```php
// Force commission calculation
add_action('init', function() {
    if (isset($_GET['calc_commission']) && isset($_GET['order_id'])) {
        $order_id = intval($_GET['order_id']);
        WCV_Commission::calculate_commission($order_id);
        echo 'Commission calculated for order ' . $order_id;
        exit;
    }
});
// Visit: yoursite.com?calc_commission=1&order_id=123
```

---

### "Vendors can't withdraw funds"

**Solution 1: Check Minimum Amount**
1. Go to **WC Vendors** → **Settings** → **Payments**
2. Check "Minimum Payment Amount"
3. Make sure vendor balance exceeds this

**Solution 2: Check Payment Schedule**
- Is it set to "Manual"?
- When was last payment run?
- Are there pending payments?

**Solution 3: Check Payment Method**
1. Vendor must set up payment method
2. Go to dashboard → **Payment** tab
3. Enter PayPal email or bank details

---

## 📧 Email Issues

### "Vendor emails not sending"

**Solution 1: Check Email Settings**
1. Go to **WooCommerce** → **Settings** → **Emails**
2. Make sure vendor emails are enabled:
   - ✅ Vendor New Order
   - ✅ Vendor Approval
   - ✅ Vendor Application

**Solution 2: Install SMTP Plugin**
1. Install "WP Mail SMTP" or "Post SMTP"
2. Configure with email service:
   - Gmail
   - SendGrid  
   - Mailgun
3. Send test email

**Solution 3: Check Spam**
- Check spam/junk folder
- Add sender to contacts
- Use professional email domain

---

## 🎨 Display & Styling Issues

### "Vendor pages don't match theme"

**Solution 1: Enable Integration**
1. Go to **Appearance** → **Customize**
2. Find **Reign WC Vendors Settings**
3. Enable "Theme Integration"
4. **Publish**

**Solution 2: Copy Templates**
1. Copy from: `/plugins/wc-vendors/templates/`
2. Paste to: `/themes/reign-child/wc-vendors/`
3. Edit templates to match theme

**Solution 3: Add Compatibility CSS**
```css
/* Add to Customizer → Additional CSS */
.wcv-vendor-header {
    background: var(--reign-primary-color);
}

.wcv-dashboard-wrapper {
    max-width: var(--reign-container-width);
    margin: 0 auto;
}

.wcv-navigation {
    font-family: var(--reign-font-family);
}
```

---

### "Mobile view not working"

**Solution 1: Check Responsive Settings**
1. **Appearance** → **Customize** → **WC Vendors** → **Mobile**
2. Enable "Responsive Layout"
3. Set "Mobile Columns" to 1 or 2

**Solution 2: Fix Viewport Meta**
```html
<!-- Should be in header.php -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Solution 3: Add Mobile CSS**
```css
@media (max-width: 768px) {
    .wcv-grid {
        grid-template-columns: 1fr !important;
    }
    
    .vendor-card {
        width: 100% !important;
    }
}
```

---

## ⚠️ Common Error Messages

### Error Dictionary

| Error Message | Meaning | Fix |
|--------------|---------|-----|
| "Invalid vendor" | User isn't vendor role | Change user role to Vendor |
| "No payment method" | PayPal/Bank not set | Vendor must add payment details |
| "Capability denied" | Missing permission | Check WC Vendors → Capabilities |
| "Store not found" | URL/Permalink issue | Reset permalinks |
| "Commission error" | Calculation failed | Check commission settings |
| "Theme incompatible" | Wrong theme active | Activate Reign theme |

---

## 🔧 Advanced Debugging

### Enable Debug Mode

```php
// Add all to wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', true);
define('SCRIPT_DEBUG', true);
define('SAVEQUERIES', true);
```

### Check Database Tables

```sql
-- Check if vendor tables exist
SHOW TABLES LIKE '%wcv%';

-- Should see:
-- wp_wcv_commissions
-- wp_wcv_commission_meta
-- Maybe others
```

### Test User Capabilities

```php
// Check what vendor can do
$user = wp_get_current_user();
if (in_array('vendor', $user->roles)) {
    echo '<pre>';
    print_r($user->allcaps);
    echo '</pre>';
}
```

---

## 🎯 Quick Fixes Checklist

### Try These First (in order):

1. [ ] Clear all caches
2. [ ] Reset permalinks  
3. [ ] Update all plugins
4. [ ] Switch to parent theme
5. [ ] Deactivate other plugins
6. [ ] Check PHP error log
7. [ ] Increase memory limit
8. [ ] Re-save settings
9. [ ] Check user permissions
10. [ ] Test with default WordPress theme

---

## 🔄 Reset Procedures

### Complete Vendor Reset

**Warning: Backs up data first!**

```php
// Reset all vendor data
function reset_vendor_data($vendor_id) {
    // Clear user meta
    $meta_keys = array(
        'wcv_vendor_approved',
        'wcv_vendor_application',
        'pv_shop_name',
        'pv_shop_description'
    );
    
    foreach ($meta_keys as $key) {
        delete_user_meta($vendor_id, $key);
    }
    
    // Reset role
    $user = new WP_User($vendor_id);
    $user->set_role('customer');
    
    // Then re-apply as vendor
    $user->add_role('vendor');
}
```

### Clear All WC Vendors Data

```sql
-- BACKUP FIRST!
-- Remove all vendor data
DELETE FROM wp_usermeta WHERE meta_key LIKE 'wcv_%';
DELETE FROM wp_usermeta WHERE meta_key LIKE 'pv_%';
TRUNCATE TABLE wp_wcv_commissions;
```

---

## 📞 Getting Support

### Before Contacting Support

**Gather this information:**
1. WordPress version
2. WooCommerce version  
3. WC Vendors version
4. Reign theme version
5. PHP version
6. Error messages (exact text)
7. When problem started
8. Recent changes made

### Support Template

```
Subject: [WC Vendors Issue] Brief description

Environment:
- WordPress: [version]
- WooCommerce: [version]
- WC Vendors: [version]
- Reign Theme: [version]
- PHP: [version]

Issue:
[Describe what's wrong]

Steps to reproduce:
1. [First step]
2. [Second step]
3. [What happens]

What I've tried:
- [Solution 1]
- [Solution 2]

Error message:
[Paste exact error]

Screenshots attached: Yes/No
```

### Contact Support

- 📧 Email: support@wbcomdesigns.com
- 🌐 Forum: wbcomdesigns.com/support
- 📝 Ticket: Open from your account
- ⏱️ Response: 24-48 hours

---

## 💡 Prevention Tips

### Avoid Future Issues

1. **Always backup before updates**
2. **Test on staging site first**
3. **Update plugins one at a time**
4. **Check changelog before updating**
5. **Monitor error logs regularly**
6. **Keep PHP version current**
7. **Don't modify core plugin files**
8. **Use child theme for customizations**

---

**Still Having Issues?**

Don't worry! Our support team is here to help. Contact us with your issue details and we'll get you sorted out quickly.

🌟 Remember: Most issues have simple solutions. Stay calm and work through the steps!