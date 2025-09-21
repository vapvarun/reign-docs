# Reign Sensei Addon - Developer Guide

## What You'll Learn
This comprehensive guide provides developers with advanced customization techniques, hooks, filters, and code examples for extending the Reign Sensei addon functionality.

## Quick Overview
**Audience:** Developers, advanced users
**Difficulty:** Advanced
**Prerequisites:** PHP, WordPress development knowledge

---

## Part 1: Architecture Overview

### Addon Structure

```
reign-sensei-addon/
├── includes/
│   ├── class-reign-sensei-core.php
│   ├── class-reign-sensei-customizer.php
│   ├── class-reign-sensei-templates.php
│   ├── class-reign-sensei-woocommerce.php
│   └── class-reign-sensei-ajax.php
├── templates/
│   ├── course/
│   ├── lesson/
│   └── quiz/
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
└── reign-sensei-addon.php
```

### Core Classes

**Main initialization:**
```php
class Reign_Sensei_Addon {
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
        add_action('sensei_before_main_content', array($this, 'before_main_content'));
    }
}
```

---

## Part 2: Available Hooks and Filters

### Action Hooks

**Course-related actions:**

```php
// Before course content
do_action('reign_sensei_before_course_content', $course_id);

// After course enrollment
do_action('reign_sensei_after_course_enrollment', $course_id, $user_id);

// Before lesson start
do_action('reign_sensei_before_lesson_start', $lesson_id, $course_id);

// After lesson completion
do_action('reign_sensei_after_lesson_completion', $lesson_id, $user_id);

// Before quiz attempt
do_action('reign_sensei_before_quiz_attempt', $quiz_id, $user_id);

// After quiz completion
do_action('reign_sensei_after_quiz_completion', $quiz_id, $user_id, $grade);

// After certificate generation
do_action('reign_sensei_after_certificate_generated', $course_id, $user_id);
```

**Example usage:**
```php
// Add custom tracking after course enrollment
add_action('reign_sensei_after_course_enrollment', 'custom_enrollment_tracking', 10, 2);
function custom_enrollment_tracking($course_id, $user_id) {
    // Send to analytics
    wp_remote_post('https://analytics.example.com/track', array(
        'body' => array(
            'event' => 'course_enrollment',
            'course_id' => $course_id,
            'user_id' => $user_id,
            'timestamp' => current_time('timestamp'),
            'course_title' => get_the_title($course_id),
            'user_email' => get_userdata($user_id)->user_email
        )
    ));

    // Add to custom database table
    global $wpdb;
    $wpdb->insert(
        $wpdb->prefix . 'custom_course_tracking',
        array(
            'course_id' => $course_id,
            'user_id' => $user_id,
            'enrolled_date' => current_time('mysql')
        )
    );
}
```

### Filter Hooks

**Content modification filters:**

```php
// Modify course card content
apply_filters('reign_sensei_course_card_content', $content, $course_id);

// Customize lesson navigation
apply_filters('reign_sensei_lesson_navigation', $navigation, $lesson_id);

// Filter quiz questions display
apply_filters('reign_sensei_quiz_questions', $questions, $quiz_id);

// Customize student dashboard
apply_filters('reign_sensei_student_dashboard_content', $content, $user_id);

// Modify course pricing display
apply_filters('reign_sensei_course_price_html', $price_html, $course_id);
```

