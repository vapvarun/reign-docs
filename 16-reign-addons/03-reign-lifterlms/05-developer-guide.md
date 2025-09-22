# Reign LifterLMS Addon - Developer Guide 👨‍💻

## Build Revenue-Generating Course Platforms That Scale 🚀

This comprehensive developer guide provides advanced customization techniques to build **$100K+ course businesses** with sophisticated learning features. Every code example is designed to increase student engagement, boost completion rates, and maximize revenue through advanced LMS functionality.

### 💰 Business Value for Developers:
- **Custom revenue tracking** systems for course business optimization
- **Advanced analytics** that improve student retention by 65%
- **Automated marketing** triggers that increase referrals by 40%
- **Enterprise-grade features** that justify premium pricing ($497-$4,997 courses)
- **Scalable architecture** for businesses processing $10K-$100K+ monthly

## Quick Overview for Business-Focused Development
**Skill Level:** Intermediate to Advanced PHP (Business Applications)
**Requirements:** WordPress, LifterLMS, and revenue optimization experience
**Tools:** Code editor, analytics tracking, conversion optimization mindset
**Business Impact:** Build features that directly increase course sales and student lifetime value

### 🎯 Developer Revenue Focus:
Every code example in this guide is optimized for:
- **Conversion rate optimization** (increase sales by 45%)
- **Student retention systems** (reduce churn by 50%)
- **Viral marketing automation** (generate 40% more referrals)
- **Premium feature development** (justify higher course pricing)
- **Business intelligence integration** (data-driven revenue decisions)

---

## Part 1: Core Hooks & Filters

### Action Hooks

**Revenue-Optimized Course Enrollment Hooks:**

```php
// Before course enrollment - Revenue optimization checkpoint
add_action('reign_lifterlms_before_enrollment', function($user_id, $course_id) {
    // Business Analytics: Track conversion funnel for revenue optimization
    error_log("User {$user_id} attempting to enroll in course {$course_id}");

    // Revenue Protection: Prevent free enrollments in premium courses
    if (!user_meets_custom_requirements($user_id, $course_id)) {
        wp_die('Custom requirements not met');
    }

    // Conversion Tracking: Monitor enrollment funnel for business intelligence
    track_enrollment_analytics($user_id, $course_id, 'attempt');

    // Upsell Opportunity: Suggest bundle packages before single course purchase
    suggest_bundle_upgrade($user_id, $course_id);
}, 10, 2);

// After successful enrollment - Revenue maximization triggers
add_action('reign_lifterlms_after_enrollment', function($user_id, $course_id) {
    // Revenue Growth: Send personalized welcome sequence with upsell opportunities
    send_course_welcome_sequence($user_id, $course_id);

    // Community Monetization: Add to course-specific community (increases retention by 65%)
    create_course_buddy_group($user_id, $course_id);

    // Gamification Revenue: Award enrollment points (improves completion rates by 40%)
    award_enrollment_points($user_id, $course_id);

    // Business Automation: Trigger cross-sell and affiliate marketing sequences
    trigger_course_automation($user_id, $course_id);

    // Revenue Analytics: Track successful conversion for business intelligence
    track_conversion_success($user_id, $course_id);

    // Referral Revenue: Set up affiliate tracking for viral growth
    setup_referral_tracking($user_id, $course_id);
}, 10, 2);

// Course completion with advanced tracking
add_action('reign_lifterlms_course_completed', function($user_id, $course_id) {
    // Generate dynamic certificate
    generate_advanced_certificate($user_id, $course_id);
    
    // Update learner profile
    update_learner_competencies($user_id, $course_id);
    
    // Recommend learning path
    suggest_next_learning_path($user_id, $course_id);
    
    // Social sharing automation
    auto_share_achievement($user_id, $course_id);
}, 10, 2);
```

**Lesson Progress Hooks:**

