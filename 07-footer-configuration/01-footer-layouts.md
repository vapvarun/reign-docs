# Footer Configuration Guide

## Overview

The Reign theme footer is fully customizable through the WordPress Customizer. Configure layout, widgets, colors, and content to match your site's needs.

## Accessing Footer Settings

**Location:** Appearance → Customize → Footer

## Footer Layout Options

### Widget Area Layouts

#### Layout 1: Four Columns
```
[Widget 1] [Widget 2] [Widget 3] [Widget 4]
              [Copyright Bar]
```

#### Layout 2: Three Columns
```
[Widget 1] [Widget 2] [Widget 3]
         [Copyright Bar]
```

#### Layout 3: Two Columns
```
[Widget 1 - 50%] [Widget 2 - 50%]
        [Copyright Bar]
```

#### Layout 4: One Column
```
      [Widget 1 - 100%]
      [Copyright Bar]
```

#### Layout 5: Custom Grid
```
[Widget 1 - 30%] [Widget 2 - 40%] [Widget 3 - 30%]
              [Copyright Bar]
```

## Footer Widget Areas

### Available Widget Areas
1. **Footer Widget Area 1** - Primary footer section
2. **Footer Widget Area 2** - Secondary section
3. **Footer Widget Area 3** - Third section
4. **Footer Widget Area 4** - Fourth section
5. **Copyright Widget Area** - Bottom bar

### Adding Widgets
1. Navigate to Appearance → Widgets
2. Select Footer Widget Area
3. Add widgets:
   - Text Widget
   - Menu Widget
   - Social Links
   - Recent Posts
   - Custom HTML

## Footer Customization

### Background Settings
```
Background Type: Color / Image / Gradient
Background Color: #1a1a1a
Background Image: Upload
Background Position: Center
Background Size: Cover
```

### Typography Settings
```
Footer Font Family: Inherit
Footer Font Size: 14px
Footer Line Height: 1.8
Footer Text Color: #ffffff
Footer Link Color: #667eea
Footer Link Hover: #764ba2
```

### Spacing Options
```
Footer Padding Top: 60px
Footer Padding Bottom: 30px
Widget Area Spacing: 30px
Copyright Bar Height: 50px
```

## Copyright Bar Configuration

### Copyright Text
**Location:** Customize → Footer → Copyright

Default Variables:
- `{year}` - Current year
- `{site_name}` - Site title
- `{theme_author}` - Theme developer

Example:
```
© {year} {site_name}. All rights reserved. Theme by {theme_author}
```

### Copyright Bar Layout
- **Left Aligned** - Copyright left, menu right
- **Center Aligned** - Everything centered
- **Right Aligned** - Menu left, copyright right
- **Stacked** - Copyright above, menu below

## Footer Menu

### Creating Footer Menu
1. Go to Appearance → Menus
2. Create new menu "Footer Menu"
3. Add pages:
   - Privacy Policy
   - Terms of Service
   - Contact
   - About
4. Assign to Footer Menu location

### Menu Styling
```css
.footer-menu {
    display: flex;
    gap: 20px;
}
```

## Social Links in Footer

### Adding Social Icons
1. Use Social Links Widget
2. Or add Custom HTML:
```html
<div class="footer-social">
    <a href="#" class="social-facebook">
        <i class="fab fa-facebook"></i>
    </a>
    <a href="#" class="social-twitter">
        <i class="fab fa-twitter"></i>
    </a>
</div>
```

### Supported Networks
- Facebook
- Twitter/X
- Instagram
- LinkedIn
- YouTube
- TikTok
- Discord
- GitHub

## Advanced Footer Features

### Sticky Footer
```css
.site-footer {
    position: sticky;
    bottom: 0;
}
```

### Back to Top Button
**Location:** Customize → General → Scroll to Top
- Enable/Disable
- Position: Left/Right
- Style: Circle/Square
- Offset from bottom

### Footer Scripts
**Location:** Customize → General → Custom Code → Footer
- Analytics codes
- Chat widgets
- Custom JavaScript

## Footer for Different Pages

### Page-Specific Footers
Control footer per page type:
- Homepage Footer
- Blog Footer
- Shop Footer
- BuddyPress Footer

### Conditional Display
Hide footer on specific pages:
```php
add_filter('reign_show_footer', function($show) {
    if (is_page('landing')) {
        return false;
    }
    return $show;
});
```

## Mobile Footer

### Responsive Settings
- Stack widgets on mobile
- Hide certain widgets
- Adjust spacing
- Simplify menu

### Mobile-Only Footer
Create separate mobile footer:
```css
@media (max-width: 768px) {
    .footer-desktop { display: none; }
    .footer-mobile { display: block; }
}
```

## Performance Optimization

1. **Lazy Load Images** - Footer logos/images
2. **Minify CSS** - Footer styles
3. **Async Scripts** - Footer JavaScript
4. **Reduce Widgets** - Limit to essentials
5. **Optimize Icons** - Use icon fonts

## Best Practices

1. **Keep It Simple** - Don't overload footer
2. **Important Links** - Privacy, Terms, Contact
3. **Consistent Design** - Match site style
4. **Mobile First** - Design for mobile
5. **Accessibility** - Proper contrast, links

## Troubleshooting

### Footer Not Showing
- Check page template
- Verify footer enabled
- Clear cache
- Check child theme

### Widgets Not Appearing
- Add widgets to areas
- Check widget visibility
- Verify responsive settings
- Test in different browsers

### Copyright Not Updating
- Use dynamic variables
- Clear cache
- Check PHP version
- Verify theme updates