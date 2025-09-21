# Activity Control Documentation

## Overview

Activity Control in Reign Theme provides comprehensive management of BuddyPress activity streams, allowing administrators to filter, moderate, customize, and control what appears in activity feeds. This includes content filtering, user permissions, activity types management, and advanced moderation tools.

## Core Features

- **Activity Type Management:** Control which activities appear
- **Content Moderation:** Filter and moderate posts
- **Privacy Controls:** Set visibility rules
- **Spam Protection:** Automated and manual spam control
- **Activity Templates:** Custom activity layouts
- **Performance Optimization:** Caching and lazy loading
- **Analytics:** Track activity engagement

## Activity Settings

### Global Configuration

**Location:** `Customizer → BuddyPress → Activity`

```
Enable Activity Stream: Yes
Default Tab: All Members / Friends / Groups / Mentions
Activities Per Page: 20
Load More Type: Button / Infinite Scroll / Pagination
Enable Comments: Yes
Enable Favorites: Yes
Enable Reshare: Yes
Character Limit: 0 (unlimited)
```

### Activity Types Control

**Location:** `Settings → BuddyPress → Activity`

#### Available Activity Types

| Type | Description | Default |
|------|-------------|---------|
| activity_update | Status updates | ✓ |
| new_member | New user registrations | ✓ |
| new_avatar | Profile photo changes | ✓ |
| updated_profile | Profile updates | ✓ |
| friendship_accepted | New friendships | ✓ |
| friendship_created | Friend requests | ✓ |
| created_group | New groups | ✓ |
| joined_group | Group joins | ✓ |
| group_details_updated | Group changes | ✓ |
| new_blog_post | Blog posts | ✓ |
| new_blog_comment | Blog comments | ✗ |

#### Disable Specific Types

```php
// Disable specific activity types
add_filter('bp_activity_set_action', function($args) {
    $disabled_types = array('new_avatar', 'updated_profile');

    if (in_array($args['type'], $disabled_types)) {
        return false;
    }
    return $args;
});

// Or via settings
function reign_disable_activity_types() {
    $types = array('new_blog_comment', 'friendship_created');
    foreach ($types as $type) {
        bp_activity_set_action_hidden($type, true);
    }
}
add_action('bp_init', 'reign_disable_activity_types');
```

## Content Filtering

### Bad Words Filter

```php
// Add bad words filter
add_filter('bp_activity_content_before_save', function($content) {
    $bad_words = array('spam', 'inappropriate', 'blocked');
    $replacement = '***';

    foreach ($bad_words as $word) {
        $content = str_ireplace($word, $replacement, $content);
    }

    return $content;
});
```

### Content Length Limits

```php
// Enforce character limits
add_filter('bp_activity_content_before_save', function($content) {
    $max_length = 500;

    if (strlen($content) > $max_length) {
        $content = substr($content, 0, $max_length);
        bp_core_add_message('Activity limited to ' . $max_length . ' characters', 'error');
    }

    return $content;
});
```

### Link Restrictions

```php
// Limit number of links
add_filter('bp_activity_content_before_save', function($content) {
    $max_links = 2;
    $link_count = preg_match_all('/https?:\/\//i', $content);

    if ($link_count > $max_links) {
        bp_core_add_message('Maximum ' . $max_links . ' links allowed', 'error');
        return false;
    }

    return $content;
});
```

## Privacy Controls

### Activity Visibility Levels

```php
// Set default activity privacy
add_filter('bp_activity_default_privacy', function() {
    return 'friends'; // public, friends, onlyme
});

// Add custom privacy levels
add_filter('bp_activity_privacy_levels', function($levels) {
    $levels['group_members'] = array(
        'label' => 'Group Members Only',
        'privacy' => 'group_members'
    );
    return $levels;
});
```

### User-Based Visibility

```php
// Control who sees activities
add_filter('bp_activity_user_can_read', function($can_read, $activity) {
    // Hide from non-friends
    if (!friends_check_friendship(get_current_user_id(), $activity->user_id)) {
        return false;
    }

    // Hide from blocked users
    if (is_user_blocked($activity->user_id, get_current_user_id())) {
        return false;
    }

    return $can_read;
}, 10, 2);
```

### Component-Based Privacy

```php
// Hide group activities from non-members
add_filter('bp_activity_get_where_conditions', function($where, $args) {
    if ($args['component'] == 'groups') {
        $user_groups = groups_get_user_groups(get_current_user_id());
        if (!empty($user_groups['groups'])) {
            $where['groups'] = "item_id IN (" . implode(',', $user_groups['groups']) . ")";
        }
    }
    return $where;
}, 10, 2);
```

## Spam Protection

### Automated Spam Detection

