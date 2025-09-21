# Reign LearnDash Addon - Developer Guide

## What You'll Learn
This guide provides developers with hooks, filters, and code examples to extend the Reign LearnDash addon. We'll cover customizations, API integration, and advanced LMS features.

## Quick Overview
**Skill Level:** Intermediate to Advanced PHP  
**Requirements:** WordPress development experience  
**Tools:** Code editor, local development environment

---

## Part 1: Core Hooks & Filters

### Action Hooks

**Course Enrollment Hooks:**

```php
// Before course enrollment
add_action('reign_learndash_before_enrollment', function($user_id, $course_id) {
    // Log enrollment attempt
    error_log("User {$user_id} attempting to enroll in course {$course_id}");
    
    // Check prerequisites
    if (!user_meets_prerequisites($user_id, $course_id)) {
        wp_die('Prerequisites not met');
    }
}, 10, 2);

// After successful enrollment
add_action('reign_learndash_after_enrollment', function($user_id, $course_id) {
    // Send welcome email
    send_course_welcome_email($user_id, $course_id);
    
    // Add to course group
    assign_to_study_group($user_id, $course_id);
    
    // Track analytics
    track_enrollment_event($user_id, $course_id);
}, 10, 2);

// Course completion
add_action('reign_learndash_course_completed', function($user_id, $course_id) {
    // Generate certificate
    generate_course_certificate($user_id, $course_id);
    
    // Update user progress
    update_user_learning_path($user_id);
    
    // Recommend next courses
    suggest_follow_up_courses($user_id, $course_id);
}, 10, 2);
```

**Lesson Progress Hooks:**

```php
// Before lesson access
add_action('reign_learndash_before_lesson_access', function($user_id, $lesson_id) {
    // Check if user can access lesson
    if (!can_user_access_lesson($user_id, $lesson_id)) {
        wp_redirect(get_course_url());
        exit;
    }
    
    // Track lesson start
    track_lesson_start($user_id, $lesson_id);
});

// After lesson completion
add_action('reign_learndash_lesson_completed', function($user_id, $lesson_id) {
    // Update progress tracking
    update_lesson_progress($user_id, $lesson_id);
    
    // Unlock next lesson
    unlock_next_lesson($user_id, $lesson_id);
    
    // Award points
    award_completion_points($user_id, $lesson_id);
}, 10, 2);
```

**Quiz & Assessment Hooks:**

```php
// Before quiz submission
add_action('reign_learndash_before_quiz_submit', function($user_id, $quiz_id) {
    // Validate quiz attempt
    if (!validate_quiz_attempt($user_id, $quiz_id)) {
        wp_die('Invalid quiz attempt');
    }
    
    // Save attempt timestamp
    update_user_meta($user_id, "quiz_{$quiz_id}_attempt_time", time());
});

// After quiz completion
add_action('reign_learndash_quiz_completed', function($user_id, $quiz_id, $score) {
    // Check passing grade
    $passing_score = get_quiz_passing_score($quiz_id);
    
    if ($score >= $passing_score) {
        // Award badge for high score
        if ($score >= 90) {
            award_excellence_badge($user_id, $quiz_id);
        }
        
        // Unlock next content
        unlock_next_content($user_id, $quiz_id);
    } else {
        // Provide remedial resources
        suggest_study_materials($user_id, $quiz_id);
    }
    
    // Update analytics
    track_quiz_performance($user_id, $quiz_id, $score);
}, 10, 3);
```

### Filter Hooks

**Course Display Filters:**

```php
// Modify course card data
add_filter('reign_learndash_course_card_data', function($data, $course_id) {
    // Add custom fields
    $data['estimated_hours'] = get_post_meta($course_id, 'course_duration_hours', true);
    $data['skill_level'] = get_post_meta($course_id, 'course_difficulty', true);
    $data['prerequisites'] = get_course_prerequisites($course_id);
    $data['learning_outcomes'] = get_post_meta($course_id, 'learning_outcomes', true);
    
    // Add enrollment stats
    $data['total_enrolled'] = get_course_enrollment_count($course_id);
    $data['completion_rate'] = calculate_completion_rate($course_id);
    
    return $data;
}, 10, 2);

// Filter course grid layout
add_filter('reign_learndash_course_grid_columns', function($columns, $device) {
    // Adjust columns based on device
    switch ($device) {
        case 'mobile':
            return 1;
        case 'tablet':
            return 2;
        case 'desktop':
        default:
            return 3;
    }
}, 10, 2);
```

