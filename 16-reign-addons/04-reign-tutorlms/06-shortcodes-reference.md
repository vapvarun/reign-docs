# Reign TutorLMS Addon - Shortcodes Reference

## What You'll Learn
This guide provides a complete reference for all shortcodes available in the Reign TutorLMS addon. Learn how to display courses, student progress, and learning content anywhere on your site!

## Quick Overview
**Usage Level:** Easy (just copy and paste!)
**Where to use:** Pages, posts, widgets, anywhere!
**Pro tip:** Test shortcodes on a draft page first

---

## Essential Course Shortcodes

### 1. Course Grid Display

**Display all courses in a grid:**
```
[tutor_course]
```

**With parameters:**
```
[tutor_course
    course_per_page="12"
    columns="3"
    order="DESC"
    orderby="date"
    category="web-development"]
```

**Parameters explained:**

| Parameter | Options | Default | What It Does |
|-----------|---------|---------|--------------|
| `course_per_page` | Any number | 12 | Courses per page |
| `columns` | 1, 2, 3, 4, 6 | 3 | Grid columns |
| `order` | ASC, DESC | DESC | Sort direction |
| `orderby` | date, title, menu_order, rand | date | Sort method |
| `category` | Category slug | All | Filter by category |
| `tag` | Tag slug | All | Filter by tag |
| `level` | beginner, intermediate, advanced | All | Filter by level |
| `price` | free, paid | All | Filter by price type |

**Examples:**

```
// Show 6 newest courses in 2 columns
[tutor_course course_per_page="6" columns="2" orderby="date"]

// Beginner courses only
[tutor_course level="beginner" course_per_page="8"]

// Free courses for homepage
[tutor_course price="free" course_per_page="4"]

// Specific category courses
[tutor_course category="programming" columns="3"]
```

---

### 2. Featured Courses

**Display featured courses:**
```
[tutor_course featured="true"]
```

**With custom styling:**
```
[tutor_course
    featured="true"
    columns="3"
    course_per_page="6"
    show_thumbnail="true"
    show_price="true"]
```

**What it shows:**
- Course thumbnail
- Course title and excerpt
- Instructor information
- Price and enrollment button
- Rating and student count

---

### 3. Course Categories

**List all course categories:**
```
[tutor_course_categories]
```

**With options:**
```
[tutor_course_categories
    show_count="yes"
    hide_empty="yes"
    orderby="name"
    order="ASC"]
```

**Parameters:**

| Parameter | Options | Default | Purpose |
|-----------|---------|---------|----------|
| `show_count` | yes, no | yes | Course count per category |
| `hide_empty` | yes, no | no | Hide categories with no courses |
| `orderby` | name, count, id | name | Sort method |
| `order` | ASC, DESC | ASC | Sort direction |
| `include` | Category IDs | All | Specific categories only |
| `exclude` | Category IDs | None | Exclude specific categories |

---

### 4. Course Search

**Search form for courses:**
```
[tutor_course_search]
```

**Advanced search with filters:**
```
[tutor_course_search
    show_filter="yes"
    show_categories="yes"
    show_levels="yes"
    show_instructors="yes"
    show_price_filter="yes"]
```

**Search features:**
- Text search by course title
- Category filtering
- Difficulty level filtering
- Price range filtering
- Instructor filtering
- Real-time search results

---

## Student Dashboard Shortcodes

### 5. Student Dashboard

**Complete student dashboard:**
```
[tutor_dashboard]
```

**What it includes:**
- Dashboard overview
- Enrolled courses
- Course progress
- Quiz attempts
- Assignments
- Wishlist
- Purchase history
- Profile settings

### 6. My Courses

**List student's enrolled courses:**
```
[tutor_student_dashboard_my_courses]
```

**Filter by status:**
```
[tutor_student_dashboard_my_courses status="active"]
```

**Status options:**
- `active` - Currently enrolled
- `completed` - Finished courses
- `expired` - Expired access

### 7. Course Progress

**Show progress for specific course:**
```
[tutor_course_progress course_id="123"]
```

**Advanced usage:**
```
[tutor_course_progress
    course_id="123"
    user_id="456"
    show_percentage="yes"
    show_completion_date="yes"]
```

### 8. Quiz Attempts

**Show student's quiz attempts:**
```
[tutor_student_dashboard_quiz_attempts]
```

