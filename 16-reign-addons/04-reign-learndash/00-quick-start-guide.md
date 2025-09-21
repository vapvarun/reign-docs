# Reign LearnDash Addon - Quick Start Guide

## What This Addon Provides

Reign LearnDash Addon enhances LearnDash with Reign theme integration, providing:

**Core Features (Verified):**
- Professional course and group layouts
- 6 custom shortcodes for displaying courses/groups
- Theme customization settings for LearnDash archives
- Enhanced templates and styling
- BuddyPress integration features

---

## Prerequisites

Required:
- ✅ WordPress 4.0+
- ✅ Reign Theme activated
- ✅ LearnDash LMS plugin
- ✅ Reign LearnDash Addon

Optional:
- BuddyPress (for enhanced social learning)

---

## Installation Steps

### Step 1: Install the Addon

1. **Upload via WordPress:**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   → Select reign-learndash-addon.zip
   → Install Now → Activate
   ```

2. **Verify Installation:**
   - Check Plugins page - "Reign LearnDash Addon" should be active
   - LearnDash templates should now use Reign styling

### Step 2: Configure Basic Settings

The addon works automatically with LearnDash. Available customization:

**Archive Pages:**
- Course archive layout and sidebar options
- Group archive customization settings
- Header images for course/group archives

**Groups Archive Settings (via Customizer):**
- Title and description
- Columns (default: 3)
- Template style (default: minimal)
- Search, filters, sorting options
- Pagination and view switcher

---

## Available Shortcodes

The addon provides 6 shortcodes (verified):

### Course Display Shortcodes

#### [modern_courses] / [reign_courses]
Display courses with modern styling:
```
[modern_courses]
[reign_courses]
```

### Group Display Shortcode

#### [modern_groups]
Display LearnDash groups:
```
[modern_groups]
```

### Tab Content Shortcodes (for course pages)

#### [reign_ld_pro_comments_tab_content]
Display comments tab content in courses

#### [reign_ld_pro_instructor_tab_content]
Display instructor information tab

#### [reign_ld_pro_course_content_tab_content]
Display course content tab

**Note:** Tab shortcodes are typically used in custom templates rather than pages/posts.

## Quick Test

### Verify Installation Works

1. **Test Course Shortcode:**
   Create a test page and add:
   ```
   [modern_courses]
   ```
   Should display courses with Reign styling.

2. **Check Archive Pages:**
   - Visit `/courses/` - should use enhanced Reign template
   - Visit `/groups/` - should show customized layout

3. **Verify Styling:**
   Course and group pages should match your Reign theme design.

---

## Common Usage

### Display Courses on Homepage
```
[modern_courses]
```
or
```
[reign_courses]
```

### Display Groups
```
[modern_groups]
```

### Customize Groups Archive
- Go to Appearance → Customize
- Look for LearnDash Groups settings
- Adjust title, columns, template style
- Configure search, filters, pagination

---

## Troubleshooting

### Shortcodes Not Working
1. Verify plugin is activated
2. Check LearnDash is properly configured
3. Ensure courses/groups exist and are published

### Styling Issues
1. Clear cache
2. Verify Reign theme is active
3. Check for CSS conflicts

### Template Issues
1. Ensure LearnDash is properly installed
2. Check permalink settings
3. Clear cache and test again

---

## Next Steps

For detailed configuration and customization:
- [Configuration Guide](03-configuration.md) - Theme settings
- [Course Customization](04-course-customization.md) - Appearance options
- [Developer Guide](05-developer-guide.md) - Hooks and filters
- [Shortcodes Reference](06-shortcodes-reference.md) - Complete shortcode guide

---

*Quick Start Guide verified against Reign LearnDash Addon source code*