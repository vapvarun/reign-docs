# Reign Dokan Addon - Developer Guide

## 🛠️ Build Amazing Marketplace Features

This comprehensive guide provides everything developers need to extend, customize, and integrate with Reign Dokan Addon. From simple hooks to advanced customizations - we've got you covered.

## 📦 Plugin Architecture (Complete Structure)

### Directory Structure
```
reign-dokan-addon/
├── admin/
│   ├── class-reign-dokan-admin-settings.php
│   └── reign-dokan-vertical-tabs-skeleton.php
├── assets/
│   ├── css/
│   ├── images/
│   └── js/
├── buddypress/
│   ├── class-reign-dokan-buddypress-addon.php
│   ├── class-reign-dokan-favourite-product-profile-tab.php
│   └── reign-dokan-activity.php
├── core/
│   ├── class-reign-dokan-favourite-product.php
│   ├── class-reign-dokan-single-product.php
│   ├── class-reign-dokan-theme-hooks.php
│   └── reign-dokan-functions.php
├── dokan/                              # Template overrides
│   ├── orders/
│   │   └── listing.php
│   ├── products/
│   │   ├── products-listing.php
│   │   └── products-listing-row.php
│   ├── review/
│   │   ├── listing.php
│   │   └── listing-table-tr.php
│   ├── store-header.php
│   ├── store-lists.php
│   ├── store-lists-loop.php
│   ├── store-reviews.php
│   ├── store-sidebar.php
│   ├── store-toc.php
│   ├── store.php
│   └── vendor-biography.php
├── edd-license/                        # License management
├── languages/                          # Translations
├── rda-shortcodes/
│   └── class-reign-dokan-shortcodes.php
├── rda-widgets/                        # Custom widgets
├── readme.txt
└── reign-dokan-addon.php              # Main plugin file
```

## Main Plugin Class

### File: `/reign-dokan-addon.php`

```php
class Reign_Dokan_Addon {
    // Version
    public $version = '3.5.4';

    // Singleton instance
    protected static $_instance = null;

    // Get instance
    public static function instance() {
        if (is_null(self::$_instance)) {
            self::$_instance = new self();
        }
        return self::$_instance;
    }

    // Constructor
    public function __construct() {
        $this->define_constants();
        $this->includes();
        $this->init_hooks();
        do_action('reign_dokan_addon_loaded');
    }
}
```

---

## 🎯 Core Hooks and Filters

### 🚀 Essential Actions

#### Plugin Initialization Hook
**`reign_dokan_addon_loaded`** - Your entry point for customizations
```php
// Hook into plugin initialization
add_action('reign_dokan_addon_loaded', function() {
    // Your custom marketplace features here
});
```
**Use this for:** Adding custom features, registering post types, enqueueing assets

### 🔧 Powerful Filters

#### `dokan_get_template_part`
Override Dokan template parts
```php
add_filter('dokan_get_template_part', array($this, 'dokan_get_template_part'), 10, 3);
```

#### `dokan_locate_template`
Modify template locations
```php
add_filter('dokan_locate_template', array($this, 'reign_dokan_locate_template'), 10, 3);
```

#### `rda_dokan_seller_listing_args`
Customize seller query
```php
add_filter('rda_dokan_seller_listing_args', function($args) {
    $args['number'] = 20;
    $args['orderby'] = 'registered';
    return $args;
});
```

#### `rda_dokan_store_list_args`
Modify store list template arguments
```php
add_filter('rda_dokan_store_list_args', function($args) {
    $args['show_products'] = true;
    $args['image_size'] = 'full';
    return $args;
});
```

#### `rda_store_list_loop_products_to_display`
Control products per store in listings
```php
add_filter('rda_store_list_loop_products_to_display', function() {
    return 5; // Show 5 products per store
});
```

#### `rda_dokan_store_listing_per_page`
Modify store listing defaults
```php
add_filter('rda_dokan_store_listing_per_page', function($defaults) {
    $defaults['per_page'] = 20;
    return $defaults;
});
```

## Shortcode Implementation

### File: `/rda-shortcodes/class-reign-dokan-shortcodes.php`

