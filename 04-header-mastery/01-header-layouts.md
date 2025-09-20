# Header Layouts - 4 Professional Styles

## Overview

Reign theme offers 4 distinct header layouts (v1-v4), each designed for specific use cases. These layouts are configured through the Customizer and use template files from `/template-parts/header/`.

## Accessing Header Settings

**Location:** Appearance → Customize → Header → Layout

## Header Layout Options

### Header Version 1: Logo Center Classic

**Template File:** `/template-parts/header/header-v1.php`

**Description:**
- Logo positioned in center
- Navigation menu below logo
- Classic, traditional layout

**Best For:**
- Blogs
- Traditional websites
- Sites with prominent branding

**Features:**
- Centered branding focus
- Full-width menu below
- Optional top bar support
- Sticky header compatible

### Header Version 2: Logo Left (Default)

**Template File:** `/template-parts/header/header-v2.php`

**Description:**
- Logo on the left side
- Menu aligned to the right
- Most common layout style

**Best For:**
- Business websites
- Community sites
- General purpose

**Features:**
- Standard navigation pattern
- User menu integration
- Search option available
- BuddyPress icons support

### Header Version 3: Inline Layout

**Template File:** `/template-parts/header/header-v3.php`

**Description:**
- Logo and menu in the same line
- Compact, space-efficient design

**Best For:**
- Minimal designs
- Sites with few menu items
- Modern layouts

**Features:**
- Space-efficient
- Clean appearance
- Mobile-friendly
- Inline navigation

### Header Version 4: Logo Right with Search

**Template File:** `/template-parts/header/header-v4.php`

**Description:**
- Logo positioned on the right
- Menu on the left
- Integrated search functionality

**Best For:**
- E-commerce sites
- Search-focused platforms
- Unique layouts
- RTL language sites

**Features:**
- Reversed layout
- Search options (Product Search or Default Search)
- Different visual flow
- WooCommerce optimized

## Header Configuration Options

### Sticky Header

**Location:** Customize → Header → Sticky Menu

**Settings:**
```
Enable Sticky Header: Yes/No
Custom Style for Sticky: Enable/Disable
Sticky Header Logo: Upload separate logo
Background Color: Custom color for sticky state
```

**Code Reference:**
```php
get_theme_mod( 'reign_header_sticky_menu_enable', true )
get_theme_mod( 'reign_header_sticky_menu_custom_style_enable', false )
get_theme_mod( 'reign_sticky_header_menu_logo', '' )
```

### Mobile Header

**Location:** Customize → Header → Mobile Menu

**Mobile Header Layouts:**
1. **Layout One** - Standard mobile menu
2. **Layout Two** - Centered logo
3. **Layout Three** - Custom configuration

### Top Bar

**Location:** Customize → Header → Top Bar

**Options:**
- Enable/Disable top bar
- Add social links
- Contact information
- Custom HTML content

### Left Panel

**Location:** Customize → Header → Left Panel

**Features:**
- Slide-out navigation
- Additional menu space
- Widget area support
- Mobile-friendly

## Header Search Options (Version 4)

When using Header Version 4, you can choose search functionality:

**Location:** Customize → Header → Layout → Header Search Option

**Options:**
- **Product Search** - WooCommerce product search (if WooCommerce active)
- **Default Search** - WordPress default search

**Code Reference:**
```php
get_theme_mod( 'reign_header_search_option', 'product_search' )
```

## Main Menu Hover Styles

**Location:** Customize → Header → Layout → Main Menu Hover Style

**Available Styles:**
1. **Style 1** - Basic hover
2. **Style 2** - Underline effect
3. **Style 3** - Background change
4. **Style 4** - Advanced animation

## BuddyPress Integration

### Header Icons

When BuddyPress is active, header can display:
- Notifications bubble
- Messages count
- Friend requests
- Profile dropdown

**Configuration:**
Dashboard → Reign Settings → Community Settings → Header Icons

## Customization Examples

### Custom CSS for Headers

```css
/* Header V1 Customization */
.header-desktop.version-one {
    background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
}

/* Header V2 Customization */
.header-desktop.version-two .main-navigation {
    font-weight: 600;
}

/* Header V3 Customization */
.header-desktop.version-three {
    padding: 20px 0;
}

/* Header V4 Customization */
.header-desktop.version-four .search-form {
    max-width: 300px;
}
```

### PHP Hooks

```php
// Add content before header
add_action('reign_before_header', function() {
    echo '<div class="announcement">Welcome!</div>';
});

// Modify header classes
add_filter('reign_header_class', function($classes) {
    $classes[] = 'custom-header';
    return $classes;
});
```

## Responsive Behavior

### Breakpoints
- **Desktop:** > 1024px - Full header shown
- **Tablet:** 768-1024px - Simplified header
- **Mobile:** < 768px - Mobile menu activated

### Mobile Menu Configuration

**Logged-in Users Menu Location:**
- Dashboard → Appearance → Menus
- Select "Mobile Menu - Logged-in users"

**Logged-out Users Menu Location:**
- Dashboard → Appearance → Menus
- Select "Mobile Menu - Logged-out users"

## Troubleshooting

### Header Not Displaying Correctly

1. **Check Header Version Setting**
   - Customize → Header → Layout
   - Verify correct version selected

2. **Clear Cache**
   - Browser cache
   - Plugin cache
   - CDN cache

3. **Verify Template Files**
   - Check `/template-parts/header/` exists
   - Ensure no child theme conflicts

### Sticky Header Issues

**Not Sticking:**
- Enable in Customize → Header → Sticky Menu
- Check for JavaScript errors
- Verify no CSS conflicts

**Logo Not Changing:**
- Upload sticky header logo
- Check file format (PNG/JPG/SVG)
- Clear cache

### Mobile Menu Problems

**Not Opening:**
- Check mobile menu assignment
- Verify JavaScript enabled
- Test in actual mobile device

## Best Practices

1. **Choose Layout Based on Content**
   - V1 for brand focus
   - V2 for standard sites (default)
   - V3 for minimal menus
   - V4 for search-heavy sites

2. **Optimize for Performance**
   - Use optimized logo images
   - Minimize menu items
   - Enable sticky only if needed

3. **Mobile First**
   - Test all headers on mobile
   - Configure mobile-specific menus
   - Check touch interactions

## Related Settings

- **Typography:** Customize → General → Typography → Header Main Menu
- **Colors:** Customize → Colors → Main Menu Colors
- **Mobile:** Customize → Header → Mobile Menu
- **BuddyPress:** Reign Settings → Community Settings

---

**Need Help?** The header system is flexible. Start with Version 2 (default) and experiment with other layouts to find your perfect match.