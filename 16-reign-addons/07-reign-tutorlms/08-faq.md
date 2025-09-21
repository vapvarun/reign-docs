# Reign TutorLMS Addon - FAQ

## Overview

This comprehensive FAQ addresses the most frequently asked questions about Reign TutorLMS Addon v2.0.0, covering installation, features, social integration, troubleshooting, and customization.

---

## General Questions

### Q1: What is Reign TutorLMS Addon and what does it do?

**A:** Reign TutorLMS Addon v2.0.0 is a comprehensive theme integration extension that enhances TutorLMS with advanced social learning features, including:

- **Multi-platform Integration**: Works with BuddyPress, BuddyBoss, and PeepSo
- **Enhanced Course Displays**: 2 powerful shortcodes with 25+ parameters each
- **AJAX Progress Tracking**: Real-time progress updates without page refresh
- **Context-Aware Content**: Shows different content based on user context (profile owner vs visitor)
- **Advanced Filtering**: Status-based course filtering (enrolled, completed, in-progress)
- **Social Profile Integration**: Automatic "My Courses" tabs in user profiles

### Q2: Is this just a styling plugin or does it add real functionality?

**A:** This is a comprehensive functionality plugin that goes far beyond styling. It adds:
- Advanced shortcode system with extensive parameters
- Social platform integration with automatic detection
- AJAX-powered real-time features
- Context-aware user detection
- Course filtering and management
- Template override system
- Performance optimization features

### Q3: What's the difference between this and the basic TutorLMS plugin?

**A:** While TutorLMS provides the core LMS functionality, Reign TutorLMS Addon adds:
- **Social Learning**: BuddyPress/PeepSo integration
- **Enhanced Display**: Advanced course grids and layouts
- **User Context**: Smart detection of profile owners vs visitors
- **AJAX Features**: Real-time progress updates
- **Advanced Shortcodes**: More parameters and flexibility
- **Theme Integration**: Seamless Reign theme integration

---

## Installation and Setup

### Q4: What are the system requirements?

**A:** System requirements include:

**Required:**
- WordPress 5.8 or higher
- PHP 7.4 or higher (PHP 8.0+ recommended)
- TutorLMS plugin (latest version)
- Reign Theme (latest version)
- Valid license key

**Optional for Enhanced Features:**
- BuddyPress or BuddyBoss (for social profile integration)
- PeepSo (for PeepSo platform integration)
- Elementor or WPBakery (for page builder compatibility)

### Q5: Can I use this addon without BuddyPress or PeepSo?

**A:** Yes! The addon works perfectly without social platforms. You'll get:
- Enhanced course display shortcodes
- Advanced filtering options
- AJAX progress tracking
- Context-aware content display
- All theme integration features

When social platforms are detected, additional features are automatically enabled.

### Q6: Do I need coding knowledge to use this addon?

**A:** No coding knowledge required for basic usage:
- **Installation**: Standard WordPress plugin installation
- **Configuration**: User-friendly admin interface
- **Shortcodes**: Simple copy-paste usage
- **Customization**: Visual customizer options

Advanced users can use hooks and filters for deeper customization.

### Q7: How do I activate my license?

**A:** License activation steps:
1. Purchase from WBcom Designs
2. Download the plugin ZIP file
3. Install and activate the plugin
4. Go to **Reign Settings → License**
5. Find "TutorLMS Addon" section
6. Enter license key (format: XXXX-XXXX-XXXX-XXXX)
7. Click "Activate License"
8. Look for green "Active" status

---

## Features and Functionality

### Q8: What shortcodes are available and what do they do?

**A:** Two main shortcodes are available:

**1. [reign_tutor_course]** - Main course display shortcode
- 25+ parameters for customization
- Supports grid, list, carousel layouts
- User context detection
- Progress tracking integration
- Advanced filtering options

**2. [reign_course_categories]** - Category display shortcode
- Professional category showcases
- Grid layouts (1-6 columns)
- Image and count display
- Hierarchical support

