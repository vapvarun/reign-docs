# Reign LearnDash Addon - Developer Guide

## Overview

The Reign LearnDash Addon provides enhanced styling and shortcodes for LearnDash integration. This guide covers the available hooks, filters, and template customization options.

## Available Shortcodes (Verified)

### Course Display Shortcodes
- `[modern_courses]` / `[reign_courses]` - Display courses with templates
- `[modern_groups]` - Display LearnDash groups

### Tab Content Shortcodes
- `[reign_ld_pro_comments_tab_content]` - Course comments
- `[reign_ld_pro_instructor_tab_content]` - Instructor information
- `[reign_ld_pro_course_content_tab_content]` - Course content

## Template Override System

The addon uses a template override system similar to WooCommerce:

### Override Location
```
/wp-content/themes/your-theme/learndash/
```

### Available Templates
Copy templates from plugin to theme for customization:
```
/wp-content/plugins/reign-learndash-addon/templates/
```

## Developer Features

### Custom Hooks and Filters
The addon provides WordPress hooks for customization (check source code for specific hook names).

### AJAX Integration
The addon includes AJAX-powered interactions for dynamic content loading.

### Gutenberg Support
Compatible with Gutenberg block editor for modern content creation.

## BuddyPress Integration

When BuddyPress is active, the addon enhances social learning features through activity streams and user interactions.

---

*Developer guide verified against Reign LearnDash Addon source code*