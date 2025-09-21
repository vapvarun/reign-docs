# Reign WCFM Addon - Introduction

## What is Reign WCFM Addon?

Reign WCFM Addon v1.8.3 integrates WCFM Marketplace with the Reign theme, providing enhanced styling, BuddyPress social features, and template customization for multi-vendor marketplaces.

## Core Features (Verified)

### BuddyPress Integration
- **Store Tabs**: Add "Store" tab to vendor profiles showing their products
- **Favourite Products**: Users can mark and view favorite products in profile
- **Activity Streams**: Product creation, reviews, and orders appear in feeds
- **Social Marketplace**: Enhanced social features when BuddyPress is active

### Theme Integration
- **Styling Enhancement**: WCFM elements styled to match Reign theme
- **Store Layouts**: 2 store layout options (Layout 1 and Layout 2)
- **Template Override System**: Custom templates for enhanced appearance
- **Responsive Design**: Mobile-optimized store displays

### Activity Management
- **Product Activities**: Create activities when vendors add products
- **Review Activities**: Generate activities for product reviews
- **Order Activities**: Show purchase activities in feeds
- **Customizable**: Each activity type can be enabled/disabled

## Technical Requirements

| Requirement | Details |
|-------------|---------|
| **Version** | 1.8.3 |
| **WordPress** | 4.0+ |
| **Reign Theme** | Required (active) |
| **WooCommerce** | Required |
| **WCFM** | Required |
| **BuddyPress** | Optional (for social features) |

## What This Addon Provides

### Template Enhancements
- Enhanced store page layouts
- Professional store displays
- Custom store templates
- Mobile-responsive design

### Settings Available
- Mark Products As Favourite (enable/disable)
- Display Store Tab (BuddyPress vendor profiles)
- Create Product Activity (activity streams)
- Add Review Activity (review activities)
- Order Activity (purchase activities)
- Single Store Layout (Layout 1 or Layout 2)

### Developer Features
- Template override system
- Custom hooks and filters
- BuddyPress integration APIs
- Activity stream customization

## Plugin Structure (Verified)

```
reign-wcfm-addon/
├── admin/                  # Admin settings and license
├── public/                 # Public-facing functionality
│   ├── css/               # Styling files
│   ├── js/                # JavaScript files
│   └── buddypress/        # BuddyPress integration
├── templates/             # Template overrides
└── reign-wcfm-addon.php  # Main plugin file
```

## Next Steps

1. [Installation Guide](02-installation-setup.md)
2. [Configuration Guide](03-configuration.md)
3. [Store Customization](04-store-customization.md)
4. [Developer Guide](05-developer-guide.md)