**For specific course:**
```
[tutor_student_dashboard_quiz_attempts course_id="123"]
```

---

## Instructor Dashboard Shortcodes

### 9. Instructor Dashboard

**Complete instructor dashboard:**
```
[tutor_instructor_dashboard]
```

**Dashboard sections:**
- Course management
- Student progress
- Earnings overview
- Analytics
- Course creation tools

### 10. Instructor Courses

**List instructor's courses:**
```
[tutor_instructor_dashboard_courses]
```

**With filters:**
```
[tutor_instructor_dashboard_courses
    status="published"
    orderby="date"
    order="DESC"]
```

### 11. Create Course

**Course creation form:**
```
[tutor_instructor_dashboard_create_course]
```

**Frontend course builder features:**
- Course details form
- Curriculum builder
- Lesson/quiz creation
- Media upload
- Course preview

### 12. Earnings Overview

**Instructor earnings display:**
```
[tutor_instructor_dashboard_earnings]
```

**What it shows:**
- Total earnings
- Current month earnings
- Pending withdrawals
- Course-wise revenue
- Payment history

---

## Single Course Content Shortcodes

### 13. Course Info

**Display specific course details:**
```
[tutor_course_info course_id="123"]
```

**Parameters:**

| Parameter | Required | Example | Purpose |
|-----------|----------|---------|----------|
| `course_id` | Yes | "123" | Which course |
| `show_instructor` | No | "yes" | Show instructor info |
| `show_rating` | No | "yes" | Display rating |
| `show_students` | No | "yes" | Student count |
| `show_curriculum` | No | "yes" | Course outline |

### 14. Course Curriculum

**Display course lessons and topics:**
```
[tutor_course_curriculum course_id="123"]
```

**What it shows:**
- Course topics/sections
- Lessons under each topic
- Quizzes and assignments
- Lesson duration
- Completion status (if enrolled)

### 15. Course Instructor

**Show instructor information:**
```
[tutor_course_instructor course_id="123"]
```

**Instructor details displayed:**
- Instructor photo
- Name and bio
- Social links
- Other courses by instructor
- Ratings and reviews

### 16. Course Reviews

**Display course reviews:**
```
[tutor_course_reviews course_id="123"]
```

**Review features:**
- Star ratings
- Student comments
- Review filtering
- Average rating display

---

## Enrollment & Purchase Shortcodes

### 17. Course Enrollment Button

**Enrollment/purchase button:**
```
[tutor_course_enroll_btn course_id="123"]
```

**Custom button text:**
```
[tutor_course_enroll_btn
    course_id="123"
    button_text="Start Learning Now!"
    button_class="custom-enroll-btn"]
```

### 18. Course Price

**Display course pricing:**
```
[tutor_course_price course_id="123"]
```

**What it shows:**
- Current price
- Original price (if discounted)
- Discount percentage
- Sale badge
- Currency symbol

### 19. Add to Cart

**WooCommerce integration:**
```
[tutor_course_add_to_cart course_id="123"]
```

**For WooCommerce-based course sales:**
- Add to cart functionality
- Quantity selection
- Variable pricing options

---

## Assessment & Quiz Shortcodes

### 20. Quiz List

**Display course quizzes:**
```
[tutor_course_quiz course_id="123"]
```

**Quiz information shown:**
- Quiz titles
- Question count
- Time limit
- Passing grade
- Attempt status

### 21. Quiz Results

**Show quiz attempt results:**
```
[tutor_quiz_result quiz_id="456" attempt_id="789"]
```

**Results display:**
- Score percentage
- Correct/incorrect answers
- Time taken
- Pass/fail status
- Review option

### 22. Assignment List

**Display course assignments:**
```
[tutor_course_assignments course_id="123"]
```

**Assignment details:**
- Assignment titles
- Due dates
- Submission status
- Grades received

---

## Wishlist & Favorites Shortcodes

### 23. Course Wishlist

**Display student's wishlist:**
```
[tutor_student_dashboard_wishlist]
```

### 24. Add to Wishlist Button

**Wishlist toggle button:**
```
[tutor_course_wishlist_btn course_id="123"]
```

**Button states:**
- Add to wishlist (if not in wishlist)
- Remove from wishlist (if in wishlist)
- Login required message (for guests)

---

## Social Learning Shortcodes

### 25. Course Announcements

**Display course announcements:**
```
[tutor_course_announcements course_id="123"]
```

