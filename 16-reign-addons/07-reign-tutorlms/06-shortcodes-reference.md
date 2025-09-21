# Reign TutorLMS Addon - Shortcodes Reference

## Overview

Reign TutorLMS Addon v2.0.0 provides 2 powerful shortcodes with extensive parameters for creating dynamic, context-aware course displays with multi-platform social integration (BuddyPress/PeepSo), AJAX progress tracking, and advanced filtering capabilities.

---

## Shortcode 1: [reign_tutor_course]

The primary shortcode for displaying TutorLMS courses with enhanced features, social integration, and context-aware content.

### Basic Usage

```
[reign_tutor_course]
```

### All Parameters (25+ Options)

#### Layout & Display Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `layout` | string | "grid" | Display layout style | "grid", "list", "carousel", "masonry" |
| `columns` | number | 3 | Number of columns (1-6) | `columns="4"` |
| `posts_per_page` | number | 10 | Courses to display | `posts_per_page="12"` |
| `pagination` | boolean | true | Enable pagination | `pagination="false"` |
| `grid_style` | string | "card" | Grid card style | "card", "minimal", "detailed" |
| `equal_height` | boolean | true | Equal height cards | `equal_height="false"` |

#### Course Content Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `show_instructor` | boolean | true | Display instructor info | `show_instructor="false"` |
| `show_price` | boolean | true | Display course price | `show_price="false"` |
| `show_duration` | boolean | true | Display course duration | `show_duration="false"` |
| `show_difficulty` | boolean | true | Display difficulty level | `show_difficulty="false"` |
| `show_categories` | boolean | true | Display course categories | `show_categories="false"` |
| `show_tags` | boolean | false | Display course tags | `show_tags="true"` |
| `show_enrollment_count` | boolean | false | Display enrollment numbers | `show_enrollment_count="true"` |
| `show_rating` | boolean | true | Display course ratings | `show_rating="false"` |
| `show_excerpt` | boolean | false | Display course excerpt | `show_excerpt="true"` |
| `excerpt_length` | number | 150 | Excerpt character limit | `excerpt_length="100"` |

#### Progress & Status Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `show_progress` | boolean | false | Display progress bars | `show_progress="true"` |
| `progress_style` | string | "bar" | Progress display style | "bar", "circle", "percentage" |
| `show_status` | boolean | false | Display enrollment status | `show_status="true"` |
| `status_text` | string | auto | Custom status text | `status_text="In Progress"` |

#### User Context Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `my_courses` | boolean | false | Show only user's courses | `my_courses="true"` |
| `user_id` | number | current | Specific user ID | `user_id="123"` |
| `user_context` | string | "auto" | Context detection mode | "profile_owner", "visitor", "current_user" |

#### Course Filtering Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `course_status` | string | "all" | Filter by enrollment status | "enrolled", "completed", "in_progress", "not_started" |
| `course_level` | string | "all" | Filter by difficulty level | "beginner", "intermediate", "advanced" |
| `course_category` | string | "" | Filter by category slug | `course_category="web-development"` |
| `instructor_id` | number | "" | Filter by instructor | `instructor_id="45"` |
| `enrollment_status` | string | "all" | Filter by enrollment | "enrolled", "not_enrolled" |

#### Visual & Interaction Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `show_thumbnail` | boolean | true | Display course images | `show_thumbnail="false"` |
| `thumbnail_size` | string | "medium" | Image size | "small", "medium", "large", "full" |
| `show_featured_badge` | boolean | false | Featured course badge | `show_featured_badge="true"` |
| `hover_effects` | boolean | true | Card hover animations | `hover_effects="false"` |
| `loading_animation` | string | "fade" | Loading animation style | "fade", "slide", "zoom" |

#### Ordering Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `orderby` | string | "date" | Sort criteria | "date", "title", "price", "popularity", "rating" |
| `order` | string | "DESC" | Sort direction | "ASC", "DESC" |
| `meta_key` | string | "" | Custom field sorting | `meta_key="_course_price"` |

#### AJAX & Performance Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `ajax_load` | boolean | false | Enable AJAX loading | `ajax_load="true"` |
| `lazy_load` | boolean | false | Lazy load images | `lazy_load="true"` |
| `cache_results` | boolean | true | Cache course data | `cache_results="false"` |

---

## Advanced Usage Examples

### 1. User Profile Course Display

