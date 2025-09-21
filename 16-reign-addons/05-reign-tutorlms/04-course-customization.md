# Reign TutorLMS Addon - Course Customization Guide

## Overview

This comprehensive guide covers all aspects of customizing course displays, layouts, and user experience with Reign TutorLMS Addon v2.0.0, including multi-platform social integration, AJAX progress tracking, and mobile-optimized designs.

---

## Part 1: Course Display Customization

### Course Card Layouts

#### Grid Layout Options

**Modern Card Style (Default)**
```yaml
Features:
  - Drop shadows with hover effects
  - Rounded corners (8px)
  - Smooth transitions
  - Overlay progress bars
  - Instructor avatars
  - Price badges

Customization:
  Card Background: White/Dark mode
  Border Radius: 0-20px
  Shadow Depth: None, Light, Medium, Heavy
  Hover Animation: Lift, Scale, Glow
```

**Minimal Style**
```yaml
Features:
  - Clean typography focus
  - Minimal visual elements
  - Large course titles
  - Subtle dividers
  - Text-based progress
  - Flat design aesthetic

Best For:
  - Text-heavy content
  - Professional courses
  - Academic institutions
  - Clean, distraction-free UI
```

**Detailed Style**
```yaml
Features:
  - Rich course information
  - Multiple data points
  - Comprehensive previews
  - Extended descriptions
  - Full instructor profiles
  - Detailed statistics

Use Cases:
  - Course marketplaces
  - Complex course catalogs
  - Professional training
  - Certification programs
```

#### List Layout Customization

**Horizontal List Style**
```yaml
Layout:
  Image Position: Left (thumbnail)
  Content Flow: Horizontal
  Progress: Inline bar
  Actions: Right-aligned buttons

Responsive:
  Mobile: Stacks vertically
  Tablet: Maintains horizontal
  Desktop: Full horizontal layout
```

**Vertical List Style**
```yaml
Layout:
  Image Position: Top (full width)
  Content Flow: Vertical stack
  Progress: Full-width bar
  Actions: Bottom buttons

Spacing:
  Item Padding: 20px
  Image Margin: 15px bottom
  Content Spacing: 10px between elements
```

---

## Part 2: Progress Visualization Customization

### Progress Bar Styles

#### Animated Progress Bars

**Configuration Options:**
```yaml
Style Options:
  bar_style: "rounded" | "square" | "thin" | "thick"
  animation: "smooth" | "step" | "bounce" | "elastic"
  colors: "gradient" | "solid" | "themed"
  duration: 0.5-3.0 seconds

Color Schemes:
  Default: Blue (#007cba)
  Success: Green (#28a745)
  Warning: Orange (#ffc107)
  Custom: Any hex color
  Gradient: Multi-color gradients
```

**CSS Customization:**
```css
/* Custom progress bar styling */
.reign-tutor-progress-bar {
    height: 8px;
    background: #f0f0f0;
    border-radius: 4px;
    overflow: hidden;
}

.reign-tutor-progress-bar .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #007cba 0%, #005a87 100%);
    transition: width 0.8s ease-in-out;
}

/* Progress text customization */
.reign-tutor-progress-text {
    font-size: 12px;
    font-weight: 600;
    color: #666;
    margin-top: 5px;
}
```

#### Circular Progress Indicators

**Circle Progress Configuration:**
```yaml
Circle Settings:
  size: "small" (40px) | "medium" (60px) | "large" (80px)
  thickness: 2-10px
  background_color: "#f0f0f0"
  progress_color: "#007cba"
  text_display: percentage | fraction | none

Animation:
  duration: 1.5s
  easing: "ease-out"
  delay: 0-2s
  direction: "clockwise" | "counterclockwise"
```

---

## Part 3: Social Integration Customization

### BuddyPress Profile Integration

#### Profile Tab Customization

**Tab Appearance:**
```yaml
Tab Design:
  Tab Title: "My Courses" (customizable)
  Tab Icon: Custom icon support
  Tab Position: After Activity (configurable)
  Tab Badge: Course count display

Content Layout:
  Grid Columns: 2-4 responsive
  Card Style: Matches site theme
  Pagination: 6-12 courses per page
  Filtering: Status-based filters
```

**Custom Tab Template:**
```php
// In your theme: buddypress/members/single/courses.php
<div class="reign-tutor-profile-courses">
    <div class="courses-filter">
        <select id="course-status-filter">
            <option value="all">All Courses</option>
            <option value="enrolled">Enrolled</option>
            <option value="completed">Completed</option>
            <option value="in_progress">In Progress</option>
        </select>
    </div>

    <div class="courses-grid">
        <?php echo do_shortcode('[reign_tutor_course my_courses="true" show_progress="true" user_context="profile_owner"]'); ?>
    </div>
</div>
```

#### Activity Stream Integration

