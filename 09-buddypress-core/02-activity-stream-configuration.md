# Activity Stream Configuration

## Overview

The BuddyPress Activity Stream is the social heart of your community, displaying real-time updates, posts, and interactions. Reign theme provides extensive customization options for the activity stream.

## Accessing Activity Settings

### BuddyPress Settings
**Location:** Settings → BuddyPress → Settings → Activity

### Theme Customization
**Location:** Appearance → Customize → BuddyPress → Activity

### Reign Community Settings
**Location:** Dashboard → Reign Settings → Community Settings

## Activity Stream Layout

### Layout Options

#### Layout 1: Classic Stream
```
[User Avatar] [Activity Content]
              [Activity Meta]
              [Activity Actions]
```

#### Layout 2: Card Style
```
┌─────────────────────────┐
│ [Avatar] [User Name]    │
│ [Activity Content]      │
│ [Media/Links]          │
│ [Like] [Comment] [Share]│
└─────────────────────────┘
```

#### Layout 3: Timeline
```
     |
[Date]|[Avatar][Content]
     |
[Date]|[Avatar][Content]
     |
```

#### Layout 4: Masonry Grid
```
┌────┐ ┌────┐ ┌────┐
│    │ │    │ │    │
└────┘ │    │ └────┘
┌────┐ └────┘ ┌────┐
│    │ ┌────┐ │    │
```

## Activity Types Configuration

### Enable/Disable Activity Types

```php
// Control which activities appear
function reign_filter_activity_types($types) {
    // Remove specific types
    unset($types['joined_group']);
    unset($types['friendship_created']);

    return $types;
}
add_filter('bp_activity_get_types', 'reign_filter_activity_types');
```

### Default Activity Types
- **Updates** - Status updates
- **Posts** - Blog post activities
- **Comments** - Comment activities
- **Friendships** - Friend connections
- **Groups** - Group activities
- **Members** - Member joins
- **Profile** - Profile updates

## Activity Posting

### Post Form Configuration

**Elements to Include:**
```
✓ Text Editor (with formatting)
✓ Media Upload (images/videos)
✓ GIF Picker
✓ Emoji Support
✓ Link Preview
✓ Privacy Settings
✓ @Mentions
✓ #Hashtags
```

### Character Limit
```
Default: Unlimited
Custom Limit: 280/500/1000 characters
Warning at: 90% of limit
```

### Media Settings
```
Image Upload:
- Max Size: 5MB
- Formats: JPG, PNG, GIF, WebP
- Max Images: 10

Video Upload:
- Max Size: 50MB
- Formats: MP4, WebM
- Duration: 5 minutes max
```

## Activity Display Settings

### Stream Configuration

**Items Per Page:**
```
Default: 20
Options: 5, 10, 15, 20, 25, 30, 50
Load More: Ajax / Pagination / Infinite Scroll
```

**Default Filter:**
```
○ Everything
○ Updates Only
○ Friends Only
○ Groups
○ Mentions
○ Favorites
```

### Activity Meta Display

**Show/Hide Elements:**
```
✓ User Avatar
✓ User Name
✓ Activity Time
✓ Activity Type
✓ Privacy Icon
□ User Role/Badge
□ Location
□ Mood/Status
```

### Activity Actions

**Available Actions:**
```
✓ Favorite/Like
✓ Comment
✓ Share/Repost
✓ Delete (own posts)
□ Report
□ Bookmark
□ Translate
```

## Comments Configuration

### Comment Threading
```
Enable Threading: Yes
Max Depth: 3 levels
Comments Per Activity: Show 5, Load More
Sort Order: Newest First / Oldest First
```

### Comment Features
```
✓ Rich Text Editor
✓ @Mentions in Comments
✓ Media in Comments
✓ Edit Own Comments
✓ Like Comments
```

## Notifications Integration

### Activity Notifications

**Trigger Notifications For:**
```
✓ @Mentions
✓ Comments on your activity
✓ Likes on your activity
✓ Shares of your activity
✓ Comments after you
```

### Notification Delivery
```
On-Site: ✓ Enabled
Email: ✓ Daily Digest / Instant
Push: ○ Browser Notifications
```

## Privacy Settings

### Activity Privacy Levels

**Options:**
1. **Public** - Everyone can see
2. **Logged-in Users** - Members only
3. **Friends** - Friends only
4. **Only Me** - Private
5. **Custom** - Specific members/groups

### Default Privacy
```
New Activities: Public / Friends / Only Me
Can Change: Yes / No
Remember Last: Yes / No
```