#### Register Shortcodes
```php
class Reign_Dokan_Shortcodes {
    public function __construct() {
        $this->init_hooks();
    }

    private function init_hooks() {
        add_shortcode('rda_dokan_vendors', array($this, 'render_rda_dokan_vendors'));
        add_shortcode('rda_dokan_store_listing', array($this, 'render_rda_dokan_store_listing'));
    }
}
```

#### Vendor Shortcode Implementation
```php
public function render_rda_dokan_vendors($atts = array()) {
    $atts = wp_parse_args((array) $atts, array(
        'title' => __('Featured Vendor', 'reign-dokan'),
        'per_row' => '3',
        'count' => '6',
        'show_featured_only' => false,
        'enable_slider' => false,
        'layout' => 'layout-type-1',
        'selected_vendors' => '',
    ));

    // Template output
    dokan_get_template_part('widgets/rda-sellers', '', array('atts' => $atts));
}
```

## BuddyPress Integration

### File: `/buddypress/class-reign-dokan-buddypress-addon.php`

#### Add Store Tab to Profiles
```php
class Reign_Dokan_BuddyPress_Addon {
    public function add_store_tab() {
        // Adds vendor store tab to BuddyPress profiles
        // Shows vendor products
        // Manages favorite products
    }
}
```

### File: `/buddypress/class-reign-dokan-favourite-product-profile-tab.php`

#### Favorite Products Feature
```php
class Reign_Dokan_Favourite_Product_Profile_Tab {
    // Adds favorite products tab
    // Manages user favorites
    // Ajax handlers for marking favorites
}
```

## Template Override System

### How It Works
1. Plugin checks theme directory: `/wp-content/themes/your-theme/dokan/`
2. Falls back to addon templates: `/wp-content/plugins/reign-dokan-addon/dokan/`
3. Finally uses original Dokan templates

### Override a Template
```php
// Copy from:
/wp-content/plugins/reign-dokan-addon/dokan/store-header.php

// To:
/wp-content/themes/your-theme/dokan/store-header.php

// Edit the copied file
```

## Working with Theme Settings

### Read Settings
```php
// Get theme mod values
$header_location = get_theme_mod('reign_dokan_store_header_location', true);
$show_vendor_info = get_theme_mod('reign_dokan_show_vendor_info_in_pro_page', false);
$products_count = get_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 10);
```

### Use in Conditionals
```php
if (get_theme_mod('reign_dokan_show_vendor_pros_on_pro_page', false)) {
    // Display vendor products section
    $count = get_theme_mod('reign_dokan_num_of_vendor_pros_on_pro_page', 10);
    // Query and display products
}
```

## Ajax Implementation

### Favorite Products Ajax
```php
// Ajax action for marking favorites
add_action('wp_ajax_reign_dokan_mark_favorite', 'handle_favorite');
add_action('wp_ajax_nopriv_reign_dokan_mark_favorite', 'handle_favorite');

function handle_favorite() {
    // Verify nonce
    // Process favorite action
    // Return JSON response
}
```

## Custom Widget Development

### Creating a Custom Widget
```php
class Reign_Dokan_Custom_Widget extends WP_Widget {
    public function __construct() {
        parent::__construct(
            'reign_dokan_custom',
            __('Reign Dokan Widget', 'reign-dokan')
        );
    }

    public function widget($args, $instance) {
        // Widget output
    }
}

// Register widget
add_action('widgets_init', function() {
    register_widget('Reign_Dokan_Custom_Widget');
});
```

## Database Queries

### Get Vendor Products
```php
// Query vendor products
$vendor_id = get_current_user_id();
$args = array(
    'post_type' => 'product',
    'author' => $vendor_id,
    'posts_per_page' => 10
);
$products = new WP_Query($args);
```

### Get Featured Vendors
```php
// Query featured vendors
$vendors = dokan_get_sellers(array(
    'featured' => 'yes',
    'number' => 6
));
```

---

## 🔒 Security Best Practices (Essential!)

