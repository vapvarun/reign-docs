# Reign TutorLMS Addon Documentation

## Overview
Reign TutorLMS Addon enhances TutorLMS integration with Reign theme, adding 2 custom shortcodes, profile detection, and filter fixes.

## Requirements
- WordPress 5.0+
- Reign Theme
- TutorLMS Plugin
- BuddyPress or PeepSo (optional)

## Installation
1. Upload `reign-tutorlms-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Works automatically with profile detection

## Features

### Custom Shortcodes

#### [reign_tutor_course]
Enhanced course display with smart profile detection.

**Features:**
- Auto-detects BuddyPress/PeepSo profiles
- Adjusts columns in profile context (2 vs 3)
- Progress tracking for enrolled courses
- Inherits TutorLMS course parameters

**Example:**
```
[reign_tutor_course]
```

**Smart Detection:**
- In profiles: 2 columns
- Elsewhere: 3 columns

#### [reign_course_categories]
Display course categories in grid.

**Parameters:**
- `count` - Number to show (default: '8')
- `columns` - Per row (default: '4')
- `orderby` - Sort by (default: 'name')
- `order` - ASC/DESC (default: 'ASC')
- `show_count` - Show course count (default: 'yes')
- `show_image` - Show image (default: 'yes')
- `hide_empty` - Hide empty (default: 'yes')

**Example:**
```
[reign_course_categories count="12" columns="3" show_count="yes"]
```

### Special Features

#### Profile Context Detection
Automatically detects:
- BuddyPress profiles
- PeepSo profiles (via URL patterns)
- Adjusts layout accordingly

#### TutorLMS Filter Fixes
Fixes missing hidden fields:
- `#course_filter_categories`
- `#course_filter_exclude_ids`
- `#course_filter_post_ids`

#### AJAX Progress Loading
- Loads course progress dynamically
- Nonce-secured AJAX calls
- Shows completion percentage

## TutorLMS Core Shortcodes

These come from TutorLMS (NOT Reign addon):
- `[tutor_dashboard]`
- `[tutor_instructor_list]`
- `[tutor_student_registration_form]`
- `[tutor_course]`

## Developer Reference

### Plugin Structure
```
reign-tutorlms-addon/
├── admin/
├── includes/
│   └── reign-tutor-lms-functions.php
└── reign-tutorlms-addon.php
```

### Hooks & Filters

#### Filters
```php
// Settings fields
apply_filters('reign_tutorlms_settings_fields', $fields);

// Default columns
apply_filters('reign_tutorlms_default_columns', $columns, $is_profile, $atts);
```

### AJAX Handlers
```php
// Get course progress
wp_ajax_reign_tutorlms_get_progress
wp_ajax_nopriv_reign_tutorlms_get_progress
```

### Code Examples

#### Customize Default Columns
```php
add_filter('reign_tutorlms_default_columns', function($cols, $is_profile) {
    return $is_profile ? 2 : 4;
}, 10, 2);
```

#### Access Progress Data
```javascript
jQuery.post(reign_tutorlms_ajax.ajax_url, {
    action: 'reign_tutorlms_get_progress',
    nonce: reign_tutorlms_ajax.nonce,
    course_ids: [1, 2, 3],
    user_id: 123
});
```

## Filter Fix Implementation

The addon automatically adds missing fields:
```javascript
// Added if missing
<input type="hidden" id="course_filter_categories" value="[]" />
<input type="hidden" id="course_filter_exclude_ids" value="[]" />
<input type="hidden" id="course_filter_post_ids" value="[]" />
```

## CSS Classes

### Course Progress
```css
.tutor-course-progress.reign-course-progress
.tutor-progress-bar
.tutor-progress-value
```

### Navigation Icon
```css
.reign-nav-iconic #tutorlms-courses-personal-li > a:before {
    content: "\f19d"; /* Graduation cap */
}
```

## Important Notes
- Only 2 custom shortcodes
- Smart profile detection is automatic
- Filter fixes prevent JavaScript errors
- Progress requires user enrollment

## Common Issues

### Filters not working
- Addon adds missing fields automatically
- Check JavaScript console for errors
- Clear cache

### Progress not showing
- User must be enrolled
- Check AJAX nonce
- Verify user permissions

### Profile detection failing
- Check BuddyPress/PeepSo active
- Verify URL structure
- Clear permalinks