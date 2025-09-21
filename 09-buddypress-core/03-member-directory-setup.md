# Member Directory Setup Guide

## Overview

The Member Directory is a central hub where users can discover and connect with other community members. Reign theme offers multiple layouts and extensive customization options for the member directory.

## Directory Layouts

### Available Layouts

#### Layout 1: Grid View
```
┌─────┐ ┌─────┐ ┌─────┐ ┌─────┐
│Avatar│ │Avatar│ │Avatar│ │Avatar│
│ Name │ │ Name │ │ Name │ │ Name │
│ Meta │ │ Meta │ │ Meta │ │ Meta │
└─────┘ └─────┘ └─────┘ └─────┘
```

#### Layout 2: List View
```
[Avatar] Name | Location | Last Active | [Actions]
─────────────────────────────────────────────────
[Avatar] Name | Location | Last Active | [Actions]
```

#### Layout 3: Card View
```
┌──────────────────────┐
│ [Avatar]   Name      │
│ @username            │
│ Bio excerpt...       │
│ [Follow] [Message]   │
└──────────────────────┘
```

#### Layout 4: Masonry
Variable height cards in masonry grid

### Setting Directory Layout

**Location:** Appearance → Customize → BuddyPress → Members Directory

```php
// Programmatically set layout
function reign_set_members_layout() {
    return 'grid'; // grid, list, card, masonry
}
add_filter('reign_members_directory_layout', 'reign_set_members_layout');
```

## Directory Configuration

### Members Per Page

**Settings:**
```
Default: 20 members
Options: 12, 16, 20, 24, 30, 40
Pagination: Numbers / Load More / Infinite Scroll
```

### Default Sorting

**Sort Options:**
```
○ Active (Recently active first)
○ Newest (Recently joined)
○ Alphabetical (A-Z by name)
○ Random (Randomized order)
○ Popular (Most friends/followers)
```

### Member Cards Information

**Display Options:**
```
✓ Avatar Image
✓ Display Name
✓ @Username
✓ User Role/Badge
✓ Last Active Time
✓ Member Since
□ Location
□ Brief Bio
□ Social Links
□ Mutual Friends Count
□ Groups Count
□ Points/Achievements
```

## Search & Filtering

### Member Search

**Search Configuration:**
```
Search Type: Live Search / Submit Button
Search Fields:
✓ Display Name
✓ Username
✓ Bio/About
□ Location
□ Interests
Min Characters: 3
```

### Advanced Filters

**Filter Options:**
```
Member Type:
□ All Members
□ Students
□ Instructors
□ Moderators

Profile Fields:
□ Location
□ Age Range
□ Interests
□ Skills
□ Language

Activity:
□ Recently Active (24h)
□ This Week
□ This Month
□ New Members

Connection:
□ My Friends
□ Mutual Friends
□ Following
□ Followers
```

### Filter UI Styles

**Display As:**
1. **Dropdown** - Space-saving dropdowns
2. **Checkboxes** - Multiple selections
3. **Radio Buttons** - Single selection
4. **Tags** - Clickable tag filters
5. **Sidebar** - Vertical filter panel

## Profile Fields Integration

### Displayed Fields

**Configure at:** Users → Profile Fields

**Field Types:**
```
Text Field: Name, Location, Bio
Selectbox: Country, Language, Interests
Multi-Select: Skills, Hobbies
Date: Birthday, Join Date
Number: Age, Experience Years
URL: Website, Social Links
```

### Field Visibility
```
○ Everyone
○ Logged In Users
○ My Friends
○ Only Me
○ Admins Only
```

## Member Actions

### Action Buttons

**Available Actions:**
```
Public Actions:
✓ View Profile
✓ Send Message
✓ Add Friend/Follow
✓ View Friends
✓ View Groups

Admin Actions:
□ Edit Profile
□ Ban/Suspend
□ Delete Member
□ Reset Password
```

### Button Styles
```
Style: Default / Rounded / Ghost / Solid
Position: Below Avatar / Overlay / Right Side
Size: Small / Medium / Large
Icons: None / Left / Right / Only Icons
```

## Member Badges & Achievements

### User Badges

**Display Options:**
```
Badge Position: Over Avatar / Below Name / In Meta
Badge Types:
✓ Verified Member
✓ Premium Member
✓ Moderator
✓ Top Contributor
✓ Years Active
Custom Badges: Via GamiPress/BadgeOS
```

### Achievement Integration

**Supported Plugins:**
- GamiPress
- BadgeOS
- myCred
- WP Achievements

## Cover Images

### Member Cover Photos

**Settings:**
```
Enable Cover Images: Yes
Default Cover: Pattern / Gradient / Image
Upload Size: 1920x300px recommended
Position: Top / Behind Avatar
Parallax Effect: Enable / Disable
```

### Cover Image Positioning
```php
// Custom cover image position
function reign_member_cover_position($args) {
    $args['height'] = 350;
    $args['width'] = 1920;
    return $args;
}
add_filter('bp_before_members_cover_image_settings_parse_args', 'reign_member_cover_position');
```