```php
// Spam detection system
class Reign_Activity_Spam_Detector {

    public function __construct() {
        add_filter('bp_activity_content_before_save', array($this, 'check_spam'));
        add_action('bp_activity_posted_update', array($this, 'check_rate_limit'), 10, 3);
    }

    public function check_spam($content) {
        // Check for spam patterns
        $spam_patterns = array(
            '/\b(viagra|cialis|casino|lottery)\b/i',
            '/https?:\/\/[^\s]{50,}/i', // Very long URLs
            '/(.)\1{10,}/i', // Repeated characters
            '/[A-Z\s]{20,}/i' // All caps
        );

        foreach ($spam_patterns as $pattern) {
            if (preg_match($pattern, $content)) {
                $this->mark_as_spam($content);
                return false;
            }
        }

        return $content;
    }

    public function check_rate_limit($content, $user_id, $activity_id) {
        $recent_count = $this->get_recent_activity_count($user_id, 5); // Last 5 minutes

        if ($recent_count > 5) {
            bp_activity_mark_as_spam($activity_id);
            $this->notify_admin($user_id, 'Rate limit exceeded');
        }
    }

    private function get_recent_activity_count($user_id, $minutes) {
        global $wpdb;
        $bp = buddypress();

        return $wpdb->get_var($wpdb->prepare(
            "SELECT COUNT(*) FROM {$bp->activity->table_name}
            WHERE user_id = %d
            AND date_recorded > DATE_SUB(NOW(), INTERVAL %d MINUTE)",
            $user_id, $minutes
        ));
    }

    private function mark_as_spam($content) {
        // Log spam attempt
        error_log('Spam detected: ' . substr($content, 0, 100));
        bp_core_add_message('Your activity appears to be spam', 'error');
    }

    private function notify_admin($user_id, $reason) {
        $admin_email = get_option('admin_email');
        $user = get_userdata($user_id);

        wp_mail(
            $admin_email,
            'Spam Activity Detected',
            sprintf('User %s (%s) triggered spam filter: %s',
                $user->display_name,
                $user->user_email,
                $reason
            )
        );
    }
}

new Reign_Activity_Spam_Detector();
```

### Manual Moderation

```php
// Add moderation queue
add_action('bp_activity_before_save', function($activity) {
    // New users require moderation
    $user = get_userdata($activity->user_id);
    $account_age = (time() - strtotime($user->user_registered)) / DAY_IN_SECONDS;

    if ($account_age < 7) { // Less than 7 days old
        $activity->hide_sitewide = 1; // Hide until approved
        update_activity_meta($activity->id, 'pending_moderation', true);
    }
});

// Moderation dashboard
add_action('admin_menu', function() {
    add_submenu_page(
        'buddypress',
        'Activity Moderation',
        'Moderate Activities',
        'manage_options',
        'bp-activity-moderation',
        'reign_activity_moderation_page'
    );
});
```

## Activity Templates

### Custom Activity Loop

```php
// Custom activity query
function reign_custom_activity_loop($args = array()) {
    $defaults = array(
        'type' => 'activity_update,new_member',
        'max' => 20,
        'page' => 1,
        'per_page' => 20,
        'sort' => 'DESC',
        'show_hidden' => false,
        'exclude' => false,
        'in' => false,
        'meta_query' => array()
    );

    $args = wp_parse_args($args, $defaults);

    if (bp_has_activities($args)): ?>
        <ul class="activity-list custom-style">
            <?php while (bp_activities()): bp_the_activity(); ?>
                <li class="activity-item">
                    <?php reign_activity_template(); ?>
                </li>
            <?php endwhile; ?>
        </ul>
    <?php else: ?>
        <p>No activities found</p>
    <?php endif;
}
```

### Activity Card Templates

```php
// Custom activity card
function reign_activity_template() {
    ?>
    <div class="activity-card">
        <div class="activity-header">
            <?php bp_activity_avatar(); ?>
            <div class="activity-meta">
                <?php bp_activity_action(); ?>
                <time><?php echo human_time_diff(strtotime(bp_get_activity_date_recorded())); ?> ago</time>
            </div>
        </div>

        <div class="activity-content">
            <?php if (bp_activity_has_content()): ?>
                <?php bp_activity_content_body(); ?>
            <?php endif; ?>

            <?php if (bp_get_activity_type() == 'activity_photo'): ?>
                <div class="activity-media">
                    <?php reign_activity_media(); ?>
                </div>
            <?php endif; ?>
        </div>

        <div class="activity-actions">
            <?php reign_activity_buttons(); ?>
        </div>

        <?php if (bp_activity_get_comment_count()): ?>
            <div class="activity-comments">
                <?php bp_activity_comments(); ?>
            </div>
        <?php endif; ?>
    </div>
    <?php
}
```

## Performance Optimization

### Activity Caching

