# Reign Theme Widgets Guide

## Overview

Reign Theme includes 15+ custom widgets designed specifically for community sites, social networks, and online marketplaces. These widgets integrate seamlessly with BuddyPress, WooCommerce, and other plugins.

## Widget List

### Community Widgets

1. **Reign Login Widget**
2. **Reign Member Widget**
3. **Reign Group Widget**
4. **Reign Activity Widget**
5. **Reign Who's Online Widget**
6. **Reign Friend Suggestions**
7. **Reign Group Suggestions**

### Business Widgets

8. **Reign Product Categories**
9. **Reign Featured Products**
10. **Reign Recent Products**
11. **Reign Product Search**

### Content Widgets

12. **Reign Recent Posts**
13. **Reign Popular Posts**
14. **Reign Author Bio**
15. **Reign Social Links**
16. **Reign Contact Info**

## Widget Configuration

### Accessing Widgets

**Methods:**
1. `Appearance → Widgets`
2. `Customizer → Widgets`
3. Block Editor widgets

### Widget Areas

**Available Widget Areas:**
- Left Sidebar
- Right Sidebar
- Footer Widget Area 1-4
- Top Bar Left/Right
- Activity Sidebar
- Member Sidebar
- Group Sidebar
- Shop Sidebar
- Forum Sidebar

## Community Widgets

### Reign Login Widget

**Purpose:** Display login form or user dashboard

**Settings:**
```
Title: Welcome
Show for Logged In: Yes/No
Show Avatar: Yes/No
Avatar Size: 50px
Show User Menu: Yes/No
Show Logout Button: Yes/No
Custom Login URL: (optional)
Custom Register URL: (optional)
```

**Features:**
- Displays login form for guests
- Shows user dashboard for members
- Quick stats display
- Notification badges
- Custom menu items

**PHP Usage:**
```php
// Programmatically display
the_widget('Reign_Login_Widget', array(
    'title' => 'Member Area',
    'show_avatar' => true,
    'avatar_size' => 60
));
```

### Reign Member Widget

**Purpose:** Display members list with filters

**Settings:**
```
Title: Community Members
Max Members: 5
Member Type: All/Specific
Display Type: Active/Newest/Popular/Random
Show Avatar: Yes/No
Show Member Name: Yes/No
Show Last Active: Yes/No
Show Member Type: Yes/No
Show Friend Button: Yes/No
Link to Profile: Yes/No
```

**Filter Options:**
```php
// Customize member query
add_filter('reign_member_widget_args', function($args) {
    $args['per_page'] = 10;
    $args['type'] = 'active';
    return $args;
});
```

### Reign Group Widget

**Purpose:** Display groups with various filters

**Settings:**
```
Title: Popular Groups
Max Groups: 5
Group Type: All/Public/Private/Hidden
Display Type: Active/Newest/Popular/Random/Alphabetical
Show Avatar: Yes/No
Show Group Name: Yes/No
Show Member Count: Yes/No
Show Group Type: Yes/No
Show Join Button: Yes/No
Link to Groups: Yes/No
```

**Custom Display:**
```php
// Modify group widget output
add_filter('reign_group_widget_item', function($html, $group) {
    $html .= '<div class="custom-meta">';
    $html .= 'Created: ' . $group->date_created;
    $html .= '</div>';
    return $html;
}, 10, 2);
```

### Reign Activity Widget

**Purpose:** Display site activity feed

**Settings:**
```
Title: Latest Activity
Max Activities: 10
Scope: All/Friends/Groups/Mentions
Action Filter: (multiple selections)
Show Avatar: Yes/No
Show Timestamp: Yes/No
Show Actions: Yes/No
Hide Spam: Yes/No
```

**Activity Types:**
- Status Updates
- New Members
- New Groups
- Friendships
- Profile Updates
- Forum Posts
- Blog Posts

### Reign Who's Online Widget

**Purpose:** Display currently online members

**Settings:**
```
Title: Who's Online
Max Members: 10
Online Time: 5/10/15/30 minutes
Show Avatar: Yes/No
Avatar Size: Small/Medium/Large
Show Username: Yes/No
Show Display Name: Yes/No
Link to Profile: Yes/No
```

**Online Detection:**
```php
// Customize online duration
add_filter('reign_online_duration', function() {
    return 15 * MINUTE_IN_SECONDS;
});
```

### Reign Friend Suggestions