**Activity Types Customization:**
```yaml
Course Enrollment Activity:
  Template: "{user} enrolled in {course}"
  Include: Course thumbnail, price, instructor
  Privacy: Respects course privacy settings

Course Completion Activity:
  Template: "{user} completed {course} with {progress}% progress"
  Include: Certificate badge, completion time
  Achievement: Unlock special badges

Progress Milestone Activity:
  Template: "{user} reached {milestone}% in {course}"
  Triggers: 25%, 50%, 75% completion
  Include: Progress visualization
```

### PeepSo Integration Customization

#### Profile Widget Styling

**PeepSo Course Widget:**
```yaml
Widget Configuration:
  Title: "Learning Progress"
  Display: Grid or list view
  Course Count: 3-9 courses
  Show Progress: Yes/No
  Include Actions: Enroll, Continue, View

Styling Options:
  Background: Transparent/Card style
  Borders: None/Subtle/Prominent
  Typography: Match PeepSo theme
  Colors: PeepSo color scheme
```

---

## Part 4: Mobile Optimization

### Responsive Design Customization

#### Mobile Course Cards

**Touch-Optimized Design:**
```yaml
Mobile Specifications:
  Minimum Touch Target: 44px
  Card Padding: 16px
  Font Sizes: 16px+ for readability
  Button Spacing: 12px minimum
  Image Aspect: 16:9 for videos, 4:3 for images

Interaction:
  Tap Highlights: Disabled (iOS)
  Hover States: Touch-friendly alternatives
  Gestures: Swipe for course navigation
  Loading: Progressive with placeholders
```

**Mobile Layout Code:**
```css
/* Mobile-first responsive design */
@media (max-width: 768px) {
    .reign-tutor-courses-grid {
        grid-template-columns: 1fr;
        gap: 16px;
        padding: 16px;
    }

    .reign-tutor-course-card {
        padding: 16px;
        border-radius: 8px;
    }

    .course-title {
        font-size: 18px;
        line-height: 1.4;
        margin-bottom: 8px;
    }

    .course-meta {
        font-size: 14px;
        margin-bottom: 12px;
    }

    .course-actions {
        margin-top: 16px;
    }

    .course-button {
        min-height: 44px;
        font-size: 16px;
        padding: 12px 20px;
    }
}
```

#### Mobile Navigation

**Course Navigation Optimization:**
```yaml
Navigation Elements:
  Back Button: Always visible
  Progress Indicator: Top of screen
  Next/Previous: Large touch targets
  Menu Access: Hamburger or tab bar

Performance:
  Lazy Loading: Images and content
  Preloading: Next lesson content
  Caching: Offline content access
  Compression: Optimized assets
```

---

## Part 5: AJAX Customization

### Real-Time Progress Updates

#### Progress Tracking Configuration

**AJAX Settings:**
```yaml
Update Frequency:
  Real-time: Immediate updates
  Batched: Every 30 seconds
  Manual: User-triggered updates

Visual Feedback:
  Loading Spinners: Custom animations
  Success Messages: Fade-in notifications
  Error Handling: Retry mechanisms

Performance:
  Debouncing: 300ms for user inputs
  Throttling: Max 1 request per second
  Caching: 5-minute client cache
```

**Custom AJAX Implementation:**
```javascript
// Custom progress update handler
function updateCourseProgress(courseId, userId, progress) {
    const data = {
        action: 'reign_tutor_update_progress',
        course_id: courseId,
        user_id: userId,
        progress: progress,
        nonce: reign_tutor_ajax.nonce
    };

    jQuery.ajax({
        url: reign_tutor_ajax.ajax_url,
        type: 'POST',
        data: data,
        beforeSend: function() {
            // Show loading indicator
            jQuery('.progress-container').addClass('updating');
        },
        success: function(response) {
            if (response.success) {
                // Update progress bar with animation
                updateProgressBar(progress);

                // Show success notification
                showNotification('Progress updated!', 'success');

                // Update profile display if visible
                updateProfileProgress(courseId, progress);
            }
        },
        error: function() {
            showNotification('Update failed. Please try again.', 'error');
        },
        complete: function() {
            jQuery('.progress-container').removeClass('updating');
        }
    });
}
```

### Dynamic Course Filtering

**Filter Interface Customization:**
```yaml
Filter Options:
  Status Filter: All, Enrolled, Completed, In Progress
  Category Filter: Multi-select dropdown
  Instructor Filter: Searchable list
  Price Filter: Range slider
  Difficulty Filter: Beginner, Intermediate, Advanced

Filter Behavior:
  Update Method: AJAX (no page reload)
  Animation: Smooth fade transitions
  URL Updates: Browser history support
  Reset Option: Clear all filters
```

---

## Part 6: Advanced Styling

### Custom CSS Framework

