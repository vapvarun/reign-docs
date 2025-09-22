# Reign Dokan Addon - Quick Start Guide for First-Time Users

## 🚀 Launch Your Marketplace in 30 Minutes

Transform your website into a professional multi-vendor marketplace where sellers can create beautiful stores and customers can shop from multiple vendors in one place. This guide gets you from zero to marketplace hero in just 30 minutes!

## 📋 What You Need (5 minutes to check)

- ✅ **WordPress website** (any hosting will work)
- ✅ **Reign Theme** active (your beautiful marketplace foundation)
- ✅ **Dokan Plugin** installed (the marketplace engine - free version works!)
- ✅ **WooCommerce** active (handles payments)
- ✅ **Reign Dokan Addon license** (from your WBcom account)

*Don't have these yet? No problem! Links to get everything are in our [installation guide](02-installation-setup.md).*

---

## 🎯 Step-by-Step Setup Process

### Step 1: Install Your Marketplace Engine (5 minutes)

**What you're doing:** Adding the professional marketplace features to your website.

1. **Download your addon** from WBcom Account → Downloads
2. **Go to** WordPress Admin → Plugins → Add New → Upload Plugin
3. **Upload & activate** the Reign Dokan Addon
4. **Success check:** You should see "Dokan" options in Reign Settings

✅ **Milestone:** Your marketplace engine is installed!

---

### Step 2: Create Your Vendor Directory (10 minutes)

**What you're doing:** Building the main page where customers browse all vendors.

1. **Create new page:** Pages → Add New → Title it "Vendors" or "Marketplace"
2. **Add this magic code:**
   ```
   [rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
   ```
3. **Publish the page**
4. **Add to menu:** Appearance → Menus → Add your new page

✅ **Milestone:** Customers can now browse vendors!

---

### Step 3: Add Featured Vendors to Homepage (5 minutes)

**What you're doing:** Showcasing your best vendors on the homepage to drive sales.

1. **Edit your homepage** (or any page/widget area)
2. **Add this code for featured vendors:**
   ```
   [rda_dokan_vendors count="4" per_row="4" show_featured_only="true" title="Featured Stores"]
   ```
3. **Save changes**

✅ **Milestone:** Your homepage now promotes top vendors!

---

### Step 4: Configure Your Marketplace Settings (10 minutes)

**What you're doing:** Making your marketplace look professional and work smoothly.

**Go to:** Appearance → Customize → Dokan Settings

**Essential Settings:**
```
✅ Store Header: Enable
✅ Store Layout: Fullwidth (looks professional)
✅ Show "Sold By": Yes (builds trust)
✅ Vendor Products: Show 10 on product pages
✅ Search: Enable store search
```

✅ **Milestone:** Your marketplace looks professional and works great!

---

## 🎉 Marketplace Launch Complete!

**Congratulations!** Your marketplace is now live with these features:
- ✅ Professional vendor directory page
- ✅ Featured vendors on homepage
- ✅ Beautiful store designs for vendors
- ✅ Customer search functionality
- ✅ Mobile-responsive layouts

---

## 🚀 Bonus Features (If You Have BuddyPress)

If BuddyPress is active, you automatically get these social features:
- **👤 Store tabs** in user profiles
- **❤️ Favorite products** functionality
- **📱 Activity stream** updates for reviews

*No setup needed - these activate automatically when BuddyPress is detected!*

---

## 🔧 Advanced Customization (For Developers)

### Template Customization Options
**Safe way to modify marketplace templates:**

1. **Copy template files from:**
   ```
   /wp-content/plugins/reign-dokan-addon/dokan/
   ```

2. **Paste into your theme:**
   ```
   /wp-content/themes/your-theme/dokan/
   ```

3. **Edit safely** - your changes survive updates!

**Available Templates:**
- `store-header.php` - Vendor store header design
- `store-lists.php` - Store directory layout
- `store-sidebar.php` - Store sidebar content
- `store.php` - Main store template

### Useful Shortcode Parameters
**Complete shortcode customization options:**

```php
// Vendor Directory with Search
[rda_dokan_store_listing per_page="12" search="yes" per_row="4"]

// Featured Vendors Showcase
[rda_dokan_vendors count="6" per_row="3" show_featured_only="true" title="Top Vendors"]
```

---

## ✅ Success Checklist

**Test these features to ensure everything works:**
- [ ] Vendor directory page shows stores
- [ ] Store headers display properly
- [ ] Search functionality works
- [ ] Featured vendors appear correctly
- [ ] BuddyPress tabs show (if using BP)
- [ ] Mobile layout looks great

---

## 🆘 Quick Troubleshooting

**Vendors not showing?**
- ✅ Check vendors are approved in Dokan settings
- ✅ Ensure vendors have published products
- ✅ Verify shortcode spelling is correct

**Styling looks wrong?**
- ✅ Clear all caching plugins
- ✅ Confirm Reign theme is active
- ✅ Check if CSS files are loading

**Missing BuddyPress features?**
- ✅ Confirm BuddyPress plugin is active
- ✅ Ensure user has vendor role
- ✅ Refresh permalinks (Settings → Permalinks → Save)

---

## 📚 What's Next?

### For Marketplace Success:
1. **[Complete configuration](03-configuration.md)** - Fine-tune all settings
2. **[Customize appearance](04-store-customization.md)** - Make it match your brand
3. **[Learn all shortcodes](07-shortcodes-reference.md)** - Master advanced features
4. **[Developer guide](05-developer-guide.md)** - Custom modifications

### Business Growth:
- Set up vendor registration and approval process
- Configure commission structures
- Add payment gateways
- Create vendor onboarding materials
- Plan marketing campaigns

---

*🏆 Your marketplace empire starts now! Need help? Check our [FAQ](08-faq.md) or contact support.*