**Purpose:** Suggest friends based on mutual connections

**Settings:**
```
Title: People You May Know
Max Suggestions: 5
Suggestion Logic: Mutual Friends/Interests/Groups
Show Avatar: Yes/No
Show Mutual Count: Yes/No
Show Add Friend Button: Yes/No
Exclude Connected: Yes
```

**Algorithm Customization:**
```php
// Modify suggestion algorithm
add_filter('reign_friend_suggestions_query', function($user_ids) {
    // Custom logic for suggestions
    return $user_ids;
});
```

### Reign Group Suggestions

**Purpose:** Suggest groups based on interests

**Settings:**
```
Title: Groups You Might Like
Max Suggestions: 5
Base On: Friends' Groups/Popular/Categories
Show Cover Image: Yes/No
Show Description: Yes/No
Show Member Count: Yes/No
Show Join Button: Yes/No
```

## Business Widgets

### Reign Product Categories

**Purpose:** Display WooCommerce categories

**Settings:**
```
Title: Shop Categories
Display Type: List/Dropdown/Grid
Show Count: Yes/No
Show Hierarchy: Yes/No
Hide Empty: Yes/No
Order By: Name/Count/ID
Order: ASC/DESC
Exclude: (category IDs)
```

**Grid Layout:**
```css
.reign-product-cats-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 15px;
}
```

### Reign Featured Products

**Purpose:** Showcase featured products

**Settings:**
```
Title: Featured Products
Products: 4
Columns: 1/2/3/4
Order By: Date/Price/Rating/Sales
Show Image: Yes/No
Show Title: Yes/No
Show Price: Yes/No
Show Rating: Yes/No
Show Add to Cart: Yes/No
```

### Reign Recent Products

**Purpose:** Display latest products

**Settings:**
```
Title: New Arrivals
Products: 6
Columns: 2
Category: All/Specific
Show Sale Badge: Yes/No
Show Quick View: Yes/No
```

### Reign Product Search

**Purpose:** Advanced product search

**Settings:**
```
Title: Search Products
Placeholder: Search products...
Show Categories Dropdown: Yes/No
Show Price Range: Yes/No
Show Submit Button: Yes/No
Search In: Title/Description/SKU
```

## Content Widgets

### Reign Recent Posts

**Purpose:** Display recent blog posts

**Settings:**
```
Title: Latest News
Number of Posts: 5
Category: All/Specific
Post Type: post/custom
Show Featured Image: Yes/No
Image Position: Left/Top
Show Excerpt: Yes/No
Excerpt Length: 55
Show Date: Yes/No
Show Author: Yes/No
Show Comments: Yes/No
```

**Custom Query:**
```php
// Modify posts query
add_filter('reign_recent_posts_args', function($args) {
    $args['meta_key'] = 'featured';
    $args['meta_value'] = 'yes';
    return $args;
});
```

### Reign Popular Posts

**Purpose:** Display popular posts by views/comments

**Settings:**
```
Title: Trending Now
Number of Posts: 5
Popular By: Views/Comments
Time Range: All Time/Month/Week/Day
Show View Count: Yes/No
Show Thumbnail: Yes/No
Thumbnail Size: thumbnail/medium/large
```

### Reign Author Bio

**Purpose:** Display author information

**Settings:**
```
Title: About Author
Show on: Single Posts/Pages/Both
Show Avatar: Yes/No
Avatar Size: 96
Show Name: Yes/No
Show Bio: Yes/No
Show Website: Yes/No
Show Social Links: Yes/No
Show Post Count: Yes/No
```

### Reign Social Links

**Purpose:** Display social media links

**Settings:**
```
Title: Follow Us
Facebook URL:
Twitter URL:
Instagram URL:
LinkedIn URL:
YouTube URL:
TikTok URL:
Discord URL:
Icon Style: Default/Rounded/Square
Icon Size: Small/Medium/Large
Open in New Tab: Yes/No
Show Labels: Yes/No
```

**Icon Styles:**
```css
/* Rounded icons */
.reign-social-rounded a {
    border-radius: 50%;
    padding: 10px;
    background: var(--reign-primary-color);
}

/* Square icons */
.reign-social-square a {
    border-radius: 5px;
    padding: 8px;
}
```

### Reign Contact Info

**Purpose:** Display contact information

