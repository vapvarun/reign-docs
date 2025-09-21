# Reign TutorLMS Addon - Configuration Guide

## Overview

This comprehensive configuration guide covers all aspects of setting up Reign TutorLMS Addon v2.0.0, including multi-platform integration (BuddyPress/PeepSo), AJAX progress tracking, context-aware displays, and advanced social learning features.

---

## Part 1: Core TutorLMS Integration Settings

### Basic Integration Configuration

**Location:** `Appearance → Customize → Reign TutorLMS Settings`

#### 1. General Integration
```yaml
Enable TutorLMS Integration: Yes
Theme Compatibility Mode: Auto-detect
Template Override: Enable
Custom Styling: Enable
Mobile Optimization: Yes
```

#### 2. Course Display Settings
```yaml
Course Grid Layout:
  Desktop Columns: 3
  Tablet Columns: 2
  Mobile Columns: 1
  Gap Between Items: 20px

Card Style:
  Style: Modern with shadows
  Border Radius: 8px
  Hover Effects: Enabled
  Loading Animation: Fade in
```

#### 3. Progress Tracking
```yaml
Enable Progress Bars: Yes
Progress Style: Animated
Show Percentage: Yes
Update Frequency: Real-time
AJAX Loading: Enabled
Fallback Method: Page refresh
```

---

## Part 2: Multi-Platform Social Integration

### BuddyPress/BuddyBoss Configuration

**Location:** `Reign Settings → Social Integration → BuddyPress`

#### Profile Tab Settings
```yaml
Tab Configuration:
  Tab Name: "My Courses"
  Tab Slug: courses
  Tab Position: After Activity
  Tab Visibility: Public/Members only

Display Options:
  Show All Courses: Yes
  Show In Progress: Yes
  Show Completed: Yes
  Show Enrolled Count: Yes
  Enable Pagination: Yes (10 per page)
```

#### Activity Stream Integration
```yaml
Activity Types:
  Course Enrollment: Enabled
  Lesson Completion: Enabled
  Course Completion: Enabled
  Quiz Completion: Enabled
  Certificate Earned: Enabled

Activity Content:
  Show Course Thumbnail: Yes
  Show Progress Percentage: Yes
  Include Course Link: Yes
  Custom Activity Text: Enabled
```

#### Group Integration
```yaml
Group Courses:
  Enable Group Course Association: Yes
  Auto-enroll Group Members: Optional
  Group Admin Course Management: Yes
  Bulk Enrollment: Enabled
  Group Course Tab: Enabled
```

### PeepSo Integration

**Location:** `Reign Settings → Social Integration → PeepSo`

#### Profile Integration
```yaml
PeepSo Profile Tab:
  Tab Name: "Learning"
  Tab Icon: education
  Tab Position: Custom order
  Privacy Level: Public/Members

Course Display:
  Layout: Grid
  Items Per Page: 9
  Show Progress: Yes
  Show Enrollment Date: Yes
  Filter Options: Enabled
```

#### Stream Integration
```yaml
PeepSo Stream Posts:
  Course Activities: Enabled
  Achievement Posts: Enabled
  Certificate Sharing: Enabled
  Custom Post Templates: Yes
  Privacy Controls: Per user settings
```

---

## Part 3: Context-Aware Display Configuration

### User Context Detection

**Location:** `Customizer → Reign TutorLMS → Context Settings`

#### Context Types
```yaml
Profile Owner Context:
  Show All Courses: Yes (enrolled, completed, in-progress)
  Show Private Courses: Yes
  Show Detailed Progress: Yes
  Enable Course Management: Yes

Profile Visitor Context:
  Show Public Courses Only: Yes
  Hide Private Information: Yes
  Show Basic Progress: Optional
  Enable Social Interactions: Yes

Logged-in User Context:
  Show Enrollment Status: Yes
  Show Available Actions: Yes
  Personalized Recommendations: Yes

Guest User Context:
  Show Course Catalog: Yes
  Hide User-specific Data: Yes
  Show Enrollment CTA: Yes
  Limited Information: Yes
```

#### Privacy Controls
```yaml
User Privacy Settings:
  Course Privacy: Public/Private/Friends
  Progress Sharing: Enabled/Disabled
  Achievement Sharing: Public/Private
  Profile Visibility: Customizable

Admin Override:
  Force Public Courses: No
  Admin Full Access: Yes
  Instructor Access: Limited
  Privacy Enforcement: Strict
```

---

## Part 4: Advanced Shortcode Configuration

### Course Display Shortcode Settings

**Shortcode:** `[reign_tutor_course]`

#### Layout Parameters
```yaml
Layout Options:
  layout: "grid" | "list" | "carousel" | "masonry"
  columns: 1-6 (responsive)
  posts_per_page: 1-100
  pagination: true/false

Grid Specific:
  grid_style: "card" | "minimal" | "detailed"
  card_hover: true/false
  equal_height: true/false

List Specific:
  list_style: "horizontal" | "vertical"
  show_excerpt: true/false
  excerpt_length: 150
```

