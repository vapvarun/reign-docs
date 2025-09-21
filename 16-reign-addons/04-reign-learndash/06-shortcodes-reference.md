# Reign LearnDash Addon - Shortcodes Reference

## What You'll Learn
This guide provides a complete reference for all shortcodes available in the Reign LearnDash addon. Learn how to display courses, user progress, and learning content anywhere on your site!

## Quick Overview  
**Usage Level:** Easy (just copy and paste!)  
**Where to use:** Pages, posts, widgets, anywhere!  
**Pro tip:** Test shortcodes on a draft page first

---

## Essential Course Shortcodes

### 1. Course List

**Display all courses in a grid:**
```
[learndash_courses]
```

**With parameters:**
```
[learndash_courses 
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
| `columns` | 1, 2, 3, 4 | 3 | Grid columns |
| `orderby` | date, title, menu_order, price | date | Sort method |
| `order` | ASC, DESC | DESC | Sort direction |
| `category` | Category slug | All | Filter by category |
| `tag` | Tag slug | All | Filter by tag |
| `price` | free, paid, open | All | Filter by price type |
| `featured` | true, false | false | Show only featured |

**Examples:**

```
// Show 6 newest courses in 2 columns
[learndash_courses per_page="6" columns="2" orderby="date"]

// Free courses only
[learndash_courses price="free" per_page="8"]

// Featured courses for homepage
[learndash_courses featured="true" per_page="4"]
```

---

### 2. Single Course Info

**Display specific course details:**
```
[course_info course_id="123"]
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
| `course_id` | Yes | "123" | Which course |
| `show_price` | No | "yes" | Display price |
| `show_instructor` | No | "yes" | Show instructor |
| `show_progress` | No | "yes" | User progress (if enrolled) |

---

### 3. Course Categories

**List all course categories:**
```
[learndash_course_categories]
```

**With options:**
```
[learndash_course_categories 
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

## User Progress Shortcodes

### 4. User Profile

**Show user's learning progress:**
```
[ld_profile]
```

**For specific user:**
```
[ld_profile user_id="456"]
```

**What it includes:**
- Enrolled courses
- Course progress
- Completed courses
- Certificates earned
- Quiz results
- Points/achievements

---

### 5. Course Progress

**Show progress for specific course:**
```
[course_progress course_id="123"]
```

**Advanced usage:**
```
[course_progress 
    course_id="123"
    user_id="456"
    show_percentage="yes"
    show_details="yes"]
```

---

### 6. My Courses

**List user's enrolled courses:**
```
[ld_course_list]
```

**Filter by status:**
```
[ld_course_list status="in_progress"]
```

**Status options:**
- `all` - All enrolled courses
- `in_progress` - Currently taking
- `completed` - Finished courses
- `not_started` - Enrolled but not started

---

## Assessment Shortcodes

### 7. Quiz List

**Show quizzes for a course:**
```
[course_quizzes course_id="123"]
```

**Quiz results:**
```
[quiz_results quiz_id="789" user_id="456"]
```

---

### 8. Certificate Display

**Show user certificates:**
```
[ld_certificates]
```

**Specific certificate:**
```
[ld_certificate certificate_id="101" user_id="456"]
```

---

## Instructor Shortcodes

### 9. Instructor Profile

**Display instructor information:**
```
[instructor_profile instructor_id="789"]
```

**What it shows:**
- Instructor bio and photo
- Courses they teach
- Ratings and reviews
- Social links
- Experience/credentials

---

### 10. Instructor Courses

**List courses by specific instructor:**
```
[instructor_courses instructor_id="789"]
```

**With layout options:**
```
[instructor_courses 
    instructor_id="789"
    columns="2"
    show_ratings="yes"]
```

---

## Navigation & Login Shortcodes

### 11. Course Navigation

**Add course navigation menu:**
```
[course_navigation course_id="123"]
```

**What it includes:**
- Course outline
- Lesson links
- Progress indicators
- Next/previous buttons

---

### 12. Learning Dashboard

**Complete student dashboard:**
```
[learndash_user_dashboard]
```

**What students see:**
- Course overview
- Recent activity
- Upcoming assignments
- Achievement progress
- Quick actions

---

### 13. Login Form

**LearnDash-specific login:**
```
[learndash_login]
```

**With redirect:**
```
[learndash_login redirect="/my-courses/"]
```

---

## Course Content Shortcodes

### 14. Lesson List

**Show lessons for a course:**
```
[course_lessons course_id="123"]
```

**Advanced options:**
```
[course_lessons 
    course_id="123"
    show_status="yes"
    show_duration="yes"
    num="10"]
