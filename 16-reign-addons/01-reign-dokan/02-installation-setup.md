# Reign Dokan Addon - Installation & Setup

## Prerequisites (Verified)

Before installing Reign Dokan Addon v3.5.4:

### Required Components
1. **WordPress** 4.0 or higher
2. **Reign Theme** (activated)
3. **WooCommerce**
4. **Dokan Plugin** (Free or Pro)

### Optional Components
- **BuddyPress** - For social marketplace features

## Installation

### Standard WordPress Installation

1. **Download the Plugin**
   - Get `reign-dokan-addon.zip` from your WBcom Designs account

2. **Upload via WordPress Admin**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   ```
   - Select the ZIP file
   - Click "Install Now"
   - Click "Activate"

3. **Alternative: FTP Upload**
   ```
   Extract ZIP → Upload to /wp-content/plugins/reign-dokan-addon/
   Activate from WordPress Admin
   ```

## Initial Setup

### Step 1: License Activation (If Required)
If using a licensed version, activate via WBcom Designs license manager.

### Step 2: Basic Configuration

#### Configure Dokan First
1. **Navigate to Dokan → Settings**
2. Complete basic Dokan configuration:
   - Enable vendor registration
   - Set commission rates
   - Configure store URLs

#### Configure Reign Addon Settings
1. **Navigate to Appearance → Customize → Dokan Settings**
2. Configure available options:
   - Store header display and layout
   - Vendor product showcase settings
   - "Sold by" attribution display

### Step 3: Add Shortcodes to Pages

Create pages with these shortcodes:

#### Store Listing Page
```
Create a new page and add:
[rda_dokan_store_listing per_page="12" search="yes"]
```

#### Featured Vendors Section
```
Add to homepage or any page:
[rda_dokan_vendors count="6" per_row="3" show_featured_only="true"]
```

## Verification

### Test Installation Success

1. **Check Plugin is Active**
   - Go to Plugins page - should see "Reign Dokan Addon" active

2. **Verify Shortcodes Work**
   - Create test page with `[rda_dokan_vendors]`
   - Should display without errors

3. **Check Template Loading**
   - Visit Dokan store pages
   - Should use Reign-styled templates

### Common Issues

#### Templates Not Loading
- Clear cache
- Ensure Reign theme is active
- Check Dokan is properly configured

#### Shortcodes Not Working
- Verify plugin is activated
- Check for PHP errors
- Ensure Dokan is working first

## Template Customization

If you need to customize templates:

1. **Copy from plugin to theme:**
   ```
   From: /wp-content/plugins/reign-dokan-addon/dokan/store.php
   To: /wp-content/themes/your-theme/dokan/store.php
   ```

2. **Edit the copied file safely**

## Next Steps

- [Configuration Guide](03-configuration.md) - Configure all settings
- [Store Customization](04-store-customization.md) - Customize appearance
- [Shortcodes Reference](07-shortcodes-reference.md) - Complete shortcode guide

---

*Installation guide verified against Reign Dokan Addon v3.5.4*