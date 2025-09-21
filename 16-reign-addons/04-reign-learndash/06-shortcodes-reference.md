# Reign LearnDash Addon - Shortcodes Reference

## Overview

This guide provides a complete reference for all shortcodes available in the Reign LearnDash addon, including both standard LearnDash shortcodes and Reign-specific enhancements.

---

## Reign Custom Shortcodes (Verified from Plugin)

These shortcodes are actually implemented in the Reign LearnDash addon plugin:

### 1. [modern_courses] / [reign_courses]

**Modern course display with advanced filtering and templates.**

Both shortcodes are identical - `[reign_courses]` is an alias for `[modern_courses]`.

**Basic Usage:**
```
[modern_courses]
[reign_courses]
```

**Full Parameters:**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 12 | Any number | Courses per page |
| `columns` | 3 | 1-6 | Number of columns in grid |
| `template` | classic | classic, minimal, premium, detailed | Visual template style |
| `view` | grid | grid, list | Layout view type |
| `course_ids` | - | Comma-separated IDs | Specific courses to display |
| `category` | - | Category slug | Filter by category |
| `tag` | - | Tag slug | Filter by tag |
| `instructor` | - | Username or ID | Filter by instructor |
| `instructor_role` | - | Role name | Filter by instructor role |
| `price_type` | all | free, paid, all | Filter by price |
| `enrolled` | all | yes, no, all | Show enrolled/not enrolled |
| `orderby` | date | date, title, menu_order, rand, popularity, rating | Sort method |
| `order` | DESC | ASC, DESC | Sort direction |
| `show_filters` | yes | yes, no | Display filter options |
| `show_search` | yes | yes, no | Display search bar |
| `show_sorting` | yes | yes, no | Display sorting dropdown |
| `show_progress` | yes | yes, no | Show progress bars |
| `show_reviews` | yes | yes, no | Display ratings |
| `progress_min` | - | 0-100 | Minimum progress % |
| `progress_max` | - | 0-100 | Maximum progress % |
| `pagination` | numbers | numbers, load_more, infinite, both, none | Pagination style |

**Examples:**

```
// Display 6 courses in 2 columns
[modern_courses per_page="6" columns="2"]

// Show only free courses with premium template
[modern_courses price_type="free" template="premium"]

// Featured courses by specific instructor
[modern_courses instructor="john-smith" tag="featured" columns="3"]

// Enrolled courses with progress tracking
[modern_courses enrolled="yes" show_progress="yes" orderby="title"]

// Category-specific without filters
[modern_courses category="advanced" show_filters="no" show_search="no"]

// Specific courses in minimal style
[modern_courses course_ids="101,102,103" template="minimal" pagination="none"]
```

**Template Styles:**

- **Classic**: Traditional course card with thumbnail, title, description, price, enrollment count
- **Minimal**: Clean design focusing on title and thumbnail
- **Premium**: Rich visual design with hover effects, instructor avatar, prominent ratings
- **Detailed**: Comprehensive information including full description, lesson count, duration

---

### 2. [modern_groups]

**Modern LearnDash groups display with advanced templates.**

**Basic Usage:**
```
[modern_groups]
```

**Parameters:**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 12 | Any number | Groups per page |
| `columns` | 3 | 1-6 | Number of columns |
| `template` | minimal | minimal, premium, detailed, creative, compact | Visual template |
| `orderby` | date | date, title, menu_order, member_count, course_count | Sort method |
| `order` | DESC | ASC, DESC | Sort direction |
| `show_filters` | yes | yes, no | Display filters |
| `show_search` | yes | yes, no | Display search |
| `show_sorting` | yes | yes, no | Display sorting |
| `show_view_switcher` | yes | yes, no | Grid/list switcher |
| `show_pagination` | yes | yes, no | Display pagination |
| `pagination_type` | numbers | numbers, load_more, infinite | Pagination style |

**Examples:**

```
// Display 8 groups in 4 columns
[modern_groups per_page="8" columns="4"]

// Premium template sorted by member count
[modern_groups template="premium" orderby="member_count"]

// Groups with load more pagination
[modern_groups pagination_type="load_more" show_filters="no"]
```

---

### 3. Course Tab Content Shortcodes

These shortcodes are used to display specific course information, typically within course page tabs:

#### [reign_ld_pro_comments_tab_content]

**Display course comments/discussions.**

```
[reign_ld_pro_comments_tab_content]
```

- Must be used within a course page context
- Displays course comments and discussion threads
- Integrates with WordPress comment system

#### [reign_ld_pro_instructor_tab_content]