### ✅ Nonce Verification (Always Required)
```php
// Protect all Ajax and form handlers
if (!wp_verify_nonce($_POST['nonce'], 'reign_dokan_nonce')) {
    wp_die('Security check failed');
}
```
**Why:** Prevents CSRF attacks and unauthorized actions

### 🧹 Data Sanitization (Clean All Input)
```php
// Sanitize different types of user input
$vendor_id = absint($_POST['vendor_id']);           // Numbers only
$search_term = sanitize_text_field($_POST['search']); // Plain text
$html_content = wp_kses_post($_POST['content']);     // Safe HTML
$email = sanitize_email($_POST['email']);            // Email addresses
$url = esc_url_raw($_POST['website']);               // URLs
```
**Rule:** Never trust user input - always sanitize!

### 👤 Capability Checks (Permission Control)
```php
// Always check user permissions
if (!current_user_can('dokan_view_store')) {
    wp_die('Permission denied');
}

// Common capability checks
if (current_user_can('manage_options')) {}      // Admin only
if (current_user_can('dokan_add_product')) {}   // Vendor only
if (is_user_logged_in()) {}                     // Members only
```
**Best Practice:** Check permissions before any sensitive operation

## Performance Optimization

### Caching
```php
// Cache expensive queries
$cache_key = 'reign_dokan_featured_vendors';
$vendors = get_transient($cache_key);

if (false === $vendors) {
    $vendors = dokan_get_sellers(array('featured' => 'yes'));
    set_transient($cache_key, $vendors, HOUR_IN_SECONDS);
}
```

### Lazy Loading
```php
// Load resources only when needed
if (is_dokan_store_page()) {
    wp_enqueue_script('reign-dokan-store');
}
```

## Debugging

### Enable Debug Mode
```php
// In wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

### Debug Helpers
```php
// Log to debug file
error_log('Reign Dokan: ' . print_r($data, true));

// Conditional debugging
if (defined('WP_DEBUG') && WP_DEBUG) {
    var_dump($vendor_data);
}
```

---

## 💼 Popular Development Tasks (Copy & Use)

### 🎴 Add Custom Tab to Vendor Stores
**Example: Add "Certifications" tab to stores**
```php
// Add to functions.php or custom plugin
add_filter('dokan_store_tabs', function($tabs) {
    $tabs['certifications'] = array(
        'title' => __('Certifications', 'reign-dokan'),
        'url' => dokan_get_store_url() . 'certifications'
    );
    return $tabs;
});
```
**Result:** New tab appears on all vendor store pages

### 🔍 Customize Store Directory Query
**Example: Show newest vendors first**
```php
add_action('pre_get_posts', function($query) {
    if (is_dokan_store_listing()) {
        $query->set('orderby', 'registered');
        $query->set('order', 'DESC');  // Newest first
        $query->set('posts_per_page', 20); // Show 20 per page
    }
});
```
**Use Case:** Perfect for "New Vendors" sections

### ➕ Add Custom Fields to Vendor Profiles
**Example: Add social media links**
```php
// Save custom field when vendor updates profile
add_action('dokan_store_profile_saved', function($store_id, $settings) {
    update_user_meta($store_id, 'vendor_instagram', $settings['instagram']);
    update_user_meta($store_id, 'vendor_facebook', $settings['facebook']);
}, 10, 2);

// Display in store header
add_action('dokan_store_header_info_fields', function($store_id) {
    $instagram = get_user_meta($store_id, 'vendor_instagram', true);
    if ($instagram) {
        echo '<a href="' . esc_url($instagram) . '">Instagram</a>';
    }
});
```
**Result:** Vendors can add social links to their stores

## License Management

### File: `/edd-license/`
- Uses EDD Software Licensing
- License key: `wbcom_reign_dokan_addon_license_key`
- Status: `wbcom_reign_dokan_addon_license_status`

## Resources

- **Plugin Files**: `/wp-content/plugins/reign-dokan-addon/`
- **Templates**: `/dokan/` directory
- **Hooks Reference**: This guide
- **Support**: WBcom Designs

---

*Developer guide verified against Reign Dokan Addon v3.5.4 source code*