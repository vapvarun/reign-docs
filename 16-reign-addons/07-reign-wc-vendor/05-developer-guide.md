# Reign WC Vendors Addon - Developer Guide

## What You'll Learn
This guide provides developers with hooks, filters, and code examples to extend the Reign WC Vendors addon. We'll cover customizations, API integration, and advanced features.

## Quick Overview
**Skill Level:** Intermediate to Advanced PHP  
**Requirements:** Basic WordPress development knowledge  
**Tools:** Code editor, local development environment

---

## Part 1: Core Hooks & Filters

### Action Hooks

**Vendor Registration Hooks:**

```php
// Before vendor application form
add_action('reign_wcv_before_vendor_application', function() {
    echo '<div class="custom-notice">Join our marketplace!</div>';
});

// After vendor approval
add_action('reign_wcv_vendor_approved', function($vendor_id) {
    // Send welcome package
    send_vendor_welcome_email($vendor_id);
    // Create sample products
    create_starter_products($vendor_id);
}, 10, 1);

// On vendor store creation
add_action('reign_wcv_store_created', function($store_id, $vendor_id) {
    // Set up default store settings
    update_user_meta($vendor_id, 'store_banner', 'default-banner.jpg');
    update_user_meta($vendor_id, 'store_notice', 'Welcome to our store!');
}, 10, 2);
```

**Product Management Hooks:**

```php
// Before product submission
add_action('reign_wcv_before_product_submit', function($product_data) {
    // Validate custom fields
    if (empty($product_data['custom_field'])) {
        wp_die('Custom field is required');
    }
});

// After product approval
add_action('reign_wcv_product_approved', function($product_id, $vendor_id) {
    // Notify vendor
    $vendor = get_userdata($vendor_id);
    wp_mail($vendor->user_email, 'Product Approved!', 'Your product is live.');
    
    // Add to featured products
    if (get_post_meta($product_id, '_quality_score', true) > 90) {
        update_post_meta($product_id, '_featured', 'yes');
    }
}, 10, 2);
```

**Order Processing Hooks:**

```php
// On new order for vendor
add_action('reign_wcv_vendor_order_created', function($order_id, $vendor_id) {
    // Track vendor sales
    $sales_count = get_user_meta($vendor_id, 'total_sales', true);
    update_user_meta($vendor_id, 'total_sales', $sales_count + 1);
    
    // Check for milestones
    if ($sales_count == 100) {
        add_vendor_badge($vendor_id, 'centurion');
    }
}, 10, 2);

// On order completion
add_action('reign_wcv_order_completed', function($order_id, $vendor_id) {
    // Calculate vendor rating
    update_vendor_rating($vendor_id);
    // Process commission
    process_vendor_commission($order_id, $vendor_id);
}, 10, 2);
```

### Filter Hooks

**Store Display Filters:**

```php
// Modify store header
add_filter('reign_wcv_store_header_data', function($data, $vendor_id) {
    // Add custom fields
    $data['verified'] = get_user_meta($vendor_id, 'verified_vendor', true);
    $data['specialty'] = get_user_meta($vendor_id, 'store_specialty', true);
    $data['years_active'] = calculate_years_active($vendor_id);
    
    return $data;
}, 10, 2);

// Filter store tabs
add_filter('reign_wcv_store_tabs', function($tabs, $vendor_id) {
    // Add custom tab
    $tabs['certificates'] = array(
        'title' => 'Certifications',
        'priority' => 25,
        'callback' => 'display_vendor_certificates'
    );
    
    // Remove reviews if new vendor
    $join_date = get_userdata($vendor_id)->user_registered;
    if (strtotime($join_date) > strtotime('-30 days')) {
        unset($tabs['reviews']);
    }
    
    return $tabs;
}, 10, 2);
```

**Commission Filters:**