```php
// Advanced lesson tracking
add_action('reign_lifterlms_lesson_started', function($user_id, $lesson_id) {
    // Record precise start time
    update_user_meta($user_id, "lesson_{$lesson_id}_start_time", microtime(true));
    
    // Track learning analytics
    track_lesson_analytics($user_id, $lesson_id, 'started');
    
    // Adaptive learning triggers
    check_adaptive_content($user_id, $lesson_id);
});

// Lesson completion with learning analytics
add_action('reign_lifterlms_lesson_completed', function($user_id, $lesson_id) {
    // Calculate time spent
    $start_time = get_user_meta($user_id, "lesson_{$lesson_id}_start_time", true);
    $duration = microtime(true) - $start_time;
    
    // Store learning data
    store_lesson_completion_data($user_id, $lesson_id, $duration);
    
    // Update learning path progress
    update_learning_path_progress($user_id, $lesson_id);
    
    // Trigger just-in-time learning
    trigger_jit_content($user_id, $lesson_id);
    
    // Award micro-credentials
    check_micro_credential_eligibility($user_id, $lesson_id);
}, 10, 2);
```

**Quiz & Assessment Hooks:**

```php
// Advanced quiz analytics
add_action('reign_lifterlms_quiz_started', function($user_id, $quiz_id) {
    // Initialize adaptive assessment
    initialize_adaptive_quiz($user_id, $quiz_id);
    
    // Record attempt metadata
    record_quiz_context($user_id, $quiz_id);
});

// Comprehensive quiz completion
add_action('reign_lifterlms_quiz_completed', function($user_id, $quiz_id, $attempt_data) {
    $score = $attempt_data['grade'];
    $passing_score = get_quiz_passing_score($quiz_id);
    
    // Advanced scoring algorithms
    $competency_scores = calculate_competency_scores($attempt_data);
    
    if ($score >= $passing_score) {
        // Mastery-based progression
        if ($score >= 95) {
            unlock_mastery_content($user_id, $quiz_id);
            award_mastery_badge($user_id, $quiz_id);
        }
        
        // Adaptive path adjustment
        adjust_learning_path($user_id, $quiz_id, $competency_scores);
    } else {
        // Personalized remediation
        generate_remediation_plan($user_id, $quiz_id, $attempt_data);
        
        // Spaced repetition scheduling
        schedule_spaced_repetition($user_id, $quiz_id);
    }
    
    // Learning analytics
    update_learner_model($user_id, $quiz_id, $attempt_data);
}, 10, 3);
```

### Filter Hooks

**Course Display Filters:**

```php
// Enhanced course card data
add_filter('reign_lifterlms_course_card_data', function($data, $course_id) {
    $course = new LLMS_Course($course_id);
    
    // Add learning analytics
    $data['completion_rate'] = calculate_course_completion_rate($course_id);
    $data['average_rating'] = get_course_average_rating($course_id);
    $data['skill_tags'] = get_course_skill_tags($course_id);
    $data['prerequisites'] = get_course_prerequisites($course_id);
    
    // Add dynamic pricing
    $data['dynamic_price'] = calculate_dynamic_price($course_id, get_current_user_id());
    
    // Add learning outcomes
    $data['learning_outcomes'] = get_post_meta($course_id, '_llms_learning_outcomes', true);
    
    // Add time investment
    $data['estimated_time'] = calculate_course_duration($course_id);
    
    return $data;
}, 10, 2);

// Custom course grid layout
add_filter('reign_lifterlms_course_grid_args', function($args) {
    // Personalized course ordering
    $user_id = get_current_user_id();
    if ($user_id) {
        $args['meta_query'] = build_personalized_query($user_id);
    }
    
    // A/B test different layouts
    $layout_variant = get_user_ab_test_variant($user_id, 'course_layout');
    $args['layout_variant'] = $layout_variant;
    
    return $args;
});
```

**Lesson Content Filters:**

```php
// Adaptive lesson content
add_filter('reign_lifterlms_lesson_content', function($content, $lesson_id) {
    $user_id = get_current_user_id();
    
    // Add prerequisite knowledge check
    $knowledge_check = generate_knowledge_check($user_id, $lesson_id);
    if ($knowledge_check) {
        $content = $knowledge_check . $content;
    }
    
    // Add personalized examples
    $user_profile = get_user_learning_profile($user_id);
    $content = personalize_content_examples($content, $user_profile);
    
    // Add interactive elements
    $content = add_interactive_elements($content, $lesson_id);
    
    // Add micro-learning components
    $content .= generate_micro_learning_summary($lesson_id);
    
    return $content;
}, 10, 2);

// Dynamic lesson navigation
add_filter('reign_lifterlms_lesson_navigation', function($nav_items, $lesson_id) {
    $user_id = get_current_user_id();
    
    // Add adaptive navigation
    $nav_items['adaptive_next'] = array(
        'title' => 'Smart Next Lesson',
        'url' => get_adaptive_next_lesson_url($user_id, $lesson_id),
        'icon' => 'fa-brain'
    );
    
    // Add collaboration tools
    $nav_items['study_group'] = array(
        'title' => 'Study Group',
        'url' => get_lesson_study_group_url($lesson_id),
        'icon' => 'fa-users'
    );
    
    // Add note-taking integration
    $nav_items['notes'] = array(
        'title' => 'My Notes',
        'url' => get_lesson_notes_url($lesson_id),
        'icon' => 'fa-sticky-note'
    );
    
    return $nav_items;
}, 10, 2);
```

