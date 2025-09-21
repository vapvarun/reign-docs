# bbPress Forums Complete Integration Guide

## Overview

bbPress is WordPress's native forum plugin, bringing bulletin board functionality to your site. Reign theme provides extensive bbPress integration with custom templates, enhanced layouts, and seamless BuddyPress connectivity.

## Installation & Setup

### Installing bbPress

1. **Install bbPress:**
   ```
   Plugins → Add New → Search "bbPress"
   Install and Activate
   ```

2. **Initial Configuration:**
   - Settings → Forums
   - Configure forum settings
   - Set user roles
   - Enable features

3. **Reign Integration:**
   - Auto-detected on activation
   - Custom templates at `/reign-theme/bbpress/`
   - Styled forum layouts
   - BuddyPress integration enabled

## Forum Structure

### Forum Hierarchy

```
Forums (Parent)
├── Sub-Forums
│   ├── Topics
│   │   ├── Replies
│   │   └── Reply to Reply
│   └── Sticky Topics
└── Categories
    └── Tagged Topics
```

### Creating Forums

**Forum Settings:**
```php
// Create forum programmatically
$forum_data = array(
    'post_title' => 'General Discussion',
    'post_content' => 'Forum for general topics',
    'post_status' => 'publish',
    'post_type' => 'forum',
    'post_parent' => 0, // Parent forum ID
    'menu_order' => 1,
    'meta_input' => array(
        '_bbp_forum_type' => 'forum', // or 'category'
        '_bbp_status' => 'open', // or 'closed'
        '_bbp_visibility' => 'publish', // or 'private', 'hidden'
    )
);

$forum_id = wp_insert_post($forum_data);
```

## Forum Templates

### Template Hierarchy

**Reign bbPress Templates:**
```
reign-theme/bbpress/
├── content-archive-forum.php
├── content-archive-topic.php
├── content-single-forum.php
├── content-single-topic.php
├── content-single-reply.php
├── form-reply.php
├── form-topic.php
├── loop-forums.php
├── loop-replies.php
├── loop-topics.php
└── user-profile.php
```

### Forum Archive Page

**Custom Forum Layout:**
```php
// Override forum archive
reign-child/bbpress/content-archive-forum.php

<div class="reign-forums-wrapper">
    <div class="forums-header">
        <h1><?php bbp_forum_archive_title(); ?></h1>
        <?php bbp_breadcrumb(); ?>
    </div>

    <div class="forums-grid">
        <?php while (bbp_forums()) : bbp_the_forum(); ?>
            <div class="forum-card">
                <div class="forum-icon">
                    <?php reign_forum_icon(); ?>
                </div>
                <div class="forum-content">
                    <h3><?php bbp_forum_title(); ?></h3>
                    <p><?php bbp_forum_content(); ?></p>
                    <div class="forum-meta">
                        <span><?php bbp_forum_topic_count(); ?> Topics</span>
                        <span><?php bbp_forum_post_count(); ?> Posts</span>
                    </div>
                </div>
                <div class="forum-freshness">
                    <?php bbp_forum_freshness_link(); ?>
                </div>
            </div>
        <?php endwhile; ?>
    </div>
</div>
```

### Single Forum View

**Forum Display Options:**
```
Layout Styles:
1. Classic Table - Traditional forum layout
2. Modern Cards - Card-based topics
3. List View - Detailed topic list
4. Grid View - Visual topic grid
```

## Topic Management

### Creating Topics

**Topic Form Customization:**
```php
// Add custom fields to topic form
function reign_bbp_topic_form_fields() {
    ?>
    <div class="bbp-form-group">
        <label for="topic_priority">Priority</label>
        <select name="topic_priority" id="topic_priority">
            <option value="normal">Normal</option>
            <option value="urgent">Urgent</option>
            <option value="low">Low</option>
        </select>
    </div>
    <?php
}
add_action('bbp_theme_before_topic_form_submit_wrapper', 'reign_bbp_topic_form_fields');
```

### Topic Display

**Single Topic Layout:**
```php
// Custom topic template
<div class="reign-topic-wrapper">
    <div class="topic-header">
        <h1><?php bbp_topic_title(); ?></h1>
        <div class="topic-meta">
            <?php bbp_topic_author_link(); ?>
            <span class="topic-date"><?php bbp_topic_post_date(); ?></span>
            <span class="topic-views"><?php bbp_topic_voice_count(); ?> Participants</span>
        </div>
    </div>

    <div class="topic-content">
        <?php bbp_topic_content(); ?>
    </div>

    <div class="topic-tags">
        <?php bbp_topic_tag_list(); ?>
    </div>

    <div class="topic-replies">
        <?php bbp_get_template_part('loop', 'replies'); ?>
    </div>

    <?php if (bbp_current_user_can_access_create_reply_form()) : ?>
        <?php bbp_get_template_part('form', 'reply'); ?>
    <?php endif; ?>
</div>
```

