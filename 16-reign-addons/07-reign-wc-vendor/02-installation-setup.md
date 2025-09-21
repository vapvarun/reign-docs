# Reign WC Vendors Addon - Installation & Setup Guide

## What You'll Learn
This guide will walk you through installing and setting up the Reign WC Vendors addon for your multi-vendor marketplace. We'll make it super simple - no technical knowledge required!

## Before You Start - Quick Checklist ✅

**You'll need these installed first:**
1. ✅ WordPress (version 5.0 or higher)
2. ✅ Reign Theme (latest version)
3. ✅ WooCommerce plugin (free from WordPress.org)
4. ✅ WC Vendors Marketplace plugin (free version is fine to start)

**Also helpful to have:**
- Your purchase receipt from WBcom Designs
- About 15-20 minutes of time
- A cup of coffee ☕ (optional but recommended!)

---

## Part 1: Download Your Files

### Step 1: Get Your Files from WBcom

1. **Login to your account:**
   - Go to `wbcomdesigns.com`
   - Click "My Account" (top right)
   - Enter your email and password

2. **Find your purchase:**
   - Click "Downloads" in your account menu
   - Look for "Reign WC Vendors Addon"
   - Click the blue "Download" button

3. **Save the file:**
   - Save to your Downloads folder
   - The file will be named something like `reign-wc-vendors-addon.zip`
   - **Don't unzip it!** WordPress needs it zipped

### Step 2: Check You Have Everything

Your download should include:
- `reign-wc-vendors-addon.zip` (the main plugin)
- `license.txt` (your license key)
- `readme.txt` (quick notes)

---

## Part 2: Install the Addon

### Method 1: Easy WordPress Upload (Recommended)

1. **Go to your WordPress admin:**
   ```
   yoursite.com/wp-admin
   ```

2. **Navigate to Plugins:**
   - Click **Plugins** in the left menu
   - Click **Add New** button at the top
   - Click **Upload Plugin** button

3. **Upload your file:**
   - Click **Choose File**
   - Select `reign-wc-vendors-addon.zip`
   - Click **Install Now**
   - Wait for "Plugin installed successfully" message

4. **Activate it:**
   - Click **Activate Plugin**
   - You'll see a success message

### Method 2: Using FTP (If Upload Fails)

**When to use this:** If you get "file too large" error

1. **Unzip the file on your computer**
2. **Connect to your site via FTP**
3. **Navigate to:** `/wp-content/plugins/`
4. **Upload the entire folder:** `reign-wc-vendors-addon`
5. **Go to WordPress admin → Plugins**
6. **Find and activate** Reign WC Vendors Addon

---

## Part 3: Activate Your License

### Why License Activation Matters
- ✅ Enables automatic updates
- ✅ Access to support
- ✅ Unlock all features
- ✅ Security patches

### Steps to Activate:

1. **Find your license key:**
   - Check your email receipt
   - Or login to WBcom account → Licenses
   - Copy the long code (like: XXXX-XXXX-XXXX-XXXX)

2. **Enter in WordPress:**
   - Go to **Reign Settings** → **License**
   - Find "Reign WC Vendors Addon"
   - Paste your license key
   - Click **Activate**

3. **Confirm activation:**
   - Look for green "Active" status
   - If red, double-check the key

**License Troubleshooting:**

| Problem | Solution |
|---------|----------|
| "Invalid license" | Remove any spaces, check for typos |
| "Already in use" | Deactivate on old site first |
| "Expired" | Renew at wbcomdesigns.com |
| "Site mismatch" | Make sure URL matches (www vs non-www) |

---

## Part 4: Initial Setup Wizard

### Step 1: Run the Setup Wizard

**After activation, you'll see:**
- A notice: "Run WC Vendors Setup"
- Click **Run Setup Wizard**

**If you don't see it:**
- Go to **WC Vendors** → **Settings**
- Click **Setup Wizard** tab

### Step 2: Basic Marketplace Settings

**Page 1: Store Settings**
```
Store Name: [Your Marketplace Name]
Store URL: /vendors/ (leave default)
Vendor Role: WC Vendor (leave default)
```
Click **Next**

**Page 2: Commission Settings**
```
Default Commission: 80% (vendors keep 80%)
Who pays fees?: Vendor (recommended)
Tax handling: Vendor (they handle their taxes)
```
Click **Next**

**Page 3: Capabilities**
- ✅ Can submit products
- ✅ Can edit products
- ✅ Can manage orders
- ❌ Can edit published products (uncheck for control)

Click **Finish**

---

## Part 5: Create Essential Pages

### Automatic Page Creation

The plugin should create these pages automatically:
1. **Vendor Dashboard** - Where vendors manage their store
2. **Vendors** - List of all vendors
3. **Vendor Application** - Sign-up form for new vendors

### If Pages Weren't Created:

**Create Vendor Dashboard Page:**
1. **Pages** → **Add New**
2. Title: "Vendor Dashboard"
3. Add shortcode: `[wcv_vendor_dashboard]`
4. **Publish**

**Create Vendors List Page:**
1. **Pages** → **Add New**
2. Title: "Our Vendors"
3. Add shortcode: `[wcv_vendorslist]`
4. **Publish**

**Create Application Page:**
1. **Pages** → **Add New**
2. Title: "Become a Vendor"
3. Add shortcode: `[wcv_vendor_application]`
4. **Publish**