**Lesson Content Filters:**

```php
// Add custom content to lessons
add_filter('reign_learndash_lesson_content', function($content, $lesson_id) {
    // Add lesson objectives
    $objectives = get_post_meta($lesson_id, 'lesson_objectives', true);
    if ($objectives) {
        $content = '<div class="lesson-objectives">' . 
                   '<h3>What You\'ll Learn:</h3>' . 
                   '<ul>' . $objectives . '</ul>' . 
                   '</div>' . $content;
    }
    
    // Add estimated reading time
    $reading_time = calculate_reading_time($content);
    $content = '<div class="reading-time">Estimated time: ' . $reading_time . ' minutes</div>' . $content;
    
    return $content;
}, 10, 2);

// Customize lesson navigation
add_filter('reign_learndash_lesson_navigation', function($nav_items, $lesson_id) {
    // Add custom navigation items
    $nav_items['notes'] = array(
        'title' => 'My Notes',
        'url' => get_lesson_notes_url($lesson_id),
        'icon' => 'fa-sticky-note'
    );
    
    $nav_items['discuss'] = array(
        'title' => 'Discuss',
        'url' => get_lesson_discussion_url($lesson_id),
        'icon' => 'fa-comments'
    );
    
    return $nav_items;
}, 10, 2);
```

**User Progress Filters:**

```php
// Customize progress calculation
add_filter('reign_learndash_course_progress', function($progress, $user_id, $course_id) {
    // Include quiz scores in progress
    $quiz_progress = get_user_quiz_progress($user_id, $course_id);
    $lesson_progress = get_user_lesson_progress($user_id, $course_id);
    
    // Weighted progress (70% lessons, 30% quizzes)
    $weighted_progress = ($lesson_progress * 0.7) + ($quiz_progress * 0.3);
    
    return $weighted_progress;
}, 10, 3);
```

---

## Part 2: Custom Learning Features

### Learning Path System

```php
class Reign_LearnDash_Learning_Paths {
    
    private $paths = array();
    
    public function __construct() {
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Register custom post type for learning paths
        $this->register_learning_path_post_type();
        
        // Add hooks
        add_action('learndash_course_completed', array($this, 'check_path_progress'), 10, 2);
        add_filter('reign_learndash_user_dashboard', array($this, 'add_path_widget'));
    }
    
    public function register_learning_path_post_type() {
        register_post_type('learning_path', array(
            'labels' => array(
                'name' => 'Learning Paths',
                'singular_name' => 'Learning Path'
            ),
            'public' => true,
            'supports' => array('title', 'editor', 'thumbnail'),
            'show_in_menu' => 'learndash-lms'
        ));
    }
    
    public function create_learning_path($title, $courses, $description = '') {
        $path_id = wp_insert_post(array(
            'post_title' => $title,
            'post_content' => $description,
            'post_type' => 'learning_path',
            'post_status' => 'publish'
        ));
        
        if ($path_id) {
            update_post_meta($path_id, 'path_courses', $courses);
            update_post_meta($path_id, 'path_order', array_keys($courses));
            return $path_id;
        }
        
        return false;
    }
    
    public function enroll_user_in_path($user_id, $path_id) {
        $courses = get_post_meta($path_id, 'path_courses', true);
        
        if ($courses) {
            // Enroll in first course
            $first_course = reset($courses);
            ld_update_course_access($user_id, $first_course, false);
            
            // Track path enrollment
            update_user_meta($user_id, 'learning_path_' . $path_id, array(
                'enrolled_date' => time(),
                'current_course' => $first_course,
                'completed_courses' => array()
            ));
        }
    }
    
    public function check_path_progress($data) {
        $user_id = $data['user']->ID;
        $course_id = $data['course']->ID;
        
        // Find learning paths that include this course
        $paths = $this->get_user_learning_paths($user_id);
        
        foreach ($paths as $path_id => $path_data) {
            $path_courses = get_post_meta($path_id, 'path_courses', true);
            
            if (in_array($course_id, $path_courses)) {
                $this->advance_path_progress($user_id, $path_id, $course_id);
            }
        }
    }
    
    private function advance_path_progress($user_id, $path_id, $completed_course_id) {
        $path_progress = get_user_meta($user_id, 'learning_path_' . $path_id, true);
        $path_courses = get_post_meta($path_id, 'path_courses', true);
        $course_order = get_post_meta($path_id, 'path_order', true);
        
        // Mark course as completed
        $path_progress['completed_courses'][] = $completed_course_id;
        
        // Find next course
        $current_index = array_search($completed_course_id, $course_order);
        $next_index = $current_index + 1;
        
        if (isset($course_order[$next_index])) {
            // Enroll in next course
            $next_course = $course_order[$next_index];
            ld_update_course_access($user_id, $next_course, false);
            $path_progress['current_course'] = $next_course;
            
            // Send notification
            $this->send_next_course_notification($user_id, $next_course);
        } else {
            // Path completed
            $path_progress['completed_date'] = time();
            $this->award_path_completion_certificate($user_id, $path_id);
        }
        
        update_user_meta($user_id, 'learning_path_' . $path_id, $path_progress);
    }
    
    public function get_user_learning_paths($user_id) {
        $paths = array();
        $user_meta = get_user_meta($user_id);
        
        foreach ($user_meta as $key => $value) {
            if (strpos($key, 'learning_path_') === 0) {
                $path_id = str_replace('learning_path_', '', $key);
                $paths[$path_id] = $value[0];
            }
        }
        
        return $paths;
    }
    
    private function send_next_course_notification($user_id, $course_id) {
        $user = get_userdata($user_id);
        $course = get_post($course_id);
        
        $subject = 'Your Next Course is Ready!';
        $message = "Hi {$user->display_name},\n\n";
        $message .= "Congratulations on completing your previous course!\n\n";
        $message .= "Your next course '{$course->post_title}' is now available.\n\n";
        $message .= "Start learning: " . get_permalink($course_id) . "\n\n";
        $message .= "Keep up the great work!";
        
        wp_mail($user->user_email, $subject, $message);
    }
    
    private function award_path_completion_certificate($user_id, $path_id) {
        // Implementation for path completion certificate
        do_action('reign_learndash_path_completed', $user_id, $path_id);
    }
}

// Initialize learning paths
new Reign_LearnDash_Learning_Paths();
```