```php
// Modify commission rate
add_filter('reign_wcv_commission_rate', function($rate, $product_id, $vendor_id) {
    // Premium vendors get better rate
    if (is_premium_vendor($vendor_id)) {
        return $rate - 5; // 5% less commission
    }
    
    // Category-based commission
    $product_cats = wp_get_post_terms($product_id, 'product_cat', array('fields' => 'slugs'));
    if (in_array('electronics', $product_cats)) {
        return 15; // 15% for electronics
    }
    
    return $rate;
}, 10, 3);

// Filter minimum payout
add_filter('reign_wcv_minimum_payout', function($minimum, $vendor_id) {
    // VIP vendors have no minimum
    if (is_vip_vendor($vendor_id)) {
        return 0;
    }
    return $minimum;
}, 10, 2);
```

---

## Part 2: Custom Store Features

### Adding Custom Fields to Vendor Stores

```php
// Add fields to vendor settings
add_action('reign_wcv_vendor_settings_fields', function($vendor_id) {
    ?>
    <div class="form-group">
        <label>Business Type</label>
        <select name="business_type">
            <option value="individual">Individual</option>
            <option value="company">Company</option>
            <option value="nonprofit">Non-Profit</option>
        </select>
    </div>
    
    <div class="form-group">
        <label>Years in Business</label>
        <input type="number" name="years_business" min="0" max="100">
    </div>
    
    <div class="form-group">
        <label>Certifications</label>
        <textarea name="certifications" rows="3"></textarea>
    </div>
    <?php
});

// Save custom fields
add_action('reign_wcv_save_vendor_settings', function($vendor_id) {
    if (isset($_POST['business_type'])) {
        update_user_meta($vendor_id, 'business_type', sanitize_text_field($_POST['business_type']));
    }
    if (isset($_POST['years_business'])) {
        update_user_meta($vendor_id, 'years_business', intval($_POST['years_business']));
    }
    if (isset($_POST['certifications'])) {
        update_user_meta($vendor_id, 'certifications', sanitize_textarea_field($_POST['certifications']));
    }
});

// Display custom fields in store
add_action('reign_wcv_store_header_info', function($vendor_id) {
    $business_type = get_user_meta($vendor_id, 'business_type', true);
    $years = get_user_meta($vendor_id, 'years_business', true);
    
    if ($business_type) {
        echo '<span class="business-type">' . ucfirst($business_type) . '</span>';
    }
    if ($years) {
        echo '<span class="years-active">' . $years . ' years in business</span>';
    }
});
```

### Creating Vendor Badges System

```php
class Reign_WCV_Vendor_Badges {
    
    private $badges = array(
        'new_vendor' => array(
            'title' => 'New Vendor',
            'icon' => 'star',
            'criteria' => 'less_than_30_days'
        ),
        'power_seller' => array(
            'title' => 'Power Seller',
            'icon' => 'trophy',
            'criteria' => '100_sales'
        ),
        'fast_shipper' => array(
            'title' => 'Fast Shipper',
            'icon' => 'lightning',
            'criteria' => 'ships_within_24h'
        ),
        'top_rated' => array(
            'title' => 'Top Rated',
            'icon' => 'thumbs-up',
            'criteria' => '4.5_stars_minimum'
        )
    );
    
    public function __construct() {
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Check and assign badges daily
        if (!wp_next_scheduled('reign_wcv_check_badges')) {
            wp_schedule_event(time(), 'daily', 'reign_wcv_check_badges');
        }
        add_action('reign_wcv_check_badges', array($this, 'check_all_vendor_badges'));
    }
    
    public function check_all_vendor_badges() {
        $vendors = get_users(array('role' => 'vendor'));
        
        foreach ($vendors as $vendor) {
            $this->check_vendor_badges($vendor->ID);
        }
    }
    
    public function check_vendor_badges($vendor_id) {
        $earned_badges = array();
        
        // Check new vendor
        $registered = get_userdata($vendor_id)->user_registered;
        if (strtotime($registered) > strtotime('-30 days')) {
            $earned_badges[] = 'new_vendor';
        }
        
        // Check power seller
        $total_sales = $this->get_vendor_sales_count($vendor_id);
        if ($total_sales >= 100) {
            $earned_badges[] = 'power_seller';
        }
        
        // Check fast shipper
        $avg_shipping_time = $this->get_average_shipping_time($vendor_id);
        if ($avg_shipping_time <= 24) {
            $earned_badges[] = 'fast_shipper';
        }
        
        // Check top rated
        $avg_rating = $this->get_vendor_average_rating($vendor_id);
        if ($avg_rating >= 4.5) {
            $earned_badges[] = 'top_rated';
        }
        
        update_user_meta($vendor_id, 'vendor_badges', $earned_badges);
    }
    
    public function display_vendor_badges($vendor_id) {
        $badges = get_user_meta($vendor_id, 'vendor_badges', true);
        
        if (!empty($badges)) {
            echo '<div class="vendor-badges">';
            foreach ($badges as $badge_key) {
                if (isset($this->badges[$badge_key])) {
                    $badge = $this->badges[$badge_key];
                    echo '<span class="badge badge-' . $badge_key . '">';
                    echo '<i class="fa fa-' . $badge['icon'] . '"></i> ';
                    echo $badge['title'];
                    echo '</span>';
                }
            }
            echo '</div>';
        }
    }
    
    private function get_vendor_sales_count($vendor_id) {
        // Implementation
        return 0;
    }
    
    private function get_average_shipping_time($vendor_id) {
        // Implementation
        return 48;
    }
    
    private function get_vendor_average_rating($vendor_id) {
        // Implementation  
        return 0;
    }
}

// Initialize badges system
new Reign_WCV_Vendor_Badges();
```

