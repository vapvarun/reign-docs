# Child Theme Development Guide

## Overview

A child theme allows you to modify Reign theme without losing changes during updates. This guide covers creating, customizing, and maintaining a Reign child theme.

## Creating a Child Theme

### Basic Structure

**Minimum Required Files:**
```
reign-child/
├── style.css (required)
├── functions.php (required)
├── screenshot.png (optional)
└── Additional files as needed
```

### Step 1: Create style.css

```css
/*
Theme Name: Reign Child Theme
Theme URI: https://your-site.com
Description: Child theme for Reign Theme
Author: Your Name
Author URI: https://your-site.com
Template: reign-theme
Version: 1.0.0
License: GPL v3
Text Domain: reign-child
*/

/* =Child Theme Custom Styles
-------------------------------------------------------------- */

/* Your custom CSS goes below this line */
```

### Step 2: Create functions.php

```php
<?php
/**
 * Reign Child Theme Functions
 *
 * @package Reign_Child
 */

// Exit if accessed directly
if (!defined('ABSPATH')) {
    exit;
}

/**
 * Enqueue parent and child theme styles
 */
function reign_child_enqueue_styles() {

    // Parent theme styles
    wp_enqueue_style(
        'reign-parent-style',
        get_template_directory_uri() . '/style.css',
        array(),
        wp_get_theme()->parent()->get('Version')
    );

    // Child theme styles
    wp_enqueue_style(
        'reign-child-style',
        get_stylesheet_directory_uri() . '/style.css',
        array('reign-parent-style'),
        wp_get_theme()->get('Version')
    );

    // Child theme scripts
    wp_enqueue_script(
        'reign-child-scripts',
        get_stylesheet_directory_uri() . '/assets/js/custom.js',
        array('jquery'),
        '1.0.0',
        true
    );
}
add_action('wp_enqueue_scripts', 'reign_child_enqueue_styles');

/* Add your custom functions below this line */
```

### Step 3: Create screenshot.png

**Specifications:**
- Size: 1200x900px
- Format: PNG
- Content: Preview of your child theme

## Installing the Child Theme

### Method 1: Upload via WordPress

1. Zip the child theme folder
2. Go to Appearance → Themes → Add New
3. Upload Theme → Choose File
4. Select reign-child.zip
5. Install and Activate

### Method 2: FTP Upload

1. Connect via FTP
2. Navigate to `/wp-content/themes/`
3. Upload reign-child folder
4. Go to Appearance → Themes
5. Activate Reign Child Theme

### Method 3: Download from Reign

1. Login to WBcom Designs account
2. Download Reign child theme
3. Install as above

## Template Overrides

### How Template Override Works

**WordPress Template Hierarchy:**
```
1. Child Theme checks first
2. Parent Theme checks second
3. WordPress default fallback
```

### Overriding Templates

**Example: Override header.php**

1. Copy from parent: `reign-theme/header.php`
2. Paste to child: `reign-child/header.php`
3. Modify as needed

**Common Templates to Override:**
```
reign-child/
├── header.php
├── footer.php
├── single.php
├── page.php
├── archive.php
├── sidebar.php
└── template-parts/
    ├── header/
    │   └── header-v2.php
    └── content/
        └── content-single.php
```

### BuddyPress Template Overrides

**BuddyPress Templates:**
```
reign-child/
├── buddypress/
│   ├── members/
│   │   ├── single/
│   │   └── index.php
│   ├── groups/
│   │   └── single/
│   └── activity/
│       └── index.php
```

### WooCommerce Template Overrides

**WooCommerce Templates:**
```
reign-child/
├── woocommerce/
│   ├── single-product.php
│   ├── archive-product.php
│   ├── cart/
│   │   └── cart.php
│   └── checkout/
│       └── form-checkout.php
```

## Custom Functions

### Adding New Features

```php
/**
 * Add custom functionality to Reign
 */

// Add custom post type
function reign_child_custom_post_type() {
    register_post_type('portfolio',
        array(
            'labels' => array(
                'name' => __('Portfolio', 'reign-child'),
                'singular_name' => __('Portfolio Item', 'reign-child')
            ),
            'public' => true,
            'has_archive' => true,
            'supports' => array('title', 'editor', 'thumbnail'),
            'rewrite' => array('slug' => 'portfolio'),
        )
    );
}
add_action('init', 'reign_child_custom_post_type');

// Add custom image sizes
function reign_child_image_sizes() {
    add_image_size('reign-child-hero', 1920, 600, true);
    add_image_size('reign-child-square', 600, 600, true);
}
add_action('after_setup_theme', 'reign_child_image_sizes');

// Register widget areas
function reign_child_widgets_init() {
    register_sidebar(array(
        'name' => __('Child Theme Sidebar', 'reign-child'),
        'id' => 'child-sidebar',
        'description' => __('Custom sidebar for child theme', 'reign-child'),
        'before_widget' => '<div id="%1$s" class="widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>',
    ));
}
add_action('widgets_init', 'reign_child_widgets_init');
```

### Modifying Parent Functions

```php
/**
 * Remove parent theme function and replace
 */

// Remove parent function
function reign_child_remove_parent_function() {
    remove_action('reign_header', 'reign_header_function', 10);
}
add_action('init', 'reign_child_remove_parent_function');

// Add child function
function reign_child_header_function() {
    // Your custom header code
    ?>
    <header class="custom-header">
        <!-- Custom header content -->
    </header>
    <?php
}
add_action('reign_header', 'reign_child_header_function', 10);
```

## Hooks and Filters

### Using Parent Theme Hooks

