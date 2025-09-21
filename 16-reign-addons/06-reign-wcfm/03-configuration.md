# Reign WCFM Addon - Configuration Guide

## Theme Customizer Settings

### Access Customizer Options

```
Appearance > Customize > Reign WCFM Settings
```

## Store Listing Configuration

### Layout Options

#### Grid Layout Settings

```php
// Customizer settings
'reign_wcfm_store_layout' => array(
    'type'    => 'select',
    'choices' => array(
        'grid' => 'Grid View',
        'list' => 'List View',
        'map'  => 'Map View'
    ),
    'default' => 'grid'
)
```

**Grid Configuration:**

| Setting | Options | Default | Description |
|---------|---------|---------|-------------|
| Columns Desktop | 2, 3, 4 | 3 | Stores per row on desktop |
| Columns Tablet | 1, 2 | 2 | Stores per row on tablet |
| Columns Mobile | 1 | 1 | Stores per row on mobile |
| Items Per Page | 9, 12, 15, 18, 21 | 12 | Stores shown per page |
| Card Style | Classic, Modern, Minimal | Modern | Store card design style |

### Store Card Elements

Toggle display of elements in store listings:

```
Customizer > Reign WCFM > Store Card Elements
```

- ✓ **Store Banner** - Featured image/banner
- ✓ **Store Logo** - Vendor logo/avatar
- ✓ **Store Name** - Vendor store title
- ✓ **Store Rating** - Average rating stars
- ✓ **Product Count** - Total products
- ✓ **Store Address** - Location information
- ✓ **Featured Badge** - Premium vendors
- ✓ **Online Status** - Vendor availability
- ✓ **Store Categories** - Main categories
- ✓ **Visit Store Button** - CTA button
- ✓ **Social Links** - Social media icons

## Single Store Page Configuration

### Store Header Styles

```php
'reign_wcfm_store_header' => array(
    'classic'  => 'Classic Header',
    'modern'   => 'Modern Overlay',
    'minimal'  => 'Minimal Header',
    'custom'   => 'Custom Template'
)
```

### Store Sidebar Configuration

```php
// Sidebar position options
'reign_wcfm_sidebar_position' => array(
    'left'  => 'Left Sidebar',
    'right' => 'Right Sidebar',
    'none'  => 'No Sidebar'
)
```

**Available Widgets:**
- Store Information
- Store Location/Map
- Store Categories
- Best Selling Products
- Featured Products  
- Store Contact Form
- Store Hours
- Store Policies
- Vendor Biography

### Store Tabs Configuration

```php
// Enable/disable store tabs
'reign_wcfm_store_tabs' => array(
    'products'  => true,
    'about'     => true,
    'policies'  => true,
    'reviews'   => true,
    'followers' => true,
    'enquiry'   => true
)
```

## Vendor Dashboard Settings

### Dashboard Layout

```php
'reign_wcfm_dashboard_layout' => array(
    'default'  => 'WCFM Default',
    'reign'    => 'Reign Enhanced',
    'compact'  => 'Compact View',
    'expanded' => 'Expanded View'
)
```

### Dashboard Menu Configuration

```php
// Customize dashboard menu
add_filter('wcfm_menus', function($menus) {
    // Menu customization
    $menus['dashboard']['label'] = __('Overview', 'reign-wcfm');
    $menus['products']['priority'] = 10;
    $menus['orders']['priority'] = 20;
    
    // Add custom menu item
    $menus['custom'] = array(
        'label' => __('Custom', 'reign-wcfm'),
        'url' => wcfm_get_endpoint_url('custom'),
        'icon' => 'fas fa-star',
        'priority' => 100
    );
    
    return $menus;
});
```

### Dashboard Widgets

```php
// Widget configuration
'reign_wcfm_dashboard_widgets' => array(
    'sales_stats'       => true,
    'order_stats'       => true,
    'product_stats'     => true,
    'review_stats'      => true,
    'visitor_stats'     => true,
    'commission_stats'  => true,
    'withdrawal_stats'  => true,
    'notification'      => true
)
```

## Commission Configuration

### Commission Types

```php
'reign_wcfm_commission' => array(
    'mode' => 'percent', // percent, fixed, percent_fixed
    'percent' => 10,
    'fixed' => 2,
    'tax_enable' => 'yes',
    'shipping_enable' => 'yes'
)
```

### Vendor-Specific Commission

```php
// Set individual vendor commission
add_filter('wcfm_commission_rule', function($commission_rule, $vendor_id, $product_id) {
    // Premium vendors get better rates
    if (get_user_meta($vendor_id, 'premium_vendor', true)) {
        $commission_rule['percent'] = 5; // Lower commission for premium
    }
    
    // Category-based commission
    $product_cats = wp_get_post_terms($product_id, 'product_cat', array('fields' => 'ids'));
    if (in_array(15, $product_cats)) { // Electronics category
        $commission_rule['percent'] = 8;
    }
    
    return $commission_rule;
}, 10, 3);
```

## Color Customization

### Primary Colors

```css
/* Customizer color settings */
--reign-wcfm-primary: #2c3e50;
--reign-wcfm-secondary: #3498db;
--reign-wcfm-accent: #e74c3c;
--reign-wcfm-success: #27ae60;
--reign-wcfm-border: #ecf0f1;
```

### Component-Specific Colors

```php
'store_elements_colors' => array(
    'store_banner_overlay'    => 'rgba(0,0,0,0.3)',
    'store_rating_color'      => '#ffb400',
    'featured_badge_bg'       => '#ff6b6b',
    'online_indicator'        => '#00d084',
    'sold_count_color'        => '#8b8b8b',
    'dashboard_header_bg'     => '#2c3e50'
)
```

