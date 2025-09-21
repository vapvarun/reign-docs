# Reign TutorLMS Addon - Developer Guide

## What You'll Learn
This comprehensive guide provides developers with advanced customization techniques, hooks, filters, and code examples for extending the Reign TutorLMS addon functionality.

## Quick Overview
**Audience:** Developers, advanced users
**Difficulty:** Advanced
**Prerequisites:** PHP, WordPress development knowledge

---

## Part 1: Architecture Overview

### Addon Structure

```
reign-tutorlms-addon/
├── includes/
│   ├── class-reign-tutor-core.php
│   ├── class-reign-tutor-customizer.php
│   ├── class-reign-tutor-templates.php
│   └── class-reign-tutor-ajax.php
├── templates/
│   ├── course/
│   ├── lesson/
│   └── quiz/
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
└── reign-tutorlms-addon.php
```

### Core Classes

**Main initialization:**
```php
class Reign_TutorLMS_Addon {
    private static $instance = null;

    public static function get_instance() {
        if (null === self::$instance) {
            self::$instance = new self();
        }
        return self::$instance;
    }

    private function __construct() {
        $this->init_hooks();
        $this->load_dependencies();
    }

    private function init_hooks() {
        add_action('init', array($this, 'init'));
        add_action('wp_enqueue_scripts', array($this, 'enqueue_scripts'));
    }
}
```

---

## Part 2: Available Hooks and Filters

### Action Hooks

**Course-related actions:**

```php
// Before course content
do_action('reign_tutor_before_course_content', $course_id);

// After course enrollment
do_action('reign_tutor_after_course_enrollment', $course_id, $user_id);

// Before lesson start
do_action('reign_tutor_before_lesson_start', $lesson_id, $course_id);

// After lesson completion
do_action('reign_tutor_after_lesson_completion', $lesson_id, $user_id);

// Before quiz attempt
do_action('reign_tutor_before_quiz_attempt', $quiz_id, $user_id);

// After certificate generation
do_action('reign_tutor_after_certificate_generated', $certificate_id, $course_id, $user_id);
```

**Example usage:**
```php
// Add custom tracking after course enrollment
add_action('reign_tutor_after_course_enrollment', 'custom_enrollment_tracking', 10, 2);
function custom_enrollment_tracking($course_id, $user_id) {
    // Send to analytics
    wp_remote_post('https://analytics.example.com/track', array(
        'body' => array(
            'event' => 'course_enrollment',
            'course_id' => $course_id,
            'user_id' => $user_id,
            'timestamp' => current_time('timestamp')
        )
    ));

    // Add to CRM
    $user = get_userdata($user_id);
    $course = get_post($course_id);

    // Custom CRM integration here
}
```

### Filter Hooks

**Content modification filters:**

```php
// Modify course card content
apply_filters('reign_tutor_course_card_content', $content, $course_id);

// Customize lesson navigation
apply_filters('reign_tutor_lesson_navigation', $navigation, $lesson_id);

// Filter quiz questions display
apply_filters('reign_tutor_quiz_questions', $questions, $quiz_id);

// Customize student dashboard
apply_filters('reign_tutor_student_dashboard_content', $content, $user_id);

// Modify instructor dashboard
apply_filters('reign_tutor_instructor_dashboard_content', $content, $instructor_id);
```

**Example implementations:**
```php
// Add custom course card elements
add_filter('reign_tutor_course_card_content', 'add_custom_course_info', 10, 2);
function add_custom_course_info($content, $course_id) {
    $custom_info = get_post_meta($course_id, 'custom_course_info', true);

    if ($custom_info) {
        $content .= '<div class="custom-course-info">';
        $content .= '<i class="fa fa-info-circle"></i> ' . esc_html($custom_info);
        $content .= '</div>';
    }

    return $content;
}

// Customize lesson navigation
add_filter('reign_tutor_lesson_navigation', 'custom_lesson_navigation', 10, 2);
function custom_lesson_navigation($navigation, $lesson_id) {
    $course_id = tutor_utils()->get_course_id_by_lesson($lesson_id);
    $lessons = tutor_utils()->get_course_contents_by_id($course_id);

    $nav = '<div class="custom-lesson-nav">';
    foreach ($lessons as $lesson) {
        $status = tutor_utils()->is_completed_lesson($lesson->ID) ? 'completed' : 'pending';
        $nav .= sprintf(
            '<a href="%s" class="lesson-nav-item %s">%s</a>',
            get_permalink($lesson->ID),
            $status,
            $lesson->post_title
        );
    }
    $nav .= '</div>';

    return $nav;
}
```

---

## Part 3: Template System

### Template Hierarchy

