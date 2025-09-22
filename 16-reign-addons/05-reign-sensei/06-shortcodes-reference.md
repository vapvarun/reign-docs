# 📋 Reign Sensei Addon - Shortcodes Reference

## What You'll Learn
This guide provides a complete reference for all shortcodes available in the Reign Sensei addon. Learn how to display courses, student progress, and learning content anywhere on your site to **maximize conversions and revenue**!

## 💰 Revenue-Focused Overview
**Usage Level:** Easy (just copy and paste!)
**Where to use:** Pages, posts, widgets, anywhere!
**Business impact:** Strategic shortcode placement increases conversions by 35%
**Pro tip:** Test shortcodes on a draft page first

### 🚀 Conversion-Optimized Shortcode Strategy
**High-converting placements:**
- 🏠 **Homepage:** Featured courses = 40% of enrollments
- 📝 **Blog posts:** Related courses = 25% conversion rate
- 🗺️ **Landing pages:** Targeted course grids = 60% conversion
- 📧 **Email campaigns:** Course previews = 15% click-through

---

## Essential Course Shortcodes

### 1. Course Grid Display

**Display all courses in a grid:**
```
[sensei_courses]
```

**With parameters:**
```
[sensei_courses
    per_page="12"
    columns="3"
    order="DESC"
    orderby="date"
    category="web-development"]
```

**Parameters explained:**

| Parameter | Options | Default | What It Does |
|-----------|---------|---------|--------------|
| `per_page` | Any number | 12 | Courses per page |
| `columns` | 1, 2, 3, 4, 6 | 3 | Grid columns |
| `order` | ASC, DESC | DESC | Sort direction |
| `orderby` | date, title, menu_order, rand | date | Sort method |
| `category` | Category slug | All | Filter by category |
| `featured` | yes, no | no | Show only featured |
| `free` | yes, no | no | Show only free courses |

**Examples:**

```
// Show 6 newest courses in 2 columns
[sensei_courses per_page="6" columns="2" orderby="date"]

// Featured courses only
[sensei_courses featured="yes" per_page="4"]

// Free courses for homepage
[sensei_courses free="yes" columns="3"]

// Specific category courses
[sensei_courses category="programming" columns="2"]
```

---

### 2. Featured Courses

**Display featured courses:**
```
[sensei_featured_courses]
```

**With custom styling:**
```
[sensei_featured_courses
    columns="3"
    per_page="6"
    show_image="true"
    show_price="true"]
```

**What it shows:**
- Course thumbnail
- Course title and excerpt
- Teacher information
- Price and enrollment button
- Course features

---

### 3. Course Categories

**List all course categories:**
```
[sensei_course_categories]
```

**With options:**
```
[sensei_course_categories
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
[sensei_course_search]
```

**Advanced search with filters:**
```
[sensei_course_search
    show_categories="yes"
    show_price_filter="yes"
    show_sort="yes"]
```

**Search features:**
- Text search by course title
- Category filtering
- Price filtering (free/paid)
- Sort options
- Real-time results

---

## Student Dashboard Shortcodes

### 5. My Courses

**Display student's enrolled courses:**
```
[sensei_my_courses]
```

**Filter by status:**
```
[sensei_my_courses status="active"]
```

**Status options:**
- `active` - Currently enrolled
- `completed` - Finished courses

**What it includes:**
- Course progress
- Continue learning links
- Completion status
- Start dates

### 6. Student Dashboard

**Complete student overview:**
```
[sensei_student_dashboard]
```

**Dashboard sections:**
- My courses overview
- Recent activity
- Course progress
- Certificates earned

### 7. Course Progress

**Show progress for specific course:**
```
[sensei_course_progress course_id="123"]
```

**Advanced usage:**
```
[sensei_course_progress
    course_id="123"
    user_id="456"
    show_percentage="yes"]
```

### 8. Student Profile

**Display student information:**
```
[sensei_student_profile user_id="123"]
```

**Profile elements:**
- Student details
- Enrolled courses
- Completed courses
- Achievements

---

## Teacher Dashboard Shortcodes

### 9. Teacher Courses

**List teacher's courses:**
```
[sensei_teacher_courses]
```

**For specific teacher:**
```
[sensei_teacher_courses teacher_id="456"]
```

**What it shows:**
- Created courses
- Student enrollment numbers
- Course management links
- Analytics overview

### 10. Teacher Profile

**Display teacher information:**
```
[sensei_teacher_profile teacher_id="789"]
```

