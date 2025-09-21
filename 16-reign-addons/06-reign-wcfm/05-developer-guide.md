# Reign WCFM Addon - Developer Guide

## What This Guide Covers
This guide helps developers extend and customize the Reign WCFM addon. We'll cover hooks, filters, custom code, and API integration with practical examples.

---

## Getting Started for Developers

### File Structure Overview

```
reign-wcfm-addon/
├── reign-wcfm-addon.php          # Main plugin file
├── includes/
│   ├── class-loader.php          # Loads all components
│   ├── class-public.php          # Frontend functionality
│   ├── class-admin.php           # Admin functionality
│   ├── class-templates.php       # Template management
│   ├── class-widgets.php         # Custom widgets
│   └── class-buddypress.php      # BuddyPress integration
├── templates/                    # Override these in your theme
│   ├── store-listing.php
│   ├── single-store.php
│   └── vendor-dashboard/
├── assets/
│   ├── css/                      # Stylesheets
│   ├── js/                       # JavaScript files
│   └── images/                   # Default images
└── languages/                     # Translation files
```

### How to Override Templates

**Step 1:** Copy template from plugin
```bash
# From:
/plugins/reign-wcfm-addon/templates/store-listing.php

# To:
/themes/reign-theme/wcfm/store/store-listing.php
```

**Step 2:** Modify as needed
```php
// Your custom code in the copied template
<?php
// Custom store listing layout
if (is_user_logged_in()) {
    // Show extra info for logged-in users
}
?>
```

---

## Essential Hooks and Filters

### Action Hooks - Add Your Custom Code

#### Store Listing Hooks

```php
// Before store listing
add_action('reign_wcfm_before_store_listing', function() {
    echo '<div class="custom-banner">Featured Vendors This Week!</div>';
});

// After each store card
add_action('reign_wcfm_after_store_card', function($vendor_id) {
    $sales = get_vendor_total_sales($vendor_id);
    echo '<span class="total-sales">' . $sales . ' sales</span>';
});

// After store listing
add_action('reign_wcfm_after_store_listing', function() {
    echo '<div class="marketplace-stats">500+ Vendors | 10,000+ Products</div>';
});
```

#### Single Store Hooks

```php
// Customize store header
add_action('wcfmmp_before_store_header', function($vendor_id) {
    if (is_premium_vendor($vendor_id)) {
        echo '<div class="premium-badge">Premium Vendor</div>';
    }
});

// Add content after store tabs
add_action('wcfmmp_after_store_tabs', function($vendor_id) {
    // Add guarantee banner
    echo '<div class="satisfaction-guarantee">
            <i class="fa fa-shield"></i> 
            100% Satisfaction Guaranteed
          </div>';
});
```

#### Vendor Dashboard Hooks

```php
// Add custom dashboard widget
add_action('wcfm_dashboard_widget', function() {
    ?>
    <div class="wcfm-container">
        <h2>Marketing Tips</h2>
        <p>Boost your sales with these tips...</p>
    </div>
    <?php
});

// After dashboard menu
add_action('wcfm_dashboard_after_menu', function() {
    echo '<div class="vendor-tier">Gold Vendor</div>';
});
```

### Filter Hooks - Modify Existing Data

#### Modify Store Query

```php
// Change how stores are sorted
add_filter('wcfmmp_stores_query_args', function($args) {
    // Sort by highest rated first
    $args['meta_key'] = '_wcfmmp_avg_review_rating';
    $args['orderby'] = 'meta_value_num';
    $args['order'] = 'DESC';
    
    // Only show verified vendors
    $args['meta_query'][] = array(
        'key' => 'wcfm_verified',
        'value' => 'yes'
    );
    
    return $args;
});
```

#### Customize Store Data

```php
// Add custom data to store info
add_filter('wcfmmp_store_data', function($data, $vendor_id) {
    // Add response time
    $data['response_time'] = get_user_meta($vendor_id, 'avg_response_time', true);
    
    // Add specialty
    $data['specialty'] = get_user_meta($vendor_id, 'store_specialty', true);
    
    return $data;
}, 10, 2);
```

#### Modify Dashboard Menus