---

## Part 3: REST API Integration

### Custom REST Endpoints

```php
class Reign_WCV_REST_API {
    
    public function __construct() {
        add_action('rest_api_init', array($this, 'register_routes'));
    }
    
    public function register_routes() {
        // Get vendor details
        register_rest_route('reign-wcv/v1', '/vendor/(?P<id>\d+)', array(
            'methods' => 'GET',
            'callback' => array($this, 'get_vendor'),
            'permission_callback' => '__return_true'
        ));
        
        // Get vendor products
        register_rest_route('reign-wcv/v1', '/vendor/(?P<id>\d+)/products', array(
            'methods' => 'GET',
            'callback' => array($this, 'get_vendor_products'),
            'permission_callback' => '__return_true'
        ));
        
        // Update vendor settings
        register_rest_route('reign-wcv/v1', '/vendor/(?P<id>\d+)/settings', array(
            'methods' => 'POST',
            'callback' => array($this, 'update_vendor_settings'),
            'permission_callback' => array($this, 'check_vendor_permission')
        ));
    }
    
    public function get_vendor($request) {
        $vendor_id = $request['id'];
        $vendor = get_userdata($vendor_id);
        
        if (!$vendor) {
            return new WP_Error('vendor_not_found', 'Vendor not found', array('status' => 404));
        }
        
        return array(
            'id' => $vendor_id,
            'name' => $vendor->display_name,
            'store_name' => get_user_meta($vendor_id, 'pv_shop_name', true),
            'description' => get_user_meta($vendor_id, 'pv_shop_description', true),
            'logo' => get_user_meta($vendor_id, 'shop_logo', true),
            'banner' => get_user_meta($vendor_id, 'shop_banner', true),
            'rating' => $this->get_vendor_rating($vendor_id),
            'products_count' => $this->get_vendor_products_count($vendor_id),
            'member_since' => $vendor->user_registered
        );
    }
    
    public function get_vendor_products($request) {
        $vendor_id = $request['id'];
        $page = isset($request['page']) ? $request['page'] : 1;
        $per_page = isset($request['per_page']) ? $request['per_page'] : 10;
        
        $args = array(
            'post_type' => 'product',
            'author' => $vendor_id,
            'posts_per_page' => $per_page,
            'paged' => $page,
            'post_status' => 'publish'
        );
        
        $products = new WP_Query($args);
        $response = array();
        
        foreach ($products->posts as $product) {
            $product_obj = wc_get_product($product->ID);
            $response[] = array(
                'id' => $product->ID,
                'name' => $product->post_title,
                'price' => $product_obj->get_price(),
                'image' => wp_get_attachment_url($product_obj->get_image_id()),
                'rating' => $product_obj->get_average_rating(),
                'stock' => $product_obj->get_stock_quantity()
            );
        }
        
        return array(
            'products' => $response,
            'total' => $products->found_posts,
            'pages' => $products->max_num_pages
        );
    }
    
    public function update_vendor_settings($request) {
        $vendor_id = $request['id'];
        $settings = $request->get_json_params();
        
        // Update allowed settings
        $allowed_settings = array('shop_name', 'shop_description', 'shop_banner', 'shop_logo');
        
        foreach ($settings as $key => $value) {
            if (in_array($key, $allowed_settings)) {
                update_user_meta($vendor_id, 'pv_' . $key, sanitize_text_field($value));
            }
        }
        
        return array('success' => true, 'message' => 'Settings updated');
    }
    
    public function check_vendor_permission($request) {
        $vendor_id = $request['id'];
        return current_user_can('manage_options') || get_current_user_id() == $vendor_id;
    }
    
    private function get_vendor_rating($vendor_id) {
        // Implementation
        return 4.5;
    }
    
    private function get_vendor_products_count($vendor_id) {
        return count_user_posts($vendor_id, 'product');
    }
}

// Initialize REST API
new Reign_WCV_REST_API();
```

