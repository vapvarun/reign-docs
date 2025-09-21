# Reign Dokan Addon - Shortcodes Reference

## What You'll Find Here
A complete guide to all shortcodes available with the Reign Dokan addon. Copy, paste, and customize these shortcodes to display marketplace content exactly how you want it.

## Quick Overview
**Total shortcodes:** 30+ powerful options
**Difficulty:** Easy - just copy and paste!
**Pro tip:** Test shortcodes on a draft page first

---

## Part 1: Store Display Shortcodes

### Store Listing Grid

**Display all vendor stores:**

```
[dokan-stores]
```

**With parameters:**

```
[dokan-stores 
    per_page="12"
    columns="3"
    search="yes"
    category="yes"
    featured="yes"]
```

**All parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `per_page` | Number | 10 | Stores per page |
| `columns` | 1-6 | 3 | Grid columns |
| `search` | yes/no | yes | Show search bar |
| `category` | yes/no | yes | Category filter |
| `featured` | yes/no | no | Featured only |
| `order` | ASC/DESC | ASC | Sort order |
| `orderby` | name/date/random | name | Sort by |
| `with_products_only` | yes/no | no | Hide empty stores |

### Featured Stores

**Show only featured vendors:**

```
[dokan-stores featured="yes" per_page="6" columns="3"]
```

### Best Selling Vendors

**Display top performing stores:**

```
[dokan-best-selling-vendor 
    no_of_vendor="8"
    title="Top Sellers"]
```

---

## Part 2: Product Display Shortcodes

### Vendor Products

**Show products from specific vendor:**

```
[dokan-vendor-products 
    vendor_id="5"
    per_page="12"
    columns="4"]
```

### Best Selling Products

**Marketplace best sellers:**

```
[dokan-best-selling-product 
    no_of_product="8"
    columns="4"
    title="Best Sellers"]
```

### Top Rated Products

**Highest rated products:**

```
[dokan-top-rated-product 
    no_of_product="8"
    title="Top Rated"]
```

**Product parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `no_of_product` | Number | 8 | Products to show |
| `columns` | 1-6 | 4 | Grid columns |
| `title` | Text | blank | Section title |
| `vendor_id` | Number | all | Specific vendor |
| `category` | Slug | all | Product category |

---

## Part 3: Vendor Dashboard Shortcodes

### Vendor Dashboard

**Complete vendor dashboard:**

```
[dokan-dashboard]
```

**Dashboard includes:**
- Sales overview
- Product management
- Orders management
- Withdrawal requests
- Store settings
- Reports

### Vendor Registration

**Vendor signup form:**

```
[dokan-vendor-registration]
```

**Custom registration:**

```
[dokan-vendor-registration 
    role="seller"
    redirect="/vendor-dashboard/"]
```

---

## Part 4: Customer Account Shortcodes

### Customer Dashboard

**Customer order tracking:**

```
[dokan-customer-dashboard]
```

### Customer Migration

**Convert customer to vendor:**

```
[dokan-customer-migration]
```

**Migration form parameters:**

```
[dokan-customer-migration 
    title="Become a Seller"
    button_text="Start Selling"]
```

---

## Part 5: Store Components

### Store Header

**Display store banner and info:**

```
[dokan-store-header vendor_id="5"]
```

### Store Products

**Products from current store:**

```
[dokan-store-products]
```

### Store Categories

**Vendor's product categories:**

```
[dokan-store-categories 
    vendor_id="5"
    show_count="yes"]
```

### Store Contact Form

**Contact vendor form:**

```
[dokan-store-contact vendor_id="5"]
```

---

## Part 6: Marketplace Statistics

### Vendor Count

**Total number of vendors:**

```
[dokan-vendor-count]
```

**With custom text:**

```
[dokan-vendor-count 
    before="We have "
    after=" amazing vendors!"]
```

### Product Count

**Total marketplace products:**

```
[dokan-product-count]
```

### Sales Statistics

**Marketplace overview:**

```
[dokan-marketplace-stats 
    show_vendors="yes"
    show_products="yes"
    show_orders="yes"]
```

---

## Part 7: Search & Filter Shortcodes

### Store Search

**Vendor search form:**

```
[dokan-store-search 
    placeholder="Search stores..."
    button_text="Search"]
```

### Product Search

**Search with vendor filter:**

```
[dokan-product-search 
    show_vendor_filter="yes"
    show_category_filter="yes"]
```

### Location Filter

**Search by location:**

