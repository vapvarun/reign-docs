# Reign Dokan Addon - Store Customization Guide

## Available Customization Options

Based on the verified theme settings available in Reign Dokan Addon v3.5.4:

### Store Header Configuration

#### Store Header Display
- **Setting**: `reign_dokan_store_header_location`
- **Options**: Enable or disable store header display
- **Access**: Appearance → Customize → Dokan Settings

#### Store Header Layout
- **Setting**: `reign_dokan_store_header_layout`
- **Options**:
  - `'fullwidth'` - Full width header
  - `'contained'` - Contained width header

### Product Page Vendor Display

#### Vendor Header on Product Pages
- **Setting**: `reign_dokan_show_vendor_header_on_pro_page`
- **Purpose**: Show/hide vendor header on single product pages

#### Vendor Header Width
- **Setting**: `reign_dokan_show_vendor_header_width`
- **Options**: Fullwidth or contained

#### Vendor Products Showcase
- **Setting**: `reign_dokan_show_vendor_pros_on_pro_page`
- **Purpose**: Display other products from the same vendor

#### Number of Vendor Products
- **Setting**: `reign_dokan_num_of_vendor_pros_on_pro_page`
- **Default**: 10 products
- **Range**: 1-50 products

#### "Sold By" Attribution
- **Setting**: `reign_dokan_show_sold_by_in_pro_meta`
- **Purpose**: Display "Sold by [Vendor]" in product meta

#### Vendor Info Box
- **Setting**: `reign_dokan_show_vendor_info_in_pro_page`
- **Purpose**: Display vendor information box on product pages

### Store Layout Configuration

#### Store List Layout
- **Setting**: `reign_dokan_store_list_layout`
- **Options**:
  - `'layout_one'` - Grid layout
  - `'layout_two'` - List layout

#### Store Sidebar Position
- **Setting**: `store_layout`
- **Options**:
  - `'left'` - Left sidebar
  - `'right'` - Right sidebar
  - `'none'` - No sidebar

## Template Customization

### Template Override System

The addon follows WordPress template hierarchy. You can override any template:

#### How to Override Templates

1. **Copy template from plugin to theme:**
   ```
   From: /wp-content/plugins/reign-dokan-addon/dokan/store-header.php
   To: /wp-content/themes/your-theme/dokan/store-header.php
   ```

2. **Edit the copied file safely**

#### Available Templates

Key templates you can customize:
- `store-header.php` - Store header layout
- `store-lists.php` - Store listing page
- `store-lists-loop.php` - Individual store card
- `store.php` - Main store page
- `store-sidebar.php` - Store sidebar content

## Programming Settings

You can read and modify settings programmatically:

### Reading Current Settings
```php
// Get current settings
$header_enabled = get_theme_mod('reign_dokan_store_header_location', true);
$header_layout = get_theme_mod('reign_dokan_store_header_layout', 'fullwidth');
$show_vendor_products = get_theme_mod('reign_dokan_show_vendor_pros_on_pro_page', false);
$products_count = get_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 10);
```

### Updating Settings
```php
// Update settings programmatically
set_theme_mod('reign_dokan_store_header_location', true);
set_theme_mod('reign_dokan_show_vendor_pros_on_pro_page', true);
set_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 15);
```

### Using Settings in Templates
```php
// In your template files
if (get_theme_mod('reign_dokan_show_vendor_header_on_pro_page', false)) {
    // Display vendor header
    dokan_get_template_part('store-header');
}

if (get_theme_mod('reign_dokan_show_vendor_pros_on_pro_page', false)) {
    $count = get_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 10);
    // Display vendor products
}
```

## Available Hooks & Filters

For advanced customization, use these verified hooks:

### Filters
```php
// Customize vendor listing
add_filter('rda_dokan_seller_listing_args', function($args) {
    $args['number'] = 20;
    $args['orderby'] = 'registered';
    return $args;
});

// Modify store list arguments
add_filter('rda_dokan_store_list_args', function($args) {
    $args['show_products'] = true;
    $args['image_size'] = 'medium';
    return $args;
});

// Control products per store
add_filter('rda_store_list_loop_products_to_display', function() {
    return 5; // Show 5 products per store
});
```

### Actions
```php
// Hook into plugin initialization
add_action('reign_dokan_addon_loaded', function() {
    // Your initialization code
});
```

## Styling Customization

### CSS Classes to Target

Target these CSS classes for styling:
```css
/* Store listing customization */
.rda-dokan-store-lists-wrapper {
    /* Store listing container */
}

.dokan-seller-wrap {
    /* Individual store card */
}

/* Vendor display customization */
.rda-dokan-vendors-wrapper {
    /* Vendor display container */
}

.vendor-item {
    /* Individual vendor card */
}

/* Store page elements */
.store-content {
    /* Store main content */
}

.store-footer {
    /* Store footer area */
}
```

## Common Customizations

### Change Store Listing Layout
```php
// Force grid layout
add_filter('rda_dokan_store_list_args', function($args) {
    $args['layout'] = 'grid';
    return $args;
});
```

### Customize Vendor Products Count
```php
// Show different number of products based on user role
add_filter('rda_store_list_loop_products_to_display', function() {
    if (current_user_can('manage_options')) {
        return 10; // Admin sees more
    }
    return 4; // Regular users see fewer
});
```

## Best Practices

1. **Always test changes** on staging before production
2. **Use child theme** for template overrides
3. **Clear cache** after making changes
4. **Check mobile responsiveness**
5. **Validate settings** before saving

## Next Steps

- [Troubleshooting Guide](06-troubleshooting.md) - Fix common issues
- [Developer Guide](05-developer-guide.md) - Advanced hooks and filters
- [Shortcodes Reference](07-shortcodes-reference.md) - Shortcode parameters

---

*Store customization guide verified against Reign Dokan Addon v3.5.4 source code*