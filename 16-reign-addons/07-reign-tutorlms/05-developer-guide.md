# Reign TutorLMS Addon - Developer Guide

## Overview

This comprehensive developer guide covers extending, customizing, and integrating with Reign TutorLMS Addon v2.0.0, including hook system, API integration, custom development patterns, and advanced social learning features.

---

## Part 1: Plugin Architecture

### Core Plugin Structure

```
reign-tutorlms-addon/
├── reign-tutorlms-addon.php     # Main plugin file
├── includes/
│   ├── class-reign-tutor-core.php      # Core functionality
│   ├── class-reign-tutor-shortcodes.php # Shortcode system
│   ├── class-reign-tutor-ajax.php      # AJAX handlers
│   ├── class-reign-tutor-social.php    # Social integration
│   └── class-reign-tutor-utils.php     # Utility functions
├── assets/
│   ├── css/
│   │   ├── public.css           # Frontend styles
│   │   └── admin.css           # Admin styles
│   └── js/
│       ├── public.js           # Frontend scripts
│       ├── admin.js            # Admin scripts
│       └── ajax.js             # AJAX functionality
├── templates/
│   ├── course-card.php         # Course display template
│   ├── course-grid.php         # Grid layout template
│   ├── course-progress.php     # Progress display
│   └── profile-integration.php # Social profile template
└── languages/
    └── reign-tutorlms-addon.pot # Translation file
```

### Main Plugin Class

```php
<?php
/**
 * Main plugin class structure
 */
class Reign_TutorLMS_Addon {

    /**
     * Plugin version
     */
    const VERSION = '2.0.0';

    /**
     * Singleton instance
     */
    private static $instance = null;

    /**
     * Core components
     */
    public $shortcodes;
    public $ajax;
    public $social;
    public $utils;

    /**
     * Get singleton instance
     */
    public static function get_instance() {
        if (null === self::$instance) {
            self::$instance = new self();
        }
        return self::$instance;
    }

    /**
     * Initialize plugin
     */
    private function __construct() {
        $this->define_constants();
        $this->load_dependencies();
        $this->init_hooks();
    }

    /**
     * Define plugin constants
     */
    private function define_constants() {
        define('REIGN_TUTOR_VERSION', self::VERSION);
        define('REIGN_TUTOR_PLUGIN_DIR', plugin_dir_path(__FILE__));
        define('REIGN_TUTOR_PLUGIN_URL', plugin_dir_url(__FILE__));
        define('REIGN_TUTOR_TEMPLATE_PATH', REIGN_TUTOR_PLUGIN_DIR . 'templates/');
    }

    /**
     * Load required dependencies
     */
    private function load_dependencies() {
        require_once REIGN_TUTOR_PLUGIN_DIR . 'includes/class-reign-tutor-shortcodes.php';
        require_once REIGN_TUTOR_PLUGIN_DIR . 'includes/class-reign-tutor-ajax.php';
        require_once REIGN_TUTOR_PLUGIN_DIR . 'includes/class-reign-tutor-social.php';
        require_once REIGN_TUTOR_PLUGIN_DIR . 'includes/class-reign-tutor-utils.php';

        $this->shortcodes = new Reign_TutorLMS_Shortcodes();
        $this->ajax = new Reign_TutorLMS_Ajax();
        $this->social = new Reign_TutorLMS_Social();
        $this->utils = new Reign_TutorLMS_Utils();
    }

    /**
     * Initialize WordPress hooks
     */
    private function init_hooks() {
        add_action('init', array($this, 'init'), 0);
        add_action('wp_enqueue_scripts', array($this, 'enqueue_scripts'));
        add_action('wp_enqueue_scripts', array($this, 'enqueue_styles'));

        // Social platform integration hooks
        add_action('bp_init', array($this->social, 'init_buddypress'));
        add_action('plugins_loaded', array($this->social, 'init_peepso'), 20);
    }

    /**
     * Plugin initialization
     */
    public function init() {
        // Initialize components
        $this->shortcodes->init();
        $this->ajax->init();
        $this->social->init();

        // Load text domain
        load_plugin_textdomain(
            'reign-tutorlms-addon',
            false,
            dirname(plugin_basename(__FILE__)) . '/languages/'
        );
    }
}

// Initialize plugin
function reign_tutorlms_addon() {
    return Reign_TutorLMS_Addon::get_instance();
}

// Start the plugin
reign_tutorlms_addon();
```

---

## Part 2: Hook System and Filters

### Available Action Hooks

#### Course Display Hooks

```php
/**
 * Before course grid renders
 * @param array $args Shortcode arguments
 */
do_action('reign_tutor_before_course_grid', $args);

/**
 * After course grid renders
 * @param array $args Shortcode arguments
 * @param array $courses Course data
 */
do_action('reign_tutor_after_course_grid', $args, $courses);

/**
 * Before individual course card
 * @param int $course_id Course ID
 * @param array $args Display arguments
 */
do_action('reign_tutor_before_course_card', $course_id, $args);

/**
 * After individual course card
 * @param int $course_id Course ID
 * @param array $args Display arguments
 */
do_action('reign_tutor_after_course_card', $course_id, $args);

/**
 * Course enrollment action
 * @param int $user_id User ID
 * @param int $course_id Course ID
 */
do_action('reign_tutor_course_enrolled', $user_id, $course_id);

/**
 * Course completion action
 * @param int $user_id User ID
 * @param int $course_id Course ID
 * @param float $completion_percentage Completion percentage
 */
do_action('reign_tutor_course_completed', $user_id, $course_id, $completion_percentage);

/**
 * Progress update action
 * @param int $user_id User ID
 * @param int $course_id Course ID
 * @param float $progress Progress percentage
 */
do_action('reign_tutor_progress_updated', $user_id, $course_id, $progress);
```

#### Social Integration Hooks

