# Reign Dokan Addon - Configuration Guide

## Theme Customizer Settings

### Access Customizer Options

```
Appearance > Customize > Reign Dokan Settings
```

## Store Listing Configuration

### Layout Options

#### Grid Layout Settings

```php
// Customizer settings
'reign_dokan_store_layout' => array(
    'type'    => 'select',
    'choices' => array(
        'grid' => 'Grid View',
        'list' => 'List View',
    ),
    'default' => 'grid'
)
```

**Grid Configuration:**

| Setting | Options | Default | Description |
|---------|---------|---------|-------------|
| Columns Desktop | 2, 3, 4 | 3 | Store cards per row on desktop |
| Columns Tablet | 1, 2 | 2 | Store cards per row on tablet |
| Columns Mobile | 1 | 1 | Store cards per row on mobile |
| Items Per Page | 6, 9, 12, 15, 18 | 12 | Stores shown per page |
| Card Style | Classic, Modern, Minimal | Modern | Store card design style |

#### List Layout Settings

```php
// List view specific options
'reign_dokan_list_style' => array(
    'compact'  => 'Compact List',
    'detailed' => 'Detailed List',
    'table'    => 'Table View'
)
```

### Store Card Elements

Toggle display of elements in store listings:

```
Customizer > Reign Dokan > Store Card Elements
```

- ☑ **Store Banner** - Featured image/banner
- ☑ **Store Logo** - Vendor logo/avatar  
- ☑ **Store Name** - Vendor store title
- ☑ **Store Rating** - Star ratings
- ☑ **Product Count** - Number of products
- ☑ **Store Address** - Location info
- ☑ **Featured Badge** - For featured vendors
- ☑ **Online Status** - Show if vendor online
- ☑ **Store Categories** - Product categories
- ☑ **Visit Store Button** - CTA button

## Single Store Page Configuration

### Store Header Styles

#### Style 1: Classic Header
```css
.store-header-classic {
    banner: full-width;
    logo: left-aligned;
    info: below-banner;
}
```

#### Style 2: Modern Header
```css
.store-header-modern {
    banner: contained;
    logo: overlay-center;
    info: overlay-bottom;
}
```

#### Style 3: Minimal Header
```css
.store-header-minimal {
    banner: none;
    logo: inline;
    info: single-row;
}
```

### Store Sidebar Configuration

```php
// Sidebar position options
'reign_dokan_sidebar_position' => array(
    'left'  => 'Left Sidebar',
    'right' => 'Right Sidebar', 
    'none'  => 'No Sidebar'
)
```

**Available Widgets:**
- Store Info
- Store Location/Map
- Store Categories
- Best Selling Products
- Featured Products
- Store Contact Form
- Store Opening Hours
- Store Policies

### Store Tabs Configuration

```php
// Enable/disable store tabs
'reign_dokan_store_tabs' => array(
    'products' => true,
    'reviews'  => true,
    'terms'    => true,
    'support'  => true
)
```

## Vendor Dashboard Settings

### Dashboard Menu Items

```php
// Control dashboard menu
add_filter('dokan_get_dashboard_nav', function($menus) {
    // Customize menu items
    return $menus;
});
```

**Default Menu Structure:**
```
Dashboard
├── Products
│   ├── All Products
│   └── Add New
├── Orders
├── Coupons
├── Reports
├── Reviews
├── Withdraw
├── Store Settings
└── Payment Settings
```

### Dashboard Widgets

```php
// Widget areas
'reign_dokan_dashboard_widgets' => array(
    'sales_overview'    => true,
    'recent_orders'     => true,
    'product_stats'     => true,
    'review_summary'    => true,
    'announcement'      => true
)
```

## Color Customization

### Primary Colors

```css
/* Customizer color settings */
--reign-dokan-primary: #3498db;
--reign-dokan-secondary: #2ecc71;
--reign-dokan-accent: #e74c3c;
--reign-dokan-text: #2c3e50;
--reign-dokan-border: #ecf0f1;
```

### Component-Specific Colors

```php
// Store elements
'store_banner_overlay'    => 'rgba(0,0,0,0.3)',
'store_rating_color'      => '#ffb400',
'featured_badge_bg'       => '#ff6b6b',
'online_indicator'        => '#00d084',
'sold_count_color'        => '#8b8b8b'
```

## Typography Settings

### Font Configuration

