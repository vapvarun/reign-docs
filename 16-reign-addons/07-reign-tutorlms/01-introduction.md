# Reign TutorLMS Addon - Introduction

## What is Reign TutorLMS Addon?

Reign TutorLMS Addon v2.0.0 is a focused theme integration extension that enhances TutorLMS with the Reign theme, providing enhanced course displays, multi-platform profile integration (BuddyPress/BuddyBoss/PeepSo), progress tracking, and platform-agnostic social learning features.

## Core Features (Comprehensive Analysis)

### 1. Enhanced Course Display
- **[reign_tutor_course] Shortcode**: Advanced course display with extensive parameters
- **Profile Context Awareness**: Automatically detects BuddyPress, PeepSo, and standard profile contexts
- **Progress Visualization**: AJAX-powered course progress tracking with visual indicators
- **Responsive Grid Layouts**: Customizable columns (2, 3, or 4) with mobile optimization

### 2. Multi-Platform Profile Integration
- **BuddyPress/BuddyBoss Support**: Automatic "My Courses" tab integration
- **PeepSo Compatibility**: Profile tab integration with PeepSo social platform
- **Universal Detection**: Smart platform detection and appropriate integration
- **Context-Aware Display**: Shows profile owner's courses, not logged-in user's courses

### 3. Advanced Course Filtering & Display
- **User-Specific Courses**: `my_courses="yes"` parameter for enrolled courses
- **Progress Integration**: `show_progress="yes"` for visual progress tracking
- **Course Status Filtering**: all, completed, in_progress, not_started
- **Layout Customization**: Multiple layout styles (default, grid, list)
- **Instructor Controls**: Show/hide instructor information

### 4. Course Categories Enhancement
- **[reign_course_categories] Shortcode**: Professional category display
- **Grid Layout Support**: Configurable columns (1-6) for category showcase
- **Category Thumbnails**: Visual category representation with images
- **Course Count Display**: Show number of courses per category

## Technical Specifications

| Specification | Details |
|--------------|----------|
| **Version** | 2.0.0 |
| **Author** | Wbcom Designs |
| **WordPress** | 5.8+ |
| **TutorLMS** | Latest version required |
| **Reign Theme** | Required (active) |
| **BuddyPress** | Optional (for profile integration) |
| **PeepSo** | Optional (for profile integration) |

## Key Benefits

### For Course Creators
- **Enhanced Course Presentation**: Professional course displays with Reign theme integration
- **Social Platform Integration**: Automatic profile integration across multiple platforms
- **Progress Visualization**: Student engagement tracking with visual progress indicators
- **Flexible Display Options**: Multiple shortcode parameters for customized presentations

### For Students
- **Social Learning Experience**: Profile integration with BuddyPress/PeepSo for community learning
- **Progress Tracking**: Visual course progress in profiles and course displays
- **Enhanced Course Discovery**: Improved category displays and course filtering
- **Mobile-Optimized Learning**: Responsive design for learning on any device

### For Site Administrators
- **Platform Flexibility**: Works with BuddyPress, PeepSo, or standard WordPress
- **Easy Integration**: Automatic detection and setup for social platforms
- **Performance Optimization**: AJAX progress loading and efficient queries
- **Developer-Friendly**: Extensive hooks and filters for customization

## Plugin Architecture

### Core Components
- **Shortcode System**: 2 specialized shortcodes with extensive parameters
- **Profile Integration**: Multi-platform social profile enhancement
- **Progress System**: AJAX-powered progress tracking
- **Admin Interface**: Centralized settings with platform detection

### Advanced Features
- **Context Detection**: Smart user detection across different platforms
- **AJAX Integration**: Dynamic progress loading without page refresh
- **Security Features**: Proper nonce verification and data sanitization
- **Performance Optimized**: Efficient database queries and caching

## Development Features

### For Developers
- **Extensive Hooks**: Multiple filters and actions for customization
- **Context-Aware Functions**: Smart user detection utilities
- **Security Standards**: Proper WordPress coding standards compliance
- **Template Integration**: CSS and JavaScript enhancements

### Platform Integration
- **BuddyPress Integration**: Uses `bp_core_new_nav_item()` for profile tabs
- **PeepSo Integration**: Uses `peepso_navigation_profile` filter
- **Universal Compatibility**: Works without social platforms as well
- **Profile Context Detection**: Automatic user context awareness

## Social Learning Features

### Profile Enhancement
- **"My Courses" Tab**: Dedicated learning section in user profiles
- **Progress Display**: Course completion visualization in social profiles
- **User Context Awareness**: Shows appropriate user's courses in profile views
- **Multi-Platform Support**: Consistent experience across social platforms

### Course Display Enhancement
- **Enhanced Course Cards**: Professional styling with Reign theme integration
- **Progress Integration**: Visual progress bars for enrolled courses
- **Category Showcases**: Professional category displays with thumbnails
- **Responsive Design**: Mobile-optimized course presentations

## Next Steps

1. [Installation Guide](02-installation-setup.md)
2. [Configuration Guide](03-configuration.md)
3. [Course Creation](04-course-creation.md)
4. [Developer Guide](05-developer-guide.md)