```php
/**
 * BuddyPress profile tab initialization
 * @param int $user_id User ID
 */
do_action('reign_tutor_bp_profile_tab_init', $user_id);

/**
 * PeepSo profile integration
 * @param int $user_id User ID
 * @param array $profile_data Profile information
 */
do_action('reign_tutor_peepso_profile_init', $user_id, $profile_data);

/**
 * Social activity creation
 * @param string $activity_type Type of activity
 * @param int $user_id User ID
 * @param array $activity_data Activity data
 */
do_action('reign_tutor_social_activity_created', $activity_type, $user_id, $activity_data);
```

### Available Filter Hooks

#### Content Filters

```php
/**
 * Filter course card content
 * @param string $content Card HTML content
 * @param int $course_id Course ID
 * @param array $args Display arguments
 */
$content = apply_filters('reign_tutor_course_card_content', $content, $course_id, $args);

/**
 * Filter course grid query arguments
 * @param array $query_args WP_Query arguments
 * @param array $shortcode_args Shortcode arguments
 */
$query_args = apply_filters('reign_tutor_course_query_args', $query_args, $shortcode_args);

/**
 * Filter progress bar HTML
 * @param string $progress_html Progress bar HTML
 * @param int $user_id User ID
 * @param int $course_id Course ID
 * @param float $progress Progress percentage
 */
$progress_html = apply_filters('reign_tutor_progress_display', $progress_html, $user_id, $course_id, $progress);

/**
 * Filter course categories display
 * @param string $categories_html Categories HTML
 * @param array $categories Category data
 * @param array $args Display arguments
 */
$categories_html = apply_filters('reign_tutor_categories_display', $categories_html, $categories, $args);
```

#### User Context Filters

```php
/**
 * Filter user context detection
 * @param string $context Detected context (profile_owner, visitor, current_user, guest)
 * @param int $profile_user_id Profile user ID
 * @param int $current_user_id Current user ID
 */
$context = apply_filters('reign_tutor_user_context', $context, $profile_user_id, $current_user_id);

/**
 * Filter user courses based on context
 * @param array $courses Course list
 * @param int $user_id User ID
 * @param string $context User context
 * @param array $args Query arguments
 */
$courses = apply_filters('reign_tutor_user_courses', $courses, $user_id, $context, $args);

/**
 * Filter course visibility based on privacy settings
 * @param bool $is_visible Course visibility
 * @param int $course_id Course ID
 * @param int $user_id User ID
 * @param string $context Context
 */
$is_visible = apply_filters('reign_tutor_course_visibility', $is_visible, $course_id, $user_id, $context);
```

### Hook Usage Examples

#### Add Custom Course Information

```php
/**
 * Add custom information to course cards
 */
function add_custom_course_info($content, $course_id, $args) {
    // Add custom field data
    $custom_field = get_post_meta($course_id, '_custom_course_data', true);

    if ($custom_field) {
        $custom_html = '<div class="custom-course-info">';
        $custom_html .= '<span class="custom-label">Special Feature:</span>';
        $custom_html .= '<span class="custom-value">' . esc_html($custom_field) . '</span>';
        $custom_html .= '</div>';

        // Insert before course actions
        $content = str_replace(
            '<div class="course-actions">',
            $custom_html . '<div class="course-actions">',
            $content
        );
    }

    return $content;
}
add_filter('reign_tutor_course_card_content', 'add_custom_course_info', 10, 3);
```

#### Custom Progress Tracking

```php
/**
 * Track course progress milestones
 */
function track_progress_milestones($user_id, $course_id, $progress) {
    $milestones = [25, 50, 75, 100];
    $previous_progress = get_user_meta($user_id, "_course_progress_{$course_id}", true);

    foreach ($milestones as $milestone) {
        if ($progress >= $milestone && $previous_progress < $milestone) {
            // Trigger milestone achievement
            do_action('reign_tutor_milestone_reached', $user_id, $course_id, $milestone);

            // Create social activity
            if (function_exists('bp_activity_add')) {
                bp_activity_add([
                    'user_id' => $user_id,
                    'type' => 'course_milestone',
                    'action' => sprintf(
                        '%s reached %d%% completion in %s',
                        bp_core_get_userlink($user_id),
                        $milestone,
                        get_the_title($course_id)
                    ),
                    'primary_link' => get_permalink($course_id),
                    'component' => 'tutor'
                ]);
            }
        }
    }

    // Update stored progress
    update_user_meta($user_id, "_course_progress_{$course_id}", $progress);
}
add_action('reign_tutor_progress_updated', 'track_progress_milestones', 10, 3);
```

---

## Part 3: AJAX Development

### AJAX Handler Structure

