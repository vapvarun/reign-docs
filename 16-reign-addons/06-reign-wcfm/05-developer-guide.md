# Reign WCFM Addon - Developer Guide

## Overview

The Reign WCFM Addon provides hooks and filters for customizing WCFM integration with the Reign theme. This guide covers the available developer features.

## Plugin Structure (Verified)

```
reign-wcfm-addon/
├── admin/                  # Admin settings and license
├── public/                 # Public-facing functionality
│   ├── css/               # Styling files
│   ├── js/                # JavaScript files
│   └── buddypress/        # BuddyPress integration
├── templates/             # Template overrides
└── reign-wcfm-addon.php  # Main plugin file
```

## Available Hooks and Filters

### Template System

#### Template Override Filter
```php
// Filter WCFM template locations
add_filter('wcfm_locate_template', 'custom_wcfm_template_override', 10, 4);
function custom_wcfm_template_override($template, $template_name, $template_path, $default_path) {
    // Custom template logic
    return $template;
}
```

### Store Layout Filter

#### Store Wrapper Class
```php
// Add custom classes to store wrapper
add_filter('wcfm_store_wrapper_class', 'custom_store_classes');
function custom_store_classes($classes) {
    $classes .= ' custom-store-class';
    return $classes;
}
```

### BuddyPress Integration

#### Customize Tab Names
```php
// Customize favorite products tab name
add_filter('reign_wcfm_favourite_product_tab_name', function($name) {
    return __('My Favorites', 'textdomain');
});

// Customize vendor store tab name
add_filter('reign_wcfm_vendor_store_tab_name', function($name) {
    return __('Vendor Shop', 'textdomain');
});
```

#### Activity Stream Integration
```php
// Hook into product creation activity
add_action('transition_post_status', 'custom_product_activity', 10, 3);
function custom_product_activity($new_status, $old_status, $post) {
    if ($post->post_type === 'product' && $new_status === 'publish') {
        // Custom activity logic
    }
}
```

### Favorite Products System

#### Custom Favorite Products Query
```php
// Modify favorite products query
add_filter('woocommerce_shortcode_products_query', 'custom_favorite_products', 10, 3);
function custom_favorite_products($query_args, $attributes, $type) {
    if (bp_is_current_component('favourite')) {
        // Custom query modifications
    }
    return $query_args;
}
```

## Template Customization

### Override Templates

Copy templates from plugin to theme:

**Source:**
```
/wp-content/plugins/reign-wcfm-addon/templates/
```

**Destination:**
```
/wp-content/themes/your-theme/wcfm/
```

### Available Templates
- Store layout templates
- BuddyPress integration templates
- Activity stream templates

## JavaScript Integration

### AJAX Parameters
The addon provides localized JavaScript parameters:
```javascript
// Available in reign_wcfm_addon_js_params
ajax_url    // WordPress AJAX URL
home_url    // Site home URL
nonce       // Security nonce
```

### Custom AJAX Handlers
```php
// Add custom AJAX handler
add_action('wp_ajax_custom_wcfm_action', 'handle_custom_wcfm_action');
add_action('wp_ajax_nopriv_custom_wcfm_action', 'handle_custom_wcfm_action');

function handle_custom_wcfm_action() {
    // Verify nonce
    if (!wp_verify_nonce($_POST['nonce'], 'reign-wcfm-nonce')) {
        wp_die('Security check failed');
    }

    // Custom logic
    wp_send_json_success($response);
}
```

## BuddyPress Development

### Profile Tab Development
```php
// Add custom profile tab
add_action('bp_setup_nav', 'add_custom_wcfm_tab');
function add_custom_wcfm_tab() {
    bp_core_new_nav_item(array(
        'name' => __('Custom Tab', 'textdomain'),
        'slug' => 'custom-tab',
        'screen_function' => 'custom_tab_screen_function',
        'position' => 90
    ));
}
```

### Activity Stream Development
```php
// Register custom activity type
add_action('bp_register_activity_actions', 'register_custom_wcfm_activity');
function register_custom_wcfm_activity() {
    bp_activity_set_action(
        'wcfm',
        'custom_action',
        __('Custom WCFM Action', 'textdomain')
    );
}
```

## Security Considerations

### Nonce Verification
Always verify nonces in AJAX handlers:
```php
if (!wp_verify_nonce($_POST['nonce'], 'reign-wcfm-nonce')) {
    wp_die('Security check failed');
}
```

### User Capability Checks
```php
if (!current_user_can('manage_woocommerce')) {
    wp_die('Insufficient permissions');
}
```

### Data Sanitization
```php
$product_id = absint($_POST['product_id']);
$action = sanitize_text_field($_POST['action']);
```

---

*Developer guide verified against Reign WCFM Addon v1.8.3 source code*