```php
/**
 * Hook into Reign theme actions
 */

// Before header
add_action('reign_before_header', function() {
    echo '<div class="announcement-bar">Welcome to our site!</div>';
});

// After content
add_action('reign_after_content', function() {
    if (is_single()) {
        echo '<div class="related-posts">' . get_related_posts() . '</div>';
    }
});

// In footer
add_action('reign_footer', function() {
    echo '<div class="custom-footer-widget">Custom content</div>';
}, 20);
```

### Using Parent Theme Filters

```php
/**
 * Filter Reign theme output
 */

// Modify excerpt length
add_filter('excerpt_length', function($length) {
    return 30; // 30 words
});

// Change login redirect
add_filter('reign_login_redirect', function($redirect_url, $user) {
    if (in_array('subscriber', $user->roles)) {
        return home_url('/member-dashboard');
    }
    return $redirect_url;
}, 10, 2);

// Modify header classes
add_filter('reign_header_class', function($classes) {
    $classes[] = 'custom-header-class';
    if (is_front_page()) {
        $classes[] = 'home-header';
    }
    return $classes;
});
```

## Custom Styling

### CSS Best Practices

```css
/* Use specific selectors to override parent */
.reign-theme .site-header {
    background: #custom-color;
}

/* Use CSS variables for consistency */
:root {
    --child-primary: #0073aa;
    --child-secondary: #23282d;
    --child-accent: #00a0d2;
}

/* Responsive design */
@media (max-width: 768px) {
    .reign-theme .custom-element {
        display: none;
    }
}

/* Dark mode support */
[data-theme="dark"] .custom-element {
    background: #1a1a1a;
    color: #ffffff;
}
```

### SASS/SCSS Structure

```scss
// Directory structure
reign-child/
├── assets/
│   ├── scss/
│   │   ├── abstracts/
│   │   │   ├── _variables.scss
│   │   │   └── _mixins.scss
│   │   ├── components/
│   │   │   ├── _buttons.scss
│   │   │   └── _cards.scss
│   │   ├── layouts/
│   │   │   ├── _header.scss
│   │   │   └── _footer.scss
│   │   └── main.scss
│   └── css/
│       └── main.css (compiled)
```

## JavaScript Customization

### Adding Custom Scripts

```javascript
// assets/js/custom.js
(function($) {
    'use strict';

    $(document).ready(function() {

        // Custom navigation
        $('.custom-nav-toggle').on('click', function() {
            $('.custom-nav').toggleClass('active');
        });

        // Smooth scrolling
        $('a[href*="#"]').on('click', function(e) {
            e.preventDefault();
            $('html, body').animate({
                scrollTop: $($(this).attr('href')).offset().top
            }, 500);
        });

        // Ajax load more
        $('#load-more').on('click', function() {
            var button = $(this);
            var page = button.data('page');

            $.ajax({
                url: reign_child_ajax.ajax_url,
                type: 'post',
                data: {
                    action: 'load_more_posts',
                    page: page,
                    nonce: reign_child_ajax.nonce
                },
                success: function(response) {
                    $('#posts-container').append(response);
                    button.data('page', page + 1);
                }
            });
        });
    });

})(jQuery);
```

### Localizing Scripts

```php
function reign_child_localize_scripts() {
    wp_localize_script('reign-child-scripts', 'reign_child_ajax', array(
        'ajax_url' => admin_url('admin-ajax.php'),
        'nonce' => wp_create_nonce('reign_child_nonce'),
        'i18n' => array(
            'loading' => __('Loading...', 'reign-child'),
            'load_more' => __('Load More', 'reign-child'),
        )
    ));
}
add_action('wp_enqueue_scripts', 'reign_child_localize_scripts');
```

## Custom Page Templates

### Creating Page Templates

```php
<?php
/**
 * Template Name: Custom Full Width
 * Template Post Type: page, post
 *
 * @package Reign_Child
 */

get_header();
?>

<div class="custom-full-width-template">
    <div class="container-fluid">
        <?php
        while (have_posts()) :
            the_post();
            ?>
            <article id="post-<?php the_ID(); ?>" <?php post_class(); ?>>
                <?php the_content(); ?>
            </article>
            <?php
        endwhile;
        ?>
    </div>
</div>

<?php
get_footer();
```

## Version Control

### Git Setup

**.gitignore for Child Theme:**
```
# Dependencies
node_modules/
vendor/

# Build files
*.map
*.min.css
*.min.js

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db

# WordPress
wp-config.php
```

### Deployment

```bash
# Build for production
npm run build

# Create release
git tag -a v1.0.0 -m "Release version 1.0.0"
git push origin v1.0.0
```

## Maintenance

### Updating Child Theme

```php
/**
 * Auto-update notification
 */
function reign_child_update_check() {
    $version = get_option('reign_child_version');
    $current = wp_get_theme()->get('Version');

    if (version_compare($current, $version, '>')) {
        // Run update procedures
        reign_child_run_updates();
        update_option('reign_child_version', $current);
    }
}
add_action('init', 'reign_child_update_check');
```

### Debug Mode

```php
// Enable debug in child theme
if (WP_DEBUG) {
    error_log('Reign Child: Debug message');

    add_action('wp_footer', function() {
        echo '<!-- Debug: Template = ' . get_page_template() . ' -->';
    });
}
```

## Best Practices

1. **Minimal Overrides** - Only override what's necessary
2. **Documentation** - Comment your code
3. **Performance** - Optimize assets
4. **Compatibility** - Test with parent theme updates
5. **Backup** - Version control everything
6. **Security** - Sanitize and escape data
7. **Responsive** - Mobile-first approach
8. **Accessibility** - Follow WCAG guidelines