```php
// Customize vendor dashboard menu
add_filter('wcfm_menus', function($menus) {
    // Add custom menu item
    $menus['marketing'] = array(
        'label' => __('Marketing Tools', 'reign-wcfm'),
        'url' => wcfm_get_endpoint_url('marketing'),
        'icon' => 'fa-bullhorn',
        'priority' => 75
    );
    
    // Remove unwanted menu
    unset($menus['knowledgebase']);
    
    // Reorder menus
    $menus['products']['priority'] = 10;
    $menus['orders']['priority'] = 20;
    
    return $menus;
}, 100);
```

---

## Creating Custom Functionality

### Add Custom Fields to Vendor Registration

```php
// Add field to registration form
add_action('wcfm_membership_registration_form_after', function() {
    ?>
    <div class="wcfm-form-group">
        <label>Business Type</label>
        <select name="business_type">
            <option value="individual">Individual</option>
            <option value="company">Company</option>
        </select>
    </div>
    <?php
});

// Save custom field
add_action('wcfm_vendor_registration_saved', function($vendor_id, $data) {
    if (isset($_POST['business_type'])) {
        update_user_meta($vendor_id, 'business_type', sanitize_text_field($_POST['business_type']));
    }
}, 10, 2);
```

### Create Custom Vendor Badge System

```php
class Reign_Vendor_Badges {
    
    public function __construct() {
        add_action('wcfmmp_store_header_after_store_name', array($this, 'display_badges'));
    }
    
    public function display_badges($vendor_id) {
        $badges = $this->get_vendor_badges($vendor_id);
        
        if (!empty($badges)) {
            echo '<div class="vendor-badges">';
            foreach ($badges as $badge) {
                echo '<span class="badge badge-' . $badge['type'] . '">';
                echo '<i class="' . $badge['icon'] . '"></i> ';
                echo $badge['label'];
                echo '</span>';
            }
            echo '</div>';
        }
    }
    
    private function get_vendor_badges($vendor_id) {
        $badges = array();
        
        // Top Seller Badge
        $sales = $this->get_vendor_sales($vendor_id);
        if ($sales > 100) {
            $badges[] = array(
                'type' => 'gold',
                'icon' => 'fa fa-trophy',
                'label' => 'Top Seller'
            );
        }
        
        // Verified Badge
        if (get_user_meta($vendor_id, 'wcfm_verified', true) == 'yes') {
            $badges[] = array(
                'type' => 'verified',
                'icon' => 'fa fa-check-circle',
                'label' => 'Verified'
            );
        }
        
        // Fast Shipper Badge
        $ship_time = get_user_meta($vendor_id, 'average_shipping_time', true);
        if ($ship_time && $ship_time < 2) {
            $badges[] = array(
                'type' => 'fast',
                'icon' => 'fa fa-bolt',
                'label' => 'Fast Shipping'
            );
        }
        
        return $badges;
    }
    
    private function get_vendor_sales($vendor_id) {
        global $wpdb;
        
        $count = $wpdb->get_var($wpdb->prepare(
            "SELECT COUNT(DISTINCT order_id) 
             FROM {$wpdb->prefix}wcfm_marketplace_orders 
             WHERE vendor_id = %d 
             AND order_status = 'completed'",
            $vendor_id
        ));
        
        return $count ?: 0;
    }
}

// Initialize badge system
new Reign_Vendor_Badges();
```

### Add Custom Commission Rules

```php
// Dynamic commission based on vendor performance
add_filter('wcfm_commission_rule', function($rule, $vendor_id, $product_id, $order) {
    
    // Get vendor level
    $vendor_level = get_user_meta($vendor_id, 'vendor_level', true);
    
    // Adjust commission based on level
    switch($vendor_level) {
        case 'bronze':
            $rule['percent'] = 15; // 15% commission
            break;
        case 'silver':
            $rule['percent'] = 12; // 12% commission
            break;
        case 'gold':
            $rule['percent'] = 10; // 10% commission
            break;
        case 'platinum':
            $rule['percent'] = 7;  // 7% commission
            break;
        default:
            $rule['percent'] = 20; // Default 20% commission
    }
    
    // Special category commissions
    $product_cats = wp_get_post_terms($product_id, 'product_cat', array('fields' => 'ids'));
    
    // Electronics get different commission
    if (in_array(25, $product_cats)) { // 25 is electronics category ID
        $rule['percent'] = $rule['percent'] - 2; // 2% less commission
    }
    
    // Holiday season adjustment
    $current_month = date('n');
    if ($current_month == 11 || $current_month == 12) { // Nov-Dec
        $rule['percent'] = $rule['percent'] - 1; // 1% holiday bonus for vendors
    }
    
    return $rule;
}, 10, 4);
```