**Template loading order:**
```
1. theme/tutor/reign-templates/
2. reign-addon/templates/
3. tutor-plugin/templates/
```

### Custom Template Creation

**Override course archive:**
```php
// In your theme: tutor/reign-templates/archive-courses.php
<?php
get_header();

// Custom course archive layout
$courses = new WP_Query(array(
    'post_type' => 'courses',
    'posts_per_page' => 12,
    'meta_query' => array(
        array(
            'key' => '_tutor_course_status',
            'value' => 'published'
        )
    )
));

if ($courses->have_posts()) :
    echo '<div class="reign-course-grid">';
    while ($courses->have_posts()) : $courses->the_post();
        // Include custom course card template
        include locate_template('tutor/reign-templates/course-card.php');
    endwhile;
    echo '</div>';

    // Custom pagination
    reign_tutor_pagination($courses);
endif;

wp_reset_postdata();
get_footer();
?>
```

**Custom course card template:**
```php
// theme/tutor/reign-templates/course-card.php
<?php
$course_id = get_the_ID();
$instructor = tutor_utils()->get_course_instructor_by_course($course_id);
$course_rating = tutor_utils()->get_course_rating($course_id);
$students = tutor_utils()->count_enrolled_users_by_course($course_id);
?>

<div class="reign-course-card" data-course-id="<?php echo esc_attr($course_id); ?>">
    <div class="course-thumbnail">
        <?php if (has_post_thumbnail()) : ?>
            <a href="<?php the_permalink(); ?>">
                <?php the_post_thumbnail('medium'); ?>
            </a>
        <?php endif; ?>

        <!-- Custom overlay with quick actions -->
        <div class="course-overlay">
            <button class="quick-preview" data-course="<?php echo esc_attr($course_id); ?>">
                <i class="fa fa-eye"></i> Preview
            </button>
            <button class="add-to-wishlist" data-course="<?php echo esc_attr($course_id); ?>">
                <i class="fa fa-heart"></i> Save
            </button>
        </div>
    </div>

    <div class="course-content">
        <div class="course-meta">
            <span class="course-category">
                <?php echo get_the_terms($course_id, 'course-category')[0]->name; ?>
            </span>
            <span class="course-level">
                <?php echo get_post_meta($course_id, '_tutor_course_level', true); ?>
            </span>
        </div>

        <h3 class="course-title">
            <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
        </h3>

        <div class="course-excerpt">
            <?php echo wp_trim_words(get_the_excerpt(), 20); ?>
        </div>

        <div class="course-instructor">
            <img src="<?php echo esc_url(get_avatar_url($instructor->ID, 32)); ?>" alt="">
            <span><?php echo esc_html($instructor->display_name); ?></span>
        </div>

        <div class="course-stats">
            <div class="rating">
                <?php tutor_utils()->star_rating_generator($course_rating->rating_avg); ?>
                <span>(<?php echo esc_html($course_rating->rating_count); ?>)</span>
            </div>
            <div class="students">
                <i class="fa fa-users"></i> <?php echo esc_html($students); ?> students
            </div>
        </div>

        <div class="course-footer">
            <div class="course-price">
                <?php tutor_course_price(); ?>
            </div>
            <div class="course-actions">
                <?php
                $enroll_btn = tutor_course_loop_add_to_cart(false);
                echo $enroll_btn;
                ?>
            </div>
        </div>
    </div>
</div>
```

---

## Part 4: AJAX Implementation

### Custom AJAX Handlers