### Advanced Assessment System

```php
class Reign_LearnDash_Advanced_Assessments {
    
    public function __construct() {
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Custom question types
        add_filter('learndash_quiz_question_types', array($this, 'add_custom_question_types'));
        
        // Advanced scoring
        add_filter('learndash_quiz_score_calculation', array($this, 'custom_score_calculation'), 10, 3);
        
        // Adaptive quizzes
        add_action('learndash_quiz_question_answered', array($this, 'adaptive_question_selection'));
    }
    
    public function add_custom_question_types($types) {
        $types['drag_drop'] = 'Drag and Drop';
        $types['hotspot'] = 'Image Hotspot';
        $types['code_evaluation'] = 'Code Evaluation';
        $types['peer_review'] = 'Peer Review';
        
        return $types;
    }
    
    public function custom_score_calculation($score, $quiz_id, $user_answers) {
        // Implement competency-based scoring
        $competencies = get_post_meta($quiz_id, 'quiz_competencies', true);
        
        if ($competencies) {
            $competency_scores = array();
            
            foreach ($user_answers as $question_id => $answer) {
                $question_competencies = get_post_meta($question_id, 'question_competencies', true);
                $is_correct = $this->check_answer_correctness($question_id, $answer);
                
                foreach ($question_competencies as $competency) {
                    if (!isset($competency_scores[$competency])) {
                        $competency_scores[$competency] = array('correct' => 0, 'total' => 0);
                    }
                    
                    $competency_scores[$competency]['total']++;
                    if ($is_correct) {
                        $competency_scores[$competency]['correct']++;
                    }
                }
            }
            
            // Calculate weighted score based on competency importance
            $weighted_score = 0;
            $total_weight = 0;
            
            foreach ($competency_scores as $competency => $data) {
                $weight = get_competency_weight($competency);
                $competency_score = ($data['correct'] / $data['total']) * 100;
                $weighted_score += $competency_score * $weight;
                $total_weight += $weight;
            }
            
            return $total_weight > 0 ? $weighted_score / $total_weight : $score;
        }
        
        return $score;
    }
    
    public function adaptive_question_selection($data) {
        $user_id = $data['user_id'];
        $quiz_id = $data['quiz_id'];
        $question_id = $data['question_id'];
        $is_correct = $data['is_correct'];
        
        // Implement adaptive algorithm
        $user_ability = get_user_meta($user_id, 'quiz_ability_' . $quiz_id, true) ?: 0;
        $question_difficulty = get_post_meta($question_id, 'question_difficulty', true) ?: 0;
        
        // Update user ability based on response
        if ($is_correct) {
            $user_ability += 0.1;
        } else {
            $user_ability -= 0.1;
        }
        
        // Clamp ability between -3 and 3
        $user_ability = max(-3, min(3, $user_ability));
        update_user_meta($user_id, 'quiz_ability_' . $quiz_id, $user_ability);
        
        // Select next question based on ability
        $this->select_next_adaptive_question($user_id, $quiz_id, $user_ability);
    }
    
    private function select_next_adaptive_question($user_id, $quiz_id, $user_ability) {
        // Find questions with difficulty close to user ability
        $target_difficulty = $user_ability;
        $tolerance = 0.5;
        
        $questions = get_quiz_questions($quiz_id);
        $answered_questions = get_user_answered_questions($user_id, $quiz_id);
        
        $available_questions = array_diff($questions, $answered_questions);
        $suitable_questions = array();
        
        foreach ($available_questions as $question_id) {
            $difficulty = get_post_meta($question_id, 'question_difficulty', true);
            
            if (abs($difficulty - $target_difficulty) <= $tolerance) {
                $suitable_questions[] = $question_id;
            }
        }
        
        if (!empty($suitable_questions)) {
            $next_question = $suitable_questions[array_rand($suitable_questions)];
            update_user_meta($user_id, 'quiz_next_question_' . $quiz_id, $next_question);
        }
    }
}

// Initialize advanced assessments
new Reign_LearnDash_Advanced_Assessments();
```

