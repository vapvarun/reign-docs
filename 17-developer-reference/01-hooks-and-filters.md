# Reign Theme Hooks and Filters Reference

## Overview

Reign theme provides extensive hooks and filters for developers to customize functionality without modifying core files. This reference covers all available hooks, their usage, and practical examples.

## Action Hooks

### Header Hooks

#### reign_before_header
**Location:** Before the header element
**Usage:**
```php
add_action('reign_before_header', function() {
    echo '<div class="top-banner">Special Announcement</div>';
});
```

#### reign_header
**Location:** Main header output
**Priority:** Default 10
```php
add_action('reign_header', function() {
    get_template_part('template-parts/header/custom-header');
}, 15);
```

#### reign_after_header
**Location:** After header element
```php
add_action('reign_after_header', function() {
    if (is_front_page()) {
        get_template_part('template-parts/hero-slider');
    }
});
```

#### reign_before_masthead
**Location:** Before masthead wrapper
```php
add_action('reign_before_masthead', function() {
    echo '<div class="progress-bar"></div>';
});
```

#### reign_masthead_top
**Location:** Top of masthead content
```php
add_action('reign_masthead_top', function() {
    if (function_exists('yoast_breadcrumb')) {
        yoast_breadcrumb('<p id="breadcrumbs">', '</p>');
    }
});
```

### Content Hooks

#### reign_before_content
**Location:** Before main content area
```php
add_action('reign_before_content', function() {
    if (is_single()) {
        echo '<div class="reading-time">' . get_reading_time() . '</div>';
    }
});
```

#### reign_before_post
**Location:** Before individual post
```php
add_action('reign_before_post', function() {
    global $post;
    echo '<div class="post-meta-top">';
    echo 'Views: ' . get_post_meta($post->ID, 'views', true);
    echo '</div>';
});
```

#### reign_after_post_content
**Location:** After post content
```php
add_action('reign_after_post_content', function() {
    if (is_single()) {
        // Author box
        get_template_part('template-parts/author-box');
        // Related posts
        get_template_part('template-parts/related-posts');
    }
});
```

#### reign_after_content
**Location:** After main content area
```php
add_action('reign_after_content', function() {
    if (is_page('contact')) {
        echo do_shortcode('[contact_map]');
    }
});
```

### Sidebar Hooks

#### reign_before_sidebar
**Location:** Before sidebar element
```php
add_action('reign_before_sidebar', function() {
    if (is_user_logged_in()) {
        echo '<div class="user-welcome">Welcome back!</div>';
    }
});
```

#### reign_sidebar
**Location:** Main sidebar output
```php
add_action('reign_sidebar', function() {
    if (is_category('news')) {
        dynamic_sidebar('news-sidebar');
    } else {
        dynamic_sidebar('sidebar-1');
    }
});
```

#### reign_after_sidebar
**Location:** After sidebar element
```php
add_action('reign_after_sidebar', function() {
    echo '<div class="sidebar-ad">Advertisement</div>';
});
```

### Footer Hooks

#### reign_before_footer
**Location:** Before footer element
```php
add_action('reign_before_footer', function() {
    get_template_part('template-parts/newsletter-signup');
});
```

#### reign_footer
**Location:** Main footer output
```php
add_action('reign_footer', function() {
    ?>
    <div class="custom-footer-content">
        <div class="footer-column">
            <?php dynamic_sidebar('footer-custom'); ?>
        </div>
    </div>
    <?php
}, 5);
```

#### reign_after_footer
**Location:** After footer element
```php
add_action('reign_after_footer', function() {
    echo '<div class="copyright-extended">Additional legal text</div>';
});
```

### BuddyPress Hooks

#### reign_bp_before_member_header
**Location:** Before member header
```php
add_action('reign_bp_before_member_header', function() {
    $user_id = bp_displayed_user_id();
    $verified = get_user_meta($user_id, 'verified', true);
    if ($verified) {
        echo '<span class="verified-badge">✓ Verified</span>';
    }
});
```