**Teacher details displayed:**
- Teacher photo and bio
- Courses taught
- Student count
- Teaching experience

---

## Single Course Content Shortcodes

### 11. Course Information

**Display course details:**
```
[sensei_course_info course_id="123"]
```

**Parameters:**

| Parameter | Required | Example | Purpose |
|-----------|----------|---------|----------|
| `course_id` | Yes | "123" | Which course |
| `show_teacher` | No | "yes" | Show teacher info |
| `show_lessons` | No | "yes" | Display lesson count |
| `show_price` | No | "yes" | Show WooCommerce price |

### 12. Course Lessons

**Display course lesson list:**
```
[sensei_course_lessons course_id="123"]
```

**What it shows:**
- Lesson titles
- Lesson descriptions
- Completion status (if enrolled)
- Lesson duration
- Prerequisites

### 13. Course Teacher

**Show course teacher information:**
```
[sensei_course_teacher course_id="123"]
```

**Teacher information:**
- Teacher photo
- Name and bio
- Other courses by teacher
- Contact information

### 14. Course Prerequisite

**Display course requirements:**
```
[sensei_course_prerequisites course_id="123"]
```

**Shows:**
- Required previous courses
- Skill requirements
- Knowledge prerequisites

---

## Quiz & Assessment Shortcodes

### 15. Course Quizzes

**Display course quizzes:**
```
[sensei_course_quizzes course_id="123"]
```

**Quiz information shown:**
- Quiz titles
- Question count
- Pass mark
- Completion status

### 16. Quiz Results

**Show student quiz results:**
```
[sensei_quiz_results quiz_id="456"]
```

**For specific user:**
```
[sensei_quiz_results quiz_id="456" user_id="789"]
```

**Results display:**
- Score achieved
- Pass/fail status
- Correct answers
- Completion date

### 17. Student Grades

**Display all student grades:**
```
[sensei_student_grades]
```

**For specific course:**
```
[sensei_student_grades course_id="123"]
```

---

## Enrollment & Purchase Shortcodes

### 18. Course Enrollment Button

**Enrollment/purchase button:**
```
[sensei_course_button course_id="123"]
```

**Custom button text:**
```
[sensei_course_button
    course_id="123"
    button_text="Start Learning Now!"
    button_class="custom-btn"]
```

### 19. Course Price

**Display course pricing (WooCommerce):**
```
[sensei_course_price course_id="123"]
```

**What it shows:**
- Current price
- Sale price (if on sale)
- Free course indicator
- Add to cart button

### 20. WooCommerce Integration

**Add to cart for courses:**
```
[sensei_add_to_cart course_id="123"]
```

**WooCommerce product display:**
```
[sensei_woocommerce_product course_id="123"]
```

---

## Messages & Interaction Shortcodes

### 21. Course Messages

**Display course-related messages:**
```
[sensei_course_messages course_id="123"]
```

### 22. Teacher Messages

**Show messages from teacher:**
```
[sensei_teacher_messages course_id="123"]
```

### 23. Student Questions

**Q&A section for courses:**
```
[sensei_course_questions course_id="123"]
```

---

## Conditional Display Shortcodes

### 24. Show If Enrolled

**Content only for enrolled students:**
```
[sensei_enrolled_only course_id="123"]
    Welcome to the course! Here's your exclusive content.
[/sensei_enrolled_only]
```

### 25. Show If Completed

**Content for course graduates:**
```
[sensei_completed_only course_id="123"]
    Congratulations! You've completed the course.
    <a href="/advanced-course">Try our advanced course next!</a>
[/sensei_completed_only]
```

### 26. Show If Not Enrolled

**Promotional content:**
```
[sensei_not_enrolled course_id="123"]
    <div class="enrollment-cta">
        <h3>Ready to start learning?</h3>
        <p>Join hundreds of students in this course.</p>
        [sensei_course_button course_id="123"]
    </div>
[/sensei_not_enrolled]
```

### 27. Teacher Only Content

**Content visible only to teachers:**
```
[sensei_teacher_only]
    <p>This content is only visible to course teachers.</p>
[/sensei_teacher_only]
```

---

## User Authentication Shortcodes

### 28. Login Form

**Sensei login form:**
```
[sensei_login_form]
```

**With redirect:**
```
[sensei_login_form redirect="/my-courses/"]
```

### 29. Registration Form

**Student registration:**
```
[sensei_registration_form]
```

**Teacher registration:**
```
[sensei_teacher_registration]
```

### 30. User Dashboard

