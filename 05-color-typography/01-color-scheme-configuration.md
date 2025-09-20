# Color Scheme Configuration

## Overview

Reign theme provides comprehensive color customization options through the WordPress Customizer. Control every aspect of your site's color scheme from a centralized location.

## Accessing Color Settings

**Location:** Appearance → Customize → Colors

## Color Sections Available

### 1. Theme Colors
- Primary Color
- Secondary Color
- Tertiary Color
- Background Colors
- Text Colors

### 2. Header Colors
- Header Background
- Header Text
- Menu Colors
- Menu Hover States
- Sticky Header Colors

### 3. Footer Colors
- Footer Background
- Footer Text
- Footer Links
- Footer Widget Areas

### 4. BuddyPress Colors
- Activity Stream
- Member Cards
- Group Layouts
- Profile Headers

### 5. WooCommerce Colors
- Product Cards
- Sale Badges
- Cart Buttons
- Checkout Elements

## Color Scheme Presets

### Available Presets
1. **Default** - Clean and professional
2. **Dark Mode** - Modern dark interface
3. **Corporate** - Business-focused palette
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