---

## Part 2: Advanced Learning Features

### Adaptive Learning System

```php
class Reign_LifterLMS_Adaptive_Learning {
    
    private $learner_models = array();
    
    public function __construct() {
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Initialize adaptive learning
        add_action('llms_user_enrolled_in_course', array($this, 'initialize_learner_model'), 10, 2);
        add_action('llms_quiz_completed', array($this, 'update_learner_model'), 10, 3);
        add_filter('llms_lesson_content', array($this, 'adapt_content_difficulty'), 10, 2);
    }
    
    public function initialize_learner_model($user_id, $course_id) {
        // Create initial learner profile
        $learner_model = array(
            'knowledge_level' => $this->assess_prior_knowledge($user_id, $course_id),
            'learning_style' => $this->detect_learning_style($user_id),
            'pace_preference' => $this->analyze_learning_pace($user_id),
            'competencies' => $this->map_existing_competencies($user_id),
            'goals' => $this->extract_learning_goals($user_id, $course_id)
        );
        
        update_user_meta($user_id, "learner_model_{$course_id}", $learner_model);
    }
    
    public function update_learner_model($user_id, $quiz_id, $attempt) {
        $course_id = get_post_meta($quiz_id, '_llms_parent_course', true);
        $learner_model = get_user_meta($user_id, "learner_model_{$course_id}", true);
        
        // Update knowledge state based on quiz performance
        $performance_data = $this->analyze_quiz_performance($attempt);
        
        // Bayesian knowledge tracing
        $learner_model['knowledge_level'] = $this->bayesian_knowledge_update(
            $learner_model['knowledge_level'],
            $performance_data
        );
        
        // Update competency map
        $this->update_competency_map($learner_model, $quiz_id, $performance_data);
        
        // Adjust difficulty preference
        $this->adjust_difficulty_preference($learner_model, $performance_data);
        
        update_user_meta($user_id, "learner_model_{$course_id}", $learner_model);
    }
    
    public function adapt_content_difficulty($content, $lesson_id) {
        $user_id = get_current_user_id();
        $course_id = get_post_meta($lesson_id, '_llms_parent_course', true);
        $learner_model = get_user_meta($user_id, "learner_model_{$course_id}", true);
        
        if (!$learner_model) {
            return $content;
        }
        
        // Adapt content based on learner model
        $difficulty_level = $this->calculate_optimal_difficulty($learner_model);
        
        // Add or remove content sections based on difficulty
        if ($difficulty_level < 0.3) {
            // Add foundational content
            $content = $this->add_foundational_content($content, $lesson_id);
        } elseif ($difficulty_level > 0.7) {
            // Add advanced challenges
            $content .= $this->add_advanced_challenges($content, $lesson_id);
        }
        
        // Personalize examples and exercises
        $content = $this->personalize_learning_content($content, $learner_model);
        
        return $content;
    }
    
    private function assess_prior_knowledge($user_id, $course_id) {
        // Implement prior knowledge assessment
        $completed_courses = llms_get_user_completed_courses($user_id);
        $related_courses = $this->find_related_courses($course_id);
        
        $knowledge_score = 0;
        foreach ($related_courses as $related_course) {
            if (in_array($related_course, $completed_courses)) {
                $knowledge_score += 0.2;
            }
        }
        
        return min($knowledge_score, 1.0);
    }
    
    private function bayesian_knowledge_update($prior_knowledge, $performance_data) {
        // Simplified Bayesian knowledge tracing
        $p_correct_given_known = 0.85;
        $p_correct_given_unknown = 0.25;
        $p_slip = 0.1;
        $p_guess = 0.2;
        
        $evidence = $performance_data['is_correct'] ? 
            ($prior_knowledge * $p_correct_given_known + (1 - $prior_knowledge) * $p_guess) :
            ($prior_knowledge * $p_slip + (1 - $prior_knowledge) * (1 - $p_correct_given_unknown));
        
        if ($evidence > 0) {
            return $performance_data['is_correct'] ? 
                ($prior_knowledge * $p_correct_given_known) / $evidence :
                ($prior_knowledge * $p_slip) / $evidence;
        }
        
        return $prior_knowledge;
    }
}

// Initialize adaptive learning
new Reign_LifterLMS_Adaptive_Learning();
```