---

## Part 4: AJAX Implementation

### Vendor Dashboard AJAX

```php
class Reign_WCV_Dashboard_Ajax {
    
    public function __construct() {
        // Dashboard stats
        add_action('wp_ajax_reign_wcv_get_dashboard_stats', array($this, 'get_dashboard_stats'));
        
        // Quick product edit
        add_action('wp_ajax_reign_wcv_quick_edit_product', array($this, 'quick_edit_product'));
        
        // Bulk actions
        add_action('wp_ajax_reign_wcv_bulk_action', array($this, 'handle_bulk_action'));
    }
    
    public function get_dashboard_stats() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_wcv_nonce')) {
            wp_die('Security check failed');
        }
        
        $vendor_id = get_current_user_id();
        $period = sanitize_text_field($_POST['period']);
        
        $stats = array(
            'total_sales' => $this->get_period_sales($vendor_id, $period),
            'total_orders' => $this->get_period_orders($vendor_id, $period),
            'pending_orders' => $this->get_pending_orders($vendor_id),
            'total_products' => $this->get_total_products($vendor_id),
            'revenue' => $this->get_period_revenue($vendor_id, $period),
            'commission_earned' => $this->get_period_commission($vendor_id, $period)
        );
        
        // Add chart data
        $stats['chart_data'] = $this->get_chart_data($vendor_id, $period);
        
        wp_send_json_success($stats);
    }
    
    public function quick_edit_product() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_wcv_nonce')) {
            wp_die('Security check failed');
        }
        
        $product_id = intval($_POST['product_id']);
        $vendor_id = get_current_user_id();
        
        // Check ownership
        if (get_post_field('post_author', $product_id) != $vendor_id) {
            wp_send_json_error('You can only edit your own products');
        }
        
        // Update product
        $product = wc_get_product($product_id);
        
        if (isset($_POST['price'])) {
            $product->set_regular_price(floatval($_POST['price']));
        }
        
        if (isset($_POST['sale_price'])) {
            $product->set_sale_price(floatval($_POST['sale_price']));
        }
        
        if (isset($_POST['stock'])) {
            $product->set_stock_quantity(intval($_POST['stock']));
        }
        
        if (isset($_POST['status'])) {
            $product->set_status(sanitize_text_field($_POST['status']));
        }
        
        $product->save();
        
        wp_send_json_success(array(
            'message' => 'Product updated successfully',
            'product_id' => $product_id
        ));
    }
    
    public function handle_bulk_action() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_wcv_nonce')) {
            wp_die('Security check failed');
        }
        
        $action = sanitize_text_field($_POST['bulk_action']);
        $items = array_map('intval', $_POST['items']);
        $vendor_id = get_current_user_id();
        
        switch ($action) {
            case 'delete':
                foreach ($items as $product_id) {
                    if (get_post_field('post_author', $product_id) == $vendor_id) {
                        wp_delete_post($product_id, false);
                    }
                }
                $message = 'Products deleted';
                break;
                
            case 'draft':
                foreach ($items as $product_id) {
                    if (get_post_field('post_author', $product_id) == $vendor_id) {
                        wp_update_post(array(
                            'ID' => $product_id,
                            'post_status' => 'draft'
                        ));
                    }
                }
                $message = 'Products set to draft';
                break;
                
            case 'publish':
                foreach ($items as $product_id) {
                    if (get_post_field('post_author', $product_id) == $vendor_id) {
                        wp_update_post(array(
                            'ID' => $product_id,
                            'post_status' => 'publish'
                        ));
                    }
                }
                $message = 'Products published';
                break;
        }
        
        wp_send_json_success(array('message' => $message));
    }
    
    private function get_period_sales($vendor_id, $period) {
        // Implementation
        return 0;
    }
    
    private function get_period_orders($vendor_id, $period) {
        // Implementation
        return 0;
    }
    
    private function get_pending_orders($vendor_id) {
        // Implementation
        return 0;
    }
    
    private function get_total_products($vendor_id) {
        return count_user_posts($vendor_id, 'product');
    }
    
    private function get_period_revenue($vendor_id, $period) {
        // Implementation
        return 0;
    }
    
    private function get_period_commission($vendor_id, $period) {
        // Implementation
        return 0;
    }
    
    private function get_chart_data($vendor_id, $period) {
        // Implementation
        return array();
    }
}

// Initialize AJAX handlers
new Reign_WCV_Dashboard_Ajax();
```