```php
<?php
/**
 * AJAX functionality class
 */
class Reign_TutorLMS_Ajax {

    /**
     * Initialize AJAX hooks
     */
    public function init() {
        // Progress update AJAX
        add_action('wp_ajax_reign_tutor_update_progress', array($this, 'update_progress'));
        add_action('wp_ajax_nopriv_reign_tutor_update_progress', array($this, 'update_progress'));

        // Course filtering AJAX
        add_action('wp_ajax_reign_tutor_filter_courses', array($this, 'filter_courses'));
        add_action('wp_ajax_nopriv_reign_tutor_filter_courses', array($this, 'filter_courses'));

        // Social integration AJAX
        add_action('wp_ajax_reign_tutor_social_action', array($this, 'social_action'));

        // Enqueue AJAX script
        add_action('wp_enqueue_scripts', array($this, 'enqueue_ajax_script'));
    }

    /**
     * Enqueue AJAX script
     */
    public function enqueue_ajax_script() {
        wp_enqueue_script(
            'reign-tutor-ajax',
            REIGN_TUTOR_PLUGIN_URL . 'assets/js/ajax.js',
            array('jquery'),
            REIGN_TUTOR_VERSION,
            true
        );

        wp_localize_script('reign-tutor-ajax', 'reign_tutor_ajax', array(
            'ajax_url' => admin_url('admin-ajax.php'),
            'nonce' => wp_create_nonce('reign_tutor_ajax_nonce'),
            'messages' => array(
                'updating' => __('Updating progress...', 'reign-tutorlms-addon'),
                'updated' => __('Progress updated!', 'reign-tutorlms-addon'),
                'error' => __('Update failed. Please try again.', 'reign-tutorlms-addon')
            )
        ));
    }

    /**
     * Handle progress update AJAX request
     */
    public function update_progress() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_tutor_ajax_nonce')) {
            wp_die(__('Security check failed', 'reign-tutorlms-addon'));
        }

        $user_id = intval($_POST['user_id']);
        $course_id = intval($_POST['course_id']);
        $progress = floatval($_POST['progress']);

        // Validate user permissions
        if (!current_user_can('edit_user', $user_id) && get_current_user_id() !== $user_id) {
            wp_send_json_error(__('Permission denied', 'reign-tutorlms-addon'));
        }

        // Update progress
        $updated = tutor_utils()->update_course_progress($user_id, $course_id, $progress);

        if ($updated) {
            // Trigger progress update action
            do_action('reign_tutor_progress_updated', $user_id, $course_id, $progress);

            wp_send_json_success(array(
                'progress' => $progress,
                'message' => __('Progress updated successfully', 'reign-tutorlms-addon')
            ));
        } else {
            wp_send_json_error(__('Failed to update progress', 'reign-tutorlms-addon'));
        }
    }

    /**
     * Handle course filtering AJAX request
     */
    public function filter_courses() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_tutor_ajax_nonce')) {
            wp_die(__('Security check failed', 'reign-tutorlms-addon'));
        }

        $filters = array(
            'course_status' => sanitize_text_field($_POST['course_status']),
            'category' => sanitize_text_field($_POST['category']),
            'instructor' => intval($_POST['instructor']),
            'price_range' => sanitize_text_field($_POST['price_range'])
        );

        $args = array(
            'posts_per_page' => intval($_POST['posts_per_page']),
            'paged' => intval($_POST['paged'])
        );

        // Build query based on filters
        $query_args = $this->build_filter_query($filters, $args);

        // Execute query
        $courses = new WP_Query($query_args);

        if ($courses->have_posts()) {
            $html = '';
            while ($courses->have_posts()) {
                $courses->the_post();
                $html .= $this->render_course_card(get_the_ID(), $args);
            }
            wp_reset_postdata();

            wp_send_json_success(array(
                'html' => $html,
                'found_posts' => $courses->found_posts,
                'max_pages' => $courses->max_num_pages
            ));
        } else {
            wp_send_json_success(array(
                'html' => '<p>' . __('No courses found', 'reign-tutorlms-addon') . '</p>',
                'found_posts' => 0,
                'max_pages' => 0
            ));
        }
    }

    /**
     * Build WP_Query arguments from filters
     */
    private function build_filter_query($filters, $args) {
        $query_args = array(
            'post_type' => tutor()->course_post_type,
            'post_status' => 'publish',
            'posts_per_page' => $args['posts_per_page'],
            'paged' => $args['paged']
        );

        // Category filter
        if (!empty($filters['category'])) {
            $query_args['tax_query'] = array(
                array(
                    'taxonomy' => 'course-category',
                    'field' => 'slug',
                    'terms' => $filters['category']
                )
            );
        }

        // Instructor filter
        if (!empty($filters['instructor'])) {
            $query_args['meta_query'] = array(
                array(
                    'key' => '_tutor_course_instructor',
                    'value' => $filters['instructor'],
                    'compare' => '='
                )
            );
        }

        // Apply filters
        $query_args = apply_filters('reign_tutor_filter_query_args', $query_args, $filters);

        return $query_args;
    }
}
```

### Frontend AJAX JavaScript

