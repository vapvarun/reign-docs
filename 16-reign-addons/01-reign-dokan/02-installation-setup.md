# Reign Dokan Addon - Complete Installation & Setup Guide

## 🏗️ Building Your Marketplace Foundation

This guide walks you through installing and setting up your Reign Dokan Addon step-by-step. By the end, you'll have a fully functional marketplace with beautiful vendor stores and professional features.

## 📋 Before You Start (Requirements Check)

### ✅ Required Components (Must Have These First)
1. **WordPress** 4.0 or higher *(Most hosting providers have this)*
2. **Reign Theme** activated *(Your marketplace's beautiful foundation)*
3. **WooCommerce** plugin active *(Handles payments and orders)*
4. **Dokan Plugin** installed *(Free or Pro version - the marketplace engine)*

### 🎁 Optional Components (Nice to Have)
- **BuddyPress** - Adds social marketplace features and vendor profiles
- **WBcom License** - For automatic updates and premium support

*Missing something? Links to get everything are provided below!*

---

## 🚀 Installation Process (15 minutes)

### Step 1: Get Your Addon (5 minutes)

**Option A: Download from WBcom Account**
1. **Login to** [WBcom Designs Account](https://wbcomdesigns.com/my-account/)
2. **Navigate to** Downloads → Reign Dokan Addon
3. **Download** the `reign-dokan-addon.zip` file

**Option B: Already have the file?** Perfect! Continue to Step 2.

---

### Step 2: Install via WordPress (5 minutes)

**Easy Installation Method:**
1. **Go to** WordPress Admin → Plugins → Add New → Upload Plugin
2. **Choose file** and select your `reign-dokan-addon.zip`
3. **Click** "Install Now"
4. **Click** "Activate" when installation completes

**Alternative: FTP Installation** *(For developers)*
```
1. Extract the ZIP file
2. Upload folder to: /wp-content/plugins/reign-dokan-addon/
3. Activate from WordPress Admin → Plugins
```

**✅ Success Check:** You should see "Reign Dokan Addon" in your active plugins list.

---

### Step 3: License Activation (2 minutes)

**If you have a license key:**
1. **Go to** WordPress Admin → Reign Settings → License
2. **Find** "Reign Dokan Addon" section
3. **Enter** your license key
4. **Click** "Activate License"

*This enables automatic updates and premium support.*

---

### Step 4: Connect Everything Together (3 minutes)

**Configure Dokan First** *(The marketplace engine)*
1. **Navigate to** Dokan → Settings
2. **Enable vendor registration** *(allows sellers to join)*
3. **Set commission rates** *(your marketplace earnings)*
4. **Configure store URLs** *(how vendor stores look)*

**Then Configure Reign Enhancements**
1. **Go to** Appearance → Customize → Dokan Settings
2. **Enable beautiful features:**
   - ✅ Store header display
   - ✅ Professional layout options
   - ✅ "Sold by" vendor attribution
   - ✅ Vendor product showcases

---

## 🎯 Create Your Marketplace Pages (10 minutes)

### Main Vendor Directory Page
**Purpose:** Where customers browse all vendors

1. **Create new page:** Pages → Add New
2. **Title it:** "Vendors", "Marketplace", or "Stores"
3. **Add this shortcode:**
   ```
   [rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
   ```
4. **Publish & add to main menu**

### Featured Vendors Section
**Purpose:** Promote top vendors on homepage

1. **Edit your homepage** (or any page)
2. **Add this shortcode:**
   ```
   [rda_dokan_vendors count="6" per_row="3" show_featured_only="true" title="Featured Stores"]
   ```
3. **Save changes**

---

## ✅ Test Your Installation (5 minutes)

**Success Checklist - Make sure everything works:**

### Plugin Status Check
- [ ] **Go to** Plugins page → Should see "Reign Dokan Addon" active ✅
- [ ] **Check for errors** → No error messages in WordPress ✅

### Shortcode Functionality Test
- [ ] **Create test page** with `[rda_dokan_vendors]` shortcode ✅
- [ ] **View page** → Should display vendors without errors ✅

### Template Loading Verification
- [ ] **Visit any Dokan store page** ✅
- [ ] **Check design** → Should use beautiful Reign styling ✅

**🎉 All green? Perfect! Your marketplace is ready!**

---

## 🚨 Troubleshooting (If Something's Wrong)

### Problem: Templates Look Plain/Unstyled
**Causes & Solutions:**
- ✅ **Clear all cache** (caching plugins, browser cache)
- ✅ **Confirm Reign theme is active** (not just installed)
- ✅ **Check Dokan is working** (create test vendor store)

### Problem: Shortcodes Show as Text
**Causes & Solutions:**
- ✅ **Verify addon is activated** (check Plugins page)
- ✅ **Look for PHP errors** (check WordPress debug log)
- ✅ **Ensure Dokan works first** (test basic Dokan functionality)

### Problem: Pages Won't Save
**Causes & Solutions:**
- ✅ **Check plugin conflicts** (deactivate others temporarily)
- ✅ **Increase memory limit** (contact hosting provider)
- ✅ **Clear browser cache** (try different browser)

---

## 🔧 Advanced Customization (For Developers)

### Safe Template Customization
**How to modify marketplace templates without losing changes during updates:**

1. **Copy template files from plugin:**
   ```
   Source: /wp-content/plugins/reign-dokan-addon/dokan/store.php
   Destination: /wp-content/themes/your-theme/dokan/store.php
   ```

2. **Edit the copied files** - Your changes are now update-safe!

### Available Templates for Customization
- `store-header.php` - Vendor store header design
- `store-lists.php` - Store directory listing layout
- `store-sidebar.php` - Store sidebar content
- `store.php` - Main store page template

---

## 🚀 What's Next?

### Immediate Next Steps:
1. **[Complete Configuration](03-configuration.md)** - Fine-tune all marketplace settings
2. **[Customize Store Appearance](04-store-customization.md)** - Match your brand perfectly
3. **[Master All Shortcodes](07-shortcodes-reference.md)** - Unlock advanced features

### Business Setup:
- Configure vendor registration process
- Set up commission structures
- Add payment gateways
- Create vendor onboarding materials

### Growth Features:
- Add social marketplace features with BuddyPress
- Set up email marketing for vendors
- Create vendor training materials
- Plan marketplace marketing campaigns

---

## 🆘 Need More Help?

- **[FAQ](08-faq.md)** - Common questions and answers
- **[Troubleshooting Guide](06-troubleshooting.md)** - Fix specific issues
- **[Developer Guide](05-developer-guide.md)** - Advanced customization
- **[Support](mailto:support@wbcomdesigns.com)** - Contact our team

---

*🏗️ Installation Complete! Your marketplace foundation is solid and ready to grow.*