**Example implementations:**
```php
// Add custom course card elements
add_filter('reign_sensei_course_card_content', 'add_custom_course_info', 10, 2);
function add_custom_course_info($content, $course_id) {
    $difficulty = get_post_meta($course_id, '_course_difficulty', true);
    $estimated_time = get_post_meta($course_id, '_course_estimated_time', true);

    if ($difficulty || $estimated_time) {
        $custom_info = '<div class="custom-course-meta">';

        if ($difficulty) {
            $custom_info .= '<span class="course-difficulty difficulty-' . esc_attr($difficulty) . '">';
            $custom_info .= '<i class="fa fa-signal"></i> ' . esc_html(ucfirst($difficulty));
            $custom_info .= '</span>';
        }

        if ($estimated_time) {
            $custom_info .= '<span class="course-time">';
            $custom_info .= '<i class="fa fa-clock-o"></i> ' . esc_html($estimated_time);
            $custom_info .= '</span>';
        }

        $custom_info .= '</div>';

        $content .= $custom_info;
    }

    return $content;
}

// Customize lesson navigation
add_filter('reign_sensei_lesson_navigation', 'custom_lesson_navigation', 10, 2);
function custom_lesson_navigation($navigation, $lesson_id) {
    $course_id = Sensei()->lesson->get_course_id($lesson_id);
    $lessons = Sensei()->course->course_lessons($course_id);

    $nav = '<div class="custom-lesson-nav">';
    $nav .= '<h4>Course Progress</h4>';

    foreach ($lessons as $lesson) {
        $status = Sensei_Utils::user_completed_lesson($lesson->ID, get_current_user_id()) ? 'completed' : 'pending';
        $current = ($lesson->ID == $lesson_id) ? 'current' : '';

        $nav .= sprintf(
            '<a href="%s" class="lesson-nav-item %s %s">%s</a>',
            get_permalink($lesson->ID),
            $status,
            $current,
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
1. theme/sensei/reign-templates/
2. reign-addon/templates/
3. sensei-plugin/templates/
```

### Custom Template Creation

**Override course archive:**
```php
// In your theme: sensei/reign-templates/archive-course.php
<?php
get_header();

// Custom course archive layout
$courses = new WP_Query(array(
    'post_type' => 'course',
    'posts_per_page' => 12,
    'meta_query' => array(
        array(
            'key' => '_course_featured',
            'value' => 'featured',
            'compare' => 'LIKE'
        )
    )
));

if ($courses->have_posts()) :
    echo '<div class="reign-course-grid">';
    while ($courses->have_posts()) : $courses->the_post();
        // Include custom course card template
        include locate_template('sensei/reign-templates/course-card.php');
    endwhile;
    echo '</div>';

    // Custom pagination
    reign_sensei_pagination($courses);
endif;

wp_reset_postdata();
get_footer();
?>
```

**Custom course card template:**
```php
// theme/sensei/reign-templates/course-card.php
<?php
$course_id = get_the_ID();
$course_lessons = Sensei()->course->course_lessons($course_id);
$lesson_count = count($course_lessons);
$course_author = get_userdata(get_post_field('post_author', $course_id));
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
            <?php
            $course_cats = get_the_terms($course_id, 'course-category');
            if ($course_cats && !is_wp_error($course_cats)) :
            ?>
                <span class="course-category">
                    <?php echo esc_html($course_cats[0]->name); ?>
                </span>
            <?php endif; ?>

            <span class="lesson-count">
                <i class="fa fa-play-circle"></i> <?php echo esc_html($lesson_count); ?> lessons
            </span>
        </div>

        <h3 class="course-title">
            <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
        </h3>

        <div class="course-excerpt">
            <?php echo wp_trim_words(get_the_excerpt(), 20); ?>
        </div>

        <div class="course-author">
            <?php echo get_avatar($course_author->ID, 32); ?>
            <span><?php echo esc_html($course_author->display_name); ?></span>
        </div>

        <div class="course-footer">
            <div class="course-price">
                <?php
                $product_id = Sensei_WC::get_course_product_id($course_id);
                if ($product_id) {
                    $product = wc_get_product($product_id);
                    echo $product->get_price_html();
                } else {
                    echo '<span class="free-course">Free</span>';
                }
                ?>
            </div>
            <div class="course-actions">
                <?php
                $course_link = Sensei_Course::get_course_action_button_link($course_id);
                $button_text = Sensei_Course::get_course_action_button_text($course_id);
                ?>
                <a href="<?php echo esc_url($course_link); ?>" class="course-action-btn">
                    <?php echo esc_html($button_text); ?>
                </a>
            </div>
        </div>
    </div>
</div>
```

---

## Part 4: WooCommerce Integration

### Custom Product Integration