### JavaScript for AJAX Calls

```javascript
// Dashboard stats refresh
jQuery(document).ready(function($) {
    
    // Load dashboard stats
    function loadDashboardStats(period) {
        $.ajax({
            url: reign_wcv_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_wcv_get_dashboard_stats',
                nonce: reign_wcv_ajax.nonce,
                period: period
            },
            success: function(response) {
                if (response.success) {
                    updateDashboard(response.data);
                }
            }
        });
    }
    
    // Quick edit product
    $('.quick-edit-product').on('click', function(e) {
        e.preventDefault();
        
        var productId = $(this).data('product-id');
        var price = $('#price-' + productId).val();
        var stock = $('#stock-' + productId).val();
        
        $.ajax({
            url: reign_wcv_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_wcv_quick_edit_product',
                nonce: reign_wcv_ajax.nonce,
                product_id: productId,
                price: price,
                stock: stock
            },
            success: function(response) {
                if (response.success) {
                    showNotification('Product updated', 'success');
                } else {
                    showNotification(response.data, 'error');
                }
            }
        });
    });
    
    // Bulk actions
    $('#apply-bulk-action').on('click', function() {
        var action = $('#bulk-action-selector').val();
        var items = [];
        
        $('.product-checkbox:checked').each(function() {
            items.push($(this).val());
        });
        
        if (items.length === 0) {
            showNotification('Please select items', 'warning');
            return;
        }
        
        $.ajax({
            url: reign_wcv_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_wcv_bulk_action',
                nonce: reign_wcv_ajax.nonce,
                bulk_action: action,
                items: items
            },
            success: function(response) {
                if (response.success) {
                    showNotification(response.data.message, 'success');
                    location.reload();
                }
            }
        });
    });
    
    // Helper functions
    function updateDashboard(data) {
        $('#total-sales').text(data.total_sales);
        $('#total-orders').text(data.total_orders);
        $('#pending-orders').text(data.pending_orders);
        $('#total-products').text(data.total_products);
        $('#revenue').text('$' + data.revenue);
        $('#commission').text('$' + data.commission_earned);
        
        // Update chart
        updateChart(data.chart_data);
    }
    
    function showNotification(message, type) {
        var notification = $('<div class="notice notice-' + type + '">')
            .text(message)
            .prependTo('#wpbody-content')
            .fadeIn();
        
        setTimeout(function() {
            notification.fadeOut(function() {
                $(this).remove();
            });
        }, 3000);
    }
    
    // Initialize
    loadDashboardStats('month');
    
    // Period selector
    $('#period-selector').on('change', function() {
        loadDashboardStats($(this).val());
    });
});
```

---

## Part 5: Database Queries

### Custom Database Operations

