# WC Vendors Marketplace Integration Guide

## Overview

WC Vendors transforms your WooCommerce store into a multi-vendor marketplace. Reign theme provides seamless integration with WC Vendors, offering custom vendor dashboards, enhanced store pages, and social selling features through BuddyPress integration.

## Installation & Setup

### Installing WC Vendors

1. **Prerequisites:**
   - WooCommerce installed and configured
   - Reign theme activated

2. **Install WC Vendors:**
   ```
   Free Version:
   Plugins → Add New → Search "WC Vendors Marketplace"
   Install and Activate

   Pro Version:
   Purchase from wcvendors.com
   Upload and activate WC Vendors Pro
   ```

3. **Initial Configuration:**
   - WC Vendors → Settings
   - Configure commission rates
   - Set vendor capabilities
   - Configure registration

### Reign Integration Features

**Automatic Enhancements:**
- Styled vendor dashboards
- Custom vendor store pages
- BuddyPress vendor profiles
- Responsive vendor forms
- Enhanced product management

## Vendor Dashboard

### Dashboard Access

**Frontend Dashboard URL:**
```
yoursite.com/dashboard/

Sections:
- Dashboard (Overview)
- Products
- Orders
- Shop Settings
- Ratings
- Coupons (Pro)
```

### Dashboard Customization

```php
// Customize vendor dashboard menu
function reign_wcv_dashboard_menu($menu_items) {
    // Add custom menu item
    $menu_items['custom'] = array(
        'label' => __('Analytics', 'reign'),
        'url' => WCV_Vendors::get_vendor_dashboard_url() . 'analytics/',
        'icon' => 'fa fa-chart-line',
        'priority' => 15
    );

    // Remove item
    unset($menu_items['ratings']);

    return $menu_items;
}
add_filter('wcv_vendor_dashboard_menu_items', 'reign_wcv_dashboard_menu');
```

### Dashboard Styling

```css
/* Reign + WC Vendors Dashboard */
.wcv-dashboard-wrapper {
    background: var(--reign-background);
    padding: 30px;
    border-radius: 10px;
}

.wcv-dashboard-navigation {
    background: white;
    border-radius: 8px;
    padding: 0;
    overflow: hidden;
}

.wcv-dashboard-navigation li a {
    padding: 15px 20px;
    border-bottom: 1px solid #e1e4e8;
    transition: all 0.3s;
}

.wcv-dashboard-navigation li.active a {
    background: var(--reign-primary);
    color: white;
}

/* Stats cards */
.wcv-stats-card {
    background: white;
    border-radius: 8px;
    padding: 20px;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
```

## Vendor Store Pages

### Store Layout

**Store URL Structure:**
```
yoursite.com/vendors/vendor-name/
```

### Store Header

```php
// Custom vendor store header
function reign_wcv_store_header($vendor_id) {
    $vendor = get_userdata($vendor_id);
    $store_name = WCV_Vendors::get_vendor_shop_name($vendor_id);
    $store_description = get_user_meta($vendor_id, 'pv_shop_description', true);
    ?>
    <div class="reign-vendor-header">
        <div class="vendor-banner">
            <?php
            $banner = get_user_meta($vendor_id, '_wcv_store_banner', true);
            if ($banner) {
                echo wp_get_attachment_image($banner, 'full');
            }
            ?>
        </div>
        <div class="vendor-info-wrapper">
            <div class="vendor-avatar">
                <?php echo get_avatar($vendor_id, 150); ?>
            </div>
            <div class="vendor-details">
                <h1><?php echo esc_html($store_name); ?></h1>
                <p><?php echo esc_html($store_description); ?></p>
                <div class="vendor-meta">
                    <span class="vendor-rating">
                        <?php
                        if (class_exists('WCVendors_Pro')) {
                            echo WCVendors_Pro_Ratings_Controller::ratings_link($vendor_id);
                        }
                        ?>
                    </span>
                    <span class="vendor-products">
                        <?php
                        $products = WCV_Vendors::get_vendor_products($vendor_id);
                        echo count($products) . ' Products';
                        ?>
                    </span>
                </div>
            </div>
            <div class="vendor-actions">
                <?php if (is_user_logged_in()) : ?>
                    <button class="follow-vendor" data-vendor="<?php echo $vendor_id; ?>">
                        Follow
                    </button>
                    <button class="contact-vendor" data-vendor="<?php echo $vendor_id; ?>">
                        Contact
                    </button>
                <?php endif; ?>
            </div>
        </div>
    </div>
    <?php
}
add_action('wcvendors_before_vendor_store', 'reign_wcv_store_header');
```

### Store Tabs

```php
// Add custom store tabs
function reign_wcv_store_tabs($tabs, $vendor_id) {
    $tabs['about'] = array(
        'title' => __('About', 'reign'),
        'priority' => 10,
        'content' => reign_vendor_about_tab($vendor_id)
    );

    $tabs['policies'] = array(
        'title' => __('Policies', 'reign'),
        'priority' => 20,
        'content' => reign_vendor_policies_tab($vendor_id)
    );

    return $tabs;
}
add_filter('wcv_store_tabs', 'reign_wcv_store_tabs', 10, 2);
```

