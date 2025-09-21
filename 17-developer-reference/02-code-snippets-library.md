# Reign Theme Code Snippets Library

## Overview

This comprehensive library contains ready-to-use code snippets for customizing and extending Reign Theme. All snippets should be added to your child theme's `functions.php` file or a custom plugin.

## Header Customizations

### Change Logo Programmatically

```php
// Change logo based on page
add_filter('reign_site_logo', function($logo_url) {
    if (is_page('special-page')) {
        return get_stylesheet_directory_uri() . '/images/special-logo.png';
    }
    return $logo_url;
});
```

### Add Custom Header Content

```php
// Add content after header
add_action('reign_after_header', function() {
    if (is_front_page()) {
        echo '<div class="custom-banner">Welcome to our community!</div>';
    }
});
```

### Sticky Header on Scroll

```php
// Enable sticky header programmatically
add_filter('reign_sticky_header_enabled', '__return_true');

// Customize sticky header offset
add_filter('reign_sticky_header_offset', function() {
    return 100; // pixels from top
});
```

### Custom Menu Walker

```php
// Add icons to menu items
class Reign_Icon_Menu_Walker extends Walker_Nav_Menu {
    function start_el(&$output, $item, $depth = 0, $args = null, $id = 0) {
        $icon = get_post_meta($item->ID, '_menu_item_icon', true);
        if ($icon) {
            $item->title = '<i class="' . $icon . '"></i> ' . $item->title;
        }
        parent::start_el($output, $item, $depth, $args, $id);
    }
}

// Use custom walker
add_filter('wp_nav_menu_args', function($args) {
    if ($args['theme_location'] == 'primary') {
        $args['walker'] = new Reign_Icon_Menu_Walker();
    }
    return $args;
});
```

## Footer Customizations

### Dynamic Copyright Year

```php
// Auto-update copyright year
add_filter('reign_footer_copyright_text', function($text) {
    $year = date('Y');
    return str_replace('[year]', $year, $text);
});
```

### Add Widget Area to Footer

```php
// Register new footer widget area
add_action('widgets_init', function() {
    register_sidebar(array(
        'name' => 'Footer Widget Area 5',
        'id' => 'footer-widget-area-5',
        'before_widget' => '<div class="widget %2$s">',
        'after_widget' => '</div>',
    ));
});

// Display the widget area
add_action('reign_footer_widgets', function() {
    if (is_active_sidebar('footer-widget-area-5')) {
        dynamic_sidebar('footer-widget-area-5');
    }
});
```

## BuddyPress Customizations

### Redirect After Login

```php
// Redirect to activity page after login
add_filter('login_redirect', function($redirect_to, $request, $user) {
    if (isset($user->roles) && is_array($user->roles)) {
        if (in_array('subscriber', $user->roles)) {
            return bp_get_activity_directory_permalink();
        }
    }
    return $redirect_to;
}, 10, 3);
```

### Custom Activity Types

```php
// Register custom activity type
add_action('bp_register_activity_actions', function() {
    bp_activity_set_action(
        'custom_component',
        'custom_action',
        __('Custom Activity', 'reign'),
        'custom_activity_format',
        __('Custom Activities', 'reign'),
        array('activity', 'member')
    );
});

// Format custom activity
function custom_activity_format($action, $activity) {
    return sprintf('%s performed a custom action', bp_core_get_userlink($activity->user_id));
}
```

### Modify Members Loop

```php
// Change members per page
add_filter('bp_after_has_members_parse_args', function($args) {
    $args['per_page'] = 20;
    $args['type'] = 'newest';
    return $args;
});
```

### Add Custom Profile Tab

```php
// Add new profile tab
add_action('bp_setup_nav', function() {
    global $bp;

    bp_core_new_nav_item(array(
        'name' => 'Custom Tab',
        'slug' => 'custom-tab',
        'screen_function' => 'reign_custom_tab_screen',
        'position' => 50,
        'parent_url' => bp_loggedin_user_domain() . '/custom-tab/',
        'parent_slug' => $bp->profile->slug,
        'default_subnav_slug' => 'custom-sub'
    ));
});

function reign_custom_tab_screen() {
    add_action('bp_template_content', 'reign_custom_tab_content');
    bp_core_load_template('members/single/plugins');
}

function reign_custom_tab_content() {
    echo '<h2>Custom Tab Content</h2>';
    // Add your content here
}
```

### Custom Group Meta

