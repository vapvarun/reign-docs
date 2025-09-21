# Color Scheme Configuration

## Overview

Reign theme provides comprehensive color customization options through the WordPress Customizer powered by Kirki Framework. The theme includes 7 predefined color schemes plus unlimited custom color options.

## Accessing Color Settings

**Location:** Appearance → Customize → Colors

## Predefined Color Schemes

Reign includes 7 professionally designed color schemes:

### 1. **Default**
- Primary: #3b5998 (Facebook Blue)
- Secondary: #e5e5e5
- Best for: Social networks, community sites

### 2. **Clean** (Recommended)
- Primary: #2d89ef (Bright Blue)
- Secondary: #f5f5f5
- Best for: Modern, minimalist designs

### 3. **Dark**
- Primary: #333333
- Secondary: #1a1a1a
- Best for: Gaming, entertainment, tech sites

### 4. **Dating**
- Primary: #e91e63 (Pink)
- Secondary: #fce4ec
- Best for: Dating platforms, social sites

### 5. **Ectoplasm**
- Primary: #523f6d (Purple)
- Secondary: #a3b745
- Best for: Creative, artistic communities

### 6. **Sunrise**
- Primary: #dd823b (Orange)
- Secondary: #ccaf0b
- Best for: Energy, motivation, fitness sites

### 7. **Coffee**
- Primary: #46403c (Brown)
- Secondary: #59524c
- Best for: Blogs, magazines, content sites

### Switching Color Schemes

1. Navigate to `Customizer → Colors`
2. Select "Color Scheme" radio button set
3. Choose your preferred scheme
4. Click "Publish" to apply changes

**Note:** Switching schemes updates all color settings simultaneously.

## Detailed Color Customization Options

### Top Bar Colors
- `reign_header_topbar_bg_color` - Top bar background
- `reign_header_topbar_text_color` - Top bar text
- `reign_header_topbar_text_hover_color` - Hover state

### Header Colors

**Main Header:**
- `reign_header_bg_color` - Header background
- `reign_header_text_color` - Header text and navigation
- `reign_header_text_hover_color` - Navigation hover
- `reign_header_text_active_color` - Active/current page

**Sticky Header:**
- `reign_sticky_header_bg_color` - Background when scrolled
- `reign_sticky_header_text_color` - Text in sticky state
- `reign_sticky_header_transparency` - Opacity level

**Mobile Header:**
- `reign_mobile_header_bg_color` - Mobile menu background
- `reign_mobile_menu_text_color` - Mobile navigation text
- `reign_mobile_menu_border_color` - Dividers

### Body & Content Colors

**Main Content:**
- `reign_site_body_bg_color` - Main site background
- `reign_site_body_text_color` - Primary text color
- `reign_site_link_color` - Default link color
- `reign_site_link_hover_color` - Link hover state

**Theme Colors:**
- `reign_colors_theme` - Primary theme color
- `reign_site_secondary_bg_color` - Secondary backgrounds
- `reign_site_section_bg_color` - Section backgrounds
- `reign_site_border_color` - Default borders

### Button Colors

**Primary Buttons:**
- `reign_site_button_bg_color` - Button background
- `reign_site_button_text_color` - Button text
- `reign_site_button_hover_bg_color` - Hover background
- `reign_site_button_hover_text_color` - Hover text

### Footer Colors

**Footer Widgets:**
- `reign_footer_widget_area_bg_color` - Footer background
- `reign_footer_widget_area_text_color` - Footer text
- `reign_footer_widget_area_link_color` - Footer links
- `reign_footer_widget_area_link_hover_color` - Link hover

**Copyright Area:**
- `reign_footer_copyright_bg_color` - Copyright background
- `reign_footer_copyright_text_color` - Copyright text
- `reign_footer_copyright_link_color` - Copyright links

### BuddyPress Colors
- Activity stream backgrounds
- Member card styling
- Group headers
- Profile navigation
- Notification badges

### WooCommerce Colors
- Product card backgrounds
- Price colors
- Sale badge styling
- Add to cart buttons
- Checkout elements

## Youzify Integration

If using Youzify plugin, Reign provides an override option:

```
Customizer → Colors → Override Youzify Default Appearance Mode
```

- **ON**: Reign colors override Youzify styling
- **OFF**: Youzify maintains its own color scheme

