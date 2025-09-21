# Reign WCFM Addon - Troubleshooting Guide

## How to Use This Guide
Find your issue below and follow the step-by-step solutions. Each solution starts with the easiest fix and progresses to more advanced options.

---

## 🔴 Installation Issues

### "Plugin won't activate"

**What's happening:** You see an error when trying to activate the addon.

**Solution 1: Check Requirements**
1. Go to **Plugins** page
2. Make sure these are active:
   - ✅ Reign Theme
   - ✅ WooCommerce
   - ✅ WCFM Marketplace
3. Try activating again

**Solution 2: Check PHP Version**
1. Go to **Tools** → **Site Health** → **Info** → **Server**
2. Look for PHP version (needs 7.4 or higher)
3. If lower, contact your host to upgrade

**Solution 3: Check Error Log**
1. Add this to wp-config.php:
   ```php
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   ```
2. Try activating again
3. Check `/wp-content/debug.log` for errors
4. Share error with support

### "License key not working"

**What's happening:** Your license key is rejected.

**Solution 1: Check Key Format**
- Remove spaces before/after key
- Copy directly from WBcom account
- Don't include quotes or brackets

**Solution 2: Check Site URL**
1. Is this a new domain? Deactivate on old site first
2. Using staging? May need separate license
3. Changed from http to https? Update in WBcom account

**Solution 3: Reset License**
1. Login to wbcomdesigns.com
2. Go to **My Account** → **Licenses**
3. Click **Deactivate** for all sites
4. Try activating on your site again

---

## 🛍️ Store Display Problems

### "Stores not showing up"

**What's happening:** Store listing page is empty or shows error.

**Solution 1: Check Page Setup**
1. Go to **Pages**
2. Find "Store List" page
3. Make sure it contains: `[wcfm_stores]`
4. Publish/Update the page

**Solution 2: Reset Permalinks**
1. Go to **Settings** → **Permalinks**
2. Don't change anything
3. Just click **Save Changes**
4. This refreshes URL structure

**Solution 3: Check Vendor Status**
1. Go to **WCFM** → **Vendors**
2. Are vendors "Approved"?
3. Click **Edit** on vendor
4. Set status to "Active"

### "Store layout looks broken"

**What's happening:** Stores display but look messy.

**Solution 1: Clear All Caches**
```
Browser: Ctrl+F5 (PC) or Cmd+Shift+R (Mac)
Plugin: WP Rocket/W3 Total Cache → Clear Cache
CDN: CloudFlare → Purge Cache
Host: Contact host to clear server cache
```

**Solution 2: Regenerate CSS**
1. Go to **Appearance** → **Customize**
2. Make any small change (like a color)
3. Click **Publish**
4. Change it back and **Publish** again

**Solution 3: Check for Plugin Conflicts**
1. Deactivate all plugins except:
   - WooCommerce
   - WCFM
   - Reign WCFM
2. Check if fixed
3. Reactivate plugins one by one
4. Find the conflicting plugin

### "Store images not loading"

**What's happening:** Broken image icons or missing banners.

**Solution 1: Check Image Sizes**
- Banner: 1920x400px or 1200x300px
- Logo: 150x150px
- Format: JPG or PNG
- Size: Under 2MB each

**Solution 2: Check Upload Permissions**
1. Vendor goes to **Dashboard** → **Store Settings**
2. Can they see upload buttons?
3. If not, go to **WCFM** → **Capability**
4. Enable "Upload Files" for vendors

**Solution 3: Regenerate Thumbnails**
1. Install "Regenerate Thumbnails" plugin
2. Go to **Tools** → **Regenerate Thumbnails**
3. Click **Regenerate All**

---

## 👥 Vendor Dashboard Issues

### "Vendors can't access dashboard"

**What's happening:** Vendors get error or redirect when trying to access dashboard.

**Solution 1: Check User Role**
1. Go to **Users**
2. Click on vendor's name
3. Look for "Role"
4. Should be "Vendor" or "Store Vendor"
5. If not, change and save