### Q9: How does the context-aware feature work?

**A:** Context detection automatically determines:

- **Profile Owner**: User viewing their own profile
  - Shows all enrolled courses
  - Displays detailed progress
  - Enables course management

- **Profile Visitor**: User viewing someone else's profile
  - Shows public courses only
  - Respects privacy settings
  - Limited information display

- **Guest User**: Not logged in
  - Shows course catalog
  - No personal information
  - Enrollment CTAs displayed

### Q10: What social platforms are supported?

**A:** Currently supported platforms:

**BuddyPress/BuddyBoss:**
- Automatic profile tab creation
- Activity stream integration
- Group course management
- Privacy controls

**PeepSo:**
- Profile navigation integration
- Stream post creation
- Widget support
- Privacy integration

**Standard WordPress:**
- Works without social platforms
- User profile enhancements
- Basic social features

### Q11: How does AJAX progress tracking work?

**A:** AJAX progress tracking provides:
- **Real-time Updates**: Progress updates without page refresh
- **Visual Feedback**: Smooth animations and transitions
- **Performance Optimized**: Efficient background processing
- **Error Handling**: Graceful fallbacks if AJAX fails
- **Cross-platform**: Works on desktop and mobile

---

## Customization Questions

### Q12: Can I customize the appearance of course displays?

**A:** Yes! Multiple customization options:

**Via Customizer:**
- **Appearance → Customize → Reign TutorLMS**
- Course grid layouts
- Progress bar styles
- Color schemes
- Mobile optimization

**Via CSS:**
- Custom CSS classes provided
- Theme-compatible styling
- Responsive design support

**Via Templates:**
- Override plugin templates in your theme
- Custom template hierarchy
- Developer-friendly hooks

### Q13: How do I change the course grid layout?

**A:** Multiple ways to customize layouts:

**Shortcode Parameters:**
```
[reign_tutor_course layout="grid" columns="4"]
[reign_tutor_course layout="list"]
[reign_tutor_course layout="carousel"]
```

**Customizer Settings:**
- **Appearance → Customize → Reign TutorLMS → Course Display**
- Choose columns (1-6)
- Select layout style
- Configure mobile behavior

### Q14: Can I show only specific courses?

**A:** Yes! Advanced filtering options:

**By User Status:**
```
[reign_tutor_course my_courses="true" course_status="enrolled"]
[reign_tutor_course course_status="completed"]
[reign_tutor_course course_status="in_progress"]
```

**By Category/Instructor:**
```
[reign_tutor_course course_category="web-development"]
[reign_tutor_course instructor_id="45"]
```

**By User Context:**
```
[reign_tutor_course user_context="profile_owner"]
[reign_tutor_course user_id="123"]
```

### Q15: How do I customize progress bar appearance?

**A:** Progress bar customization options:

**Style Options:**
```
[reign_tutor_course progress_style="bar"]     # Default bar
[reign_tutor_course progress_style="circle"]  # Circular progress
[reign_tutor_course progress_style="percentage"] # Text only
```

**CSS Customization:**
```css
.reign-tutor-progress-bar {
    height: 10px;
    background: #f0f0f0;
    border-radius: 5px;
}

.progress-fill {
    background: linear-gradient(90deg, #007cba, #005a87);
}
```

---

## Social Integration Questions

### Q16: How do I enable BuddyPress integration?

**A:** BuddyPress integration is automatic:

1. **Install BuddyPress** (if not already installed)
2. **Activate required components**:
   - User Profiles
   - Activity Streams
3. **Activate Reign TutorLMS Addon**
4. **Check profile pages** - "My Courses" tab should appear automatically

If not working, see troubleshooting guide.

### Q17: Can users control course privacy in their profiles?

**A:** Yes! Privacy controls include:

**BuddyPress:**
- Uses BuddyPress privacy settings
- Respects friend/public visibility
- Admin can set defaults

**PeepSo:**
- Integrates with PeepSo privacy system
- Per-user privacy controls
- Activity stream privacy