## Typography Settings

### Font Configuration

```php
'reign_wcfm_typography' => array(
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
    ),
    'dashboard_heading' => array(
        'font-family' => 'inherit',
        'font-size'   => '20px',
        'font-weight' => '600'
    )
)
```

## BuddyPress Integration Settings

### Profile Integration

```php
// Enable store tab in BuddyPress profile
'reign_wcfm_bp_integration' => true,

// Tab position
'reign_wcfm_bp_tab_position' => 40,

// Tab visibility
'reign_wcfm_bp_tab_visibility' => 'public',

// Show sub-tabs
'reign_wcfm_bp_subtabs' => array(
    'products'    => true,
    'reviews'     => true,
    'followers'   => true,
    'about'       => true
)
```

### Activity Stream Integration

```php
// Activity types
'reign_wcfm_activities' => array(
    'new_product'      => true,
    'product_update'   => false,
    'new_coupon'       => true,
    'store_review'     => true,
    'store_follower'   => true,
    'product_sold'     => false
)
```

## Email Notification Settings

### Email Templates

```php
'reign_wcfm_emails' => array(
    'vendor_new_order' => array(
        'enabled' => true,
        'subject' => 'New order #{order_number}',
        'heading' => 'New Order Received'
    ),
    'vendor_commission_invoice' => array(
        'enabled' => true,
        'subject' => 'Commission Invoice #{invoice_number}',
        'heading' => 'Commission Invoice'
    ),
    'withdrawal_request_approved' => array(
        'enabled' => true,
        'subject' => 'Withdrawal Request Approved',
        'heading' => 'Your withdrawal has been processed'
    )
)
```

## Membership Configuration

### Membership Plans

```php
'reign_wcfm_membership' => array(
    'enable' => true,
    'trial_period' => 14, // days
    'renewal_notification' => 7, // days before expiry
    'auto_renewal' => true,
    'plan_change' => 'immediate' // or 'next_cycle'
)
```

### Plan Features Matrix

```php
// Define plan features
$membership_features = array(
    'basic' => array(
        'product_limit' => 50,
        'gallery_images' => 5,
        'commission' => 15,
        'withdrawal' => 'weekly',
        'support' => 'standard'
    ),
    'premium' => array(
        'product_limit' => 500,
        'gallery_images' => 10,
        'commission' => 10,
        'withdrawal' => 'daily',
        'support' => 'priority'
    ),
    'enterprise' => array(
        'product_limit' => -1, // unlimited
        'gallery_images' => -1,
        'commission' => 5,
        'withdrawal' => 'instant',
        'support' => 'dedicated'
    )
);
```

## Advanced Configuration

### Custom CSS

```css
/* Add via Customizer > Additional CSS */

/* Store listing customization */
.wcfm-store-wrap.reign-grid {
    gap: 30px;
}

/* Store card hover effect */
.reign-store-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

/* Dashboard customization */
.wcfm_dashboard_reign {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
```

### PHP Hooks Configuration

```php
// Modify store query
add_filter('wcfmmp_stores_query_args', function($args) {
    // Show only approved vendors
    $args['meta_query'][] = array(
        'key' => 'store_approved',
        'value' => 'yes'
    );
    
    // Sort by rating
    $args['orderby'] = 'meta_value_num';
    $args['meta_key'] = '_wcfmmp_avg_review_rating';
    $args['order'] = 'DESC';
    
    return $args;
});

// Add custom store data
add_action('reign_wcfm_store_card_footer', function($vendor_id) {
    $verified = get_user_meta($vendor_id, 'wcfm_verification', true);
    if ($verified) {
        echo '<span class="verified-badge">Verified</span>';
    }
});
```

## Performance Settings

### Caching Options

```php
'reign_wcfm_cache' => array(
    'store_list'      => 3600,  // 1 hour
    'store_data'      => 1800,  // 30 minutes
    'product_data'    => 900,   // 15 minutes
    'commission_data' => 7200   // 2 hours
)
```

### Lazy Loading

```php
'reign_wcfm_lazy_load' => array(
    'images'    => true,
    'products'  => true,
    'reviews'   => false,
    'stores'    => true
)
```

## Mobile Settings

### Mobile-Specific Options

```php
'reign_wcfm_mobile' => array(
    'simplified_dashboard' => true,
    'touch_friendly'      => true,
    'swipe_navigation'    => true,
    'compact_view'        => true,
    'quick_actions'       => true
)
```

## SEO Configuration

### Meta Tags Settings

```php
'reign_wcfm_seo' => array(
    'store_title_format'  => '%store_name% - %site_name%',
    'meta_description'    => true,
    'schema_markup'       => true,
    'og_tags'            => true,
    'twitter_cards'      => true
)
```

## Import/Export Settings

### Backup Configuration

```bash
# Export settings
wp option get reign_wcfm_settings --format=json > wcfm-settings.json

# Import settings  
wp option update reign_wcfm_settings --format=json < wcfm-settings.json
```

## Troubleshooting Configuration

### Debug Mode

```php
// Enable debug mode
define('REIGN_WCFM_DEBUG', true);
define('WCFM_DEBUG', true);

// Log configuration issues
if (REIGN_WCFM_DEBUG) {
    error_log('Reign WCFM Config: ' . print_r($config, true));
}
```

## Next Steps

- [Store Customization](04-store-customization.md) - Customize vendor stores
- [Developer Guide](05-developer-guide.md) - Advanced development
- [Troubleshooting](07-troubleshooting.md) - Common issues
- [FAQ](08-faq.md) - Frequently asked questions