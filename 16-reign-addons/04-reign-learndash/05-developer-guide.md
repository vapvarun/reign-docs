# Reign LearnDash Addon - Developer Guide

## 🛠️ Build Amazing Learning Features

This comprehensive guide provides everything developers need to extend, customize, and integrate with Reign LearnDash Addon. From simple hooks to advanced customizations - unlock the full potential of your learning platform.

---

## 🎯 Available Shortcodes (Complete List)

### Primary Course Display Shortcodes

**`[modern_courses]` / `[reign_courses]`** - Main course display
```php
// Basic usage
echo do_shortcode('[modern_courses]');

// Advanced with all parameters
echo do_shortcode('[modern_courses
    template="premium"
    udemy_style="yes"
    columns="3"
    per_page="12"
    show_reviews="yes"
    show_price="yes"
    category="web-development"
]');
```
**Use cases:** Course catalogs, homepage displays, category pages

**`[modern_groups]`** - LearnDash group display
```php
// Display learning groups
echo do_shortcode('[modern_groups columns="4" show_members="yes"]');
```
**Use cases:** Community pages, group directories

### Tab Content Shortcodes (For Custom Layouts)

**`[reign_ld_pro_comments_tab_content]`** - Course discussions
```php
// Add course comments section
echo do_shortcode('[reign_ld_pro_comments_tab_content course_id="123"]');
```

**`[reign_ld_pro_instructor_tab_content]`** - Instructor details
```php
// Display instructor information
echo do_shortcode('[reign_ld_pro_instructor_tab_content]');
```

**`[reign_ld_pro_course_content_tab_content]`** - Course curriculum
```php
// Show course content structure
echo do_shortcode('[reign_ld_pro_course_content_tab_content]');
```

---

## 🎨 Template Override System

### Safe Template Customization
**Never lose changes during updates!**

#### How to Override Templates

1. **Copy template from plugin:**
   ```
   Source: /wp-content/plugins/reign-learndash-addon/templates/[template-name].php
   ```

2. **Paste into your theme:**
   ```
   Destination: /wp-content/themes/your-theme/learndash/[template-name].php
   ```

3. **Edit freely** - Your changes are now update-safe!

#### Available Templates to Customize

**Course Display Templates:**
- `course-card-premium.php` - Premium course cards
- `course-card-minimal.php` - Minimal course cards
- `course-card-udemy.php` - Udemy-style cards
- `course-grid.php` - Course grid layouts
- `course-filters.php` - Filter interfaces

**Group Templates:**
- `group-card.php` - Group display cards
- `group-grid.php` - Group grid layouts

**Widget Templates:**
- `widget-course-list.php` - Course list widget
- `widget-course-search.php` - Search widget

#### Template Hierarchy
```php
// Plugin checks in this order:
1. /your-theme/learndash/template-name.php  // Your override
2. /reign-learndash-addon/templates/template-name.php  // Plugin default
3. /learndash/templates/template-name.php  // LearnDash default
```

---

## 🔧 Hooks & Filters Reference

### Actions (Extend Functionality)

**Course Display Actions:**
```php
// Before course grid
do_action('reign_learndash_before_course_grid');

// After each course card
do_action('reign_learndash_after_course_card', $course_id);

// Inside course card (for adding custom elements)
do_action('reign_learndash_course_card_footer', $course_id);

// After course grid
do_action('reign_learndash_after_course_grid');
```

**Review System Actions:**
```php
// After review submission
do_action('reign_learndash_after_review_submit', $course_id, $rating, $review);

// Before review display
do_action('reign_learndash_before_reviews', $course_id);
```

### Filters (Modify Behavior)

**Course Query Filters:**
```php
// Modify course query arguments
add_filter('reign_learndash_courses_query_args', function($args) {
    $args['posts_per_page'] = 20;
    $args['orderby'] = 'menu_order';
    return $args;
});

// Filter course display
add_filter('reign_learndash_show_course', function($show, $course_id) {
    // Custom logic to show/hide courses
    return $show;
}, 10, 2);
```

**Template Filters:**
```php
// Change template path
add_filter('reign_learndash_template_path', function($template, $name) {
    if ($name === 'course-card') {
        return 'custom-path/custom-card.php';
    }
    return $template;
}, 10, 2);
```

---

## 🚀 AJAX Implementation

### Dynamic Course Loading
```javascript
// Load more courses via AJAX
jQuery.ajax({
    url: reign_learndash_ajax.ajax_url,
    type: 'POST',
    data: {
        action: 'reign_load_more_courses',
        page: 2,
        category: 'web-development',
        nonce: reign_learndash_ajax.nonce
    },
    success: function(response) {
        // Append courses to grid
        jQuery('.course-grid').append(response.html);
    }
});
```