```php
class Reign_WCV_Database {
    
    /**
     * Get vendor statistics
     */
    public function get_vendor_stats($vendor_id, $start_date = null, $end_date = null) {
        global $wpdb;
        
        if (!$start_date) {
            $start_date = date('Y-m-01');
        }
        if (!$end_date) {
            $end_date = date('Y-m-d');
        }
        
        // Get total sales
        $sales_query = $wpdb->prepare("
            SELECT COUNT(DISTINCT p.ID) as order_count,
                   SUM(oi.product_gross_revenue) as total_revenue
            FROM {$wpdb->prefix}woocommerce_order_items oi
            INNER JOIN {$wpdb->posts} p ON oi.order_id = p.ID
            WHERE p.post_type = 'shop_order'
            AND p.post_status IN ('wc-completed', 'wc-processing')
            AND oi.vendor_id = %d
            AND p.post_date BETWEEN %s AND %s
        ", $vendor_id, $start_date, $end_date);
        
        $sales = $wpdb->get_row($sales_query);
        
        // Get product count
        $product_count = $wpdb->get_var($wpdb->prepare("
            SELECT COUNT(*) FROM {$wpdb->posts}
            WHERE post_type = 'product'
            AND post_author = %d
            AND post_status = 'publish'
        ", $vendor_id));
        
        // Get average rating
        $rating_query = $wpdb->prepare("
            SELECT AVG(meta_value) as average_rating
            FROM {$wpdb->commentmeta} cm
            INNER JOIN {$wpdb->comments} c ON cm.comment_id = c.comment_ID
            INNER JOIN {$wpdb->posts} p ON c.comment_post_ID = p.ID
            WHERE p.post_author = %d
            AND cm.meta_key = 'rating'
            AND c.comment_approved = '1'
        ", $vendor_id);
        
        $average_rating = $wpdb->get_var($rating_query);
        
        return array(
            'order_count' => $sales->order_count ?: 0,
            'total_revenue' => $sales->total_revenue ?: 0,
            'product_count' => $product_count,
            'average_rating' => round($average_rating, 2)
        );
    }
    
    /**
     * Get best selling products for vendor
     */
    public function get_vendor_bestsellers($vendor_id, $limit = 5) {
        global $wpdb;
        
        $query = $wpdb->prepare("
            SELECT p.ID, p.post_title,
                   SUM(oi.product_qty) as total_sold,
                   SUM(oi.product_gross_revenue) as total_revenue
            FROM {$wpdb->prefix}woocommerce_order_items oi
            INNER JOIN {$wpdb->posts} p ON oi.product_id = p.ID
            WHERE p.post_author = %d
            AND p.post_type = 'product'
            GROUP BY p.ID
            ORDER BY total_sold DESC
            LIMIT %d
        ", $vendor_id, $limit);
        
        return $wpdb->get_results($query);
    }
    
    /**
     * Get vendor commission history
     */
    public function get_commission_history($vendor_id, $limit = 10) {
        global $wpdb;
        
        $query = $wpdb->prepare("
            SELECT c.*,
                   p.post_title as product_name,
                   o.post_date as order_date
            FROM {$wpdb->prefix}wcv_commissions c
            INNER JOIN {$wpdb->posts} p ON c.product_id = p.ID
            INNER JOIN {$wpdb->posts} o ON c.order_id = o.ID
            WHERE c.vendor_id = %d
            ORDER BY c.created_date DESC
            LIMIT %d
        ", $vendor_id, $limit);
        
        return $wpdb->get_results($query);
    }
}
```

---

## Part 6: Template Overrides

### Override Vendor Store Template