## Online Status

### Status Indicators

**Display Options:**
```
Status Types:
● Online (Green)
● Away (Yellow)
● Busy (Red)
● Offline (Gray)

Position: Avatar Corner / Name Badge
Update Interval: 60 seconds
Show Last Seen: Yes / No
```

### Custom Status Messages
```
Enable Custom Status: Yes
Max Characters: 50
Emoji Support: Yes
Duration: 24 hours / Until Changed
```

## Member Types

### Creating Member Types

```php
function reign_register_member_types() {
    bp_register_member_type('student', array(
        'labels' => array(
            'name' => 'Students',
            'singular_name' => 'Student',
        ),
        'has_directory' => true,
        'directory_slug' => 'students',
    ));

    bp_register_member_type('instructor', array(
        'labels' => array(
            'name' => 'Instructors',
            'singular_name' => 'Instructor',
        ),
        'has_directory' => true,
        'directory_slug' => 'instructors',
    ));
}
add_action('bp_register_member_types', 'reign_register_member_types');
```

### Member Type Tabs
```
All Members | Students (45) | Instructors (12) | Staff (8)
```

## Privacy Settings

### Directory Privacy

**Options:**
```
Directory Visibility:
○ Public (Everyone)
○ Logged In Users Only
○ Members Only (Verified)
○ Friends of Members

Hide Members:
□ New members (< 7 days)
□ Inactive members (> 30 days)
□ Suspended members
□ Private profiles
```

### Profile Visibility

**Member Control:**
```
Allow members to:
✓ Hide from directory
✓ Hide profile fields
✓ Block other members
✓ Restrict messaging
```

## Responsive Design

### Mobile Layout

**Mobile Adjustments:**
```
< 768px:
- Single column layout
- Condensed member cards
- Slide-out filters
- Tap to reveal actions

< 480px:
- Minimal card design
- Avatar + Name only
- Bottom sheet actions
```

### Touch Interactions
```
Swipe: Next/Previous member
Long Press: Quick actions menu
Pull to Refresh: Reload directory
Pinch: Zoom avatar
```

## Performance

### Optimization Settings

```php
// Limit member queries
function reign_optimize_member_queries($args) {
    $args['per_page'] = 20;
    $args['populate_extras'] = false; // Disable extra queries
    return $args;
}
add_filter('bp_after_has_members_parse_args', 'reign_optimize_member_queries');
```

### Caching
```
Cache Duration: 1 hour
Cache Key: members_directory_{page}_{filter}_{sort}
Clear On: New member, Profile update
```

### Lazy Loading
```
Enable: Yes
Load: 10 members initially
Then: Load 10 more on scroll
Offset: 200px from bottom
```

## Widgets

### Members Widgets

**Available Widgets:**
1. **Recently Active Members**
2. **Newest Members**
3. **Popular Members**
4. **Random Members**
5. **Featured Members**
6. **Online Members**

### Widget Settings
```
Title: Active Community Members
Number: 5 members
Show: Avatar + Name + Meta
Avatar Size: 50px
Link to: Profile / Message / Directory
```

## Shortcodes

### Members Directory Shortcode

```
[reign_members
    type="active"
    max="20"
    layout="grid"
    columns="4"
    show_filters="yes"]
```

### Member List Shortcode

```
[reign_member_list
    include="1,2,3,4,5"
    exclude=""
    type="newest"
    layout="list"]
```

## Hooks & Filters

### Useful Hooks

```php
// Before directory
do_action('bp_before_directory_members_page');

// After member avatar
do_action('bp_directory_members_item_avatar');

// Custom member meta
do_action('bp_directory_members_item_meta');

// After directory
do_action('bp_after_directory_members_page');
```

### Filters

```php
// Modify member query
add_filter('bp_ajax_querystring', 'custom_members_query');

// Change avatar size
add_filter('bp_core_avatar_dimension', 'custom_avatar_size');

// Add custom column
add_filter('reign_members_directory_columns', 'add_custom_column');
```

## Troubleshooting

### Members Not Showing

**Check:**
1. BuddyPress activated
2. Members component enabled
3. User roles have correct capabilities
4. Privacy settings
5. Theme compatibility mode

### Search Not Working

**Solutions:**
- Clear permalinks
- Check JavaScript errors
- Verify Ajax URL
- Test without plugins
- Check search index

### Performance Issues

**Optimize:**
- Reduce members per page
- Disable populate_extras
- Enable caching
- Optimize avatar sizes
- Use CDN for images

## Best Practices

1. **Performance** - Limit to 20-30 members per page
2. **Mobile First** - Test on mobile devices
3. **Privacy** - Respect user privacy settings
4. **Accessibility** - Proper ARIA labels
5. **SEO** - Meta descriptions for directory pages
6. **User Experience** - Clear action buttons
7. **Filtering** - Relevant filter options only
8. **Caching** - Implement proper caching strategy