### 26. Q&A Section

**Course Q&A display:**
```
[tutor_course_qna course_id="123"]
```

**Q&A features:**
- Ask questions
- View all questions
- Instructor answers
- Upvote questions
- Search functionality

### 27. Student List

**Show enrolled students:**
```
[tutor_course_students course_id="123"]
```

**Student information:**
- Student avatars
- Names (if privacy allows)
- Enrollment dates
- Progress indicators

---

## Advanced Shortcodes

### 28. Course Filter

**Advanced course filtering:**
```
[tutor_course_filter]
```

**Filter options:**
- Categories
- Difficulty levels
- Price ranges
- Ratings
- Instructors
- Duration

### 29. Live Classes

**Zoom meeting integration:**
```
[tutor_zoom_meetings course_id="123"]
```

**Meeting information:**
- Scheduled meetings
- Join meeting links
- Recording access
- Meeting history

### 30. Certificates

**Display earned certificates:**
```
[tutor_student_dashboard_certificates]
```

**For specific certificate:**
```
[tutor_certificate certificate_id="789"]
```

---

## Layout & Display Shortcodes

### 31. Course Carousel

**Rotating course display:**
```
[tutor_course_carousel
    course_per_page="6"
    autoplay="true"
    dots="true"
    arrows="true"]
```

### 32. Course Tabs

**Tabbed course display:**
```
[tutor_course_tabs]
```

**Tab categories:**
- Featured courses
- New courses
- Popular courses
- Free courses

### 33. Instructor Grid

**Display instructors:**
```
[tutor_instructors
    instructors_per_page="8"
    columns="4"
    order="DESC"]
```

---

## Conditional Display Shortcodes

### 34. Show If Enrolled

**Content only for enrolled students:**
```
[tutor_enrolled_only course_id="123"]
    Welcome to the course! Here's your exclusive content.
[/tutor_enrolled_only]
```

### 35. Show If Completed

**Content for course graduates:**
```
[tutor_completed_only course_id="123"]
    Congratulations! You've completed the course.
    <a href="/advanced-course">Try our advanced course next!</a>
[/tutor_completed_only]
```

### 36. Show If Not Enrolled

**Promotional content:**
```
[tutor_not_enrolled course_id="123"]
    <div class="enrollment-cta">
        <h3>Ready to start learning?</h3>
        <p>Join thousands of students in this course.</p>
        [tutor_course_enroll_btn course_id="123"]
    </div>
[/tutor_not_enrolled]
```

---

## Page Layout Examples

### Homepage Layout

```html
<!-- Hero Section -->
<h1>Master New Skills with Expert-Led Courses</h1>
[tutor_course_search show_filter="yes"]

<!-- Featured Courses -->
<h2>Featured Courses</h2>
[tutor_course featured="true" course_per_page="6" columns="3"]

<!-- Course Categories -->
<h2>Browse by Category</h2>
[tutor_course_categories show_count="yes" hide_empty="yes"]

<!-- Latest Courses -->
<h2>New Courses</h2>
[tutor_course orderby="date" course_per_page="6" columns="3"]

<!-- Top Instructors -->
<h2>Meet Our Instructors</h2>
[tutor_instructors instructors_per_page="4" columns="4"]

<!-- Call to Action -->
[tutor_not_logged_in]
    <div class="cta-section">
        <h3>Ready to Get Started?</h3>
        <a href="/register" class="button">Create Free Account</a>
    </div>
[/tutor_not_logged_in]
```

### Course Catalog Page

```html
<h1>Course Catalog</h1>

<!-- Search and Filters -->
[tutor_course_search show_filter="yes" show_categories="yes" show_levels="yes"]

<!-- Course Grid -->
[tutor_course course_per_page="12" columns="3"]
```

### Student Dashboard

```html
<h1>My Learning Dashboard</h1>

<!-- Main Dashboard -->
[tutor_dashboard]

<!-- Quick Course Access -->
<h2>Continue Learning</h2>
[tutor_student_dashboard_my_courses status="active"]

<!-- Recent Quiz Results -->
<h2>Recent Quiz Results</h2>
[tutor_student_dashboard_quiz_attempts]

<!-- Wishlist -->
<h2>My Wishlist</h2>
[tutor_student_dashboard_wishlist]

<!-- Certificates -->
<h2>My Certificates</h2>
[tutor_student_dashboard_certificates]
```