```javascript
/**
 * AJAX functionality for Reign TutorLMS
 */
(function($) {
    'use strict';

    var ReignTutorAjax = {

        /**
         * Initialize AJAX functionality
         */
        init: function() {
            this.bindEvents();
            this.initProgressTracking();
            this.initCourseFiltering();
        },

        /**
         * Bind event handlers
         */
        bindEvents: function() {
            // Progress update events
            $(document).on('lesson_completed', this.updateProgress);
            $(document).on('quiz_completed', this.updateProgress);

            // Course filtering events
            $(document).on('change', '.course-filter', this.filterCourses);
            $(document).on('click', '.filter-reset', this.resetFilters);

            // Pagination events
            $(document).on('click', '.reign-course-pagination a', this.loadPage);
        },

        /**
         * Initialize progress tracking
         */
        initProgressTracking: function() {
            // Real-time progress updates
            $('.reign-tutor-progress').each(function() {
                var $this = $(this);
                var courseId = $this.data('course-id');
                var userId = $this.data('user-id');

                // Monitor progress changes
                setInterval(function() {
                    ReignTutorAjax.checkProgress(courseId, userId, $this);
                }, 5000); // Check every 5 seconds
            });
        },

        /**
         * Update course progress
         */
        updateProgress: function(e, data) {
            var courseId = data.course_id;
            var userId = data.user_id;
            var progress = data.progress;

            $.ajax({
                url: reign_tutor_ajax.ajax_url,
                type: 'POST',
                data: {
                    action: 'reign_tutor_update_progress',
                    course_id: courseId,
                    user_id: userId,
                    progress: progress,
                    nonce: reign_tutor_ajax.nonce
                },
                beforeSend: function() {
                    $('.progress-container[data-course-id="' + courseId + '"]')
                        .addClass('updating');
                },
                success: function(response) {
                    if (response.success) {
                        ReignTutorAjax.animateProgress(courseId, progress);
                        ReignTutorAjax.showNotification(
                            reign_tutor_ajax.messages.updated,
                            'success'
                        );

                        // Trigger custom event
                        $(document).trigger('reign_tutor_progress_updated', {
                            course_id: courseId,
                            user_id: userId,
                            progress: progress
                        });
                    }
                },
                error: function() {
                    ReignTutorAjax.showNotification(
                        reign_tutor_ajax.messages.error,
                        'error'
                    );
                },
                complete: function() {
                    $('.progress-container[data-course-id="' + courseId + '"]')
                        .removeClass('updating');
                }
            });
        },

        /**
         * Animate progress bar
         */
        animateProgress: function(courseId, progress) {
            var $progressBar = $('.reign-tutor-progress[data-course-id="' + courseId + '"] .progress-fill');
            var $progressText = $('.reign-tutor-progress[data-course-id="' + courseId + '"] .progress-text');

            // Animate progress bar
            $progressBar.animate({
                width: progress + '%'
            }, 800, 'easeOutCubic');

            // Animate progress text
            $({ counter: parseFloat($progressText.text()) }).animate({
                counter: progress
            }, {
                duration: 800,
                easing: 'easeOutCubic',
                step: function() {
                    $progressText.text(Math.ceil(this.counter) + '%');
                }
            });
        },

        /**
         * Filter courses via AJAX
         */
        filterCourses: function(e) {
            e.preventDefault();

            var $form = $(e.target).closest('.course-filters');
            var $container = $('.reign-tutor-courses-grid');

            var filters = {
                course_status: $form.find('[name="course_status"]').val(),
                category: $form.find('[name="category"]').val(),
                instructor: $form.find('[name="instructor"]').val(),
                price_range: $form.find('[name="price_range"]').val()
            };

            $.ajax({
                url: reign_tutor_ajax.ajax_url,
                type: 'POST',
                data: {
                    action: 'reign_tutor_filter_courses',
                    ...filters,
                    posts_per_page: $container.data('posts-per-page') || 10,
                    paged: 1,
                    nonce: reign_tutor_ajax.nonce
                },
                beforeSend: function() {
                    $container.addClass('loading');
                    $container.append('<div class="loading-overlay"><div class="spinner"></div></div>');
                },
                success: function(response) {
                    if (response.success) {
                        $container.html(response.data.html);

                        // Update pagination
                        ReignTutorAjax.updatePagination(response.data.max_pages, 1);

                        // Update URL without page reload
                        ReignTutorAjax.updateURL(filters);

                        // Trigger custom event
                        $(document).trigger('reign_tutor_courses_filtered', response.data);
                    }
                },
                complete: function() {
                    $container.removeClass('loading');
                    $container.find('.loading-overlay').remove();
                }
            });
        },

        /**
         * Show notification message
         */
        showNotification: function(message, type) {
            var $notification = $('<div class="reign-notification ' + type + '">' + message + '</div>');

            $('body').append($notification);

            setTimeout(function() {
                $notification.addClass('show');
            }, 100);

            setTimeout(function() {
                $notification.removeClass('show');
                setTimeout(function() {
                    $notification.remove();
                }, 300);
            }, 3000);
        },

        /**
         * Update browser URL
         */
        updateURL: function(filters) {
            if (history.pushState) {
                var url = new URL(window.location);

                Object.keys(filters).forEach(function(key) {
                    if (filters[key]) {
                        url.searchParams.set(key, filters[key]);
                    } else {
                        url.searchParams.delete(key);
                    }
                });

                history.pushState(null, '', url.toString());
            }
        }
    };

    // Initialize when document ready
    $(document).ready(function() {
        ReignTutorAjax.init();
    });

    // Expose to global scope
    window.ReignTutorAjax = ReignTutorAjax;

})(jQuery);
```

---

## Part 4: Social Integration Development

### BuddyPress Integration