## User Roles & Capabilities

### Forum Roles

**Available Roles:**
```php
// bbPress roles
$roles = array(
    'bbp_keymaster' => 'Keymaster (Admin)',
    'bbp_moderator' => 'Moderator',
    'bbp_participant' => 'Participant',
    'bbp_spectator' => 'Spectator',
    'bbp_blocked' => 'Blocked',
);

// Assign role
bbp_set_user_role($user_id, 'bbp_moderator');
```

### Custom Capabilities

```php
// Add custom capability
function reign_bbp_custom_caps($caps, $cap, $user_id) {
    // Allow specific users to moderate
    if ($cap === 'moderate' && is_trusted_user($user_id)) {
        $caps = array('moderate');
    }
    return $caps;
}
add_filter('bbp_map_meta_caps', 'reign_bbp_custom_caps', 10, 3);
```

## BuddyPress Integration

### Group Forums

**Enable Group Forums:**
```php
// Settings → Forums → BuddyPress Integration
// Check "Allow BuddyPress Groups to have their own forums"

// Create group forum programmatically
function reign_create_group_forum($group_id) {
    $group = groups_get_group($group_id);

    $forum_id = bbp_insert_forum(array(
        'post_title' => $group->name . ' Forum',
        'post_content' => $group->description,
        'post_status' => 'publish',
    ));

    groups_update_groupmeta($group_id, 'forum_id', $forum_id);
}
add_action('groups_group_create_complete', 'reign_create_group_forum');
```

### Profile Forums Tab

```php
// Add Forums tab to BuddyPress profile
function reign_bp_forums_tab() {
    bp_core_new_nav_item(array(
        'name' => 'Forums',
        'slug' => 'forums',
        'screen_function' => 'reign_bp_forums_screen',
        'position' => 50,
        'default_subnav_slug' => 'topics'
    ));
}
add_action('bp_setup_nav', 'reign_bp_forums_tab');
```

## Forum Widgets

### Available Widgets

**bbPress Widgets:**
```
1. Forums List - Display forums
2. Topics List - Recent/Popular topics
3. Replies List - Recent replies
4. Single Forum - Specific forum
5. Login Widget - Forum login
6. Forum Statistics - Stats widget
7. Topic Views - Popular topics
```

### Widget Configuration

```php
// Register custom forum widget area
register_sidebar(array(
    'name' => 'Forum Sidebar',
    'id' => 'forum-sidebar',
    'description' => 'Widgets for forum pages',
    'before_widget' => '<div class="forum-widget %2$s">',
    'after_widget' => '</div>',
));

// Display in forum template
if (is_bbpress()) {
    dynamic_sidebar('forum-sidebar');
}
```

## Shortcodes

### Forum Shortcodes

**Display Forums:**
```
[bbp-forum-index] - All forums
[bbp-single-forum id="123"] - Single forum
[bbp-forum-form] - Create forum form
```

**Display Topics:**
```
[bbp-topic-index] - All topics
[bbp-single-topic id="456"] - Single topic
[bbp-topic-form] - Create topic form
[bbp-topic-form forum_id="123"] - Topic form for specific forum
```

**User Shortcodes:**
```
[bbp-login] - Login form
[bbp-register] - Registration form
[bbp-lost-pass] - Password recovery
[bbp-user-profile] - User profile
```

**Statistics:**
```
[bbp-stats] - Forum statistics
[bbp-single-view] - Specific view
```

## Styling & Customization

### Custom CSS

```css
/* Reign + bbPress Styling */

/* Forum layout */
.bbpress-forums {
    background: var(--reign-background);
    padding: 20px;
    border-radius: 10px;
}

/* Forum cards */
.forum-card {
    background: white;
    border: 1px solid #e1e4e8;
    border-radius: 8px;
    padding: 20px;
    margin-bottom: 15px;
    transition: all 0.3s;
}

.forum-card:hover {
    box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    transform: translateY(-2px);
}

/* Topic list */
.bbp-topics {
    list-style: none;
    padding: 0;
}

.bbp-topic-title {
    font-size: 18px;
    font-weight: 600;
    color: var(--reign-primary);
}

/* User badges */
.bbp-author-role {
    display: inline-block;
    padding: 2px 8px;
    border-radius: 3px;
    font-size: 11px;
    text-transform: uppercase;
}

.bbp-author-role-moderator {
    background: #28a745;
    color: white;
}

.bbp-author-role-keymaster {
    background: #dc3545;
    color: white;
}

/* Mobile responsive */
@media (max-width: 768px) {
    .bbpress-forums {
        padding: 10px;
    }

    .forum-card {
        padding: 15px;
    }
}
```

### PHP Hooks