**Enhanced WooCommerce integration:**
```php
class Reign_Sensei_WooCommerce {
    public function __construct() {
        add_filter('woocommerce_product_tabs', array($this, 'add_course_tabs'), 20);
        add_action('woocommerce_after_single_product_summary', array($this, 'add_course_curriculum'), 15);
        add_filter('woocommerce_product_data_tabs', array($this, 'add_course_data_tab'));
    }

    public function add_course_tabs($tabs) {
        global $post;

        // Check if this product is a course
        $course_id = Sensei_WC::get_course_id_by_product_id($post->ID);

        if ($course_id) {
            $tabs['course_curriculum'] = array(
                'title'    => __('Course Curriculum', 'reign-sensei'),
                'priority' => 15,
                'callback' => array($this, 'course_curriculum_tab_content')
            );

            $tabs['course_instructor'] = array(
                'title'    => __('Instructor', 'reign-sensei'),
                'priority' => 20,
                'callback' => array($this, 'course_instructor_tab_content')
            );
        }

        return $tabs;
    }

    public function course_curriculum_tab_content() {
        global $post;

        $course_id = Sensei_WC::get_course_id_by_product_id($post->ID);
        if (!$course_id) return;

        $lessons = Sensei()->course->course_lessons($course_id);

        if (!empty($lessons)) {
            echo '<div class="course-curriculum-tab">';
            echo '<h3>' . __('What You\'ll Learn', 'reign-sensei') . '</h3>';
            echo '<ul class="course-lessons-list">';

            foreach ($lessons as $lesson) {
                $lesson_length = get_post_meta($lesson->ID, '_lesson_length', true);
                echo '<li>';
                echo '<i class="fa fa-play-circle"></i> ';
                echo esc_html($lesson->post_title);
                if ($lesson_length) {
                    echo ' <span class="lesson-duration">(' . esc_html($lesson_length) . ')</span>';
                }
                echo '</li>';
            }

            echo '</ul>';
            echo '</div>';
        }
    }

    public function course_instructor_tab_content() {
        global $post;

        $course_id = Sensei_WC::get_course_id_by_product_id($post->ID);
        if (!$course_id) return;

        $instructor = get_userdata(get_post_field('post_author', $course_id));

        if ($instructor) {
            echo '<div class="course-instructor-tab">';
            echo '<div class="instructor-profile">';
            echo '<div class="instructor-avatar">';
            echo get_avatar($instructor->ID, 80);
            echo '</div>';
            echo '<div class="instructor-info">';
            echo '<h4>' . esc_html($instructor->display_name) . '</h4>';
            echo '<p>' . esc_html(get_user_meta($instructor->ID, 'description', true)) . '</p>';
            echo '</div>';
            echo '</div>';
            echo '</div>';
        }
    }
}

new Reign_Sensei_WooCommerce();
```

---

## Part 5: AJAX Implementation

### Custom AJAX Handlers

