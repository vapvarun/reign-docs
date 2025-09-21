# Reign WP Job Manager Addon - Developer Guide

## Architecture Overview

### Plugin Structure

```
reign-wp-job-manager-addon/
├── reign-wp-job-manager-addon.php  # Main plugin file
├── inc/
│   ├── class-reign-job-loader.php
│   ├── class-reign-job-public.php
│   ├── class-reign-job-admin.php
│   ├── class-reign-job-templates.php
│   ├── class-reign-job-widgets.php
│   ├── class-reign-job-buddypress.php
│   └── class-reign-job-ajax.php
├── templates/
│   ├── content-job_listing.php
│   ├── content-single-job_listing.php
│   ├── job-dashboard.php
│   ├── job-filters.php
│   └── job-application.php
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
└── languages/
```

### Class Hierarchy

```php
Reign_Job_Manager_Addon
├── Reign_Job_Loader
├── Reign_Job_Public
├── Reign_Job_Admin
├── Reign_Job_Templates
├── Reign_Job_Widgets
├── Reign_Job_BuddyPress
└── Reign_Job_Ajax
```

## Core Classes

### Main Plugin Class

```php
/**
 * Main plugin class
 */
class Reign_Job_Manager_Addon {
    
    /**
     * Plugin version
     */
    const VERSION = '2.8.5';
    
    /**
     * Plugin instance
     */
    private static $instance = null;
    
    /**
     * Get plugin instance
     */
    public static function get_instance() {
        if (null === self::$instance) {
            self::$instance = new self();
        }
        return self::$instance;
    }
    
    /**
     * Constructor
     */
    private function __construct() {
        $this->define_constants();
        $this->includes();
        $this->init_hooks();
    }
    
    /**
     * Define constants
     */
    private function define_constants() {
        define('REIGN_JOB_VERSION', self::VERSION);
        define('REIGN_JOB_PATH', plugin_dir_path(__FILE__));
        define('REIGN_JOB_URL', plugin_dir_url(__FILE__));
        define('REIGN_JOB_BASENAME', plugin_basename(__FILE__));
    }
    
    /**
     * Include required files
     */
    private function includes() {
        require_once REIGN_JOB_PATH . 'inc/class-reign-job-loader.php';
        require_once REIGN_JOB_PATH . 'inc/class-reign-job-public.php';
        require_once REIGN_JOB_PATH . 'inc/class-reign-job-admin.php';
        require_once REIGN_JOB_PATH . 'inc/class-reign-job-templates.php';
        
        if (class_exists('BuddyPress')) {
            require_once REIGN_JOB_PATH . 'inc/class-reign-job-buddypress.php';
        }
    }
    
    /**
     * Initialize hooks
     */
    private function init_hooks() {
        add_action('init', array($this, 'init'));
        add_action('wp_enqueue_scripts', array($this, 'enqueue_scripts'));
        add_filter('template_include', array($this, 'template_loader'));
    }
}
```

### Template Management Class

```php
/**
 * Template management
 */
class Reign_Job_Templates {
    
    /**
     * Get template
     */
    public static function get_template($template_name, $args = array()) {
        // Extract args
        if ($args) {
            extract($args);
        }
        
        // Look for template in theme
        $template = locate_template(array(
            'reign-job-manager/' . $template_name,
            'job_manager/' . $template_name,
            $template_name
        ));
        
        // Fallback to plugin template
        if (!$template) {
            $template = REIGN_JOB_PATH . 'templates/' . $template_name;
        }
        
        // Allow filtering
        $template = apply_filters('reign_job_get_template', $template, $template_name, $args);
        
        if (file_exists($template)) {
            include $template;
        }
    }
    
    /**
     * Get template part
     */
    public static function get_template_part($slug, $name = '') {
        $template = '';
        
        // Look in theme
        if ($name) {
            $template = locate_template(array(
                "reign-job-manager/{$slug}-{$name}.php",
                "job_manager/{$slug}-{$name}.php"
            ));
        }
        
        // Get default from plugin
        if (!$template && $name && file_exists(REIGN_JOB_PATH . "templates/{$slug}-{$name}.php")) {
            $template = REIGN_JOB_PATH . "templates/{$slug}-{$name}.php";
        }
        
        if (!$template) {
            $template = REIGN_JOB_PATH . "templates/{$slug}.php";
        }
        
        // Allow filtering
        $template = apply_filters('reign_job_get_template_part', $template, $slug, $name);
        
        if ($template) {
            load_template($template, false);
        }
    }
    
    /**
     * Locate template
     */
    public static function locate_template($template_names) {
        $located = '';
        
        foreach ((array) $template_names as $template_name) {
            if (!$template_name) {
                continue;
            }
            
            // Theme template
            if (file_exists(get_stylesheet_directory() . '/reign-job-manager/' . $template_name)) {
                $located = get_stylesheet_directory() . '/reign-job-manager/' . $template_name;
                break;
            }
            
            // Plugin template
            if (file_exists(REIGN_JOB_PATH . 'templates/' . $template_name)) {
                $located = REIGN_JOB_PATH . 'templates/' . $template_name;
                break;
            }
        }
        
        return $located;
    }
}
```