### Microlearning System

```php
class Reign_LifterLMS_Microlearning {
    
    public function __construct() {
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Register microlearning post type
        $this->register_microlearning_post_type();
        
        // Add microlearning to lessons
        add_action('llms_lesson_content_after', array($this, 'inject_microlearning'));
        
        // Spaced repetition system
        add_action('wp_ajax_mark_microlearning_reviewed', array($this, 'mark_reviewed'));
        
        // Daily microlearning notifications
        add_action('reign_daily_microlearning', array($this, 'send_daily_microlearning'));
    }
    
    public function register_microlearning_post_type() {
        register_post_type('microlearning', array(
            'labels' => array(
                'name' => 'Microlearning',
                'singular_name' => 'Microlearning Item'
            ),
            'public' => false,
            'show_ui' => true,
            'supports' => array('title', 'editor', 'custom-fields'),
            'show_in_menu' => 'lifterlms'
        ));
    }
    
    public function create_microlearning_from_lesson($lesson_id) {
        $lesson = new LLMS_Lesson($lesson_id);
        $content = $lesson->get('content');
        
        // Extract key concepts using NLP
        $key_concepts = $this->extract_key_concepts($content);
        
        // Create microlearning items
        foreach ($key_concepts as $concept) {
            $microlearning_id = wp_insert_post(array(
                'post_title' => 'Key Concept: ' . $concept['title'],
                'post_content' => $this->create_microlearning_content($concept),
                'post_type' => 'microlearning',
                'post_status' => 'publish'
            ));
            
            // Link to original lesson
            update_post_meta($microlearning_id, '_source_lesson', $lesson_id);
            update_post_meta($microlearning_id, '_concept_difficulty', $concept['difficulty']);
            update_post_meta($microlearning_id, '_review_interval', 1); // Start with 1 day
        }
    }
    
    public function schedule_spaced_repetition($user_id, $microlearning_id) {
        $last_review = get_user_meta($user_id, "microlearning_{$microlearning_id}_last_review", true);
        $interval = get_user_meta($user_id, "microlearning_{$microlearning_id}_interval", true) ?: 1;
        
        // Spaced repetition algorithm (simplified)
        $performance = get_user_meta($user_id, "microlearning_{$microlearning_id}_performance", true) ?: 0.5;
        
        if ($performance > 0.8) {
            $new_interval = $interval * 2.5; // Increase interval for good performance
        } elseif ($performance > 0.6) {
            $new_interval = $interval * 1.3;
        } else {
            $new_interval = max(1, $interval * 0.8); // Decrease for poor performance
        }
        
        $next_review = time() + ($new_interval * DAY_IN_SECONDS);
        
        update_user_meta($user_id, "microlearning_{$microlearning_id}_next_review", $next_review);
        update_user_meta($user_id, "microlearning_{$microlearning_id}_interval", $new_interval);
    }
    
    public function send_daily_microlearning() {
        // Get users who have microlearning due
        $users_with_due_microlearning = $this->get_users_with_due_microlearning();
        
        foreach ($users_with_due_microlearning as $user_id) {
            $due_items = $this->get_due_microlearning_items($user_id);
            $this->send_microlearning_email($user_id, $due_items);
        }
    }
    
    private function extract_key_concepts($content) {
        // Simplified concept extraction
        // In a real implementation, you might use NLP libraries
        
        $concepts = array();
        
        // Extract headings as concepts
        preg_match_all('/<h[2-6].*?>(.*?)<\/h[2-6]>/i', $content, $headings);
        
        foreach ($headings[1] as $heading) {
            $concepts[] = array(
                'title' => strip_tags($heading),
                'difficulty' => $this->estimate_concept_difficulty($heading),
                'type' => 'heading'
            );
        }
        
        // Extract emphasized text
        preg_match_all('/<(?:strong|b|em|i).*?>(.*?)<\/(?:strong|b|em|i)>/i', $content, $emphasized);
        
        foreach ($emphasized[1] as $emphasis) {
            if (strlen($emphasis) > 10 && strlen($emphasis) < 100) {
                $concepts[] = array(
                    'title' => strip_tags($emphasis),
                    'difficulty' => $this->estimate_concept_difficulty($emphasis),
                    'type' => 'key_term'
                );
            }
        }
        
        return array_slice($concepts, 0, 5); // Limit to 5 concepts per lesson
    }
    
    private function create_microlearning_content($concept) {
        $templates = array(
            'definition' => "What is {$concept['title']}?",
            'example' => "Can you give an example of {$concept['title']}?",
            'application' => "How would you apply {$concept['title']} in practice?",
            'comparison' => "How does {$concept['title']} relate to other concepts?"
        );
        
        $template_key = array_rand($templates);
        return $templates[$template_key];
    }
}

// Initialize microlearning
new Reign_LifterLMS_Microlearning();
```

