# Reign GeoDirectory Addon Documentation

## Overview
Reign GeoDirectory Addon provides social platform integration for GeoDirectory, supporting BOTH BuddyPress and PeepSo - **WITHOUT adding any custom shortcodes**.

## Requirements
- WordPress 5.0+
- Reign Theme
- GeoDirectory Plugin
- BuddyPress OR PeepSo (at least one required)

## Installation
1. Upload `reign-geodirectory` to `/wp-content/plugins/`
2. Activate plugin
3. Configure in Reign Settings → GeoDirectory

## Features

### NO Custom Shortcodes
**Important:** This addon adds NO shortcodes. All shortcodes come from GeoDirectory plugin.

### Dual Platform Support
Unique feature: Works with BOTH BuddyPress AND PeepSo.

### BuddyPress Integration

#### Profile Features
- Adds "Places" tab to profiles
- Shows user's listed places
- Displays favorite places
- Tracks location activities

#### Notifications
- Location addition notifications
- Favorite notifications
- Review notifications
- Custom formatted messages

### PeepSo Integration

#### Activity Stream
- Location creation activities
- Review activities
- Favorite place activities
- User permission controls

#### Privacy Controls
- User-level activity settings
- Meta-based permissions
- Filterable privacy options

## GeoDirectory Core Shortcodes

Use these GeoDirectory shortcodes (styled by Reign):
- `[gd_listings]` - Location listings
- `[gd_map]` - Map display
- `[gd_categories]` - Categories
- `[gd_search]` - Search form
- `[gd_login_form]` - Login form

## Developer Reference

### Plugin Structure
```
reign-geodirectory/
├── admin/
│   ├── class-reign-buddypress-geodirectory-options.php
│   └── class-reign-peepso-geodirectory-options.php
├── core/
│   ├── class-bp-geodirectory-activities.php
│   ├── class-geodirectory-bp-notifications.php
│   ├── class-bp-geodirectory-places-tab.php
│   ├── class-peepso-geodirectory-activities.php
│   └── class-peepso-geodirectory-places-tab.php
└── reign-geodirectory.php
```

### Hooks & Filters

#### Filters - BuddyPress
```php
// Activity content
apply_filters('filter_geodir_add_location_activity', $content, $location, $member_id);
apply_filters('filter_geodir_add_loction_review_activity', $content, $review, $member_id);
apply_filters('geodir_review_users_lists', $users);

// Notifications
apply_filters('bp_geodir_add_location_notification_format', $format, $location_id, $format_type);
apply_filters('bp_geodir_marked_favorite_notification_format', $format, $member_id, $location_id, $format_type, $notification_id);
apply_filters('bp_geodir_marked_review_notification_format', $format, $member_id, $location_id, $format_type, $notification_id);

// Template
apply_filters('bp_core_template_plugin', $template);
```

#### Filters - PeepSo
```php
// Activity permissions
apply_filters('alter_peepso_geodirectory_activity_allowed_by_user', $allowed, $setting_key, $user_id);

// Activity content
apply_filters('filter_geodir_add_loction_review_activity', $content, $location, $user_id);

// Rating label
apply_filters('geodir_overall_rating_label', $label);
```

#### Actions
```php
// Theme options rendering
do_action('render_theme_options_for_[key]');
```

### Code Examples

#### Customize Activity Content
```php
// BuddyPress activity
add_filter('filter_geodir_add_location_activity', function($content, $location, $member_id) {
    // Modify activity content
    return $content;
}, 10, 3);
```

#### Modify Notifications
```php
// Custom notification format
add_filter('bp_geodir_add_location_notification_format', function($format, $location_id, $format_type) {
    if ($format_type === 'string') {
        return __('New place added!', 'textdomain');
    }
    return $format;
}, 10, 3);
```

#### PeepSo Permissions
```php
// Control activity permissions
add_filter('alter_peepso_geodirectory_activity_allowed_by_user', function($allowed, $setting, $user_id) {
    // Custom permission logic
    return $allowed;
}, 10, 3);
```

## Configuration

### BuddyPress Settings
Located in: Reign Settings → GeoDirectory → BuddyPress
- Enable/disable activities
- Configure notifications
- Set profile tab options

### PeepSo Settings
Located in: Reign Settings → GeoDirectory → PeepSo
- Activity stream options
- Privacy settings
- Permission controls

## Activity Types

### Tracked Activities
1. **Location Addition** - User adds new place
2. **Reviews** - User reviews location
3. **Favorites** - User favorites place
4. **Updates** - Location updates

### Activity Privacy
- Respects platform privacy settings
- User-controllable permissions
- Filterable at code level

## Notification System

### BuddyPress Notifications
- Real-time notifications
- Formatted messages
- Links to relevant content
- Mark read/unread

### Notification Types
1. Location added
2. Place favorited
3. Review received
4. Location updated

## Important Notes
- NO custom shortcodes added
- Supports BOTH BP and PeepSo
- All location features from GeoDirectory
- Focus entirely on social integration

## Common Issues

### Places tab not showing
- Verify BP/PeepSo active
- Check user has places
- Clear cache

### Activities not posting
- Check activity settings
- Verify permissions
- Ensure components active

### Notifications not working
- Enable in settings
- Check notification component
- Verify user settings