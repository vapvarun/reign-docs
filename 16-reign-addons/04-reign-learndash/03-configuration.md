# Reign LearnDash Addon - Configuration Guide (Complete)

## Overview

The Reign LearnDash Addon v4.8.2 provides extensive configuration options for course display, BuddyPress integration, review systems, and social learning features. This guide covers all available settings and customization options.

## Course Display Configuration

### Layout Templates (4 Available)

1. **Classic Template** - Traditional course card design
2. **Minimal Template** - Clean, simple course display
3. **Premium Template** - Enhanced layout with additional details
4. **Detailed Template** - Comprehensive course information display

### Layout Options (3 Designs)

1. **Layout One** - Default grid layout with standard spacing
2. **Layout Two** - Enhanced grid with improved typography
3. **Layout Three** - Advanced layout with premium styling

### Udemy-Style Course Cards

Enable professional course cards similar to Udemy:
```
[modern_courses udemy_style="yes" template="premium" show_price="yes" show_reviews="yes"]
```

**Udemy-style features include:**
- Course thumbnails with overlay effects
- Star ratings and review counts
- Course pricing display
- Progress bars for enrolled users
- Instructor information with avatars
- Course statistics (lessons, students, duration)

## Course & Group Filtering Configuration

### Advanced Filter Options

**Category Filtering:**
- Dropdown category selector
- Multi-select category checkboxes
- Category tag cloud interface

**Instructor Filtering:**
- Filter by instructor name/username
- Filter by instructor role
- Instructor-specific course pages

**Price Type Filtering:**
- Free courses only
- Paid courses only
- All courses (mixed)

**Enrollment Status Filtering:**
- Show enrolled courses only
- Show non-enrolled courses
- Show all courses with enrollment indicators

**Progress-Based Filtering:**
- Minimum progress percentage
- Maximum progress percentage
- Completion status filtering

## BuddyPress Integration Configuration

### Course-Group Synchronization

**Automatic Group Creation:**
- Enable/disable automatic BuddyPress group creation for courses
- Configure group privacy settings (public, private, hidden)
- Set default group roles (member, moderator, admin)

**User Synchronization:**
- Sync course enrollment with group membership
- Automatic role assignment based on course progress
- Group leader assignment for instructors

### Activity Stream Configuration

**Activity Types (All Configurable):**
- Course enrollment activities
- Course completion activities
- Lesson completion activities
- Topic completion activities
- Quiz completion activities
- Course review and rating activities
- Group joining/leaving activities

**Activity Settings:**
- Enable/disable specific activity types
- Configure activity privacy levels
- Set activity notification preferences

### Profile Integration

**LearnDash Courses Tab:**
- Add dedicated courses tab to user profiles
- Display enrolled courses with progress
- Show completed courses and achievements
- Configure tab position and visibility

**Profile Display Options:**
- Grid or list view for enrolled courses
- Progress bars and completion indicators
- Course ratings and review access
- Social sharing features

## Review & Rating System Configuration

### Rating System Setup

**5-Star Rating System:**
- Enable/disable course ratings
- Configure rating display options
- Set rating submission permissions

**Review Management:**
- Enable detailed course reviews
- Configure review moderation settings
- Set review character limits
- Enable/disable guest reviews

**Rating Analytics:**
- Display rating breakdowns by star count
- Show average ratings with review counts
- Configure rating aggregation methods

### Review Display Configuration

**Review Elements:**
- Star rating visualization
- Review titles and detailed comments
- User information display (avatar, name, date)
- Review helpfulness voting
- Review sorting and filtering

## Widget Configuration

### Course Categories Widget

**Configuration Options:**
- Display format (dropdown, list, cloud)
- Category count display
- Hierarchical category display
- Custom styling options

### Course Listing Widget

**Display Settings:**
- Number of courses to display
- Course ordering options (recent, popular, rated)
- Template selection (mini, compact, detailed)
- Thumbnail size and display

### Course Search Widget