**Course preview and wishlist functionality:**
```php
class Reign_Sensei_Ajax {
    public function __construct() {
        add_action('wp_ajax_reign_course_preview', array($this, 'course_preview'));
        add_action('wp_ajax_nopriv_reign_course_preview', array($this, 'course_preview'));

        add_action('wp_ajax_reign_add_to_wishlist', array($this, 'add_to_wishlist'));
        add_action('wp_ajax_nopriv_reign_add_to_wishlist', array($this, 'add_to_wishlist'));

        add_action('wp_ajax_reign_track_lesson_progress', array($this, 'track_lesson_progress'));
    }

    public function course_preview() {
        check_ajax_referer('reign_sensei_nonce', 'nonce');

        $course_id = intval($_POST['course_id']);

        if (!$course_id) {
            wp_die('Invalid course ID');
        }

        $course = get_post($course_id);
        $instructor = get_userdata($course->post_author);
        $lessons = Sensei()->course->course_lessons($course_id);

        $preview_data = array(
            'title' => $course->post_title,
            'description' => $course->post_content,
            'excerpt' => $course->post_excerpt,
            'instructor' => array(
                'name' => $instructor->display_name,
                'bio' => get_user_meta($instructor->ID, 'description', true),
                'avatar' => get_avatar_url($instructor->ID, 64)
            ),
            'lessons' => $this->format_lessons($lessons),
            'features' => $this->get_course_features($course_id),
            'woocommerce' => $this->get_woocommerce_data($course_id)
        );

        wp_send_json_success($preview_data);
    }

    public function add_to_wishlist() {
        if (!is_user_logged_in()) {
            wp_send_json_error('Please login to add to wishlist');
        }

        check_ajax_referer('reign_sensei_nonce', 'nonce');

        $course_id = intval($_POST['course_id']);
        $user_id = get_current_user_id();

        $wishlist = get_user_meta($user_id, '_sensei_course_wishlist', true);
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

        update_user_meta($user_id, '_sensei_course_wishlist', $wishlist);

        wp_send_json_success(array(
            'action' => $action,
            'count' => count($wishlist),
            'message' => $action === 'added' ? 'Added to wishlist' : 'Removed from wishlist'
        ));
    }

    public function track_lesson_progress() {
        if (!is_user_logged_in()) {
            wp_die('Unauthorized');
        }

        check_ajax_referer('reign_sensei_nonce', 'nonce');

        $lesson_id = intval($_POST['lesson_id']);
        $time_spent = intval($_POST['time_spent']);
        $user_id = get_current_user_id();

        // Track time spent on lesson
        $existing_time = get_user_meta($user_id, "_lesson_{$lesson_id}_time_spent", true);
        $total_time = intval($existing_time) + $time_spent;

        update_user_meta($user_id, "_lesson_{$lesson_id}_time_spent", $total_time);

        // Track engagement
        $this->track_engagement_event($user_id, $lesson_id, 'time_spent', $time_spent);

        wp_send_json_success(array(
            'total_time' => $total_time,
            'formatted_time' => $this->format_time($total_time)
        ));
    }

    private function format_lessons($lessons) {
        $formatted = array();

        foreach ($lessons as $lesson) {
            $formatted[] = array(
                'title' => $lesson->post_title,
                'excerpt' => wp_trim_words($lesson->post_excerpt, 15),
                'duration' => get_post_meta($lesson->ID, '_lesson_length', true),
                'is_preview' => get_post_meta($lesson->ID, '_lesson_preview', true),
                'complexity' => get_post_meta($lesson->ID, '_lesson_complexity', true)
            );
        }

        return $formatted;
    }

    private function get_course_features($course_id) {
        $lessons = Sensei()->course->course_lessons($course_id);
        $quizzes = Sensei()->course->course_quizzes($course_id);

        return array(
            'lesson_count' => count($lessons),
            'quiz_count' => count($quizzes),
            'estimated_duration' => get_post_meta($course_id, '_course_duration', true),
            'difficulty' => get_post_meta($course_id, '_course_difficulty', true),
            'certificate' => Sensei_Certificates::course_has_certificate($course_id),
            'prerequisites' => $this->get_course_prerequisites($course_id)
        );
    }

    private function get_woocommerce_data($course_id) {
        $product_id = Sensei_WC::get_course_product_id($course_id);

        if (!$product_id) {
            return array('is_purchasable' => false);
        }

        $product = wc_get_product($product_id);

        return array(
            'is_purchasable' => true,
            'price' => $product->get_price(),
            'price_html' => $product->get_price_html(),
            'add_to_cart_url' => $product->add_to_cart_url(),
            'is_in_stock' => $product->is_in_stock()
        );
    }
}

new Reign_Sensei_Ajax();
```

---

## Part 6: Analytics & Progress Tracking

### Advanced Analytics Implementation

