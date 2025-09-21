# Reign LifterLMS Addon - Shortcodes Reference (Complete)

## Available Shortcodes (Comprehensive Analysis)

Reign LifterLMS Addon v2.4.1 provides 2 advanced shortcodes with extensive functionality based on comprehensive source code analysis:

---

## Course Display Shortcodes

### [reign_lifterlms_courses]

Advanced course display with grid layouts, category filtering, and slider functionality.

**Basic Usage:**
```
[reign_lifterlms_courses]
```

**Complete Parameters (from source code analysis):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `posts_per_page` | -1 | Any number | Number of courses to display (-1 for all) |
| `per_row` | 3 | 1-6 | Number of columns in grid layout |
| `enable_slider` | false | true, false | Enable slider/carousel functionality |
| `id` | - | Comma-separated IDs | Specific course IDs to display |
| `category` | - | Category slug | Filter by course category |

**Advanced Examples:**

```
// Complete course catalog with grid layout
[reign_lifterlms_courses posts_per_page="12" per_row="3"]

// Course slider for homepage
[reign_lifterlms_courses posts_per_page="6" per_row="3" enable_slider="true"]

// Specific category courses
[reign_lifterlms_courses category="web-development" per_row="4" posts_per_page="8"]

// Featured courses with specific IDs
[reign_lifterlms_courses id="123,456,789" per_row="3"]

// All courses in slider format
[reign_lifterlms_courses posts_per_page="-1" per_row="4" enable_slider="true"]
```

### [reign_lifterlms_instructors]

Professional instructor display with social media integration and responsive layouts.

**Basic Usage:**
```
[reign_lifterlms_instructors]
```

**Complete Parameters (from source code analysis):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_row` | 4 | 1-6 | Number of columns for instructor display |
| `total` | - | Any number | Limit number of instructors shown |
| `enable_slider` | false | true, false | Enable slider/carousel functionality |

**Advanced Examples:**

```
// Instructor directory with 4 columns
[reign_lifterlms_instructors per_row="4"]

// Limited instructor showcase
[reign_lifterlms_instructors per_row="3" total="6"]

// Instructor slider for homepage
[reign_lifterlms_instructors per_row="4" enable_slider="true"]