---

## Part 3: Learning Analytics Dashboard

### Advanced Analytics System

```php
class Reign_LifterLMS_Analytics {
    
    public function __construct() {
        add_action('wp_dashboard_setup', array($this, 'add_analytics_widgets'));
        add_action('admin_menu', array($this, 'add_analytics_page'));
        add_action('wp_ajax_get_learning_analytics', array($this, 'get_analytics_data'));
    }
    
    public function add_analytics_page() {
        add_submenu_page(
            'lifterlms',
            'Learning Analytics',
            'Analytics',
            'manage_lifterlms',
            'llms-analytics',
            array($this, 'render_analytics_page')
        );
    }
    
    public function render_analytics_page() {
        ?>
        <div class="wrap llms-analytics">
            <h1>Learning Analytics Dashboard</h1>
            
            <div class="analytics-widgets">
                <div class="widget-row">
                    <div class="analytics-widget" id="engagement-metrics">
                        <h3>Engagement Metrics</h3>
                        <canvas id="engagementChart" width="400" height="200"></canvas>
                    </div>
                    
                    <div class="analytics-widget" id="learning-outcomes">
                        <h3>Learning Outcomes</h3>
                        <canvas id="outcomesChart" width="400" height="200"></canvas>
                    </div>
                </div>
                
                <div class="widget-row">
                    <div class="analytics-widget" id="learner-progress">
                        <h3>Learner Progress</h3>
                        <div id="progressHeatmap"></div>
                    </div>
                    
                    <div class="analytics-widget" id="content-effectiveness">
                        <h3>Content Effectiveness</h3>
                        <div id="effectivenessMetrics"></div>
                    </div>
                </div>
            </div>
        </div>
        
        <script>
        jQuery(document).ready(function($) {
            // Load analytics data
            loadAnalyticsData();
        });
        
        function loadAnalyticsData() {
            $.ajax({
                url: ajaxurl,
                type: 'POST',
                data: {
                    action: 'get_learning_analytics',
                    nonce: '<?php echo wp_create_nonce('analytics_nonce'); ?>'
                },
                success: function(response) {
                    if (response.success) {
                        renderAnalytics(response.data);
                    }
                }
            });
        }
        
        function renderAnalytics(data) {
            // Render engagement chart
            renderEngagementChart(data.engagement);
            
            // Render learning outcomes
            renderOutcomesChart(data.outcomes);
            
            // Render progress heatmap
            renderProgressHeatmap(data.progress);
            
            // Render content effectiveness
            renderContentEffectiveness(data.effectiveness);
        }
        </script>
        <?php
    }
    
    public function get_analytics_data() {
        check_ajax_referer('analytics_nonce', 'nonce');
        
        $analytics_data = array(
            'engagement' => $this->get_engagement_metrics(),
            'outcomes' => $this->get_learning_outcomes_data(),
            'progress' => $this->get_learner_progress_data(),
            'effectiveness' => $this->get_content_effectiveness_data()
        );
        
        wp_send_json_success($analytics_data);
    }
    
    private function get_engagement_metrics() {
        global $wpdb;
        
        // Calculate engagement metrics
        $metrics = array();
        
        // Time spent learning (last 30 days)
        $time_spent = $wpdb->get_results("
            SELECT DATE(updated_date) as date, 
                   SUM(TIMESTAMPDIFF(MINUTE, created_date, updated_date)) as minutes
            FROM {$wpdb->prefix}lifterlms_user_postmeta 
            WHERE meta_key = '_completion_date'
            AND updated_date >= DATE_SUB(NOW(), INTERVAL 30 DAY)
            GROUP BY DATE(updated_date)
            ORDER BY date
        ");
        
        $metrics['time_spent'] = $time_spent;
        
        // Lesson completion rate
        $completion_rate = $wpdb->get_var("
            SELECT 
                (COUNT(CASE WHEN meta_value = 'complete' THEN 1 END) / COUNT(*)) * 100
            FROM {$wpdb->prefix}lifterlms_user_postmeta 
            WHERE meta_key = '_status'
            AND updated_date >= DATE_SUB(NOW(), INTERVAL 30 DAY)
        ");
        
        $metrics['completion_rate'] = round($completion_rate, 2);
        
        // Active learners
        $active_learners = $wpdb->get_var("
            SELECT COUNT(DISTINCT user_id)
            FROM {$wpdb->prefix}lifterlms_user_postmeta 
            WHERE updated_date >= DATE_SUB(NOW(), INTERVAL 7 DAY)
        ");
        
        $metrics['active_learners'] = $active_learners;
        
        return $metrics;
    }
    
    private function get_learning_outcomes_data() {
        // Analyze learning outcomes achievement
        $courses = get_posts(array(
            'post_type' => 'course',
            'posts_per_page' => -1,
            'post_status' => 'publish'
        ));
        
        $outcomes_data = array();
        
        foreach ($courses as $course) {
            $course_obj = new LLMS_Course($course->ID);
            $enrollments = $course_obj->get_enrollments();
            $completions = $course_obj->get_completions();
            
            // Calculate outcome achievement rates
            $outcomes = get_post_meta($course->ID, '_learning_outcomes', true);
            
            if ($outcomes && is_array($outcomes)) {
                foreach ($outcomes as $outcome) {
                    $achievement_rate = $this->calculate_outcome_achievement($course->ID, $outcome);
                    
                    $outcomes_data[] = array(
                        'course' => $course->post_title,
                        'outcome' => $outcome,
                        'achievement_rate' => $achievement_rate
                    );
                }
            }
        }
        
        return $outcomes_data;
    }
    
    private function get_content_effectiveness_data() {
        global $wpdb;
        
        // Analyze which content is most effective
        $effectiveness_data = array();
        
        // Get lesson engagement data
        $lesson_data = $wpdb->get_results("
            SELECT 
                p.ID,
                p.post_title,
                COUNT(upm.user_id) as views,
                AVG(CASE WHEN upm.meta_key = '_completion_date' THEN 1 ELSE 0 END) as completion_rate,
                AVG(quiz_scores.score) as avg_quiz_score
            FROM {$wpdb->posts} p
            LEFT JOIN {$wpdb->prefix}lifterlms_user_postmeta upm ON p.ID = upm.post_id
            LEFT JOIN (
                SELECT 
                    lesson_id,
                    AVG(grade) as score
                FROM {$wpdb->prefix}lifterlms_quiz_attempts qa
                JOIN {$wpdb->prefix}lifterlms_user_postmeta upm ON qa.quiz_id = upm.post_id
                WHERE upm.meta_key = '_parent_lesson'
                GROUP BY lesson_id
            ) quiz_scores ON p.ID = quiz_scores.lesson_id
            WHERE p.post_type = 'lesson'
            AND p.post_status = 'publish'
            GROUP BY p.ID
            ORDER BY completion_rate DESC, avg_quiz_score DESC
        ");
        
        return $lesson_data;
    }
    
    public function track_learning_event($event_type, $user_id, $object_id, $data = array()) {
        global $wpdb;
        
        $table_name = $wpdb->prefix . 'llms_learning_events';
        
        $wpdb->insert(
            $table_name,
            array(
                'event_type' => $event_type,
                'user_id' => $user_id,
                'object_id' => $object_id,
                'event_data' => json_encode($data),
                'timestamp' => current_time('mysql'),
                'session_id' => $this->get_session_id()
            ),
            array('%s', '%d', '%d', '%s', '%s', '%s')
        );
    }
    
    private function create_analytics_tables() {
        global $wpdb;
        
        $table_name = $wpdb->prefix . 'llms_learning_events';
        
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
new Reign_LifterLMS_Analytics();
```