```php
class Reign_Sensei_Analytics {
    private $table_name;

    public function __construct() {
        global $wpdb;
        $this->table_name = $wpdb->prefix . 'reign_sensei_analytics';

        add_action('init', array($this, 'init'));
        add_action('sensei_user_lesson_end', array($this, 'track_lesson_completion'), 10, 2);
        add_action('sensei_user_quiz_grade', array($this, 'track_quiz_completion'), 10, 4);
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

    public function track_lesson_completion($user_id, $lesson_id) {
        $course_id = Sensei()->lesson->get_course_id($lesson_id);

        $this->track_event('lesson_completed', array(
            'course_id' => $course_id,
            'lesson_id' => $lesson_id,
            'completion_time' => current_time('mysql'),
            'time_spent' => get_user_meta($user_id, "_lesson_{$lesson_id}_time_spent", true)
        ));

        // Check if course is completed
        if (Sensei_Utils::user_completed_course($course_id, $user_id)) {
            $this->track_event('course_completed', array(
                'course_id' => $course_id,
                'completion_time' => current_time('mysql'),
                'total_time_spent' => $this->calculate_course_time_spent($course_id, $user_id)
            ));
        }
    }

    public function track_quiz_completion($user_id, $quiz_id, $grade, $passmark) {
        $lesson_id = Sensei()->quiz->get_lesson_id($quiz_id);
        $course_id = Sensei()->lesson->get_course_id($lesson_id);

        $this->track_event('quiz_completed', array(
            'course_id' => $course_id,
            'lesson_id' => $lesson_id,
            'quiz_id' => $quiz_id,
            'grade' => $grade,
            'passmark' => $passmark,
            'passed' => $grade >= $passmark,
            'attempt_count' => $this->get_quiz_attempt_count($user_id, $quiz_id)
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

    public function get_learning_path_analytics($user_id) {
        global $wpdb;

        $sql = $wpdb->prepare("
            SELECT
                c.course_id,
                c.post_title as course_title,
                COUNT(l.lesson_id) as lessons_completed,
                AVG(CASE WHEN q.event_type = 'quiz_completed' THEN
                    JSON_EXTRACT(q.event_data, '$.grade') END) as avg_quiz_score,
                MIN(c.created_at) as first_activity,
                MAX(c.created_at) as last_activity
            FROM {$this->table_name} c
            LEFT JOIN {$this->table_name} l ON c.course_id = l.course_id
                AND l.event_type = 'lesson_completed' AND l.user_id = c.user_id
            LEFT JOIN {$this->table_name} q ON c.course_id = q.course_id
                AND q.event_type = 'quiz_completed' AND q.user_id = c.user_id
            LEFT JOIN {$wpdb->posts} p ON c.course_id = p.ID
            WHERE c.user_id = %d
            GROUP BY c.course_id
        ", $user_id);

        return $wpdb->get_results($sql);
    }

    private function calculate_course_time_spent($course_id, $user_id) {
        $lessons = Sensei()->course->course_lessons($course_id);
        $total_time = 0;

        foreach ($lessons as $lesson) {
            $lesson_time = get_user_meta($user_id, "_lesson_{$lesson->ID}_time_spent", true);
            $total_time += intval($lesson_time);
        }

        return $total_time;
    }
}

new Reign_Sensei_Analytics();
```

---

## Part 7: Custom Course Features

### Advanced Course Functionality

