# Reign TutorLMS Addon Documentation

## Welcome to Reign TutorLMS Addon v2.0.0

Transform your TutorLMS into a comprehensive social learning platform with enhanced course displays, multi-platform profile integration (BuddyPress/PeepSo), AJAX progress tracking, and advanced social learning features.

---

## 🚀 Quick Start

New to Reign TutorLMS Addon? Start here:

### [Quick Start Guide →](00-quick-start-guide.md)
Get up and running in 35 minutes with our step-by-step quick start guide.

**What you'll learn:**
- Install and activate the addon
- Configure social integration
- Create your first enhanced course display
- Set up AJAX progress tracking
- Test multi-platform features

---

## 📖 Complete Documentation

### Core Documentation

| Guide | Description | Time to Read |
|-------|-------------|--------------|
| **[Introduction](01-introduction.md)** | Overview of features and capabilities | 10 min |
| **[Installation & Setup](02-installation-setup.md)** | Complete installation guide | 20 min |
| **[Configuration](03-configuration.md)** | Advanced configuration options | 30 min |
| **[Course Customization](04-course-customization.md)** | Design and layout customization | 25 min |

### Advanced Documentation

| Guide | Description | For Who |
|-------|-------------|---------|
| **[Developer Guide](05-developer-guide.md)** | Hooks, filters, and custom development | Developers |
| **[Shortcodes Reference](06-shortcodes-reference.md)** | Complete shortcode documentation | Content Creators |
| **[Troubleshooting](07-troubleshooting.md)** | Common issues and solutions | Administrators |
| **[FAQ](08-faq.md)** | Frequently asked questions | Everyone |

---

## 🎯 Key Features Overview

### Social Learning Integration
- **BuddyPress/BuddyBoss**: Automatic profile tabs and activity integration
- **PeepSo**: Native profile and stream integration
- **Context Detection**: Smart user context awareness
- **Privacy Controls**: Granular privacy and visibility settings

### Enhanced Course Displays
- **2 Powerful Shortcodes**: [reign_tutor_course] and [reign_course_categories]
- **25+ Parameters**: Extensive customization options
- **Multiple Layouts**: Grid, list, carousel, and masonry
- **Responsive Design**: Mobile-optimized displays

### AJAX Features
- **Real-time Progress**: Progress updates without page refresh
- **Dynamic Filtering**: Course filtering with smooth animations
- **Performance Optimized**: Efficient background processing
- **Error Handling**: Graceful fallbacks and user feedback

### Advanced Functionality
- **User Context Awareness**: Profile owner vs visitor detection
- **Status-based Filtering**: All, enrolled, completed, in-progress
- **Template Override System**: Custom template hierarchy
- **Performance Optimization**: Caching and lazy loading

---

## 🛠️ Common Use Cases

### 1. Educational Institution
**Goal**: Create a comprehensive online learning platform with social features

**Setup:**
- Enable BuddyPress integration for student profiles
- Use course grids on homepage and category pages
- Set up instructor profiles with course showcases
- Configure activity streams for course achievements

**Key Features Used:**
- Social profile integration
- Course categorization
- Progress tracking
- Community features

### 2. Corporate Training Platform
**Goal**: Deliver employee training with progress tracking

**Setup:**
- Configure private course access
- Set up department-based course filtering
- Enable progress reporting
- Create manager dashboards

**Key Features Used:**
- Context-aware displays
- Advanced filtering
- Progress tracking
- Privacy controls

### 3. Course Marketplace
**Goal**: Create a platform for selling online courses

**Setup:**
- Enable public course catalogs
- Configure instructor profiles
- Set up course reviews and ratings
- Optimize for mobile shopping

**Key Features Used:**
- Course showcases
- Instructor displays
- Mobile optimization
- Social proof features

### 4. Community Learning Platform
**Goal**: Build a social learning community

**Setup:**
- Full BuddyPress/PeepSo integration
- Enable course discussions
- Set up learning groups
- Configure achievement sharing

**Key Features Used:**
- Social integration
- Activity streams
- Group features
- Community tools

---

## 🔧 Installation Quick Reference

### System Requirements
```yaml
WordPress: 5.8+
PHP: 7.4+ (8.0+ recommended)
TutorLMS: Latest version
Reign Theme: Latest version
License: Valid and activated
```

### Optional Dependencies
```yaml
BuddyPress/BuddyBoss: For social features
PeepSo: For PeepSo integration
Elementor/WPBakery: For page builders
```

### Installation Steps
1. **Download** from WBcom account
2. **Install** via WordPress admin
3. **Activate** the plugin
4. **License** activation in Reign Settings
5. **Configure** in Customizer