---

## Part 6: Connect with Reign Theme

### Enable Theme Integration

1. **Go to:** **Appearance** → **Customize**
2. **Click:** **Reign WC Vendors Settings**
3. **Toggle ON:** "Enable Reign Integration"
4. **Click:** **Publish**

### What This Does:
- ✅ Matches vendor pages to your theme design
- ✅ Adds vendor info to member profiles
- ✅ Integrates with BuddyPress (if active)
- ✅ Shows vendor badges

---

## Part 7: Configure Menu Items

### Add to Main Menu

1. **Go to:** **Appearance** → **Menus**
2. **Select your main menu**
3. **Add these pages:**
   - Our Vendors (for shoppers)
   - Become a Vendor (for recruiting)
   - Vendor Dashboard (for logged-in vendors)

### Create Vendor Menu (Optional)

**For vendor-only navigation:**
1. Create new menu called "Vendor Menu"
2. Add: Dashboard, Products, Orders, Settings
3. Assign to "Vendor Dashboard Menu" location

---

## Part 8: Test Your Setup

### Quick Test Checklist

**Test as a visitor:**
- [ ] Can you see the vendors list page?
- [ ] Can you view individual vendor stores?
- [ ] Does the application form appear?

**Test as a vendor:**
1. Create test user account
2. Apply to become vendor
3. Approve application (as admin)
4. Login as vendor
5. Check dashboard access

### How to Create Test Vendor:

1. **Create user:** **Users** → **Add New**
2. **Apply as vendor:** Visit application page, fill form
3. **Approve:** **Users** → find user → change role to "Vendor"
4. **Test login:** Use incognito/private browser window

---

## Part 9: Essential Settings to Configure

### Payment Settings

**Go to:** **WC Vendors** → **Settings** → **Payments**

```yaml
Payment Schedule: Weekly (recommended to start)
Payment Method: PayPal Adaptive Payments
Minimum Payout: $50 (prevents tiny transfers)
Hold Period: 7 days (for dispute resolution)
```

### Email Settings

**Go to:** **WooCommerce** → **Settings** → **Emails**

**Enable these vendor emails:**
- ✅ Vendor New Order
- ✅ Vendor Application
- ✅ Product Approved
- ✅ Commission Paid

### Product Settings

**Go to:** **WC Vendors** → **Settings** → **Products**

```yaml
Product Management: Vendors can manage
Product Approval: Required (you review first)
Product Types: Simple, Variable
Max Gallery Images: 8
```

---

## Part 10: Final Checks

### Security Checklist

- [ ] SSL certificate installed (https://)
- [ ] Strong admin password
- [ ] Vendor capabilities limited appropriately
- [ ] Payment test mode OFF when going live

### Performance Optimization

1. **Install caching plugin** (WP Rocket or W3 Total Cache)
2. **Optimize images** (Smush or ShortPixel)
3. **Set up CDN** (Cloudflare free plan works)

### Backup Setup

**Before going live:**
1. Install UpdraftPlus (free)
2. Set weekly backups
3. Store in cloud (Google Drive/Dropbox)

---

## Troubleshooting Common Issues

### "Plugin won't activate"

**Check these in order:**
1. Is WooCommerce active? (required)
2. Is WC Vendors active? (required)
3. Is Reign theme active? (required)
4. PHP version 7.2+? (check in Tools → Site Health)

### "Vendors can't see dashboard"

**Quick fixes:**
1. **Permalinks:** Settings → Permalinks → Save (refreshes URLs)
2. **User role:** Check user has "Vendor" role
3. **Page exists:** Verify dashboard page wasn't deleted

### "Emails not sending"

**Solution:**
1. Install "WP Mail SMTP" plugin
2. Configure with your email service
3. Send test email
4. Check spam folders

### "License won't activate"

1. **Clear license field completely**
2. **Copy fresh from email** (no spaces)
3. **Check site URL** matches license
4. **Contact support** if still failing

---

## What's Next?

### Your marketplace is installed! Now:

1. **[Configure Your Marketplace →](03-configuration.md)**
   - Set commissions
   - Configure payments
   - Set vendor limits

2. **[Customize Vendor Stores →](04-store-customization.md)**
   - Design store pages
   - Add custom fields
   - Set up widgets

3. **[Recruit Your First Vendors →](08-faq.md)**
   - Marketing strategies
   - Onboarding process
   - Support setup

---

## Quick Reference

### Important URLs After Setup

```
Vendor Dashboard: yoursite.com/vendor-dashboard/
Vendor List: yoursite.com/vendors/
Become a Vendor: yoursite.com/vendor-application/
Admin Settings: yoursite.com/wp-admin/admin.php?page=wcv-settings
```

### Default Shortcodes

| Shortcode | What It Shows | Where to Use |
|-----------|---------------|---------------|
| `[wcv_vendorslist]` | All vendors grid | Vendors page |
| `[wcv_vendor_dashboard]` | Vendor control panel | Dashboard page |
| `[wcv_vendor_application]` | Sign-up form | Application page |
| `[wcv_pro_dashboard]` | Pro dashboard (if upgraded) | Pro dashboard page |

---

**Need Help?**  
📧 Email: support@wbcomdesigns.com  
📚 Documentation: docs.wbcomdesigns.com  
💬 Community: facebook.com/groups/wbcom