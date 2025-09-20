# Elementor Integration Guide

## Overview

Elementor is the leading WordPress page builder, and Reign theme provides full compatibility with custom widgets, templates, and enhanced features specifically designed for community and e-commerce sites.

## Installation & Setup

### Installing Elementor

1. **Install Elementor:**
   ```
   Plugins → Add New → Search "Elementor"
   Install and Activate
   ```

2. **Elementor Pro (Optional):**
   - Purchase from elementor.com
   - Install Elementor Pro plugin
   - Activate license

3. **Reign-Elementor Integration:**
   - Auto-detected on activation
   - Custom widgets loaded
   - Theme styles integrated

## Reign Custom Widgets

### Community Widgets

#### BuddyPress Activity Widget
```
Widget Name: Reign Activity Stream
Settings:
- Type: Sitewide/Friends/Groups
- Max Items: 5-50
- Show Filters: Yes/No
- Show Post Form: Yes/No
- Layout: List/Grid/Cards
```

#### Members Grid Widget
```
Widget Name: Reign Members
Options:
- Layout: Grid/List/Carousel
- Columns: 2-6
- Member Type: All/Specific
- Order: Active/Newest/Random
- Show: Avatar/Name/Last Active
```

#### Groups Display Widget
```
Widget Name: Reign Groups
Features:
- Display Type: Grid/List/Slider
- Max Groups: 10-50
- Filter: Popular/Active/Newest
- Show Meta: Members Count/Activity
```

### E-commerce Widgets

#### Product Grid Plus
```
Enhanced WooCommerce Grid:
- Quick View
- Wishlist Button
- Compare Feature
- Ajax Add to Cart
- Sale Countdown
```

#### Shop Categories
```
Category Display:
- Image + Title
- Product Count
- Subcategories
- Custom Icons
- Hover Effects
```

### Custom Headers/Footers

#### Header Builder
```
Elements:
- Logo (Regular/Sticky/Mobile)
- Navigation Menu
- Search Bar
- User Menu
- Cart Icon
- Social Icons
- Custom HTML
```

#### Footer Builder
```
Sections:
- Widget Areas
- Copyright Text
- Footer Menu
- Social Links
- Newsletter Form
- Back to Top
```

## Theme Builder Integration

### Template Types

**Available Templates:**
```
✓ Single Post
✓ Post Archive
✓ Single Page
✓ 404 Page
✓ Search Results
✓ Single Product (WooCommerce)
✓ Product Archive
✓ Member Profile (BuddyPress)
✓ Group Single
✓ Activity Page
```

### Creating Custom Templates

1. **Navigate to:** Templates → Theme Builder
2. **Add New:** Select template type
3. **Design:** Use Elementor editor
4. **Conditions:** Set display rules
5. **Publish:** Save and activate

### Dynamic Content

**Dynamic Tags:**
```
Post/Page:
- Title
- Content
- Featured Image
- Custom Fields
- Author Info

BuddyPress:
- Member Name
- Avatar
- Cover Image
- Last Active
- Member Type

WooCommerce:
- Product Price
- Add to Cart
- Product Gallery
- Stock Status
- Reviews
```

## Global Styles

### Color System

**Reign Color Integration:**
```css
/* Use theme colors in Elementor */
Primary Color: var(--reign-primary)
Secondary: var(--reign-secondary)
Text: var(--reign-text)
Background: var(--reign-background)
```

### Typography System

**Font Integration:**
```
Headings: Theme Default
Body: Theme Default
Custom: Google Fonts
Variable Fonts: Supported
```

### Spacing System

**Consistent Spacing:**
```
XS: 5px
S: 10px
M: 20px
L: 40px
XL: 80px
```

## Page Layouts

### Full Width Pages

**Setup:**
1. Edit with Elementor
2. Page Settings → Page Layout
3. Select: Elementor Full Width
4. Hide Title: Yes

### Landing Pages

**Elements for Landing:**
```
- Hero Section
- Features Grid
- Testimonials
- Pricing Table
- CTA Sections
- Newsletter
- Footer
```

### Community Pages

**BuddyPress Pages:**
```
Custom Activity Page:
- Activity Feed Widget
- Filters Sidebar
- Post Update Form
- Online Members

Custom Members Page:
- Search Bar
- Filter Options
- Members Grid
- Pagination
```

## Performance Optimization

### Elementor Settings

**Optimize Performance:**
```
Settings → Elementor → Advanced:
✓ Improved Asset Loading
✓ Improved DOM Output
✓ Optimized Image Loading
✓ Dynamic CSS Print Method
□ Element Caching (test first)
```

### Widget Load Control

