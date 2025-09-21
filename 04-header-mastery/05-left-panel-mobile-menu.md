# Left Panel & Mobile Menu Configuration

## Overview

Reign Theme features a sophisticated left panel navigation system and mobile menu that provides seamless navigation across all devices. The left panel can function as a primary navigation method on desktop or transform into a mobile menu on smaller screens.

## Left Panel Configuration

### Enabling Left Panel

**Location:** `Customizer → Header → Left Panel`

```
Enable Left Panel: ON
Panel Position: Left / Right
Panel Width: 280px
Trigger Type: Hamburger Icon / Text / Both
Panel Style: Overlay / Push / Slide
Background: Color / Image / Gradient
Close on ESC: Yes
Close on Outside Click: Yes
```

### Panel Layouts

#### Style 1: Overlay Panel
```css
.reign-left-panel-overlay {
    position: fixed;
    top: 0;
    left: -280px;
    width: 280px;
    height: 100%;
    background: #ffffff;
    z-index: 99999;
    transition: left 0.3s ease;
}

.reign-left-panel-overlay.active {
    left: 0;
}
```

#### Style 2: Push Panel
```css
.reign-left-panel-push {
    position: fixed;
    left: -280px;
    transition: left 0.3s ease;
}

.reign-left-panel-push.active {
    left: 0;
}

body.panel-open {
    margin-left: 280px;
    transition: margin 0.3s ease;
}
```

#### Style 3: Slide Panel
```css
.reign-left-panel-slide {
    transform: translateX(-100%);
    transition: transform 0.3s ease;
}

.reign-left-panel-slide.active {
    transform: translateX(0);
}
```

## Mobile Menu Settings

### Basic Configuration

**Location:** `Customizer → Header → Mobile Menu`

```
Mobile Breakpoint: 1024px
Menu Type: Slide / Dropdown / Accordion
Menu Position: Left / Right / Top / Bottom
Show Logo: Yes
Logo Position: Top / Inside Menu
Show Search: Yes
Show User Menu: Yes (if logged in)
```

### Mobile Menu Styles

#### Hamburger Icon Styles

```php
// Icon variations
$menu_icons = array(
    'hamburger' => '☰',
    'dots' => '⋮',
    'grid' => '⋯⋯',
    'custom' => 'Menu'
);
```

```css
/* Animated hamburger */
.mobile-menu-toggle {
    width: 30px;
    height: 24px;
    position: relative;
}

.mobile-menu-toggle span {
    position: absolute;
    height: 3px;
    width: 100%;
    background: #333;
    transition: all 0.3s;
}

.mobile-menu-toggle.active span:nth-child(1) {
    transform: rotate(45deg);
    top: 10px;
}

.mobile-menu-toggle.active span:nth-child(2) {
    opacity: 0;
}

.mobile-menu-toggle.active span:nth-child(3) {
    transform: rotate(-45deg);
    bottom: 10px;
}
```

## Panel Content Structure

### Menu Organization

```html
<!-- Left panel structure -->
<div class="reign-left-panel">
    <!-- Panel Header -->
    <div class="panel-header">
        <div class="panel-logo">
            <img src="logo.png" alt="Site Logo">
        </div>
        <button class="panel-close">×</button>
    </div>

    <!-- User Section (if logged in) -->
    <div class="panel-user-section">
        <div class="user-avatar">
            <?php echo get_avatar(get_current_user_id(), 60); ?>
        </div>
        <div class="user-info">
            <h4><?php echo wp_get_current_user()->display_name; ?></h4>
            <a href="<?php echo bp_loggedin_user_domain(); ?>">View Profile</a>
        </div>
    </div>

    <!-- Search -->
    <div class="panel-search">
        <form action="<?php echo home_url('/'); ?>" method="get">
            <input type="search" name="s" placeholder="Search...">
            <button type="submit"><i class="fa fa-search"></i></button>
        </form>
    </div>

    <!-- Navigation -->
    <nav class="panel-navigation">
        <?php wp_nav_menu(array(
            'theme_location' => 'left-panel-menu',
            'menu_class' => 'panel-menu',
            'container' => false,
            'walker' => new Reign_Panel_Menu_Walker()
        )); ?>
    </nav>

    <!-- Widgets Area -->
    <div class="panel-widgets">
        <?php dynamic_sidebar('left-panel-widgets'); ?>
    </div>

    <!-- Social Links -->
    <div class="panel-social">
        <?php reign_social_links(); ?>
    </div>

    <!-- Footer -->
    <div class="panel-footer">
        <p>&copy; <?php echo date('Y'); ?> <?php bloginfo('name'); ?></p>
    </div>
</div>
```

### Custom Menu Walker