// Compact instructor display
[reign_lifterlms_instructors per_row="2" total="4"]
```

---

## Advanced Features

### Course Display Features
When using `[reign_lifterlms_courses]`:
- **Responsive Grid Layouts**: Automatic column adjustment for mobile
- **Category Filtering**: Display courses from specific categories
- **Slider Functionality**: Optional carousel with navigation controls
- **Exclude Current Course**: Automatically excludes current course on single course pages
- **Professional Styling**: Enhanced Reign theme integration

### Instructor Display Features
When using `[reign_lifterlms_instructors]`:
- **Social Media Integration**: Displays instructor social profiles from Yoast SEO
- **Contact Information**: Shows email, website, AIM, Yahoo IM, Jabber
- **Professional Avatars**: Enhanced instructor profile images
- **Course Relationship**: Shows courses taught by each instructor
- **Responsive Design**: Mobile-optimized instructor cards

---

## Widget Integration

The addon provides 7 custom widgets that complement the shortcodes:

### Course-Related Widgets

#### 1. Course Categories Widget
Display course category listings in sidebars:
- Hierarchical category display
- Course count per category
- Customizable styling

#### 2. Course Difficulties Widget
Show course difficulty levels:
- Beginner, Intermediate, Advanced filtering
- Visual difficulty indicators
- Course count per level

#### 3. Course Search Widget
LifterLMS-specific search functionality:
- Course title search
- Category filtering integration
- Advanced search options

#### 4. Course Listing Widget
Customizable course displays for sidebars:
- Featured courses display
- Recent courses listing
- Category-specific courses

#### 5. Course Overview Widget
Single course information display:
- Course details summary
- Enrollment information
- Progress indicators

### Membership & Student Widgets

#### 6. Membership Listing Widget
Display membership plans:
- Membership plan showcases
- Pricing information
- Feature comparisons

#### 7. Enrolled Students Widget
Student count and enrollment displays:
- Total enrolled students
- Recent enrollments
- Student avatars/profiles

---

## BuddyPress Integration Features

### Activity Stream Integration
Automatic activity logging for:
- **Course Enrollment**: When students enroll in courses
- **Course Completion**: When courses are completed
- **Lesson Completion**: Individual lesson progress
- **Quiz Activities**: Quiz participation and results (pass/fail)
- **Certificate Activities**: Certificate earning notifications
- **Achievement Activities**: Badge and achievement unlocks

### Profile Integration
Enhanced BuddyPress profiles with:
- **Courses Tab**: Dedicated learning section in user profiles
- **Activity Preferences**: Individual control over activity notifications
- **Progress Display**: Course progress visualization
- **Social Learning**: Learning achievements in social profiles

### Group Learning Features
- **Course-Group Linking**: Connect courses with BuddyPress groups
- **Auto-Enrollment**: Automatic group membership for course students
- **Group Activities**: Course-specific activity feeds within groups
- **Bulk Management**: Streamlined student enrollment processes

---

## Enhanced Dashboard Integration

### Student Dashboard Enhancement
The addon enhances the LifterLMS student dashboard with:

#### Dashboard Navigation Styles
- **Style 1**: Traditional dashboard with sidebar navigation
- **Style 2**: Modern tabbed interface with horizontal navigation

#### Dashboard Configuration Options
- **Dashboard Title**: Customizable dashboard title text
- **Items Per Row**: Configurable layout for courses, memberships, achievements
- **Display Elements**: Toggle visibility of various dashboard components

---

## Template System Integration

### Distraction-Free Learning Mode
Optional distraction-free layout for lessons:
- Removes site header and footer on lesson pages
- Minimal navigation for focused learning
- Clean, distraction-free interface
- Mobile-optimized layout

### Template Override System
Available templates for customization:
- Single course page templates
- Single lesson/quiz/assignment templates
- Course archive page templates
- Membership archive templates
- Student dashboard section templates

**Override Location:**
```
/wp-content/themes/reign-child/lifterlms/
```

---

## Advanced Usage Examples

### Learning Platform Homepage
```
<!-- Hero Section - Featured Courses -->
[reign_lifterlms_courses posts_per_page="8" per_row="4" enable_slider="true"]

<!-- Instructor Showcase -->
[reign_lifterlms_instructors per_row="4" total="8" enable_slider="true"]

<!-- Recent Courses -->
[reign_lifterlms_courses posts_per_page="6" per_row="3"]

<!-- Category-Specific Courses -->
[reign_lifterlms_courses category="web-development" posts_per_page="6" per_row="3"]
```

### Course Category Pages
```
<!-- Web Development Courses -->
[reign_lifterlms_courses category="web-development" posts_per_page="12" per_row="3"]

<!-- Design Courses -->
[reign_lifterlms_courses category="design" posts_per_page="12" per_row="3"]

<!-- Business Courses -->
[reign_lifterlms_courses category="business" posts_per_page="12" per_row="3"]
```

### Instructor Directory Page
```
<!-- All Instructors in Grid -->
[reign_lifterlms_instructors per_row="3"]

<!-- Top Instructors Slider -->
[reign_lifterlms_instructors per_row="4" total="12" enable_slider="true"]
```

### Landing Page with Slider
```
<!-- Course Spotlight Slider -->
[reign_lifterlms_courses posts_per_page="8" per_row="3" enable_slider="true"]

<!-- Meet Our Instructors -->
[reign_lifterlms_instructors per_row="4" enable_slider="true"]
```

### Sidebar Course Display
```
<!-- Featured Courses Widget Alternative -->
[reign_lifterlms_courses posts_per_page="3" per_row="1"]

