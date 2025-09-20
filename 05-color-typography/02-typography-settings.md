# Typography Settings Guide

## Overview

Control all typography aspects of your Reign theme through the Customizer. Set fonts, sizes, weights, and styles for every element.

## Accessing Typography Settings

**Location:** Appearance → Customize → General → Typography

## Typography Sections

### 1. Body Typography
```
Font Family: System Font / Google Font / Custom
Font Size: 16px (default)
Line Height: 1.6
Font Weight: 400
Text Transform: None
Letter Spacing: 0
```

### 2. Heading Typography

#### H1 Settings
- Font Size: 36px
- Line Height: 1.2
- Font Weight: 700
- Text Transform options

#### H2-H6 Settings
Individual controls for each heading level

### 3. Menu Typography

#### Main Menu
- Font Family: Inherit or custom
- Font Size: 14px
- Font Weight: 500
- Text Transform: Uppercase/None
- Letter Spacing: 1px

#### Mobile Menu
Separate typography settings for mobile

### 4. Widget Typography
- Widget Titles
- Widget Content
- Sidebar Widgets
- Footer Widgets

## Google Fonts Integration

### How to Add Google Fonts
1. Select "Google Font" from Font Family dropdown
2. Choose from 900+ Google Fonts
3. Select font weights needed
4. Apply to specific elements

### Performance Tips
- Limit to 2-3 font families
- Load only needed weights
- Use font-display: swap
- Consider system fonts first

## Font Loading Options

### Loading Methods
1. **Standard** - Default loading
2. **Async** - Non-blocking load
3. **Preload** - Priority loading
4. **System Fonts** - No loading needed

## Custom Fonts

### Adding Custom Fonts
1. Upload font files via Media Library
2. Add @font-face CSS
3. Select in Typography settings

### Supported Formats
- WOFF2 (recommended)
- WOFF
- TTF
- EOT (legacy)

## Responsive Typography

### Mobile Settings
```
Mobile Base Font Size: 14px
Tablet Base Font Size: 15px
Desktop Base Font Size: 16px
```

### Fluid Typography
Enable responsive scaling:
- Min Font Size: 14px
- Max Font Size: 18px
- Scale with viewport

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

## Troubleshooting

### Common Issues

#### Fonts Not Loading
- Check font URL
- Verify file permissions
- Clear cache
- Check console errors

#### Google Fonts Slow
- Reduce font weights
- Use font-display: swap
- Consider local hosting
- Enable browser caching

#### Custom Fonts Missing
- Verify @font-face syntax
- Check file paths
- Ensure CORS headers
- Test MIME types