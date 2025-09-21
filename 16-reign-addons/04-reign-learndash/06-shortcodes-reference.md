# Reign LearnDash Addon - Shortcodes Reference (Complete)

## Available Shortcodes (Comprehensive Analysis)

Reign LearnDash Addon v4.8.2 provides 6 shortcodes with extensive functionality based on comprehensive source code analysis:

---

## Course Display Shortcodes

### [modern_courses] / [reign_courses]

Both shortcodes are identical - `[reign_courses]` is an alias for `[modern_courses]`. This is the most advanced course display shortcode with 25+ parameters.

**Basic Usage:**
```
[modern_courses]
[reign_courses]
```

**Complete Parameters (from source code analysis):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 12 | Any number | Courses per page |
| `columns` | 3 | 1-6 | Number of columns in grid |
| `orderby` | date | date, title, menu_order, price, popularity | Sort method |
| `order` | DESC | ASC, DESC | Sort direction |
| `category` | - | Category slug/ID | Filter by category |
| `tag` | - | Tag slug/ID | Filter by tag |
| `course_ids` | - | Comma-separated IDs | Specific courses to display |
| `show_filters` | yes | yes, no | Display filter options |
| `show_search` | yes | yes, no | Display search bar |
| `show_sorting` | yes | yes, no | Display sorting dropdown |
| `show_progress` | yes | yes, no | Show progress bars for enrolled users |
| `show_reviews` | yes | yes, no | Display star ratings and review counts |
| `template` | classic | classic, minimal, premium, detailed | Visual template style |
| `layout` | layout_one | layout_one, layout_two, layout_three | Course card layout design |
| `view` | grid | grid, list | Layout view type |
| `instructor` | - | Username or ID | Filter by instructor |
| `instructor_role` | - | Role name | Filter by instructor role |
| `price_type` | - | free, paid, all | Filter by price type |
| `enrolled` | - | yes, no, all | Show enrolled/not enrolled courses |
| `progress_min` | - | 0-100 | Minimum progress percentage |
| `progress_max` | - | 0-100 | Maximum progress percentage |
| `pagination` | numbers | numbers, load_more, infinite, both | Pagination style |
| `show_course_count` | yes | yes, no | Display total course count |
| `show_view_switcher` | yes | yes, no | Grid/list view toggle |
| `show_price` | yes | yes, no | Display course pricing |
| `show_instructor` | yes | yes, no | Display instructor information |
| `show_categories` | yes | yes, no | Display course categories |
| `show_duration` | yes | yes, no | Display course duration |
| `show_students` | yes | yes, no | Display enrolled student count |
| `show_lessons` | yes | yes, no | Display lesson count |
| `udemy_style` | no | yes, no | Enable Udemy-style course cards |

**Advanced Examples:**

```
// Udemy-style course display
[modern_courses template="premium" udemy_style="yes" show_price="yes" show_reviews="yes"]

// Course catalog with filters
[modern_courses per_page="12" columns="4" show_filters="yes" show_search="yes" show_sorting="yes"]

// Instructor courses page
[modern_courses instructor="john-smith" template="detailed" show_instructor="yes"]

// Free courses only
[modern_courses price_type="free" template="minimal" columns="3"]

// User's enrolled courses
[modern_courses enrolled="yes" show_progress="yes" template="premium"]

// Category-specific courses
[modern_courses category="web-development" layout="layout_two" per_page="8"]
```

## Group Display Shortcode

### [modern_groups]

Advanced LearnDash groups display with comprehensive customization options.

**Basic Usage:**
```
[modern_groups]
```

**Complete Parameters (from source code):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 12 | Any number | Groups per page |
| `columns` | 3 | 1-6 | Number of columns |
| `orderby` | date | date, title, menu_order | Sort method |
| `order` | DESC | ASC, DESC | Sort direction |
| `template` | minimal | minimal, premium, detailed, creative, compact | Visual template |
| `show_filters` | yes | yes, no | Display filter options |
| `show_search` | yes | yes, no | Display search functionality |
| `show_sorting` | yes | yes, no | Display sorting options |
| `show_view_switcher` | yes | yes, no | Grid/list view switcher |
| `show_pagination` | yes | yes, no | Display pagination |
| `pagination_type` | numbers | numbers, load_more, infinite | Pagination style |
| `show_progress` | yes | yes, no | Show group progress |
| `show_members` | yes | yes, no | Show member count |
| `show_courses` | yes | yes, no | Show associated course count |
| `show_price` | yes | yes, no | Show group pricing |
| `show_categories` | yes | yes, no | Show group categories |
| `show_instructor` | yes | yes, no | Show group leader/instructor |
| `categories` | - | Comma-separated IDs | Filter by categories |
| `tags` | - | Comma-separated IDs | Filter by tags |
| `instructor_id` | - | User ID | Filter by specific instructor |
| `enrolled_only` | no | yes, no | Show only enrolled groups |
| `default_view` | grid | grid, list | Default view mode |
| `buddypress_sync` | no | yes, no | Enable BuddyPress group sync |