```php
// Cache activity queries
function reign_get_cached_activities($args) {
    $cache_key = 'reign_activities_' . md5(serialize($args));
    $activities = get_transient($cache_key);

    if (false === $activities) {
        $activities = bp_activity_get($args);
        set_transient($cache_key, $activities, 5 * MINUTE_IN_SECONDS);
    }

    return $activities;
}

// Clear cache on new activity
add_action('bp_activity_posted_update', function() {
    global $wpdb;
    $wpdb->query("DELETE FROM {$wpdb->options} WHERE option_name LIKE '_transient_reign_activities_%'");
});
```

### Lazy Loading

```javascript
// Lazy load activities
jQuery(document).ready(function($) {
    var page = 2;
    var loading = false;

    $(window).scroll(function() {
        if (loading) return;

        if ($(window).scrollTop() + $(window).height() > $(document).height() - 100) {
            loading = true;

            $.ajax({
                url: ajaxurl,
                type: 'POST',
                data: {
                    action: 'load_more_activities',
                    page: page,
                    _ajax_nonce: reign_ajax.nonce
                },
                success: function(response) {
                    $('.activity-list').append(response.html);
                    page++;
                    loading = false;
                }
            });
        }
    });
});
```

### Database Optimization

```sql
-- Add indexes for better performance
ALTER TABLE wp_bp_activity
ADD INDEX idx_user_component (user_id, component),
ADD INDEX idx_type_date (type, date_recorded),
ADD INDEX idx_hide_sitewide (hide_sitewide);

-- Clean old activities
DELETE FROM wp_bp_activity
WHERE date_recorded < DATE_SUB(NOW(), INTERVAL 1 YEAR)
AND type IN ('new_avatar', 'updated_profile');
```

## Moderation Tools

### Admin Controls

```php
// Add bulk actions for activities
add_filter('bulk_actions-buddypress_page_bp-activity', function($actions) {
    $actions['mark_spam'] = 'Mark as Spam';
    $actions['unmark_spam'] = 'Not Spam';
    $actions['delete_permanently'] = 'Delete Permanently';
    return $actions;
});

// Handle bulk actions
add_filter('handle_bulk_actions-buddypress_page_bp-activity', function($redirect, $action, $activity_ids) {
    switch ($action) {
        case 'mark_spam':
            foreach ($activity_ids as $id) {
                bp_activity_mark_as_spam($id);
            }
            break;

        case 'delete_permanently':
            foreach ($activity_ids as $id) {
                bp_activity_delete(array('id' => $id));
            }
            break;
    }
    return $redirect;
}, 10, 3);
```

### User Reporting

```php
// Add report button to activities
add_action('bp_activity_entry_meta', function() {
    if (!is_user_logged_in()) return;
    ?>
    <a href="#" class="activity-report" data-activity-id="<?php echo bp_get_activity_id(); ?>">
        Report
    </a>
    <?php
});

// Handle activity reports
add_action('wp_ajax_report_activity', function() {
    $activity_id = intval($_POST['activity_id']);
    $reason = sanitize_text_field($_POST['reason']);

    // Save report
    $report_id = wp_insert_post(array(
        'post_type' => 'activity_report',
        'post_status' => 'pending',
        'post_title' => 'Activity Report #' . $activity_id,
        'meta_input' => array(
            'activity_id' => $activity_id,
            'reporter_id' => get_current_user_id(),
            'reason' => $reason
        )
    ));

    // Auto-hide after threshold
    $report_count = get_post_meta($activity_id, 'report_count', true);
    $report_count = $report_count ? $report_count + 1 : 1;
    update_post_meta($activity_id, 'report_count', $report_count);

    if ($report_count >= 5) {
        bp_activity_mark_as_spam($activity_id);
    }

    wp_send_json_success();
});
```

## Activity Filters

### Custom Filters

```php
// Add custom activity filters
add_filter('bp_activity_get_where_conditions', function($where, $args) {
    // Filter by meta value
    if (!empty($args['meta_key'])) {
        global $wpdb;
        $where['meta'] = $wpdb->prepare(
            "a.id IN (SELECT activity_id FROM {$wpdb->prefix}bp_activity_meta WHERE meta_key = %s AND meta_value = %s)",
            $args['meta_key'],
            $args['meta_value']
        );
    }

    // Date range filter
    if (!empty($args['date_from'])) {
        $where['date_from'] = "date_recorded >= '{$args['date_from']}'";
    }

    return $where;
}, 10, 2);
```

### Frontend Filters

