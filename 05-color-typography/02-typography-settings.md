# Typography Settings Guide

## Overview

Reign Theme provides comprehensive typography controls through the WordPress Customizer powered by Kirki Framework. Customize fonts, sizes, weights, line heights, and more for every element of your site with live preview.

## Accessing Typography Settings

**Primary Location:** Appearance → Customize → General → Typography

**Additional Typography Controls:**
- Header → Menu Typography
- Footer → Footer Typography
- Blog → Blog Typography
- BuddyPress → Community Typography

## Typography Sections

### 1. Body Typography

#### Font Family Options

**System Fonts (Fastest Performance):**
```css
-apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
Oxygen-Sans, Ubuntu, Cantarell, "Helvetica Neue", sans-serif
```

**Google Fonts:**
- 900+ fonts available
- Auto-loaded on demand
- GDPR compliant options
- Local hosting available

**Custom Fonts:**
- Upload WOFF, WOFF2, TTF, OTF
- Self-hosted for privacy
- Brand-specific fonts

#### Body Font Settings
```
Font Family: Choose from dropdown
Font Size: 14px-20px (default: 16px)
Line Height: 1.2-2.0 (default: 1.6)
Font Weight: 100-900 (default: 400)
Font Style: Normal/Italic
Text Transform: None/Uppercase/Lowercase/Capitalize
Letter Spacing: -2px to 5px (default: 0)
```

**CSS Variable:**
```css
--reign-body-font: 'Your Font', sans-serif;
--reign-font-size-base: 16px;
--reign-line-height-base: 1.6;
```

### 2. Heading Typography

#### Global Heading Font
```
Heading Font Family: Inherit or custom
Font Weight: 100-900 (default: 600)
Font Style: Normal/Italic
Text Transform: None/Uppercase/Lowercase/Capitalize
```

#### Individual Heading Levels

**H1 Settings:**
```
Desktop: 36px-60px (default: 48px)
Tablet: 32px-48px (default: 40px)
Mobile: 28px-40px (default: 32px)
Line Height: 1.2
Font Weight: 700
Margin Bottom: 20px
```

**H2 Settings:**
```
Desktop: 30px-48px (default: 36px)
Tablet: 28px-40px (default: 32px)
Mobile: 24px-32px (default: 28px)
Line Height: 1.3
Font Weight: 600
Margin Bottom: 18px
```

**H3 Settings:**
```
Desktop: 24px-36px (default: 28px)
Tablet: 22px-32px (default: 26px)
Mobile: 20px-28px (default: 24px)
Line Height: 1.4
Font Weight: 600
Margin Bottom: 16px
```

**H4-H6 Settings:**
- H4: 20px-28px (default: 24px)
- H5: 18px-24px (default: 20px)
- H6: 16px-20px (default: 18px)

### 3. Menu Typography

#### Primary Menu
```
Location: Customizer → Header → Menu Typography
```

**Settings:**
- Font Family: Inherit or custom
- Font Size: 14px-18px (default: 15px)
- Font Weight: 400-700 (default: 500)
- Text Transform: None/Uppercase/Lowercase
- Letter Spacing: 0-2px
- Line Height: 1.5-2.0

#### Top Bar Menu
**Settings:**
- Font Size: 12px-14px
- Font Weight: 400-600
- Usually uppercase for visual hierarchy

#### Mobile Menu
**Optimized for Touch:**
- Font Size: 16px-20px (larger for touch targets)
- Font Weight: 400-600
- Line Height: 1.8-2.2 (extra spacing)
- Full-width tap areas

#### Dropdown Menu
- Font Size: 14px-16px
- Slightly smaller than main menu
- Normal text transform

### 4. Widget Typography

#### Widget Titles
**Settings:**
- Font Size: 18px-24px (default: 20px)
- Font Weight: 500-700 (default: 600)
- Text Transform: Options available
- Margin Bottom: 15px-25px
- Color: Inherits from heading color

#### Widget Content
**Settings:**
- Font Size: 14px-16px (default: 15px)
- Line Height: 1.5-1.7
- Color: Inherits from body text

#### Sidebar Widgets
- Can have different settings than footer
- Usually slightly smaller
- Tighter spacing for sidebars

#### Footer Widgets
- Often lighter color for dark footers
- May use different font family
- Adjustable via Footer settings

## Google Fonts Integration

### How to Add Google Fonts
1. Navigate to Typography settings
2. Click Font Family dropdown
3. Select "Google Fonts" tab
4. Choose from 900+ fonts
5. Select required font weights (limit to 2-3)
6. Choose character subsets needed
7. Apply to specific elements

### Performance Settings

**Font Loading Method:**
```
Async (Recommended): Non-blocking, better performance
Sync: Blocking load, no FOUT
```

**Font Display Strategy:**
```css
font-display: swap; /* Recommended - shows fallback immediately */
font-display: block; /* Hide text until font loads */
font-display: fallback; /* Compromise between swap and block */
```

### Character Subsets
Load only needed character sets:
- Latin (default)
- Latin Extended
- Cyrillic
- Greek
- Vietnamese
- Arabic
- Hebrew

### Performance Best Practices
1. **Limit Font Families**: Maximum 2-3 families
2. **Optimize Weights**: Load only used weights (400, 600, 700)
3. **Preload Critical Fonts**:
   ```html
   <link rel="preload" href="font.woff2" as="font" crossorigin>
   ```
4. **Use System Fonts First**: Consider for body text
5. **Enable Browser Caching**: Via .htaccess or server config

## Font Loading Options

### Loading Methods
1. **Standard** - Default loading
2. **Async** - Non-blocking load
3. **Preload** - Priority loading
4. **System Fonts** - No loading needed

