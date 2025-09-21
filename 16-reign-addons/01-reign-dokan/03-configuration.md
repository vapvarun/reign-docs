# Reign Dokan Addon - Configuration Guide

## Overview

This guide covers all configuration options available in Reign Dokan Addon v3.5.4. All settings are managed through WordPress Customizer and theme modifications.

## Accessing Configuration

Navigate to: **Appearance → Customize → Dokan Settings**

## Available Theme Settings (Verified)

### Store Header Settings

#### reign_dokan_store_header_location
- **Type:** Boolean
- **Default:** `true`
- **Purpose:** Control where store header appears
- **Options:**
  - `true` - Display store header
  - `false` - Hide store header

#### reign_dokan_store_header_layout
- **Type:** String
- **Default:** `'fullwidth'`
- **Purpose:** Store header layout style
- **Options:**
  - `'fullwidth'` - Full width header
  - `'contained'` - Contained width

### Product Page Settings

#### reign_dokan_show_vendor_header_on_pro_page
- **Type:** Boolean
- **Default:** `false`
- **Purpose:** Display vendor header on single product pages
- **Options:**
  - `true` - Show vendor header
  - `false` - Hide vendor header

#### reign_dokan_show_vendor_header_width
- **Type:** String
- **Default:** `'fullwidth'`
- **Purpose:** Width of vendor header on product pages
- **Options:**
  - `'fullwidth'` - Full width
  - `'contained'` - Contained width

#### reign_dokan_show_vendor_pros_on_pro_page
- **Type:** Boolean
- **Default:** `false`
- **Purpose:** Show other products from same vendor
- **Options:**
  - `true` - Display vendor products
  - `false` - Hide vendor products

#### reign_dokan_num_of_vendor_pros_on_pro_page
- **Type:** Integer
- **Default:** `10`
- **Purpose:** Number of vendor products to display
- **Range:** 1-50 products

#### reign_dokan_show_sold_by_in_pro_meta
- **Type:** Boolean
- **Default:** `true`
- **Purpose:** Show "Sold by [Vendor]" in product meta
- **Options:**
  - `true` - Display sold by
  - `false` - Hide sold by

#### reign_dokan_show_vendor_info_in_pro_page
- **Type:** Boolean
- **Default:** `false`
- **Purpose:** Display vendor information box on product page
- **Options:**
  - `true` - Show vendor info
  - `false` - Hide vendor info

### Store Layout Settings

#### reign_dokan_store_list_layout
- **Type:** String
- **Default:** `'layout_one'`
- **Purpose:** Store listing page layout style
- **Options:**
  - `'layout_one'` - Grid layout
  - `'layout_two'` - List layout
  - Custom layouts if added

#### store_layout
- **Type:** String
- **Default:** `'left'`
- **Purpose:** Sidebar position on store pages
- **Options:**
  - `'left'` - Left sidebar
  - `'right'` - Right sidebar
  - `'none'` - No sidebar

## Programmatic Configuration

### Reading Settings

```php
// Get a setting value
$header_enabled = get_theme_mod('reign_dokan_store_header_location', true);
$products_count = get_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 10);
$store_layout = get_theme_mod('reign_dokan_store_list_layout', 'layout_one');
```

### Updating Settings

```php
// Set a setting value programmatically
set_theme_mod('reign_dokan_show_vendor_pros_on_pro_page', true);
set_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 20);
```

### Using in Templates

```php
// In your template files
if (get_theme_mod('reign_dokan_show_vendor_header_on_pro_page', false)) {
    // Display vendor header
    dokan_get_template_part('store-header');
}
```

## Shortcode Configuration

### Store Listing Shortcode Settings

Configure via shortcode parameters:
```
[rda_dokan_store_listing
    per_page="12"        // Stores per page
    search="yes"         // Enable search
    per_row="3"          // Stores per row
    featured="no"        // Show featured only
    enable_slider="false" // Carousel mode
]
```

### Vendors Display Settings

```
[rda_dokan_vendors
    title="Featured Vendors"  // Section title
    per_row="3"               // Vendors per row
    count="6"                 // Number to show
    show_featured_only="true" // Featured filter
    layout="layout-type-1"    // Layout style
]
```

## BuddyPress Integration Settings

BuddyPress features activate automatically when BuddyPress is active. No additional configuration required.

### Features Enabled:
- Vendor store tab in profiles
- Favorite products functionality
- Activity stream integration

### Customizing BP Tab Names

```php
// Change tab name via filter
add_filter('reign_dokan_store_primary_bp_tab_name', function() {
    return __('My Shop', 'textdomain');
});
```

## Developer Filters for Configuration

### Modify Store Listing

```php
// Customize store listing query
add_filter('rda_dokan_seller_listing_args', function($args) {
    $args['number'] = 20;
    $args['orderby'] = 'registered';
    $args['order'] = 'DESC';
    return $args;
});
```

### Adjust Products Display

```php
// Change products shown per store
add_filter('rda_store_list_loop_products_to_display', function() {
    return 5; // Show 5 products
});
```

### Customize Template Arguments

```php
// Modify store list template args
add_filter('rda_dokan_store_list_args', function($args) {
    $args['show_products'] = false;
    $args['image_size'] = 'thumbnail';
    return $args;
});
```

## Configuration Best Practices

### Performance Optimization
1. Limit products per vendor (10-20 recommended)
2. Use pagination for store listings
3. Enable search only if needed
4. Consider caching for heavy traffic

### User Experience
1. Keep store headers visible for branding
2. Show "Sold by" for transparency
3. Display 3-4 stores per row on desktop
4. Enable vendor products on product pages

### Mobile Optimization
1. Set per_row="1" for mobile views
2. Reduce products shown on mobile
3. Simplify headers for small screens

## Template File Settings

Templates using these settings:

| Template File | Settings Used |
|--------------|---------------|
| store.php | store_layout |
| store-lists-loop.php | reign_dokan_store_list_layout |
| store-header.php | reign_dokan_store_header_location, reign_dokan_store_header_layout |
| single-product.php | All product page settings |

## Troubleshooting Configuration

### Settings Not Applying?
1. Clear cache (browser and server)
2. Check theme mod is saved
3. Verify template is using setting
4. Check for filter overrides

### Default Values Loading?
- Settings may not be saved yet
- Use Customizer to save once
- Check database for theme_mods

### Custom Settings Needed?
Add your own settings:
```php
// Add custom setting
add_action('customize_register', function($wp_customize) {
    $wp_customize->add_setting('my_custom_dokan_setting', array(
        'default' => 'value',
        'type' => 'theme_mod',
    ));
});
```

## Configuration Checklist

- [ ] Store header location configured
- [ ] Product page vendor display set
- [ ] Number of vendor products defined
- [ ] Store listing layout selected
- [ ] Sidebar position chosen
- [ ] Shortcode parameters tested
- [ ] BuddyPress features verified
- [ ] Mobile settings optimized

## Getting Help

- **Developer Guide**: [Developer Documentation](./05-developer-guide.md)
- **Shortcodes**: [Shortcode Reference](./07-shortcodes-reference.md)
- **Support**: Contact WBcom Designs

---

*All settings verified against Reign Dokan Addon v3.5.4 source code*