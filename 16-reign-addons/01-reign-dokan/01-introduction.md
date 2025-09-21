# Reign Dokan Addon - Introduction

## What is Reign Dokan Addon?

Reign Dokan Addon v3.5.4 is a premium WordPress plugin that integrates Dokan multivendor marketplace with the Reign theme, providing professional store layouts, custom shortcodes, and BuddyPress social features.

## Key Features (Verified)

### Template Enhancements
- Professional store page layouts
- Enhanced store headers with layout controls
- Custom vendor product displays
- Mobile-optimized store templates
- Template override system for customization

### Custom Shortcodes
- **[rda_dokan_vendors]** - Display vendor listings with layout options
- **[rda_dokan_store_listing]** - Show searchable store listings with pagination

### BuddyPress Integration
- Vendor store tabs in user profiles
- Favorite products functionality
- Activity stream integration for reviews
- Social marketplace features

### Configuration Options
- Store header display controls
- Vendor product showcase settings
- "Sold by" vendor attribution
- Layout width controls (fullwidth/contained)
- Products per page settings

## Technical Specifications

| Specification | Details |
|--------------|----------|
| **Version** | 3.5.4 |
| **WordPress** | 4.0+ |
| **Required Theme** | Reign Theme |
| **Required Plugin** | Dokan + WooCommerce |
| **Optional** | BuddyPress (for social features) |

## Actual Plugin Structure

```
reign-dokan-addon/
├── admin/
│   ├── class-reign-dokan-admin-settings.php
│   └── reign-dokan-vertical-tabs-skeleton.php
├── assets/
│   ├── css/
│   ├── images/
│   └── js/
├── buddypress/
│   ├── class-reign-dokan-buddypress-addon.php
│   ├── class-reign-dokan-favourite-product-profile-tab.php
│   └── reign-dokan-activity.php
├── core/
│   ├── class-reign-dokan-favourite-product.php
│   ├── class-reign-dokan-single-product.php
│   ├── class-reign-dokan-theme-hooks.php
│   └── reign-dokan-functions.php
├── dokan/                              # Template overrides
│   ├── orders/
│   ├── products/
│   ├── review/
│   ├── store-header.php
│   ├── store-lists.php
│   ├── store-lists-loop.php
│   ├── store.php
│   └── [other template files]
├── edd-license/                        # License management
├── languages/
├── rda-shortcodes/
│   └── class-reign-dokan-shortcodes.php
├── rda-widgets/
├── reign-dokan-addon.php              # Main plugin file
└── readme.txt
```

## Requirements

### Essential Prerequisites
1. **Reign Theme** (Active theme)
2. **Dokan Plugin** (Free or Pro)
3. **WooCommerce** (Required by Dokan)

### Optional (For Enhanced Features)
1. **BuddyPress** - Enables social marketplace features

## What This Addon Provides

### Verified Theme Settings
- `reign_dokan_store_header_location` - Control store header display
- `reign_dokan_store_header_layout` - Set header width (fullwidth/contained)
- `reign_dokan_show_vendor_pros_on_pro_page` - Show vendor products on product pages
- `reign_dokan_num_of_vendor_pros_on_pro_page` - Number of products to display
- `reign_dokan_show_sold_by_in_pro_meta` - Display "Sold by" vendor info

### Available Hooks & Filters
- `reign_dokan_addon_loaded` - Plugin initialization
- `dokan_get_template_part` - Template override system
- `rda_dokan_seller_listing_args` - Customize vendor queries
- `rda_dokan_store_list_args` - Modify store listing arguments

### Template System
Override any template by copying from plugin to theme:
```
Plugin: /wp-content/plugins/reign-dokan-addon/dokan/store.php
Theme:  /wp-content/themes/your-theme/dokan/store.php
```

## Use Cases

### Professional Marketplaces
- Multi-vendor eCommerce stores
- Digital product marketplaces
- Service provider platforms
- B2B wholesale platforms

### Community-Driven Commerce
- Local business directories with BuddyPress
- Social shopping experiences
- Vendor community building

## Quick Start

1. Install Reign Theme + Dokan + WooCommerce
2. Install and activate Reign Dokan Addon
3. Configure settings at **Appearance → Customize → Dokan Settings**
4. Add shortcodes to display vendors/stores
5. Customize templates if needed

## Next Steps

- [Installation & Setup](02-installation-setup.md) - Detailed installation guide
- [Configuration](03-configuration.md) - All available settings
- [Store Customization](04-store-customization.md) - Template customization
- [Developer Guide](05-developer-guide.md) - Hooks and filters
- [Shortcodes Reference](07-shortcodes-reference.md) - Complete shortcode guide

---

*Introduction updated based on Reign Dokan Addon v3.5.4 source code verification*