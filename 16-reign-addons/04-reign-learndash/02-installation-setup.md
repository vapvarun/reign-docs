# Reign LearnDash Addon - Installation & Setup

## Prerequisites

Required:
- ✅ WordPress 4.0+
- ✅ Reign Theme (activated)
- ✅ LearnDash LMS plugin
- ✅ Reign LearnDash Addon files

Optional:
- BuddyPress (for social learning features)

---

## Installation

### Step 1: Install the Plugin

1. **Upload via WordPress Admin:**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   → Select reign-learndash-addon.zip
   → Install Now → Activate
   ```

2. **Alternative: FTP Upload**
   ```
   Extract ZIP → Upload to /wp-content/plugins/reign-learndash-addon/
   Activate from WordPress Admin
   ```

### Step 2: Verify Installation

1. **Check Plugin Status:**
   - Go to Plugins page
   - "Reign LearnDash Addon" should be active

2. **Test Shortcodes:**
   Create a test page and add:
   ```
   [modern_courses]
   ```
   Should display courses with Reign styling.

---

## Configuration

### Archive Settings (Optional)

The addon automatically enhances LearnDash archives. For groups archive customization:

1. **Go to Appearance → Customize**
2. **Look for LearnDash Groups settings**
3. **Configure options:**
   - Archive title and description
   - Number of columns (default: 3)
   - Template style (default: minimal)
   - Enable/disable search, filters, sorting
   - Pagination options

### Using Shortcodes

#### Display Courses
```
[modern_courses]
[modern_courses per_page="6" columns="2" template="premium"]
```

#### Display Groups
```
[modern_groups]
[modern_groups columns="4" show_search="no"]
```

---

## Verification

### Test the Installation

1. **Archive Pages:**
   - Visit `/courses/` - should use enhanced Reign template
   - Visit `/groups/` - should show customized layout

2. **Shortcodes:**
   - Add `[modern_courses]` to a test page
   - Should display courses with professional styling

3. **Styling:**
   - Course and group pages should match your Reign theme design
   - Mobile responsive layouts should work

---

## Troubleshooting

### Common Issues

#### Shortcodes Not Working
1. Verify plugin is activated
2. Check LearnDash is properly configured
3. Ensure courses/groups exist and are published

#### Styling Issues
1. Clear cache
2. Verify Reign theme is active
3. Check for CSS conflicts

#### Template Issues
1. Ensure LearnDash is properly installed
2. Check permalink settings
3. Clear cache and test again

---

## Next Steps

- [Configuration Guide](03-configuration.md) - Detailed settings
- [Course Customization](04-course-customization.md) - Appearance options
- [Shortcodes Reference](06-shortcodes-reference.md) - Complete shortcode guide

---

*Installation guide verified against Reign LearnDash Addon source code*