```javascript
// Activity filter UI
jQuery(document).ready(function($) {
    // Filter by type
    $('#activity-filter-by').change(function() {
        var filter = $(this).val();

        $.ajax({
            url: ajaxurl,
            type: 'POST',
            data: {
                action: 'filter_activities',
                filter: filter,
                _ajax_nonce: reign_ajax.nonce
            },
            success: function(response) {
                $('.activity-list').html(response.html);
            }
        });
    });

    // Search activities
    $('#activity-search').on('keyup', function() {
        var search = $(this).val();

        if (search.length < 3) return;

        $.ajax({
            url: ajaxurl,
            type: 'POST',
            data: {
                action: 'search_activities',
                search: search,
                _ajax_nonce: reign_ajax.nonce
            },
            success: function(response) {
                $('.activity-list').html(response.html);
            }
        });
    });
});
```

## Analytics

### Activity Metrics

```php
// Track activity engagement
function reign_track_activity_view($activity_id) {
    $views = bp_activity_get_meta($activity_id, 'view_count', true);
    $views = $views ? $views + 1 : 1;
    bp_activity_update_meta($activity_id, 'view_count', $views);

    // Track unique viewers
    $viewers = bp_activity_get_meta($activity_id, 'unique_viewers', true);
    $viewers = $viewers ? $viewers : array();

    if (!in_array(get_current_user_id(), $viewers)) {
        $viewers[] = get_current_user_id();
        bp_activity_update_meta($activity_id, 'unique_viewers', $viewers);
    }
}

// Get activity stats
function reign_get_activity_stats($activity_id) {
    return array(
        'views' => bp_activity_get_meta($activity_id, 'view_count', true),
        'unique_viewers' => count(bp_activity_get_meta($activity_id, 'unique_viewers', true)),
        'comments' => bp_activity_get_comment_count($activity_id),
        'favorites' => bp_activity_get_meta($activity_id, 'favorite_count', true),
        'shares' => bp_activity_get_meta($activity_id, 'share_count', true)
    );
}
```

### Engagement Reports

```php
// Generate activity report
function reign_activity_engagement_report($start_date, $end_date) {
    global $wpdb;
    $bp = buddypress();

    $report = $wpdb->get_results($wpdb->prepare("
        SELECT
            DATE(date_recorded) as date,
            COUNT(*) as total_activities,
            COUNT(DISTINCT user_id) as unique_users,
            AVG(CHAR_LENGTH(content)) as avg_content_length,
            SUM(CASE WHEN type = 'activity_update' THEN 1 ELSE 0 END) as status_updates,
            SUM(CASE WHEN type = 'new_member' THEN 1 ELSE 0 END) as new_members
        FROM {$bp->activity->table_name}
        WHERE date_recorded BETWEEN %s AND %s
        GROUP BY DATE(date_recorded)
        ORDER BY date DESC
    ", $start_date, $end_date));

    return $report;
}
```

## Mobile Optimization

### Touch Controls

```javascript
// Swipe actions for activities
var touchStartX = 0;
var touchEndX = 0;

document.addEventListener('touchstart', function(e) {
    touchStartX = e.touches[0].clientX;
}, false);

document.addEventListener('touchend', function(e) {
    touchEndX = e.changedTouches[0].clientX;
    handleSwipe();
}, false);

function handleSwipe() {
    var swipeDistance = touchEndX - touchStartX;
    var activity = document.querySelector('.activity-item.active');

    if (Math.abs(swipeDistance) > 50) {
        if (swipeDistance > 0) {
            // Swipe right - like
            likeActivity(activity.dataset.activityId);
        } else {
            // Swipe left - hide
            hideActivity(activity.dataset.activityId);
        }
    }
}
```

### Mobile Layout

```css
/* Mobile activity stream */
@media (max-width: 768px) {
    .activity-list {
        padding: 0;
    }

    .activity-item {
        border-radius: 0;
        margin-bottom: 10px;
        box-shadow: 0 1px 3px rgba(0,0,0,0.1);
    }

    .activity-content {
        font-size: 16px;
        line-height: 1.5;
    }

    .activity-actions {
        display: flex;
        justify-content: space-around;
        padding: 10px 0;
        border-top: 1px solid #eee;
    }

    .activity-action-button {
        flex: 1;
        text-align: center;
        padding: 10px;
    }
}
```

## Troubleshooting

### Common Issues

#### Activities Not Showing

**Solutions:**
1. Check activity component is active
2. Verify database tables exist
3. Check user permissions
4. Clear activity cache

#### Duplicate Activities

**Solutions:**
```php
// Prevent duplicates
add_filter('bp_activity_before_save', function($activity) {
    $exists = bp_activity_get(array(
        'user_id' => $activity->user_id,
        'content' => $activity->content,
        'type' => $activity->type,
        'max' => 1
    ));

    if (!empty($exists['activities'])) {
        return false;
    }
    return $activity;
});
```

#### Performance Issues

**Solutions:**
1. Enable activity caching
2. Limit activities per page
3. Optimize database indexes
4. Use CDN for media

---

*For more BuddyPress features, see the Community Setup documentation.*