```php
<?php
/**
 * BuddyPress integration class
 */
class Reign_TutorLMS_BuddyPress {

    /**
     * Initialize BuddyPress integration
     */
    public function init() {
        if (!function_exists('bp_is_active')) {
            return;
        }

        // Add profile navigation tab
        add_action('bp_setup_nav', array($this, 'setup_nav'), 100);

        // Add profile tab content
        add_action('bp_template_content', array($this, 'profile_content'));

        // Activity stream integration
        add_action('tutor_course_complete_after', array($this, 'create_completion_activity'), 10, 2);
        add_action('tutor_lesson_completed_after', array($this, 'create_lesson_activity'), 10, 2);
    }

    /**
     * Setup profile navigation
     */
    public function setup_nav() {
        global $bp;

        bp_core_new_nav_item(array(
            'name' => __('My Courses', 'reign-tutorlms-addon'),
            'slug' => 'courses',
            'position' => 30,
            'screen_function' => array($this, 'screen_function'),
            'default_subnav_slug' => 'enrolled'
        ));

        // Sub-navigation items
        bp_core_new_subnav_item(array(
            'name' => __('Enrolled', 'reign-tutorlms-addon'),
            'slug' => 'enrolled',
            'parent_url' => trailingslashit(bp_displayed_user_domain() . 'courses'),
            'parent_slug' => 'courses',
            'screen_function' => array($this, 'enrolled_screen')
        ));

        bp_core_new_subnav_item(array(
            'name' => __('Completed', 'reign-tutorlms-addon'),
            'slug' => 'completed',
            'parent_url' => trailingslashit(bp_displayed_user_domain() . 'courses'),
            'parent_slug' => 'courses',
            'screen_function' => array($this, 'completed_screen')
        ));

        bp_core_new_subnav_item(array(
            'name' => __('In Progress', 'reign-tutorlms-addon'),
            'slug' => 'in-progress',
            'parent_url' => trailingslashit(bp_displayed_user_domain() . 'courses'),
            'parent_slug' => 'courses',
            'screen_function' => array($this, 'progress_screen')
        ));
    }

    /**
     * Main screen function
     */
    public function screen_function() {
        add_action('bp_template_title', function() {
            echo __('My Courses', 'reign-tutorlms-addon');
        });

        add_action('bp_template_content', array($this, 'profile_content'));

        bp_core_load_template(apply_filters('bp_core_template_plugin', 'members/single/plugins'));
    }

    /**
     * Enrolled courses screen
     */
    public function enrolled_screen() {
        add_action('bp_template_content', function() {
            $user_id = bp_displayed_user_id();
            echo do_shortcode("[reign_tutor_course my_courses='true' user_id='{$user_id}' course_status='enrolled' show_progress='true']");
        });

        bp_core_load_template(apply_filters('bp_core_template_plugin', 'members/single/plugins'));
    }

    /**
     * Profile tab content
     */
    public function profile_content() {
        $user_id = bp_displayed_user_id();
        $current_user_id = get_current_user_id();

        // Determine context
        $context = ($user_id === $current_user_id) ? 'profile_owner' : 'visitor';

        // Get user courses
        $courses = tutor_utils()->get_enrolled_courses_by_user($user_id);

        if ($courses) {
            echo '<div class="reign-bp-courses-wrapper">';
            echo do_shortcode("[reign_tutor_course my_courses='true' user_id='{$user_id}' user_context='{$context}' show_progress='true']");
            echo '</div>';
        } else {
            echo '<div class="no-courses-message">';
            if ($context === 'profile_owner') {
                echo '<p>' . __('You haven\'t enrolled in any courses yet.', 'reign-tutorlms-addon') . '</p>';
                echo '<a href="' . tutor_utils()->course_archive_page_url() . '" class="btn btn-primary">';
                echo __('Browse Courses', 'reign-tutorlms-addon') . '</a>';
            } else {
                echo '<p>' . sprintf(__('%s hasn\'t enrolled in any public courses.', 'reign-tutorlms-addon'), bp_get_displayed_user_fullname()) . '</p>';
            }
            echo '</div>';
        }
    }

    /**
     * Create course completion activity
     */
    public function create_completion_activity($course_id, $user_id) {
        if (!function_exists('bp_activity_add')) {
            return;
        }

        $course_title = get_the_title($course_id);
        $course_link = get_permalink($course_id);
        $user_link = bp_core_get_userlink($user_id);

        bp_activity_add(array(
            'user_id' => $user_id,
            'type' => 'tutor_course_completed',
            'action' => sprintf(
                __('%s completed the course %s', 'reign-tutorlms-addon'),
                $user_link,
                '<a href="' . $course_link . '">' . $course_title . '</a>'
            ),
            'content' => '',
            'primary_link' => $course_link,
            'component' => 'tutor',
            'item_id' => $course_id
        ));
    }

    /**
     * Create lesson completion activity
     */
    public function create_lesson_activity($lesson_id, $user_id) {
        if (!function_exists('bp_activity_add')) {
            return;
        }

        $lesson_title = get_the_title($lesson_id);
        $lesson_link = get_permalink($lesson_id);
        $course_id = tutor_utils()->get_course_id_by_lesson($lesson_id);
        $course_title = get_the_title($course_id);
        $user_link = bp_core_get_userlink($user_id);

        bp_activity_add(array(
            'user_id' => $user_id,
            'type' => 'tutor_lesson_completed',
            'action' => sprintf(
                __('%s completed the lesson %s in %s', 'reign-tutorlms-addon'),
                $user_link,
                '<a href="' . $lesson_link . '">' . $lesson_title . '</a>',
                $course_title
            ),
            'content' => '',
            'primary_link' => $lesson_link,
            'component' => 'tutor',
            'item_id' => $lesson_id,
            'secondary_item_id' => $course_id
        ));
    }
}
```

### PeepSo Integration

```php
<?php
/**
 * PeepSo integration class
 */
class Reign_TutorLMS_PeepSo {

    /**
     * Initialize PeepSo integration
     */
    public function init() {
        if (!class_exists('PeepSo')) {
            return;
        }

        // Add profile tab
        add_filter('peepso_navigation_profile', array($this, 'add_profile_tab'), 10, 2);

        // Add profile widget
        add_action('peepso_profile_sidebar_init', array($this, 'add_profile_widget'));

        // Stream integration
        add_action('tutor_course_complete_after', array($this, 'create_stream_post'), 10, 2);
    }

    /**
     * Add courses tab to profile navigation
     */
    public function add_profile_tab($navigation, $user_id) {
        $navigation['courses'] = array(
            'href' => PeepSoUrlSegments::get_instance()->get_url('profile', $user_id, 'courses'),
            'label' => __('Courses', 'reign-tutorlms-addon'),
            'icon' => 'ps-icon-education'
        );

        return $navigation;
    }

    /**
     * Add courses widget to profile
     */
    public function add_profile_widget() {
        // Register widget
        add_action('peepso_action_render_profile_segment_courses', array($this, 'render_profile_courses'));
    }

    /**
     * Render profile courses content
     */
    public function render_profile_courses() {
        $user_id = PeepSoProfileShortcode::get_instance()->get_view_user_id();
        $current_user_id = get_current_user_id();

        // Check privacy settings
        if (!$this->can_view_courses($user_id, $current_user_id)) {
            echo '<div class="ps-alert">' . __('This user\'s courses are private.', 'reign-tutorlms-addon') . '</div>';
            return;
        }

        // Determine context
        $context = ($user_id === $current_user_id) ? 'profile_owner' : 'visitor';

        echo '<div class="peepso-courses-wrapper">';
        echo do_shortcode("[reign_tutor_course my_courses='true' user_id='{$user_id}' user_context='{$context}' columns='2']");
        echo '</div>';
    }

    /**
     * Check if current user can view courses
     */
    private function can_view_courses($profile_user_id, $current_user_id) {
        // Profile owner can always see own courses
        if ($profile_user_id === $current_user_id) {
            return true;
        }

        // Check PeepSo privacy settings
        $privacy = get_user_meta($profile_user_id, 'peepso_course_privacy', true);

        switch ($privacy) {
            case 'public':
                return true;
            case 'friends':
                return PeepSoUser::get_instance($profile_user_id)->is_friend_with($current_user_id);
            case 'private':
            default:
                return false;
        }
    }

    /**
     * Create stream post for course completion
     */
    public function create_stream_post($course_id, $user_id) {
        if (!class_exists('PeepSoActivity')) {
            return;
        }

        $course_title = get_the_title($course_id);
        $course_link = get_permalink($course_id);

        $content = sprintf(
            __('Just completed the course: %s', 'reign-tutorlms-addon'),
            '<a href="' . $course_link . '">' . $course_title . '</a>'
        );

        $activity = new PeepSoActivity();
        $activity->add_post(
            $user_id,
            $user_id,
            $content,
            'tutor_course_completed',
            'tutor',
            0,
            0
        );
    }
}
```