<!-- Recent Courses -->
[reign_lifterlms_courses posts_per_page="5" per_row="1"]
```

---

## Review System Integration

### Enhanced Course Reviews
The addon enhances LifterLMS reviews with:
- **Interactive Star Ratings**: AJAX-powered rating submission
- **Review Analytics**: Detailed rating breakdowns (1-5 star distribution)
- **Average Rating Display**: Calculated average ratings with review counts
- **Social Integration**: BuddyPress activity stream integration for reviews

---

## Performance Optimization

### Best Practices
```
// Use reasonable course counts for better performance
[reign_lifterlms_courses posts_per_page="12"]

// Enable slider for better UX with many courses
[reign_lifterlms_courses posts_per_page="6" enable_slider="true"]

// Use category filtering to reduce queries
[reign_lifterlms_courses category="featured" posts_per_page="8"]
```

### Mobile Optimization
- Responsive grid layouts that adjust to screen size
- Touch-friendly slider controls
- Optimized loading for mobile devices
- Progressive image loading for course thumbnails

---

## Troubleshooting

### Shortcode Not Displaying
1. Verify plugin is activated (v2.4.1+)
2. Check LifterLMS is properly configured
3. Ensure courses exist and are published
4. Clear all caches (page, object, plugin)

### BuddyPress Features Not Working
1. Verify BuddyPress is active and configured
2. Check BuddyPress components are enabled (Activity, Groups)
3. Ensure users have appropriate permissions
4. Test activity logging with different user roles

### Layout Issues
1. Check theme compatibility with grid layouts
2. Verify CSS conflicts with existing styles
3. Test with default WordPress theme
4. Clear browser and theme caches

### Slider Not Working
1. Ensure `enable_slider="true"` is set correctly
2. Check JavaScript conflicts with other plugins
3. Verify jQuery is loaded properly
4. Test with minimal plugin configuration

---

## LifterLMS Core Shortcodes

These shortcodes come from LifterLMS plugin itself and are enhanced by Reign styling:

### Core LifterLMS Shortcodes
- `[lifterlms_courses]` - Basic course listing (LifterLMS core)
- `[lifterlms_memberships]` - Membership plans (LifterLMS core)
- `[lifterlms_my_account]` - Student dashboard (LifterLMS core)
- `[lifterlms_course_syllabus]` - Course curriculum (LifterLMS core)
- `[lifterlms_course_progress]` - Progress tracking (LifterLMS core)

These receive enhanced Reign theme styling when the addon is active.

---

*Comprehensive shortcodes reference based on complete analysis of Reign LifterLMS Addon v2.4.1 source code*

---

### 2. Single Course Information

**Display specific course details:**
```
[lifterlms_course_info id="123"]
```

**What it shows:**
- Course title and description
- Instructor information
- Price and enrollment button
- Duration and difficulty
- Student count and ratings

**Parameters:**

| Parameter | Required | Example | Purpose |
|-----------|----------|---------|----------|
| `id` | Yes | "123" | Which course |
| `show_price` | No | "yes" | Display price |
| `show_instructor` | No | "yes" | Show instructor |
| `show_progress` | No | "yes" | User progress (if enrolled) |
| `show_syllabus` | No | "yes" | Course outline |

---

### 3. Course Categories

**List all course categories:**
```
[lifterlms_course_categories]
```

**With options:**
```
[lifterlms_course_categories 
    show_count="yes"
    hide_empty="yes"
    orderby="name"]
```

**Parameters:**

| Parameter | Options | Default | Purpose |
|-----------|---------|---------|----------|
| `show_count` | yes, no | yes | Course count per category |
| `hide_empty` | yes, no | no | Hide categories with no courses |
| `orderby` | name, count, id | name | Sort method |
| `order` | ASC, DESC | ASC | Sort direction |

---

## Student Dashboard Shortcodes

### 4. My Account Dashboard

**Complete student dashboard:**
```
[lifterlms_my_account]
```

**What it includes:**
- Course progress overview
- Enrolled courses list
- Achievements and certificates
- Order history
- Account settings
- Membership information

---

### 5. Student Courses

**List user's enrolled courses:**
```
[lifterlms_student_dashboard]
```

**Filter by status:**
```
[lifterlms_student_dashboard status="enrolled"]
```

**Status options:**
- `enrolled` - Currently enrolled
- `completed` - Finished courses
- `expired` - Expired access

---

### 6. Course Progress

**Show progress for specific course:**
```
[lifterlms_course_progress course_id="123"]
```

**Advanced usage:**
```
[lifterlms_course_progress 
    course_id="123"
    user_id="456"
    show_percentage="yes"]