**Settings Location:**
- User profile → Privacy Settings
- Course-specific privacy options
- Global admin controls

### Q18: How are course activities shown in social streams?

**A:** Activity types include:

**Course Enrollment:**
- "John enrolled in JavaScript Basics"
- Shows course thumbnail and link

**Course Completion:**
- "Jane completed Advanced WordPress with 95% score"
- Includes completion badge

**Lesson Progress:**
- "Mike completed Lesson 3 in Web Development"
- Shows lesson link and course context

**Achievements:**
- "Sarah earned JavaScript Expert certificate"
- Displays achievement badge

### Q19: Can I disable social features?

**A:** Yes! Multiple control levels:

**Global Disable:**
- Deactivate BuddyPress/PeepSo plugins
- Social features automatically disabled

**Selective Disable:**
- **Customizer → Reign TutorLMS → Social Integration**
- Toggle specific features on/off
- Activity stream controls
- Profile integration controls

**User-Level Control:**
- Users can set privacy preferences
- Opt-out of activity sharing
- Control profile visibility

---

## Performance Questions

### Q20: Does this addon slow down my site?

**A:** No, the addon is optimized for performance:

**Performance Features:**
- **Efficient Queries**: Optimized database queries
- **Smart Caching**: Intelligent caching system
- **Lazy Loading**: Images load on demand
- **AJAX Optimization**: Minimal server requests
- **Mobile Optimized**: Fast mobile performance

**Best Practices:**
- Use caching plugins (WP Rocket, W3 Total Cache)
- Optimize images
- Use CDN for course media
- Regular database optimization

### Q21: How can I optimize course loading speed?

**A:** Performance optimization tips:

**Shortcode Optimization:**
```
[reign_tutor_course posts_per_page="12" cache_results="true"]
[reign_tutor_course lazy_load="true" ajax_load="true"]
```

**Image Optimization:**
- Use appropriate image sizes
- Enable lazy loading
- Compress course images
- Use WebP format when possible

**Caching Configuration:**
- Cache course catalog pages
- Exclude user-specific pages
- Cache AJAX responses (short duration)

### Q22: What about mobile performance?

**A:** Mobile optimization includes:

**Responsive Design:**
- Mobile-first approach
- Touch-optimized interfaces
- Adaptive layouts

**Performance Features:**
- Reduced resource loading
- Optimized images
- Efficient AJAX calls
- Progressive loading

**Mobile-Specific Settings:**
```
[reign_tutor_course columns="1" layout="list" thumbnail_size="small"]
```

---

## Troubleshooting Questions

### Q23: "My Courses" tab is not showing in profiles. Why?

**A:** Common causes and solutions:

**Check BuddyPress/PeepSo:**
- Ensure social platform is active
- Verify "User Profiles" component enabled
- Check for theme compatibility

**Clear Caches:**
- Clear all website caches
- Clear browser cache
- Reset user sessions

**Plugin Conflicts:**
- Deactivate other plugins temporarily
- Test with default theme
- Check for JavaScript errors

**Manual Fix:**
See troubleshooting guide for detailed solutions.

### Q24: Progress bars are not updating. How to fix?

**A:** AJAX troubleshooting steps:

**Check Browser Console:**
- Open developer tools (F12)
- Look for JavaScript errors
- Check network tab for failed requests

**Verify AJAX Setup:**
- Ensure WordPress AJAX is enabled
- Check nonce verification
- Test with different browsers

**Server Configuration:**
- Verify PHP settings
- Check server error logs
- Test AJAX endpoint directly

### Q25: Courses are showing for wrong users. What's wrong?

**A:** Context detection issues:

**User Context Debug:**
- Check if user is logged in correctly
- Verify profile URL structure
- Clear user session data

**Privacy Settings:**
- Check course privacy settings
- Verify user permissions
- Review social platform privacy

**Cache Issues:**
- Clear user-specific caches
- Reset context detection cache
- Test in incognito mode