---

## AJAX Implementation

### Create Store Follow System

```php
// PHP Handler
class WCFM_Store_Follow {
    
    public function __construct() {
        add_action('wp_ajax_follow_store', array($this, 'handle_follow'));
        add_action('wp_ajax_nopriv_follow_store', array($this, 'handle_follow'));
        add_action('wp_enqueue_scripts', array($this, 'enqueue_scripts'));
    }
    
    public function handle_follow() {
        // Security check
        if (!wp_verify_nonce($_POST['nonce'], 'wcfm_follow_nonce')) {
            wp_die('Security check failed');
        }
        
        if (!is_user_logged_in()) {
            wp_send_json_error('Please login to follow stores');
        }
        
        $vendor_id = intval($_POST['vendor_id']);
        $user_id = get_current_user_id();
        
        // Get current follows
        $following = get_user_meta($user_id, 'following_stores', true) ?: array();
        
        if (in_array($vendor_id, $following)) {
            // Unfollow
            $following = array_diff($following, array($vendor_id));
            $message = 'Unfollowed';
            $is_following = false;
        } else {
            // Follow
            $following[] = $vendor_id;
            $message = 'Following';
            $is_following = true;
            
            // Send notification to vendor
            $this->notify_vendor($vendor_id, $user_id);
        }
        
        update_user_meta($user_id, 'following_stores', $following);
        
        // Update follower count
        $this->update_follower_count($vendor_id);
        
        wp_send_json_success(array(
            'message' => $message,
            'following' => $is_following,
            'follower_count' => get_user_meta($vendor_id, 'follower_count', true)
        ));
    }
    
    public function enqueue_scripts() {
        wp_enqueue_script(
            'wcfm-follow', 
            plugin_dir_url(__FILE__) . 'assets/js/follow.js',
            array('jquery'),
            '1.0.0',
            true
        );
        
        wp_localize_script('wcfm-follow', 'wcfm_follow', array(
            'ajax_url' => admin_url('admin-ajax.php'),
            'nonce' => wp_create_nonce('wcfm_follow_nonce')
        ));
    }
    
    private function update_follower_count($vendor_id) {
        global $wpdb;
        
        $count = $wpdb->get_var($wpdb->prepare(
            "SELECT COUNT(DISTINCT user_id) 
             FROM {$wpdb->usermeta} 
             WHERE meta_key = 'following_stores' 
             AND meta_value LIKE %s",
            '%"' . $vendor_id . '"%'
        ));
        
        update_user_meta($vendor_id, 'follower_count', $count);
    }
    
    private function notify_vendor($vendor_id, $follower_id) {
        // Create notification
        do_action('wcfm_notification', array(
            'type' => 'new_follower',
            'vendor_id' => $vendor_id,
            'follower_id' => $follower_id,
            'message' => get_userdata($follower_id)->display_name . ' is now following your store'
        ));
    }
}

new WCFM_Store_Follow();
```

