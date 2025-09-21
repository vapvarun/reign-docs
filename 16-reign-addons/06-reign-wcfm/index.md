# Reign WCFM Addon Documentation

## Overview
Reign WCFM Addon enhances WCFM Marketplace integration with Reign theme through BuddyPress integration, activity streams, and styling - **WITHOUT adding any custom shortcodes**.

## Requirements
- WordPress 4.0+
- Reign Theme
- WCFM Marketplace Plugin
- WooCommerce
- BuddyPress (optional)

## Installation
1. Upload `reign-wcfm-addon` to `/wp-content/plugins/`
2. Activate plugin
3. BuddyPress features activate automatically if BP is active

## Features

### NO Custom Shortcodes
**Important:** This addon adds NO shortcodes. All shortcodes come from WCFM core plugin.

### BuddyPress Integration
- Adds "Store" tab to user profiles
- Shows vendor products in profile
- Displays favorite products
- Activity stream integration

### Activity Stream Support
- Posts when products are created
- Posts for product reviews
- Formatted activity content

### Template & Styling
- Enhanced WCFM element styling
- Responsive design improvements
- Reign theme integration

## WCFM Core Shortcodes

Use these WCFM plugin shortcodes (styled by Reign):
- `[wcfm_stores]` - Store listings
- `[wcfm_store_info]` - Store information
- `[wcfm_inquiry]` - Inquiry form
- `[wcfm_follow]` - Follow button

## Developer Reference

### Hooks & Filters

#### Filters
```php
// Format product review activity
apply_filters('reign_wcfm_format_activity_action_product_review', $action, $activity);

// Format product creation activity
apply_filters('reign_wcfm_format_activity_action_product_create', $action, $activity);

// Customize tab names
apply_filters('reign_wcfm_favourite_product_tab_name', 'Favorites');
apply_filters('reign_wcfm_vendor_store_tab_name', 'Store');

// Tab slugs
apply_filters('reign_wcfm_favourite_product_tab_slug', 'favorites');
apply_filters('reign_wcfm_vendor_store_tab_slug', 'store');

// Posts per page (note: uses 'dokan' prefix)
apply_filters('reign_dokan_fav_product_bp_tab_posts_per_page', 10);
```

### Code Examples

#### Customize Tab Names
```php
add_filter('reign_wcfm_vendor_store_tab_name', function() {
    return __('My Shop', 'textdomain');
});

add_filter('reign_wcfm_favourite_product_tab_name', function() {
    return __('Wishlist', 'textdomain');
});
```

#### Format Activities
```php
add_filter('reign_wcfm_format_activity_action_product_review', function($action, $activity) {
    // Customize activity text
    return $action;
}, 10, 2);
```

## Common Issues

### WCFM shortcodes not working
- Verify WCFM Marketplace is active
- Check WooCommerce is installed
- Confirm WCFM license

### BuddyPress tabs missing
- Ensure BuddyPress is active
- Check user is vendor
- Clear cache

## Important Notes
- All vendor functionality comes from WCFM core
- This addon provides integration and styling only
- No custom shortcodes are added
- Focus is on social integration