#### Content Parameters
```yaml
Course Information:
  show_instructor: true/false
  show_price: true/false
  show_duration: true/false
  show_difficulty: true/false
  show_categories: true/false
  show_tags: true/false
  show_enrollment_count: true/false
  show_rating: true/false

Progress & Status:
  show_progress: true/false
  progress_style: "bar" | "circle" | "percentage"
  show_status: true/false
  status_text: custom

Visual Elements:
  show_thumbnail: true/false
  thumbnail_size: "small" | "medium" | "large"
  show_featured_badge: true/false
  custom_styling: CSS classes
```

#### User-Specific Parameters
```yaml
User Context:
  my_courses: true/false
  user_id: specific user ID
  user_context: "profile_owner" | "visitor" | "current_user"

Course Filtering:
  course_status: "all" | "enrolled" | "completed" | "in_progress" | "not_started"
  course_level: "beginner" | "intermediate" | "advanced"
  course_category: category slug
  instructor_id: specific instructor

Enrollment:
  enrollment_status: "all" | "enrolled" | "not_enrolled"
  show_enrollment_button: true/false
  enrollment_text: custom text
```

### Category Display Shortcode

**Shortcode:** `[reign_course_categories]`

#### Display Parameters
```yaml
Layout Settings:
  columns: 1-6
  show_count: true/false
  show_image: true/false
  show_description: true/false
  layout: "grid" | "list"

Category Information:
  include: category IDs
  exclude: category IDs
  orderby: "name" | "count" | "id"
  order: "ASC" | "DESC"
  hide_empty: true/false

Visual Settings:
  image_size: "thumbnail" | "medium" | "large"
  show_hierarchy: true/false
  depth: 1-5
  custom_styling: CSS classes
```

---

## Part 5: AJAX and Performance Configuration

### AJAX Settings

**Location:** `Reign Settings → Performance → AJAX`

#### Course Progress AJAX
```yaml
Progress Updates:
  Enable Real-time Updates: Yes
  Update Interval: Immediate
  Batch Updates: Yes (for performance)
  Progress Animation: Smooth

Error Handling:
  Fallback Method: Page refresh
  Retry Attempts: 3
  Timeout Duration: 30 seconds
  User Notifications: Enabled

Security:
  Nonce Verification: Enabled
  User Capability Check: Yes
  Rate Limiting: 60 requests/minute
  CSRF Protection: Enabled
```

#### Course Filtering AJAX
```yaml
Filter Updates:
  Dynamic Filtering: Enabled
  Filter Animation: Fade
  URL Updates: Yes (with history)
  Loading Indicators: Spinner

Performance:
  Cache Filter Results: 5 minutes
  Debounce Input: 300ms
  Lazy Load Images: Yes
  Progressive Loading: Yes
```

### Performance Optimization

#### Caching Configuration
```yaml
Page Caching:
  Cache Course Pages: Yes (24 hours)
  Cache User Profiles: No (dynamic content)
  Cache Course Catalog: Yes (1 hour)
  Cache Category Pages: Yes (6 hours)

Object Caching:
  Cache Course Data: Yes
  Cache User Progress: 15 minutes
  Cache Instructor Data: 1 hour
  Cache Category Data: 2 hours

AJAX Caching:
  Cache AJAX Responses: 5 minutes
  Cache User-specific Data: No
  Cache Public Data: Yes
  Invalidate on Updates: Yes
```

---

## Part 6: Mobile Optimization Settings

### Responsive Design Configuration

**Location:** `Customizer → Reign TutorLMS → Mobile Settings`

#### Mobile Layout
```yaml
Course Grid:
  Mobile Columns: 1
  Tablet Columns: 2
  Breakpoints: 768px, 1024px
  Stack Order: Title, Image, Content

Touch Optimization:
  Button Size: 44px minimum
  Touch Targets: Generous spacing
  Swipe Gestures: Enabled
  Tap Highlights: Disabled
```

#### Mobile Features
```yaml
Navigation:
  Mobile Menu: Collapsible
  Course Search: Prominent
  Profile Access: Quick toggle
  Back to Top: Enabled

Content:
  Font Size: 16px minimum
  Line Height: 1.6
  Image Loading: Lazy
  Video: Responsive embed

Performance:
  Minimize Resources: Yes
  Optimize Images: Yes
  Defer Non-critical: Yes
  Critical CSS: Inline
```

---

## Part 7: Security and Privacy Settings

### Data Protection

**Location:** `Reign Settings → Privacy → TutorLMS`

#### User Data Privacy
```yaml
Personal Information:
  Course Progress: Private by default
  Enrollment Data: User controlled
  Achievement Data: Public/Private choice
  Profile Integration: Opt-in

Data Retention:
  Progress History: Indefinite
  Activity Logs: 1 year
  Cache Data: 30 days
  Temporary Data: 24 hours

GDPR Compliance:
  Data Export: Enabled
  Data Deletion: User request
  Consent Management: Integrated
  Privacy Controls: Granular
```

