# Reign LifterLMS Addon - Shortcodes Reference

## What You'll Learn
This guide provides a complete reference for all shortcodes available in the Reign LifterLMS addon. Learn how to display courses, student progress, and learning content anywhere on your site!

## Quick Overview  
**Usage Level:** Easy (just copy and paste!)  
**Where to use:** Pages, posts, widgets, anywhere!  
**Pro tip:** Test shortcodes on a draft page first

---

## Essential Course Shortcodes

### 1. Course Catalog

**Display all courses in a grid:**
```
[lifterlms_courses]
```

**With parameters:**
```
[lifterlms_courses 
    per_page="12" 
    columns="3" 
    orderby="date" 
    order="DESC"
    category="web-development"]
```

**Parameters explained:**

| Parameter | Options | Default | What It Does |
|-----------|---------|---------|---------------|
| `per_page` | Any number | 12 | Courses per page |
| `columns` | 1, 2, 3, 4, 6 | 3 | Grid columns |
| `orderby` | date, title, menu_order, rand | date | Sort method |
| `order` | ASC, DESC | DESC | Sort direction |
| `category` | Category slug | All | Filter by category |
| `tag` | Tag slug | All | Filter by tag |
| `difficulty` | beginner, intermediate, advanced | All | Filter by level |
| `featured` | yes, no | no | Show only featured |

**Examples:**

```
// Show 6 newest courses in 2 columns
[lifterlms_courses per_page="6" columns="2" orderby="date"]

// Beginner courses only
[lifterlms_courses difficulty="beginner" per_page="8"]

// Featured courses for homepage
[lifterlms_courses featured="yes" per_page="4"]
```

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