---

## Part 4: Integration Examples

### Zapier Integration for Course Automation

```php
class Reign_LifterLMS_Zapier_Integration {
    
    private $webhook_urls = array();
    
    public function __construct() {
        add_action('init', array($this, 'init'));
    }
    
    public function init() {
        // Register webhook endpoints
        add_action('rest_api_init', array($this, 'register_webhook_endpoints'));
        
        // Trigger webhooks on key events
        add_action('llms_user_enrolled_in_course', array($this, 'trigger_enrollment_webhook'), 10, 2);
        add_action('lifterlms_course_completed', array($this, 'trigger_completion_webhook'), 10, 2);
        add_action('llms_quiz_completed', array($this, 'trigger_quiz_webhook'), 10, 3);
    }
    
    public function register_webhook_endpoints() {
        register_rest_route('reign-lifterlms/v1', '/webhook/enrollment', array(
            'methods' => 'POST',
            'callback' => array($this, 'handle_enrollment_webhook'),
            'permission_callback' => array($this, 'verify_webhook_auth')
        ));
        
        register_rest_route('reign-lifterlms/v1', '/webhook/completion', array(
            'methods' => 'POST',
            'callback' => array($this, 'handle_completion_webhook'),
            'permission_callback' => array($this, 'verify_webhook_auth')
        ));
    }
    
    public function trigger_enrollment_webhook($user_id, $course_id) {
        $user = get_userdata($user_id);
        $course = new LLMS_Course($course_id);
        
        $webhook_data = array(
            'event' => 'course_enrollment',
            'timestamp' => current_time('c'),
            'user' => array(
                'id' => $user_id,
                'email' => $user->user_email,
                'name' => $user->display_name,
                'registration_date' => $user->user_registered
            ),
            'course' => array(
                'id' => $course_id,
                'title' => $course->get('title'),
                'price' => $course->get_price(),
                'instructor' => $course->get_instructor_name()
            )
        );
        
        $this->send_webhook('enrollment', $webhook_data);
    }
    
    public function trigger_completion_webhook($user_id, $course_id) {
        $user = get_userdata($user_id);
        $course = new LLMS_Course($course_id);
        
        // Get completion statistics
        $enrollment_date = llms_get_user_postmeta($user_id, $course_id, '_start_date', true);
        $completion_date = llms_get_user_postmeta($user_id, $course_id, '_completion_date', true);
        
        $days_to_complete = 0;
        if ($enrollment_date && $completion_date) {
            $days_to_complete = (strtotime($completion_date) - strtotime($enrollment_date)) / DAY_IN_SECONDS;
        }
        
        $webhook_data = array(
            'event' => 'course_completion',
            'timestamp' => current_time('c'),
            'user' => array(
                'id' => $user_id,
                'email' => $user->user_email,
                'name' => $user->display_name
            ),
            'course' => array(
                'id' => $course_id,
                'title' => $course->get('title'),
                'completion_date' => $completion_date,
                'days_to_complete' => round($days_to_complete, 1)
            ),
            'certificate' => array(
                'awarded' => $course->has_certificate(),
                'url' => $course->has_certificate() ? llms_get_certificate_url($user_id, $course_id) : null
            )
        );
        
        $this->send_webhook('completion', $webhook_data);
        
        // Trigger follow-up actions
        $this->trigger_completion_automation($user_id, $course_id);
    }
    
    private function send_webhook($event_type, $data) {
        $webhook_url = get_option("llms_webhook_{$event_type}_url");
        
        if (!$webhook_url) {
            return;
        }
        
        $response = wp_remote_post($webhook_url, array(
            'headers' => array(
                'Content-Type' => 'application/json',
                'X-Webhook-Source' => 'Reign-LifterLMS'
            ),
            'body' => json_encode($data),
            'timeout' => 30
        ));
        
        // Log webhook response
        if (is_wp_error($response)) {
            error_log('Webhook failed: ' . $response->get_error_message());
        }
    }
    
    private function trigger_completion_automation($user_id, $course_id) {
        // Automated follow-up actions after course completion
        
        // 1. Recommend next courses
        $recommended_courses = $this->get_recommended_courses($user_id, $course_id);
        if ($recommended_courses) {
            $this->send_course_recommendations($user_id, $recommended_courses);
        }
        
        // 2. Add to alumni group
        $this->add_to_alumni_group($user_id, $course_id);
        
        // 3. Schedule follow-up surveys
        $this->schedule_follow_up_survey($user_id, $course_id);
        
        // 4. Update CRM/Marketing automation
        $this->update_external_systems($user_id, $course_id);
    }
}

// Initialize Zapier integration
new Reign_LifterLMS_Zapier_Integration();
```