---

## Part 3: REST API Integration

### Custom REST Endpoints

```php
class Reign_LearnDash_REST_API {
    
    public function __construct() {
        add_action('rest_api_init', array($this, 'register_routes'));
    }
    
    public function register_routes() {
        // Get user course progress
        register_rest_route('reign-learndash/v1', '/user/(?P<id>\d+)/progress', array(
            'methods' => 'GET',
            'callback' => array($this, 'get_user_progress'),
            'permission_callback' => array($this, 'check_user_permission')
        ));
        
        // Get course analytics
        register_rest_route('reign-learndash/v1', '/course/(?P<id>\d+)/analytics', array(
            'methods' => 'GET',
            'callback' => array($this, 'get_course_analytics'),
            'permission_callback' => array($this, 'check_instructor_permission')
        ));
        
        // Submit quiz answer
        register_rest_route('reign-learndash/v1', '/quiz/(?P<id>\d+)/answer', array(
            'methods' => 'POST',
            'callback' => array($this, 'submit_quiz_answer'),
            'permission_callback' => array($this, 'check_user_permission')
        ));
        
        // Get learning recommendations
        register_rest_route('reign-learndash/v1', '/user/(?P<id>\d+)/recommendations', array(
            'methods' => 'GET',
            'callback' => array($this, 'get_learning_recommendations'),
            'permission_callback' => array($this, 'check_user_permission')
        ));
    }
    
    public function get_user_progress($request) {
        $user_id = $request['id'];
        
        // Get all enrolled courses
        $enrolled_courses = ld_get_user_course_data($user_id);
        $progress_data = array();
        
        foreach ($enrolled_courses as $course_id => $course_data) {
            $course = get_post($course_id);
            $progress_percentage = learndash_course_progress($user_id, $course_id);
            
            $progress_data[] = array(
                'course_id' => $course_id,
                'title' => $course->post_title,
                'progress_percentage' => $progress_percentage,
                'status' => $this->get_course_status($user_id, $course_id),
                'last_activity' => $this->get_last_activity($user_id, $course_id),
                'lessons_completed' => $this->get_completed_lessons_count($user_id, $course_id),
                'total_lessons' => $this->get_total_lessons_count($course_id),
                'quizzes_passed' => $this->get_passed_quizzes_count($user_id, $course_id),
                'certificates_earned' => $this->get_certificates($user_id, $course_id)
            );
        }
        
        return rest_ensure_response($progress_data);
    }
    
    public function get_course_analytics($request) {
        $course_id = $request['id'];
        
        $analytics = array(
            'total_enrollments' => $this->get_course_enrollment_count($course_id),
            'active_students' => $this->get_active_students_count($course_id),
            'completion_rate' => $this->calculate_completion_rate($course_id),
            'average_score' => $this->get_average_quiz_scores($course_id),
            'engagement_metrics' => array(
                'avg_time_per_lesson' => $this->get_average_lesson_time($course_id),
                'discussion_participation' => $this->get_discussion_stats($course_id),
                'assignment_submission_rate' => $this->get_assignment_stats($course_id)
            ),
            'popular_lessons' => $this->get_popular_lessons($course_id),
            'challenging_areas' => $this->get_challenging_content($course_id)
        );
        
        return rest_ensure_response($analytics);
    }
    
    public function submit_quiz_answer($request) {
        $quiz_id = $request['id'];
        $user_id = get_current_user_id();
        $answers = $request->get_json_params();
        
        // Validate quiz attempt
        if (!$this->can_user_take_quiz($user_id, $quiz_id)) {
            return new WP_Error('access_denied', 'Cannot take this quiz', array('status' => 403));
        }
        
        // Process answers
        $results = array();
        foreach ($answers['questions'] as $question_id => $answer) {
            $is_correct = $this->evaluate_answer($question_id, $answer);
            $results[$question_id] = array(
                'correct' => $is_correct,
                'explanation' => get_post_meta($question_id, 'answer_explanation', true)
            );
        }
        
        // Calculate score
        $total_questions = count($answers['questions']);
        $correct_answers = array_sum(array_column($results, 'correct'));
        $score_percentage = ($correct_answers / $total_questions) * 100;
        
        // Save quiz attempt
        $this->save_quiz_attempt($user_id, $quiz_id, $answers, $score_percentage);
        
        return rest_ensure_response(array(
            'score' => $score_percentage,
            'passed' => $score_percentage >= get_quiz_passing_score($quiz_id),
            'results' => $results,
            'attempts_remaining' => $this->get_remaining_attempts($user_id, $quiz_id)
        ));
    }
    
    public function get_learning_recommendations($request) {
        $user_id = $request['id'];
        
        // Analyze user's learning history
        $completed_courses = ld_get_user_completed_courses($user_id);
        $interests = $this->analyze_user_interests($user_id, $completed_courses);
        $skill_gaps = $this->identify_skill_gaps($user_id);
        
        // Generate recommendations
        $recommendations = array(
            'next_courses' => $this->recommend_next_courses($interests, $skill_gaps),
            'skill_building' => $this->recommend_skill_courses($skill_gaps),
            'trending' => $this->get_trending_courses($interests),
            'peer_popular' => $this->get_peer_popular_courses($user_id)
        );
        
        return rest_ensure_response($recommendations);
    }
    
    public function check_user_permission($request) {
        $user_id = $request['id'];
        return current_user_can('manage_options') || get_current_user_id() == $user_id;
    }
    
    public function check_instructor_permission($request) {
        $course_id = $request['id'];
        $user_id = get_current_user_id();
        
        return current_user_can('manage_options') || 
               learndash_is_course_instructor($user_id, $course_id);
    }
    
    // Helper methods
    private function get_course_status($user_id, $course_id) {
        if (learndash_course_completed($user_id, $course_id)) {
            return 'completed';
        } elseif (learndash_user_progress($user_id, $course_id)) {
            return 'in_progress';
        } else {
            return 'not_started';
        }
    }
    
    private function get_last_activity($user_id, $course_id) {
        $activity = learndash_get_user_activity($user_id, $course_id);
        return $activity ? $activity['date'] : null;
    }
    
    private function analyze_user_interests($user_id, $completed_courses) {
        $interests = array();
        
        foreach ($completed_courses as $course_id) {
            $categories = wp_get_post_terms($course_id, 'ld_course_category');
            foreach ($categories as $category) {
                if (!isset($interests[$category->slug])) {
                    $interests[$category->slug] = 0;
                }
                $interests[$category->slug]++;
            }
        }
        
        arsort($interests);
        return array_keys(array_slice($interests, 0, 5));
    }
}

// Initialize REST API
new Reign_LearnDash_REST_API();
```