```php
// Add custom field to groups
add_action('bp_after_group_details_admin', function() {
    $group_id = bp_get_group_id();
    $custom_field = groups_get_groupmeta($group_id, 'custom_field');
    ?>
    <label>Custom Field</label>
    <input type="text" name="custom_field" value="<?php echo esc_attr($custom_field); ?>">
    <?php
});

// Save custom field
add_action('groups_group_details_edited', function($group_id) {
    if (isset($_POST['custom_field'])) {
        groups_update_groupmeta($group_id, 'custom_field', sanitize_text_field($_POST['custom_field']));
    }
});
```

## WooCommerce Customizations

### Products Per Page

```php
// Change products per page
add_filter('loop_shop_per_page', function() {
    return 24;
});
```

### Custom Product Badge

```php
// Add "New" badge to recent products
add_action('woocommerce_before_shop_loop_item_title', function() {
    global $product;
    $created = strtotime($product->get_date_created());
    $days_old = (time() - $created) / DAY_IN_SECONDS;

    if ($days_old < 30) {
        echo '<span class="new-badge">New!</span>';
    }
});
```

### Catalog Mode

```php
// Remove add to cart buttons
add_filter('woocommerce_is_purchasable', '__return_false');

// Hide prices
remove_action('woocommerce_single_product_summary', 'woocommerce_template_single_price', 10);
remove_action('woocommerce_after_shop_loop_item_title', 'woocommerce_template_loop_price', 10);
```

### Custom Checkout Fields

```php
// Add custom checkout field
add_filter('woocommerce_checkout_fields', function($fields) {
    $fields['billing']['billing_custom'] = array(
        'type' => 'text',
        'label' => 'Custom Field',
        'required' => false,
        'class' => array('form-row-wide'),
        'priority' => 25
    );
    return $fields;
});

// Save custom field
add_action('woocommerce_checkout_update_order_meta', function($order_id) {
    if (!empty($_POST['billing_custom'])) {
        update_post_meta($order_id, 'billing_custom', sanitize_text_field($_POST['billing_custom']));
    }
});
```

## Login & Registration

### Custom Registration Fields

```php
// Add field to registration form
add_action('bp_signup_profile_fields', function() {
    ?>
    <div class="register-field">
        <label>Referral Code</label>
        <input type="text" name="referral_code" id="referral_code">
    </div>
    <?php
});

// Validate and save field
add_filter('bp_signup_validate', function() {
    if (isset($_POST['referral_code'])) {
        $code = sanitize_text_field($_POST['referral_code']);
        // Add validation logic
        if (strlen($code) < 5) {
            buddypress()->signup->errors['referral_code'] = 'Invalid referral code';
        }
    }
});
```

### Auto Login After Registration

```php
// Auto login user after registration
add_action('user_register', function($user_id) {
    wp_set_current_user($user_id);
    wp_set_auth_cookie($user_id);

    // Redirect to welcome page
    wp_redirect(home_url('/welcome'));
    exit;
});
```

### Social Login Integration

```php
// Handle social login data
add_action('social_login_user_created', function($user_id, $social_data) {
    // Save social profile URL
    update_user_meta($user_id, 'facebook_profile', $social_data['link']);

    // Add to specific group
    if (function_exists('groups_join_group')) {
        groups_join_group(1, $user_id); // Group ID 1
    }
}, 10, 2);
```

## Performance Optimizations

### Lazy Load Scripts

```php
// Defer non-critical scripts
add_filter('script_loader_tag', function($tag, $handle) {
    $defer_scripts = array('non-critical-1', 'non-critical-2');

    if (in_array($handle, $defer_scripts)) {
        return str_replace(' src', ' defer src', $tag);
    }
    return $tag;
}, 10, 2);
```

### Disable Emojis

```php
// Remove emoji support
add_action('init', function() {
    remove_action('wp_head', 'print_emoji_detection_script', 7);
    remove_action('admin_print_scripts', 'print_emoji_detection_script');
    remove_action('wp_print_styles', 'print_emoji_styles');
    remove_action('admin_print_styles', 'print_emoji_styles');
    remove_filter('the_content_feed', 'wp_staticize_emoji');
    remove_filter('comment_text_rss', 'wp_staticize_emoji');
    remove_filter('wp_mail', 'wp_staticize_emoji_for_email');
});
```

### Optimize Database Queries