**Complete enrolled courses with progress:**
```
[reign_tutor_course my_courses="true" show_progress="true"
course_status="enrolled" columns="3" layout="grid"
user_context="profile_owner"]
```

### 2. Instructor Course Showcase

**Display instructor's courses with ratings:**
```
[reign_tutor_course instructor_id="45" show_rating="true"
show_enrollment_count="true" columns="4"
show_featured_badge="true" orderby="rating"]
```

### 3. Category-Specific Course Grid

**Web development courses for beginners:**
```
[reign_tutor_course course_category="web-development"
course_level="beginner" columns="3" show_difficulty="true"
show_duration="true" posts_per_page="9"]
```

### 4. Student Progress Dashboard

**In-progress courses with detailed progress:**
```
[reign_tutor_course my_courses="true" course_status="in_progress"
show_progress="true" progress_style="circle"
show_status="true" layout="list"]
```

### 5. Course Catalog with Filtering

**Complete course catalog with AJAX filtering:**
```
[reign_tutor_course ajax_load="true" show_rating="true"
show_enrollment_count="true" show_price="true"
columns="3" pagination="true" posts_per_page="12"]
```

### 6. Mobile-Optimized Course List

**Optimized for mobile devices:**
```
[reign_tutor_course columns="1" layout="list"
show_excerpt="true" excerpt_length="100"
thumbnail_size="small" hover_effects="false"]
```

### 7. Featured Courses Carousel

**Featured courses in carousel format:**
```
[reign_tutor_course layout="carousel" show_featured_badge="true"
columns="3" show_rating="true" show_price="true"
orderby="popularity" posts_per_page="6"]
```

---

## Shortcode 2: [reign_course_categories]

Display TutorLMS course categories with enhanced styling and information.

### Basic Usage

```
[reign_course_categories]
```

### All Parameters

#### Layout Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `layout` | string | "grid" | Display layout | "grid", "list", "carousel" |
| `columns` | number | 4 | Number of columns (1-6) | `columns="5"` |
| `show_count` | boolean | true | Show course count | `show_count="false"` |
| `show_image` | boolean | true | Show category images | `show_image="false"` |
| `show_description` | boolean | false | Show descriptions | `show_description="true"` |

#### Category Selection Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `include` | string | "" | Include specific categories | `include="1,5,10"` |
| `exclude` | string | "" | Exclude categories | `exclude="3,7"` |
| `parent` | number | 0 | Parent category ID | `parent="5"` |
| `child_of` | number | 0 | Child categories of | `child_of="2"` |
| `hide_empty` | boolean | true | Hide empty categories | `hide_empty="false"` |

#### Ordering Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `orderby` | string | "name" | Sort criteria | "name", "count", "id", "slug" |
| `order` | string | "ASC" | Sort direction | "ASC", "DESC" |
| `number` | number | 0 | Limit number shown | `number="8"` |

#### Visual Parameters

| Parameter | Type | Default | Description | Example |
|-----------|------|---------|-------------|---------|
| `image_size` | string | "medium" | Category image size | "thumbnail", "medium", "large" |
| `show_hierarchy` | boolean | false | Show category hierarchy | `show_hierarchy="true"` |
| `depth` | number | 0 | Hierarchy depth (0=all) | `depth="2"` |
| `style` | string | "card" | Category card style | "card", "minimal", "badge" |

---

## Category Shortcode Examples

### 1. Main Course Categories

**Top-level categories with images:**
```
[reign_course_categories columns="4" show_image="true"
show_count="true" parent="0" orderby="count" order="DESC"]
```

### 2. Category Showcase

**Featured categories with descriptions:**
```
[reign_course_categories columns="3" show_description="true"
show_image="true" include="1,5,8,12" style="card"]
```

### 3. Hierarchical Category Display

**Category hierarchy with subcategories:**
```
[reign_course_categories show_hierarchy="true" depth="2"
columns="2" layout="list" show_count="true"]
```

### 4. Minimal Category List

**Simple category badges:**
```
[reign_course_categories style="badge" columns="6"
show_image="false" show_count="false" layout="grid"]
```

---

## Context-Aware Usage

### Profile Integration Examples

#### BuddyPress Profile Tab
```php
// In BuddyPress profile template
[reign_tutor_course my_courses="true" user_context="profile_owner"
show_progress="true" columns="3"]
```