```php
// Custom walker for panel menu
class Reign_Panel_Menu_Walker extends Walker_Nav_Menu {

    function start_lvl(&$output, $depth = 0, $args = null) {
        $output .= '<ul class="panel-submenu level-' . $depth . '">';
    }

    function start_el(&$output, $item, $depth = 0, $args = null, $id = 0) {
        $classes = empty($item->classes) ? array() : (array) $item->classes;
        $classes[] = 'panel-menu-item';

        if (in_array('menu-item-has-children', $classes)) {
            $classes[] = 'has-submenu';
        }

        $class_names = join(' ', apply_filters('nav_menu_css_class', array_filter($classes), $item, $args));

        $output .= '<li class="' . esc_attr($class_names) . '">';

        // Add icon if set
        $icon = get_post_meta($item->ID, '_menu_item_icon', true);
        if ($icon) {
            $output .= '<i class="' . $icon . '"></i> ';
        }

        $attributes = !empty($item->url) ? ' href="' . esc_attr($item->url) . '"' : '';

        $output .= '<a' . $attributes . '>';
        $output .= apply_filters('the_title', $item->title, $item->ID);

        // Add arrow for submenus
        if (in_array('menu-item-has-children', $classes)) {
            $output .= '<span class="submenu-toggle"><i class="fa fa-angle-down"></i></span>';
        }

        $output .= '</a>';
    }
}
```

## BuddyPress Integration

### Activity Feed in Panel

```php
// Add activity feed to left panel
add_action('reign_left_panel_content', function() {
    if (!function_exists('bp_is_active')) return;
    ?>
    <div class="panel-activities">
        <h3>Latest Activities</h3>
        <?php if (bp_has_activities('max=5&action=activity_update')): ?>
            <ul class="mini-activity-list">
                <?php while (bp_activities()): bp_the_activity(); ?>
                    <li>
                        <?php bp_activity_avatar('width=30&height=30'); ?>
                        <div class="activity-content">
                            <?php bp_activity_action(); ?>
                        </div>
                    </li>
                <?php endwhile; ?>
            </ul>
        <?php endif; ?>
    </div>
    <?php
});
```

### Member Quick Links

```php
// Add member shortcuts
add_action('reign_panel_user_menu', function() {
    if (!is_user_logged_in()) return;
    ?>
    <ul class="panel-user-menu">
        <li><a href="<?php echo bp_loggedin_user_domain(); ?>">
            <i class="fa fa-user"></i> My Profile
        </a></li>
        <li><a href="<?php echo bp_loggedin_user_domain() . 'activity/'; ?>">
            <i class="fa fa-stream"></i> My Activity
        </a></li>
        <li><a href="<?php echo bp_loggedin_user_domain() . 'friends/'; ?>">
            <i class="fa fa-users"></i> Friends
            <?php if ($count = friends_get_total_friend_count()): ?>
                <span class="count"><?php echo $count; ?></span>
            <?php endif; ?>
        </a></li>
        <li><a href="<?php echo bp_loggedin_user_domain() . 'messages/'; ?>">
            <i class="fa fa-envelope"></i> Messages
            <?php if ($count = messages_get_unread_count()): ?>
                <span class="count"><?php echo $count; ?></span>
            <?php endif; ?>
        </a></li>
        <li><a href="<?php echo bp_loggedin_user_domain() . 'groups/'; ?>">
            <i class="fa fa-users-cog"></i> My Groups
        </a></li>
        <li><a href="<?php echo wp_logout_url(); ?>">
            <i class="fa fa-sign-out-alt"></i> Logout
        </a></li>
    </ul>
    <?php
});
```

## WooCommerce Integration

### Cart in Panel

```php
// Add mini cart to panel
add_action('reign_left_panel_content', function() {
    if (!class_exists('WooCommerce')) return;
    ?>
    <div class="panel-cart">
        <h3>Shopping Cart (<?php echo WC()->cart->get_cart_contents_count(); ?>)</h3>
        <div class="widget_shopping_cart_content">
            <?php woocommerce_mini_cart(); ?>
        </div>
    </div>
    <?php
});
```

### Product Categories

```php
// Add product categories navigation
add_action('reign_panel_navigation', function() {
    if (!class_exists('WooCommerce')) return;

    $categories = get_terms('product_cat', array('hide_empty' => true));
    ?>
    <div class="panel-product-cats">
        <h3>Shop Categories</h3>
        <ul>
            <?php foreach($categories as $category): ?>
                <li>
                    <a href="<?php echo get_term_link($category); ?>">
                        <?php echo $category->name; ?>
                        <span>(<?php echo $category->count; ?>)</span>
                    </a>
                </li>
            <?php endforeach; ?>
        </ul>
    </div>
    <?php
});
```

## JavaScript Functionality

### Panel Control