## Product Management

### Add Product Form

```php
// Enhance product submission form
function reign_wcv_product_form_fields() {
    ?>
    <div class="wcv-form-group">
        <label><?php _e('Product Video URL', 'reign'); ?></label>
        <input type="url" name="product_video" class="wcv-form-control">
    </div>

    <div class="wcv-form-group">
        <label><?php _e('Warranty Information', 'reign'); ?></label>
        <textarea name="warranty_info" class="wcv-form-control"></textarea>
    </div>
    <?php
}
add_action('wcv_after_product_details', 'reign_wcv_product_form_fields');
```

### Product Approval

```php
// Auto-approve trusted vendors
function reign_wcv_auto_approve($post_id, $post) {
    $vendor_id = get_post_field('post_author', $post_id);

    if (is_trusted_vendor($vendor_id)) {
        wp_update_post(array(
            'ID' => $post_id,
            'post_status' => 'publish'
        ));
    }
}
add_action('wcv_save_product', 'reign_wcv_auto_approve', 10, 2);
```

## Commission Management

### Commission Settings

```php
// Custom commission rates
function reign_wcv_commission_rate($commission, $product_id, $vendor_id) {
    // Category-based commission
    $terms = get_the_terms($product_id, 'product_cat');
    if ($terms && !is_wp_error($terms)) {
        foreach ($terms as $term) {
            if ($term->slug == 'electronics') {
                return 85; // 85% to vendor for electronics
            }
        }
    }

    // Vendor level commission
    $vendor_level = get_user_meta($vendor_id, 'vendor_level', true);
    if ($vendor_level == 'premium') {
        return 90; // 90% for premium vendors
    }

    return $commission;
}
add_filter('wcv_commission_rate', 'reign_wcv_commission_rate', 10, 3);
```

### Payout Settings

```php
// Configure payout schedule
function reign_wcv_payout_schedule($schedules) {
    $schedules['biweekly'] = array(
        'interval' => 1209600, // 2 weeks in seconds
        'display' => __('Bi-Weekly', 'reign')
    );
    return $schedules;
}
add_filter('wcv_payout_schedules', 'reign_wcv_payout_schedule');
```

## BuddyPress Integration

### Vendor Profile Tab

```php
// Add vendor tab to BuddyPress profile
function reign_bp_vendor_tab() {
    if (!WCV_Vendors::is_vendor(bp_displayed_user_id())) {
        return;
    }

    bp_core_new_nav_item(array(
        'name' => __('Store', 'reign'),
        'slug' => 'store',
        'screen_function' => 'reign_bp_vendor_screen',
        'position' => 40,
        'default_subnav_slug' => 'products'
    ));

    bp_core_new_subnav_item(array(
        'name' => __('Products', 'reign'),
        'slug' => 'products',
        'parent_slug' => 'store',
        'parent_url' => bp_displayed_user_domain() . 'store/',
        'screen_function' => 'reign_bp_vendor_products_screen',
        'position' => 10
    ));
}
add_action('bp_setup_nav', 'reign_bp_vendor_tab');
```

### Vendor Activity

```php
// Post vendor activities to BuddyPress
function reign_wcv_bp_activity($vendor_id, $action, $content = '') {
    if (function_exists('bp_activity_add')) {
        bp_activity_add(array(
            'user_id' => $vendor_id,
            'type' => 'vendor_update',
            'action' => $action,
            'content' => $content,
            'component' => 'wcvendors',
        ));
    }
}

// Track new products
add_action('wcv_save_product', function($post_id) {
    $vendor_id = get_post_field('post_author', $post_id);
    $product = wc_get_product($post_id);

    $action = sprintf(
        '%s added a new product: <a href="%s">%s</a>',
        bp_core_get_userlink($vendor_id),
        get_permalink($post_id),
        $product->get_name()
    );

    reign_wcv_bp_activity($vendor_id, $action);
});
```

## Vendor Capabilities

### Role Management

```php
// Customize vendor capabilities
function reign_wcv_vendor_caps($caps) {
    $caps['edit_products'] = true;
    $caps['delete_products'] = true;
    $caps['manage_product_terms'] = true;
    $caps['upload_files'] = true;
    $caps['view_woocommerce_reports'] = false; // Restrict

    return $caps;
}
add_filter('wcv_vendor_capabilities', 'reign_wcv_vendor_caps');
```

### Vendor Levels

```php
// Implement vendor levels
function reign_vendor_levels() {
    $levels = array(
        'basic' => array(
            'name' => 'Basic Vendor',
            'commission' => 70,
            'product_limit' => 50,
            'features' => array('basic_dashboard', 'standard_support')
        ),
        'pro' => array(
            'name' => 'Pro Vendor',
            'commission' => 80,
            'product_limit' => 200,
            'features' => array('advanced_dashboard', 'priority_support', 'featured_products')
        ),
        'premium' => array(
            'name' => 'Premium Vendor',
            'commission' => 90,
            'product_limit' => -1, // Unlimited
            'features' => array('full_dashboard', 'dedicated_support', 'marketing_tools')
        )
    );

    return apply_filters('reign_vendor_levels', $levels);
}
```