**Course preview functionality:**
```php
class Reign_Tutor_Ajax {
    public function __construct() {
        add_action('wp_ajax_reign_course_preview', array($this, 'course_preview'));
        add_action('wp_ajax_nopriv_reign_course_preview', array($this, 'course_preview'));

        add_action('wp_ajax_reign_add_to_wishlist', array($this, 'add_to_wishlist'));
        add_action('wp_ajax_nopriv_reign_add_to_wishlist', array($this, 'add_to_wishlist'));
    }

    public function course_preview() {
        check_ajax_referer('reign_tutor_nonce', 'nonce');

        $course_id = intval($_POST['course_id']);

        if (!$course_id) {
            wp_die('Invalid course ID');
        }

        $course = get_post($course_id);
        $instructor = tutor_utils()->get_course_instructor_by_course($course_id);
        $curriculum = tutor_utils()->get_course_curriculum($course_id);

        $preview_data = array(
            'title' => $course->post_title,
            'description' => $course->post_content,
            'instructor' => array(
                'name' => $instructor->display_name,
                'bio' => get_user_meta($instructor->ID, 'description', true),
                'avatar' => get_avatar_url($instructor->ID, 64)
            ),
            'curriculum' => $this->format_curriculum($curriculum),
            'features' => $this->get_course_features($course_id),
            'prerequisites' => get_post_meta($course_id, '_tutor_course_prerequisites', true)
        );

        wp_send_json_success($preview_data);
    }

    public function add_to_wishlist() {
        if (!is_user_logged_in()) {
            wp_send_json_error('Please login to add to wishlist');
        }

        check_ajax_referer('reign_tutor_nonce', 'nonce');

        $course_id = intval($_POST['course_id']);
        $user_id = get_current_user_id();

        $wishlist = get_user_meta($user_id, '_tutor_course_wishlist', true);
        if (!is_array($wishlist)) {
            $wishlist = array();
        }

        if (in_array($course_id, $wishlist)) {
            // Remove from wishlist
            $wishlist = array_diff($wishlist, array($course_id));
            $action = 'removed';
        } else {
            // Add to wishlist
            $wishlist[] = $course_id;
            $action = 'added';
        }

        update_user_meta($user_id, '_tutor_course_wishlist', $wishlist);

        wp_send_json_success(array(
            'action' => $action,
            'count' => count($wishlist),
            'message' => $action === 'added' ? 'Added to wishlist' : 'Removed from wishlist'
        ));
    }

    private function format_curriculum($curriculum) {
        $formatted = array();

        foreach ($curriculum as $item) {
            $formatted[] = array(
                'title' => $item->post_title,
                'type' => $item->post_type,
                'duration' => get_post_meta($item->ID, '_video_duration', true),
                'is_preview' => get_post_meta($item->ID, '_is_preview', true)
            );
        }

        return $formatted;
    }

    private function get_course_features($course_id) {
        return array(
            'duration' => get_post_meta($course_id, '_course_duration', true),
            'level' => get_post_meta($course_id, '_tutor_course_level', true),
            'language' => get_post_meta($course_id, '_course_language', true),
            'certificate' => get_post_meta($course_id, '_tutor_enable_certificate', true),
            'lifetime_access' => get_post_meta($course_id, '_lifetime_access', true)
        );
    }
}

new Reign_Tutor_Ajax();
```

**Frontend JavaScript:**
```javascript
// assets/js/reign-tutor-frontend.js
class ReignTutorFrontend {
    constructor() {
        this.init();
    }

    init() {
        this.bindEvents();
        this.initializeComponents();
    }

    bindEvents() {
        // Course preview
        $(document).on('click', '.quick-preview', (e) => {
            e.preventDefault();
            const courseId = $(e.target).closest('[data-course-id]').data('course-id');
            this.showCoursePreview(courseId);
        });

        // Wishlist functionality
        $(document).on('click', '.add-to-wishlist', (e) => {
            e.preventDefault();
            const courseId = $(e.target).closest('[data-course-id]').data('course-id');
            this.toggleWishlist(courseId, e.target);
        });

        // Course filtering
        $(document).on('change', '.course-filters input, .course-filters select', () => {
            this.filterCourses();
        });
    }

    showCoursePreview(courseId) {
        // Show loading modal
        this.showModal('loading');

        $.ajax({
            url: reign_tutor_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_course_preview',
                course_id: courseId,
                nonce: reign_tutor_ajax.nonce
            },
            success: (response) => {
                if (response.success) {
                    this.renderCoursePreview(response.data);
                } else {
                    this.showError('Failed to load course preview');
                }
            },
            error: () => {
                this.showError('Network error occurred');
            }
        });
    }

    renderCoursePreview(data) {
        const template = `
            <div class="course-preview-modal">
                <div class="modal-header">
                    <h2>${data.title}</h2>
                    <button class="modal-close">&times;</button>
                </div>
                <div class="modal-content">
                    <div class="course-info">
                        <div class="instructor-info">
                            <img src="${data.instructor.avatar}" alt="${data.instructor.name}">
                            <div>
                                <h4>${data.instructor.name}</h4>
                                <p>${data.instructor.bio}</p>
                            </div>
                        </div>
                        <div class="course-description">
                            ${data.description}
                        </div>
                        <div class="course-curriculum">
                            <h3>Course Content</h3>
                            ${this.renderCurriculum(data.curriculum)}
                        </div>
                        <div class="course-features">
                            ${this.renderFeatures(data.features)}
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button class="btn-enroll">Enroll Now</button>
                    <button class="btn-demo">Free Preview</button>
                </div>
            </div>
        `;

        this.showModal(template);
    }

    toggleWishlist(courseId, button) {
        const $button = $(button);
        const isInWishlist = $button.hasClass('in-wishlist');

        $button.prop('disabled', true);

        $.ajax({
            url: reign_tutor_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_add_to_wishlist',
                course_id: courseId,
                nonce: reign_tutor_ajax.nonce
            },
            success: (response) => {
                if (response.success) {
                    if (response.data.action === 'added') {
                        $button.addClass('in-wishlist');
                        $button.find('i').removeClass('fa-heart-o').addClass('fa-heart');
                    } else {
                        $button.removeClass('in-wishlist');
                        $button.find('i').removeClass('fa-heart').addClass('fa-heart-o');
                    }

                    this.showNotification(response.data.message, 'success');
                    this.updateWishlistCount(response.data.count);
                } else {
                    this.showNotification(response.data, 'error');
                }
            },
            complete: () => {
                $button.prop('disabled', false);
            }
        });
    }

    filterCourses() {
        const filters = this.getActiveFilters();
        const $courseGrid = $('.reign-course-grid');

        // Show loading
        $courseGrid.addClass('loading');

        $.ajax({
            url: reign_tutor_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_filter_courses',
                filters: filters,
                nonce: reign_tutor_ajax.nonce
            },
            success: (response) => {
                if (response.success) {
                    $courseGrid.html(response.data.html);
                    this.updateResultsCount(response.data.count);
                }
            },
            complete: () => {
                $courseGrid.removeClass('loading');
            }
        });
    }
}

// Initialize when document is ready
$(document).ready(() => {
    new ReignTutorFrontend();
});
```