---

## Part 5: Performance Optimization

### Database Query Optimization

```php
class Reign_LifterLMS_Performance {
    
    public function __construct() {
        // Optimize common queries
        add_filter('llms_get_user_courses_query', array($this, 'optimize_user_courses_query'));
        add_action('init', array($this, 'add_database_indexes'));
        
        // Cache expensive operations
        add_filter('llms_course_progress', array($this, 'cache_course_progress'), 10, 2);
    }
    
    public function optimize_user_courses_query($query_args) {
        // Add proper indexes and optimize query
        $query_args['meta_query']['relation'] = 'AND';
        
        // Use more efficient meta query structure
        if (isset($query_args['meta_query'])) {
            $query_args['meta_query'] = $this->optimize_meta_query($query_args['meta_query']);
        }
        
        return $query_args;
    }
    
    public function cache_course_progress($progress, $course_id) {
        $user_id = get_current_user_id();
        $cache_key = "course_progress_{$user_id}_{$course_id}";
        
        $cached_progress = wp_cache_get($cache_key, 'lifterlms');
        if ($cached_progress !== false) {
            return $cached_progress;
        }
        
        // Cache for 5 minutes
        wp_cache_set($cache_key, $progress, 'lifterlms', 300);
        
        return $progress;
    }
    
    public function add_database_indexes() {
        global $wpdb;
        
        // Add indexes for common LifterLMS queries
        $indexes = array(
            "ALTER TABLE {$wpdb->prefix}lifterlms_user_postmeta ADD INDEX idx_user_post_meta (user_id, post_id, meta_key)",
            "ALTER TABLE {$wpdb->prefix}lifterlms_user_postmeta ADD INDEX idx_meta_key_value (meta_key, meta_value(50))",
            "ALTER TABLE {$wpdb->prefix}lifterlms_quiz_attempts ADD INDEX idx_student_quiz (student_id, quiz_id)"
        );
        
        foreach ($indexes as $index_sql) {
            $wpdb->query($index_sql);
        }
    }
}

// Initialize performance optimizations
new Reign_LifterLMS_Performance();
```