#### PeepSo Profile Widget
```php
// In PeepSo profile
[reign_tutor_course user_id="{current_profile_user}"
show_progress="true" course_status="enrolled" columns="2"]
```

#### Visitor vs Owner Context
```php
// Automatically detects context
[reign_tutor_course user_context="auto" show_progress="true"
my_courses="true" columns="3"]

// When viewing own profile: Shows all courses with progress
// When viewing other's profile: Shows public courses only
```

---

## Social Integration Features

### BuddyPress Activity Integration

When used in BuddyPress contexts, the shortcodes automatically:

1. **Generate Activities**: Course enrollments and completions create activity posts
2. **Context Detection**: Shows different content for profile owners vs visitors
3. **Privacy Respect**: Honors BuddyPress privacy settings
4. **Group Integration**: Can be used in group contexts for group courses

### PeepSo Integration

For PeepSo platforms:

1. **Profile Tabs**: Automatic integration with PeepSo profile navigation
2. **Stream Posts**: Course activities appear in PeepSo streams
3. **Privacy Controls**: Integrates with PeepSo privacy system
4. **Mobile Optimization**: Optimized for PeepSo mobile apps

---

## AJAX and Performance Features

### Real-Time Updates

When `ajax_load="true"` is enabled:

1. **Progress Updates**: Course progress updates without page refresh
2. **Enrollment Status**: Real-time enrollment status changes
3. **Filtering**: Dynamic course filtering with smooth animations
4. **Pagination**: AJAX-powered pagination with URL updates

### Performance Optimization

1. **Lazy Loading**: Images load as they come into view
2. **Caching**: Results cached for improved performance
3. **Debouncing**: Input filtering debounced for smooth UX
4. **Progressive Loading**: Content loads progressively for better perceived performance

---

## Custom Styling

### CSS Classes

The shortcodes generate semantic CSS classes for easy customization:

```css
/* Course grid container */
.reign-tutor-courses-grid { }

/* Individual course cards */
.reign-tutor-course-card { }

/* Progress bars */
.reign-tutor-progress-bar { }

/* Category grid */
.reign-course-categories-grid { }

/* Context-specific styles */
.reign-context-profile-owner { }
.reign-context-visitor { }
```

### Custom Templates

Override templates in your theme:

```
/wp-content/themes/your-theme/
  └── reign-tutorlms/
      ├── course-card.php
      ├── course-progress.php
      ├── category-card.php
      └── shortcode-wrapper.php
```

---

## Browser Support

### Supported Browsers

- ✅ Chrome 70+
- ✅ Firefox 65+
- ✅ Safari 12+
- ✅ Edge 79+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

### Progressive Enhancement

- **JavaScript Disabled**: Basic functionality still works
- **Older Browsers**: Graceful degradation
- **Mobile First**: Optimized for mobile devices
- **Accessibility**: Screen reader compatible

---

## Troubleshooting

### Common Issues

**Shortcode not rendering:**
```
Solution: Check TutorLMS plugin is active and Reign theme is enabled
```

**AJAX not working:**
```
Solution: Check browser console for JavaScript errors
Verify WordPress AJAX is enabled
```

**Context detection failing:**
```
Solution: Clear user sessions and caches
Verify BuddyPress/PeepSo integration
```

**Progress not updating:**
```
Solution: Check user enrollment status
Verify course progress tracking is enabled
```

---

## Advanced Implementation

### PHP Integration

```php
// Use shortcode in PHP
echo do_shortcode('[reign_tutor_course my_courses="true" show_progress="true"]');

// With dynamic parameters
$user_id = bp_displayed_user_id();
echo do_shortcode("[reign_tutor_course user_id=\"{$user_id}\" my_courses=\"true\"]");
```

### Widget Integration

```php
// Custom widget with shortcode
class Custom_Course_Widget extends WP_Widget {
    public function widget($args, $instance) {
        echo do_shortcode('[reign_tutor_course columns="2" show_progress="true"]');
    }
}
```

---

## Next Steps

- [Course Customization Guide](04-course-customization.md) - Design and layout options
- [Developer Guide](05-developer-guide.md) - Custom development
- [Troubleshooting Guide](07-troubleshooting.md) - Common issues and solutions

**Need Help?**
📧 support@wbcomdesigns.com | 📚 docs.wbcomdesigns.com