---

## Part 5: Custom Post Types & Fields

### Add Custom Course Fields

```php
class Reign_Tutor_Custom_Fields {
    public function __construct() {
        add_action('add_meta_boxes', array($this, 'add_custom_meta_boxes'));
        add_action('save_post', array($this, 'save_custom_meta'));
    }

    public function add_custom_meta_boxes() {
        add_meta_box(
            'reign_course_custom_fields',
            'Additional Course Information',
            array($this, 'custom_fields_callback'),
            'courses',
            'normal',
            'high'
        );
    }

    public function custom_fields_callback($post) {
        wp_nonce_field('reign_course_custom_fields', 'reign_course_nonce');

        $featured_course = get_post_meta($post->ID, '_featured_course', true);
        $course_trailer = get_post_meta($post->ID, '_course_trailer', true);
        $course_language = get_post_meta($post->ID, '_course_language', true);
        $course_tags = get_post_meta($post->ID, '_course_tags', true);
        ?>

        <table class="form-table">
            <tr>
                <th><label for="featured_course">Featured Course</label></th>
                <td>
                    <input type="checkbox" id="featured_course" name="featured_course" value="1"
                           <?php checked($featured_course, '1'); ?>>
                    <label for="featured_course">Mark as featured course</label>
                </td>
            </tr>
            <tr>
                <th><label for="course_trailer">Course Trailer URL</label></th>
                <td>
                    <input type="url" id="course_trailer" name="course_trailer"
                           value="<?php echo esc_attr($course_trailer); ?>" class="regular-text">
                    <p class="description">YouTube or Vimeo URL for course preview</p>
                </td>
            </tr>
            <tr>
                <th><label for="course_language">Course Language</label></th>
                <td>
                    <select id="course_language" name="course_language">
                        <option value="">Select Language</option>
                        <?php
                        $languages = array(
                            'en' => 'English',
                            'es' => 'Spanish',
                            'fr' => 'French',
                            'de' => 'German',
                            'it' => 'Italian',
                            'pt' => 'Portuguese'
                        );

                        foreach ($languages as $code => $name) {
                            printf(
                                '<option value="%s" %s>%s</option>',
                                esc_attr($code),
                                selected($course_language, $code, false),
                                esc_html($name)
                            );
                        }
                        ?>
                    </select>
                </td>
            </tr>
            <tr>
                <th><label for="course_tags">Course Tags</label></th>
                <td>
                    <input type="text" id="course_tags" name="course_tags"
                           value="<?php echo esc_attr($course_tags); ?>" class="regular-text">
                    <p class="description">Comma-separated tags for better discoverability</p>
                </td>
            </tr>
        </table>

        <?php
    }

    public function save_custom_meta($post_id) {
        if (!isset($_POST['reign_course_nonce']) ||
            !wp_verify_nonce($_POST['reign_course_nonce'], 'reign_course_custom_fields')) {
            return;
        }

        if (defined('DOING_AUTOSAVE') && DOING_AUTOSAVE) {
            return;
        }

        if (!current_user_can('edit_post', $post_id)) {
            return;
        }

        $fields = array(
            'featured_course' => 'sanitize_text_field',
            'course_trailer' => 'esc_url_raw',
            'course_language' => 'sanitize_text_field',
            'course_tags' => 'sanitize_text_field'
        );

        foreach ($fields as $field => $sanitize_callback) {
            if (isset($_POST[$field])) {
                update_post_meta($post_id, '_' . $field, call_user_func($sanitize_callback, $_POST[$field]));
            }
        }
    }
}

new Reign_Tutor_Custom_Fields();
```