```php
// Before forum content
add_action('bbp_template_before_forums_loop', function() {
    echo '<div class="forums-intro">Welcome to our community forums!</div>';
});

// After topic title
add_action('bbp_theme_after_topic_title', function() {
    if (is_hot_topic()) {
        echo '<span class="hot-topic-badge">🔥 Hot</span>';
    }
});

// Custom reply actions
add_filter('bbp_reply_admin_links', function($links, $reply_id) {
    $links['report'] = '<a href="#" class="bbp-report-link">Report</a>';
    return $links;
}, 10, 2);
```

## Moderation Tools

### Moderation Actions

```php
// Auto-moderation
function reign_bbp_auto_moderate($post_id, $post) {
    $content = $post->post_content;
    $blacklist = array('spam', 'viagra', 'casino');

    foreach ($blacklist as $word) {
        if (stripos($content, $word) !== false) {
            wp_update_post(array(
                'ID' => $post_id,
                'post_status' => 'pending'
            ));
            break;
        }
    }
}
add_action('bbp_new_reply', 'reign_bbp_auto_moderate', 10, 2);
add_action('bbp_new_topic', 'reign_bbp_auto_moderate', 10, 2);
```

### User Reputation

```php
// Add reputation system
function reign_bbp_reputation($user_id) {
    $reputation = 0;

    // Points for topics
    $topics = bbp_get_user_topic_count($user_id);
    $reputation += $topics * 5;

    // Points for replies
    $replies = bbp_get_user_reply_count($user_id);
    $reputation += $replies * 2;

    // Points for favorites
    $favorites = count(bbp_get_user_favorites($user_id));
    $reputation += $favorites * 1;

    return $reputation;
}

// Display reputation
add_action('bbp_theme_after_reply_author_details', function() {
    $user_id = bbp_get_reply_author_id();
    $reputation = reign_bbp_reputation($user_id);
    echo '<div class="bbp-reputation">Reputation: ' . $reputation . '</div>';
});
```

## Performance Optimization

### Caching

```php
// Cache forum queries
function reign_cache_forum_data($forum_id) {
    $cache_key = 'bbp_forum_' . $forum_id;
    $data = wp_cache_get($cache_key);

    if (false === $data) {
        $data = array(
            'topic_count' => bbp_get_forum_topic_count($forum_id),
            'post_count' => bbp_get_forum_post_count($forum_id),
            'last_post' => bbp_get_forum_last_post_id($forum_id),
        );
        wp_cache_set($cache_key, $data, '', 3600);
    }

    return $data;
}
```

### Database Optimization

```sql
-- Optimize bbPress tables
OPTIMIZE TABLE wp_posts WHERE post_type IN ('forum', 'topic', 'reply');

-- Add indexes
ALTER TABLE wp_posts ADD INDEX idx_bbp_type (post_type, post_status);
ALTER TABLE wp_postmeta ADD INDEX idx_bbp_meta (meta_key, meta_value(10));
```

## SEO Configuration

### Forum SEO

```php
// Add meta tags for forums
function reign_bbp_seo_meta() {
    if (bbp_is_single_forum()) {
        $forum_id = bbp_get_forum_id();
        ?>
        <meta property="og:title" content="<?php bbp_forum_title($forum_id); ?>">
        <meta property="og:description" content="<?php echo wp_trim_words(bbp_get_forum_content($forum_id), 30); ?>">
        <meta property="og:type" content="website">
        <?php
    }
}
add_action('wp_head', 'reign_bbp_seo_meta');
```

### Structured Data

```php
// Add Forum schema
function reign_bbp_schema() {
    if (bbp_is_single_topic()) {
        ?>
        <script type="application/ld+json">
        {
            "@context": "https://schema.org",
            "@type": "DiscussionForumPosting",
            "headline": "<?php bbp_topic_title(); ?>",
            "text": "<?php echo wp_strip_all_tags(bbp_get_topic_content()); ?>",
            "datePublished": "<?php echo get_the_date('c', bbp_get_topic_id()); ?>",
            "author": {
                "@type": "Person",
                "name": "<?php bbp_topic_author(); ?>"
            }
        }
        </script>
        <?php
    }
}
add_action('wp_head', 'reign_bbp_schema');
```

## Troubleshooting

### Common Issues

#### Forums Not Displaying
```
Solutions:
- Flush permalinks
- Check forum visibility settings
- Verify user permissions
- Clear cache
```

#### Users Can't Post
```
Check:
- User role and capabilities
- Forum status (open/closed)
- Spam/moderation settings
- Login requirements
```

#### Styling Issues
```
Fix:
- Check template overrides
- Clear CSS cache
- Verify child theme templates
- Check plugin conflicts
```

## Best Practices

1. **Structure** - Logical forum hierarchy
2. **Moderation** - Active moderator team
3. **Rules** - Clear forum guidelines
4. **SEO** - Optimize for search engines
5. **Performance** - Cache forum queries
6. **Spam** - Implement anti-spam measures
7. **Backup** - Regular database backups
8. **Updates** - Keep bbPress updated