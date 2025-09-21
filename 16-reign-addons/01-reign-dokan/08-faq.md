# Reign Dokan Addon - Frequently Asked Questions

## About This Addon

### What exactly is the Reign Dokan addon?

Reign Dokan Addon v3.5.4 integrates Dokan multivendor marketplace with the Reign theme, providing:

**Core Features (Verified):**
- Professional store layouts and templates
- 2 custom shortcodes for displaying vendors/stores
- BuddyPress integration for social marketplace features
- Theme settings for store customization
- Template override system

**What it does:**
- Makes Dokan stores match your Reign theme design
- Provides shortcodes to display vendor listings
- Adds BuddyPress social features (when BP is active)
- Gives control over store header display and layout

**What it doesn't do:**
- Replace Dokan (you still need the main plugin)
- Handle payments (that's WooCommerce + Dokan)
- Create products for vendors
- Manage vendor registration

### Do I need this if I already have Dokan?

**Yes, if you want:**
- Store pages that match your Reign theme design
- Shortcodes to display vendor listings: `[rda_dokan_vendors]` and `[rda_dokan_store_listing]`
- BuddyPress integration for social marketplace features
- Better control over store appearance
- Template customization options

**No, if you:**
- Use a different theme (not Reign)
- Don't need design integration
- Happy with default Dokan templates
- Don't use BuddyPress

## Installation & Setup

### What are the requirements?

**Required:**
- WordPress 4.0+
- Reign Theme (activated)
- WooCommerce
- Dokan Plugin (Free or Pro)

**Optional:**
- BuddyPress (for social marketplace features)

### Is installation difficult?

**No, it's straightforward:**

1. Install required plugins (WooCommerce, Dokan)
2. Upload and activate Reign Dokan Addon
3. Configure settings at Appearance → Customize → Dokan Settings
4. Add shortcodes to display vendors/stores

### Do I need WooCommerce?

**Yes, absolutely required!**

Dokan is built on top of WooCommerce, so:
- Products are WooCommerce products
- Payments go through WooCommerce
- Orders managed by WooCommerce

**Installation order:**
1. WooCommerce first
2. Dokan second
3. Reign Dokan Addon third

## Features & Functionality

### What shortcodes are available?

**2 shortcodes included:**

#### [rda_dokan_vendors]
Display vendor listings with customizable options:
```
[rda_dokan_vendors count="6" per_row="3" show_featured_only="true"]
```

#### [rda_dokan_store_listing]
Show searchable store listings with pagination:
```
[rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
```

### What theme settings are available?

**Store Header Settings:**
- Control store header display on/off
- Set header layout (fullwidth/contained)

**Product Page Settings:**
- Show vendor header on product pages
- Display vendor products section
- Control number of vendor products (1-50)
- Show/hide "Sold by" vendor attribution

**Store Layout:**
- Choose store list layout (grid/list)
- Set sidebar position (left/right/none)

### What BuddyPress features are included?

**When BuddyPress is active:**
- Vendor store tabs in user profiles
- Favorite products functionality
- Activity stream integration for reviews
- Social marketplace features

**Note:** BuddyPress is optional but recommended for social features.

## Template Customization

### Can I customize store templates?

**Yes! Template override system available.**

**How to customize:**
1. Copy template from plugin to theme:
   ```
   From: /wp-content/plugins/reign-dokan-addon/dokan/store.php
   To: /wp-content/themes/your-theme/dokan/store.php
   ```
2. Edit the copied file safely

**Available templates:**
- `store-header.php` - Store header layout
- `store-lists.php` - Store listing page
- `store.php` - Main store page
- And more...

### Can I use hooks and filters?

**Yes! Developer-friendly hooks available:**

**Filters:**
- `rda_dokan_seller_listing_args` - Customize vendor queries
- `rda_dokan_store_list_args` - Modify store listing
- `rda_store_list_loop_products_to_display` - Control products shown

**Actions:**
- `reign_dokan_addon_loaded` - Plugin initialization

## Common Issues

### Shortcodes not working?

**Check these:**
1. Plugin is activated
2. Dokan is configured properly
3. Vendors exist and are enabled
4. Test with basic shortcode: `[rda_dokan_vendors]`

### Settings not applying?

**Try these fixes:**
1. Clear all caches
2. Go to Customizer and republish settings
3. Check theme settings are saved

### BuddyPress features missing?

**Verify:**
1. BuddyPress is active
2. User is a vendor
3. Clear BuddyPress cache

## Support

### How to get help?

**Available support:**
- Documentation (this guide)
- Email: support@wbcomdesigns.com
- Include detailed description and steps to reproduce issues

### Before contacting support:

**Gather this information:**
- WordPress version
- Reign theme version
- Dokan version
- Plugin version
- Error messages (if any)

---

*FAQ verified against Reign Dokan Addon v3.5.4 source code*