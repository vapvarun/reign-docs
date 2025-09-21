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