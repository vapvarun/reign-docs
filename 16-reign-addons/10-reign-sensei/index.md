# Reign Sensei Addon Documentation

## Overview
Reign Sensei Addon integrates Sensei LMS with Reign theme through BuddyPress group courses and course reviews - **WITHOUT adding any custom shortcodes**.

## Requirements
- WordPress 5.0+
- Reign Theme
- Sensei LMS Plugin
- BuddyPress (required for main features)

## Installation
1. Upload `reign-sensei-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Configure in Reign Settings → Sensei

## Features

### NO Custom Shortcodes
**Important:** This addon adds NO shortcodes. All shortcodes come from Sensei LMS plugin.

### BuddyPress Group Integration
- Adds "Courses" tab to BuddyPress groups
- Group admins can associate courses
- Members access group courses
- Group-specific course management

### Course Review System
- Star rating for courses
- Review comments
- Review display templates
- Rating aggregation

### Activity Stream Integration
- Course enrollment activities
- Course completion activities
- Lesson activities
- Review activities

## Sensei Core Shortcodes

Use these Sensei plugin shortcodes (styled by Reign):
- `[sensei_courses]` - Course listing
- `[sensei_lessons]` - Lesson listing
- `[sensei_user_courses]` - User's courses
- `[sensei_featured_courses]` - Featured courses
- `[sensei_course_categories]` - Categories

## Developer Reference

### Plugin Structure
```
reign-sensei-addon/
├── admin/
├── buddypress/
│   └── class-reign-sensei-bp-group-add-course.php
├── course-review/
│   ├── review.php
│   └── review-rating.php
└── reign-sensei-addon.php
```

### Hooks & Filters

#### Filters
```php
// Admin settings
apply_filters('wbtm_[slug]_vertical_tabs', $tabs);
apply_filters('get_default_reign_sensei_activity_content', $content);

// Group integration
apply_filters('reign_sensei_courses_group_tab_name', 'Courses');

// Reviews
apply_filters('wb_ld_course_get_star_rating_html', $html, $rating, $count);
```

#### Actions
```php
// Group screens
do_action('reign_sensei_group_admin_screen_before_save', $group_id);
do_action('reign_sensei_group_admin_screen_after_save', $group_id);
do_action('reign_sensei_before_courses_page_content');
do_action('reign_sensei_after_courses_page_content');
do_action('reign_sensei_create_group_screen_before_save', $group_id);
do_action('reign_sensei_create_group_screen_after_save', $group_id);
do_action('reign_sensei_group_manage_screen_before_save', $group_id);
do_action('reign_sensei_group_manage_screen_after_save', $group_id);

// Reviews
do_action('reign_sensei_course_review_before', $comment);
do_action('reign_sensei_course_review_meta', $comment);
do_action('reign_sensei_course_review_before_comment_meta', $comment);
```

### Code Examples

#### Customize Group Tab Name
```php
add_filter('reign_sensei_courses_group_tab_name', function() {
    return __('Learning', 'textdomain');
});
```

#### Modify Activity Content
```php
add_filter('get_default_reign_sensei_activity_content', function($content) {
    // Customize default activity text
    return $content;
});
```

#### Customize Star Rating Display
```php
add_filter('wb_ld_course_get_star_rating_html', function($html, $rating, $count) {
    // Customize rating HTML
    return $html;
}, 10, 3);
```

#### Hook Into Group Save
```php
add_action('reign_sensei_group_admin_screen_after_save', function($group_id) {
    // Custom actions after group course save
});
```

## Group Course Management

### For Group Admins
1. Navigate to group admin
2. Select "Courses" tab
3. Associate courses with group
4. Save settings

### For Members
1. Visit group
2. Click "Courses" tab
3. Access group courses

## Course Reviews

### Review Components
- 5-star rating system
- Written review text
- Review metadata
- Author information

### Display Templates
- Review listing
- Individual review
- Rating summary
- Review form

## Activity Stream

### Activity Types
- Course enrollment
- Course completion
- Lesson completion
- Course reviews

### Activity Privacy
- Respects BuddyPress privacy settings
- Group activities in group context
- User activities in profiles

## Important Notes
- NO custom shortcodes added
- Requires BuddyPress for main features
- All course functionality from Sensei
- Focus on social learning aspects

## Common Issues

### Group tab not showing
- Verify BuddyPress active
- Check group component enabled
- Confirm user permissions

### Reviews not displaying
- Enable course reviews in settings
- Check template overrides
- Clear cache

### Activities not posting
- Verify activity component active
- Check activity settings
- Confirm user permissions