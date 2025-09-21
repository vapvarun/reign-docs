# Reign Dokan Addon - Developer Guide

## Architecture Overview

### Plugin Structure

```
reign-dokan-addon/
├── reign-dokan-addon.php          # Main plugin file
├── inc/
│   ├── class-reign-dokan-loader.php
│   ├── class-reign-dokan-public.php
│   ├── class-reign-dokan-admin.php
│   ├── class-reign-dokan-templates.php
│   ├── class-reign-dokan-widgets.php
│   └── class-reign-dokan-buddypress.php
├── templates/
│   ├── store/
│   ├── vendor/
│   └── widgets/
└── assets/
    ├── css/
    ├── js/
    └── images/
```

### Class Hierarchy

```php
Reign_Dokan_Addon
├── Reign_Dokan_Loader
├── Reign_Dokan_Public
├── Reign_Dokan_Admin
├── Reign_Dokan_Templates
├── Reign_Dokan_Widgets
└── Reign_Dokan_BuddyPress
```

## Core Classes

### Main Plugin Class

```php
/**
 * Main plugin class
 */
class Reign_Dokan_Addon {
    
    /**
     * Plugin version
     */
    const VERSION = '3.5.4';
    
    /**
     * Plugin instance
     */
    private static $instance = null;
    
    /**
     * Get plugin instance
     */
    public static function get_instance() {
        if (null === self::$instance) {
            self::$instance = new self();
        }
        return self::$instance;
    }
    
    /**
     * Constructor
     */
    private function __construct() {
        $this->define_constants();
        $this->includes();
        $this->init_hooks();
    }
    
    /**
     * Define constants
     */
    private function define_constants() {
        define('REIGN_DOKAN_VERSION', self::VERSION);
        define('REIGN_DOKAN_PATH', plugin_dir_path(__FILE__));
        define('REIGN_DOKAN_URL', plugin_dir_url(__FILE__));
    }
}
```

### Template Loader Class

```php
/**
 * Template management
 */
class Reign_Dokan_Templates {
    
    /**
     * Get template
     */
    public static function get_template($template_name, $args = array()) {
        // Extract args
        if ($args) {
            extract($args);
        }
        
        // Look for template in theme
        $template = locate_template(array(
            'reign-dokan/' . $template_name,
            $template_name
        ));
        
        // Fallback to plugin template
        if (!$template) {
            $template = REIGN_DOKAN_PATH . 'templates/' . $template_name;
        }
        
        // Allow filtering
        $template = apply_filters('reign_dokan_get_template', $template, $template_name, $args);
        
        if (file_exists($template)) {
            include $template;
        }
    }
    
    /**
     * Get template part
     */
    public static function get_template_part($slug, $name = '') {
        $template = '';
        
        // Look in theme
        if ($name) {
            $template = locate_template(array(
                "reign-dokan/{$slug}-{$name}.php",
                "reign-dokan/{$slug}.php"
            ));
        }
        
        // Get default from plugin
        if (!$template && $name && file_exists(REIGN_DOKAN_PATH . "templates/{$slug}-{$name}.php")) {
            $template = REIGN_DOKAN_PATH . "templates/{$slug}-{$name}.php";
        }
        
        if (!$template) {
            $template = REIGN_DOKAN_PATH . "templates/{$slug}.php";
        }
        
        // Allow filtering
        $template = apply_filters('reign_dokan_get_template_part', $template, $slug, $name);
        
        if ($template) {
            load_template($template, false);
        }
    }
}
```

## Hooks and Filters

### Action Hooks

```php
/**
 * Available action hooks
 */

// Store listing
do_action('reign_dokan_before_store_listing');
do_action('reign_dokan_after_store_listing');
do_action('reign_dokan_store_card_before', $vendor_id);
do_action('reign_dokan_store_card_after', $vendor_id);

// Single store
do_action('reign_dokan_before_store_header', $vendor_id);
do_action('reign_dokan_after_store_header', $vendor_id);
do_action('reign_dokan_before_store_tabs', $vendor_id);
do_action('reign_dokan_after_store_tabs', $vendor_id);

// Vendor dashboard
do_action('reign_dokan_dashboard_before');
do_action('reign_dokan_dashboard_after');
do_action('reign_dokan_dashboard_widget', $widget_id);
```

### Filter Hooks

```php
/**
 * Available filter hooks
 */

// Store query
add_filter('reign_dokan_store_query_args', function($args) {
    // Modify store query
    $args['meta_query'] = array(
        array(
            'key' => 'featured_vendor',
            'value' => 'yes'
        )
    );
    return $args;
});

// Store data
add_filter('reign_dokan_store_data', function($data, $vendor_id) {
    // Add custom data
    $data['custom_field'] = get_user_meta($vendor_id, 'custom_field', true);
    return $data;
}, 10, 2);

// Template paths
add_filter('reign_dokan_template_path', function($path, $template) {
    // Change template path
    return $path;
}, 10, 2);
```