---

## Part 5: Custom Development Patterns

### Creating Custom Course Displays

```php
<?php
/**
 * Custom course display example
 */
function create_custom_course_grid($args = array()) {
    $defaults = array(
        'posts_per_page' => 9,
        'columns' => 3,
        'show_progress' => true,
        'layout' => 'grid',
        'course_status' => 'all'
    );

    $args = wp_parse_args($args, $defaults);

    // Build query
    $query_args = array(
        'post_type' => tutor()->course_post_type,
        'post_status' => 'publish',
        'posts_per_page' => $args['posts_per_page']
    );

    // Add user-specific filtering
    if ($args['course_status'] !== 'all' && is_user_logged_in()) {
        $user_id = get_current_user_id();
        $enrolled_courses = tutor_utils()->get_enrolled_courses_ids_by_user($user_id);

        switch ($args['course_status']) {
            case 'enrolled':
                $query_args['post__in'] = $enrolled_courses ?: array(0);
                break;
            case 'completed':
                $completed_courses = array();
                foreach ($enrolled_courses as $course_id) {
                    if (tutor_utils()->is_completed_course($course_id, $user_id)) {
                        $completed_courses[] = $course_id;
                    }
                }
                $query_args['post__in'] = $completed_courses ?: array(0);
                break;
        }
    }

    // Execute query
    $courses = new WP_Query($query_args);

    if (!$courses->have_posts()) {
        return '<p class="no-courses">' . __('No courses found.', 'reign-tutorlms-addon') . '</p>';
    }

    // Start output
    $output = '<div class="custom-course-grid columns-' . $args['columns'] . ' layout-' . $args['layout'] . '">';

    while ($courses->have_posts()) {
        $courses->the_post();
        $course_id = get_the_ID();

        $output .= '<div class="course-item">';
        $output .= render_custom_course_card($course_id, $args);
        $output .= '</div>';
    }

    $output .= '</div>';

    wp_reset_postdata();

    return $output;
}

/**
 * Render individual course card
 */
function render_custom_course_card($course_id, $args) {
    $user_id = get_current_user_id();
    $is_enrolled = tutor_utils()->is_enrolled($course_id, $user_id);
    $progress = $is_enrolled ? tutor_utils()->get_course_completed_percent($course_id, $user_id) : 0;

    ob_start();
    ?>
    <article class="custom-course-card" data-course-id="<?php echo $course_id; ?>">
        <div class="course-image">
            <?php if (has_post_thumbnail($course_id)): ?>
                <a href="<?php echo get_permalink($course_id); ?>">
                    <?php echo get_the_post_thumbnail($course_id, 'medium', array('class' => 'course-thumbnail')); ?>
                </a>
            <?php endif; ?>

            <?php if ($args['show_progress'] && $progress > 0): ?>
                <div class="progress-overlay">
                    <div class="progress-circle" data-progress="<?php echo $progress; ?>">
                        <span><?php echo round($progress); ?>%</span>
                    </div>
                </div>
            <?php endif; ?>
        </div>

        <div class="course-content">
            <h3 class="course-title">
                <a href="<?php echo get_permalink($course_id); ?>">
                    <?php echo get_the_title($course_id); ?>
                </a>
            </h3>

            <div class="course-meta">
                <?php
                // Instructor
                $instructor = tutor_utils()->get_course_instructor_by_course($course_id);
                if ($instructor): ?>
                    <div class="instructor">
                        <?php echo get_avatar($instructor->ID, 24); ?>
                        <span><?php echo $instructor->display_name; ?></span>
                    </div>
                <?php endif; ?>

                <?php
                // Duration
                $duration = get_post_meta($course_id, '_tutor_course_duration', true);
                if ($duration): ?>
                    <div class="duration">
                        <i class="icon-clock"></i>
                        <span><?php echo $duration; ?></span>
                    </div>
                <?php endif; ?>

                <?php
                // Price
                $price = tutor_utils()->get_course_price($course_id);
                if ($price): ?>
                    <div class="price">
                        <span class="amount"><?php echo $price; ?></span>
                    </div>
                <?php endif; ?>
            </div>

            <div class="course-excerpt">
                <?php echo wp_trim_words(get_post_field('post_excerpt', $course_id), 20); ?>
            </div>

            <?php if ($args['show_progress'] && $is_enrolled): ?>
                <div class="course-progress">
                    <div class="progress-bar">
                        <div class="progress-fill" style="width: <?php echo $progress; ?>%"></div>
                    </div>
                    <span class="progress-text"><?php echo round($progress); ?>% <?php _e('Complete', 'reign-tutorlms-addon'); ?></span>
                </div>
            <?php endif; ?>

            <div class="course-actions">
                <?php if ($is_enrolled): ?>
                    <a href="<?php echo get_permalink($course_id); ?>" class="btn btn-primary">
                        <?php echo ($progress > 0) ? __('Continue', 'reign-tutorlms-addon') : __('Start Course', 'reign-tutorlms-addon'); ?>
                    </a>
                <?php else: ?>
                    <a href="<?php echo get_permalink($course_id); ?>" class="btn btn-outline">
                        <?php _e('View Course', 'reign-tutorlms-addon'); ?>
                    </a>
                <?php endif; ?>
            </div>
        </div>
    </article>
    <?php
    return ob_get_clean();
}
```