```
[dokan-store-location-filter 
    show_map="yes"
    radius_search="yes"]
```

---

## Part 8: Geolocation Shortcodes

### Store Map

**Display all vendors on map:**

```
[dokan-stores-map 
    width="100%"
    height="400px"
    zoom="12"]
```

**Map parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `width` | px/% | 100% | Map width |
| `height` | px | 400px | Map height |
| `zoom` | 1-20 | 12 | Zoom level |
| `center_lat` | Number | auto | Center latitude |
| `center_lng` | Number | auto | Center longitude |

### Vendor Location

**Single vendor map:**

```
[dokan-vendor-location 
    vendor_id="5"
    height="300px"]
```

---

## Part 9: Vendor Application

### Application Form

**Vendor application process:**

```
[dokan-vendor-application]
```

### Application Status

**Check application status:**

```
[dokan-application-status]
```

---

## Part 10: Social & Reviews

### Store Reviews

**Display vendor reviews:**

```
[dokan-store-reviews 
    vendor_id="5"
    per_page="10"]
```

### Review Form

**Add review for vendor:**

```
[dokan-store-review-form vendor_id="5"]
```

### Social Links

**Vendor social profiles:**

```
[dokan-store-social 
    vendor_id="5"
    show_icons="yes"]
```

---

## Part 11: Subscription Shortcodes

### Subscription Packs

**Display membership plans:**

```
[dokan-subscription-packs]
```

**Custom pack display:**

```
[dokan-subscription-packs 
    columns="3"
    featured_first="yes"
    show_free="no"]
```

### Current Subscription

**Vendor's active subscription:**

```
[dokan-my-subscription]
```

---

## Part 12: Vendor Widgets

### Top Vendors

**Sidebar widget for top vendors:**

```
[dokan-top-vendors 
    count="5"
    show_avatar="yes"
    show_rating="yes"]
```

### Recent Products

**Latest vendor products:**

```
[dokan-recent-products 
    vendor_id="5"
    count="6"
    columns="2"]
```

### Store Info

**Vendor information widget:**

```
[dokan-store-info 
    vendor_id="5"
    show_banner="yes"
    show_rating="yes"
    show_location="yes"]
```

---

## Part 13: Advanced Combinations

### Complete Marketplace Homepage

```html
<!-- Hero Section -->
<div class="marketplace-hero">
    <h1>Welcome to Our Marketplace</h1>
    [dokan-store-search]
</div>

<!-- Stats -->
[dokan-marketplace-stats]

<!-- Featured Vendors -->
<h2>Featured Stores</h2>
[dokan-stores featured="yes" per_page="6" columns="3"]

<!-- Best Sellers -->
[dokan-best-selling-product no_of_product="8" title="Best Selling Products"]

<!-- Top Rated -->
[dokan-top-rated-product no_of_product="8" title="Customer Favorites"]

<!-- All Stores -->
<h2>Browse All Stores</h2>
[dokan-stores per_page="12" columns="4"]
```

### Vendor Landing Page

```html
<!-- Store Header -->
[dokan-store-header vendor_id="5"]

<!-- Store Categories -->
<div class="store-categories">
    [dokan-store-categories vendor_id="5"]
</div>

<!-- Store Products -->
[dokan-vendor-products vendor_id="5" per_page="12"]

<!-- Store Reviews -->
<h3>Customer Reviews</h3>
[dokan-store-reviews vendor_id="5"]

<!-- Contact Form -->
<h3>Contact Vendor</h3>
[dokan-store-contact vendor_id="5"]
```

### Category Page

```html
<!-- Category Header -->
<h1>Electronics Stores</h1>

<!-- Stores in Category -->
[dokan-stores category="electronics" per_page="12"]

<!-- Products from Category -->
[dokan-vendor-products category="electronics"]
```

---

## Part 14: Mobile Optimized Shortcodes

### Mobile Store Grid

```
[dokan-stores 
    columns="1" 
    per_page="10"
    search="yes"]
```

### Mobile Product Display

```
[dokan-vendor-products 
    columns="2"
    per_page="8"]
```

---

## Part 15: Conditional Shortcodes

### Vendor Only Content

**Show to vendors only:**

```php
[dokan-if-vendor]
    [dokan-dashboard]
[/dokan-if-vendor]
```

### Customer Only Content

**Show to customers only:**

```php
[dokan-if-customer]
    [dokan-customer-migration]
[/dokan-if-customer]
```

### Guest Only Content

**Show to non-logged users:**