## Template Override System

### Override Templates in Theme

```php
/**
 * Template hierarchy
 */

// Theme template locations (in order of priority):
// 1. /theme/reign-dokan/store-listing.php
// 2. /theme/templates/reign-dokan/store-listing.php
// 3. /plugin/templates/store-listing.php (fallback)

// Example: Override store header
// Copy from: /plugins/reign-dokan-addon/templates/store-header.php
// Paste to: /themes/reign-theme/reign-dokan/store-header.php
```

### Creating Custom Templates

```php
/**
 * Custom template example
 */

// In theme's functions.php
add_filter('reign_dokan_get_template', function($template, $template_name, $args) {
    if ($template_name === 'store/featured-badge.php') {
        // Use custom template
        return get_stylesheet_directory() . '/custom-templates/featured-badge.php';
    }
    return $template;
}, 10, 3);
```

## Widget Development

### Creating Custom Widget

```php
/**
 * Custom Dokan widget
 */
class Reign_Dokan_Custom_Widget extends WP_Widget {
    
    public function __construct() {
        parent::__construct(
            'reign_dokan_custom',
            __('Reign Dokan Custom Widget', 'reign-dokan'),
            array('description' => __('Custom widget for Dokan stores', 'reign-dokan'))
        );
    }
    
    public function widget($args, $instance) {
        // Get current vendor
        $vendor_id = get_query_var('author');
        
        if (!dokan_is_store_page() || !$vendor_id) {
            return;
        }
        
        $vendor = dokan()->vendor->get($vendor_id);
        
        echo $args['before_widget'];
        
        if (!empty($instance['title'])) {
            echo $args['before_title'] . apply_filters('widget_title', $instance['title']) . $args['after_title'];
        }
        
        // Widget content
        Reign_Dokan_Templates::get_template('widgets/custom-widget.php', array(
            'vendor' => $vendor,
            'instance' => $instance
        ));
        
        echo $args['after_widget'];
    }
    
    public function form($instance) {
        // Widget admin form
        $title = !empty($instance['title']) ? $instance['title'] : '';
        ?>
        <p>
            <label for="<?php echo esc_attr($this->get_field_id('title')); ?>">
                <?php esc_attr_e('Title:', 'reign-dokan'); ?>
            </label>
            <input class="widefat" 
                   id="<?php echo esc_attr($this->get_field_id('title')); ?>" 
                   name="<?php echo esc_attr($this->get_field_name('title')); ?>" 
                   type="text" 
                   value="<?php echo esc_attr($title); ?>">
        </p>
        <?php
    }
}

// Register widget
add_action('widgets_init', function() {
    register_widget('Reign_Dokan_Custom_Widget');
});
```

## AJAX Implementation

### AJAX Handler

```php
/**
 * AJAX functionality
 */
class Reign_Dokan_Ajax {
    
    public function __construct() {
        // Public AJAX
        add_action('wp_ajax_nopriv_reign_dokan_filter', array($this, 'filter_stores'));
        add_action('wp_ajax_reign_dokan_filter', array($this, 'filter_stores'));
        
        // Private AJAX
        add_action('wp_ajax_reign_dokan_follow', array($this, 'follow_vendor'));
    }
    
    /**
     * Filter stores
     */
    public function filter_stores() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_dokan_nonce')) {
            wp_die('Security check failed');
        }
        
        // Get filter parameters
        $category = sanitize_text_field($_POST['category']);
        $location = sanitize_text_field($_POST['location']);
        $rating = intval($_POST['rating']);
        
        // Build query
        $args = array(
            'role' => 'seller',
            'number' => 12,
            'paged' => $_POST['page'] ?? 1
        );
        
        // Add meta query
        if ($category) {
            $args['meta_query'][] = array(
                'key' => 'store_category',
                'value' => $category
            );
        }
        
        // Get vendors
        $vendors = new WP_User_Query($args);
        
        // Build response
        ob_start();
        
        if ($vendors->results) {
            foreach ($vendors->results as $vendor) {
                Reign_Dokan_Templates::get_template('store-card.php', array(
                    'vendor' => $vendor
                ));
            }
        } else {
            echo '<p>' . __('No stores found', 'reign-dokan') . '</p>';
        }
        
        $html = ob_get_clean();
        
        wp_send_json_success(array(
            'html' => $html,
            'found' => $vendors->total_users,
            'max_pages' => ceil($vendors->total_users / 12)
        ));
    }
}
```

### JavaScript Integration