## Dark Mode Settings

### Enabling Dark Mode

```
Customizer → General → Dark Mode
```

**Options:**
- Enable Dark Mode Toggle
- Default Mode: Light/Dark/Auto
- Auto-detect System Preference
- Save User Preference

**Note:** All color settings have dark mode equivalents that activate automatically.

## CSS Variables & Custom Properties

Reign uses CSS custom properties for easy customization:

```css
:root {
    --reign-primary-color: #2d89ef;
    --reign-secondary-color: #f5f5f5;
    --reign-text-color: #333333;
    --reign-link-color: #2d89ef;
    --reign-border-color: #e5e5e5;
    --reign-header-bg: #ffffff;
    --reign-footer-bg: #1a1a1a;
}
```

### Override in Child Theme

```css
/* Child theme style.css */
:root {
    --reign-primary-color: #your-color !important;
    --reign-secondary-color: #your-color !important;
}
```

## Performance Optimization

### Color Loading
- Dynamic CSS is generated on save
- Styles are cached for performance
- CSS is minified automatically
- Critical CSS is inlined

### Best Practices
1. Use predefined color schemes when possible
2. Limit custom color variations
3. Test color contrast for accessibility
4. Clear cache after color changes

## Troubleshooting

### Colors Not Updating

**Solutions:**
1. Clear browser cache (Ctrl+F5)
2. Clear server/plugin cache
3. Check file permissions for CSS generation
4. Disable caching plugins temporarily
5. Regenerate CSS in Customizer

### Color Conflicts

If colors are being overridden:

```css
/* Increase specificity */
body.reign-theme .element {
    color: #your-color !important;
}
```

## Export/Import Color Settings

### Export Settings
1. Install Customizer Export/Import plugin
2. Go to `Customizer → Export/Import`
3. Click "Export"
4. Save .dat file with all color settings

### Import Settings
1. Go to `Customizer → Export/Import`
2. Choose your .dat file
3. Click "Import"
4. Preview before publishing

## Accessibility Guidelines

### WCAG Compliance
- Normal Text: 4.5:1 contrast ratio
- Large Text: 3:1 contrast ratio
- UI Components: 3:1 contrast ratio

### Testing Tools
- Chrome DevTools Contrast Checker
- WebAIM Contrast Checker
- Accessibility Insights

## Advanced Customization

### Creating Custom Color Schemes

```php
// In child theme functions.php
function my_custom_color_scheme() {
    return array(
        'primary' => '#custom1',
        'secondary' => '#custom2',
        'header_bg' => '#custom3',
        // Add all color options
    );
}
add_filter('reign_color_schemes', 'my_custom_color_scheme');
```

### Conditional Colors

```php
// Different colors for different pages
add_action('wp_head', function() {
    if (is_page('special-page')) {
        ?>
        <style>
            :root {
                --reign-primary-color: #special-color;
            }
        </style>
        <?php
    }
});
```

## Integration with Page Builders

### Elementor
- Theme colors available in color picker
- Global colors sync automatically
- Can override per element

### Gutenberg
- Theme color palette in block editor
- Custom colors per block
- Global styles support

### Other Builders
- Beaver Builder: Import theme colors
- Divi: Use theme defaults
- Visual Composer: Color synchronization

---

*For more customization options, see the Typography Settings guide.*
4. **Community** - Warm social colors
5. **Creative** - Vibrant and bold
6. **Minimal** - Subtle grayscale

## Dark Mode Configuration

### Enable Dark Mode
**Location:** Customize → General → Dark Mode

### Dark Mode Options
- Toggle Style (4 styles available)
- Auto-detect system preference
- User preference cookie
- Separate dark color scheme

## Custom CSS for Colors

Add custom color rules:
```css
/* Custom color overrides */
:root {
    --reign-primary: #667eea;
    --reign-secondary: #764ba2;
    --reign-text: #333333;
}
```

## Performance Considerations

- Use CSS variables for consistency
- Minimize custom color rules
- Test contrast ratios for accessibility
- Optimize for dark/light mode switching

## Best Practices

1. **Maintain Contrast** - WCAG AA compliance minimum
2. **Brand Consistency** - Use your brand colors
3. **Test Dark Mode** - Ensure readability
4. **Mobile Testing** - Colors may appear different
5. **Browser Testing** - Cross-browser compatibility