```javascript
// JavaScript (follow.js)
jQuery(document).ready(function($) {
    
    $('.follow-store-btn').on('click', function(e) {
        e.preventDefault();
        
        var $btn = $(this);
        var vendor_id = $btn.data('vendor-id');
        
        $btn.addClass('loading');
        
        $.ajax({
            url: wcfm_follow.ajax_url,
            type: 'POST',
            data: {
                action: 'follow_store',
                vendor_id: vendor_id,
                nonce: wcfm_follow.nonce
            },
            success: function(response) {
                if (response.success) {
                    if (response.data.following) {
                        $btn.addClass('following')
                            .removeClass('not-following')
                            .html('<i class="fa fa-check"></i> Following');
                    } else {
                        $btn.removeClass('following')
                            .addClass('not-following')
                            .html('<i class="fa fa-plus"></i> Follow');
                    }
                    
                    // Update follower count
                    $('.follower-count').text(response.data.follower_count);
                    
                    // Show notification
                    showNotification(response.data.message);
                } else {
                    alert(response.data);
                }
            },
            complete: function() {
                $btn.removeClass('loading');
            }
        });
    });
    
    function showNotification(message) {
        var $notification = $('<div class="wcfm-notification">' + message + '</div>');
        $('body').append($notification);
        
        setTimeout(function() {
            $notification.addClass('show');
        }, 100);
        
        setTimeout(function() {
            $notification.removeClass('show');
            setTimeout(function() {
                $notification.remove();
            }, 300);
        }, 3000);
    }
});
```

---

## REST API Endpoints

### Create Custom API for Mobile Apps

```php
// Register REST routes
add_action('rest_api_init', function() {
    
    // Get all stores
    register_rest_route('wcfm/v1', '/stores', array(
        'methods' => 'GET',
        'callback' => 'wcfm_api_get_stores',
        'permission_callback' => '__return_true',
        'args' => array(
            'per_page' => array(
                'default' => 10,
                'sanitize_callback' => 'absint'
            ),
            'page' => array(
                'default' => 1,
                'sanitize_callback' => 'absint'
            ),
            'search' => array(
                'sanitize_callback' => 'sanitize_text_field'
            ),
            'category' => array(
                'sanitize_callback' => 'sanitize_text_field'
            )
        )
    ));
    
    // Get single store
    register_rest_route('wcfm/v1', '/store/(?P<id>\d+)', array(
        'methods' => 'GET',
        'callback' => 'wcfm_api_get_store',
        'permission_callback' => '__return_true'
    ));
    
    // Get store products
    register_rest_route('wcfm/v1', '/store/(?P<id>\d+)/products', array(
        'methods' => 'GET',
        'callback' => 'wcfm_api_get_store_products',
        'permission_callback' => '__return_true'
    ));
});

// API callback functions
function wcfm_api_get_stores($request) {
    $args = array(
        'role' => 'wcfm_vendor',
        'number' => $request['per_page'],
        'paged' => $request['page']
    );
    
    if ($request['search']) {
        $args['search'] = '*' . $request['search'] . '*';
    }
    
    $vendors = new WP_User_Query($args);
    $stores = array();
    
    foreach ($vendors->results as $vendor) {
        $store_user = wcfmmp_get_store($vendor->ID);
        
        $stores[] = array(
            'id' => $vendor->ID,
            'name' => $store_user->get_shop_name(),
            'url' => $store_user->get_shop_url(),
            'logo' => $store_user->get_avatar(),
            'banner' => $store_user->get_banner(),
            'rating' => $store_user->get_avg_review_rating(),
            'location' => $store_user->get_address(),
            'phone' => $store_user->get_phone(),
            'email' => $store_user->get_email(),
            'social' => array(
                'facebook' => $store_user->get_facebook(),
                'twitter' => $store_user->get_twitter(),
                'instagram' => $store_user->get_instagram()
            )
        );
    }
    
    return new WP_REST_Response($stores, 200);
}
```

---

## Database Operations

### Custom Database Queries