```javascript
/**
 * AJAX JavaScript
 */
(function($) {
    'use strict';
    
    var ReignDokan = {
        
        init: function() {
            this.bindEvents();
        },
        
        bindEvents: function() {
            $(document).on('click', '.reign-dokan-filter', this.filterStores);
            $(document).on('click', '.reign-follow-vendor', this.followVendor);
        },
        
        filterStores: function(e) {
            e.preventDefault();
            
            var $button = $(this);
            var data = {
                action: 'reign_dokan_filter',
                nonce: reign_dokan_vars.nonce,
                category: $('#store-category').val(),
                location: $('#store-location').val(),
                rating: $('#store-rating').val()
            };
            
            $button.addClass('loading');
            
            $.post(reign_dokan_vars.ajax_url, data, function(response) {
                if (response.success) {
                    $('.dokan-store-listing').html(response.data.html);
                    
                    // Update pagination
                    if (response.data.max_pages > 1) {
                        // Show pagination
                    }
                }
                $button.removeClass('loading');
            });
        },
        
        followVendor: function(e) {
            e.preventDefault();
            
            if (!reign_dokan_vars.is_logged_in) {
                alert('Please login to follow vendors');
                return;
            }
            
            var $button = $(this);
            var vendor_id = $button.data('vendor-id');
            
            $.post(reign_dokan_vars.ajax_url, {
                action: 'reign_dokan_follow',
                nonce: reign_dokan_vars.nonce,
                vendor_id: vendor_id
            }, function(response) {
                if (response.success) {
                    $button.toggleClass('following');
                    $button.text(response.data.button_text);
                }
            });
        }
    };
    
    $(document).ready(function() {
        ReignDokan.init();
    });
    
})(jQuery);
```

## REST API Endpoints

### Custom REST Routes

```php
/**
 * Register REST API endpoints
 */
add_action('rest_api_init', function() {
    
    // Get stores endpoint
    register_rest_route('reign-dokan/v1', '/stores', array(
        'methods' => 'GET',
        'callback' => 'reign_dokan_get_stores',
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
            'category' => array(
                'sanitize_callback' => 'sanitize_text_field'
            )
        )
    ));
    
    // Get store details
    register_rest_route('reign-dokan/v1', '/store/(?P<id>\d+)', array(
        'methods' => 'GET',
        'callback' => 'reign_dokan_get_store',
        'permission_callback' => '__return_true'
    ));
});

/**
 * Get stores callback
 */
function reign_dokan_get_stores($request) {
    $args = array(
        'role' => 'seller',
        'number' => $request['per_page'],
        'paged' => $request['page']
    );
    
    if ($request['category']) {
        $args['meta_query'] = array(
            array(
                'key' => 'store_category',
                'value' => $request['category']
            )
        );
    }
    
    $vendors = new WP_User_Query($args);
    $stores = array();
    
    foreach ($vendors->results as $vendor) {
        $store = dokan()->vendor->get($vendor->ID);
        $stores[] = array(
            'id' => $vendor->ID,
            'name' => $store->get_shop_name(),
            'url' => $store->get_shop_url(),
            'logo' => $store->get_avatar(),
            'banner' => $store->get_banner(),
            'rating' => $store->get_rating(),
            'products' => $store->get_product_count()
        );
    }
    
    return new WP_REST_Response($stores, 200);
}
```

## Database Operations

### Custom Tables

```php
/**
 * Create custom tables
 */
function reign_dokan_create_tables() {
    global $wpdb;
    
    $charset_collate = $wpdb->get_charset_collate();
    
    $sql = "CREATE TABLE IF NOT EXISTS {$wpdb->prefix}reign_dokan_follows (
        id bigint(20) NOT NULL AUTO_INCREMENT,
        user_id bigint(20) NOT NULL,
        vendor_id bigint(20) NOT NULL,
        followed_at datetime DEFAULT CURRENT_TIMESTAMP,
        PRIMARY KEY (id),
        KEY user_id (user_id),
        KEY vendor_id (vendor_id),
        UNIQUE KEY user_vendor (user_id, vendor_id)
    ) $charset_collate;";
    
    require_once(ABSPATH . 'wp-admin/includes/upgrade.php');
    dbDelta($sql);
}

// Run on activation
register_activation_hook(__FILE__, 'reign_dokan_create_tables');
```

### Data Queries