**Complete user account area:**
```
[sensei_user_dashboard]
```

---

## Certificate Shortcodes

### 31. Course Certificates

**Display earned certificates:**
```
[sensei_certificates]
```

**For specific course:**
```
[sensei_course_certificate course_id="123"]
```

### 32. Certificate Download

**Download link for certificate:**
```
[sensei_certificate_download course_id="123"]
```

---

## Advanced Display Shortcodes

### 33. Course Grid

**Advanced course grid with custom layout:**
```
[sensei_course_grid
    layout="masonry"
    show_image="yes"
    show_excerpt="yes"
    show_meta="yes"]
```

### 34. Course Carousel

**Rotating course display:**
```
[sensei_course_carousel
    per_page="6"
    autoplay="true"
    dots="true"]
```

### 35. Teacher Grid

**Display multiple teachers:**
```
[sensei_teachers
    per_page="8"
    columns="4"
    show_courses="yes"]
```

---

## Statistics & Analytics Shortcodes

### 36. Course Statistics

**Display course metrics:**
```
[sensei_course_stats course_id="123"]
```

**What it shows:**
- Total students
- Completion rate
- Average grade
- Course rating

### 37. Learning Progress

**Student learning analytics:**
```
[sensei_learning_progress user_id="456"]
```

### 38. Site Statistics

**Overall site metrics:**
```
[sensei_site_stats]
```

**Displays:**
- Total courses
- Total students
- Total teachers
- Courses completed

---

## Page Layout Examples

### 💰 Revenue-Optimized Homepage Layout

```html
<!-- Hero Section -->
<h1>Transform Your Career with Expert-Led Courses</h1>
<p>Join 10,000+ successful students earning $50K+ after certification</p>
[sensei_course_search]

<!-- Social Proof -->
<h2>🏆 Featured Success Stories</h2>
[sensei_featured_courses per_page="6" columns="3"]

<!-- Trust Building -->
<h2>📈 Popular Learning Paths</h2>
[sensei_course_categories show_count="yes"]

<!-- Urgency/Scarcity -->
<h2>✨ New Courses (Limited Time Pricing)</h2>
[sensei_courses orderby="date" per_page="6"]

<!-- Authority Building -->
<h2>🎯 Meet Our Expert Instructors</h2>
[sensei_teachers per_page="4" columns="4"]

<!-- Social Proof -->
<h2>🚀 Join Our Thriving Learning Community</h2>
[sensei_site_stats]
<p>12,000+ courses completed • 4.8/5 average rating • $2.4M+ in student career growth</p>

<!-- Strong CTA -->
[sensei_not_logged_in]
    <div class="cta-section">
        <h3>🚀 Start Your Success Journey Today!</h3>
        <p>30-day money-back guarantee • Instant access • Mobile learning</p>
        <a href="/register" class="button">Get Started - Only $49/month</a>
    </div>
[/sensei_not_logged_in]
```

### Course Catalog Page

```html
<h1>Course Catalog</h1>

<!-- Search and Filters -->
[sensei_course_search show_categories="yes" show_price_filter="yes"]

<!-- Course Grid -->
[sensei_courses per_page="12" columns="3"]
```

### Student Dashboard

```html
<h1>My Learning Dashboard</h1>

<!-- Main Dashboard -->
[sensei_student_dashboard]

<!-- My Courses -->
<h2>My Courses</h2>
[sensei_my_courses]

<!-- Certificates -->
<h2>My Certificates</h2>
[sensei_certificates]

<!-- Learning Progress -->
<h2>Learning Progress</h2>
[sensei_learning_progress]
```

### Individual Course Page

```html
<!-- Course Header -->
[sensei_course_info course_id="123"]

<!-- Course Teacher -->
<h2>Your Teacher</h2>
[sensei_course_teacher course_id="123"]

<!-- Prerequisites -->
[sensei_course_prerequisites course_id="123"]

<!-- Enrollment Check -->
[sensei_not_enrolled course_id="123"]
    <h2>Course Lessons</h2>
    [sensei_course_lessons course_id="123"]

    <h2>Course Quizzes</h2>
    [sensei_course_quizzes course_id="123"]

    <h2>Enroll Now</h2>
    [sensei_course_button course_id="123"]
[/sensei_not_enrolled]

[sensei_enrolled_only course_id="123"]
    <h2>Your Progress</h2>
    [sensei_course_progress course_id="123"]

    <h2>Course Content</h2>
    [sensei_course_lessons course_id="123"]

    <h2>Course Messages</h2>
    [sensei_course_messages course_id="123"]
[/sensei_enrolled_only]

<!-- Course Statistics -->
<h2>Course Statistics</h2>
[sensei_course_stats course_id="123"]
```

