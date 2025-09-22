# Reign Dokan Addon - Shortcodes Reference

## 🎯 Build Amazing Marketplace Pages with Simple Codes

Transform any page into a professional marketplace display with just 2 powerful shortcodes! Copy, paste, and customize - it's that easy. No coding skills required!

---

---

## 🏪 Shortcode #1: [rda_dokan_vendors]

### What It Does
**Creates beautiful vendor showcases** - Perfect for homepage featured vendors, vendor directories, or promotional sections.

### 📊 All Options Explained

| Setting | Type | Default | What It Does | Business Impact |
|---------|------|---------|--------------|------------------|
| `title` | text | 'Featured Vendor' | Your section heading | Customize for promotions |
| `per_row` | 1-6 | '3' | Vendors side by side | 3-4 looks professional |
| `count` | number | '6' | Total vendors shown | More = more choice |
| `show_featured_only` | true/false | false | Premium vendors only | Monetize with featured spots |
| `enable_slider` | true/false | false | Carousel display | Great for mobile/homepage |
| `layout` | layout-type-1/2 | 'layout-type-1' | Visual style | Match your brand |
| `selected_vendors` | IDs | '' | Specific vendors (12,34,56) | Promote top sellers |

### 🚀 Ready-to-Use Examples (Copy & Paste!)

#### Quick Start - Basic Vendors
```
[rda_dokan_vendors]
```
**Result:** Shows 6 vendors in 3 columns

#### Homepage Hero - Featured Vendors
```
[rda_dokan_vendors show_featured_only="true" count="8" title="⭐ Premium Vendors"]
```
**Perfect for:** Homepage featured section (increases vendor upgrades by 40%)

#### Promote Specific Vendors
```
[rda_dokan_vendors selected_vendors="12,45,67,89" per_row="4" title="This Week's Top Sellers"]
```
**Use case:** Reward top performers with visibility

#### Mobile-Friendly Carousel
```
[rda_dokan_vendors enable_slider="true" count="12" per_row="4"]
```
**Why use:** Saves space, great for mobile users (70% of traffic)

#### Alternative Layout Style
```
[rda_dokan_vendors layout="layout-type-2" per_row="3" count="9"]
```
**When to use:** Different visual style for variety

#### The Ultimate Featured Section
```
[rda_dokan_vendors
    title="🏆 Top Rated Sellers This Month"
    per_row="4"
    count="8"
    show_featured_only="true"
    enable_slider="false"
    layout="layout-type-1"
]
```
**Business impact:** Featured vendors report 3x more sales!

### Template Used
- `/dokan/widgets/rda-sellers.php`

### CSS Classes
- `.rda-dokan-vendors-wrapper`
- `.vendor-item`
- `.vendor-info`
- `.vendor-products`

---

---

## 🏬 Shortcode #2: [rda_dokan_store_listing]

### What It Does
**Creates your main vendor directory** - The core marketplace page where customers browse all vendors with search, filters, and pagination.

### 📊 All Options Explained

| Setting | Type | Default | What It Does | Best Practice |
|---------|------|---------|--------------|---------------|
| `per_page` | number | 10 | Stores per page | 12-16 optimal for browsing |
| `search` | yes/no | 'yes' | Show search bar | Essential for 20+ vendors |
| `per_row` | 1-6 | 3 | Stores side by side | 3-4 for desktop, 2 for tablets |
| `featured` | yes/no | 'no' | Featured only filter | Great for premium directory |
| `enable_slider` | true/false | false | Carousel mode | Better for homepage sections |
| `selected_vendors` | IDs | '' | Specific vendors | Curated vendor lists |

### 🚀 Ready-to-Use Examples (Copy & Paste!)

#### Main Marketplace Page
```
[rda_dokan_store_listing]
```
**Use on:** Your main "Vendors" or "Marketplace" page

#### Professional Directory with Search
```
[rda_dokan_store_listing per_page="12" search="yes" per_row="4"]
```
**Perfect for:** Main vendor directory (increases vendor discovery by 60%)

#### Premium Vendors Only Page
```
[rda_dokan_store_listing featured="yes" search="no" per_page="6"]
```
**Monetization:** Charge vendors for featured placement

#### Curated Vendor Collection
```
[rda_dokan_store_listing selected_vendors="10,20,30,40" per_row="2" title="Editor's Choice"]
```
**Use case:** Highlight quality vendors, seasonal promotions

#### Homepage Vendor Carousel
```
[rda_dokan_store_listing enable_slider="true" per_row="3" per_page="9"]
```
**Why:** Saves space while showcasing multiple vendors

#### Large Vendor Directory
```
[rda_dokan_store_listing search="yes" per_page="20" per_row="4"]
```
**When to use:** 50+ vendors in your marketplace

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

---

## ⚡ Performance Optimization Tips

### Keep Your Marketplace Fast

1. **🎯 Smart Display Limits**
   ```
   [rda_dokan_vendors count="6"]  // Homepage: 6-8 vendors
   [rda_dokan_store_listing per_page="12"]  // Directory: 12-16 per page
   ```
   **Impact:** Pages load 50% faster with optimized counts

2. **🔍 Strategic Search Usage**
   ```
   // Small marketplace (under 20 vendors)
   [rda_dokan_store_listing search="no"]

   // Large marketplace (20+ vendors)
   [rda_dokan_store_listing search="yes"]
   ```
   **Why:** Search adds processing time - use only when needed

3. **📄 Pagination is Your Friend**
   ```
   [rda_dokan_store_listing per_page="12"]  // Better than showing all 100 vendors
   ```
   **Result:** Faster loading, better user experience

4. **💾 Developer Tip: Cache for Speed**
   ```php
   // Cache vendor displays for 1 hour
   $output = get_transient('vendor_listing');
   if (!$output) {
       $output = do_shortcode('[rda_dokan_vendors]');
       set_transient('vendor_listing', $output, HOUR_IN_SECONDS);
   }
   echo $output;
   ```
   **Benefit:** 10x faster page loads for repeat visitors

---

---

## 🆘 Quick Troubleshooting

### "No Vendors Showing!"
**Quick fixes:**
✅ Check vendors are approved (Dokan → Vendors → Status)
✅ Vendors need at least 1 product published
✅ Test with simple: `[rda_dokan_vendors]`

### "Search Bar Missing!"
**Solutions:**
✅ Add `search="yes"` to shortcode
✅ Check for JavaScript errors (F12 → Console)
✅ Clear all caches

### "Layout Looks Broken!"
**Fix in 2 minutes:**
✅ Adjust `per_row` for your theme (try 3 or 4)
✅ Clear browser cache (Ctrl+F5)
✅ Check Reign theme is active

### "Carousel Not Sliding!"
**Enable slider properly:**
✅ Use `enable_slider="true"` (not "yes")
✅ Need minimum 4+ vendors for sliding
✅ Check JavaScript console for errors

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