```

---

## Assessment & Achievement Shortcodes

### 7. Course Syllabus

**Display course outline:**
```
[lifterlms_course_syllabus id="123"]
```

**What it shows:**
- All lessons organized by sections
- Quizzes and assignments
- Completion status
- Time estimates

---

### 8. Achievements

**Show user achievements:**
```
[lifterlms_achievements]
```

**For specific user:**
```
[lifterlms_achievements user_id="456"]
```

---

### 9. Certificates

**Display earned certificates:**
```
[lifterlms_certificates]
```

**Specific certificate:**
```
[lifterlms_certificate id="789"]
```

---

## Instructor Shortcodes

### 10. Instructor Profile

**Display instructor information:**
```
[lifterlms_instructor id="789"]
```

**What it shows:**
- Instructor bio and photo
- Courses they teach
- Ratings and reviews
- Social links
- Qualifications

---

### 11. Instructor Courses

**List courses by specific instructor:**
```
[lifterlms_instructor_courses instructor_id="789"]
```

**With layout options:**
```
[lifterlms_instructor_courses 
    instructor_id="789"
    columns="2"
    show_price="yes"]
```

---

## Membership Shortcodes

### 12. Membership Plans

**Display membership options:**
```
[lifterlms_memberships]
```

**With filtering:**
```
[lifterlms_memberships 
    featured="yes"
    orderby="price"
    order="ASC"]
```

---

### 13. Membership Information

**Show membership details:**
```
[lifterlms_membership_info id="456"]
```

**What it includes:**
- Membership features
- Included courses
- Pricing information
- Access duration

---

## Registration & Checkout Shortcodes

### 14. Registration Form

**Student registration:**
```
[lifterlms_registration]
```

**With redirect:**
```
[lifterlms_registration redirect="/dashboard/"]
```

---

### 15. Login Form

**Student login:**
```
[lifterlms_login]
```

**With custom redirect:**
```
[lifterlms_login redirect="/my-courses/"]
```

---

### 16. Checkout Form

**Course purchase form:**
```
[lifterlms_checkout]
```

**Note:** This shortcode is typically used on the dedicated checkout page.

---

## Search & Filter Shortcodes

### 17. Course Search

**Search form for courses:**
```
[lifterlms_search_courses]
```

**With filters:**
```
[lifterlms_search_courses 
    show_categories="yes"
    show_difficulty="yes"
    show_instructors="yes"]
```

---

### 18. Featured Courses

**Highlight specific courses:**
```
[lifterlms_featured_courses]
```

**Custom selection:**
```
[lifterlms_featured_courses course_ids="123,456,789"]
```

---

## Pricing & Access Shortcodes

### 19. Course Pricing

**Display course pricing table:**
```
[lifterlms_pricing course_id="123"]
```

**What it shows:**
- One-time purchase options
- Access plan details
- Payment plan options
- Membership alternatives

---

### 20. Access Plans

**Show all access options:**
```
[lifterlms_access_plans course_id="123"]
```

---

## Conditional Shortcodes

### 21. Show If Enrolled

**Content only for enrolled students:**
```
[lifterlms_if_enrolled course_id="123"]
    Welcome to the course! Here's your exclusive content.
[/lifterlms_if_enrolled]
```

---

### 22. Show If Completed

**Content for course graduates:**
```
[lifterlms_if_completed course_id="123"]
    Congratulations! You've completed the course.
    <a href="/advanced-course">Try our advanced course next!</a>
[/lifterlms_if_completed]
```

---

### 23. Show If Not Enrolled

**Promotional content:**
```
[lifterlms_if_not_enrolled course_id="123"]
    <div class="enrollment-cta">
        <h3>Ready to start learning?</h3>
        <p>Join thousands of students in this course.</p>
        [lifterlms_course_button course_id="123"]
    </div>