---

## Part 4: Advanced Analytics

### Learning Analytics Dashboard

```php
class Reign_LearnDash_Analytics {
    
    public function __construct() {
        add_action('wp_dashboard_setup', array($this, 'add_dashboard_widgets'));
        add_action('admin_menu', array($this, 'add_analytics_page'));
        add_action('wp_ajax_get_learning_analytics', array($this, 'get_analytics_data'));
    }
    
    public function add_dashboard_widgets() {
        wp_add_dashboard_widget(
            'reign_learndash_analytics',
            'Learning Analytics Overview',
            array($this, 'dashboard_widget_content')
        );
    }
    
    public function dashboard_widget_content() {
        $stats = $this->get_quick_stats();
        ?>
        <div class="learning-stats">
            <div class="stat-item">
                <h3><?php echo $stats['total_students']; ?></h3>
                <p>Total Students</p>
            </div>
            <div class="stat-item">
                <h3><?php echo $stats['active_courses']; ?></h3>
                <p>Active Courses</p>
            </div>
            <div class="stat-item">
                <h3><?php echo $stats['completion_rate']; ?>%</h3>
                <p>Avg Completion Rate</p>
            </div>
            <div class="stat-item">
                <h3><?php echo $stats['certificates_issued']; ?></h3>
                <p>Certificates Issued</p>
            </div>
        </div>
        
        <canvas id="learningChart" width="400" height="200"></canvas>
        
        <script>
        // Chart.js implementation for learning progress visualization
        var ctx = document.getElementById('learningChart').getContext('2d');
        var chart = new Chart(ctx, {
            type: 'line',
            data: <?php echo json_encode($this->get_chart_data()); ?>,
            options: {
                responsive: true,
                scales: {
                    y: {
                        beginAtZero: true
                    }
                }
            }
        });
        </script>
        <?php
    }
    
    public function generate_learning_report($user_id = null, $course_id = null, $date_range = '30_days') {
        $report = array(
            'period' => $date_range,
            'generated_at' => current_time('mysql'),
            'data' => array()
        );
        
        if ($user_id) {
            // Individual user report
            $report['type'] = 'user';
            $report['data'] = $this->get_user_analytics($user_id, $date_range);
        } elseif ($course_id) {
            // Course-specific report
            $report['type'] = 'course';
            $report['data'] = $this->get_course_analytics($course_id, $date_range);
        } else {
            // System-wide report
            $report['type'] = 'system';
            $report['data'] = $this->get_system_analytics($date_range);
        }
        
        return $report;
    }
    
    private function get_user_analytics($user_id, $date_range) {
        $user = get_userdata($user_id);
        $enrolled_courses = ld_get_user_course_data($user_id);
        
        return array(
            'user_info' => array(
                'name' => $user->display_name,
                'email' => $user->user_email,
                'registration_date' => $user->user_registered
            ),
            'learning_summary' => array(
                'total_courses' => count($enrolled_courses),
                'completed_courses' => count(ld_get_user_completed_courses($user_id)),
                'in_progress_courses' => $this->get_in_progress_courses_count($user_id),
                'total_lessons_completed' => $this->get_total_lessons_completed($user_id),
                'average_quiz_score' => $this->get_user_average_quiz_score($user_id),
                'certificates_earned' => count(learndash_get_user_certificates($user_id))
            ),
            'engagement_metrics' => array(
                'login_frequency' => $this->get_login_frequency($user_id, $date_range),
                'avg_session_duration' => $this->get_avg_session_duration($user_id, $date_range),
                'content_interaction' => $this->get_content_interaction_stats($user_id, $date_range),
                'discussion_participation' => $this->get_discussion_participation($user_id, $date_range)
            ),
            'learning_path_progress' => $this->get_learning_path_progress($user_id),
            'skill_development' => $this->get_skill_development_tracking($user_id),
            'recommendations' => $this->get_personalized_recommendations($user_id)
        );
    }
    
    private function get_course_analytics($course_id, $date_range) {
        $course = get_post($course_id);
        $enrolled_users = learndash_get_course_users_list($course_id);
        
        return array(
            'course_info' => array(
                'title' => $course->post_title,
                'created_date' => $course->post_date,
                'last_modified' => $course->post_modified,
                'instructor' => get_post_meta($course_id, 'course_instructor', true)
            ),
            'enrollment_metrics' => array(
                'total_enrollments' => count($enrolled_users),
                'active_students' => $this->get_active_students_count($course_id, $date_range),
                'completion_rate' => $this->calculate_completion_rate($course_id),
                'dropout_rate' => $this->calculate_dropout_rate($course_id),
                'enrollment_trend' => $this->get_enrollment_trend($course_id, $date_range)
            ),
            'content_performance' => array(
                'popular_lessons' => $this->get_popular_lessons($course_id),
                'challenging_content' => $this->get_challenging_content($course_id),
                'average_completion_time' => $this->get_average_completion_time($course_id),
                'content_effectiveness' => $this->analyze_content_effectiveness($course_id)
            ),
            'assessment_analytics' => array(
                'quiz_performance' => $this->get_quiz_performance_stats($course_id),
                'common_mistakes' => $this->identify_common_mistakes($course_id),
                'score_distribution' => $this->get_score_distribution($course_id),
                'retake_patterns' => $this->analyze_retake_patterns($course_id)
            ),
            'engagement_patterns' => array(
                'peak_activity_times' => $this->get_peak_activity_times($course_id),
                'content_consumption_patterns' => $this->analyze_consumption_patterns($course_id),
                'discussion_activity' => $this->get_discussion_activity($course_id),
                'help_seeking_behavior' => $this->analyze_help_seeking($course_id)
            )
        );
    }
    
    public function track_learning_event($event_type, $user_id, $object_id, $additional_data = array()) {
        global $wpdb;
        
        $table_name = $wpdb->prefix . 'reign_learning_events';
        
        $wpdb->insert(
            $table_name,
            array(
                'event_type' => $event_type,
                'user_id' => $user_id,
                'object_id' => $object_id,
                'event_data' => json_encode($additional_data),
                'timestamp' => current_time('mysql'),
                'session_id' => $this->get_session_id()
            ),
            array('%s', '%d', '%d', '%s', '%s', '%s')
        );
    }
    
    private function create_analytics_tables() {
        global $wpdb;
        
        $table_name = $wpdb->prefix . 'reign_learning_events';
        
        $charset_collate = $wpdb->get_charset_collate();
        
        $sql = "CREATE TABLE $table_name (
            id bigint(20) NOT NULL AUTO_INCREMENT,
            event_type varchar(50) NOT NULL,
            user_id bigint(20) NOT NULL,
            object_id bigint(20) NOT NULL,
            event_data longtext,
            timestamp datetime DEFAULT CURRENT_TIMESTAMP,
            session_id varchar(100),
            PRIMARY KEY (id),
            KEY user_id (user_id),
            KEY event_type (event_type),
            KEY timestamp (timestamp)
        ) $charset_collate;";
        
        require_once(ABSPATH . 'wp-admin/includes/upgrade.php');
        dbDelta($sql);
    }
}

// Initialize analytics
new Reign_LearnDash_Analytics();
```