```php
// Get top performing vendors
function get_top_vendors($limit = 10) {
    global $wpdb;
    
    $results = $wpdb->get_results($wpdb->prepare(
        "SELECT 
            v.vendor_id,
            u.display_name as vendor_name,
            COUNT(DISTINCT v.order_id) as total_orders,
            SUM(v.gross_total) as total_sales,
            AVG(r.review_rating) as avg_rating
        FROM {$wpdb->prefix}wcfm_marketplace_orders v
        LEFT JOIN {$wpdb->users} u ON v.vendor_id = u.ID
        LEFT JOIN {$wpdb->prefix}wcfm_marketplace_reviews r ON v.vendor_id = r.vendor_id
        WHERE v.order_status = 'completed'
        AND v.created >= DATE_SUB(NOW(), INTERVAL 30 DAY)
        GROUP BY v.vendor_id
        ORDER BY total_sales DESC
        LIMIT %d",
        $limit
    ));
    
    return $results;
}

// Get vendor analytics
function get_vendor_analytics($vendor_id, $days = 30) {
    global $wpdb;
    
    return $wpdb->get_row($wpdb->prepare(
        "SELECT 
            COUNT(DISTINCT order_id) as total_orders,
            SUM(gross_total) as gross_sales,
            SUM(commission) as total_commission,
            AVG(gross_total) as avg_order_value,
            COUNT(DISTINCT customer_id) as unique_customers
        FROM {$wpdb->prefix}wcfm_marketplace_orders
        WHERE vendor_id = %d
        AND created >= DATE_SUB(NOW(), INTERVAL %d DAY)
        AND order_status IN ('completed', 'processing')",
        $vendor_id,
        $days
    ));
}
```

---

## Performance Optimization

### Implement Caching

```php
// Cache vendor data
class WCFM_Cache_Manager {
    
    private $cache_group = 'wcfm_vendor';
    private $cache_time = 3600; // 1 hour
    
    public function get_vendor_data($vendor_id) {
        $cache_key = 'vendor_' . $vendor_id;
        $data = wp_cache_get($cache_key, $this->cache_group);
        
        if ($data === false) {
            $data = $this->fetch_vendor_data($vendor_id);
            wp_cache_set($cache_key, $data, $this->cache_group, $this->cache_time);
        }
        
        return $data;
    }
    
    private function fetch_vendor_data($vendor_id) {
        $store = wcfmmp_get_store($vendor_id);
        
        return array(
            'info' => $store->get_shop_info(),
            'products' => $this->get_vendor_products($vendor_id),
            'rating' => $store->get_avg_review_rating(),
            'reviews' => $store->get_reviews_count(),
            'followers' => get_user_meta($vendor_id, 'follower_count', true)
        );
    }
    
    public function clear_vendor_cache($vendor_id) {
        $cache_key = 'vendor_' . $vendor_id;
        wp_cache_delete($cache_key, $this->cache_group);
    }
}
```

---

## Security Best Practices

### Secure Custom Endpoints

```php
// Always verify nonces
if (!wp_verify_nonce($_POST['nonce'], 'wcfm_action')) {
    wp_die('Security check failed');
}

// Sanitize all inputs
$vendor_id = absint($_POST['vendor_id']);
$search_term = sanitize_text_field($_POST['search']);
$email = sanitize_email($_POST['email']);

// Check capabilities
if (!current_user_can('manage_woocommerce')) {
    wp_die('Insufficient permissions');
}

// Validate vendor
if (!wcfm_is_vendor($vendor_id)) {
    wp_die('Invalid vendor');
}

// Escape output
echo esc_html($vendor_name);
echo esc_url($store_url);
echo esc_attr($css_class);
```

---

## Debugging and Testing

### Enable Debug Logging

```php
// In wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
define('WCFM_DEBUG', true);

// Custom debug function
function wcfm_debug_log($message, $data = null) {
    if (!defined('WCFM_DEBUG') || !WCFM_DEBUG) {
        return;
    }
    
    $log_message = '[WCFM Debug] ' . $message;
    
    if ($data !== null) {
        $log_message .= ' - Data: ' . print_r($data, true);
    }
    
    error_log($log_message);
}

// Usage
wcfm_debug_log('Vendor registration', $_POST);
wcfm_debug_log('Commission calculated', array('vendor' => $vendor_id, 'amount' => $commission));
```

---

## Next Steps

- [Troubleshooting Guide](07-troubleshooting.md) - Fix common issues
- [FAQ](08-faq.md) - Frequently asked questions
- [Store Customization](04-store-customization.md) - Frontend customization

---

**Developer Resources:**  
📚 [WCFM Documentation](https://wclovers.com/docs)  
💻 [GitHub Examples](https://github.com/wclovers)  
🔧 [Support Forum](https://wclovers.com/forums)