---

## Part 6: Advanced Analytics

### Custom Analytics Implementation

```php
class Reign_Tutor_Analytics {
    private $table_name;

    public function __construct() {
        global $wpdb;
        $this->table_name = $wpdb->prefix . 'reign_tutor_analytics';

        add_action('init', array($this, 'init'));
        add_action('tutor_lesson_completed_after', array($this, 'track_lesson_completion'), 10, 2);
        add_action('tutor_quiz/attempt_ended', array($this, 'track_quiz_completion'), 10, 2);
    }

    public function init() {
        $this->create_analytics_table();
        $this->schedule_analytics_cleanup();
    }

    private function create_analytics_table() {
        global $wpdb;

        $charset_collate = $wpdb->get_charset_collate();

        $sql = "CREATE TABLE IF NOT EXISTS {$this->table_name} (
            id bigint(20) unsigned NOT NULL AUTO_INCREMENT,
            user_id bigint(20) unsigned NOT NULL,
            course_id bigint(20) unsigned NOT NULL,
            lesson_id bigint(20) unsigned DEFAULT NULL,
            quiz_id bigint(20) unsigned DEFAULT NULL,
            event_type varchar(50) NOT NULL,
            event_data longtext,
            ip_address varchar(45),
            user_agent text,
            created_at datetime DEFAULT CURRENT_TIMESTAMP,
            PRIMARY KEY (id),
            KEY user_id (user_id),
            KEY course_id (course_id),
            KEY event_type (event_type),
            KEY created_at (created_at)
        ) $charset_collate;";

        require_once(ABSPATH . 'wp-admin/includes/upgrade.php');
        dbDelta($sql);
    }

    public function track_event($event_type, $data = array()) {
        global $wpdb;

        $event_data = array(
            'user_id' => get_current_user_id(),
            'event_type' => sanitize_text_field($event_type),
            'event_data' => wp_json_encode($data),
            'ip_address' => $this->get_user_ip(),
            'user_agent' => $_SERVER['HTTP_USER_AGENT'] ?? '',
            'created_at' => current_time('mysql')
        );

        // Add course/lesson/quiz IDs if present
        if (isset($data['course_id'])) {
            $event_data['course_id'] = intval($data['course_id']);
        }
        if (isset($data['lesson_id'])) {
            $event_data['lesson_id'] = intval($data['lesson_id']);
        }
        if (isset($data['quiz_id'])) {
            $event_data['quiz_id'] = intval($data['quiz_id']);
        }

        $wpdb->insert($this->table_name, $event_data);
    }

    public function track_lesson_completion($lesson_id, $user_id) {
        $course_id = tutor_utils()->get_course_id_by_lesson($lesson_id);

        $this->track_event('lesson_completed', array(
            'course_id' => $course_id,
            'lesson_id' => $lesson_id,
            'completion_time' => current_time('mysql'),
            'time_spent' => $this->calculate_time_spent($lesson_id, $user_id)
        ));

        // Check if course is completed
        if (tutor_utils()->is_completed_course($course_id, $user_id)) {
            $this->track_event('course_completed', array(
                'course_id' => $course_id,
                'completion_time' => current_time('mysql'),
                'total_time_spent' => $this->calculate_course_time_spent($course_id, $user_id)
            ));
        }
    }

    public function track_quiz_completion($quiz_id, $attempt_id) {
        $course_id = tutor_utils()->get_course_id_by_lesson($quiz_id);
        $attempt = tutor_utils()->get_quiz_attempt($attempt_id);

        $this->track_event('quiz_completed', array(
            'course_id' => $course_id,
            'quiz_id' => $quiz_id,
            'attempt_id' => $attempt_id,
            'score' => $attempt->earned_marks,
            'total_marks' => $attempt->total_marks,
            'time_spent' => $attempt->attempt_ended_at - $attempt->attempt_started_at,
            'passed' => $attempt->earned_marks >= ($attempt->total_marks * 0.8)
        ));
    }

    public function get_course_analytics($course_id, $date_range = 30) {
        global $wpdb;

        $start_date = date('Y-m-d', strtotime("-{$date_range} days"));

        $sql = $wpdb->prepare("
            SELECT
                event_type,
                COUNT(*) as event_count,
                DATE(created_at) as event_date
            FROM {$this->table_name}
            WHERE course_id = %d
            AND created_at >= %s
            GROUP BY event_type, DATE(created_at)
            ORDER BY created_at DESC
        ", $course_id, $start_date);

        return $wpdb->get_results($sql);
    }

    public function get_student_progress_analytics($user_id, $course_id = null) {
        global $wpdb;

        $where_clause = "WHERE user_id = %d";
        $params = array($user_id);

        if ($course_id) {
            $where_clause .= " AND course_id = %d";
            $params[] = $course_id;
        }

        $sql = $wpdb->prepare("
            SELECT
                course_id,
                COUNT(CASE WHEN event_type = 'lesson_completed' THEN 1 END) as lessons_completed,
                COUNT(CASE WHEN event_type = 'quiz_completed' THEN 1 END) as quizzes_taken,
                AVG(CASE WHEN event_type = 'quiz_completed' THEN
                    JSON_EXTRACT(event_data, '$.score') END) as avg_quiz_score,
                MIN(created_at) as first_activity,
                MAX(created_at) as last_activity
            FROM {$this->table_name}
            {$where_clause}
            GROUP BY course_id
        ", ...$params);

        return $wpdb->get_results($sql);
    }

    private function calculate_time_spent($lesson_id, $user_id) {
        // Implementation to track time spent on lesson
        // This would require JavaScript tracking on frontend
        return get_user_meta($user_id, "lesson_{$lesson_id}_time_spent", true) ?: 0;
    }

    private function get_user_ip() {
        $ip_keys = array('HTTP_X_FORWARDED_FOR', 'HTTP_X_REAL_IP', 'HTTP_CLIENT_IP', 'REMOTE_ADDR');

        foreach ($ip_keys as $key) {
            if (!empty($_SERVER[$key])) {
                $ip = explode(',', $_SERVER[$key])[0];
                if (filter_var(trim($ip), FILTER_VALIDATE_IP, FILTER_FLAG_NO_PRIV_RANGE | FILTER_FLAG_NO_RES_RANGE)) {
                    return trim($ip);
                }
            }
        }

        return $_SERVER['REMOTE_ADDR'] ?? '';
    }
}

new Reign_Tutor_Analytics();
```