```php
'reign_dokan_typography' => array(
    'store_title' => array(
        'font-family' => 'inherit',
        'font-size'   => '24px',
        'font-weight' => '600',
        'line-height' => '1.4'
    ),
    'product_title' => array(
        'font-family' => 'inherit',
        'font-size'   => '16px',
        'font-weight' => '500'
    )
)
```

## BuddyPress Integration Settings

### Profile Integration

```php
// Enable store tab in BuddyPress profile
'reign_dokan_bp_integration' => true,

// Tab position
'reign_dokan_bp_tab_position' => 30,

// Tab visibility
'reign_dokan_bp_tab_visibility' => 'public'
```

### Activity Stream Integration

```php
// Activity types
'reign_dokan_activities' => array(
    'new_product'    => true,
    'new_review'     => true,
    'store_updated'  => false,
    'product_sold'   => false
)
```

## Advanced Configuration

### Custom CSS

```css
/* Add via Customizer > Additional CSS */

/* Store listing customization */
.dokan-store-wrap.reign-grid {
    gap: 30px;
}

/* Store card hover effect */
.reign-store-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

/* Custom badge */
.reign-featured-vendor::before {
    content: 'FEATURED';
    position: absolute;
    top: 10px;
    right: 10px;
    background: #ff6b6b;
    color: white;
    padding: 5px 10px;
    font-size: 11px;
    border-radius: 3px;
}
```

### PHP Hooks Configuration

```php
// functions.php customization

// Modify store listing query
add_filter('dokan_store_listing_args', function($args) {
    $args['orderby'] = 'registered';
    $args['order'] = 'DESC';
    return $args;
});

// Add custom store meta
add_action('reign_dokan_store_card_footer', function($vendor_id) {
    $verified = get_user_meta($vendor_id, 'dokan_verification', true);
    if ($verified) {
        echo '<span class="verified-badge">Verified</span>';
    }
});

// Customize products per page
add_filter('dokan_store_products_per_page', function() {
    return 24;
});
```

## Performance Settings

### Lazy Loading

```php
'reign_dokan_lazy_load' => array(
    'images'   => true,
    'products' => true,
    'reviews'  => false
)
```

### Cache Settings

```php
// Cache duration in seconds
'reign_dokan_cache' => array(
    'store_list'    => 3600,  // 1 hour
    'store_data'    => 1800,  // 30 minutes
    'product_data'  => 900,   // 15 minutes
)
```

## Mobile-Specific Settings

### Mobile Layout Options

```php
'reign_dokan_mobile' => array(
    'simplified_header' => true,
    'touch_friendly'    => true,
    'infinite_scroll'   => false,
    'compact_view'      => true
)
```

### Responsive Breakpoints

```css
/* Customizable breakpoints */
@media (max-width: 768px) { /* Tablet */ }
@media (max-width: 480px) { /* Mobile */ }
```

## SEO Configuration

### Meta Tags

```php
// Store page meta
'reign_dokan_seo' => array(
    'store_title_format' => '%store_name% - %site_name%',
    'meta_description'   => true,
    'og_tags'           => true,
    'schema_markup'     => true
)
```

## Widget Areas

### Register Widget Areas

```php
// Available widget areas
'Store Listing Top'
'Store Listing Bottom'
'Store Sidebar'
'Store Header'
'Vendor Dashboard Sidebar'
```

## Email Notification Settings

### Customize Email Templates

```php
// Email customization
add_filter('dokan_email_heading', function($heading, $email) {
    // Customize email headings
    return $heading;
}, 10, 2);
```

## Import/Export Settings

### Export Configuration

```bash
# Export settings via WP-CLI
wp option get reign_dokan_settings --format=json > dokan-settings.json
```

### Import Configuration

```bash
# Import settings
wp option update reign_dokan_settings --format=json < dokan-settings.json
```

## Complete Reign Dokan Settings

### Main Settings Location

**Access all Reign Dokan settings:**
```
WP Admin > Reign Settings > Dokan
```

### Store Header Configuration

**Set Store Header Location:**
- Above store banner
- Below store banner
- Inside banner overlay
- Custom position via hook

### Product Search in Header

**Enable product search:**
```php
// Add to header
add_action('reign_header_icons_group', 'reign_dokan_product_search');
```

### BuddyPress Features

#### Show Products on Vendor BP Profile

**Enable setting:**
```
Reign Settings > Dokan > Show product on Registered Vendor's BP Profile
```

Adds products tab to vendor's BuddyPress profile.

