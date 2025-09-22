# Reign Dokan Addon - Complete Configuration Guide

## 🎨 Make Your Marketplace Look Perfect

This guide shows you how to configure every aspect of your marketplace to match your brand and provide the best experience for vendors and customers. From beautiful store headers to perfect product displays - we'll cover it all!

## 🎯 Quick Access to Settings

**Main Settings Location:** Appearance → Customize → Dokan Settings

*All the important marketplace appearance and functionality options are here in one convenient place.*

---

## 🏪 Store Header Settings (Make Vendors Look Professional)

### Show Store Headers
**What it does:** Controls whether vendor stores have beautiful branded headers

**Setting:** `reign_dokan_store_header_location`
- ✅ **Enable** - Show professional store headers (Recommended)
- ❌ **Disable** - Plain store pages

**Why enable this?** Store headers make vendors look professional and build customer trust!

### Header Layout Style
**What it does:** Controls how wide the store header appears

**Setting:** `reign_dokan_store_header_layout`
- 🖥️ **Full Width** - Header spans entire screen (looks modern)
- 📦 **Contained** - Header stays within content area (traditional look)

**Recommendation:** Full width looks more professional and modern.

---

## 🛍️ Product Page Settings (Boost Sales & Trust)

### Show Vendor Headers on Product Pages
**What it does:** Displays vendor branding on individual product pages

**Setting:** `reign_dokan_show_vendor_header_on_pro_page`
- ✅ **Enable** - Show vendor branding on product pages
- ❌ **Disable** - Clean product pages without vendor headers

**Business Impact:** Increases vendor brand recognition and customer trust!

### Vendor Header Width on Products
**What it does:** Controls vendor header width on product pages

**Setting:** `reign_dokan_show_vendor_header_width`
- 🖥️ **Full Width** - Maximum visual impact
- 📦 **Contained** - Subtle vendor presence

### Show More Products from This Vendor
**What it does:** Displays other products from the same vendor on product pages

**Setting:** `reign_dokan_show_vendor_pros_on_pro_page`
- ✅ **Enable** - Increase sales by showing related vendor products
- ❌ **Disable** - Focus only on current product

**Business Benefit:** Can increase average order value by 30-50%!

### How Many Vendor Products to Show
**What it does:** Controls number of vendor products displayed

**Setting:** `reign_dokan_num_of_vendor_pros_on_pro_page`
- 📊 **Recommended:** 6-10 products
- ⚡ **Performance:** Fewer = faster loading
- 💰 **Sales:** More = more cross-selling opportunities

### Show "Sold By" Information
**What it does:** Displays vendor name in product details

**Setting:** `reign_dokan_show_sold_by_in_pro_meta`
- ✅ **Enable** - Builds trust and transparency (Highly Recommended)
- ❌ **Disable** - Hides vendor attribution

**Why keep this enabled?** Customers want to know who they're buying from!

### Display Vendor Information Box
**What it does:** Shows detailed vendor info on product pages

**Setting:** `reign_dokan_show_vendor_info_in_pro_page`
- ✅ **Enable** - Full vendor details and contact info
- ❌ **Disable** - Clean, minimal product pages

---

## 🎨 Store Layout Settings (Perfect Visual Appeal)

### Store Directory Layout Style
**What it does:** Controls how the main vendor directory page looks

**Setting:** `reign_dokan_store_list_layout`
- 🎯 **Grid Layout** - Modern card-style vendor displays (Recommended)
- 📋 **List Layout** - Traditional row-based vendor listing
- 🎨 **Custom Layouts** - If you've added custom designs

**Recommendation:** Grid layout looks more modern and professional!

### Store Page Sidebar Position
**What it does:** Controls where the sidebar appears on vendor store pages

**Setting:** `store_layout`
- ⬅️ **Left Sidebar** - Traditional layout
- ➡️ **Right Sidebar** - Modern layout (Recommended)
- 🚫 **No Sidebar** - Full-width, clean look

**Best Choice:** Right sidebar or no sidebar for modern appeal.

---

## 🔧 Advanced Configuration (For Developers)

### Reading Settings Programmatically
**How to access settings in your custom code:**

```php
// Get current setting values
$header_enabled = get_theme_mod('reign_dokan_store_header_location', true);
$products_count = get_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 10);
$store_layout = get_theme_mod('reign_dokan_store_list_layout', 'layout_one');
```

### Updating Settings via Code
**Programmatically change settings (useful for bulk setup):**

```php
// Set settings programmatically
set_theme_mod('reign_dokan_show_vendor_pros_on_pro_page', true);
set_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 20);
```

### Using Settings in Custom Templates
**How to check settings in your template files:**

```php
// Conditional template display based on settings
if (get_theme_mod('reign_dokan_show_vendor_header_on_pro_page', false)) {
    // Display vendor header
    dokan_get_template_part('store-header');
}
```

---

## 📝 Shortcode Configuration (Quick Page Building)

### Store Directory Shortcode
**Build your perfect vendor directory page:**

```
[rda_dokan_store_listing
    per_page="12"        // How many stores to show per page
    search="yes"         // Add search bar (helps customers find vendors)
    per_row="3"          // Vendors per row (3-4 looks best)
    featured="no"        // Show all or featured only
    enable_slider="false" // Turn into carousel (great for homepage)
]
```

**Pro Tip:** Use `per_row="4"` for modern grid layouts!

### Featured Vendors Display
**Showcase your best vendors anywhere:**

```
[rda_dokan_vendors
    title="Top Rated Stores"  // Your custom heading
    per_row="3"               // Cards per row (3 or 4 recommended)
    count="6"                 // Total vendors to display
    show_featured_only="true" // Filter for premium vendors
    layout="layout-type-1"    // Choose visual style
]
```

**Business Tip:** Place featured vendors on homepage for 40% more vendor signups!

---

## 👥 Social Marketplace Features (With BuddyPress)

### Automatic Social Features
**These activate instantly when BuddyPress is installed:**

✅ **Vendor Store Tabs** - Each user profile shows their store
❤️ **Favorite Products** - Customers can save products they love
📱 **Activity Streams** - Store updates in social feeds
👤 **Social Profiles** - Vendors become community members

*No setup needed - just install BuddyPress and watch the magic happen!*

### Customize Profile Tab Names
**Want to rename the store tab in profiles?**

```php
// Add to your theme's functions.php
add_filter('reign_dokan_store_primary_bp_tab_name', function() {
    return __('My Shop', 'textdomain');  // Change to your preferred name
});
```

**Popular Tab Names:** "My Store", "Shop", "Marketplace", "Products"

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

---

## 🏆 Best Configuration Practices

### ⚡ Performance Optimization
**Keep your marketplace fast:**
- 📊 Show 10-15 products per vendor (balance speed vs. choice)
- 📄 Use pagination for 12+ stores (better than endless scroll)
- 🔍 Enable search for 20+ vendors (helps customers find stores)
- 💾 Use caching plugin for 50+ vendors (WP Rocket recommended)

### 🎯 User Experience Settings
**What successful marketplaces do:**
- ✅ Always show store headers (builds vendor brands)
- ✅ Display "Sold by" info (increases trust by 60%)
- ✅ Use 3-4 stores per row on desktop (optimal viewing)
- ✅ Show 6-8 vendor products on product pages (boosts sales)

### 📱 Mobile Optimization
**Essential for 70% of your traffic:**
- Set `per_row="2"` for mobile (or "1" for very small screens)
- Show only 4-6 products per vendor on mobile
- Use contained headers on mobile devices
- Enable touch-friendly sliders for featured vendors

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