```php
class Reign_Sensei_Course_Features {
    public function __construct() {
        add_action('add_meta_boxes', array($this, 'add_course_meta_boxes'));
        add_action('save_post', array($this, 'save_course_meta'));
        add_filter('sensei_course_loop_content', array($this, 'add_course_features'), 20, 2);
    }

    public function add_course_meta_boxes() {
        add_meta_box(
            'reign_course_features',
            'Advanced Course Features',
            array($this, 'course_features_callback'),
            'course',
            'normal',
            'high'
        );
    }

    public function course_features_callback($post) {
        wp_nonce_field('reign_course_features', 'reign_course_nonce');

        $difficulty = get_post_meta($post->ID, '_course_difficulty', true);
        $estimated_time = get_post_meta($post->ID, '_course_estimated_time', true);
        $prerequisites = get_post_meta($post->ID, '_course_prerequisites', true);
        $learning_outcomes = get_post_meta($post->ID, '_course_learning_outcomes', true);
        $target_audience = get_post_meta($post->ID, '_course_target_audience', true);
        ?>

        <table class="form-table">
            <tr>
                <th><label for="course_difficulty">Course Difficulty</label></th>
                <td>
                    <select id="course_difficulty" name="course_difficulty">
                        <option value="">Select Difficulty</option>
                        <option value="beginner" <?php selected($difficulty, 'beginner'); ?>>Beginner</option>
                        <option value="intermediate" <?php selected($difficulty, 'intermediate'); ?>>Intermediate</option>
                        <option value="advanced" <?php selected($difficulty, 'advanced'); ?>>Advanced</option>
                    </select>
                </td>
            </tr>
            <tr>
                <th><label for="course_estimated_time">Estimated Time</label></th>
                <td>
                    <input type="text" id="course_estimated_time" name="course_estimated_time"
                           value="<?php echo esc_attr($estimated_time); ?>" class="regular-text">
                    <p class="description">e.g., "4 hours", "2 weeks", "Self-paced"</p>
                </td>
            </tr>
            <tr>
                <th><label for="course_prerequisites">Prerequisites</label></th>
                <td>
                    <textarea id="course_prerequisites" name="course_prerequisites" rows="3" class="large-text"><?php echo esc_textarea($prerequisites); ?></textarea>
                    <p class="description">What students should know before taking this course</p>
                </td>
            </tr>
            <tr>
                <th><label for="course_learning_outcomes">Learning Outcomes</label></th>
                <td>
                    <textarea id="course_learning_outcomes" name="course_learning_outcomes" rows="5" class="large-text"><?php echo esc_textarea($learning_outcomes); ?></textarea>
                    <p class="description">What students will learn (one outcome per line)</p>
                </td>
            </tr>
            <tr>
                <th><label for="course_target_audience">Target Audience</label></th>
                <td>
                    <textarea id="course_target_audience" name="course_target_audience" rows="3" class="large-text"><?php echo esc_textarea($target_audience); ?></textarea>
                    <p class="description">Who this course is designed for</p>
                </td>
            </tr>
        </table>

        <?php
    }

    public function save_course_meta($post_id) {
        if (!isset($_POST['reign_course_nonce']) ||
            !wp_verify_nonce($_POST['reign_course_nonce'], 'reign_course_features')) {
            return;
        }

        if (defined('DOING_AUTOSAVE') && DOING_AUTOSAVE) {
            return;
        }

        if (!current_user_can('edit_post', $post_id)) {
            return;
        }

        $fields = array(
            'course_difficulty' => 'sanitize_text_field',
            'course_estimated_time' => 'sanitize_text_field',
            'course_prerequisites' => 'sanitize_textarea_field',
            'course_learning_outcomes' => 'sanitize_textarea_field',
            'course_target_audience' => 'sanitize_textarea_field'
        );

        foreach ($fields as $field => $sanitize_callback) {
            if (isset($_POST[$field])) {
                update_post_meta($post_id, '_' . $field, call_user_func($sanitize_callback, $_POST[$field]));
            }
        }
    }

    public function add_course_features($content, $course_id) {
        $features = '';

        $difficulty = get_post_meta($course_id, '_course_difficulty', true);
        $estimated_time = get_post_meta($course_id, '_course_estimated_time', true);

        if ($difficulty || $estimated_time) {
            $features .= '<div class="course-features">';

            if ($difficulty) {
                $features .= '<span class="course-difficulty difficulty-' . esc_attr($difficulty) . '">';
                $features .= esc_html(ucfirst($difficulty));
                $features .= '</span>';
            }

            if ($estimated_time) {
                $features .= '<span class="course-time">';
                $features .= esc_html($estimated_time);
                $features .= '</span>';
            }

            $features .= '</div>';
        }

        return $content . $features;
    }
}

new Reign_Sensei_Course_Features();
```

---

## Part 8: Frontend JavaScript Integration

**Advanced frontend functionality:**
```javascript
// assets/js/reign-sensei-frontend.js
class ReignSenseiFrontend {
    constructor() {
        this.init();
    }

    init() {
        this.bindEvents();
        this.initializeComponents();
        this.trackLearningTime();
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

        // Lesson progress tracking
        $(document).on('click', '.mark-complete', (e) => {
            e.preventDefault();
            this.markLessonComplete($(e.target).data('lesson-id'));
        });

        // Quiz auto-save
        $('.sensei-quiz-form').on('change', 'input, textarea, select', () => {
            this.autoSaveQuiz();
        });
    }

    showCoursePreview(courseId) {
        this.showModal('loading');

        $.ajax({
            url: reign_sensei_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_course_preview',
                course_id: courseId,
                nonce: reign_sensei_ajax.nonce
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
                    <div class="course-preview-content">
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
                        <div class="course-lessons">
                            <h3>Course Content (${data.features.lesson_count} lessons)</h3>
                            ${this.renderLessons(data.lessons)}
                        </div>
                        <div class="course-features">
                            ${this.renderFeatures(data.features)}
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    ${this.renderEnrollmentButton(data.woocommerce)}
                </div>
            </div>
        `;

        this.showModal(template);
    }

    toggleWishlist(courseId, button) {
        const $button = $(button);

        $button.prop('disabled', true);

        $.ajax({
            url: reign_sensei_ajax.ajax_url,
            type: 'POST',
            data: {
                action: 'reign_add_to_wishlist',
                course_id: courseId,
                nonce: reign_sensei_ajax.nonce
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
                }
            },
            complete: () => {
                $button.prop('disabled', false);
            }
        });
    }

    trackLearningTime() {
        if (!$('body').hasClass('single-lesson')) return;

        let startTime = Date.now();
        let lessonId = $('body').data('lesson-id');

        // Track time every 30 seconds
        setInterval(() => {
            let timeSpent = Math.floor((Date.now() - startTime) / 1000);

            if (timeSpent >= 30) { // Only track if spent at least 30 seconds
                $.ajax({
                    url: reign_sensei_ajax.ajax_url,
                    type: 'POST',
                    data: {
                        action: 'reign_track_lesson_progress',
                        lesson_id: lessonId,
                        time_spent: timeSpent,
                        nonce: reign_sensei_ajax.nonce
                    }
                });

                startTime = Date.now(); // Reset timer
            }
        }, 30000);
    }

    autoSaveQuiz() {
        clearTimeout(this.quizSaveTimeout);

        this.quizSaveTimeout = setTimeout(() => {
            const formData = $('.sensei-quiz-form').serialize();

            $.ajax({
                url: reign_sensei_ajax.ajax_url,
                type: 'POST',
                data: formData + '&action=reign_autosave_quiz&nonce=' + reign_sensei_ajax.nonce,
                success: (response) => {
                    this.showNotification('Quiz progress saved', 'info', 2000);
                }
            });
        }, 5000);
    }
}