[/lifterlms_if_not_enrolled]
```

---

## Interactive Shortcodes

### 24. Course Button

**Enrollment/access button:**
```
[lifterlms_course_button course_id="123"]
```

**Custom text:**
```
[lifterlms_course_button course_id="123" text="Start Learning Now!"]
```

---

### 25. Course Reviews

**Display course ratings:**
```
[lifterlms_course_reviews course_id="123"]
```

**Review form:**
```
[lifterlms_course_review_form course_id="123"]
```

---

## Notification Shortcodes

### 26. Course Notices

**Important course announcements:**
```
[lifterlms_course_notices course_id="123"]
```

---

### 27. User Notifications

**Personal notifications:**
```
[lifterlms_notifications]
```

---

## Page Layout Examples

### Homepage Layout

```html
<!-- Hero Section -->
<h1>Transform Your Career with Online Learning</h1>
[lifterlms_search_courses]

<!-- Featured Courses -->
<h2>Featured Courses</h2>
[lifterlms_featured_courses per_page="6" columns="3"]

<!-- Course Categories -->
<h2>Browse by Category</h2>
[lifterlms_course_categories show_count="yes"]

<!-- Latest Courses -->
<h2>New Courses</h2>
[lifterlms_courses orderby="date" per_page="6"]

<!-- Call to Action -->
[lifterlms_if_not_logged_in]
    <div class="cta-section">
        <h3>Ready to Get Started?</h3>
        <a href="/register" class="button">Create Free Account</a>
    </div>
[/lifterlms_if_not_logged_in]
```

### Course Catalog Page

```html
<h1>Course Catalog</h1>

<!-- Search and Filters -->
[lifterlms_search_courses show_categories="yes" show_difficulty="yes"]

<!-- Course Grid -->
[lifterlms_courses per_page="12" columns="3"]
```

### Student Dashboard

```html
<h1>My Learning Dashboard</h1>

<!-- Main Dashboard -->
[lifterlms_my_account]

<!-- Quick Course Access -->
<h2>Continue Learning</h2>
[lifterlms_student_dashboard status="enrolled"]

<!-- Achievements -->
<h2>My Achievements</h2>
[lifterlms_achievements]

<!-- Certificates -->
<h2>My Certificates</h2>
[lifterlms_certificates]
```

### Individual Course Page

```html
<!-- Course Header -->
[lifterlms_course_info id="123"]

<!-- Enrollment Check -->
[lifterlms_if_not_enrolled course_id="123"]
    <h2>Course Curriculum</h2>
    [lifterlms_course_syllabus id="123"]
    
    <h2>What You'll Learn</h2>
    <!-- Course benefits and outcomes -->
    
    <h2>Choose Your Access Plan</h2>
    [lifterlms_access_plans course_id="123"]
[/lifterlms_if_not_enrolled]

[lifterlms_if_enrolled course_id="123"]
    <h2>Your Progress</h2>
    [lifterlms_course_progress course_id="123"]
    
    <h2>Course Content</h2>
    [lifterlms_course_syllabus id="123"]
[/lifterlms_if_enrolled]

<!-- Reviews -->
<h2>Student Reviews</h2>
[lifterlms_course_reviews course_id="123"]

<!-- Instructor -->
<h2>Your Instructor</h2>
[lifterlms_instructor id="789"]
```

### Instructor Page

```html
<h1>Meet Your Instructor</h1>

<!-- Instructor Profile -->
[lifterlms_instructor id="789"]

<!-- Their Courses -->
<h2>Courses by This Instructor</h2>
[lifterlms_instructor_courses instructor_id="789" columns="2"]

<!-- Student Testimonials -->
<h2>What Students Say</h2>
<!-- Custom testimonials -->
```

### Membership Page

```html
<h1>Membership Plans</h1>

<!-- Membership Options -->
[lifterlms_memberships]