#### reign_bp_after_member_header
**Location:** After member header
```php
add_action('reign_bp_after_member_header', function() {
    echo '<div class="member-stats">';
    echo 'Member since: ' . bp_get_member_registered();
    echo '</div>';
});
```

#### reign_bp_before_activity_entry
**Location:** Before activity item
```php
add_action('reign_bp_before_activity_entry', function() {
    $activity_id = bp_get_activity_id();
    if (is_featured_activity($activity_id)) {
        echo '<span class="featured">Featured</span>';
    }
});
```

### WooCommerce Hooks

#### reign_before_shop_loop
**Location:** Before product loop
```php
add_action('reign_before_shop_loop', function() {
    echo '<div class="shop-filters">';
    echo do_shortcode('[product_filter]');
    echo '</div>';
});
```

#### reign_after_shop_loop_item
**Location:** After product in loop
```php
add_action('reign_after_shop_loop_item', function() {
    global $product;
    echo '<div class="product-badges">';
    if ($product->is_on_sale()) {
        echo '<span class="sale-percentage">-' . get_sale_percentage($product) . '%</span>';
    }
    echo '</div>';
});
```

#### reign_before_single_product
**Location:** Before single product
```php
add_action('reign_before_single_product', function() {
    echo '<div class="product-navigation">';
    previous_post_link('%link', '← Previous Product');
    next_post_link('%link', 'Next Product →');
    echo '</div>';
});
```

## Filter Hooks

### Layout Filters

#### reign_sidebar_position
**Filter:** Sidebar position
**Default:** 'right'
```php
add_filter('reign_sidebar_position', function($position) {
    if (is_page('full-width')) {
        return 'none';
    }
    if (is_category()) {
        return 'left';
    }
    return $position;
});
```

#### reign_container_class
**Filter:** Container CSS class
**Default:** 'container'
```php
add_filter('reign_container_class', function($class) {
    if (is_page_template('template-wide.php')) {
        return 'container-fluid';
    }
    return $class;
});
```

#### reign_content_width
**Filter:** Content width
**Default:** 1170
```php
add_filter('reign_content_width', function($width) {
    if (is_page_template('template-narrow.php')) {
        return 960;
    }
    return $width;
});
```

### Header Filters

#### reign_header_class
**Filter:** Header CSS classes
```php
add_filter('reign_header_class', function($classes) {
    if (is_user_logged_in()) {
        $classes[] = 'logged-in-header';
    }
    if (is_front_page()) {
        $classes[] = 'transparent-header';
    }
    return $classes;
});
```

#### reign_logo_url
**Filter:** Logo link URL
**Default:** home_url('/')
```php
add_filter('reign_logo_url', function($url) {
    if (is_multisite()) {
        return network_home_url('/');
    }
    return $url;
});
```

#### reign_menu_args
**Filter:** Navigation menu arguments
```php
add_filter('reign_menu_args', function($args) {
    if (wp_is_mobile()) {
        $args['menu'] = 'mobile-menu';
    }
    $args['walker'] = new Custom_Nav_Walker();
    return $args;
});
```

### Content Filters

#### reign_excerpt_length
**Filter:** Excerpt word count
**Default:** 55
```php
add_filter('reign_excerpt_length', function($length) {
    if (is_home()) {
        return 30;
    }
    if (is_category()) {
        return 40;
    }
    return $length;
});
```

#### reign_excerpt_more
**Filter:** Excerpt more text
**Default:** '...'
```php
add_filter('reign_excerpt_more', function($more) {
    return '... <a href="' . get_permalink() . '">Continue Reading</a>';
});
```

#### reign_post_thumbnail_size
**Filter:** Post thumbnail size
**Default:** 'large'
```php
add_filter('reign_post_thumbnail_size', function($size) {
    if (is_home()) {
        return 'medium';
    }
    if (is_single()) {
        return 'full';
    }
    return $size;
});
```

### BuddyPress Filters

#### reign_bp_members_per_page
**Filter:** Members per page
**Default:** 20
```php
add_filter('reign_bp_members_per_page', function($count) {
    if (wp_is_mobile()) {
        return 10;
    }
    return 30;
});
```

