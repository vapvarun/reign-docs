# Reign LearnDash Addon Documentation

## Overview
Reign LearnDash Addon integrates LearnDash LMS with Reign theme, adding 6 custom shortcodes and extensive BuddyPress/PeepSo integration.

## Requirements
- WordPress 5.0+
- Reign Theme
- LearnDash LMS Plugin
- BuddyPress or PeepSo (optional)

## Installation
1. Upload `reign-learndash-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Configure in Reign Settings → LearnDash

## Features

### Custom Shortcodes (Verified from Code)

#### [modern_courses] / [reign_courses]
Display courses in modern grid layout.

**Parameters:**
- `per_page` - Courses per page (default: -1)
- `cols` - Columns (default: 3)
- `display_all` - Show all courses (default: false)
- `enrolled_only` - Show only enrolled (default: false)
- `in_progress_only` - Show only in progress (default: false)

**Example:**
```
[modern_courses per_page="12" cols="4"]
[reign_courses enrolled_only="true" cols="3"]
```

#### [modern_groups]
Display LearnDash groups in modern layout.

**Example:**
```
[modern_groups]
```

#### [reign_ld_pro_comments_tab_content]
Display course comments tab content for profiles.

#### [reign_ld_pro_instructor_tab_content]
Display instructor tab content for profiles.

#### [reign_ld_pro_course_content_tab_content]
Display course content tab for profiles.

### Social Integration

#### BuddyPress Features
- Course tab in user profiles
- Group course associations
- Activity stream for course activities
- Course completion tracking

#### PeepSo Features
- Course profile sections
- Activity stream integration
- Course progress display

### Activity Tracking
- Course enrollment
- Lesson completion
- Quiz completion
- Certificate earning
- Course comments

## LearnDash Core Shortcodes

These come from LearnDash (NOT Reign addon):
- `[ld_course_list]` - Course listing
- `[learndash_course_progress]` - Progress bar
- `[ld_profile]` - User profile
- `[ld_course_info]` - Course information

## Developer Reference

### Plugin Structure
```
reign-learndash-addon/
├── admin/
├── assets/
├── buddypress/
├── inc/
├── peepso/
├── public/
└── reign-learndash-addon.php
```

### Hooks & Filters

#### Actions
```php
// After settings update
do_action('reign_ld_pro_after_settings_update', $settings);

// Activity actions
do_action('reign_ld_pro_after_course_enrollment', $course_id, $user_id);
do_action('reign_ld_pro_after_lesson_completion', $lesson_id, $user_id);
```

#### Filters
```php
// Course grid columns
apply_filters('reign_ld_pro_course_grid_columns', 3);

// Activity text
apply_filters('reign_ld_pro_activity_course_enrolled', $text);
apply_filters('reign_ld_pro_activity_lesson_completed', $text);

// Tab names
apply_filters('reign_ld_pro_courses_tab_name', 'Courses');
apply_filters('reign_ld_pro_certificates_tab_name', 'Certificates');
```

### Code Examples

#### Customize Grid Columns
```php
add_filter('reign_ld_pro_course_grid_columns', function() {
    return 4; // 4 columns
});
```

#### Modify Tab Names
```php
add_filter('reign_ld_pro_courses_tab_name', function() {
    return __('My Learning', 'textdomain');
});
```

#### Custom Activity Text
```php
add_filter('reign_ld_pro_activity_course_enrolled', function($text) {
    return __('just started learning', 'textdomain');
});
```

## Configuration

### Theme Settings
Available in Customizer → Reign Settings → LearnDash:
- Enable/disable profile tabs
- Activity stream settings
- Course display options
- Group integration settings

### Database Options
Settings stored as:
- `reign_learndash_addon_options`
- `reign_ld_pro_bp_integration`

## Important Notes
- Only 6 custom shortcodes (not 18+ as incorrectly documented before)
- `[modern_courses]` and `[reign_courses]` are aliases
- Heavy focus on social platform integration
- Activity tracking requires BuddyPress/PeepSo

## Common Issues

### Shortcodes not working
- Verify LearnDash is active
- Check shortcode spelling
- Confirm courses exist

### Profile tabs missing
- Enable in Reign Settings
- Check BuddyPress/PeepSo active
- User must have course activity

### Activities not posting
- Check activity settings
- Verify BP/PS components active
- Clear cache