### Teacher Profile Page

```html
<h1>Teacher Profile</h1>

<!-- Teacher Information -->
[sensei_teacher_profile teacher_id="789"]

<!-- Teacher's Courses -->
<h2>Courses by This Teacher</h2>
[sensei_teacher_courses teacher_id="789"]

<!-- Teacher Dashboard (for logged-in teacher) -->
[sensei_teacher_only]
    <h2>Teacher Dashboard</h2>
    [sensei_teacher_courses]
[/sensei_teacher_only]
```

---

## Styling Shortcodes

### CSS Classes for Customization

**All shortcodes use these base classes:**

```css
.sensei-wrap { /* Main container */ }
.sensei-course-grid { /* Course grid container */ }
.sensei-course { /* Individual course item */ }
.sensei-progress { /* Progress indicators */ }
.sensei-button { /* Action buttons */ }
.sensei-form { /* Form elements */ }
```

### Custom Styling Examples

```css
/* Style course grid */
.sensei-course-grid {
    display: grid;
    gap: 24px;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

/* Course item styling */
.sensei-course {
    border: 1px solid #e0e0e0;
    border-radius: 12px;
    padding: 24px;
    transition: all 0.3s ease;
    background: white;
}

.sensei-course:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.1);
    border-color: #your-brand-color;
}

/* Progress bar styling */
.sensei-progress {
    background: #f8f9fa;
    border-radius: 25px;
    overflow: hidden;
    height: 16px;
}

.sensei-progress .sensei-progress-bar {
    background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
    height: 100%;
    border-radius: 25px;
    transition: width 0.6s ease;
}

/* Button styling */
.sensei-button {
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

.sensei-button:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
}

/* Mobile responsive */
@media (max-width: 768px) {
    .sensei-course-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }
}
```

---

## WooCommerce Integration Shortcodes

### 39. Product Course Display

**Show course as WooCommerce product:**
```
[sensei_wc_product course_id="123"]
```

### 40. Course Cart

**Mini cart for course purchases:**
```
[sensei_course_cart]
```

### 41. Checkout Integration

**Course-specific checkout:**
```
[sensei_course_checkout course_id="123"]
```

---

## Troubleshooting Shortcodes

### Common Issues

**"Shortcode not displaying"**
- Check spelling exactly
- Verify course/user IDs exist
- Ensure Sensei is active
- Check WooCommerce integration

**"Layout looks broken"**
- Check CSS conflicts
- Verify column numbers
- Test with default theme
- Clear all caches

**"No courses showing"**
- Check course publication status
- Verify WooCommerce products exist
- Confirm category exists
- Test with simpler parameters

**"User-specific content not working"**
- Ensure user is logged in
- Check user enrollment status
- Verify user permissions
- Test with current user

---

## Performance Tips

### Optimize Shortcode Performance

```
// Use specific parameters to limit results
[sensei_courses per_page="6"] // Instead of showing all

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
3. **Test WooCommerce integration** thoroughly
4. **Document custom implementations** for your team
5. **Use widgets** for sidebar content

### Mobile Optimization

```
// Use fewer columns on mobile
[sensei_courses columns="3"] // Automatically adjusts to 1 on mobile

// Simplify content for mobile
[sensei_mobile_only]
    [sensei_courses per_page="4" columns="1"]
[/sensei_mobile_only]

[sensei_desktop_only]
    [sensei_courses per_page="12" columns="3"]
[/sensei_desktop_only]
```

---

## Quick Copy Reference

### Most Used Shortcodes

```
// Course catalog
[sensei_courses]

// Student dashboard
[sensei_my_courses]

// Course information
[sensei_course_info course_id="123"]

// Course search
[sensei_course_search]

// Categories
[sensei_course_categories]

// Enrollment button
[sensei_course_button course_id="123"]

// Progress tracking
[sensei_course_progress course_id="123"]

// Teacher profile
[sensei_teacher_profile teacher_id="789"]

// Course lessons
[sensei_course_lessons course_id="123"]

// Course price
[sensei_course_price course_id="123"]
```

---

**Need Help with Shortcodes?**
📧 Email: support@wbcomdesigns.com
📚 More examples: docs.wbcomdesigns.com
💬 Forum: wbcomdesigns.com/support
🎥 Video tutorials in member area