# Reign Dokan Addon - Shortcodes Reference

## Available Shortcodes

Reign Dokan Addon provides **2 custom shortcodes** for enhanced marketplace displays.

---

## 1. [rda_dokan_vendors]

### Purpose
Display featured or selected vendors with customizable layouts and optional carousel mode.

### All Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `title` | string | 'Featured Vendor' | Section heading/title |
| `per_row` | string | '3' | Number of vendors per row (1-6) |
| `count` | string | '6' | Total vendors to display |
| `show_featured_only` | boolean | false | Show only featured vendors |
| `enable_slider` | boolean | false | Enable carousel/slider mode |
| `layout` | string | 'layout-type-1' | Layout style (layout-type-1, layout-type-2) |
| `selected_vendors` | string | '' | Comma-separated vendor IDs to display specific vendors |

### Usage Examples

#### Basic Usage
```
[rda_dokan_vendors]
```

#### Show Featured Vendors
```
[rda_dokan_vendors show_featured_only="true" count="8" title="Premium Vendors"]
```

#### Display Specific Vendors
```
[rda_dokan_vendors selected_vendors="12,45,67,89" per_row="4"]
```

#### Carousel Mode
```
[rda_dokan_vendors enable_slider="true" count="12" per_row="4"]
```

#### Custom Layout
```
[rda_dokan_vendors layout="layout-type-2" per_row="3" count="9"]
```

#### Full Example
```
[rda_dokan_vendors
    title="Top Rated Sellers"
    per_row="4"
    count="8"
    show_featured_only="true"
    enable_slider="false"
    layout="layout-type-1"
]
```

### Template Used
- `/dokan/widgets/rda-sellers.php`

### CSS Classes
- `.rda-dokan-vendors-wrapper`
- `.vendor-item`
- `.vendor-info`
- `.vendor-products`

---

## 2. [rda_dokan_store_listing]

### Purpose
Display a searchable store listing with pagination and filtering options.

### All Parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `per_page` | integer | 10 | Number of stores per page |
| `search` | string | 'yes' | Enable search bar ('yes'/'no') |
| `per_row` | integer | 3 | Stores per row (1-6) |
| `featured` | string | 'no' | Show featured stores only ('yes'/'no') |
| `enable_slider` | boolean | false | Enable carousel mode |
| `selected_vendors` | string | '' | Comma-separated vendor IDs for specific vendors |

### Usage Examples

#### Basic Store Listing
```
[rda_dokan_store_listing]
```

#### With Search and Pagination
```
[rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
```

#### Featured Stores Only
```
[rda_dokan_store_listing featured="yes" search="no" per_page="6"]
```

#### Specific Vendors in Grid
```
[rda_dokan_store_listing selected_vendors="10,20,30,40" per_row="2"]
```

#### Slider Mode
```
[rda_dokan_store_listing enable_slider="true" per_row="3" per_page="9"]
```

#### No Search, More Stores
```
[rda_dokan_store_listing search="no" per_page="20" per_row="4"]
```

### Template Used
- `/dokan/store-lists.php`
- `/dokan/store-lists-loop.php`

### CSS Classes
- `.rda-dokan-store-lists-wrapper`
- `.dokan-seller-wrap`
- `.store-content`
- `.store-footer`

### Search Functionality
When `search="yes"`, the shortcode displays:
- Search input field
- Search button
- Results filter by store name
- GET parameter: `dokan_seller_search`

---

## Developer Filters

### For [rda_dokan_vendors]

None specific - uses template system for customization.

### For [rda_dokan_store_listing]

#### Filter Default Parameters
```php
add_filter('rda_dokan_store_listing_per_page', function($defaults) {
    $defaults['per_page'] = 20;
    $defaults['per_row'] = 4;
    return $defaults;
});
```

#### Modify Seller Query
```php
add_filter('rda_dokan_seller_listing_args', function($args) {
    $args['orderby'] = 'registered';
    $args['order'] = 'DESC';
    $args['meta_key'] = 'dokan_enable_selling';
    $args['meta_value'] = 'yes';
    return $args;
});
```

#### Customize Template Arguments
```php
add_filter('rda_dokan_store_list_args', function($args) {
    $args['show_products'] = true;
    $args['image_size'] = 'medium';
    $args['enable_pagination'] = true;
    return $args;
});
```