```php
// Cache expensive queries
function get_popular_posts_cached() {
    $cache_key = 'reign_popular_posts';
    $posts = get_transient($cache_key);

    if (false === $posts) {
        $posts = get_posts(array(
            'meta_key' => 'post_views',
            'orderby' => 'meta_value_num',
            'posts_per_page' => 10
        ));
        set_transient($cache_key, $posts, HOUR_IN_SECONDS);
    }

    return $posts;
}
```

## Styling & Design

### Add Body Classes

```php
// Add custom body classes
add_filter('body_class', function($classes) {
    if (is_user_logged_in()) {
        $classes[] = 'logged-in-user';
        $classes[] = 'role-' . wp_get_current_user()->roles[0];
    }

    if (bp_is_activity_component()) {
        $classes[] = 'bp-activity-page';
    }

    return $classes;
});
```

### Custom CSS Based on User Role

```php
// Add role-specific styles
add_action('wp_head', function() {
    if (current_user_can('administrator')) {
        ?>
        <style>
            .admin-only { display: block !important; }
            body { border-top: 3px solid red; }
        </style>
        <?php
    }
});
```

### Dynamic Theme Colors

```php
// Change colors based on time of day
add_action('wp_head', function() {
    $hour = date('G');
    $color = ($hour >= 6 && $hour <= 18) ? '#3498db' : '#2c3e50';
    ?>
    <style>
        :root {
            --reign-primary-color: <?php echo $color; ?>;
        }
    </style>
    <?php
});
```

## Content Management

### Custom Excerpt Length

```php
// Change excerpt length
add_filter('excerpt_length', function() {
    return is_front_page() ? 20 : 55;
});

// Custom excerpt more text
add_filter('excerpt_more', function() {
    return '... <a href="' . get_permalink() . '">Continue reading</a>';
});
```

### Post Views Counter

```php
// Track post views
add_action('wp_head', function() {
    if (is_single()) {
        $post_id = get_the_ID();
        $views = get_post_meta($post_id, 'post_views', true);
        $views = $views ? $views + 1 : 1;
        update_post_meta($post_id, 'post_views', $views);
    }
});

// Display post views
function reign_get_post_views($post_id) {
    $views = get_post_meta($post_id, 'post_views', true);
    return $views ? $views : 0;
}
```

### Related Posts

```php
// Get related posts by category
function reign_get_related_posts($post_id, $limit = 3) {
    $categories = wp_get_post_categories($post_id);

    $args = array(
        'category__in' => $categories,
        'post__not_in' => array($post_id),
        'posts_per_page' => $limit,
        'orderby' => 'rand'
    );

    return new WP_Query($args);
}
```

## User Management

### Custom User Roles

```php
// Add custom role
add_action('init', function() {
    add_role('premium_member', 'Premium Member', array(
        'read' => true,
        'edit_posts' => true,
        'upload_files' => true,
        'premium_content' => true
    ));
});
```

### User Online Status

```php
// Update user online status
add_action('init', function() {
    if (is_user_logged_in()) {
        update_user_meta(get_current_user_id(), 'last_online', current_time('timestamp'));
    }
});

// Check if user is online
function is_user_online($user_id) {
    $last_online = get_user_meta($user_id, 'last_online', true);
    $timeout = 15 * MINUTE_IN_SECONDS;
    return ($last_online && (current_time('timestamp') - $last_online) < $timeout);
}
```

### Welcome Email

```php
// Custom welcome email
add_filter('wp_new_user_notification_email', function($email, $user, $blogname) {
    $email['subject'] = sprintf('Welcome to %s!', $blogname);
    $email['message'] = sprintf(
        'Hi %s,\n\nWelcome to our community!\n\nYour username: %s\n\nGet started: %s\n\nBest regards,\nThe Team',
        $user->display_name,
        $user->user_login,
        home_url('/getting-started/')
    );
    return $email;
}, 10, 3);
```

## Navigation & Menus

### Breadcrumbs

```php
// Generate breadcrumbs
function reign_breadcrumbs() {
    $sep = ' > ';
    $home = 'Home';

    echo '<div class="breadcrumbs">';
    echo '<a href="' . home_url() . '">' . $home . '</a>' . $sep;

    if (is_category() || is_single()) {
        the_category(', ');
        if (is_single()) {
            echo $sep;
            the_title();
        }
    } elseif (is_page()) {
        echo the_title();
    }
    echo '</div>';
}
```

### Conditional Menu Items