**Advanced Examples:**

```
// Premium group display with BuddyPress sync
[modern_groups template="premium" buddypress_sync="yes" show_members="yes"]

// Groups by specific instructor
[modern_groups instructor_id="123" template="detailed" columns="2"]

// User's enrolled groups
[modern_groups enrolled_only="yes" show_progress="yes" template="compact"]
```

## Course Tab Content Shortcodes

Advanced tab content shortcodes for single course pages:

### [reign_ld_pro_comments_tab_content]

Display course comments, discussions, and reviews.

**Usage:**
```
[reign_ld_pro_comments_tab_content]
```

**Features:**
- Course reviews and ratings display
- Comment threading and moderation
- Star rating submission forms
- Review analytics and aggregation

### [reign_ld_pro_instructor_tab_content]

Display comprehensive instructor information.

**Usage:**
```
[reign_ld_pro_instructor_tab_content]
```

**Features:**
- Instructor biography and credentials
- Instructor courses listing
- Social media links and contact information
- Instructor ratings and reviews

### [reign_ld_pro_course_content_tab_content]

Display main course content and curriculum.

**Usage:**
```
[reign_ld_pro_course_content_tab_content]
```

**Features:**
- Course curriculum outline
- Lesson and topic listing
- Progress tracking integration
- Course materials and downloads

---

## Widget Integration

The addon provides 3 custom widgets that work with shortcode-like functionality:

### Course Categories Widget
Display course categories in sidebars with customizable styling.

### Course Listing Widget
Show featured or recent courses in widget areas.

### Course Search Widget
Advanced course search functionality for sidebars.

---

## BuddyPress Social Learning Integration

### Enrolled Courses Profile Display
When BuddyPress is active, users get a dedicated "LearnDash Courses" tab in their profiles showing:
- Enrolled courses with progress
- Completed courses and achievements
- Course-related activities and interactions
- Social learning features

### Course-Group Synchronization
Automatic creation and management of BuddyPress groups for courses:
```
// Enable BuddyPress sync in course shortcodes
[modern_courses buddypress_sync="yes"]
[modern_groups buddypress_sync="yes"]
```

---

## Advanced Usage Examples

### Complete Learning Portal Homepage
```
// Featured courses section
[modern_courses per_page="8" columns="4" template="premium" udemy_style="yes" category="featured"]

// Recent courses
[modern_courses per_page="6" columns="3" orderby="date" template="minimal"]

// Learning groups
[modern_groups per_page="4" columns="2" template="creative" show_members="yes"]
```

### User Profile Course Display
```
// User's enrolled courses
[modern_courses enrolled="yes" show_progress="yes" template="detailed" columns="2"]

// User's groups
[modern_groups enrolled_only="yes" show_progress="yes" template="compact"]
```

### Instructor Profile
```
// Instructor's courses
[modern_courses instructor="current" template="premium" show_students="yes" show_reviews="yes"]
```

### Course Category Pages
```
// Web Development courses
[modern_courses category="web-development" template="premium" show_filters="yes" udemy_style="yes"]
```

---

## Related Courses Feature

The addon automatically displays related courses based on:
- Course categories and tags
- Instructor relationships
- Course difficulty level
- User enrollment history

**Configuration:** Related courses appear automatically on single course pages and can be customized through admin settings.

---

## Troubleshooting

### Shortcodes Not Displaying
1. Verify plugin is activated (version 4.8.2+)
2. Check LearnDash is properly configured
3. Ensure courses/groups exist and are published
4. Clear all caches (page, object, and plugin caches)

### BuddyPress Features Not Working
1. Verify BuddyPress is active and properly configured
2. Check BuddyPress components are enabled (Groups, Activity)
3. Ensure user permissions are correctly set
4. Test with BuddyPress sync enabled

### Performance Issues
1. Limit `per_page` to reasonable numbers (12-24 for courses, 8-16 for groups)
2. Use specific category/tag filters instead of showing all content
3. Enable caching and optimize images
4. Consider pagination over infinite scroll for large datasets

### Template Issues
1. Check template parameter spelling (classic, minimal, premium, detailed)
2. Verify layout options (layout_one, layout_two, layout_three)
3. Clear theme and plugin caches
4. Test with default Reign theme settings

---

*Comprehensive shortcodes reference based on complete analysis of Reign LearnDash Addon v4.8.2 source code*