## Hooks and Filters

### Action Hooks

```php
/**
 * Available action hooks
 */

// Job listing
do_action('reign_job_before_job_listing');
do_action('reign_job_after_job_listing');
do_action('reign_job_before_job_loop');
do_action('reign_job_after_job_loop');

// Single job
do_action('reign_job_before_single_job');
do_action('reign_job_after_single_job');
do_action('reign_job_single_job_header');
do_action('reign_job_single_job_content');
do_action('reign_job_single_job_sidebar');

// Job application
do_action('reign_job_before_application_form');
do_action('reign_job_after_application_form');
do_action('reign_job_application_submitted', $application_id);

// Company
do_action('reign_job_before_company_profile');
do_action('reign_job_after_company_profile');
```

### Filter Hooks

```php
/**
 * Available filter hooks
 */

// Job query
add_filter('reign_job_query_args', function($args) {
    // Modify job query
    $args['meta_query'][] = array(
        'key' => '_featured',
        'value' => '1'
    );
    return $args;
});

// Job data
add_filter('reign_job_data', function($data, $post_id) {
    // Add custom data
    $data['custom_field'] = get_post_meta($post_id, 'custom_field', true);
    return $data;
}, 10, 2);

// Template paths
add_filter('reign_job_template_path', function($path, $template) {
    // Change template path
    if ($template === 'custom-template.php') {
        $path = get_stylesheet_directory() . '/custom/' . $template;
    }
    return $path;
}, 10, 2);

// Job fields
add_filter('reign_job_fields', function($fields) {
    // Add custom field
    $fields['custom_field'] = array(
        'label' => 'Custom Field',
        'type' => 'text',
        'required' => false
    );
    return $fields;
});
```

## AJAX Implementation

### AJAX Handler Class

```php
/**
 * AJAX functionality
 */
class Reign_Job_Ajax {
    
    public function __construct() {
        // Public AJAX
        add_action('wp_ajax_nopriv_reign_job_search', array($this, 'search_jobs'));
        add_action('wp_ajax_reign_job_search', array($this, 'search_jobs'));
        
        // Private AJAX
        add_action('wp_ajax_reign_job_save', array($this, 'save_job'));
        add_action('wp_ajax_reign_job_apply', array($this, 'apply_job'));
    }
    
    /**
     * Search jobs
     */
    public function search_jobs() {
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_job_nonce')) {
            wp_die('Security check failed');
        }
        
        // Get search parameters
        $keyword = sanitize_text_field($_POST['keyword']);
        $location = sanitize_text_field($_POST['location']);
        $category = intval($_POST['category']);
        $job_type = sanitize_text_field($_POST['job_type']);
        
        // Build query
        $args = array(
            'post_type' => 'job_listing',
            'post_status' => 'publish',
            's' => $keyword,
            'posts_per_page' => 12,
            'paged' => $_POST['page'] ?? 1
        );
        
        // Location search
        if ($location) {
            $args['meta_query'][] = array(
                'key' => '_job_location',
                'value' => $location,
                'compare' => 'LIKE'
            );
        }
        
        // Category filter
        if ($category) {
            $args['tax_query'][] = array(
                'taxonomy' => 'job_listing_category',
                'terms' => $category
            );
        }
        
        // Job type filter
        if ($job_type) {
            $args['tax_query'][] = array(
                'taxonomy' => 'job_listing_type',
                'field' => 'slug',
                'terms' => $job_type
            );
        }
        
        // Get jobs
        $jobs = new WP_Query($args);
        
        // Build response
        ob_start();
        
        if ($jobs->have_posts()) {
            while ($jobs->have_posts()) {
                $jobs->the_post();
                Reign_Job_Templates::get_template('content-job_listing.php');
            }
        } else {
            echo '<p>' . __('No jobs found', 'reign-job-manager') . '</p>';
        }
        
        $html = ob_get_clean();
        
        wp_send_json_success(array(
            'html' => $html,
            'found' => $jobs->found_posts,
            'max_pages' => $jobs->max_num_pages
        ));
    }
    
    /**
     * Save job
     */
    public function save_job() {
        // Check login
        if (!is_user_logged_in()) {
            wp_send_json_error('Please login to save jobs');
        }
        
        // Verify nonce
        if (!wp_verify_nonce($_POST['nonce'], 'reign_job_nonce')) {
            wp_send_json_error('Security check failed');
        }
        
        $job_id = intval($_POST['job_id']);
        $user_id = get_current_user_id();
        
        // Get saved jobs
        $saved = get_user_meta($user_id, 'saved_jobs', true);
        if (!$saved) {
            $saved = array();
        }
        
        // Toggle save status
        if (in_array($job_id, $saved)) {
            $saved = array_diff($saved, array($job_id));
            $message = 'Job removed from saved';
        } else {
            $saved[] = $job_id;
            $message = 'Job saved successfully';
        }
        
        // Update user meta
        update_user_meta($user_id, 'saved_jobs', $saved);
        
        wp_send_json_success(array(
            'message' => $message,
            'saved' => in_array($job_id, $saved)
        ));
    }
}
```