<!-- Benefits Comparison -->
<h2>Compare Plans</h2>
<!-- Custom comparison table -->

<!-- FAQ -->
<h2>Frequently Asked Questions</h2>
<!-- Custom FAQ content -->
```

---

## Styling Shortcodes

### CSS Classes for Customization

**All shortcodes use these base classes:**

```css
.llms-wrapper { /* Main container */ }
.llms-course-list { /* Course grid container */ }
.llms-course { /* Individual course card */ }
.llms-progress { /* Progress indicators */ }
.llms-button { /* Action buttons */ }
.llms-form { /* Form elements */ }
```

### Custom Styling Examples

```css
/* Style course cards */
.llms-course {
    border: 1px solid #e0e0e0;
    border-radius: 12px;
    padding: 24px;
    transition: all 0.3s ease;
    background: white;
}

.llms-course:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
    border-color: #your-brand-color;
}

/* Progress bar styling */
.llms-progress {
    background: #f8f9fa;
    border-radius: 25px;
    overflow: hidden;
    height: 16px;
}

.llms-progress .llms-progress-bar {
    background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
    height: 100%;
    border-radius: 25px;
    transition: width 0.6s ease;
}

/* Button styling */
.llms-button-primary {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 16px 32px;
    border-radius: 8px;
    border: none;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    transition: all 0.3s ease;
}

.llms-button-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
}

/* Course grid responsive */
.llms-course-list {
    display: grid;
    gap: 24px;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

@media (max-width: 768px) {
    .llms-course-list {
        grid-template-columns: 1fr;
        gap: 16px;
    }
}
```

---

## Troubleshooting Shortcodes

### Common Issues

**"Shortcode not displaying"**
- Check spelling exactly
- Verify course/user IDs exist
- Ensure LifterLMS is active
- Clear cache

**"Layout looks broken"**
- Check CSS conflicts
- Verify column numbers
- Test with default theme
- Clear browser cache

**"No courses showing"**
- Check course publication status
- Verify user permissions
- Confirm category/tag exists
- Test with simpler parameters

**"User-specific content not working"**
- Ensure user is logged in
- Check user enrollment status
- Verify user ID format
- Test with current user

---

## Performance Tips

### Optimize Shortcode Performance

```
// Use specific parameters to limit results
[lifterlms_courses per_page="6"] // Instead of showing all

// Cache-friendly: avoid user-specific shortcodes on cached pages
// Use AJAX loading for dynamic content

// Minimize nested shortcodes
// Use specific IDs when possible
```

---

## Pro Tips

### Advanced Usage

1. **Combine shortcodes** for rich page layouts
2. **Use conditional shortcodes** for personalization
3. **Test on staging** before going live
4. **Document custom implementations** for your team
5. **Use widgets** for sidebar content

### Mobile Optimization

```
// Use fewer columns on mobile
[lifterlms_courses columns="3"] // Automatically adjusts to 1 on mobile

// Simplify content for mobile
[lifterlms_if_mobile]
    [lifterlms_courses per_page="4" columns="1"]
[/lifterlms_if_mobile]

[lifterlms_if_desktop]
    [lifterlms_courses per_page="12" columns="3"]
[/lifterlms_if_desktop]
```

---

## Quick Copy Reference

### Most Used Shortcodes

```
// Course catalog
[lifterlms_courses]

// Student dashboard
[lifterlms_my_account]

// Course information
[lifterlms_course_info id="123"]

// Course search
[lifterlms_search_courses]

// Categories
[lifterlms_course_categories]

// Student courses
[lifterlms_student_dashboard]

// Course button
[lifterlms_course_button course_id="123"]

// Progress tracking
[lifterlms_course_progress course_id="123"]

// Instructor profile
[lifterlms_instructor id="789"]

// Login form
[lifterlms_login]
```

---

**Need Help with Shortcodes?**  
📧 Email: support@wbcomdesigns.com  
📚 More examples: docs.wbcomdesigns.com  
💬 Forum: wbcomdesigns.com/support  
🎥 Video tutorials in member area