```php
// In your theme: /reign-child/wcvendors/store/store-header.php

<?php
/**
 * Store Header Template Override
 */

$vendor_id = get_query_var('author');
$vendor = get_userdata($vendor_id);
$store_info = get_user_meta($vendor_id);
?>

<div class="reign-wcv-store-header">
    <?php if ($banner = get_user_meta($vendor_id, 'banner_image', true)) : ?>
        <div class="store-banner">
            <img src="<?php echo esc_url($banner); ?>" alt="Store Banner">
        </div>
    <?php endif; ?>
    
    <div class="store-info-wrapper">
        <div class="container">
            <div class="store-logo">
                <?php if ($logo = get_user_meta($vendor_id, 'store_logo', true)) : ?>
                    <img src="<?php echo esc_url($logo); ?>" alt="Store Logo">
                <?php else : ?>
                    <div class="default-logo">
                        <?php echo substr($vendor->display_name, 0, 1); ?>
                    </div>
                <?php endif; ?>
            </div>
            
            <div class="store-details">
                <h1 class="store-name"><?php echo esc_html($vendor->display_name); ?></h1>
                
                <?php if ($tagline = get_user_meta($vendor_id, 'store_tagline', true)) : ?>
                    <p class="store-tagline"><?php echo esc_html($tagline); ?></p>
                <?php endif; ?>
                
                <div class="store-meta">
                    <?php
                    // Display badges
                    do_action('reign_wcv_store_badges', $vendor_id);
                    
                    // Display rating
                    $rating = get_user_meta($vendor_id, 'average_rating', true);
                    if ($rating) {
                        echo '<div class="store-rating">';
                        echo '<span class="rating-stars">' . wc_get_rating_html($rating) . '</span>';
                        echo '<span class="rating-count">(' . get_user_meta($vendor_id, 'rating_count', true) . ' reviews)</span>';
                        echo '</div>';
                    }
                    
                    // Member since
                    echo '<div class="member-since">Member since ' . date('F Y', strtotime($vendor->user_registered)) . '</div>';
                    ?>
                </div>
            </div>
            
            <div class="store-actions">
                <?php if (is_user_logged_in() && get_current_user_id() != $vendor_id) : ?>
                    <button class="follow-store" data-vendor="<?php echo $vendor_id; ?>">
                        <i class="fa fa-heart"></i> Follow Store
                    </button>
                <?php endif; ?>
                
                <button class="contact-vendor" data-vendor="<?php echo $vendor_id; ?>">
                    <i class="fa fa-envelope"></i> Contact
                </button>
            </div>
        </div>
    </div>
    
    <div class="store-tabs">
        <div class="container">
            <?php
            $tabs = apply_filters('reign_wcv_store_tabs', array(
                'products' => 'Products',
                'about' => 'About',
                'policies' => 'Policies',
                'reviews' => 'Reviews'
            ), $vendor_id);
            
            foreach ($tabs as $key => $label) {
                $active = (get_query_var('tab') == $key || (!get_query_var('tab') && $key == 'products')) ? 'active' : '';
                echo '<a href="?tab=' . $key . '" class="tab-link ' . $active . '">' . $label . '</a>';
            }
            ?>
        </div>
    </div>
</div>
```

---

## Quick Reference

### Important Functions

```php
// Check if user is vendor
WC_Vendors::is_vendor($user_id)

// Get vendor shop URL
WCV_Vendors::get_vendor_shop_page($vendor_id)

// Get vendor products
WCV_Vendors::get_vendor_products($vendor_id)

// Get vendor commission
WCV_Commission::get_vendor_commission($order_id, $vendor_id)

// Check vendor capability
WCV_Vendors::can_vendor_edit_product($vendor_id, $product_id)
```

### Key Filters

```php
// Commission rate
apply_filters('wcv_commission_rate', $rate, $product_id, $vendor_id)

// Vendor capabilities
apply_filters('wcv_vendor_capabilities', $capabilities, $vendor_id)

// Store tabs
apply_filters('wcv_store_tabs', $tabs, $vendor_id)

// Dashboard menu
apply_filters('wcv_dashboard_menu_items', $items, $vendor_id)
```

### Key Actions

```php
// After vendor registration
do_action('wcv_vendor_registered', $vendor_id)

// After product approval
do_action('wcv_product_approved', $product_id, $vendor_id)

// After order complete
do_action('wcv_order_complete', $order_id, $vendor_id)

// Store header
do_action('wcv_store_header', $vendor_id)
```

---

**Need Development Help?**  
📧 Email: support@wbcomdesigns.com  
👨‍💻 Custom development available  
📚 API Docs: docs.wbcomdesigns.com/api