```php
/**
 * Custom queries
 */
class Reign_Dokan_Query {
    
    /**
     * Get featured vendors
     */
    public static function get_featured_vendors($limit = 6) {
        global $wpdb;
        
        $results = $wpdb->get_results(
            $wpdb->prepare(
                "SELECT user_id 
                FROM {$wpdb->usermeta} 
                WHERE meta_key = 'dokan_feature_seller' 
                AND meta_value = 'yes' 
                LIMIT %d",
                $limit
            )
        );
        
        $vendors = array();
        foreach ($results as $result) {
            $vendors[] = dokan()->vendor->get($result->user_id);
        }
        
        return $vendors;
    }
    
    /**
     * Get top rated vendors
     */
    public static function get_top_rated_vendors($limit = 10) {
        global $wpdb;
        
        $results = $wpdb->get_results(
            $wpdb->prepare(
                "SELECT vendor_id, AVG(rating) as avg_rating 
                FROM {$wpdb->prefix}dokan_vendor_balance 
                GROUP BY vendor_id 
                ORDER BY avg_rating DESC 
                LIMIT %d",
                $limit
            )
        );
        
        return $results;
    }
}
```

## Performance Optimization

### Caching Implementation

```php
/**
 * Cache management
 */
class Reign_Dokan_Cache {
    
    /**
     * Get cached data
     */
    public static function get($key) {
        return get_transient('reign_dokan_' . $key);
    }
    
    /**
     * Set cached data
     */
    public static function set($key, $data, $expiration = 3600) {
        return set_transient('reign_dokan_' . $key, $data, $expiration);
    }
    
    /**
     * Delete cached data
     */
    public static function delete($key) {
        return delete_transient('reign_dokan_' . $key);
    }
    
    /**
     * Clear all cache
     */
    public static function flush() {
        global $wpdb;
        
        $wpdb->query(
            "DELETE FROM {$wpdb->options} 
            WHERE option_name LIKE '_transient_reign_dokan_%' 
            OR option_name LIKE '_transient_timeout_reign_dokan_%'"
        );
    }
}

// Usage example
$vendors = Reign_Dokan_Cache::get('featured_vendors');

if (!$vendors) {
    $vendors = Reign_Dokan_Query::get_featured_vendors();
    Reign_Dokan_Cache::set('featured_vendors', $vendors, HOUR_IN_SECONDS);
}
```

## Security Best Practices

### Nonce Verification

```php
/**
 * Security checks
 */
function reign_dokan_verify_request() {
    // Check nonce
    if (!wp_verify_nonce($_REQUEST['_wpnonce'], 'reign_dokan_action')) {
        wp_die(__('Security check failed', 'reign-dokan'));
    }
    
    // Check capabilities
    if (!current_user_can('edit_posts')) {
        wp_die(__('Permission denied', 'reign-dokan'));
    }
    
    // Sanitize input
    $vendor_id = absint($_POST['vendor_id']);
    $action = sanitize_text_field($_POST['action']);
    
    // Validate vendor
    if (!dokan_is_user_seller($vendor_id)) {
        wp_die(__('Invalid vendor', 'reign-dokan'));
    }
}
```

## Testing

### Unit Tests

```php
/**
 * PHPUnit test example
 */
class Test_Reign_Dokan extends WP_UnitTestCase {
    
    public function setUp() {
        parent::setUp();
        
        // Create test vendor
        $this->vendor_id = $this->factory->user->create(array(
            'role' => 'seller'
        ));
        
        // Set vendor meta
        update_user_meta($this->vendor_id, 'dokan_enable_selling', 'yes');
    }
    
    public function test_vendor_creation() {
        $vendor = dokan()->vendor->get($this->vendor_id);
        
        $this->assertInstanceOf('WeDevs\Dokan\Vendor\Vendor', $vendor);
        $this->assertTrue($vendor->is_vendor());
    }
    
    public function test_store_url() {
        $vendor = dokan()->vendor->get($this->vendor_id);
        $url = $vendor->get_shop_url();
        
        $this->assertContains('/store/', $url);
    }
}
```

## Debugging

### Debug Logger

```php
/**
 * Debug logging
 */
class Reign_Dokan_Debug {
    
    public static function log($message, $type = 'info') {
        if (!defined('REIGN_DOKAN_DEBUG') || !REIGN_DOKAN_DEBUG) {
            return;
        }
        
        $log_file = WP_CONTENT_DIR . '/debug-reign-dokan.log';
        $timestamp = current_time('mysql');
        
        $entry = sprintf(
            "[%s] [%s] %s\n",
            $timestamp,
            strtoupper($type),
            $message
        );
        
        error_log($entry, 3, $log_file);
    }
}

// Usage
Reign_Dokan_Debug::log('Vendor query executed', 'info');
Reign_Dokan_Debug::log('Error loading template: ' . $template, 'error');
```

## Resources

- [Dokan Documentation](https://wedevs.com/docs/dokan/)
- [WordPress Plugin Handbook](https://developer.wordpress.org/plugins/)
- [Reign Theme Developer Docs](https://wbcomdesigns.com/docs/reign-theme/)
- [Support Forum](https://wbcomdesigns.com/support/)