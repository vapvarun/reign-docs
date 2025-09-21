# Reign LearnDash Addon - Introduction

## What is Reign LearnDash Addon?

Reign LearnDash Addon integrates LearnDash LMS with the Reign WordPress theme, providing enhanced course layouts, custom shortcodes, and BuddyPress social learning features.

## Core Features (Verified)

### Course Display Enhancement
- **6 Custom Shortcodes**: Display courses and groups with multiple templates
- **Archive Templates**: Enhanced course and group archive pages
- **Custom Layouts**: Professional course card designs with multiple templates

### Shortcodes Included
- `[modern_courses]` / `[reign_courses]` - Display courses with filtering and templates
- `[modern_groups]` - Display LearnDash groups with customization options
- 3 tab content shortcodes for course pages

### Theme Integration
- **Archive Customization**: Configure course/group archive headers and layouts
- **Groups Archive Settings**: Title, columns, template style, search/filter options
- **Sidebar Controls**: Left/right sidebar configuration for archives

### BuddyPress Features
- Enhanced social learning when BuddyPress is active
- Course review system integration
- Learning activity streams

## Technical Requirements

| Requirement | Details |
|-------------|---------|
| **WordPress** | 4.0+ |
| **Reign Theme** | Required (active) |
| **LearnDash** | Required |
| **BuddyPress** | Optional (for social features) |

## What This Addon Provides

### Template Enhancements
- Professional course archive layouts
- Enhanced group display templates
- Course review system integration
- Mobile-responsive designs

### Customization Options
- Multiple course/group templates (classic, minimal, premium, detailed)
- Configurable columns and pagination
- Filter and search functionality
- Progress tracking displays

### Developer Features
- Template override system
- Custom hooks and filters
- AJAX-powered interactions
- Gutenberg block support

## Plugin Structure (Verified)

```
reign-learndash-addon/
├── admin/                  # Admin settings
├── assets/                 # CSS, JS, images
├── buddypress/            # BuddyPress integration
├── course-review/         # Course review system
├── general/               # Core hooks and functions
├── includes/              # Shortcode classes
├── learndash/            # LearnDash integration
├── ld-dashboard/         # Dashboard enhancements
├── templates/            # Template files
└── reign-learndash-addon.php
```

## Next Steps

- [Quick Start Guide](00-quick-start-guide.md) - Get started quickly
- [Installation Guide](02-installation-setup.md) - Detailed installation
- [Configuration Guide](03-configuration.md) - Settings and customization
- [Shortcodes Reference](06-shortcodes-reference.md) - Complete shortcode guide

---

*Introduction verified against Reign LearnDash Addon source code*