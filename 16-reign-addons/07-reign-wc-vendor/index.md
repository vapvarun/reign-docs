# Reign WC Vendors Addon Documentation

## Overview
Reign WC Vendors Addon integrates WC Vendors Pro with Reign theme, adding one custom shortcode, BuddyPress integration, and favorite products functionality.

## Requirements
- WordPress 4.0+
- Reign Theme
- WC Vendors Pro Plugin
- WooCommerce
- BuddyPress (optional)

## Installation
1. Upload `reign-wc-vendor-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Configure in Reign Settings

## Features

### Custom Shortcode

#### [reign-wcvendors-sellers]
Display searchable vendor listing with pagination.

**Features:**
- Vendor search functionality
- Pagination support
- Responsive grid layout
- Shows vendor shop names
- Links to vendor stores

**Example:**
```
[reign-wcvendors-sellers]
```

**Note:** This is the ONLY custom shortcode added by this addon.

### BuddyPress Integration
- Adds "Store" tab to vendor profiles
- Favorite products functionality
- Ajax-powered favorite button

### Custom Widgets
- Shop Owner Widget
- Vendor List Widget
- Vendor Profile Widget

### Template Overrides
Located in `/templates/wc-vendors/`:
- `front/` - Frontend templates
- `store/` - Store templates

## WC Vendors Core Shortcodes

These come from WC Vendors Pro (NOT Reign addon):
- `[wcv_vendorslist]` - Vendor listing
- `[wcv_pro_dashboard]` - Vendor dashboard
- `[wcv_orders]` - Vendor orders
- `[wcv_shop_settings]` - Shop settings

## Developer Reference

### Plugin Structure
```
reign-wc-vendor-addon/
├── admin/
├── assets/
├── public/
│   └── class-reign-wcvendors-addon-public.php
├── includes/
│   ├── class-reign-wcvendors-addon.php
│   └── class-reign-wcvendors-addon-loader.php
├── templates/
│   └── wc-vendors/
└── reign-wc-vendor-addon.php
```

### Hooks & Filters

#### Filters
```php
// Template location
apply_filters('reign_wc_vendors_locate_template', $template, $template_name, $template_path, $default_path);

// Shop description length (default: 350)
apply_filters('reign_wc_vendors_shop_description_limit', 350);

// Store address format
apply_filters('reign_wc_vendors_format_store_address_output', $address, $vendor_id);

// Social media settings
apply_filters('reign_wc_vendors_get_social_media_settings', $settings);

// BuddyPress tab names
apply_filters('reign_wc_vendors_store_primary_bp_tab_name', 'Store');
apply_filters('reign_wc_vendors_store_primary_bp_tab_slug', 'store');

// Vendor sales count
apply_filters('rwcv_store_total_sales_count', $count, $vendor_id);

// Sellers per page (default: 12)
apply_filters('rmcv_seller_list_count_per_page', 12);
```

### Code Examples

#### Customize Vendors Per Page
```php
add_filter('rmcv_seller_list_count_per_page', function() {
    return 24;
});
```

#### Customize Tab Names
```php
add_filter('reign_wc_vendors_store_primary_bp_tab_name', function() {
    return __('My Shop', 'textdomain');
});
```

#### Adjust Description Length
```php
add_filter('reign_wc_vendors_shop_description_limit', function() {
    return 500;
});
```

## CSS Classes
- `.reign-wcv-seller-list-filter` - Search wrapper
- `.wcv-seller-list-filter-inner-wrapper` - Inner wrapper
- `.reign-wcv-item-seller-count` - Vendor count display

## Important Notes
- Only ONE custom shortcode: `[reign-wcvendors-sellers]`
- Other vendor shortcodes come from WC Vendors Pro
- Focus on BuddyPress integration and styling
- Favorite products require user login