**Solution 2: Check Dashboard Page**
1. Go to **WCFM** → **Settings** → **Dashboard**
2. Is dashboard page selected?
3. Does page exist and published?
4. Does it have `[wcfm_vendor_dashboard]` shortcode?

**Solution 3: Reset Vendor Permissions**
```php
// Add to functions.php temporarily
add_action('init', function() {
    $user = wp_get_current_user();
    if (in_array('wcfm_vendor', $user->roles)) {
        $user->add_cap('access_wcfm_vendor_dashboard');
    }
});
```

### "Dashboard menu items missing"

**What's happening:** Vendors can't see all menu options.

**Solution 1: Check Capabilities**
1. Go to **WCFM** → **Capability**
2. Click on **Vendor** tab
3. Check boxes for menu items you want
4. Save changes

**Solution 2: Check Membership Level**
1. Using WCFM Membership?
2. Go to **WCFM** → **Memberships**
3. Edit vendor's membership plan
4. Enable required features

### "Dashboard very slow"

**What's happening:** Dashboard takes forever to load.

**Solution 1: Reduce Dashboard Widgets**
1. Vendor clicks **Screen Options** (top right)
2. Uncheck unnecessary widgets
3. Reduce date range in reports

**Solution 2: Optimize Database**
1. Install "WP-Optimize" plugin
2. Run database cleanup
3. Optimize tables

---

## 💰 Commission & Payment Issues

### "Commissions not calculating"

**What's happening:** Orders complete but no commission appears.

**Solution 1: Check Commission Settings**
1. Go to **WCFM** → **Settings** → **Commission**
2. Is commission enabled?
3. Set commission type (%, fixed, etc.)
4. Save settings

**Solution 2: Check Order Status**
1. Commissions only calculate on "Completed" orders
2. Go to **WooCommerce** → **Orders**
3. Change order status to "Completed"
4. Check if commission appears

**Solution 3: Recalculate Commission**
```php
// Run once to recalculate
add_action('init', function() {
    if (isset($_GET['recalc_commission'])) {
        $order_id = $_GET['order_id'];
        do_action('wcfmmp_order_status_completed', $order_id);
        echo 'Commission recalculated for order ' . $order_id;
        exit;
    }
});
// Visit: yoursite.com?recalc_commission=1&order_id=123
```

### "Vendors can't withdraw money"

**What's happening:** Withdrawal button missing or not working.

**Solution 1: Check Minimum Threshold**
1. Go to **WCFM** → **Settings** → **Withdrawal**
2. Check minimum withdrawal amount
3. Make sure vendor has enough balance

**Solution 2: Check Payment Methods**
1. Same location as above
2. Is at least one payment method enabled?
3. Common options: PayPal, Bank Transfer, Stripe

**Solution 3: Check Vendor Payment Settings**
1. Vendor goes to **Dashboard** → **Payment**
2. Have they set up payment details?
3. For PayPal: Need email
4. For Bank: Need account details

---

## 📧 Email Issues

### "Vendors not receiving emails"

**What's happening:** Order notifications not reaching vendors.

**Solution 1: Check Email Settings**
1. Go to **WCFM** → **Settings** → **Email**
2. Is "New Order" email enabled for vendors?
3. Check email template is not empty

**Solution 2: Install SMTP Plugin**
1. Install "WP Mail SMTP" plugin
2. Configure with your email service:
   - Gmail
   - SendGrid
   - Mailgun
3. Send test email

**Solution 3: Check Spam Folder**
- Tell vendors to check spam
- Add your domain to whitelist
- Use professional email (not free gmail for sending)

---

## 🎨 Styling Issues

### "Colors not matching theme"

**What's happening:** WCFM uses different colors than your site.

**Solution 1: Use Customizer**
1. **Appearance** → **Customize** → **WCFM Colors**
2. Match colors to your theme
3. Click **Publish**

**Solution 2: Use WCFM Colorizer**
1. **WCFM** → **Settings** → **Dashboard Colorizer**
2. Set dashboard colors
3. Save changes

**Solution 3: Add Custom CSS**
```css
/* Add to Customizer > Additional CSS */
.wcfm_header_panel {
    background: #your-color !important;
}
.wcfm_menu_item {
    color: #your-color !important;
}
```