---

## Part 5: Integration Examples

### Zoom Integration for Live Classes

```php
class Reign_LearnDash_Zoom_Integration {
    
    private $zoom_api_key;
    private $zoom_api_secret;
    
    public function __construct() {
        $this->zoom_api_key = get_option('reign_zoom_api_key');
        $this->zoom_api_secret = get_option('reign_zoom_api_secret');
        
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Add live class fields to lessons
        add_action('add_meta_boxes', array($this, 'add_zoom_meta_box'));
        add_action('save_post', array($this, 'save_zoom_settings'));
        
        // Display Zoom link in lesson
        add_filter('reign_learndash_lesson_content', array($this, 'add_zoom_link'));
        
        // Handle Zoom webhooks
        add_action('wp_ajax_nopriv_zoom_webhook', array($this, 'handle_zoom_webhook'));
    }
    
    public function create_zoom_meeting($lesson_id, $meeting_data) {
        $endpoint = 'https://api.zoom.us/v2/users/me/meetings';
        
        $headers = array(
            'Authorization' => 'Bearer ' . $this->get_jwt_token(),
            'Content-Type' => 'application/json'
        );
        
        $body = json_encode(array(
            'topic' => $meeting_data['topic'],
            'type' => 2, // Scheduled meeting
            'start_time' => $meeting_data['start_time'],
            'duration' => $meeting_data['duration'],
            'timezone' => get_option('timezone_string'),
            'settings' => array(
                'host_video' => true,
                'participant_video' => true,
                'join_before_host' => false,
                'mute_upon_entry' => true,
                'waiting_room' => true,
                'auto_recording' => 'cloud'
            )
        ));
        
        $response = wp_remote_post($endpoint, array(
            'headers' => $headers,
            'body' => $body,
            'timeout' => 30
        ));
        
        if (is_wp_error($response)) {
            return false;
        }
        
        $meeting = json_decode(wp_remote_retrieve_body($response), true);
        
        if (isset($meeting['id'])) {
            // Save meeting data to lesson
            update_post_meta($lesson_id, 'zoom_meeting_id', $meeting['id']);
            update_post_meta($lesson_id, 'zoom_join_url', $meeting['join_url']);
            update_post_meta($lesson_id, 'zoom_start_url', $meeting['start_url']);
            
            return $meeting;
        }
        
        return false;
    }
    
    public function add_zoom_link($content, $lesson_id) {
        $zoom_meeting_id = get_post_meta($lesson_id, 'zoom_meeting_id', true);
        
        if ($zoom_meeting_id) {
            $meeting_info = $this->get_meeting_info($zoom_meeting_id);
            $join_url = get_post_meta($lesson_id, 'zoom_join_url', true);
            
            $zoom_content = '<div class="zoom-meeting-info">';
            $zoom_content .= '<h3>Live Class</h3>';
            $zoom_content .= '<p><strong>Start Time:</strong> ' . date('F j, Y \\a\\t g:i A', strtotime($meeting_info['start_time'])) . '</p>';
            $zoom_content .= '<p><strong>Duration:</strong> ' . $meeting_info['duration'] . ' minutes</p>';
            
            if ($this->is_meeting_live($meeting_info)) {
                $zoom_content .= '<a href="' . $join_url . '" class="zoom-join-button" target="_blank">Join Live Class</a>';
            } else {
                $zoom_content .= '<p>Live class will start at the scheduled time.</p>';
            }
            
            $zoom_content .= '</div>';
            
            $content = $zoom_content . $content;
        }
        
        return $content;
    }
    
    private function get_jwt_token() {
        $header = json_encode(array('typ' => 'JWT', 'alg' => 'HS256'));
        $payload = json_encode(array(
            'iss' => $this->zoom_api_key,
            'exp' => time() + 3600
        ));
        
        $base64Header = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($header));
        $base64Payload = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($payload));
        
        $signature = hash_hmac('sha256', $base64Header . "." . $base64Payload, $this->zoom_api_secret, true);
        $base64Signature = str_replace(['+', '/', '='], ['-', '_', ''], base64_encode($signature));
        
        return $base64Header . "." . $base64Payload . "." . $base64Signature;
    }
}

// Initialize Zoom integration
new Reign_LearnDash_Zoom_Integration();
```