```php
// Show/hide menu items based on login status
add_filter('wp_nav_menu_items', function($items, $args) {
    if ($args->theme_location == 'primary') {
        if (is_user_logged_in()) {
            $items = str_replace('Login', 'Logout', $items);
            $items = str_replace('#login', wp_logout_url(), $items);
        } else {
            // Remove member-only items
            $items = preg_replace('/<li[^>]*class="[^"]*member-only[^"]*"[^>]*>.*?<\/li>/s', '', $items);
        }
    }
    return $items;
}, 10, 2);
```

## Widgets & Sidebars

### Conditional Sidebar

```php
// Show different sidebar based on user role
add_filter('reign_sidebar_id', function($sidebar) {
    if (current_user_can('premium_member')) {
        return 'premium-sidebar';
    }
    return $sidebar;
});
```

### Custom Widget

```php
// Create custom widget
class Reign_Custom_Widget extends WP_Widget {
    function __construct() {
        parent::__construct(
            'reign_custom_widget',
            'Reign Custom Widget',
            array('description' => 'A custom widget for Reign theme')
        );
    }

    public function widget($args, $instance) {
        echo $args['before_widget'];
        echo '<h3>Custom Widget Content</h3>';
        // Widget content here
        echo $args['after_widget'];
    }
}

// Register widget
add_action('widgets_init', function() {
    register_widget('Reign_Custom_Widget');
});
```

## Security Enhancements

### Content Protection

```php
// Protect content for members only
add_filter('the_content', function($content) {
    if (is_single() && in_category('premium')) {
        if (!is_user_logged_in()) {
            return '<p>This content is for members only. <a href="/login">Please login</a>.</p>';
        }
    }
    return $content;
});
```

### Disable REST API for Non-Logged Users

```php
// Restrict REST API
add_filter('rest_authentication_errors', function($result) {
    if (!is_user_logged_in()) {
        return new WP_Error('rest_not_logged_in', 'You must be logged in to use the REST API.', array('status' => 401));
    }
    return $result;
});
```

## Email Customizations

### Custom Email Templates

```php
// Customize BuddyPress emails
add_filter('bp_email_get_content_html', function($content, $email_type) {
    if ($email_type == 'activity-comment') {
        // Add custom header
        $header = '<div style="background:#3498db;color:white;padding:20px;">
                   <h1>New Comment on Your Activity</h1>
                   </div>';
        $content = $header . $content;
    }
    return $content;
}, 10, 2);
```

## Admin Customizations

### Custom Admin Columns

```php
// Add custom column to users list
add_filter('manage_users_columns', function($columns) {
    $columns['last_login'] = 'Last Login';
    return $columns;
});

add_filter('manage_users_custom_column', function($value, $column_name, $user_id) {
    if ($column_name == 'last_login') {
        $last_login = get_user_meta($user_id, 'last_login', true);
        return $last_login ? date('Y-m-d H:i', $last_login) : 'Never';
    }
    return $value;
}, 10, 3);
```

### Admin Notices

```php
// Show admin notice for configuration
add_action('admin_notices', function() {
    if (!get_option('reign_configured')) {
        ?>
        <div class="notice notice-warning is-dismissible">
            <p>Please complete <a href="/wp-admin/admin.php?page=reign-settings">Reign Theme setup</a>.</p>
        </div>
        <?php
    }
});
```

## Utility Functions

### Debug Helper

```php
// Better debug output
function reign_debug($data, $die = false) {
    echo '<pre style="background:#f5f5f5;padding:10px;border:1px solid #ddd;">';
    print_r($data);
    echo '</pre>';
    if ($die) die();
}
```

### Check Plugin Active

```php
// Check if specific plugin is active
function reign_is_plugin_active($plugin) {
    $active_plugins = array(
        'buddypress' => 'buddypress/bp-loader.php',
        'woocommerce' => 'woocommerce/woocommerce.php',
        'bbpress' => 'bbpress/bbpress.php',
        'elementor' => 'elementor/elementor.php'
    );

    if (isset($active_plugins[$plugin])) {
        return is_plugin_active($active_plugins[$plugin]);
    }
    return false;
}
```

### Format Number

```php
// Format large numbers (1.2K, 3.5M)
function reign_format_number($number) {
    if ($number >= 1000000) {
        return round($number / 1000000, 1) . 'M';
    } elseif ($number >= 1000) {
        return round($number / 1000, 1) . 'K';
    }
    return $number;
}
```

---

*Remember: Always test code snippets on a staging site first. Use a child theme or custom plugin for modifications.*