**Settings:**
```
Title: Contact Us
Company Name:
Address:
Phone:
Email:
Hours:
Map Embed: (Google Maps iframe)
Show Icons: Yes/No
```

## Advanced Widget Features

### Widget Visibility

**Conditional Display:**
```php
// Show widget only for members
add_filter('widget_display_callback', function($instance, $widget, $args) {
    if ($widget->id_base === 'reign_members' && !is_user_logged_in()) {
        return false;
    }
    return $instance;
}, 10, 3);
```

### Widget Caching

**Enable Caching:**
```php
// Cache widget output
add_filter('reign_widget_cache_time', function() {
    return HOUR_IN_SECONDS;
});
```

### Custom Widget Areas

**Register New Area:**
```php
// Add custom widget area
function reign_custom_widget_area() {
    register_sidebar(array(
        'name' => 'Custom Area',
        'id' => 'custom-area',
        'before_widget' => '<div class="widget %2$s">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>',
    ));
}
add_action('widgets_init', 'reign_custom_widget_area');
```

### Widget Styling

**Global Widget Styles:**
```css
/* Widget container */
.widget {
    margin-bottom: 30px;
    padding: 20px;
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

/* Widget title */
.widget-title {
    font-size: 18px;
    font-weight: 600;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 2px solid var(--reign-primary-color);
}

/* Widget content */
.widget-content {
    font-size: 14px;
    line-height: 1.6;
}
```

### Widget Templates

**Override Widget Template:**
```php
// Create in child theme
reign-child/
├── widgets/
│   ├── login-widget.php
│   ├── member-widget.php
│   └── group-widget.php
```

**Template Example:**
```php
<?php
/**
 * Custom Login Widget Template
 */
?>
<div class="reign-login-widget-custom">
    <?php if (is_user_logged_in()): ?>
        <div class="user-dashboard">
            <!-- Custom logged in view -->
        </div>
    <?php else: ?>
        <div class="login-form">
            <!-- Custom login form -->
        </div>
    <?php endif; ?>
</div>
```

## Mobile Optimization

### Responsive Widget Design

```css
/* Mobile widget adjustments */
@media (max-width: 768px) {
    .widget {
        padding: 15px;
        margin-bottom: 20px;
    }

    .widget-grid {
        grid-template-columns: 1fr;
    }

    .reign-member-widget .member-item {
        display: flex;
        align-items: center;
    }
}
```

### Touch-Friendly Elements

```css
/* Larger touch targets */
.widget button,
.widget a.button {
    min-height: 44px;
    padding: 10px 15px;
}
```

## Performance Tips

### Lazy Loading

```php
// Lazy load widget content
add_filter('reign_widget_lazy_load', '__return_true');
```

### Optimize Queries

```php
// Reduce database queries
add_filter('reign_widget_query_args', function($args) {
    $args['no_found_rows'] = true;
    $args['update_post_meta_cache'] = false;
    return $args;
});
```

### Widget Output Cache

```php
// Cache widget HTML
function reign_cache_widget_output($widget_id) {
    $cache_key = 'reign_widget_' . $widget_id;
    $output = get_transient($cache_key);

    if (false === $output) {
        // Generate widget output
        $output = reign_generate_widget($widget_id);
        set_transient($cache_key, $output, HOUR_IN_SECONDS);
    }

    return $output;
}
```

## Troubleshooting

### Widgets Not Showing

**Solutions:**
1. Check widget visibility settings
2. Verify widget area is called in template
3. Clear cache
4. Check for JavaScript errors

### Widget Styling Issues

**Solutions:**
1. Check theme compatibility
2. Increase CSS specificity
3. Clear browser cache
4. Inspect CSS conflicts

### Performance Problems

**Solutions:**
1. Enable widget caching
2. Reduce number of items displayed
3. Optimize database queries
4. Use lazy loading

## Widget Hooks

### Available Actions

```php
// Before widget output
do_action('reign_before_widget', $widget_id);

// After widget output
do_action('reign_after_widget', $widget_id);

// Widget settings saved
do_action('reign_widget_updated', $widget_id, $settings);
```

### Available Filters

```php
// Widget output
apply_filters('reign_widget_output', $output, $widget_id);

// Widget settings
apply_filters('reign_widget_settings', $settings, $widget_id);

// Widget query
apply_filters('reign_widget_query', $query, $widget_id);
```

---

*For sidebar configuration, see the Sidebar Configuration guide.*