---

## Quick Reference

### Important Functions

```php
// Check course enrollment
learndash_user_get_enrolled_courses($user_id)

// Get course progress
learndash_course_progress($user_id, $course_id)

// Check course completion
learndash_course_completed($user_id, $course_id)

// Get quiz results
learndash_get_user_quiz_attempts($user_id, $quiz_id)

// Enroll user in course
ld_update_course_access($user_id, $course_id, $remove = false)

// Get course lessons
learndash_get_course_lessons_list($course_id)
```

### Key Filters

```php
// Course content
apply_filters('learndash_course_content', $content, $course_id)

// Lesson navigation
apply_filters('learndash_lesson_nav', $nav, $lesson_id)

// Quiz questions
apply_filters('learndash_quiz_questions', $questions, $quiz_id)

// User progress
apply_filters('learndash_user_progress', $progress, $user_id, $course_id)
```

### Key Actions

```php
// Course enrollment
do_action('learndash_update_course_access', $user_id, $course_id, $access)

// Lesson completion
do_action('learndash_lesson_completed', $data)

// Quiz completion
do_action('learndash_quiz_completed', $data)

// Course completion
do_action('learndash_course_completed', $data)
```

---

**Need Development Help?**  
📧 Email: support@wbcomdesigns.com  
👨‍💻 Custom development available  
📚 API Docs: docs.wbcomdesigns.com/api  
💬 Developer forum: wbcomdesigns.com/dev-support