---

## Part 7: Integration Examples

### Third-party Service Integrations

**Zoom Integration Enhancement:**
```php
class Reign_Tutor_Zoom_Enhanced {
    private $zoom_api_key;
    private $zoom_api_secret;

    public function __construct() {
        $this->zoom_api_key = get_option('reign_zoom_api_key');
        $this->zoom_api_secret = get_option('reign_zoom_api_secret');

        add_action('tutor_zoom_meeting_created', array($this, 'enhanced_meeting_creation'), 10, 2);
        add_filter('tutor_zoom_meeting_data', array($this, 'customize_meeting_data'), 10, 2);
    }

    public function enhanced_meeting_creation($meeting_id, $course_id) {
        // Send calendar invites to enrolled students
        $enrolled_students = tutor_utils()->get_enrolled_users_by_course($course_id);

        foreach ($enrolled_students as $student) {
            $this->send_calendar_invite($student, $meeting_id);
        }

        // Create follow-up tasks
        $this->create_meeting_followup_tasks($meeting_id, $course_id);
    }

    private function send_calendar_invite($student, $meeting_id) {
        $meeting_data = get_post_meta($meeting_id, '_zoom_meeting_data', true);

        $ical_content = $this->generate_ical($meeting_data);

        wp_mail(
            $student->user_email,
            'Live Class Invitation',
            'You have been invited to a live class session.',
            array('Content-Type: text/html; charset=UTF-8'),
            array(
                'calendar-invite.ics' => $ical_content
            )
        );
    }

    private function generate_ical($meeting_data) {
        $start_time = date('Ymd\THis\Z', strtotime($meeting_data['start_time']));
        $end_time = date('Ymd\THis\Z', strtotime($meeting_data['start_time'] . ' +' . $meeting_data['duration'] . ' minutes'));

        $ical = "BEGIN:VCALENDAR\r\n";
        $ical .= "VERSION:2.0\r\n";
        $ical .= "PRODID:-//Your Site//Course Meeting//EN\r\n";
        $ical .= "BEGIN:VEVENT\r\n";
        $ical .= "UID:" . uniqid() . "@yoursite.com\r\n";
        $ical .= "DTSTART:{$start_time}\r\n";
        $ical .= "DTEND:{$end_time}\r\n";
        $ical .= "SUMMARY:{$meeting_data['topic']}\r\n";
        $ical .= "DESCRIPTION:Join URL: {$meeting_data['join_url']}\r\n";
        $ical .= "END:VEVENT\r\n";
        $ical .= "END:VCALENDAR\r\n";

        return $ical;
    }
}
```