## Activity Filtering

### Filter Bar Options

**Available Filters:**
```
- Everything
- Updates
- Posts
- Comments
- New Members
- Friendships
- Groups
- Favorites
```

### Search Functionality
```
Search Type: Live / On Submit
Search In: Content / Username / Both
Min Characters: 3
```

### Date Filtering
```
□ Today
□ Yesterday
□ This Week
□ This Month
□ This Year
□ Date Range
```

## Activity Moderation

### Auto-Moderation

**Spam Prevention:**
```
✓ Akismet Integration
✓ Link Limit: Max 3 links
✓ Keyword Blacklist
✓ New User Restrictions
```

**Content Moderation:**
```
Hold for Review if:
- Contains blacklisted words
- Too many links (>3)
- New user (<24 hours)
- Reported by users (>3 reports)
```

### Manual Moderation

**Moderator Actions:**
- Edit any activity
- Delete any activity
- Mark as spam
- Ban user
- Clear activity history

## Performance Optimization

### Caching Strategy

```php
// Cache activity queries
set_transient('bp_activity_' . $user_id, $activities, HOUR_IN_SECONDS);
```

### Lazy Loading
```
Enable: ✓
Offset: 100px
Placeholder: Activity skeleton
```

### Database Optimization
```sql
-- Add indexes for better performance
ALTER TABLE wp_bp_activity
ADD INDEX idx_user_type (user_id, type);

ALTER TABLE wp_bp_activity
ADD INDEX idx_date_type (date_recorded, type);
```

## Custom Activity Types

### Register Custom Type

```php
function reign_register_custom_activity() {
    bp_activity_set_action(
        'custom_component',
        'custom_action',
        __('Custom Activity', 'reign'),
        'reign_format_custom_activity',
        __('Custom Activities', 'reign'),
        array('activity', 'member')
    );
}
add_action('bp_register_activity_actions', 'reign_register_custom_activity');
```

### Custom Activity Template

```php
function reign_custom_activity_template() {
    ?>
    <div class="custom-activity">
        <h3><?php bp_activity_action(); ?></h3>
        <div class="activity-content">
            <?php bp_activity_content_body(); ?>
        </div>
    </div>
    <?php
}
```

## Activity Widgets

### Available Widgets

1. **Site Wide Activity** - Main activity stream
2. **Latest Activity** - Recent updates
3. **Popular Activity** - Most liked/commented
4. **Friend Activity** - Friends' updates
5. **Group Activity** - Group updates

### Widget Configuration
```
Title: Latest Community Activity
Number of Items: 5
Show: Updates/Posts/Comments/All
Avatar Size: 50px
Excerpt Length: 100 characters
```

## Shortcodes

### Activity Stream Shortcode

```
[reign_activity_stream
    type="sitewide"
    max="20"
    filter="updates"
    show_filters="yes"
    show_post_form="yes"]
```

### Parameters:
- `type`: sitewide/friends/groups/favorites
- `max`: Number of activities
- `filter`: Default filter
- `show_filters`: Display filter bar
- `show_post_form`: Display post form

## REST API

### Activity Endpoints

```
GET /wp-json/buddypress/v1/activity
POST /wp-json/buddypress/v1/activity
GET /wp-json/buddypress/v1/activity/{id}
PUT /wp-json/buddypress/v1/activity/{id}
DELETE /wp-json/buddypress/v1/activity/{id}
```

### Example Request
```javascript
fetch('/wp-json/buddypress/v1/activity', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'X-WP-Nonce': wpApiSettings.nonce
    },
    body: JSON.stringify({
        content: 'Hello World!',
        type: 'activity_update'
    })
});
```

## Troubleshooting

### Activity Not Showing

**Check:**
1. Activity component enabled
2. User has permission to view
3. Privacy settings
4. Cache cleared
5. Database tables exist

### Posting Failures

**Solutions:**
- Check user capabilities
- Verify nonce/security
- Check character limits
- Review spam settings
- Check server timeout

### Performance Issues

**Optimize:**
- Limit activities per page
- Enable caching
- Optimize queries
- Use CDN for media
- Clean old activities

## Best Practices

1. **Content Moderation** - Set up keyword filtering
2. **Performance** - Limit activities displayed
3. **Privacy** - Configure appropriate defaults
4. **Spam Prevention** - Enable Akismet
5. **User Experience** - Enable rich media
6. **Mobile** - Test responsive layout
7. **Accessibility** - Proper ARIA labels
8. **SEO** - Configure meta tags