### Custom Widget Development

```php
<?php
/**
 * Custom TutorLMS courses widget
 */
class Reign_TutorLMS_Courses_Widget extends WP_Widget {

    /**
     * Widget constructor
     */
    public function __construct() {
        parent::__construct(
            'reign_tutor_courses',
            __('Reign TutorLMS Courses', 'reign-tutorlms-addon'),
            array(
                'description' => __('Display TutorLMS courses with enhanced features', 'reign-tutorlms-addon')
            )
        );
    }

    /**
     * Widget output
     */
    public function widget($args, $instance) {
        $title = apply_filters('widget_title', $instance['title']);
        $number = !empty($instance['number']) ? $instance['number'] : 5;
        $show_progress = !empty($instance['show_progress']) ? $instance['show_progress'] : false;
        $course_status = !empty($instance['course_status']) ? $instance['course_status'] : 'all';

        echo $args['before_widget'];

        if (!empty($title)) {
            echo $args['before_title'] . $title . $args['after_title'];
        }

        // Build shortcode attributes
        $shortcode_attrs = array(
            'posts_per_page' => $number,
            'columns' => 1,
            'layout' => 'list',
            'show_progress' => $show_progress ? 'true' : 'false',
            'course_status' => $course_status
        );

        // Render courses
        echo do_shortcode('[reign_tutor_course ' . $this->build_shortcode_attrs($shortcode_attrs) . ']');

        echo $args['after_widget'];
    }

    /**
     * Widget form
     */
    public function form($instance) {
        $title = !empty($instance['title']) ? $instance['title'] : __('Recent Courses', 'reign-tutorlms-addon');
        $number = !empty($instance['number']) ? $instance['number'] : 5;
        $show_progress = !empty($instance['show_progress']) ? $instance['show_progress'] : false;
        $course_status = !empty($instance['course_status']) ? $instance['course_status'] : 'all';
        ?>
        <p>
            <label for="<?php echo $this->get_field_id('title'); ?>">
                <?php _e('Title:', 'reign-tutorlms-addon'); ?>
            </label>
            <input class="widefat" id="<?php echo $this->get_field_id('title'); ?>"
                   name="<?php echo $this->get_field_name('title'); ?>" type="text"
                   value="<?php echo esc_attr($title); ?>">
        </p>

        <p>
            <label for="<?php echo $this->get_field_id('number'); ?>">
                <?php _e('Number of courses:', 'reign-tutorlms-addon'); ?>
            </label>
            <input class="tiny-text" id="<?php echo $this->get_field_id('number'); ?>"
                   name="<?php echo $this->get_field_name('number'); ?>" type="number"
                   step="1" min="1" value="<?php echo esc_attr($number); ?>" size="3">
        </p>

        <p>
            <input class="checkbox" type="checkbox" <?php checked($show_progress); ?>
                   id="<?php echo $this->get_field_id('show_progress'); ?>"
                   name="<?php echo $this->get_field_name('show_progress'); ?>">
            <label for="<?php echo $this->get_field_id('show_progress'); ?>">
                <?php _e('Show progress bars', 'reign-tutorlms-addon'); ?>
            </label>
        </p>

        <p>
            <label for="<?php echo $this->get_field_id('course_status'); ?>">
                <?php _e('Course status:', 'reign-tutorlms-addon'); ?>
            </label>
            <select class="widefat" id="<?php echo $this->get_field_id('course_status'); ?>"
                    name="<?php echo $this->get_field_name('course_status'); ?>">
                <option value="all" <?php selected($course_status, 'all'); ?>><?php _e('All courses', 'reign-tutorlms-addon'); ?></option>
                <option value="enrolled" <?php selected($course_status, 'enrolled'); ?>><?php _e('Enrolled courses', 'reign-tutorlms-addon'); ?></option>
                <option value="completed" <?php selected($course_status, 'completed'); ?>><?php _e('Completed courses', 'reign-tutorlms-addon'); ?></option>
                <option value="in_progress" <?php selected($course_status, 'in_progress'); ?>><?php _e('In progress courses', 'reign-tutorlms-addon'); ?></option>
            </select>
        </p>
        <?php
    }

    /**
     * Update widget
     */
    public function update($new_instance, $old_instance) {
        $instance = array();
        $instance['title'] = (!empty($new_instance['title'])) ? strip_tags($new_instance['title']) : '';
        $instance['number'] = (!empty($new_instance['number'])) ? absint($new_instance['number']) : 5;
        $instance['show_progress'] = !empty($new_instance['show_progress']);
        $instance['course_status'] = (!empty($new_instance['course_status'])) ? sanitize_key($new_instance['course_status']) : 'all';

        return $instance;
    }

    /**
     * Build shortcode attributes string
     */
    private function build_shortcode_attrs($attrs) {
        $output = '';
        foreach ($attrs as $key => $value) {
            $output .= $key . '="' . esc_attr($value) . '" ';
        }
        return trim($output);
    }
}

// Register widget
function register_reign_tutor_courses_widget() {
    register_widget('Reign_TutorLMS_Courses_Widget');
}
add_action('widgets_init', 'register_reign_tutor_courses_widget');
```

---

## Part 6: Testing and Debugging

### Development Environment Setup

