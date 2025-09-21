# Reign LifterLMS Addon Documentation

## Overview
Reign LifterLMS Addon integrates LifterLMS with Reign theme, adding 2 custom shortcodes and extensive BuddyPress activity integration.

## Requirements
- WordPress 5.0+
- Reign Theme
- LifterLMS Plugin
- BuddyPress (optional)

## Installation
1. Upload `reign-lifterlms-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Configure in Reign Settings → LifterLMS

## Features

### Custom Shortcodes

#### [reign_lifterlms_courses]
Display courses with customizable layout.

**Parameters:**
- `posts_per_page` - Number of courses (default: -1)
- `per_row` - Courses per row (default: '3')
- `enable_slider` - Enable carousel (default: false)
- `id` - Specific course IDs (comma-separated)
- `category` - Course categories
- `membership` - Membership association

**Example:**
```
[reign_lifterlms_courses per_row="4" posts_per_page="12"]
[reign_lifterlms_courses id="1,2,3" enable_slider="true"]
```

#### [reign_lifterlms_instructors]
Display instructor listings.

**Parameters:**
- `per_row` - Instructors per row (default: '4')
- `total` - Limit number (default: false)
- `enable_slider` - Enable carousel (default: false)

**Example:**
```
[reign_lifterlms_instructors per_row="3" total="6"]
```

### BuddyPress Integration
- Adds courses tab to profiles
- Group course associations
- Activity stream tracking
- Favorite courses

### Activity Tracking
- Course enrollment
- Lesson completion
- Topic completion
- Course completion
- Quiz completion
- Comments on lessons/courses

## LifterLMS Core Shortcodes

These come from LifterLMS (NOT Reign addon):
- `[lifterlms_courses]`
- `[lifterlms_my_courses]`
- `[lifterlms_checkout]`
- `[lifterlms_my_account]`

## Developer Reference

### Plugin Structure
```
reign-lifterlms-addon/
├── admin/
├── buddypress/
├── core/
│   ├── class-reign-lifterlms-course-shortcode.php
│   └── class-reign-lifterlms-instructor-shortcode.php
└── reign-lifterlms-addon.php
```

### Hooks & Filters

#### Actions
```php
// After activity registration
do_action('reign_bp_lifterlms_after_register_activity_actions');
```

#### Filters
```php
// Activity text filters
apply_filters('reign_bp_ld_action_start_course_text', 'Started a course');
apply_filters('reign_bp_ld_action_lesson_complete_text', 'Completed a lesson');
apply_filters('reign_bp_ld_action_topic_complete_text', 'Completed a topic');
apply_filters('reign_bp_ld_action_course_complete_text', 'Completed a course');
apply_filters('reign_bp_ld_action_quiz_complete_text', 'Completed a quiz');
apply_filters('reign_bp_ld_action_lesson_comment_text', 'Lesson comment');
apply_filters('reign_bp_ld_action_course_comment_text', 'Course comment');

// Activity formatting
apply_filters('reign_llms_addon_format_course_enrolled_activity', $action, $activity);
apply_filters('reign_llms_addon_format_completed_lesson', $action, $activity);
apply_filters('reign_llms_addon_format_completed_topic', $action, $activity);
apply_filters('reign_llms_addon_format_completed_course', $action, $activity);
apply_filters('reign_llms_addon_format_completed_quiz', $action, $activity);
apply_filters('reign_llms_addon_format_lesson_comment', $action, $activity);
apply_filters('reign_llms_addon_action_course_comment', $action, $activity);

// Settings filter
apply_filters('reign_lifter_options_activity_settings_list', $settings);
```

### Code Examples

#### Customize Activity Text
```php
add_filter('reign_bp_ld_action_course_complete_text', function() {
    return __('Successfully completed course', 'textdomain');
});
```

#### Format Activity Display
```php
add_filter('reign_llms_addon_format_course_enrolled_activity', function($action, $activity) {
    // Customize activity display
    return $action;
}, 10, 2);
```

## Configuration

### Admin Settings
Located in: Reign Settings → LifterLMS
- BuddyPress integration options
- Activity stream settings
- Profile tab configuration

## Important Notes
- Only 2 custom shortcodes (not more)
- Heavy focus on BuddyPress activities
- Group course functionality available
- Instructor display requires users with courses