### Filter Updates
```javascript
// AJAX-powered filtering
jQuery('.course-filter').on('change', function() {
    var filters = {
        category: jQuery('#category').val(),
        price: jQuery('#price').val(),
        rating: jQuery('#rating').val()
    };

    // Update courses without page reload
    reign_update_courses(filters);
});
```

---

## 📦 Gutenberg Block Development

### Register Custom Block
```javascript
// Register Reign Courses block
wp.blocks.registerBlockType('reign-learndash/courses', {
    title: 'Reign Courses',
    icon: 'welcome-learn-more',
    category: 'reign-blocks',
    attributes: {
        template: {
            type: 'string',
            default: 'premium'
        },
        columns: {
            type: 'number',
            default: 3
        },
        udemy_style: {
            type: 'boolean',
            default: true
        }
    },
    edit: ReignCoursesEdit,
    save: ReignCoursesSave
});
```

---

## 👥 BuddyPress Integration API

### Activity Stream Integration
```php
// Log course enrollment activity
function log_course_enrollment($user_id, $course_id) {
    if (function_exists('bp_activity_add')) {
        bp_activity_add(array(
            'action' => sprintf('%s enrolled in %s',
                bp_core_get_userlink($user_id),
                get_the_title($course_id)
            ),
            'type' => 'course_enrollment',
            'item_id' => $course_id,
            'user_id' => $user_id
        ));
    }
}
add_action('learndash_course_enrolled', 'log_course_enrollment', 10, 2);
```

### Profile Tab Integration
```php
// Add custom courses tab to BuddyPress profiles
function add_courses_profile_tab() {
    bp_core_new_nav_item(array(
        'name' => 'My Courses',
        'slug' => 'courses',
        'screen_function' => 'courses_screen',
        'position' => 30,
        'default_subnav_slug' => 'enrolled'
    ));
}
add_action('bp_setup_nav', 'add_courses_profile_tab');
```

### Group-Course Sync
```php
// Sync course enrollment with BuddyPress groups
function sync_course_group($user_id, $course_id) {
    $group_id = get_course_group_id($course_id);
    if ($group_id) {
        groups_join_group($group_id, $user_id);
    }
}
add_action('learndash_course_enrolled', 'sync_course_group', 10, 2);
```

---

## 💼 Common Development Tasks

### Add Custom Course Meta
```php
// Display custom course information
add_action('reign_learndash_course_card_footer', function($course_id) {
    $difficulty = get_post_meta($course_id, 'course_difficulty', true);
    echo '<span class="course-difficulty">' . esc_html($difficulty) . '</span>';
});
```

### Customize Review System
```php
// Add review incentive
add_filter('reign_learndash_review_form_fields', function($fields) {
    $fields['incentive'] = array(
        'type' => 'checkbox',
        'label' => 'Earn 10 points for your review!',
        'required' => false
    );
    return $fields;
});
```

### Create Custom Shortcode
```php
// Register instructor courses shortcode
function reign_instructor_courses_shortcode($atts) {
    $atts = shortcode_atts(array(
        'instructor_id' => get_current_user_id(),
        'limit' => 10
    ), $atts);

    // Query instructor courses
    $courses = get_instructor_courses($atts['instructor_id'], $atts['limit']);

    // Return formatted output
    return reign_render_courses($courses);
}
add_shortcode('instructor_courses', 'reign_instructor_courses_shortcode');
```

---

## 🔒 Security Best Practices

### Nonce Verification
```php
// Always verify nonces in AJAX handlers
if (!wp_verify_nonce($_POST['nonce'], 'reign_learndash_nonce')) {
    wp_die('Security check failed');
}
```

### Data Sanitization
```php
// Sanitize all user input
$course_id = absint($_POST['course_id']);
$review_text = sanitize_textarea_field($_POST['review']);
$rating = min(5, max(1, intval($_POST['rating'])));
```

### Capability Checks
```php
// Check user permissions
if (!current_user_can('edit_courses')) {
    wp_die('Permission denied');
}
```

---

## ⚡ Performance Optimization

### Caching Implementation
```php
// Cache expensive queries
function get_popular_courses($limit = 10) {
    $cache_key = 'reign_popular_courses_' . $limit;
    $courses = get_transient($cache_key);

    if (false === $courses) {
        $courses = query_popular_courses($limit);
        set_transient($cache_key, $courses, HOUR_IN_SECONDS);
    }

    return $courses;
}
```

### Lazy Loading
```php
// Implement lazy loading for course images
add_filter('reign_learndash_course_thumbnail_attributes', function($attr) {
    $attr['loading'] = 'lazy';
    $attr['decoding'] = 'async';
    return $attr;
});
```

---

## 📚 Resources & Support

- **Hook Reference**: Complete list in plugin code
- **Template Examples**: `/templates/` directory
- **Support Forum**: [WBcom Designs Support](https://wbcomdesigns.com/support)
- **Documentation**: This guide and inline code comments

---

*🔧 Build something amazing with Reign LearnDash Addon!*