```php
<?php
/**
 * Development helpers and debugging tools
 */

// Enable debug mode for development
if (defined('WP_DEBUG') && WP_DEBUG) {

    /**
     * Log debug information
     */
    function reign_tutor_debug_log($message, $data = null) {
        if (is_array($data) || is_object($data)) {
            error_log('Reign TutorLMS Debug: ' . $message . ' - ' . print_r($data, true));
        } else {
            error_log('Reign TutorLMS Debug: ' . $message . ($data ? ' - ' . $data : ''));
        }
    }

    /**
     * Debug shortcode rendering
     */
    add_action('reign_tutor_before_course_grid', function($args) {
        reign_tutor_debug_log('Course grid rendering started', $args);
    });

    add_action('reign_tutor_after_course_grid', function($args, $courses) {
        reign_tutor_debug_log('Course grid rendering completed', array(
            'args' => $args,
            'course_count' => is_object($courses) ? $courses->found_posts : count($courses)
        ));
    });

    /**
     * Debug AJAX requests
     */
    add_action('wp_ajax_reign_tutor_update_progress', function() {
        reign_tutor_debug_log('AJAX Progress Update Request', $_POST);
    }, 1);

    /**
     * Debug social integration
     */
    add_action('reign_tutor_social_activity_created', function($type, $user_id, $data) {
        reign_tutor_debug_log('Social Activity Created', array(
            'type' => $type,
            'user_id' => $user_id,
            'data' => $data
        ));
    });
}

/**
 * Development tools class
 */
class Reign_TutorLMS_Dev_Tools {

    /**
     * Add development admin menu
     */
    public static function init() {
        if (defined('WP_DEBUG') && WP_DEBUG) {
            add_action('admin_menu', array(__CLASS__, 'add_dev_menu'));
        }
    }

    /**
     * Add development menu
     */
    public static function add_dev_menu() {
        add_submenu_page(
            'tutor',
            'Reign TutorLMS Dev Tools',
            'Dev Tools',
            'manage_options',
            'reign-tutor-dev',
            array(__CLASS__, 'dev_tools_page')
        );
    }

    /**
     * Development tools page
     */
    public static function dev_tools_page() {
        ?>
        <div class="wrap">
            <h1>Reign TutorLMS Development Tools</h1>

            <div class="card">
                <h2>Cache Management</h2>
                <p>Clear various caches used by the plugin.</p>
                <button type="button" class="button" onclick="reignTutorClearCache('all')">Clear All Caches</button>
                <button type="button" class="button" onclick="reignTutorClearCache('courses')">Clear Course Cache</button>
                <button type="button" class="button" onclick="reignTutorClearCache('progress')">Clear Progress Cache</button>
            </div>

            <div class="card">
                <h2>Test Data Generation</h2>
                <p>Generate test data for development.</p>
                <button type="button" class="button" onclick="reignTutorGenerateTestData('courses')">Generate Test Courses</button>
                <button type="button" class="button" onclick="reignTutorGenerateTestData('enrollments')">Generate Test Enrollments</button>
                <button type="button" class="button" onclick="reignTutorGenerateTestData('progress')">Generate Test Progress</button>
            </div>

            <div class="card">
                <h2>Integration Testing</h2>
                <p>Test various integration points.</p>
                <button type="button" class="button" onclick="reignTutorTestIntegration('buddypress')">Test BuddyPress Integration</button>
                <button type="button" class="button" onclick="reignTutorTestIntegration('peepso')">Test PeepSo Integration</button>
                <button type="button" class="button" onclick="reignTutorTestIntegration('ajax')">Test AJAX Functionality</button>
            </div>

            <div class="card">
                <h2>Performance Analysis</h2>
                <p>Analyze plugin performance.</p>
                <button type="button" class="button" onclick="reignTutorAnalyzePerformance()">Run Performance Analysis</button>
                <div id="performance-results"></div>
            </div>
        </div>

        <script>
        function reignTutorClearCache(type) {
            jQuery.post(ajaxurl, {
                action: 'reign_tutor_dev_clear_cache',
                cache_type: type,
                nonce: '<?php echo wp_create_nonce('reign_tutor_dev_nonce'); ?>'
            }, function(response) {
                alert(response.data.message);
            });
        }

        function reignTutorGenerateTestData(type) {
            jQuery.post(ajaxurl, {
                action: 'reign_tutor_dev_generate_data',
                data_type: type,
                nonce: '<?php echo wp_create_nonce('reign_tutor_dev_nonce'); ?>'
            }, function(response) {
                alert(response.data.message);
            });
        }

        function reignTutorTestIntegration(platform) {
            jQuery.post(ajaxurl, {
                action: 'reign_tutor_dev_test_integration',
                platform: platform,
                nonce: '<?php echo wp_create_nonce('reign_tutor_dev_nonce'); ?>'
            }, function(response) {
                alert(response.data.message);
            });
        }

        function reignTutorAnalyzePerformance() {
            jQuery('#performance-results').html('<p>Analyzing performance...</p>');

            jQuery.post(ajaxurl, {
                action: 'reign_tutor_dev_analyze_performance',
                nonce: '<?php echo wp_create_nonce('reign_tutor_dev_nonce'); ?>'
            }, function(response) {
                jQuery('#performance-results').html(response.data.html);
            });
        }
        </script>
        <?php
    }
}

// Initialize development tools
Reign_TutorLMS_Dev_Tools::init();
```

---

## Next Steps

This developer guide provides the foundation for extending and customizing Reign TutorLMS Addon. For additional resources:

- [Troubleshooting Guide](07-troubleshooting.md) - Common issues and solutions
- [FAQ](08-faq.md) - Frequently asked questions
- [WBcom Developer Resources](https://docs.wbcomdesigns.com/developers/)

**Need Development Support?**
📧 developers@wbcomdesigns.com | 📚 docs.wbcomdesigns.com/api