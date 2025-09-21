# Reign WCFM Addon - Store Customization

## Overview

The Reign WCFM Addon provides basic store customization through layout options and template overrides. This addon focuses on styling integration rather than extensive customization features.

## Available Customization Options

### Store Layout Options

The addon provides 2 store layout options:

1. **Layout 1** - Default store layout
2. **Layout 2** - Alternative store layout design

**To change layout:**
1. Go to Reign Settings → WCFM
2. Under Store Settings
3. Select "Single Store Layout"
4. Choose Layout 1 or Layout 2
5. Save settings

### Template Customization

#### Override System
Copy templates from plugin to theme for safe customization:

**Source Location:**
```
/wp-content/plugins/reign-wcfm-addon/templates/
```

**Target Location:**
```
/wp-content/themes/your-theme/wcfm/
```

#### Available Templates
- Store header layouts
- Store listing displays
- Store detail pages
- Custom store templates

### Styling Enhancements

The addon automatically applies Reign theme styling to:
- WCFM store pages
- Vendor dashboards
- Store listings
- Product displays

### BuddyPress Integration Styling

When BuddyPress is active, the addon styles:
- Store tabs in user profiles
- Favorite products displays
- Activity stream items
- Social marketplace elements

## Customization Examples

### Basic Layout Switch
Change all stores to use Layout 2:
```
Reign Settings → WCFM → Store Settings → Layout 2
```

### Template Override
Copy and customize store header:
```
Copy: reign-wcfm-addon/templates/store-header.php
To: your-theme/wcfm/store-header.php
```

### Custom CSS
Add custom styling for stores:
```css
/* Custom store styling */
.wcfm-store-wrapper.layout_two {
    /* Custom layout 2 styles */
}
```

## Limitations

The Reign WCFM addon is primarily a styling integration addon and does not provide:
- Advanced store customization tools
- Layout builders
- Color pickers
- Font customization
- Complex design options

For advanced store customization, these features would need to come from:
- WCFM core plugin settings
- Custom theme development
- Additional WCFM plugins

---

*Store customization guide verified against Reign WCFM Addon v1.8.3 source code*