### "Mobile view not working"

**What's happening:** Site not responsive on phones.

**Solution 1: Check Mobile Settings**
1. **Appearance** → **Customize** → **Mobile Settings**
2. Enable "Responsive Mode"
3. Save and check

**Solution 2: Check Theme Support**
1. Does Reign theme have updates?
2. Update theme and addon
3. Clear all caches

---

## 🔍 Search & Filter Problems

### "Store search not working"

**What's happening:** Search returns no results or wrong results.

**Solution 1: Rebuild Search Index**
1. Go to **WCFM** → **Settings** → **Store**
2. Save settings without changes
3. This rebuilds search data

**Solution 2: Check Search Settings**
```php
// Add to functions.php
add_filter('wcfmmp_stores_query_args', function($args) {
    // Enable search in store name and description
    $args['search_columns'] = array('user_login', 'user_nicename', 'display_name');
    return $args;
});
```

### "Filters not applying"

**What's happening:** Category/location filters don't work.

**Solution 1: Check AJAX**
1. Open browser console (F12)
2. Try using filter
3. Look for red errors
4. Share errors with support

**Solution 2: Disable Cache for Store Page**
1. In caching plugin, exclude:
   - /store/*
   - /stores/*
   - /vendor/*

---

## ⚠️ Error Messages Explained

### Common Errors and What They Mean

| Error Message | What It Means | Quick Fix |
|--------------|---------------|----------|
| "Invalid vendor" | User isn't a vendor | Check user role |
| "Permission denied" | Capability issue | Check WCFM Capability settings |
| "Store not found" | URL issue | Reset permalinks |
| "Commission error" | Calculation failed | Check commission settings |
| "Upload failed" | File too large or wrong type | Check upload settings |
| "Payment gateway error" | Payment setup issue | Check payment configuration |

---

## 🆘 Emergency Fixes

### "Everything is broken!"

**The Nuclear Option - Complete Reset:**

1. **Backup everything first!**
2. Deactivate all plugins
3. Switch to default theme
4. Reactivate only:
   - WooCommerce
   - WCFM
   - Reign theme
   - Reign WCFM
5. Test basic functionality
6. Gradually add back other plugins

### "White screen of death"

**Recovery Steps:**

1. **Via FTP/File Manager:**
   ```
   Rename: /plugins/reign-wcfm-addon/
   To: /plugins/reign-wcfm-addon-disabled/
   ```

2. **Enable Debug:**
   ```php
   // In wp-config.php
   define('WP_DEBUG', true);
   define('WP_DEBUG_DISPLAY', true);
   ```

3. **Check error and fix**

4. **Rename back when fixed**

---

## 📞 Getting Help

### Before Contacting Support

**Gather This Information:**
1. WordPress version
2. Theme version
3. WCFM version
4. PHP version
5. Error messages (exact text)
6. When did it start?
7. What changed recently?

**Try These First:**
1. Clear all caches
2. Update all plugins
3. Check for conflicts
4. Read this guide

### Contact Support

**How to Get Fast Help:**

1. **Email Template:**
   ```
   Subject: [WCFM Addon] Brief description of issue
   
   License Key: XXXX-XXXX-XXXX
   Site URL: yoursite.com
   
   Issue: Describe what's wrong
   Steps taken: What you've tried
   Error message: Exact text
   
   Attached: Screenshots
   ```

2. **Where to Contact:**
   - Email: support@wbcomdesigns.com
   - Forum: wbcomdesigns.com/support
   - Priority: With valid license

---

## ✅ Prevention Tips

### Keep Things Running Smoothly

1. **Regular Updates**
   - Update weekly
   - Test on staging first
   - Keep backups

2. **Monitor Performance**
   - Check site speed
   - Watch error logs
   - Monitor vendor feedback

3. **Best Practices**
   - Don't modify plugin files
   - Use child theme
   - Document customizations
   - Regular backups

---

**Still stuck?** Don't worry! Contact support with your issue details and we'll help you get sorted.