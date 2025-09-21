# Reign LearnDash Addon - Course Customization (Complete)

## Overview

The Reign LearnDash Addon v4.8.2 provides extensive course customization options including multiple templates, Udemy-style layouts, advanced filtering, review systems, and BuddyPress social learning integration.

## Course Display Templates

### Template Options (4 Available)

#### 1. Classic Template
- Traditional course card design
- Standard layout with essential information
- Compatible with all course types
- Optimized for general use

```
[modern_courses template="classic"]
```

#### 2. Minimal Template
- Clean, simple course display
- Reduced visual clutter
- Focus on course essentials
- Perfect for large course catalogs

```
[modern_courses template="minimal"]
```

#### 3. Premium Template
- Enhanced layout with additional details
- Professional appearance
- Rich course information display
- Ideal for paid courses

```
[modern_courses template="premium"]
```

#### 4. Detailed Template
- Comprehensive course information display
- Maximum course metadata
- Advanced course statistics
- Best for course comparison pages

```
[modern_courses template="detailed"]
```

### Layout Designs (3 Options)

#### Layout One
- Standard grid layout with balanced spacing
- Default typography and styling
- Compatible with all templates

```
[modern_courses layout="layout_one"]
```

#### Layout Two
- Enhanced grid with improved typography
- Better visual hierarchy
- Optimized spacing and alignment

```
[modern_courses layout="layout_two"]
```

#### Layout Three
- Premium styling with advanced design elements
- Professional appearance
- Enhanced visual effects

```
[modern_courses layout="layout_three"]
```

## Udemy-Style Course Cards

### Enable Udemy-Style Design

Transform course cards to match professional online learning platforms:

```
[modern_courses udemy_style="yes" template="premium" show_price="yes" show_reviews="yes"]
```

### Udemy-Style Features

**Visual Elements:**
- Professional course thumbnails with overlay effects
- Hover animations and transitions
- Clean typography and spacing
- Modern card design

**Course Information:**
- Course pricing prominently displayed
- Star ratings and review counts
- Instructor information with avatars
- Course statistics (lessons, students, duration)
- Progress bars for enrolled users

**Interactive Elements:**
- Hover effects on course cards
- Quick preview functionality
- Social sharing buttons
- Wishlist/favorites integration

### Advanced Udemy-Style Configuration

```
[modern_courses
    udemy_style="yes"
    template="premium"
    layout="layout_three"
    show_price="yes"
    show_reviews="yes"
    show_instructor="yes"
    show_students="yes"
    show_duration="yes"
    show_lessons="yes"
    columns="3"]
```

## Course Review & Rating System

### 5-Star Rating System

**Enable Course Ratings:**
```
[modern_courses show_reviews="yes" template="premium"]
```

**Rating Features:**
- Star rating display on course cards
- Average rating calculation
- Total review count display
- Rating breakdown analytics

### Advanced Review System

**Review Components:**
- Star ratings (1-5 stars)
- Review titles and detailed comments
- User information (name, avatar, date)
- Review helpfulness voting
- Review moderation and approval

**Review Display Options:**
```
[modern_courses
    show_reviews="yes"
    template="detailed"
    show_review_count="yes"
    show_rating_breakdown="yes"]
```

### Review Analytics

**Rating Breakdown:**
- Percentage distribution by star rating
- Total number of reviews
- Average rating calculation
- Recent review highlights

## BuddyPress Social Learning Customization

### Course-Group Synchronization

**Enable Automatic Group Creation:**
```
[modern_courses buddypress_sync="yes" show_groups="yes"]
```

**Synchronization Features:**
- Automatic BuddyPress group creation for courses
- User synchronization between courses and groups
- Group privacy settings based on course access
- Role mapping (student → member, instructor → admin)

### Profile Integration

**Enrolled Courses Display:**
```
[modern_courses enrolled="yes" show_progress="yes" template="premium" columns="2"]
```

**Profile Features:**
- Dedicated "LearnDash Courses" tab in user profiles
- Course progress visualization
- Achievement and completion status
- Social sharing capabilities

### Activity Stream Integration

**Activity Types:**
- Course enrollment activities
- Lesson and topic completion
- Quiz completion activities
- Course review submissions
- Achievement unlocks

**Activity Display:**
```
[modern_courses show_activities="yes" activity_types="enrollment,completion,reviews"]
```

## Advanced Filtering & Search

### Filter Configuration

**Enable All Filters:**
```
[modern_courses
    show_filters="yes"
    show_search="yes"
    show_sorting="yes"
    show_view_switcher="yes"]
```

**Available Filters:**
- Category filtering (dropdown, checkboxes, tag cloud)
- Instructor filtering by name or role
- Price type filtering (free, paid, all)
- Enrollment status filtering
- Progress-based filtering
- Rating-based filtering

### Search Functionality

**AJAX-Powered Search:**
- Real-time course filtering
- No page reload required
- Instant results display
- Smart suggestions

