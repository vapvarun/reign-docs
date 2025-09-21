# Reign Dokan Addon - Professional Marketplace Integration

## Overview

Reign Dokan Addon seamlessly integrates Dokan with the Reign theme, providing enhanced marketplace functionality with beautiful layouts and improved vendor management.

**Version:** 3.5.4  
**Author:** Wbcom Designs  
**Compatibility:** Tested up to WordPress 6.6.2

## Key Features

### Store Listing Layouts

**Two Professional Layout Options:**

#### 1. Grid Layout
- Modern card-based store display
- Visual store previews
- Featured vendor highlighting
- Responsive columns
- Quick store access

#### 2. List Layout  
- Detailed store information
- Extended vendor details
- Product previews
- Store ratings display
- Comprehensive vendor info

### Template Files Included

The addon provides custom template files that override default Dokan templates:

- `store.php` - Single store page template
- `store-header.php` - Custom store header with enhanced branding (7.8KB enhanced version)
- `store-lists.php` - Store listing page
- `store-lists-loop.php` - Store listing loop with Reign styling (9KB custom code)
- `store-reviews.php` - Enhanced review display
- `store-sidebar.php` - Store sidebar widgets
- `store-toc.php` - Store table of contents
- `vendor-biography.php` - Vendor bio section

## Integration Features

### Enhanced Store Header
The custom `store-header.php` (7.8KB) provides:
- Professional vendor branding
- Store banner customization
- Social media links
- Store statistics display
- Contact information

### Improved Store Lists Loop
The `store-lists-loop.php` (9KB) includes:
- Advanced filtering options
- Sorting capabilities
- Pagination improvements
- AJAX loading
- Mobile optimization

### Custom Widgets Support

As documented in "How to set Widgets in reign-dokan-addon":
- Store category widget
- Featured vendors widget
- Top rated stores
- Recent products
- Store search widget

## Service Creation Features

Based on documentation "Create Service using Dokan Dashboard":
- Service product type support
- Booking integration
- Service scheduling
- Duration settings
- Service provider management

## Shortcodes Available

From "Available Shortcodes for StoreMate Dokan":
- `[dokan-stores]` - Display store listings
- `[dokan-best-selling-product]` - Best selling products
- `[dokan-vendor-dashboard]` - Vendor dashboard
- `[dokan-new-product]` - Latest products
- Custom Reign-enhanced shortcodes for layouts

## Filters for Customization

As per "Filters for StoreMate Dokan":
- `dokan_get_template_part` - Template part filtering
- `dokan_locate_template` - Template location override
- `reign_dokan_store_layout` - Layout selection
- `reign_dokan_grid_columns` - Grid column control
- Additional Reign-specific filters

## Installation & Setup

### Requirements
- WordPress 4.0 or higher
- Reign Theme activated
- Dokan plugin (Lite or Pro)
- PHP 7.2+

### Installation Steps
1. Upload plugin to `/wp-content/plugins/`
2. Activate through WordPress admin
3. Configure settings in Customizer
4. Set up widgets if needed

### License Activation
The addon integrates with Reign theme license panel:
- Navigate to Reign > License
- Find "Reign Dokan Addon" section
- Enter your license key
- Activate for updates

## Customizer Options

### Store Listing Settings
- Layout selection (Grid/List)
- Columns per row (2-4)
- Items per page
- Sidebar position
- Show/hide elements

### Single Store Settings
- Header style
- Tab arrangement
- Product display
- Review settings
- Contact form display

## Performance Optimizations

- Template caching
- Lazy loading for store images
- AJAX pagination
- Minified CSS/JS
- Database query optimization

## Developer Features

### Hooks Available
```php
// Action hooks
do_action('reign_dokan_before_store_loop');
do_action('reign_dokan_after_store_header');
do_action('reign_dokan_store_sidebar');

// Filter hooks  
add_filter('reign_dokan_store_layout', 'custom_layout');
add_filter('reign_dokan_grid_columns', 'custom_columns');
```

### Template Override
You can override templates in your child theme:
```
reign-child/
├── dokan/
│   ├── store.php
│   ├── store-header.php
│   └── store-lists.php
```

## Compatibility

### Tested With
- Dokan Lite & Pro
- WooCommerce 8.0+
- BuddyPress integration
- bbPress forums
- Popular cache plugins
- SEO plugins

## Support & Updates

- Regular updates for compatibility
- Premium support included
- Documentation available
- Active development
- Community forum access

## Changelog Highlights

**Version 3.5.4**
- WordPress 6.6.2 compatibility
- Performance improvements
- Bug fixes

**Previous Updates**
- Enhanced store header design
- Added list layout option
- Mobile responsiveness improvements
- Widget additions
- Filter enhancements

## Get Started

Transform your Dokan marketplace with professional layouts and enhanced functionality designed specifically for the Reign theme.

[Download Reign Dokan Addon →](https://wbcomdesigns.com/downloads/reign-dokan-addon/)

---

*Part of the Reign ecosystem - Premium WordPress solutions by Wbcom Designs*