## Custom Fonts

### Adding Custom Fonts

#### Method 1: Theme Upload
1. Navigate to `Customizer → Typography → Custom Fonts`
2. Click "Upload Font"
3. Upload font files (WOFF2 recommended)
4. Name your font family
5. Select in typography dropdowns

#### Method 2: Manual CSS
```css
/* Add to Additional CSS or child theme */
@font-face {
    font-family: 'CustomFont';
    src: url('font.woff2') format('woff2'),
         url('font.woff') format('woff');
    font-weight: 400;
    font-style: normal;
    font-display: swap;
}
```

### Supported Formats
- **WOFF2** (Recommended - best compression)
- **WOFF** (Good compatibility)
- **TTF/OTF** (Larger files)
- **EOT** (IE legacy - usually not needed)

### Variable Fonts
Reign supports variable fonts for ultimate flexibility:
```css
@font-face {
    font-family: 'VariableFont';
    src: url('font-variable.woff2') format('woff2-variations');
    font-weight: 100 900; /* Full weight range */
}

## Responsive Typography

### Breakpoint Settings
```
Desktop: 1024px and above
Tablet: 768px to 1023px
Mobile: 767px and below
```

### Responsive Controls

Each typography setting can have different values per device:

**Desktop/Tablet/Mobile Toggle:**
- Click device icons in Customizer
- Set different sizes for each breakpoint
- Preview changes in real-time

### Mobile-Specific Settings
```css
/* Automatic responsive scaling */
body {
    font-size: 16px; /* Desktop */
}

@media (max-width: 1023px) {
    body {
        font-size: 15px; /* Tablet */
    }
}

@media (max-width: 767px) {
    body {
        font-size: 14px; /* Mobile */
    }
}
```

### Fluid Typography (CSS Clamp)

Enable smooth scaling between breakpoints:
```css
/* Modern fluid typography */
font-size: clamp(14px, 2.5vw, 18px);
/* Min: 14px, Preferred: 2.5vw, Max: 18px */
```

## RTL Typography Support

### RTL Settings
- Automatic font adjustment
- RTL-friendly font families
- Proper text alignment
- Direction-aware spacing

## Advanced Typography

### CSS Variables
```css
:root {
    --reign-font-primary: 'Inter', sans-serif;
    --reign-font-heading: 'Poppins', sans-serif;
    --reign-font-size-base: 16px;
    --reign-line-height: 1.6;
}
```

### Custom CSS
Add via Customize → Custom CSS

## Performance Optimization

1. **Subset Fonts** - Load only needed characters
2. **Limit Weights** - 2-3 weights maximum
3. **Local Fonts** - Host fonts locally
4. **Fallback Stack** - Define system fallbacks
5. **Preconnect** - Add preconnect for Google Fonts

## Accessibility

### Best Practices
- Minimum 16px for body text
- Sufficient line height (1.5+)
- High contrast ratios
- Avoid all caps for body text
- Test with screen readers

## Special Typography Settings

### BuddyPress Typography
```
Customizer → BuddyPress → Typography
```

**Activity Stream:**
- Activity text: 15px-16px
- Activity meta: 13px-14px
- Comments: 14px-15px

**Member Profiles:**
- Display name: 24px-32px
- @username: 16px-18px
- Member type: 14px-16px

### WooCommerce Typography
```
Customizer → WooCommerce → Typography
```

**Product Titles:**
- Shop page: 16px-20px
- Single product: 28px-36px

**Prices:**
- Regular: 18px-24px, weight 600
- Sale: Line-through for original

**Buttons:**
- Add to Cart: 14px-16px
- Checkout: 16px-18px bold

### Form Typography

**Input Fields:**
- Font Size: 14px-16px
- Height: 40px-50px
- Placeholder: Lighter color

**Labels:**
- Font Size: 14px-16px
- Font Weight: 500-600
- Margin: 5px-10px bottom

## Troubleshooting

### Common Issues

#### Fonts Not Loading
**Solutions:**
- Check font file paths
- Verify CORS settings
- Clear all caches
- Check browser console for 404s
- Ensure proper MIME types on server

#### Google Fonts GDPR Issues
**Solutions:**
- Use local hosting option
- Implement cookie consent
- Switch to system fonts
- Use Bunny Fonts (GDPR-compliant alternative)

#### Performance Problems
**Solutions:**
- Reduce number of font weights
- Use WOFF2 format
- Implement font-display: swap
- Enable browser caching
- Preload critical fonts

#### Custom Fonts Missing
**Check:**
```css
/* Correct @font-face syntax */
@font-face {
    font-family: 'FontName'; /* Consistent naming */
    src: url('../fonts/font.woff2') format('woff2'); /* Correct path */
    font-weight: 400; /* Match usage */
    font-style: normal;
    font-display: swap;
}
```

#### Mobile Display Issues
- Check responsive settings
- Verify viewport meta tag
- Test on actual devices
- Adjust mobile-specific sizes

## Best Practices

### Typography Hierarchy
1. **Clear Size Progression**: Each level distinctly smaller
2. **Consistent Spacing**: Proportional margins
3. **Weight Variation**: Use weight for emphasis
4. **Limited Families**: 2 fonts maximum (heading + body)

### Readability Guidelines
1. **Body Text**: Minimum 16px
2. **Line Height**: 1.5-1.6 for body
3. **Line Length**: 45-75 characters
4. **Paragraph Spacing**: 1em minimum
5. **Contrast**: WCAG AA compliance

### Performance Focus
1. System fonts for body text
2. Single Google font for headings
3. Limit to 3 weights total
4. Use variable fonts when possible
5. Implement proper caching

---

*For color customization, see the Color Scheme Configuration guide.*