**Advanced Search Options:**
```
[modern_courses
    show_search="yes"
    search_placeholder="Search courses..."
    enable_ajax_search="yes"
    search_categories="yes"
    search_instructors="yes"]
```

## Related Courses Customization

### Algorithm Configuration

**Related Course Factors:**
- Primary: Course categories and tags
- Secondary: Instructor relationships
- Tertiary: Course difficulty level
- Advanced: User enrollment history and preferences

**Display Configuration:**
```
[modern_courses
    show_related="yes"
    related_count="6"
    related_template="minimal"
    related_columns="3"]
```

### Related Courses Display

**Positioning Options:**
- Before course content
- After course content
- In sidebar widget
- Custom placement via shortcode

## Widget Customization

### Course Categories Widget

**Configuration Options:**
- Display format (dropdown, list, hierarchical)
- Category count display
- Custom styling and colors
- Icon integration

### Course Listing Widget

**Display Settings:**
- Number of courses (1-20)
- Template selection (mini, compact, detailed)
- Ordering options (recent, popular, rated)
- Thumbnail size and styling

### Course Search Widget

**Search Features:**
- Live search functionality
- Category filtering integration
- Advanced search options
- Custom result styling

## Instructor Customization

### Instructor Course Pages

**Display Instructor Courses:**
```
[modern_courses
    instructor="current"
    template="detailed"
    show_instructor="yes"
    show_students="yes"
    show_reviews="yes"
    show_duration="yes"]
```

**Instructor Features:**
- Instructor biography and credentials
- Course statistics and performance
- Student reviews and ratings
- Social media integration

### Instructor Profile Enhancement

**Enhanced Instructor Display:**
- Professional instructor cards
- Course portfolio showcase
- Student testimonials
- Achievement badges

## Performance Optimization

### Query Optimization

**Efficient Loading:**
```
[modern_courses
    per_page="12"
    enable_lazy_loading="yes"
    optimize_queries="yes"
    cache_duration="3600"]
```

**Performance Best Practices:**
- Reasonable course counts per page (12-24)
- Image optimization and lazy loading
- Database query caching
- Template fragment caching

### Mobile Optimization

**Responsive Design:**
- Mobile-first approach
- Touch-friendly interfaces
- Optimized loading for mobile devices
- Progressive image loading

## Customization Examples

### Complete Learning Portal

**Homepage Configuration:**
```
<!-- Hero Section - Featured Courses -->
[modern_courses
    per_page="8"
    columns="4"
    template="premium"
    udemy_style="yes"
    category="featured"
    show_price="yes"
    show_reviews="yes"]

<!-- Recent Courses -->
[modern_courses
    per_page="6"
    columns="3"
    orderby="date"
    template="minimal"
    show_filters="yes"]

<!-- Top Rated Courses -->
[modern_courses
    per_page="4"
    columns="2"
    orderby="rating"
    template="detailed"
    show_reviews="yes"
    show_instructor="yes"]
```

### Course Category Pages

**Web Development Courses:**
```
[modern_courses
    category="web-development"
    template="premium"
    udemy_style="yes"
    show_filters="yes"
    show_search="yes"
    show_instructor="yes"
    show_reviews="yes"
    show_price="yes"
    show_duration="yes"]
```

### User Dashboard

**Personal Learning Dashboard:**
```
<!-- Enrolled Courses -->
[modern_courses
    enrolled="yes"
    show_progress="yes"
    template="detailed"
    columns="2"
    show_completion="yes"]

<!-- Recommended Courses -->
[modern_courses
    recommended="yes"
    template="premium"
    columns="3"
    show_reviews="yes"]
```

### Instructor Profile

**Instructor Course Showcase:**
```
[modern_courses
    instructor="current"
    template="premium"
    show_students="yes"
    show_reviews="yes"
    show_duration="yes"
    show_lessons="yes"
    udemy_style="yes"]
```

## Advanced Customization

### Custom CSS Integration

**Template-Specific Styling:**
```css
/* Premium Template Customization */
.reign-course-template-premium {
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.1);
}

/* Udemy-Style Cards */
.reign-course-udemy-style {
    transition: transform 0.3s ease;
}

.reign-course-udemy-style:hover {
    transform: translateY(-5px);
}
```

### Template Overrides

**Custom Template Creation:**
1. Copy template files from plugin to theme
2. Customize HTML structure and styling
3. Add custom functionality
4. Maintain update compatibility

### Hook Integration

**Custom Functionality:**
```php
// Add custom course metadata
add_action('reign_course_card_after_title', 'custom_course_info');

// Modify course query
add_filter('reign_courses_query_args', 'custom_query_modification');

// Custom review display
add_filter('reign_course_review_display', 'custom_review_format');
```

---

*Comprehensive course customization guide based on complete analysis of Reign LearnDash Addon v4.8.2 source code*