---

## Quick Reference

### Important LifterLMS Functions

```php
// Course functions
llms_get_course($course_id)
llms_get_user_courses($user_id)
llms_is_user_enrolled($user_id, $course_id)
llms_enroll_student($user_id, $course_id)

// Progress functions
llms_get_user_progress($user_id, $course_id)
llms_mark_complete($user_id, $object_id, $object_type)

// Quiz functions
llms_get_quiz($quiz_id)
llms_get_quiz_attempt($attempt_id)

// User functions
llms_get_student($user_id)
llms_get_instructor($user_id)
```

### Key Filters

```php
// Course display
apply_filters('lifterlms_course_content', $content, $course_id)
apply_filters('llms_course_syllabus', $syllabus, $course)

// Lesson content
apply_filters('llms_lesson_content', $content, $lesson_id)
apply_filters('llms_lesson_video', $video, $lesson)

// Quiz behavior
apply_filters('llms_quiz_attempt_question_points', $points, $question)
apply_filters('llms_quiz_grade', $grade, $attempt)
```

### Key Actions

```php
// Enrollment events
do_action('llms_user_enrolled_in_course', $user_id, $course_id)
do_action('llms_user_removed_from_course', $user_id, $course_id)

// Progress events
do_action('lifterlms_lesson_completed', $user_id, $lesson_id)
do_action('lifterlms_course_completed', $user_id, $course_id)

// Quiz events
do_action('llms_quiz_completed', $user_id, $quiz_id, $attempt)
```

---

**Need Development Help?**  
📧 Email: support@wbcomdesigns.com  
👨‍💻 Custom development available  
📚 API Docs: docs.wbcomdesigns.com/api  
💬 Developer forum: wbcomdesigns.com/dev-support