```

---

### 15. Course Outline

**Complete course structure:**
```
[course_outline course_id="123"]
```

**Shows:**
- All lessons organized
- Quizzes and assignments
- Completion status
- Time estimates

---

### 16. Recent Courses

**Latest published courses:**
```
[recent_courses num="5"]
```

---

## Search & Filter Shortcodes

### 17. Course Search

**Search form for courses:**
```
[course_search]
```

**With filters:**
```
[course_search 
    show_categories="yes"
    show_difficulty="yes"
    show_price_filter="yes"]
```

---

### 18. Featured Courses

**Highlight specific courses:**
```
[featured_courses course_ids="123,456,789"]
```

**Parameters:**

| Parameter | Example | Purpose |
|-----------|---------|----------|
| `course_ids` | "123,456,789" | Specific courses |
| `columns` | "3" | Layout columns |
| `show_excerpt` | "yes" | Course descriptions |

---

## Group Learning Shortcodes

### 19. Group Courses

**Show courses for a group:**
```
[group_courses group_id="456"]
```

---

### 20. Group Progress

**Track group learning:**
```
[group_progress group_id="456"]
```

**Shows:**
- Group member progress
- Completion rates
- Group statistics
- Leaderboards

---

## Interactive Shortcodes

### 21. Course Enrollment Button

**Add enrollment button anywhere:**
```
[course_enrollment course_id="123"]
```

**Custom button text:**
```
[course_enrollment course_id="123" button_text="Start Learning Now!"]
```

---

### 22. Course Rating

**Display course ratings:**
```
[course_rating course_id="123"]
```

**Rating form:**
```
[course_rating_form course_id="123"]
```

---

## Conditional Shortcodes

### 23. Show If Enrolled

**Content only for enrolled students:**
```
[if_enrolled course_id="123"]
    Welcome to the course! Here are your exclusive materials.
[/if_enrolled]
```

---

### 24. Show If Completed

**Content for course graduates:**
```
[if_completed course_id="123"]
    Congratulations! You've completed the course.
    <a href="/advanced-course">Try our advanced course next!</a>
[/if_completed]
```

---

### 25. Show If Not Enrolled

**Promotional content:**
```
[if_not_enrolled course_id="123"]
    <div class="enrollment-cta">
        <h3>Ready to start learning?</h3>
        <p>Join thousands of students in this popular course.</p>
        [course_enrollment course_id="123"]
    </div>
[/if_not_enrolled]
```

---

## Advanced Shortcodes

### 26. Course Statistics

**Display course stats:**
```
[course_stats course_id="123"]
```

**Shows:**
- Total enrollments
- Completion rate
- Average rating
- Total lessons/quizzes

---

### 27. Learning Achievements

**Show user badges/achievements:**
```
[user_achievements user_id="456"]
```

---

### 28. Course Calendar

**Upcoming course events:**
```
[course_calendar]
```

**For specific course:**
```
[course_calendar course_id="123"]
```

---

## Page Layout Examples

### Homepage Layout

```html
<!-- Hero Section -->
<h1>Start Learning Today</h1>
[course_search]

<!-- Featured Courses -->
<h2>Featured Courses</h2>
[featured_courses course_ids="123,456,789" columns="3"]

<!-- Course Categories -->
<h2>Browse by Category</h2>
[learndash_course_categories show_count="yes"]

<!-- Recent Courses -->
<h2>Latest Courses</h2>
[recent_courses num="6"]

<!-- Call to Action -->
[if_not_logged_in]
    <div class="cta-section">
        <h3>Ready to Start Learning?</h3>
        <a href="/register" class="button">Create Free Account</a>
    </div>
[/if_not_logged_in]
```

### Course Archive Page

```html
<h1>All Courses</h1>

<!-- Search and Filters -->
[course_search show_categories="yes" show_difficulty="yes"]

<!-- Course Grid -->
[learndash_courses per_page="12" columns="3" orderby="date"]
```

### Student Dashboard

```html
<h1>My Learning Dashboard</h1>

<!-- Main Dashboard -->
[learndash_user_dashboard]

<!-- My Courses -->
<h2>My Courses</h2>
[ld_course_list]

<!-- Achievements -->
<h2>My Achievements</h2>
[user_achievements]