```javascript
// Left panel controller
class LeftPanelController {
    constructor() {
        this.panel = document.querySelector('.reign-left-panel');
        this.trigger = document.querySelector('.panel-trigger');
        this.close = document.querySelector('.panel-close');
        this.overlay = document.querySelector('.panel-overlay');
        this.isOpen = false;

        this.init();
    }

    init() {
        // Open panel
        this.trigger?.addEventListener('click', (e) => {
            e.preventDefault();
            this.open();
        });

        // Close panel
        this.close?.addEventListener('click', () => this.close());
        this.overlay?.addEventListener('click', () => this.close());

        // ESC key close
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && this.isOpen) {
                this.close();
            }
        });

        // Submenu toggles
        this.initSubmenus();

        // Swipe gestures
        this.initSwipeGestures();
    }

    open() {
        this.panel.classList.add('active');
        document.body.classList.add('panel-open');
        this.overlay?.classList.add('active');
        this.isOpen = true;

        // Trigger event
        document.dispatchEvent(new CustomEvent('panelOpened'));
    }

    close() {
        this.panel.classList.remove('active');
        document.body.classList.remove('panel-open');
        this.overlay?.classList.remove('active');
        this.isOpen = false;

        // Trigger event
        document.dispatchEvent(new CustomEvent('panelClosed'));
    }

    initSubmenus() {
        const submenuToggles = document.querySelectorAll('.submenu-toggle');

        submenuToggles.forEach(toggle => {
            toggle.addEventListener('click', (e) => {
                e.preventDefault();
                e.stopPropagation();

                const parent = toggle.closest('.has-submenu');
                const submenu = parent.querySelector('.panel-submenu');

                parent.classList.toggle('open');

                // Slide animation
                if (parent.classList.contains('open')) {
                    submenu.style.maxHeight = submenu.scrollHeight + 'px';
                } else {
                    submenu.style.maxHeight = '0';
                }
            });
        });
    }

    initSwipeGestures() {
        let touchStartX = 0;
        let touchEndX = 0;

        this.panel.addEventListener('touchstart', (e) => {
            touchStartX = e.touches[0].clientX;
        });

        this.panel.addEventListener('touchend', (e) => {
            touchEndX = e.changedTouches[0].clientX;
            this.handleSwipe();
        });

        handleSwipe() {
            const swipeDistance = touchEndX - touchStartX;

            if (swipeDistance > 50 && this.isOpen) {
                // Swipe right to close (for left panel)
                this.close();
            }
        }
    }
}

// Initialize
document.addEventListener('DOMContentLoaded', () => {
    new LeftPanelController();
});
```

### Mobile Menu Enhancements

```javascript
// Enhanced mobile menu
class MobileMenu {
    constructor() {
        this.menu = document.querySelector('.mobile-menu');
        this.accordionItems = document.querySelectorAll('.accordion-menu-item');

        this.init();
    }

    init() {
        // Accordion functionality
        this.accordionItems.forEach(item => {
            const trigger = item.querySelector('.accordion-trigger');
            const content = item.querySelector('.accordion-content');

            trigger?.addEventListener('click', () => {
                // Close other items
                this.accordionItems.forEach(otherItem => {
                    if (otherItem !== item) {
                        otherItem.classList.remove('active');
                    }
                });

                // Toggle current item
                item.classList.toggle('active');

                // Animate height
                if (item.classList.contains('active')) {
                    content.style.maxHeight = content.scrollHeight + 'px';
                } else {
                    content.style.maxHeight = '0';
                }
            });
        });

        // Search functionality
        this.initSearch();
    }

    initSearch() {
        const searchToggle = document.querySelector('.mobile-search-toggle');
        const searchBox = document.querySelector('.mobile-search-box');

        searchToggle?.addEventListener('click', () => {
            searchBox.classList.toggle('active');
            if (searchBox.classList.contains('active')) {
                searchBox.querySelector('input').focus();
            }
        });
    }
}
```

## Styling & Customization

### Custom Panel Styles

```css
/* Dark theme panel */
.reign-left-panel.dark-theme {
    background: #1a1a1a;
    color: #fff;
}

.reign-left-panel.dark-theme .panel-menu a {
    color: #e0e0e0;
}

.reign-left-panel.dark-theme .panel-menu a:hover {
    background: #2a2a2a;
    color: #fff;
}

/* Glass morphism effect */
.reign-left-panel.glass {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border-right: 1px solid rgba(255, 255, 255, 0.2);
}

/* Gradient background */
.reign-left-panel.gradient {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
}
```

### Mobile Menu Animations