### JavaScript AJAX Implementation

```javascript
/**
 * AJAX JavaScript
 */
(function($) {
    'use strict';
    
    var ReignJobManager = {
        
        init: function() {
            this.bindEvents();
            this.initFilters();
        },
        
        bindEvents: function() {
            $(document).on('submit', '.reign-job-search-form', this.searchJobs);
            $(document).on('click', '.save-job', this.saveJob);
            $(document).on('click', '.load-more-jobs', this.loadMore);
            $(document).on('change', '.job-filter', this.filterJobs);
        },
        
        searchJobs: function(e) {
            e.preventDefault();
            
            var $form = $(this);
            var data = {
                action: 'reign_job_search',
                nonce: reign_job_vars.nonce,
                keyword: $form.find('[name="search_keywords"]').val(),
                location: $form.find('[name="search_location"]').val(),
                category: $form.find('[name="search_categories"]').val(),
                job_type: $form.find('[name="job_types[]"]:checked').map(function() {
                    return $(this).val();
                }).get()
            };
            
            $('.job-listings').addClass('loading');
            
            $.post(reign_job_vars.ajax_url, data, function(response) {
                if (response.success) {
                    $('.job-listings').html(response.data.html);
                    
                    // Update pagination
                    if (response.data.max_pages > 1) {
                        $('.job-pagination').show();
                    }
                }
                $('.job-listings').removeClass('loading');
            });
        },
        
        saveJob: function(e) {
            e.preventDefault();
            
            var $button = $(this);
            var job_id = $button.data('job-id');
            
            if (!reign_job_vars.is_logged_in) {
                alert('Please login to save jobs');
                return;
            }
            
            $.post(reign_job_vars.ajax_url, {
                action: 'reign_job_save',
                nonce: reign_job_vars.nonce,
                job_id: job_id
            }, function(response) {
                if (response.success) {
                    $button.toggleClass('saved');
                    
                    if (response.data.saved) {
                        $button.html('<i class="fas fa-heart"></i> Saved');
                    } else {
                        $button.html('<i class="far fa-heart"></i> Save');
                    }
                    
                    // Show notification
                    ReignJobManager.showNotification(response.data.message);
                }
            });
        },
        
        showNotification: function(message) {
            var $notification = $('<div class="job-notification">' + message + '</div>');
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
        }
    };
    
    $(document).ready(function() {
        ReignJobManager.init();
    });
    
})(jQuery);
```

## REST API Endpoints

### Register REST Routes

