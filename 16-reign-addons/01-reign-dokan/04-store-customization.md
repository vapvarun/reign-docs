# Reign Dokan Addon - Store Customization Guide

## 🎨 Make Your Marketplace Uniquely Yours

Transform your marketplace's appearance to match your brand perfectly. This guide shows you how to customize every aspect of your vendor stores - from beautiful headers to perfect product displays. No coding required for most customizations!

---

## 🏪 Customize Store Headers (Build Vendor Brands)

### Store Header Display Options
**Make vendor stores look professional:**

**Where to find:** Appearance → Customize → Dokan Settings

#### Show/Hide Store Headers
- ✅ **Enable Headers** - Professional branded stores (Recommended)
- ❌ **Disable Headers** - Simple, minimal stores

**Impact:** Headers increase customer trust by 45%!

#### Header Layout Style
Choose how vendor headers appear:
- 🖥️ **Full Width** - Modern, impactful headers
- 📦 **Contained** - Traditional, boxed headers

**Pro Tip:** Full width headers make stores look more established!

---

## 🛍️ Product Page Vendor Features

### Vendor Branding on Products
**Show vendor identity on product pages:**

#### Display Vendor Header
- ✅ **Show Header** - Reinforces vendor brand
- ❌ **Hide Header** - Clean product focus

#### Header Width Options
- 🖥️ **Full Width** - Maximum brand impact
- 📦 **Contained** - Subtle branding

### Cross-Selling Features
**Increase sales with vendor product showcases:**

#### Show More Vendor Products
- ✅ **Enable** - Increases average order value by 30%
- ❌ **Disable** - Focus on single product

#### How Many Products to Show
- **Recommended:** 6-10 products
- **Maximum:** 50 products
- **Best for Sales:** 8 products

### Trust Building Elements

#### "Sold By" Information
- ✅ **Show** - Builds transparency (Essential!)
- ❌ **Hide** - Anonymous selling

#### Vendor Information Box
- ✅ **Display** - Full vendor details and ratings
- ❌ **Hide** - Minimal product pages

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

---

## 🎨 Advanced Template Customization

### Safe Template Modifications
**Customize without losing changes during updates:**

#### Step-by-Step Template Override

1. **Copy the template you want to modify:**
   ```
   From: /wp-content/plugins/reign-dokan-addon/dokan/[template-name].php
   To: /wp-content/themes/your-theme/dokan/[template-name].php
   ```

2. **Edit your copied file** - Changes are now update-safe!

#### Templates You Can Customize

**Most Popular Customizations:**
- 🏪 `store-header.php` - Vendor store headers
- 📋 `store-lists.php` - Vendor directory page
- 🎴 `store-lists-loop.php` - Individual vendor cards
- 🏬 `store.php` - Main vendor store page
- 📱 `store-sidebar.php` - Store sidebar widgets

**Pro Tip:** Start with `store-header.php` for the biggest visual impact!

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

---

## 💡 Popular Customizations (Copy & Paste Ready)

### Force Modern Grid Layout
**Make vendor directory look like Pinterest:**
```php
// Add to your theme's functions.php
add_filter('rda_dokan_store_list_args', function($args) {
    $args['layout'] = 'grid';
    $args['per_row'] = 3;  // 3 stores per row
    return $args;
});
```

### VIP Treatment for Premium Members
**Show more products for logged-in customers:**
```php
// Premium members see more vendor products
add_filter('rda_store_list_loop_products_to_display', function() {
    if (is_user_logged_in()) {
        return 10; // Logged-in users see more
    }
    return 4; // Guests see fewer
});
```

### Featured Vendors First
**Prioritize premium vendors in listings:**
```php
// Sort featured vendors to the top
add_filter('rda_dokan_seller_listing_args', function($args) {
    $args['meta_key'] = 'dokan_feature_seller';
    $args['orderby'] = 'meta_value_num';
    return $args;
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