<!-- Certificates -->
<h2>My Certificates</h2>
[ld_certificates]
```

### Individual Course Page

```html
<!-- Course Header -->
[course_info course_id="123"]

<!-- Enrollment Check -->
[if_not_enrolled course_id="123"]
    <h2>Course Outline</h2>
    [course_outline course_id="123"]
    
    <h2>What You'll Learn</h2>
    <!-- Course benefits and outcomes -->
    
    [course_enrollment course_id="123"]
[/if_not_enrolled]

[if_enrolled course_id="123"]
    <h2>Your Progress</h2>
    [course_progress course_id="123"]
    
    <h2>Course Content</h2>
    [course_lessons course_id="123"]
[/if_enrolled]

<!-- Reviews -->
<h2>Student Reviews</h2>
[course_rating course_id="123"]

<!-- Instructor -->
<h2>Your Instructor</h2>
[instructor_profile instructor_id="789"]
```

### Instructor Page

```html
<h1>Meet Your Instructor</h1>

<!-- Instructor Bio -->
[instructor_profile instructor_id="789"]

<!-- Their Courses -->
<h2>Courses by This Instructor</h2>
[instructor_courses instructor_id="789" columns="2"]

<!-- Student Reviews -->
<h2>What Students Say</h2>
<!-- Custom testimonials -->
```

---

## Styling Shortcodes

### CSS Classes for Customization

**All shortcodes use these base classes:**

```css
.learndash-wrapper { /* Main container */ }
.ld-course-card { /* Course cards */ }
.ld-course-grid { /* Course grid layout */ }
.ld-progress-bar { /* Progress indicators */ }
.ld-button { /* Action buttons */ }
.ld-user-dashboard { /* Dashboard layout */ }
```

### Custom Styling Examples

```css
/* Style course cards */
.ld-course-card {
    border: 1px solid #eee;
    border-radius: 8px;
    padding: 20px;
    transition: transform 0.3s;
}

.ld-course-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 25px rgba(0,0,0,0.1);
}

/* Progress bar styling */
.ld-progress-bar {
    background: #f0f0f0;
    border-radius: 20px;
    overflow: hidden;
}

.ld-progress-bar-fill {
    background: linear-gradient(90deg, #4CAF50, #8BC34A);
    height: 20px;
    border-radius: 20px;
    transition: width 0.5s ease;
}

/* Button styling */
.ld-button {
    background: #your-brand-color;
    color: white;
    padding: 12px 24px;
    border-radius: 5px;
    text-decoration: none;
    display: inline-block;
    font-weight: 600;
    transition: background 0.3s;
}

.ld-button:hover {
    background: #darker-brand-color;
    color: white;
}
```

---

## Troubleshooting Shortcodes

### Common Issues

**"Shortcode not displaying"**
- Check spelling exactly
- Verify course/user IDs exist
- Ensure LearnDash is active
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
[learndash_courses per_page="6"] // Instead of showing all

// Cache-friendly: avoid user-specific shortcodes on cached pages
// Use AJAX loading for dynamic content

// Minimize nested shortcodes
// Use specific IDs when possible
```

---

## Pro Tips

### Advanced Usage

1. **Combine shortcodes** for rich layouts
2. **Use conditional shortcodes** for personalization
3. **Test on staging** before going live
4. **Document custom shortcodes** for your team
5. **Use widgets** for sidebar content

### Mobile Optimization

```
// Use fewer columns on mobile
[learndash_courses columns="3"] // Shows as 1 on mobile automatically

// Simplify content for mobile
[if_mobile]
    [learndash_courses per_page="4" columns="1"]
[/if_mobile]

[if_desktop]
    [learndash_courses per_page="12" columns="3"]
[/if_desktop]
```

---

## Quick Copy Reference

### Most Used Shortcodes

```
// Course listings
[learndash_courses]

// User dashboard
[learndash_user_dashboard]

// User profile
[ld_profile]

// Course search
[course_search]

// Course categories
[learndash_course_categories]

// User courses
[ld_course_list]

// Course enrollment
[course_enrollment course_id="123"]

// Course progress
[course_progress course_id="123"]

// Course info
[course_info course_id="123"]

// Login form
[learndash_login]
```

---

**Need Help with Shortcodes?**  
📧 Email: support@wbcomdesigns.com  
📚 More examples: docs.wbcomdesigns.com  
💬 Forum: wbcomdesigns.com/support  
🎥 Video tutorials in member area