```css
/* Slide in from left */
@keyframes slideInLeft {
    from {
        transform: translateX(-100%);
    }
    to {
        transform: translateX(0);
    }
}

.mobile-menu.slide-in {
    animation: slideInLeft 0.3s ease-out;
}

/* Fade and scale */
@keyframes fadeScale {
    from {
        opacity: 0;
        transform: scale(0.9);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}

.mobile-menu-item {
    animation: fadeScale 0.2s ease-out;
    animation-fill-mode: both;
}

.mobile-menu-item:nth-child(1) { animation-delay: 0.1s; }
.mobile-menu-item:nth-child(2) { animation-delay: 0.15s; }
.mobile-menu-item:nth-child(3) { animation-delay: 0.2s; }
```

## Widget Areas

### Register Panel Widget Area

```php
// Register widget area for left panel
function reign_register_panel_widgets() {
    register_sidebar(array(
        'name' => 'Left Panel Widgets',
        'id' => 'left-panel-widgets',
        'description' => 'Widgets for the left panel',
        'before_widget' => '<div class="panel-widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>'
    ));
}
add_action('widgets_init', 'reign_register_panel_widgets');
```

### Custom Panel Widgets

```php
// Quick links widget for panel
class Reign_Panel_Quick_Links extends WP_Widget {

    public function __construct() {
        parent::__construct(
            'reign_panel_quick_links',
            'Panel Quick Links',
            array('description' => 'Quick navigation links for left panel')
        );
    }

    public function widget($args, $instance) {
        echo $args['before_widget'];
        ?>
        <ul class="panel-quick-links">
            <li><a href="/dashboard"><i class="fa fa-tachometer-alt"></i> Dashboard</a></li>
            <li><a href="/members"><i class="fa fa-users"></i> Members</a></li>
            <li><a href="/groups"><i class="fa fa-users-cog"></i> Groups</a></li>
            <li><a href="/forums"><i class="fa fa-comments"></i> Forums</a></li>
            <li><a href="/shop"><i class="fa fa-shopping-cart"></i> Shop</a></li>
            <li><a href="/blog"><i class="fa fa-blog"></i> Blog</a></li>
        </ul>
        <?php
        echo $args['after_widget'];
    }
}
```

## Performance Optimization

### Lazy Loading Panel Content

```javascript
// Load panel content on first open
let panelLoaded = false;

document.addEventListener('panelOpened', function() {
    if (!panelLoaded) {
        fetch(ajaxurl + '?action=load_panel_content')
            .then(response => response.text())
            .then(html => {
                document.querySelector('.panel-dynamic-content').innerHTML = html;
                panelLoaded = true;
            });
    }
});
```

### Cache Panel Menu

```php
// Cache panel menu
function reign_get_panel_menu_cached() {
    $cache_key = 'reign_panel_menu_' . get_current_user_id();
    $menu = get_transient($cache_key);

    if (false === $menu) {
        ob_start();
        wp_nav_menu(array(
            'theme_location' => 'left-panel-menu',
            'echo' => true
        ));
        $menu = ob_get_clean();
        set_transient($cache_key, $menu, HOUR_IN_SECONDS);
    }

    return $menu;
}
```

## Accessibility

### ARIA Labels

```html
<nav class="reign-left-panel" role="navigation" aria-label="Main navigation">
    <button class="panel-trigger"
            aria-expanded="false"
            aria-controls="left-panel"
            aria-label="Open menu">
        <span class="sr-only">Menu</span>
    </button>

    <div id="left-panel" aria-hidden="true">
        <!-- Panel content -->
    </div>
</nav>
```

### Keyboard Navigation

```javascript
// Keyboard navigation support
document.addEventListener('keydown', function(e) {
    const panel = document.querySelector('.reign-left-panel');

    if (panel.classList.contains('active')) {
        const focusableElements = panel.querySelectorAll(
            'a, button, input, select, textarea, [tabindex]:not([tabindex="-1"])'
        );

        const firstElement = focusableElements[0];
        const lastElement = focusableElements[focusableElements.length - 1];

        // Tab trap
        if (e.key === 'Tab') {
            if (e.shiftKey) {
                if (document.activeElement === firstElement) {
                    e.preventDefault();
                    lastElement.focus();
                }
            } else {
                if (document.activeElement === lastElement) {
                    e.preventDefault();
                    firstElement.focus();
                }
            }
        }
    }
});
```

## Troubleshooting

### Common Issues

#### Panel Not Opening

**Solutions:**
1. Check JavaScript errors in console
2. Verify trigger element exists
3. Check z-index conflicts
4. Clear cache

#### Menu Items Not Showing

**Solutions:**
1. Verify menu location is assigned
2. Check user permissions
3. Clear menu cache
4. Verify walker class exists

#### Mobile Menu Issues

**Solutions:**
1. Check breakpoint settings
2. Verify mobile CSS is loading
3. Test touch events
4. Check viewport meta tag

---

*For more navigation options, see the Header Layouts documentation.*