### Q26: Shortcodes are not working. How to fix?

**A:** Shortcode troubleshooting:

**Syntax Check:**
```
✓ Correct: [reign_tutor_course columns="3"]
✗ Wrong: [reign_tutor_course columns=3]
✗ Wrong: [reign-tutor-course columns="3"]
```

**Plugin Status:**
- Ensure addon is activated
- Check license is active
- Verify TutorLMS is working

**Compatibility:**
- Test with default theme
- Check for plugin conflicts
- Verify WordPress version

---

## Advanced Usage Questions

### Q27: Can I create custom course displays programmatically?

**A:** Yes! Multiple approaches:

**PHP Integration:**
```php
// Use shortcode in templates
echo do_shortcode('[reign_tutor_course my_courses="true"]');

// Dynamic parameters
$user_id = get_current_user_id();
echo do_shortcode("[reign_tutor_course user_id='{$user_id}']");
```

**Custom Functions:**
```php
// Create custom display function
function my_custom_courses($args = array()) {
    $defaults = array(
        'columns' => 3,
        'show_progress' => true
    );
    $args = wp_parse_args($args, $defaults);
    return do_shortcode('[reign_tutor_course ' . build_shortcode_atts($args) . ']');
}
```

### Q28: How do I add custom fields to course displays?

**A:** Use available hooks:

**Filter Course Card Content:**
```php
function add_custom_course_field($content, $course_id, $args) {
    $custom_field = get_post_meta($course_id, '_my_custom_field', true);
    if ($custom_field) {
        $content .= '<div class="custom-field">' . $custom_field . '</div>';
    }
    return $content;
}
add_filter('reign_tutor_course_card_content', 'add_custom_course_field', 10, 3);
```

### Q29: Can I integrate with other social platforms?

**A:** Yes, with custom development:

**Hook into Social System:**
```php
// Add custom social platform
function add_custom_social_integration() {
    // Detect your social platform
    if (class_exists('Your_Social_Platform')) {
        // Add integration code
        add_action('your_platform_profile_tabs', 'add_courses_tab');
    }
}
add_action('init', 'add_custom_social_integration');
```

**Use Available Filters:**
```php
// Customize social activity creation
function custom_social_activity($activity_data, $user_id, $course_id) {
    // Modify activity data for your platform
    return $activity_data;
}
add_filter('reign_tutor_social_activity_data', 'custom_social_activity', 10, 3);
```

### Q30: How do I create custom widgets?

**A:** Extend the widget system:

```php
class My_Custom_Courses_Widget extends WP_Widget {
    public function widget($args, $instance) {
        // Your custom widget code
        echo do_shortcode('[reign_tutor_course columns="2"]');
    }
}

function register_my_widget() {
    register_widget('My_Custom_Courses_Widget');
}
add_action('widgets_init', 'register_my_widget');
```

---

## Licensing and Support

### Q31: What happens if my license expires?

**A:** License expiration effects:

**Immediate:**
- Plugin continues working
- All features remain functional
- No feature restrictions

**Long-term:**
- No automatic updates
- No priority support
- Security updates unavailable

**Renewal Benefits:**
- Latest features and improvements
- Security patches
- Priority support access
- New integrations

### Q32: Can I use the addon on multiple sites?

**A:** License terms depend on your purchase:

**Single Site License:**
- One production site
- Unlimited development/staging sites
- License tied to domain

**Multi-Site License:**
- Multiple production sites (as per license)
- Unlimited development/staging
- Bulk license management

**Developer License:**
- Unlimited client sites
- White-label options
- Extended support

### Q33: How do I get support?

**A:** Multiple support channels:

**Official Support:**
- 📧 Email: support@wbcomdesigns.com
- 🎫 Ticket System: wbcomdesigns.com/support/
- 📚 Documentation: docs.wbcomdesigns.com

**Community Support:**
- 💬 Facebook Group: facebook.com/groups/wbcom
- 🗨️ Forums: Community discussions
- 📹 Video Tutorials: YouTube channel