#### Content Security
```yaml
Course Content:
  Access Control: Enrollment-based
  Content Protection: Yes
  Video Protection: Referrer check
  Download Prevention: Yes

API Security:
  Authentication: WordPress nonce
  Rate Limiting: Enabled
  Input Validation: Strict
  SQL Injection Protection: Yes
```

---

## Part 8: Notification and Email Settings

### TutorLMS Email Integration

**Location:** `TutorLMS → Settings → Email`

#### Course Notifications
```yaml
Enrollment Emails:
  Student Enrollment: Enabled
  Instructor Notification: Enabled
  Admin Notification: Enabled
  Custom Templates: Yes

Progress Emails:
  Lesson Completion: Optional
  Course Completion: Enabled
  Certificate Earned: Enabled
  Achievement Unlocked: Enabled

Social Notifications:
  BuddyPress Integration: Yes
  Email + Activity: Both
  Frequency: Immediate
  Digest Options: Daily/Weekly
```

### Social Platform Notifications

#### BuddyPress Notifications
```yaml
Activity Notifications:
  Course Activities: Enabled
  Friend Course Activity: Yes
  Group Course Activity: Yes
  Email Notifications: User choice

Real-time Notifications:
  Browser Notifications: Optional
  In-app Notifications: Yes
  Badge Counts: Enabled
  Sound Alerts: User choice
```

---

## Part 9: Advanced Developer Configuration

### Custom Hooks and Filters

#### Available Hooks
```php
// Course display customization
apply_filters('reign_tutor_course_card_content', $content, $course_id);
apply_filters('reign_tutor_progress_display', $progress_html, $user_id, $course_id);
apply_filters('reign_tutor_profile_courses', $courses, $user_id, $context);

// Social integration hooks
do_action('reign_tutor_course_enrolled', $user_id, $course_id);
do_action('reign_tutor_progress_updated', $user_id, $course_id, $progress);
do_action('reign_tutor_course_completed', $user_id, $course_id);
```

#### Custom Template System
```yaml
Template Hierarchy:
  1. Child theme templates
  2. Parent theme templates
  3. Plugin templates
  4. Default fallback

Template Locations:
  /reign-tutorlms/
    ├── course-card.php
    ├── course-progress.php
    ├── profile-courses.php
    └── category-grid.php
```

### API Integration

#### REST API Endpoints
```yaml
Course Data:
  GET /wp-json/reign-tutor/v1/courses
  GET /wp-json/reign-tutor/v1/courses/{id}
  GET /wp-json/reign-tutor/v1/user/{id}/courses

Progress Data:
  GET /wp-json/reign-tutor/v1/progress/{user_id}/{course_id}
  POST /wp-json/reign-tutor/v1/progress/update

Social Data:
  GET /wp-json/reign-tutor/v1/activity/{user_id}
  POST /wp-json/reign-tutor/v1/activity/create
```

---

## Part 10: Testing and Validation

### Configuration Testing

#### Functionality Tests
```yaml
Core Features:
  ✓ Course display in profiles
  ✓ AJAX progress updates
  ✓ Context-aware content
  ✓ Shortcode rendering
  ✓ Mobile responsiveness

Social Integration:
  ✓ BuddyPress profile tabs
  ✓ PeepSo integration
  ✓ Activity stream posts
  ✓ Group course association
  ✓ Privacy controls

Performance:
  ✓ Page load times < 3s
  ✓ AJAX response < 1s
  ✓ Mobile performance
  ✓ Cache effectiveness
  ✓ Database query optimization
```

#### Validation Checklist
- [ ] All shortcodes render correctly
- [ ] Profile integration working
- [ ] AJAX functions properly
- [ ] Mobile experience optimized
- [ ] Security settings active
- [ ] Privacy controls functional
- [ ] Performance benchmarks met
- [ ] Cross-browser compatibility
- [ ] Accessibility compliance
- [ ] SEO optimization

---

## Configuration Best Practices

### Performance Optimization
1. **Enable caching** for public course data
2. **Lazy load** course images and content
3. **Optimize AJAX** calls with proper debouncing
4. **Use CDN** for course media files
5. **Monitor database** query performance

### Security Best Practices
1. **Regular updates** for all components
2. **Strong authentication** for course access
3. **Input validation** on all forms
4. **HTTPS enforcement** for all course pages
5. **Regular security audits**

### User Experience
1. **Consistent design** across all course pages
2. **Clear navigation** between course elements
3. **Responsive design** for all devices
4. **Fast loading times** for all interactions
5. **Accessible content** for all users

---

## Need Help?

**Configuration Support:**
- 📧 Email: support@wbcomdesigns.com
- 📚 Documentation: docs.wbcomdesigns.com
- 💬 Community: facebook.com/groups/wbcom
- 🎥 Video tutorials: member portal

**Next Steps:**
- [Course Customization Guide](04-course-customization.md)
- [Shortcode Reference](06-shortcodes-reference.md)
- [Developer Guide](05-developer-guide.md)