### Individual Course Page

```html
<!-- Course Header -->
[tutor_course_info course_id="123"]

<!-- Enrollment Check -->
[tutor_not_enrolled course_id="123"]
    <h2>Course Curriculum</h2>
    [tutor_course_curriculum course_id="123"]

    <h2>What You'll Learn</h2>
    <!-- Course learning outcomes -->

    <h2>Enroll Now</h2>
    [tutor_course_enroll_btn course_id="123"]
[/tutor_not_enrolled]

[tutor_enrolled_only course_id="123"]
    <h2>Your Progress</h2>
    [tutor_course_progress course_id="123"]

    <h2>Course Content</h2>
    [tutor_course_curriculum course_id="123"]

    <h2>Q&A</h2>
    [tutor_course_qna course_id="123"]
[/tutor_enrolled_only]

<!-- Reviews -->
<h2>Student Reviews</h2>
[tutor_course_reviews course_id="123"]

<!-- Instructor -->
<h2>Your Instructor</h2>
[tutor_course_instructor course_id="123"]

<!-- Announcements -->
<h2>Course Announcements</h2>
[tutor_course_announcements course_id="123"]
```

### Instructor Page

```html
<h1>Meet Your Instructor</h1>

<!-- Instructor Profile -->
[tutor_course_instructor instructor_id="789"]

<!-- Their Courses -->
<h2>Courses by This Instructor</h2>
[tutor_instructor_dashboard_courses instructor_id="789" columns="3"]

<!-- Instructor Dashboard (for logged-in instructor) -->
[tutor_instructor_only]
    <h2>Instructor Dashboard</h2>
    [tutor_instructor_dashboard]
[/tutor_instructor_only]
```

---

## Styling Shortcodes

### CSS Classes for Customization

**All shortcodes use these base classes:**

```css
.tutor-wrap { /* Main container */ }
.tutor-course-grid { /* Course grid container */ }
.tutor-course-card { /* Individual course card */ }
.tutor-progress { /* Progress indicators */ }
.tutor-btn { /* Action buttons */ }
.tutor-form { /* Form elements */ }
.tutor-dashboard { /* Dashboard sections */ }
```

### Custom Styling Examples

```css
/* Style course cards */
.tutor-course-card {
    border: 1px solid #e0e0e0;
    border-radius: 12px;
    padding: 24px;
    transition: all 0.3s ease;
    background: white;
}

.tutor-course-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
    border-color: #your-brand-color;
}

/* Progress bar styling */
.tutor-progress {
    background: #f8f9fa;
    border-radius: 25px;
    overflow: hidden;
    height: 16px;
}

.tutor-progress .tutor-progress-bar {
    background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
    height: 100%;
    border-radius: 25px;
    transition: width 0.6s ease;
}

/* Button styling */
.tutor-btn-primary {
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

.tutor-btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
}

/* Course grid responsive */
.tutor-course-grid {
    display: grid;
    gap: 24px;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

@media (max-width: 768px) {
    .tutor-course-grid {
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
- Ensure TutorLMS is active
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
[tutor_course course_per_page="6"] // Instead of showing all

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
[tutor_course columns="3"] // Automatically adjusts to 1 on mobile

// Simplify content for mobile
[tutor_mobile_only]
    [tutor_course course_per_page="4" columns="1"]
[/tutor_mobile_only]

[tutor_desktop_only]
    [tutor_course course_per_page="12" columns="3"]
[/tutor_desktop_only]
```

---

## Quick Copy Reference

### Most Used Shortcodes

```
// Course catalog
[tutor_course]

// Student dashboard
[tutor_dashboard]

// Course information
[tutor_course_info course_id="123"]

// Course search
[tutor_course_search]

// Categories
[tutor_course_categories]

// Student courses
[tutor_student_dashboard_my_courses]

// Enrollment button
[tutor_course_enroll_btn course_id="123"]

// Progress tracking
[tutor_course_progress course_id="123"]

// Instructor dashboard
[tutor_instructor_dashboard]

// Course curriculum
[tutor_course_curriculum course_id="123"]
```

---

**Need Help with Shortcodes?**
📧 Email: support@wbcomdesigns.com
📚 More examples: docs.wbcomdesigns.com
💬 Forum: wbcomdesigns.com/support
🎥 Video tutorials in member area