#### reign_bp_activity_types
**Filter:** Allowed activity types
```php
add_filter('reign_bp_activity_types', function($types) {
    // Remove certain activity types
    unset($types['friendship_created']);
    unset($types['joined_group']);

    // Add custom type
    $types['custom_achievement'] = 'Achievements';

    return $types;
});
```

#### reign_bp_member_directory_layout
**Filter:** Member directory layout
**Default:** 'grid'
```php
add_filter('reign_bp_member_directory_layout', function($layout) {
    if (isset($_GET['view']) && $_GET['view'] === 'list') {
        return 'list';
    }
    return $layout;
});
```

### WooCommerce Filters

#### reign_woo_products_per_page
**Filter:** Products per page
**Default:** 12
```php
add_filter('reign_woo_products_per_page', function($count) {
    if (is_product_category('featured')) {
        return 8;
    }
    return 16;
});
```

#### reign_woo_product_columns
**Filter:** Product grid columns
**Default:** 4
```php
add_filter('reign_woo_product_columns', function($columns) {
    if (wp_is_mobile()) {
        return 2;
    }
    if (is_product_category()) {
        return 3;
    }
    return $columns;
});
```

## Custom Hook Implementation

### Creating Your Own Hooks

```php
/**
 * Add custom hooks to your child theme
 */

// Custom action hook
function my_custom_section() {
    do_action('reign_child_before_custom_section');

    echo '<div class="custom-section">';
    // Your content
    echo '</div>';

    do_action('reign_child_after_custom_section');
}

// Custom filter hook
function get_custom_data($data) {
    $filtered_data = apply_filters('reign_child_custom_data', $data);
    return $filtered_data;
}
```

### Hook Priority

```php
// Understanding priority
add_action('reign_header', 'first_function', 5);  // Runs first
add_action('reign_header', 'second_function', 10); // Runs second (default)
add_action('reign_header', 'third_function', 15);  // Runs third

// Removing hooked functions
remove_action('reign_header', 'original_function', 10);
add_action('reign_header', 'replacement_function', 10);
```

## Advanced Usage

### Conditional Hook Logic

```php
/**
 * Apply hooks conditionally
 */
add_action('init', function() {
    // Only on specific pages
    if (is_page('special')) {
        add_action('reign_before_content', 'special_page_content');
    }

    // Only for logged-in users
    if (is_user_logged_in()) {
        add_filter('reign_sidebar_position', function() {
            return 'left';
        });
    }

    // Only on mobile
    if (wp_is_mobile()) {
        add_action('reign_after_header', 'mobile_navigation');
    }
});
```

### Hook Debugging

```php
/**
 * Debug hooks for development
 */
if (WP_DEBUG) {
    // List all hooks
    add_action('all', function($tag) {
        if (strpos($tag, 'reign_') === 0) {
            error_log('Hook fired: ' . $tag);
        }
    });

    // Show hook locations
    add_action('reign_before_content', function() {
        echo '<!-- Hook: reign_before_content -->';
    });
}
```

### Performance Considerations

```php
/**
 * Optimize hook usage
 */

// Bad - Multiple database queries
add_action('reign_header', function() {
    $data1 = get_option('option1');
    $data2 = get_option('option2');
    $data3 = get_option('option3');
});

// Good - Single cached query
add_action('reign_header', function() {
    $data = wp_cache_get('header_data');
    if (false === $data) {
        $data = array(
            'option1' => get_option('option1'),
            'option2' => get_option('option2'),
            'option3' => get_option('option3'),
        );
        wp_cache_set('header_data', $data, '', 3600);
    }
});
```

## Best Practices

1. **Use Descriptive Names** - Clear function names
2. **Document Your Hooks** - Add PHPDoc comments
3. **Check Hook Existence** - Use `has_action()` and `has_filter()`
4. **Proper Priority** - Use appropriate priority values
5. **Avoid Conflicts** - Prefix your functions
6. **Performance** - Minimize database queries
7. **Error Handling** - Check for dependencies
8. **Testing** - Test with different scenarios