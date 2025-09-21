# Reign LearnDash Addon - Shortcodes Reference

## Available Shortcodes (Verified)

Reign LearnDash Addon provides 6 shortcodes based on the actual plugin source code:

---

## Course Display Shortcodes

### [modern_courses] / [reign_courses]

Both shortcodes are identical - `[reign_courses]` is an alias for `[modern_courses]`.

**Basic Usage:**
```
[modern_courses]
[reign_courses]
```

**All Parameters (from source code):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 12 | Any number | Courses per page |
| `columns` | 3 | Number | Number of columns in grid |
| `orderby` | date | date, title, menu_order, etc. | Sort method |
| `order` | DESC | ASC, DESC | Sort direction |
| `category` | - | Category slug | Filter by category |
| `tag` | - | Tag slug | Filter by tag |
| `course_ids` | - | Comma-separated IDs | Specific courses to display |
| `show_filters` | yes | yes, no | Display filter options |
| `show_search` | yes | yes, no | Display search bar |
| `show_sorting` | yes | yes, no | Display sorting dropdown |
| `show_progress` | yes | yes, no | Show progress bars |
| `show_reviews` | yes | yes, no | Display ratings |
| `template` | classic | classic, minimal, premium, detailed | Visual template style |
| `view` | grid | grid, list | Layout view type |
| `instructor` | - | Username or ID | Filter by instructor |
| `instructor_role` | - | Role name | Filter by instructor role |
| `price_type` | - | free, paid, all | Filter by price |
| `enrolled` | - | yes, no, all | Show enrolled/not enrolled |
| `progress_min` | - | 0-100 | Minimum progress % |
| `progress_max` | - | 0-100 | Maximum progress % |
| `pagination` | numbers | numbers, load_more, infinite, both | Pagination style |

**Examples:**

```
// Basic course display
[modern_courses]

// Display 6 courses in 2 columns
[modern_courses per_page="6" columns="2"]

// Show specific courses
[modern_courses course_ids="101,102,103"]

// Filter by category
[modern_courses category="advanced"]

// Hide filters and search
[modern_courses show_filters="no" show_search="no"]
```

## Group Display Shortcode

### [modern_groups]

Display LearnDash groups with customizable templates.

**Basic Usage:**
```
[modern_groups]
```

**All Parameters (from source code):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 12 | Any number | Groups per page |
| `columns` | 3 | Number | Number of columns |
| `orderby` | date | date, title, menu_order | Sort method |
| `order` | DESC | ASC, DESC | Sort direction |
| `template` | minimal | minimal, premium, detailed, creative, compact | Visual template |
| `show_filters` | yes | yes, no | Display filters |
| `show_search` | yes | yes, no | Display search |
| `show_sorting` | yes | yes, no | Display sorting |
| `show_view_switcher` | yes | yes, no | Grid/list switcher |
| `show_pagination` | yes | yes, no | Display pagination |
| `pagination_type` | numbers | numbers, load_more, infinite | Pagination style |
| `show_progress` | yes | yes, no | Show progress |
| `show_members` | yes | yes, no | Show member count |
| `show_courses` | yes | yes, no | Show course count |
| `show_price` | yes | yes, no | Show price |
| `show_categories` | yes | yes, no | Show categories |
| `show_instructor` | yes | yes, no | Show instructor |
| `categories` | - | Comma-separated IDs | Filter by categories |
| `tags` | - | Comma-separated IDs | Filter by tags |
| `instructor_id` | - | User ID | Filter by instructor |
| `enrolled_only` | no | yes, no | Show only enrolled groups |
| `default_view` | grid | grid, list | Default view mode |

**Examples:**

```
// Basic groups display
[modern_groups]

// Display 8 groups in 4 columns
[modern_groups per_page="8" columns="4"]

// Use premium template
[modern_groups template="premium"]

// Hide filters and search
[modern_groups show_filters="no" show_search="no"]
```

## Course Tab Content Shortcodes

These shortcodes are for displaying specific course information, typically used in custom templates:

### [reign_ld_pro_comments_tab_content]

Display course comments/discussions.

```
[reign_ld_pro_comments_tab_content]
```

### [reign_ld_pro_instructor_tab_content]

Display instructor information.

```
[reign_ld_pro_instructor_tab_content]
```

### [reign_ld_pro_course_content_tab_content]

Display main course content/curriculum.

```
[reign_ld_pro_course_content_tab_content]
```

**Note:** These tab shortcodes are primarily used within course page templates and may not work correctly when used in regular pages/posts.

---

## Common Usage Examples

### Display Courses on Homepage
```
[modern_courses per_page="6" columns="3" template="premium"]
```

### Create Course Category Page
```
[modern_courses category="beginner" show_filters="yes"]
```

### Show Groups in Sidebar
```
[modern_groups per_page="4" columns="1" show_search="no"]
```

### Instructor Course Listing
```
[modern_courses instructor="john-doe" template="detailed"]
```

---

## Troubleshooting

### Shortcodes Not Displaying
1. Verify plugin is activated
2. Check LearnDash is properly configured
3. Ensure courses/groups exist and are published
4. Clear cache

### Styling Issues
1. Clear cache
2. Verify Reign theme is active
3. Check for CSS conflicts

### Performance Issues
1. Limit `per_page` to reasonable numbers (12-24)
2. Use specific filters instead of showing all content
3. Optimize course/group images

---

*Shortcodes reference verified against Reign LearnDash Addon source code*