#### Theme Integration

**Reign Theme Variables:**
```css
/* Use Reign theme variables for consistency */
:root {
    --reign-primary-color: #007cba;
    --reign-secondary-color: #6c757d;
    --reign-success-color: #28a745;
    --reign-warning-color: #ffc107;
    --reign-danger-color: #dc3545;

    --reign-border-radius: 6px;
    --reign-box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    --reign-transition: all 0.3s ease;
}

/* Apply to TutorLMS elements */
.reign-tutor-course-card {
    border-radius: var(--reign-border-radius);
    box-shadow: var(--reign-box-shadow);
    transition: var(--reign-transition);
}

.reign-tutor-course-card:hover {
    box-shadow: 0 4px 8px rgba(0,0,0,0.15);
    transform: translateY(-2px);
}
```

#### Dark Mode Support

**Dark Mode Styles:**
```css
/* Dark mode course cards */
@media (prefers-color-scheme: dark) {
    .reign-tutor-course-card {
        background: #2d3748;
        color: #e2e8f0;
        border: 1px solid #4a5568;
    }

    .course-title {
        color: #f7fafc;
    }

    .course-meta {
        color: #a0aec0;
    }

    .reign-tutor-progress-bar {
        background: #4a5568;
    }

    .progress-fill {
        background: linear-gradient(90deg, #4299e1 0%, #3182ce 100%);
    }
}

/* Manual dark mode toggle */
.dark-mode .reign-tutor-course-card {
    /* Same as above */
}
```

---

## Part 7: Performance Optimization

### Image Optimization

#### Responsive Images

**Image Handling:**
```yaml
Image Sizes:
  Thumbnail: 150x150px (course list)
  Medium: 300x200px (course cards)
  Large: 600x400px (course headers)
  Full: Original size (course details)

Loading Strategy:
  Above Fold: Immediate loading
  Below Fold: Lazy loading
  Progressive: Low-quality placeholders
  WebP Support: Modern format fallback
```

**Lazy Loading Implementation:**
```html
<!-- Responsive image with lazy loading -->
<img
    src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 300 200'%3E%3C/svg%3E"
    data-src="course-image-300x200.jpg"
    data-srcset="course-image-150x100.jpg 150w,
                 course-image-300x200.jpg 300w,
                 course-image-600x400.jpg 600w"
    data-sizes="(max-width: 768px) 100vw, (max-width: 1024px) 50vw, 33vw"
    alt="Course Title"
    class="lazy-load course-thumbnail"
    loading="lazy"
>
```

### Caching Strategies

**Client-Side Caching:**
```javascript
// Course data caching
const CourseCache = {
    data: new Map(),
    ttl: 300000, // 5 minutes

    set(key, value) {
        this.data.set(key, {
            value: value,
            timestamp: Date.now()
        });
    },

    get(key) {
        const item = this.data.get(key);
        if (!item) return null;

        if (Date.now() - item.timestamp > this.ttl) {
            this.data.delete(key);
            return null;
        }

        return item.value;
    }
};
```

---

## Part 8: Accessibility Customization

### Screen Reader Optimization

**ARIA Labels and Roles:**
```html
<!-- Accessible course card -->
<article class="reign-tutor-course-card" role="article" aria-labelledby="course-title-123">
    <h3 id="course-title-123" class="course-title">JavaScript Fundamentals</h3>

    <div class="course-progress" role="progressbar"
         aria-valuenow="75" aria-valuemin="0" aria-valuemax="100"
         aria-label="Course progress: 75% complete">
        <div class="progress-fill" style="width: 75%"></div>
        <span class="sr-only">75% complete</span>
    </div>

    <button class="course-action" aria-describedby="course-title-123">
        Continue Course
        <span class="sr-only">JavaScript Fundamentals</span>
    </button>
</article>
```

### Keyboard Navigation

**Focus Management:**
```css
/* Keyboard focus indicators */
.reign-tutor-course-card:focus-within {
    outline: 2px solid var(--reign-primary-color);
    outline-offset: 2px;
}

.course-action:focus {
    box-shadow: 0 0 0 3px rgba(0, 124, 186, 0.3);
    outline: none;
}

/* Skip links for keyboard users */
.skip-to-courses {
    position: absolute;
    left: -10000px;
    width: 1px;
    height: 1px;
    overflow: hidden;
}

.skip-to-courses:focus {
    position: static;
    width: auto;
    height: auto;
    padding: 8px 16px;
    background: var(--reign-primary-color);
    color: white;
    text-decoration: none;
}
```

---

## Part 9: Custom Templates

### Template Hierarchy