```php
[dokan-if-guest]
    [dokan-vendor-registration]
[/dokan-if-guest]
```

---

## Part 16: Custom Queries

### Custom Vendor Query

```
[dokan-stores 
    orderby="total_sales"
    order="DESC"
    meta_key="store_rating"
    meta_value="4"
    meta_compare=">="]
```

### Custom Product Query

```
[dokan-vendor-products 
    meta_key="featured"
    meta_value="yes"
    orderby="price"
    order="ASC"]
```

---

## Styling Shortcode Output

### Custom CSS Classes

```
[dokan-stores 
    css_class="custom-vendor-grid"
    wrapper_class="marketplace-section"]
```

### Custom Styling Examples

```css
/* Custom vendor grid */
.custom-vendor-grid {
    background: #f5f5f5;
    padding: 20px;
    border-radius: 10px;
}

.custom-vendor-grid .store-wrapper {
    transition: transform 0.3s;
}

.custom-vendor-grid .store-wrapper:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 20px rgba(0,0,0,0.1);
}

/* Mobile responsive */
@media (max-width: 768px) {
    .custom-vendor-grid {
        grid-template-columns: 1fr !important;
    }
}
```

---

## Troubleshooting Shortcodes

### Common Issues

**"Shortcode not displaying"**
- Check Dokan is activated
- Verify shortcode spelling
- Clear cache
- Check user permissions

**"No vendors showing"**
- Verify vendors are approved
- Check vendor products exist
- Test without filters first

**"Dashboard access denied"**
- Verify user role
- Check Dokan settings
- Clear browser cookies

### Testing Best Practices

1. Test on draft page first
2. Start with basic shortcode
3. Add parameters gradually
4. Check mobile display
5. Test with different user roles

---

## Performance Tips

### Optimize Shortcode Usage

**Do's:**
- Cache shortcode output
- Limit items per page
- Use pagination
- Lazy load images

**Don'ts:**
- Multiple complex shortcodes per page
- Unlimited product displays
- Nested shortcodes
- Skip pagination

### Caching Considerations

```php
// Cache vendor list
add_filter('dokan_store_listing_cache', '__return_true');
add_filter('dokan_store_cache_time', function() {
    return 3600; // 1 hour
});
```

---

## Advanced Tips

### Dynamic Parameters

**Use URL parameters:**

```
[dokan-stores category="{url_param:cat}"]
```

**Current vendor products:**

```
[dokan-vendor-products vendor_id="current"]
```

### Integration with Page Builders

**Elementor:**
- Use shortcode widget
- Apply custom styling
- Add animations

**Gutenberg:**
- Use shortcode block
- Wrap in groups
- Apply block styles

**WPBakery:**
- Raw HTML module
- Custom CSS box
- Responsive settings

---

## Quick Copy Templates

### Marketplace Homepage

```html
<div class="marketplace-home">
    <!-- Search -->
    [dokan-store-search]
    
    <!-- Stats -->
    [dokan-marketplace-stats]
    
    <!-- Featured -->
    [dokan-stores featured="yes" per_page="6"]
    
    <!-- Products -->
    [dokan-best-selling-product]
</div>
```

### Vendor Page Sidebar

```html
<!-- Store Info -->
[dokan-store-info vendor_id="current"]

<!-- Categories -->
[dokan-store-categories vendor_id="current"]

<!-- Contact -->
[dokan-store-contact vendor_id="current"]
```

### Footer Widgets

```html
<!-- Top Vendors -->
[dokan-top-vendors count="5"]

<!-- Recent Products -->
[dokan-recent-products count="4"]

<!-- Stats -->
[dokan-vendor-count]
```

---

## Custom Shortcode Creation

### Create Your Own

```php
function my_custom_vendor_grid() {
    return do_shortcode('[dokan-stores 
        featured="yes" 
        per_page="8" 
        columns="4"]');
}
add_shortcode('my_vendor_grid', 'my_custom_vendor_grid');

// Use: [my_vendor_grid]
```

---

**Pro Tips:**

💡 **Save favorite combinations** in a text file for reuse

🚀 **Test on staging** site first for complex layouts

🎨 **Combine with CSS** for unique designs

📱 **Always check mobile** view for responsive display

⏰ **Consider caching** for better performance

---

**Need Help with Shortcodes?**
📧 Email: support@wbcomdesigns.com
📚 Full docs: docs.wbcomdesigns.com/dokan
💬 Community: facebook.com/groups/wbcom
🎥 Video tutorials available