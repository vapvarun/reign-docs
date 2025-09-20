# Sidebar Configuration Guide

## Overview

Reign theme provides flexible sidebar management with multiple layouts, custom widths, and widget areas. Control sidebars globally or per-page basis.

## Sidebar Layouts

### Global Layout Options

**Location:** Appearance → Customize → General → Site Layout → Sidebar Layout

1. **Right Sidebar** (Default)
   - Content: 71.875% (default)
   - Sidebar: 28.125% (default)

2. **Left Sidebar**
   - Sidebar: 28.125%
   - Content: 71.875%

3. **No Sidebar**
   - Content: 100%

4. **Both Sidebars**
   - Left: 25%
   - Content: 50%
   - Right: 25%

## Sidebar Width Configuration

### Custom Width Settings

**Location:** Customize → General → Site Layout → Sidebar Width

```
Default Width: 28.125%
Custom Width Range: 20% - 40%
```

### Calculating Content Width
```
Content Width = 100% - Sidebar Width
Example: 100% - 28.125% = 71.875%
```

## Widget Areas

### Default Widget Areas

1. **Blog Sidebar** - Blog and archive pages
2. **Page Sidebar** - Static pages
3. **Shop Sidebar** - WooCommerce pages
4. **BuddyPress Sidebar** - Community pages
5. **Forum Sidebar** - bbPress forums

### Adding Widgets

1. Go to Appearance → Widgets
2. Select sidebar area
3. Add widgets:
   - Search
   - Recent Posts
   - Categories
   - Archives
   - Custom HTML
   - Text Widget

## Page-Specific Sidebars

### Override Global Settings

In page/post editor:
1. Look for "Page Attributes" or "Reign Settings"
2. Select sidebar layout:
   - Default (use global)
   - Right Sidebar
   - Left Sidebar
   - No Sidebar
   - Both Sidebars

### Custom Sidebars per Page

Using code:
```php
// Register custom sidebar
function reign_custom_sidebar() {
    register_sidebar(array(
        'name' => 'Custom Page Sidebar',
        'id' => 'custom-page-sidebar',
        'before_widget' => '<div class="widget %2$s">',
        'after_widget' => '</div>',
    ));
}
add_action('widgets_init', 'reign_custom_sidebar');
```

## Sticky Sidebar

### Enable Sticky Sidebar

**Location:** Customize → General → Site Layout → Sticky Sidebar

**Settings:**
```
Enable Sticky: Yes/No
Offset from Top: 100px (for fixed header)
Offset from Bottom: 50px
Mobile Sticky: Disabled by default
```

### Requirements for Sticky
- Sidebar shorter than content
- JavaScript enabled
- Not on mobile (optional)

## BuddyPress Sidebars

### Community Page Sidebars

**Activity Page:**
- Right sidebar recommended
- Activity widgets
- Member widgets

**Members Directory:**
- Left or right sidebar
- Member search
- Member filters

**Groups Directory:**
- Sidebar with group widgets
- Group categories
- Group search

### BuddyPress Widget Options
- Who's Online
- Recently Active Members
- Groups
- Recent Activity
- Member Statistics

## WooCommerce Sidebars

### Shop Page Sidebar

**Widgets:**
- Product Categories
- Price Filter
- Product Search
- Recent Products
- Product Tags

### Single Product Sidebar
- Related Products
- Best Sellers
- Product Reviews
- Recently Viewed

## Mobile Sidebar Behavior

### Responsive Settings

**Below 768px:**
- Sidebar moves below content
- Full width display
- Optional: Hide completely
- Toggle button option

### Mobile Menu Integration
```
Mobile Sidebar Display:
○ Below Content (default)
○ Off-canvas Left
○ Off-canvas Right
○ Hide on Mobile
```

## Advanced Sidebar Features

### Conditional Sidebars

Show different sidebars based on conditions:
```php
function reign_conditional_sidebar() {
    if (is_home()) {
        dynamic_sidebar('blog-sidebar');
    } elseif (is_shop()) {
        dynamic_sidebar('shop-sidebar');
    } else {
        dynamic_sidebar('page-sidebar');
    }
}
```

### Multiple Sidebars

Create unlimited sidebars:
1. Use plugin like "Custom Sidebars"
2. Or register via functions.php
3. Assign to specific pages
4. Manage widgets separately

## Sidebar Styling

### Custom CSS

```css
/* Sidebar styling */
.widget-area {
    background: #f8f9fa;
    padding: 30px;
    border-radius: 10px;
}

.widget {
    margin-bottom: 30px;
}

.widget-title {
    font-size: 18px;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 2px solid #667eea;
}
```

### Widget Styling
- Background colors
- Borders and shadows
- Spacing adjustments
- Typography settings

## Performance Optimization

1. **Limit Widgets** - Use only necessary widgets
2. **Lazy Load Images** - In widget areas
3. **Cache Widgets** - Use caching plugin
4. **Minimize Scripts** - Widget JavaScript
5. **Optimize Queries** - Recent posts widgets

## Troubleshooting

### Sidebar Not Showing

**Check:**
- Global sidebar settings
- Page-specific overrides
- Widget areas have widgets
- Theme support for sidebars
- Cache cleared

### Sticky Not Working

**Solutions:**
- Check JavaScript errors
- Verify offset settings
- Test without plugins
- Check browser compatibility
- Ensure proper HTML structure

### Widgets Missing

**Fix:**
- Re-save widgets
- Check widget visibility settings
- Verify user permissions
- Test in safe mode
- Check PHP errors

## Best Practices

1. **Consistent Layout** - Use same sidebar position site-wide
2. **Relevant Widgets** - Context-appropriate widgets
3. **Mobile Experience** - Test on all devices
4. **Performance** - Limit widget count
5. **Accessibility** - Proper heading structure

## Hooks and Filters

### Useful Hooks

```php
// Before sidebar
do_action('reign_before_sidebar');

// After sidebar
do_action('reign_after_sidebar');

// Custom sidebar content
add_action('reign_sidebar_content', 'custom_sidebar_content');
```

### Filters

```php
// Filter sidebar width
add_filter('reign_sidebar_width', function($width) {
    return '30%';
});

// Filter sidebar position
add_filter('reign_sidebar_position', function($position) {
    return 'left';
});
```