**Search Features:**
- Live search functionality
- Category filtering integration
- Advanced search options
- Search result styling

## Related Courses Configuration

### Algorithm Settings

**Relationship Factors:**
- Category-based recommendations (primary)
- Tag-based associations
- Instructor relationships
- Course difficulty level matching
- User enrollment history

**Display Configuration:**
- Number of related courses (1-12)
- Related courses section title
- Template selection for related courses
- Positioning (before/after course content)

### Customization Options

**Related Courses Display:**
- Grid layout with configurable columns
- Course card template selection
- Show/hide course metadata
- Custom CSS styling options

## Advanced Configuration

### Performance Optimization

**Query Optimization:**
- Chunked user queries for large enrollments
- Efficient database query caching
- Memory-efficient user retrieval
- Optimized course metadata loading

**Caching Configuration:**
- Course data caching duration
- User progress caching
- Review and rating caching
- Template fragment caching

### Template Customization

**Template Override System:**
- Copy templates to theme directory
- Safe template customization
- Version-compatible overrides
- Template hierarchy management

**Available Templates:**
- Course archive templates
- Single course page templates
- Group archive templates
- Profile integration templates
- Widget templates

## Configuration Examples

### Complete Learning Portal Setup

**Homepage Course Display:**
```
[modern_courses per_page="8" columns="4" template="premium" udemy_style="yes" show_filters="yes" show_search="yes"]
```

**Category Page Configuration:**
```
[modern_courses category="web-development" template="detailed" show_instructor="yes" show_reviews="yes" show_price="yes"]
```

**User Profile Integration:**
```
[modern_courses enrolled="yes" show_progress="yes" template="premium" columns="2"]
```

### BuddyPress Social Learning Setup

**Group-Course Synchronization:**
```
[modern_courses buddypress_sync="yes" show_groups="yes"]
[modern_groups buddypress_sync="yes" show_courses="yes"]
```

**Activity Stream Integration:**
- Enable all course-related activities
- Configure activity privacy settings
- Set up activity notifications

### Instructor-Focused Configuration

**Instructor Course Pages:**
```
[modern_courses instructor="current" template="detailed" show_students="yes" show_reviews="yes" show_duration="yes"]
```

**Instructor Profile Enhancement:**
- Enable instructor information display
- Show instructor ratings and reviews
- Display instructor course statistics

## Admin Panel Configuration

### LearnDash Integration Settings

**Course Display Options:**
- Default template selection
- Default layout configuration
- Column count settings
- Pagination preferences

**Review System Settings:**
- Enable/disable rating system
- Configure review permissions
- Set moderation requirements
- Configure rating calculations

### BuddyPress Settings

**Group Integration:**
- Enable automatic group creation
- Configure default group settings
- Set group privacy preferences
- Configure role synchronization

**Activity Logging:**
- Select activity types to log
- Configure activity visibility
- Set notification preferences

### Performance Settings

**Optimization Options:**
- Database query caching
- Template fragment caching
- Image optimization settings
- JavaScript/CSS minification

## Troubleshooting Configuration

### Common Configuration Issues

**Templates Not Applying:**
1. Clear all caches (page, object, plugin)
2. Verify template parameter spelling
3. Check theme compatibility
4. Test with default settings

**BuddyPress Integration Issues:**
1. Verify BuddyPress components are active
2. Check user permissions and roles
3. Test group synchronization settings
4. Validate activity logging configuration

**Performance Issues:**
1. Optimize course count per page
2. Enable appropriate caching
3. Check database query efficiency
4. Monitor server resource usage

### Configuration Best Practices

**Course Display:**
- Use appropriate course counts (12-24 per page)
- Enable relevant filters for user experience
- Choose templates based on content type
- Optimize images and thumbnails

**Social Learning:**
- Configure appropriate activity types
- Set reasonable privacy settings
- Enable relevant profile features
- Test group synchronization thoroughly

---

*Comprehensive configuration guide based on complete analysis of Reign LearnDash Addon v4.8.2 source code*