```php
// Load widgets conditionally
function reign_elementor_widget_control() {
    if (!is_page('heavy-page')) {
        // Unregister heavy widgets
        add_action('elementor/widgets/widgets_unregistered', function($widgets_manager) {
            $widgets_manager->unregister_widget_type('heavy-widget');
        });
    }
}
add_action('init', 'reign_elementor_widget_control');
```

### CSS Optimization

```php
// Inline critical CSS
function reign_inline_elementor_critical_css() {
    if (is_front_page()) {
        echo '<style>' . get_critical_css() . '</style>';
    }
}
add_action('wp_head', 'reign_inline_elementor_critical_css', 5);
```

## Responsive Design

### Breakpoints

**Device Breakpoints:**
```
Mobile: 320px - 767px
Tablet: 768px - 1024px
Desktop: 1025px+
Custom: Define your own
```

### Responsive Controls

**Per Device Settings:**
- Typography size
- Spacing/Padding
- Column width
- Hide/Show elements
- Alignment

## Custom CSS & JavaScript

### Adding Custom CSS

**Widget Level:**
```css
selector {
    /* Your CSS */
}

/* With responsive */
@media (max-width: 767px) {
    selector {
        /* Mobile CSS */
    }
}
```

### Adding Custom JS

**Page Level:**
```javascript
<script>
jQuery(document).ready(function($) {
    // Your code
});
</script>
```

## Popup Builder

### Creating Popups

**Popup Types:**
```
- Welcome Popup
- Exit Intent
- Time Delay
- Scroll Trigger
- Click Trigger
```

### Popup Settings

```
Display Conditions:
- Entire Site
- Specific Pages
- User Roles
- Date Range
- Device Type

Triggers:
- On Page Load
- On Scroll (%)
- On Exit Intent
- On Click
- After Inactivity
```

## Forms Integration

### Form Builders

**Compatible Forms:**
- Elementor Forms (Pro)
- Contact Form 7
- WPForms
- Gravity Forms
- Ninja Forms

### Form Styling

```css
/* Reign form styles */
.elementor-form {
    --reign-input-bg: #f5f5f5;
    --reign-input-border: #ddd;
    --reign-input-focus: var(--reign-primary);
}
```

## WooCommerce Builder

### Product Pages

**Custom Product Layout:**
```
- Product Gallery (custom)
- Product Title
- Price & Variations
- Add to Cart (styled)
- Tabs (custom design)
- Related Products
- Reviews
```

### Shop Pages

**Shop Archive:**
```
- Filters Sidebar
- Product Grid
- Sorting Options
- Pagination
- Quick View
```

### Cart & Checkout

**Custom Checkout:**
```
- Multi-step checkout
- Order summary
- Payment methods
- Trust badges
- Coupon field
```

## Maintenance Mode

### Coming Soon Page

**Create with Elementor:**
1. Templates → Landing Pages
2. Create Coming Soon
3. Settings → Reading
4. Select Coming Soon page
5. Enable Maintenance Mode

**Elements:**
- Logo
- Countdown Timer
- Newsletter Signup
- Social Links
- Contact Info

## Troubleshooting

### Common Issues

#### Styling Conflicts
```css
/* Fix with higher specificity */
.reign-theme .elementor-widget {
    /* Override styles */
}
```

#### Widget Not Loading
- Clear Elementor cache
- Regenerate CSS
- Check widget registration
- Verify dependencies

#### Performance Issues
- Reduce widgets per page
- Optimize images
- Enable lazy load
- Minimize DOM size

## Code Snippets

### Register Custom Widget

```php
class Reign_Custom_Widget extends \Elementor\Widget_Base {

    public function get_name() {
        return 'reign_custom';
    }

    public function get_title() {
        return __('Reign Custom', 'reign');
    }

    protected function _register_controls() {
        // Widget controls
    }

    protected function render() {
        // Widget output
    }
}

// Register widget
add_action('elementor/widgets/widgets_registered', function($widgets_manager) {
    $widgets_manager->register_widget_type(new Reign_Custom_Widget());
});
```

### Custom Dynamic Tag

```php
class Reign_Dynamic_Tag extends \Elementor\Core\DynamicTags\Tag {

    public function get_name() {
        return 'reign-dynamic';
    }

    public function get_title() {
        return __('Reign Dynamic', 'reign');
    }

    public function get_categories() {
        return ['text'];
    }

    public function render() {
        echo get_reign_dynamic_content();
    }
}
```

## Best Practices

1. **Performance First** - Don't overload with widgets
2. **Mobile Responsive** - Test all breakpoints
3. **Semantic HTML** - Use proper heading hierarchy
4. **Accessibility** - Alt texts, ARIA labels
5. **SEO Friendly** - Proper meta, schema markup
6. **Cache Strategy** - Use Elementor cache wisely
7. **Version Control** - Export templates regularly
8. **Testing** - Cross-browser compatibility