#### Products Per Store
```php
add_filter('rda_store_list_loop_products_to_display', function() {
    return 4; // Show 4 products per store
});
```

---

## Advanced Customization

### Custom Vendor Selection
```php
// Get specific vendors by criteria
$vendor_ids = get_users(array(
    'role' => 'seller',
    'meta_key' => 'dokan_feature_seller',
    'meta_value' => 'yes',
    'fields' => 'ID'
));
$ids = implode(',', $vendor_ids);

echo do_shortcode('[rda_dokan_vendors selected_vendors="' . $ids . '"]');
```

### Dynamic Parameters
```php
// Dynamic shortcode generation
$atts = array(
    'per_page' => get_option('vendors_per_page', 12),
    'search' => is_mobile() ? 'no' : 'yes',
    'per_row' => is_mobile() ? 1 : 3
);

$shortcode = '[rda_dokan_store_listing';
foreach ($atts as $key => $value) {
    $shortcode .= ' ' . $key . '="' . $value . '"';
}
$shortcode .= ']';

echo do_shortcode($shortcode);
```

### Conditional Display
```php
// Show different layouts based on context
if (is_front_page()) {
    echo do_shortcode('[rda_dokan_vendors show_featured_only="true" count="4"]');
} elseif (is_page('vendors')) {
    echo do_shortcode('[rda_dokan_store_listing per_page="20" search="yes"]');
}
```

---

## Styling Guide

### Vendor Display Styling
```css
/* Customize vendor cards */
.rda-dokan-vendors-wrapper .vendor-item {
    border: 1px solid #ddd;
    padding: 20px;
    margin-bottom: 20px;
}

/* Vendor image */
.vendor-item .vendor-image {
    width: 100%;
    height: 200px;
    object-fit: cover;
}
```

### Store Listing Styling
```css
/* Store grid customization */
.rda-dokan-store-lists-wrapper {
    display: grid;
    gap: 20px;
}

/* Search bar styling */
.dokan-seller-search {
    margin-bottom: 30px;
    padding: 20px;
    background: #f5f5f5;
}
```

---

## Performance Tips

1. **Limit Results**: Don't display too many vendors at once
   ```
   [rda_dokan_vendors count="6"]
   ```

2. **Disable Search** on pages with many vendors
   ```
   [rda_dokan_store_listing search="no"]
   ```

3. **Use Pagination** for large vendor lists
   ```
   [rda_dokan_store_listing per_page="12"]
   ```

4. **Cache Output** when possible
   ```php
   $output = get_transient('vendor_listing');
   if (!$output) {
       $output = do_shortcode('[rda_dokan_vendors]');
       set_transient('vendor_listing', $output, HOUR_IN_SECONDS);
   }
   echo $output;
   ```

---

## Common Issues & Solutions

### Vendors Not Displaying
- Ensure vendors are approved in Dokan settings
- Check vendors have at least one published product
- Verify vendor role is properly assigned

### Search Not Working
- Check `search="yes"` is set
- Ensure no JavaScript errors in console
- Verify search parameter name: `dokan_seller_search`

### Layout Breaking
- Check `per_row` value is appropriate for container width
- Ensure CSS is loading properly
- Clear cache after changes

### Slider Not Working
- Verify `enable_slider="true"` is set correctly
- Check slider JavaScript is loaded
- Ensure sufficient vendors for sliding

---

## Migration from Dokan Shortcodes

If migrating from standard Dokan shortcodes:

| Dokan Shortcode | Reign Equivalent |
|-----------------|------------------|
| `[dokan-stores]` | `[rda_dokan_store_listing]` |
| `[dokan-best-selling-vendor]` | `[rda_dokan_vendors show_featured_only="true"]` |

---

## Testing Checklist

- [ ] Basic shortcode displays vendors/stores
- [ ] Parameters change output correctly
- [ ] Search functionality works
- [ ] Pagination displays and functions
- [ ] Featured filter works
- [ ] Specific vendor selection works
- [ ] Slider mode activates
- [ ] Responsive layout adjusts per row

---

## Support

- **Documentation**: This guide
- **Templates**: Check `/dokan/` directory in plugin
- **Support**: Contact WBcom Designs
- **Updates**: Check changelog for new parameters

---

*Shortcode reference verified against Reign Dokan Addon v3.5.4*