#### BP Activity on Product Creation

**Enable activity:**
```
Reign Settings > Dokan > Create Product Activity
```

Features:
- Posts activity when vendor publishes product
- Shows product image and price
- Links to product page

#### BP Activity on Product Review

**Enable review activity:**
```
Reign Settings > Dokan > Add Review Activity
```

Creates activity when customers review products.

### Favorite Products Feature

#### Mark Products as Favorite

**Enable favorites:**
```
Reign Settings > Dokan > Mark Products as Favourite
```

Features:
- Heart icon on products
- Favorites tab in BP profile
- Activity stream integration
- Customizable tab settings

**Configuration options:**
```php
function reign_dokan_favorite_settings() {
    return array(
        'tab_label' => 'My Favorites',
        'tab_slug' => 'favorites',
        'tab_position' => 30,
        'show_count' => true,
        'activity_enabled' => true
    );
}
```

### Product Page Settings

**Configure product pages:**
```
Reign Settings > Dokan > Product Page Settings
```

Options:
- Vendor info position
- More products section
- Store location display
- Contact vendor button

### Withdraw Options

**Configure withdrawals:**
```
Dokan > Settings > Withdraw
```

| Method | Min Amount | Schedule | Auto |
|--------|-----------|----------|------|
| PayPal | $50 | Weekly | Yes |
| Bank | $100 | Monthly | No |
| Stripe | $25 | Instant | Yes |

### Store Page Appearance

**Set store header template:**
```
Dokan > Settings > Appearance
```

Options:
- Default (banner + info)
- Compact (minimal)
- Extended (with tabs)
- Custom template

**Vendor Setup Wizard Logo:**
- Size: 270px × 90px
- Falls back to site title

### Widget Configuration

#### How to Set Widgets

**Add vendor widgets:**
```
Appearance > Widgets > Dokan Store Sidebar
```

**Available Reign widgets:**
- Reign: Vendors (4 layouts)
- Reign: Store Info
- Reign: Top Products
- Reign: Store Categories

#### Widget Layouts

1. **Layout 1:** Grid with overlay
2. **Layout 2:** List with details
3. **Layout 3:** Carousel slider
4. **Layout 4:** Compact cards

### Elementor Integration

#### Single Store with Elementor

1. Enable Dokan Elementor module
2. Templates > Add New > Single Store
3. Use Dokan Elementor widgets
4. Customize and publish

#### Reign Vendor Listing Widget

**Setup Elementor widget:**
- Drag Reign Vendor widget
- Configure display options
- Set responsive columns
- Apply Elementor styling

### StoreMate Compatibility

#### Available Shortcodes

```
[rda_dokan_vendors
    count="6"
    per_row="3"
    show_featured_only="1"
    layout="layout-type-1"]

[rda_dokan_store_listing
    per_page="10"
    featured="yes"
    selected_vendors="1,2,3"]
```

#### StoreMate Filters

```php
// Customize store listing
add_filter('rda_dokan_store_listing_per_page', function($num) {
    return 20;
});

// Override templates
add_filter('reign_dokan_locate_template', function($template, $name) {
    // Custom template logic
    return $template;
}, 10, 2);
```

### Single Cart Icon

**Configure unified cart:**
```
Reign Settings > Dokan > Single Cart Icon
```

Features:
- Combine vendor carts
- Show total items
- Mini cart preview
- Vendor grouping

### Template Overrides

**Templates overridden by addon:**
- `store-listing.php`
- `store-header.php`
- `store-sidebar.php`
- `vendor-products.php`
- `store-toc.php`

**Override location:**
```
/themes/reign-child/dokan/
```

### System Requirements

**Minimum:**
- WordPress 5.0+
- Reign Theme (latest)
- Dokan Lite 3.0+
- WooCommerce 4.0+
- PHP 7.2+
- Memory: 256MB

**Recommended:**
- PHP 8.0+
- Memory: 512MB
- MySQL 5.7+

## Troubleshooting Configuration

### Debug Mode

```php
// Enable debug mode
define('REIGN_DOKAN_DEBUG', true);

// Log configuration issues
if (REIGN_DOKAN_DEBUG) {
    error_log('Reign Dokan Config: ' . print_r($config, true));
}
```

## Next Steps

- [Store Customization](04-store-customization.md) - Customize individual stores
- [Developer Guide](05-developer-guide.md) - Advanced development
- [Troubleshooting](06-troubleshooting.md) - Common issues