```php
/**
 * Register REST API endpoints
 */
add_action('rest_api_init', function() {
    
    // Get jobs endpoint
    register_rest_route('reign-job/v1', '/jobs', array(
        'methods' => 'GET',
        'callback' => 'reign_job_get_jobs',
        'permission_callback' => '__return_true',
        'args' => array(
            'per_page' => array(
                'default' => 10,
                'sanitize_callback' => 'absint'
            ),
            'page' => array(
                'default' => 1,
                'sanitize_callback' => 'absint'
            ),
            'search' => array(
                'sanitize_callback' => 'sanitize_text_field'
            ),
            'location' => array(
                'sanitize_callback' => 'sanitize_text_field'
            ),
            'type' => array(
                'sanitize_callback' => 'sanitize_text_field'
            )
        )
    ));
    
    // Get single job
    register_rest_route('reign-job/v1', '/job/(?P<id>\d+)', array(
        'methods' => 'GET',
        'callback' => 'reign_job_get_job',
        'permission_callback' => '__return_true'
    ));
    
    // Submit application
    register_rest_route('reign-job/v1', '/apply', array(
        'methods' => 'POST',
        'callback' => 'reign_job_submit_application',
        'permission_callback' => 'is_user_logged_in'
    ));
});

/**
 * Get jobs callback
 */
function reign_job_get_jobs($request) {
    $args = array(
        'post_type' => 'job_listing',
        'post_status' => 'publish',
        'posts_per_page' => $request['per_page'],
        'paged' => $request['page']
    );
    
    if ($request['search']) {
        $args['s'] = $request['search'];
    }
    
    if ($request['location']) {
        $args['meta_query'][] = array(
            'key' => '_job_location',
            'value' => $request['location'],
            'compare' => 'LIKE'
        );
    }
    
    $jobs = new WP_Query($args);
    $data = array();
    
    foreach ($jobs->posts as $job) {
        $data[] = array(
            'id' => $job->ID,
            'title' => $job->post_title,
            'content' => $job->post_content,
            'company' => get_the_company_name($job->ID),
            'location' => get_the_job_location($job->ID),
            'type' => wp_get_post_terms($job->ID, 'job_listing_type'),
            'url' => get_permalink($job->ID),
            'logo' => get_the_company_logo_url($job->ID),
            'featured' => is_position_featured($job->ID),
            'posted' => get_the_date('', $job->ID)
        );
    }
    
    return new WP_REST_Response($data, 200);
}
```

## Widget Development

### Custom Job Widget

```php
/**
 * Recent Jobs Widget
 */
class Reign_Job_Recent_Widget extends WP_Widget {
    
    public function __construct() {
        parent::__construct(
            'reign_job_recent',
            __('Reign Recent Jobs', 'reign-job-manager'),
            array('description' => __('Display recent job listings', 'reign-job-manager'))
        );
    }
    
    public function widget($args, $instance) {
        echo $args['before_widget'];
        
        if (!empty($instance['title'])) {
            echo $args['before_title'] . apply_filters('widget_title', $instance['title']) . $args['after_title'];
        }
        
        $number = !empty($instance['number']) ? absint($instance['number']) : 5;
        
        $jobs = new WP_Query(array(
            'post_type' => 'job_listing',
            'posts_per_page' => $number,
            'post_status' => 'publish'
        ));
        
        if ($jobs->have_posts()) {
            echo '<ul class="reign-recent-jobs">';
            
            while ($jobs->have_posts()) {
                $jobs->the_post();
                ?>
                <li>
                    <div class="job-logo">
                        <?php the_company_logo('thumbnail'); ?>
                    </div>
                    <div class="job-info">
                        <h4><a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></h4>
                        <div class="job-meta">
                            <span class="company"><?php the_company_name(); ?></span>
                            <span class="location"><?php the_job_location(); ?></span>
                        </div>
                    </div>
                </li>
                <?php
            }
            
            echo '</ul>';
            wp_reset_postdata();
        }
        
        echo $args['after_widget'];
    }
    
    public function form($instance) {
        $title = !empty($instance['title']) ? $instance['title'] : __('Recent Jobs', 'reign-job-manager');
        $number = !empty($instance['number']) ? absint($instance['number']) : 5;
        ?>
        <p>
            <label for="<?php echo esc_attr($this->get_field_id('title')); ?>">
                <?php esc_attr_e('Title:', 'reign-job-manager'); ?>
            </label>
            <input class="widefat" 
                   id="<?php echo esc_attr($this->get_field_id('title')); ?>" 
                   name="<?php echo esc_attr($this->get_field_name('title')); ?>" 
                   type="text" 
                   value="<?php echo esc_attr($title); ?>">
        </p>
        <p>
            <label for="<?php echo esc_attr($this->get_field_id('number')); ?>">
                <?php esc_attr_e('Number of jobs:', 'reign-job-manager'); ?>
            </label>
            <input class="widefat" 
                   id="<?php echo esc_attr($this->get_field_id('number')); ?>" 
                   name="<?php echo esc_attr($this->get_field_name('number')); ?>" 
                   type="number" 
                   value="<?php echo esc_attr($number); ?>">
        </p>
        <?php
    }
}

// Register widget
add_action('widgets_init', function() {
    register_widget('Reign_Job_Recent_Widget');
});
```

## Next Steps

- [Shortcode Reference](06-shortcodes-reference.md) - Available shortcodes
- [Troubleshooting](07-troubleshooting.md) - Common issues
- [FAQ](08-faq.md) - Frequently asked questions