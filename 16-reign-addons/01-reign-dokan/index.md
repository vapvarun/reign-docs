# Reign Dokan Addon Documentation

## 🛍️ Transform Your Website into a Thriving Multi-Vendor Marketplace

Welcome to the complete documentation for Reign Dokan Addon - your gateway to creating a professional, beautiful marketplace where vendors can sell and customers can shop from multiple stores in one place.

## 🚀 What This Addon Does

Reign Dokan Addon seamlessly integrates your Dokan marketplace with the stunning Reign theme, providing:
- ✨ Beautiful vendor store designs
- 🎯 Powerful shortcodes for vendor displays
- 👥 Social marketplace features with BuddyPress
- 🎨 Complete customization control

## ✅ Requirements
- WordPress 4.0+
- Reign Theme (active)
- Dokan Plugin (free or pro)
- WooCommerce
- BuddyPress (optional but recommended)

## Installation
1. Upload `reign-dokan-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Configure settings in Customizer

## Features

### Custom Shortcodes

#### [rda_dokan_vendors]
Display vendors with customizable layout.

**Parameters:**
- `title` - Section title (default: 'Featured Vendor')
- `per_row` - Vendors per row (default: '3')
- `count` - Number to display (default: '6')
- `show_featured_only` - Featured only (default: false)
- `enable_slider` - Carousel mode (default: false)
- `layout` - Layout style (default: 'layout-type-1')
- `selected_vendors` - Specific vendor IDs (comma-separated)

**Example:**
```
[rda_dokan_vendors count="8" per_row="4" show_featured_only="true"]
```

#### [rda_dokan_store_listing]
Display store listings with search.

**Parameters:**
- `per_page` - Stores per page (default: 10)
- `search` - Enable search 'yes'/'no' (default: 'yes')
- `per_row` - Stores per row (default: 3)
- `featured` - Featured only 'yes'/'no' (default: 'no')
- `enable_slider` - Slider mode (default: false)
- `selected_vendors` - Specific vendor IDs

**Example:**
```
[rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
```

### Theme Settings

Available in Customizer:

- `reign_dokan_store_header_location` - Store header location (default: true)
- `reign_dokan_store_header_layout` - Header layout (default: 'fullwidth')
- `reign_dokan_show_vendor_header_on_pro_page` - Show on product pages (default: false)
- `reign_dokan_show_vendor_header_width` - Header width (default: 'fullwidth')
- `reign_dokan_show_vendor_pros_on_pro_page` - Show vendor products (default: false)
- `reign_dokan_num_of_vendor_pros_on_pro_page` - Number of products (default: 10)
- `reign_dokan_show_sold_by_in_pro_meta` - Show "Sold by" (default: true)
- `reign_dokan_show_vendor_info_in_pro_page` - Show vendor info (default: false)
- `reign_dokan_store_list_layout` - Store list layout (default: 'layout_one')
- `store_layout` - Sidebar position (default: 'left')

### BuddyPress Integration
- Adds vendor store tab to profiles
- Favorite products functionality
- Activity stream for product reviews

### Template Overrides

Located in `/dokan/` directory:
- `store-header.php`
- `store-lists.php`
- `store-lists-loop.php`
- `store-sidebar.php`
- `store.php`
- `store-reviews.php`
- `store-toc.php`
- `vendor-biography.php`
- `orders/listing.php`
- `products/products-listing.php`
- `products/products-listing-row.php`
- `review/listing.php`
- `review/listing-table-tr.php`

## Developer Reference

### Plugin Structure
```
reign-dokan-addon/
├── admin/                  # Admin settings
├── assets/                 # CSS, JS, images
├── buddypress/            # BuddyPress integration
├── core/                  # Core functionality
├── dokan/                 # Template overrides
├── edd-license/           # License management
├── rda-shortcodes/        # Shortcode classes
├── rda-widgets/           # Custom widgets
└── reign-dokan-addon.php  # Main plugin file
```

### Hooks & Filters

#### Actions
- `reign_dokan_addon_loaded` - After plugin loads

#### Filters
- `dokan_get_template_part` - Override template parts
- `dokan_locate_template` - Override template locations
- `rda_dokan_seller_listing_args` - Modify seller query
- `rda_dokan_store_list_args` - Modify store list args
- `rda_store_list_loop_products_to_display` - Products per store (default: 3)
- `rda_dokan_store_listing_per_page` - Modify defaults

### Code Examples

#### Customize Settings
```php
// Get setting
$header_location = get_theme_mod('reign_dokan_store_header_location', true);

// Modify seller query
add_filter('rda_dokan_seller_listing_args', function($args) {
    $args['number'] = 20;
    return $args;
});

// Change products per store
add_filter('rda_store_list_loop_products_to_display', function() {
    return 5;
});
```

#### Template Override
Copy template from plugin's `/dokan/` folder to your theme's `/dokan/` folder.

## License
Uses EDD Software Licensing. License key stored as `wbcom_reign_dokan_addon_license_key`.