**Display instructor information.**

```
[reign_ld_pro_instructor_tab_content]
```

- Shows instructor bio and avatar
- Lists other courses by the same instructor
- Must be used within a course page context

#### [reign_ld_pro_course_content_tab_content]

**Display main course content/curriculum.**

```
[reign_ld_pro_course_content_tab_content course_id="123" user_id="456"]
```

**Parameters:**
- `course_id` - Course ID (uses current if not specified)
- `user_id` - User ID (uses current if not specified)

- Displays course lessons, topics, and quizzes
- Shows progress for enrolled users
- Must be used within a course page context

---

## Standard LearnDash Shortcodes (Work with Reign Theme)

### Essential Course Shortcodes

#### [ld_course_list]
**Display user's enrolled courses:**
```
[ld_course_list]
[ld_course_list status="in_progress"]
[ld_course_list status="completed"]
```

#### [learndash_course_progress]
**Show course progress:**
```
[learndash_course_progress course_id="123"]
[learndash_course_progress course_id="123" user_id="456"]
```

#### [ld_profile]
**Display user learning profile:**
```
[ld_profile]
[ld_profile user_id="456"]
```

#### [learndash_payment_buttons]
**Course payment/enrollment buttons:**
```
[learndash_payment_buttons course_id="123"]
```

### Quiz and Certificate Shortcodes

#### [ld_quiz_list]
**List quizzes:**
```
[ld_quiz_list]
[ld_quiz_list course_id="123"]
```

#### [learndash_course_certificate]
**Display course certificate:**
```
[learndash_course_certificate course_id="123"]
```

### Navigation Shortcodes

#### [course_content]
**Course navigation/outline:**
```
[course_content course_id="123"]
[course_content course_id="123" num="10"]
```

#### [ld_navigation]
**Course navigation menu:**
```
[ld_navigation course_id="123"]
```

### User Dashboard Shortcodes

#### [learndash_user_status]
**User's course status:**
```
[learndash_user_status]
```

#### [ld_user_course_points]
**Display user's points:**
```
[ld_user_course_points]
```

---

## Usage Tips

### Combining Shortcodes

Create rich layouts by combining multiple shortcodes:

```html
<!-- Course catalog page -->
<div class="course-filters">
  [modern_courses show_filters="yes" show_search="yes"]
</div>

<!-- Student dashboard -->
<div class="student-dashboard">
  [ld_profile]
  [modern_courses enrolled="yes" show_progress="yes"]
</div>

<!-- Instructor page -->
<div class="instructor-courses">
  [reign_ld_pro_instructor_tab_content]
  [modern_courses instructor="current" template="detailed"]
</div>
```

### Performance Optimization

1. **Limit results**: Use `per_page` parameter
2. **Use specific filters**: Category/tag filtering is faster than showing all
3. **Enable caching**: Works with object caching plugins
4. **Optimize images**: Ensure course thumbnails are optimized

### Styling

All Reign shortcodes include CSS classes for customization:

```css
.reign-courses-container { }
.reign-courses-grid { }
.reign-course-card { }
.reign-course-{template} { }
.reign-columns-{number} { }
.modern-groups-container { }
.modern-group-card { }
```

---

## Troubleshooting

### Shortcode not working
- Ensure Reign LearnDash addon is active
- Check for typos in shortcode name
- Verify parameters are valid
- Clear cache if using caching plugin

### Courses/Groups not displaying
- Check publication status
- Verify user permissions
- Confirm categories/tags exist
- Test with simpler parameters

### Styling issues
- Check for theme conflicts
- Verify CSS is loading
- Test with default parameters
- Check responsive breakpoints

---

## Developer Hooks

### Filters for customization

```php
// Modify course query
add_filter('reign_courses_query_args', function($args) {
    // Customize query
    return $args;
});

// Modify course output
add_filter('reign_courses_output', function($output, $atts) {
    // Customize output
    return $output;
}, 10, 2);

// Modify groups query
add_filter('modern_groups_query_args', function($args) {
    // Customize query
    return $args;
});
```

### Actions for extending

```php
// Before courses display
do_action('reign_before_courses_shortcode', $atts);

// After courses display
do_action('reign_after_courses_shortcode', $output);

// Before groups display
do_action('modern_before_groups_shortcode', $atts);

// After groups display
do_action('modern_after_groups_shortcode', $output);
```

---

## Support

For additional help with shortcodes:
- 📧 Email: support@wbcomdesigns.com
- 📚 Documentation: docs.wbcomdesigns.com
- 💬 Forum: wbcomdesigns.com/support