## Shipping Configuration

### Vendor Shipping

```php
// Enable vendor shipping
add_filter('wcvendors_vendor_shipping_enabled', '__return_true');

// Custom shipping rates
function reign_wcv_shipping_rates($rates, $vendor_id) {
    // Add express shipping for premium vendors
    if (get_user_meta($vendor_id, 'vendor_level', true) == 'premium') {
        $rates['express'] = array(
            'label' => 'Express Shipping',
            'cost' => 15,
            'delivery_time' => '1-2 days'
        );
    }

    return $rates;
}
add_filter('wcv_vendor_shipping_rates', 'reign_wcv_shipping_rates', 10, 2);
```

## Vendor Widgets

### Available Widgets

```php
// Register vendor widgets
function reign_wcv_widgets() {
    register_widget('Reign_WCV_Store_Info');
    register_widget('Reign_WCV_Top_Vendors');
    register_widget('Reign_WCV_Vendor_Products');
    register_widget('Reign_WCV_Vendor_Categories');
}
add_action('widgets_init', 'reign_wcv_widgets');
```

### Store Info Widget

```php
class Reign_WCV_Store_Info extends WP_Widget {
    public function widget($args, $instance) {
        if (!is_vendor_page()) return;

        $vendor_id = get_vendor_id();
        $store_info = get_vendor_store_info($vendor_id);
        ?>
        <div class="vendor-info-widget">
            <h3><?php echo $store_info['name']; ?></h3>
            <p><?php echo $store_info['description']; ?></p>
            <ul class="vendor-details">
                <li>📍 <?php echo $store_info['location']; ?></li>
                <li>📧 <?php echo $store_info['email']; ?></li>
                <li>📞 <?php echo $store_info['phone']; ?></li>
            </ul>
        </div>
        <?php
    }
}
```

## Shortcodes

### WC Vendors Shortcodes

```
[wcv_vendorslist] - List all vendors
[wcv_vendor_dashboard] - Vendor dashboard
[wcv_shop_settings] - Shop settings form
[wcv_orders] - Vendor orders
[wcv_vendor_products vendor_id="123"] - Vendor products
```

### Custom Shortcodes

```php
// Top vendors shortcode
function reign_wcv_top_vendors_shortcode($atts) {
    $atts = shortcode_atts(array(
        'number' => 10,
        'orderby' => 'sales'
    ), $atts);

    $vendors = get_top_vendors($atts);
    ob_start();
    ?>
    <div class="top-vendors-grid">
        <?php foreach ($vendors as $vendor) : ?>
            <div class="vendor-card">
                <?php echo get_avatar($vendor->ID, 100); ?>
                <h4><?php echo WCV_Vendors::get_vendor_shop_name($vendor->ID); ?></h4>
                <a href="<?php echo WCV_Vendors::get_vendor_shop_page($vendor->ID); ?>">
                    Visit Store
                </a>
            </div>
        <?php endforeach; ?>
    </div>
    <?php
    return ob_get_clean();
}
add_shortcode('reign_top_vendors', 'reign_wcv_top_vendors_shortcode');
```

## Email Notifications

### Vendor Emails

```php
// Customize vendor email templates
function reign_wcv_email_templates($templates) {
    $templates['new_order'] = array(
        'subject' => 'New Order #{order_number}',
        'heading' => 'You have a new order!',
        'template' => 'emails/vendor-new-order.php'
    );

    return $templates;
}
add_filter('wcv_email_templates', 'reign_wcv_email_templates');
```

## Performance Optimization

### Caching

```php
// Cache vendor data
function get_cached_vendor_data($vendor_id) {
    $cache_key = 'wcv_vendor_' . $vendor_id;
    $data = wp_cache_get($cache_key);

    if (false === $data) {
        $data = array(
            'products' => WCV_Vendors::get_vendor_products($vendor_id),
            'ratings' => WCVendors_Pro_Ratings_Controller::get_vendor_rating($vendor_id),
            'sales' => get_vendor_sales($vendor_id)
        );
        wp_cache_set($cache_key, $data, '', 3600);
    }

    return $data;
}
```

## Troubleshooting

### Common Issues

#### Dashboard Not Accessible
```
Solutions:
- Check vendor role assignment
- Verify dashboard page exists
- Clear permalinks
- Check page permissions
```

#### Products Not Showing
```
Check:
- Product approval status
- Vendor product limit
- Product visibility settings
- Cache issues
```

#### Commission Calculation Issues
```
Verify:
- Commission settings
- Product prices
- Tax settings
- Coupon applications
```

## Best Practices

1. **Security** - Validate all vendor inputs
2. **Performance** - Cache vendor queries
3. **Commission** - Clear rate structure
4. **Support** - Vendor documentation
5. **Mobile** - Test vendor dashboard
6. **Approval** - Product review process
7. **Backup** - Regular database backup
8. **Updates** - Keep plugins updated