**Template Override System:**
```
Theme Template Locations:
1. /wp-content/themes/child-theme/reign-tutorlms/
2. /wp-content/themes/parent-theme/reign-tutorlms/
3. /wp-content/plugins/reign-tutorlms-addon/templates/

Available Templates:
├── course-card.php          # Individual course card
├── course-grid.php          # Course grid container
├── course-list.php          # Course list layout
├── course-progress.php      # Progress bar component
├── category-card.php        # Category display card
├── profile-courses.php      # Profile integration
└── shortcode-wrapper.php    # Shortcode container
```

### Custom Template Examples

**Custom Course Card Template:**
```php
<?php
// course-card.php - Custom course card template
$course_id = get_the_ID();
$course = tutor()->course();
$user_id = get_current_user_id();
$progress = tutor_utils()->get_course_completed_percent($course_id, $user_id);
?>

<article class="custom-course-card" data-course-id="<?php echo $course_id; ?>">
    <div class="course-image-container">
        <?php if (has_post_thumbnail()): ?>
            <div class="course-thumbnail">
                <?php the_post_thumbnail('medium', ['class' => 'course-image']); ?>

                <?php if ($progress > 0): ?>
                    <div class="progress-overlay">
                        <div class="progress-circle" data-progress="<?php echo $progress; ?>">
                            <span class="progress-text"><?php echo round($progress); ?>%</span>
                        </div>
                    </div>
                <?php endif; ?>
            </div>
        <?php endif; ?>
    </div>

    <div class="course-content">
        <h3 class="course-title">
            <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
        </h3>

        <div class="course-meta">
            <?php
            $instructor = tutor_utils()->get_course_instructor_by_course($course_id);
            if ($instructor): ?>
                <div class="course-instructor">
                    <?php echo get_avatar($instructor->ID, 24); ?>
                    <span>by <?php echo $instructor->display_name; ?></span>
                </div>
            <?php endif; ?>

            <?php
            $duration = get_post_meta($course_id, '_tutor_course_duration', true);
            if ($duration): ?>
                <div class="course-duration">
                    <i class="icon-clock"></i>
                    <span><?php echo $duration; ?></span>
                </div>
            <?php endif; ?>
        </div>

        <div class="course-excerpt">
            <?php echo wp_trim_words(get_the_excerpt(), 20); ?>
        </div>

        <div class="course-actions">
            <?php if (tutor_utils()->is_enrolled($course_id, $user_id)): ?>
                <a href="<?php the_permalink(); ?>" class="btn btn-primary">
                    <?php echo ($progress > 0) ? 'Continue Learning' : 'Start Course'; ?>
                </a>
            <?php else: ?>
                <a href="<?php the_permalink(); ?>" class="btn btn-outline">
                    View Course
                </a>
            <?php endif; ?>
        </div>
    </div>
</article>
```

---

## Part 10: Testing and Quality Assurance

### Cross-Browser Testing

**Testing Matrix:**
```yaml
Desktop Browsers:
  - Chrome 90+ (Windows, macOS, Linux)
  - Firefox 88+ (Windows, macOS, Linux)
  - Safari 14+ (macOS)
  - Edge 90+ (Windows)

Mobile Browsers:
  - iOS Safari 14+
  - Chrome Mobile 90+
  - Samsung Internet 14+
  - Firefox Mobile 88+

Testing Tools:
  - BrowserStack for device testing
  - Chrome DevTools for responsive testing
  - Lighthouse for performance auditing
  - axe for accessibility testing
```

### Performance Benchmarks

**Target Metrics:**
```yaml
Page Load Performance:
  First Contentful Paint: < 1.5s
  Largest Contentful Paint: < 2.5s
  Cumulative Layout Shift: < 0.1
  First Input Delay: < 100ms

Course Grid Loading:
  Initial Render: < 1s
  AJAX Updates: < 500ms
  Image Loading: Progressive
  Scroll Performance: 60fps

Mobile Performance:
  3G Load Time: < 3s
  Touch Response: < 50ms
  Battery Usage: Optimized
  Data Usage: Minimized
```

---

## Best Practices Summary

### Design Guidelines
1. **Consistent Styling**: Match your site's design system
2. **Responsive Design**: Mobile-first approach
3. **Accessibility**: WCAG 2.1 AA compliance
4. **Performance**: Optimize for speed and user experience
5. **User Experience**: Intuitive navigation and clear actions

### Development Standards
1. **Semantic HTML**: Proper structure and meaning
2. **Progressive Enhancement**: Works without JavaScript
3. **Cross-Browser**: Test across multiple browsers
4. **Maintainable Code**: Clean, documented, and organized
5. **Security**: Validate inputs and sanitize outputs

---

**Next Steps:**
- [Developer Guide](05-developer-guide.md) - Advanced customization
- [Troubleshooting](07-troubleshooting.md) - Common issues
- [FAQ](08-faq.md) - Frequently asked questions

**Need Help?**
📧 support@wbcomdesigns.com | 📚 docs.wbcomdesigns.com