---

## 📊 Shortcode Quick Reference

### Course Display Shortcode
```
[reign_tutor_course]
```

**Popular Parameters:**
```
columns="3"                    # Grid columns
show_progress="true"           # Display progress bars
my_courses="true"             # User's enrolled courses
course_status="enrolled"       # Filter by status
user_context="profile_owner"   # Context detection
layout="grid"                 # Display layout
```

### Category Display Shortcode
```
[reign_course_categories]
```

**Popular Parameters:**
```
columns="4"          # Grid columns
show_count="true"    # Display course count
show_image="true"    # Category images
layout="grid"        # Display layout
```

---

## 🎨 Customization Quick Tips

### CSS Classes
```css
.reign-tutor-courses-grid     /* Course grid container */
.reign-tutor-course-card      /* Individual course cards */
.reign-tutor-progress-bar     /* Progress bars */
.reign-course-categories-grid /* Category grid */
```

### Template Override
```
/wp-content/themes/your-theme/
  └── reign-tutorlms/
      ├── course-card.php
      ├── course-progress.php
      └── category-card.php
```

### Hook Examples
```php
// Customize course card content
add_filter('reign_tutor_course_card_content', 'my_custom_content', 10, 3);

// Track progress updates
add_action('reign_tutor_progress_updated', 'my_progress_handler', 10, 3);
```

---

## 🐛 Common Issues & Quick Fixes

### "My Courses" tab not showing
```
✓ Check BuddyPress is active
✓ Verify addon license is active
✓ Clear all caches
✓ Check theme compatibility
```

### AJAX not working
```
✓ Check browser console for errors
✓ Verify nonce configuration
✓ Test with default theme
✓ Check server AJAX settings
```

### Shortcodes not rendering
```
✓ Verify shortcode syntax
✓ Check required parameters
✓ Ensure TutorLMS is active
✓ Test plugin conflicts
```

---

## 📞 Support & Resources

### Official Support
- **📧 Email**: support@wbcomdesigns.com
- **🎫 Support Portal**: wbcomdesigns.com/support/
- **📚 Documentation**: docs.wbcomdesigns.com

### Community Resources
- **💬 Facebook Group**: facebook.com/groups/wbcom
- **🗨️ Forums**: Community discussions and tips
- **📹 Video Tutorials**: YouTube channel and member area

### Developer Resources
- **🔧 API Documentation**: Developer hooks and filters
- **💻 Code Examples**: GitHub repository
- **🛠️ Custom Development**: Professional services available

---

## 🔄 Update Information

### Current Version: 2.0.0
- Enhanced social integration
- Improved AJAX functionality
- Extended shortcode parameters
- Performance optimizations
- Mobile enhancements

### Update Frequency
- **Minor Updates**: Monthly (bug fixes, small features)
- **Major Updates**: Quarterly (new features, improvements)
- **Security Updates**: As needed (immediate patches)

### Changelog
View detailed changelog and version history in your WBcom account.

---

## 🎯 What's Next?

### Immediate Next Steps
1. **[Start with Quick Guide](00-quick-start-guide.md)** - Get running in 35 minutes
2. **[Configure Features](03-configuration.md)** - Set up advanced options
3. **[Customize Display](04-course-customization.md)** - Make it yours

### Advanced Usage
1. **[Master Shortcodes](06-shortcodes-reference.md)** - Learn all parameters
2. **[Custom Development](05-developer-guide.md)** - Extend functionality
3. **[Optimize Performance](07-troubleshooting.md)** - Best practices

### Get Help
1. **[Check FAQ](08-faq.md)** - Common questions answered
2. **[Troubleshooting](07-troubleshooting.md)** - Fix common issues
3. **[Contact Support](mailto:support@wbcomdesigns.com)** - Get professional help

---

## 🏆 Success Stories

> "Reign TutorLMS Addon transformed our corporate training platform. The social integration and progress tracking features increased course completion rates by 40%."
>
> *– Sarah Johnson, Learning & Development Manager*

> "The AJAX features and mobile optimization made our course marketplace feel like a modern app. Student engagement is through the roof!"
>
> *– Mike Chen, EdTech Startup Founder*

> "Perfect integration with BuddyPress. Our learning community is now truly social with automatic profile integration and activity sharing."
>
> *– Dr. Lisa Rodriguez, Online University*

---

**Ready to get started?** [Begin with the Quick Start Guide →](00-quick-start-guide.md)

**Need help?** [Contact our support team](mailto:support@wbcomdesigns.com) - we're here to help!