**Priority Support:**
- Active license holders get priority
- Faster response times
- Direct developer access

---

## Migration and Compatibility

### Q34: Can I migrate from other LMS plugins?

**A:** Yes, but requires TutorLMS migration first:

**Migration Steps:**
1. **Migrate to TutorLMS** using available migration tools
2. **Install Reign TutorLMS Addon**
3. **Configure addon settings**
4. **Test all functionality**
5. **Update shortcodes and displays**

**Data Preservation:**
- Course content preserved
- User enrollments maintained
- Progress data migrated
- Social features added

### Q35: Is it compatible with page builders?

**A:** Yes! Compatible with major page builders:

**Elementor:**
- Use shortcode widget
- Custom Elementor widgets available
- Full visual editing support

**WPBakery:**
- Shortcode mapping included
- Visual composer elements
- Drag-and-drop support

**Gutenberg:**
- Shortcode block support
- Custom Gutenberg blocks planned
- Block editor compatibility

**Usage Example:**
```
Add shortcode widget/block:
[reign_tutor_course columns="3" show_progress="true"]
```

### Q36: What about theme compatibility?

**A:** Broad theme compatibility:

**Reign Theme:**
- Perfect integration (designed for Reign)
- All features fully supported
- Optimal performance

**Other Themes:**
- Works with most WordPress themes
- May need minor CSS adjustments
- Template override system available

**Compatibility Testing:**
- Test with your theme before purchase
- Use staging site for testing
- Contact support for theme-specific issues

---

## Future Development

### Q37: What new features are planned?

**A:** Upcoming features include:

**Short-term (next 3 months):**
- Additional social platform integrations
- Enhanced mobile features
- More shortcode parameters
- Performance improvements

**Medium-term (6 months):**
- Custom Gutenberg blocks
- Advanced analytics integration
- Gamification features
- AI-powered recommendations

**Long-term (1 year):**
- Mobile app integration
- Advanced social learning tools
- Enterprise features
- Multi-language enhancements

### Q38: How often is the addon updated?

**A:** Regular update schedule:

**Minor Updates:** Monthly
- Bug fixes
- Small feature additions
- Compatibility updates

**Major Updates:** Quarterly
- New features
- Performance improvements
- UI/UX enhancements

**Security Updates:** As needed
- Immediate security patches
- Compatibility fixes
- Critical bug fixes

### Q39: Can I request new features?

**A:** Yes! Feature request process:

**Channels:**
- Support tickets
- Community forums
- Direct developer contact
- User feedback surveys

**Priority Factors:**
- User demand
- Technical feasibility
- Alignment with roadmap
- Resource availability

**Response:**
- All requests reviewed
- Feasibility assessment
- Timeline estimation
- Implementation updates

---

## Best Practices

### Q40: What are the recommended settings for optimal performance?

**A:** Optimal configuration:

**Course Display:**
```yaml
Posts per page: 12-15 (not too many)
Columns: 3 (desktop), 1 (mobile)
Enable AJAX: Yes
Enable lazy loading: Yes
Cache results: Yes
```

**Social Integration:**
```yaml
Activity types: Selective (not all)
Privacy: User-controlled
Profile tabs: Minimal set
Cache activity: 15 minutes
```

**Performance:**
```yaml
Image optimization: Enabled
Lazy loading: Enabled
AJAX debouncing: 300ms
Cache duration: 15 minutes
Mobile optimization: Enabled
```

---

**Still Have Questions?**

📧 **Email Support:** support@wbcomdesigns.com
📚 **Documentation:** docs.wbcomdesigns.com
💬 **Community:** facebook.com/groups/wbcom
🎥 **Video Tutorials:** Available in member area

**Related Documentation:**
- [Installation Guide](02-installation-setup.md)
- [Configuration Guide](03-configuration.md)
- [Troubleshooting Guide](07-troubleshooting.md)
- [Developer Guide](05-developer-guide.md)