**CRM Integration (HubSpot example):**
```php
class Reign_Tutor_CRM_Integration {
    private $hubspot_api_key;

    public function __construct() {
        $this->hubspot_api_key = get_option('reign_hubspot_api_key');

        add_action('tutor_after_enroll', array($this, 'sync_to_crm'), 10, 2);
        add_action('tutor_course_complete_after', array($this, 'update_crm_completion'), 10, 2);
    }

    public function sync_to_crm($course_id, $user_id) {
        $user = get_userdata($user_id);
        $course = get_post($course_id);

        $contact_data = array(
            'email' => $user->user_email,
            'firstname' => $user->first_name,
            'lastname' => $user->last_name,
            'enrolled_courses' => $this->get_user_courses($user_id),
            'last_enrollment_date' => current_time('c'),
            'student_status' => 'active'
        );

        $this->update_hubspot_contact($contact_data);

        // Create deal for paid courses
        if (tutor_utils()->is_course_purchasable($course_id)) {
            $this->create_hubspot_deal($user_id, $course_id);
        }
    }

    private function update_hubspot_contact($data) {
        $endpoint = 'https://api.hubapi.com/contacts/v1/contact/createOrUpdate/email/' . $data['email'];

        $body = array(
            'properties' => array()
        );

        foreach ($data as $key => $value) {
            if ($key !== 'email') {
                $body['properties'][] = array(
                    'property' => $key,
                    'value' => $value
                );
            }
        }

        wp_remote_post($endpoint, array(
            'headers' => array(
                'Authorization' => 'Bearer ' . $this->hubspot_api_key,
                'Content-Type' => 'application/json'
            ),
            'body' => wp_json_encode($body)
        ));
    }
}
```

---

## Part 8: Performance Optimization

### Database Query Optimization

```php
class Reign_Tutor_Performance {
    public function __construct() {
        add_action('init', array($this, 'optimize_queries'));
        add_filter('posts_clauses', array($this, 'optimize_course_queries'), 10, 2);
    }

    public function optimize_queries() {
        // Add custom indexes for better performance
        $this->add_custom_indexes();

        // Cache expensive queries
        add_action('pre_get_posts', array($this, 'cache_course_queries'));
    }

    private function add_custom_indexes() {
        global $wpdb;

        // Add index for course enrollment queries
        $wpdb->query("
            CREATE INDEX IF NOT EXISTS idx_course_enrollment
            ON {$wpdb->prefix}tutor_enrollments (course_id, user_id, status)
        ");

        // Add index for course progress queries
        $wpdb->query("
            CREATE INDEX IF NOT EXISTS idx_course_progress
            ON {$wpdb->prefix}tutor_quiz_attempts (course_id, user_id, attempt_status)
        ");
    }

    public function cache_course_queries($query) {
        if (!$query->is_main_query() || is_admin()) {
            return;
        }

        if ($query->get('post_type') === 'courses') {
            // Cache course catalog queries
            $cache_key = 'reign_courses_' . md5(serialize($query->query_vars));
            $cached_results = wp_cache_get($cache_key, 'reign_tutor');

            if (false === $cached_results) {
                // Query will execute normally, then cache results
                add_action('wp', function() use ($cache_key, $query) {
                    if ($query->have_posts()) {
                        wp_cache_set($cache_key, $query->posts, 'reign_tutor', HOUR_IN_SECONDS);
                    }
                });
            }
        }
    }

    public function optimize_course_queries($clauses, $query) {
        if ($query->get('post_type') === 'courses') {
            global $wpdb;

            // Optimize enrollment count queries
            if ($query->get('meta_key') === '_tutor_course_students') {
                $clauses['join'] .= " LEFT JOIN {$wpdb->prefix}tutor_enrollments te ON {$wpdb->posts}.ID = te.course_id";
                $clauses['groupby'] = "{$wpdb->posts}.ID";
            }
        }

        return $clauses;
    }
}
```

---

## Part 9: Testing & Debugging

### Debug Helper Class

```php
class Reign_Tutor_Debug {
    private static $logs = array();

    public static function log($message, $context = array()) {
        if (!WP_DEBUG) {
            return;
        }

        $log_entry = array(
            'timestamp' => current_time('mysql'),
            'message' => $message,
            'context' => $context,
            'backtrace' => wp_debug_backtrace_summary()
        );

        self::$logs[] = $log_entry;

        // Write to debug log
        error_log('[Reign TutorLMS] ' . $message . ' ' . wp_json_encode($context));
    }

    public static function get_logs() {
        return self::$logs;
    }

    public static function debug_course_data($course_id) {
        $debug_data = array(
            'course_meta' => get_post_meta($course_id),
            'enrollment_count' => tutor_utils()->count_enrolled_users_by_course($course_id),
            'lessons' => tutor_utils()->get_course_contents_by_id($course_id),
            'instructor' => tutor_utils()->get_course_instructor_by_course($course_id),
            'rating' => tutor_utils()->get_course_rating($course_id)
        );

        self::log('Course Debug Data', array(
            'course_id' => $course_id,
            'data' => $debug_data
        ));

        return $debug_data;
    }
}

// Usage in development
if (defined('WP_DEBUG') && WP_DEBUG) {
    add_action('wp_footer', function() {
        if (current_user_can('manage_options')) {
            $logs = Reign_Tutor_Debug::get_logs();
            if (!empty($logs)) {
                echo '<script>console.log("Reign TutorLMS Debug:", ' . wp_json_encode($logs) . ');</script>';
            }
        }
    });
}
```