// Initialize when document is ready
$(document).ready(() => {
    new ReignSenseiFrontend();
});
```

---

## Part 9: Performance Optimization

### Database Query Optimization

```php
class Reign_Sensei_Performance {
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

        // Add index for course-lesson relationships
        $wpdb->query("
            CREATE INDEX IF NOT EXISTS idx_course_lesson_meta
            ON {$wpdb->postmeta} (meta_key, meta_value(10))
            WHERE meta_key = '_lesson_course'
        ");

        // Add index for quiz grades
        $wpdb->query("
            CREATE INDEX IF NOT EXISTS idx_sensei_user_answers
            ON {$wpdb->prefix}sensei_user_answers (user_id, comment_post_ID)
        ");
    }

    public function cache_course_queries($query) {
        if (!$query->is_main_query() || is_admin()) {
            return;
        }

        if ($query->get('post_type') === 'course') {
            // Cache course catalog queries
            $cache_key = 'reign_courses_' . md5(serialize($query->query_vars));
            $cached_results = wp_cache_get($cache_key, 'reign_sensei');

            if (false === $cached_results) {
                // Query will execute normally, then cache results
                add_action('wp', function() use ($cache_key, $query) {
                    if ($query->have_posts()) {
                        wp_cache_set($cache_key, $query->posts, 'reign_sensei', HOUR_IN_SECONDS);
                    }
                });
            }
        }
    }
}

new Reign_Sensei_Performance();
```

---

## Quick Reference

### Essential Hooks

```php
// Course hooks
do_action('reign_sensei_before_course_content', $course_id);
do_action('reign_sensei_after_course_enrollment', $course_id, $user_id);
apply_filters('reign_sensei_course_card_content', $content, $course_id);

// Lesson hooks
do_action('reign_sensei_before_lesson_start', $lesson_id, $course_id);
apply_filters('reign_sensei_lesson_navigation', $navigation, $lesson_id);

// Quiz hooks
do_action('reign_sensei_before_quiz_attempt', $quiz_id, $user_id);
apply_filters('reign_sensei_quiz_questions', $questions, $quiz_id);
```

### Template Locations

```
theme/sensei/reign-templates/
├── archive-course.php
├── single-course.php
├── course-card.php
├── single-lesson.php
├── single-quiz.php
└── course-results.php
```

### AJAX Endpoints

```javascript
// Course preview
action: 'reign_course_preview'

// Wishlist management
action: 'reign_add_to_wishlist'

// Progress tracking
action: 'reign_track_lesson_progress'
```

---

**Need Developer Support?**
📧 Email: developers@wbcomdesigns.com
📚 API Docs: docs.wbcomdesigns.com/api
💬 Developer Forum: forum.wbcomdesigns.com
🛠️ Code Examples: github.com/wbcomdesigns/reign-sensei-examples