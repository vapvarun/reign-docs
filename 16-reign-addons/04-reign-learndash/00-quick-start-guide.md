# Reign LearnDash Addon - Quick Start Guide

## What This Addon Provides

Reign LearnDash Addon v4.8.2 is a comprehensive learning management system integration providing advanced course layouts, social learning features, review systems, and extensive BuddyPress integration.

**Core Features (Comprehensive):**
- 6 advanced shortcodes with 25+ parameters each
- Multiple course templates (Classic, Minimal, Premium, Detailed)
- Udemy-style course cards with professional design
- Complete 5-star review and rating system
- BuddyPress social learning integration
- Course-group synchronization
- Enrolled courses display in user profiles
- Related courses algorithm
- 3 custom widgets for courses
- Advanced filtering and search capabilities

---

## Prerequisites

Required:
- ✅ WordPress 4.0+
- ✅ Reign Theme activated
- ✅ LearnDash LMS plugin

Optional:
- BuddyPress (for social learning features)

---

## Installation Steps

### Step 1: Install the Addon

1. **Upload via WordPress:**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   → Select reign-learndash-addon.zip
   → Install Now → Activate
   ```

2. **Verify Installation:**
   - Check Plugins page - "Reign LearnDash Addon" should be active
   - LearnDash courses should now use enhanced Reign styling

---

## Quick Setup & Testing

### Step 1: Test Basic Course Display

Add this shortcode to any page to test basic functionality:
```
[modern_courses]
```

### Step 2: Test Advanced Features

Try the Udemy-style course display:
```
[modern_courses template="premium" udemy_style="yes" show_price="yes" show_reviews="yes" columns="3"]
```

### Step 3: Enable BuddyPress Features (Optional)

If BuddyPress is active:
1. Check user profiles for "LearnDash Courses" tab
2. Test course enrollment activities in activity streams
3. Verify course-group synchronization

---

## Key Features Overview

### 1. Advanced Course Display

**Multiple Templates:**
- `template="classic"` - Traditional design
- `template="minimal"` - Clean layout
- `template="premium"` - Enhanced design
- `template="detailed"` - Comprehensive information

**Layout Options:**
- `layout="layout_one"` - Standard grid
- `layout="layout_two"` - Enhanced typography
- `layout="layout_three"` - Premium styling

**Udemy-Style Cards:**
```
[modern_courses udemy_style="yes" show_price="yes" show_reviews="yes" show_instructor="yes"]
```

### 2. Course Reviews & Ratings

**5-Star Rating System:**
- Course ratings and reviews
- Rating analytics and breakdowns
- Review moderation and management
- Guest review controls

**Display Reviews:**
```
[modern_courses show_reviews="yes" template="premium"]
```

### 3. BuddyPress Social Learning

**Course-Group Sync:**
```
[modern_courses buddypress_sync="yes"]
[modern_groups buddypress_sync="yes"]
```

**Profile Integration:**
- Enrolled courses tab in user profiles
- Course progress display
- Social learning activities
- Course-related discussions

### 4. Advanced Filtering

**Filter Options:**
```
[modern_courses show_filters="yes" show_search="yes" show_sorting="yes"]
```

**Specific Filters:**
```
// By category
[modern_courses category="web-development"]

// By instructor
[modern_courses instructor="john-smith"]

// By price type
[modern_courses price_type="free"]

// Enrolled courses only
[modern_courses enrolled="yes" show_progress="yes"]
```

### 5. Related Courses

Automatically displays related courses on single course pages based on:
- Course categories and tags
- Instructor relationships
- User enrollment history

### 6. Widget System

**Available Widgets:**
- Course Categories Widget
- Course Listing Widget
- Course Search Widget

Add these through Appearance → Widgets.

---

## Common Usage Examples

### Learning Portal Homepage
```
<!-- Featured Courses -->
[modern_courses per_page="8" columns="4" template="premium" udemy_style="yes" category="featured"]

<!-- Recent Courses -->
[modern_courses per_page="6" columns="3" orderby="date" template="minimal"]

<!-- Learning Groups -->
[modern_groups per_page="4" columns="2" template="creative" show_members="yes"]
```

### Course Category Pages
```
[modern_courses category="web-development" template="detailed" show_instructor="yes" show_reviews="yes" show_filters="yes"]
```

### User Profile Integration
```
<!-- User's Enrolled Courses -->
[modern_courses enrolled="yes" show_progress="yes" template="premium" columns="2"]

<!-- User's Groups -->
[modern_groups enrolled_only="yes" show_progress="yes" template="compact"]
```

### Instructor Profile
```
[modern_courses instructor="current" template="detailed" show_students="yes" show_reviews="yes"]
```

---

## BuddyPress Social Learning Setup

### Enable Course-Group Synchronization

1. **Automatic Group Creation:**
   - Courses automatically create corresponding BuddyPress groups
   - Group privacy settings mirror course access
   - Member roles sync with course enrollment

2. **Activity Stream Integration:**
   - Course enrollment activities
   - Progress completion activities
   - Review and rating activities
   - Social interactions

3. **Profile Features:**
   - "LearnDash Courses" tab in profiles
   - Enrolled courses with progress display
   - Achievement and completion status
   - Social sharing capabilities

### Test BuddyPress Features

1. Enroll in a course
2. Check your profile for the courses tab
3. Verify activities appear in streams
4. Test group synchronization

---

## Review System Setup

### Enable Course Reviews

The addon provides a complete 5-star rating system:

1. **Rating Features:**
   - Star ratings on course cards
   - Detailed review system
   - Review analytics and breakdowns
   - Rating aggregation

2. **Display Reviews:**
   ```
   [modern_courses show_reviews="yes" template="premium"]
   ```

3. **Review Management:**
   - Admin moderation controls
   - Guest review permissions
   - Review character limits
   - Spam prevention

---

## Performance Optimization

### Best Practices

1. **Course Display:**
   - Use reasonable per_page limits (12-24)
   - Enable caching for better performance
   - Optimize course images and thumbnails

2. **BuddyPress Integration:**
   - Configure appropriate activity types
   - Set reasonable group privacy settings
   - Monitor activity stream performance

3. **Review System:**
   - Enable review moderation for quality
   - Set appropriate review limits
   - Monitor review submission patterns

---

## Troubleshooting

### Common Issues

**Shortcodes Not Working:**
1. Verify plugin is activated (v4.8.2+)
2. Check LearnDash is properly configured
3. Ensure courses exist and are published
4. Clear all caches

**BuddyPress Features Missing:**
1. Verify BuddyPress is active
2. Check required components are enabled
3. Test with different user roles
4. Clear BuddyPress caches

**Review System Issues:**
1. Check review permissions
2. Verify rating display settings
3. Test with different user roles
4. Clear review caches

**Performance Issues:**
1. Reduce per_page counts
2. Enable appropriate caching
3. Optimize database queries
4. Check server resources

---

## Next Steps

For detailed configuration and advanced features:
- [Configuration Guide](03-configuration.md) - Complete settings guide
- [Course Customization](04-course-customization.md) - Advanced appearance options
- [Developer Guide](05-developer-guide.md) - Hooks, filters, and customization
- [Shortcodes Reference](06-shortcodes-reference.md) - Complete shortcode documentation

---

*Comprehensive Quick Start Guide based on complete analysis of Reign LearnDash Addon v4.8.2*