---

## Part 10: Best Practices & Security

### Security Implementation

```php
class Reign_Tutor_Security {
    public function __construct() {
        add_action('init', array($this, 'init_security'));
    }

    public function init_security() {
        // Validate course access
        add_filter('tutor_course_access_check', array($this, 'enhanced_access_check'), 10, 3);

        // Sanitize custom fields
        add_filter('reign_tutor_custom_field_value', array($this, 'sanitize_custom_field'), 10, 2);

        // Rate limiting for AJAX requests
        add_action('wp_ajax_reign_tutor_ajax', array($this, 'rate_limit_check'));
        add_action('wp_ajax_nopriv_reign_tutor_ajax', array($this, 'rate_limit_check'));
    }

    public function enhanced_access_check($has_access, $course_id, $user_id) {
        // Additional security checks

        // Check if user account is active
        $user = get_userdata($user_id);
        if (!$user || $user->user_status !== '0') {
            return false;
        }

        // Check enrollment expiry
        $enrollment_date = tutor_utils()->get_enrollment_date($course_id, $user_id);
        if ($enrollment_date) {
            $expiry_days = get_post_meta($course_id, '_access_expiry_days', true);
            if ($expiry_days && strtotime($enrollment_date . ' +' . $expiry_days . ' days') < time()) {
                return false;
            }
        }

        // Check concurrent login limit
        if ($this->check_concurrent_login_limit($user_id)) {
            return false;
        }

        return $has_access;
    }

    public function sanitize_custom_field($value, $field_type) {
        switch ($field_type) {
            case 'url':
                return esc_url_raw($value);
            case 'email':
                return sanitize_email($value);
            case 'textarea':
                return sanitize_textarea_field($value);
            case 'html':
                return wp_kses_post($value);
            default:
                return sanitize_text_field($value);
        }
    }

    public function rate_limit_check() {
        $user_ip = $this->get_user_ip();
        $rate_limit_key = 'reign_tutor_rate_limit_' . md5($user_ip);

        $requests = get_transient($rate_limit_key) ?: 0;

        if ($requests >= 60) { // 60 requests per minute
            wp_die('Rate limit exceeded', 'Too Many Requests', array('response' => 429));
        }

        set_transient($rate_limit_key, $requests + 1, MINUTE_IN_SECONDS);
    }

    private function check_concurrent_login_limit($user_id) {
        $max_concurrent = get_option('reign_tutor_max_concurrent_logins', 3);
        $active_sessions = count(get_user_meta($user_id, 'session_tokens', true) ?: array());

        return $active_sessions > $max_concurrent;
    }
}

new Reign_Tutor_Security();
```

---

## Quick Reference

### Essential Hooks

```php
// Course hooks
do_action('reign_tutor_before_course_content', $course_id);
do_action('reign_tutor_after_course_enrollment', $course_id, $user_id);
apply_filters('reign_tutor_course_card_content', $content, $course_id);

// Lesson hooks
do_action('reign_tutor_before_lesson_start', $lesson_id, $course_id);
apply_filters('reign_tutor_lesson_navigation', $navigation, $lesson_id);

// Quiz hooks
do_action('reign_tutor_before_quiz_attempt', $quiz_id, $user_id);
apply_filters('reign_tutor_quiz_questions', $questions, $quiz_id);
```

### Template Locations

```
theme/tutor/reign-templates/
├── archive-courses.php
├── single-course.php
├── course-card.php
├── lesson-content.php
└── quiz-questions.php
```

### AJAX Endpoints

```javascript
// Course preview
action: 'reign_course_preview'

// Wishlist management
action: 'reign_add_to_wishlist'

// Course filtering
action: 'reign_filter_courses'
```

---

**Need Developer Support?**
📧 Email: developers@wbcomdesigns.com
📚 API Docs: docs.wbcomdesigns.com/api
💬 Developer Forum: forum.wbcomdesigns.com
🛠️ Code Examples: github.com/wbcomdesigns/reign-tutor-examples