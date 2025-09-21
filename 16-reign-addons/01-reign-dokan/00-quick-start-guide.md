# Reign Dokan Addon - Quick Start Guide

## What This Addon Does

Reign Dokan Addon v3.5.4 enhances your Dokan multivendor marketplace with Reign theme styling, custom shortcodes, and social features. It provides professional vendor stores, enhanced layouts, and seamless BuddyPress integration.

## Prerequisites

Before installing, ensure you have:
- ✅ WordPress 4.0 or higher
- ✅ Reign Theme installed and activated
- ✅ Dokan Plugin installed and configured
- ✅ WooCommerce active (required by Dokan)
- ✅ BuddyPress (optional, for social features)

## 5-Minute Installation

### Step 1: Install the Plugin
1. Download the Reign Dokan Addon zip file
2. Go to **WordPress Admin → Plugins → Add New → Upload Plugin**
3. Choose the zip file and click **Install Now**
4. Click **Activate** after installation

### Step 2: Verify Installation
After activation, check:
- Reign Settings shows Dokan options
- Customizer has Dokan settings section
- Templates are loading from addon

## Essential Shortcodes

### Display Vendor Stores
Add this to any page to show vendor listings:
```
[rda_dokan_store_listing]
```

**With Options:**
```
[rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
```

### Show Featured Vendors
Display selected or featured vendors:
```
[rda_dokan_vendors]
```

**With Options:**
```
[rda_dokan_vendors count="6" per_row="3" show_featured_only="true" title="Top Vendors"]
```

## Basic Configuration

### 1. Create Store Listing Page
Create a new page called "Vendors" or "Stores" and add:
```
[rda_dokan_store_listing per_page="12" search="yes"]
```

### 2. Add Featured Vendors to Homepage
Add this to your homepage or any widget area:
```
[rda_dokan_vendors count="4" per_row="4" show_featured_only="true"]
```

### 3. Configure Basic Settings

Navigate to **Appearance → Customize → Dokan Settings**:

| Setting | Recommended Value | Purpose |
|---------|------------------|---------|
| Store Header Location | Enabled | Shows vendor header |
| Store Header Layout | Fullwidth | Professional look |
| Show Vendor Products | Yes | Display on product pages |
| Number of Products | 10 | Products to show |
| Show "Sold By" | Yes | Vendor attribution |

## BuddyPress Features

If BuddyPress is active, you automatically get:
- **Store Tab** in user profiles
- **Favorite Products** functionality
- **Activity Stream** updates for reviews

No configuration needed - these activate automatically!

## Template Customization

### Quick Template Override
1. Copy any template from:
   ```
   /wp-content/plugins/reign-dokan-addon/dokan/
   ```

2. Paste into your theme:
   ```
   /wp-content/themes/your-theme/dokan/
   ```

3. Edit the copied file - changes are safe from updates

### Available Templates
- `store-header.php` - Vendor store header
- `store-lists.php` - Store listing layout
- `store-sidebar.php` - Store sidebar content
- `store.php` - Main store template

## Testing Your Setup

### Checklist:
- [ ] Store listing page displays vendors
- [ ] Vendor stores show proper header
- [ ] Search functionality works
- [ ] Featured vendors display correctly
- [ ] BuddyPress tabs appear (if using BP)
- [ ] Templates load with Reign styling

## Common First Steps

### For Marketplace Owners:
1. Create main vendors page with `[rda_dokan_store_listing]`
2. Add featured vendors to homepage
3. Configure store header settings
4. Test vendor registration flow

### For Developers:
1. Review available hooks and filters
2. Set up template overrides
3. Customize shortcode outputs
4. Add custom styling if needed

## Troubleshooting Quick Fixes

### Vendors Not Showing?
- Check vendors are approved in Dokan
- Ensure vendors have products
- Verify shortcode spelling

### Styling Issues?
- Clear cache
- Check Reign theme is active
- Verify CSS is loading

### BuddyPress Features Missing?
- Confirm BuddyPress is active
- Check user is a vendor
- Clear permalinks

## Get More Help

- **Settings Guide**: See [Configuration](./03-configuration.md) for all options
- **Developer Docs**: Check [Developer Guide](./05-developer-guide.md) for hooks
- **All Shortcodes**: View [Shortcodes Reference](./07-shortcodes-reference.md)
- **Support**: Contact WBcom Designs support team

## Next Steps

Now that basic setup is complete:
1. Fine-tune your marketplace appearance
2. Configure vendor capabilities
3. Set up payment methods
4. Customize email notifications
5. Add additional Reign addons as needed

---

*Quick Start Complete! Your Dokan marketplace is now enhanced with Reign theme features.*