# Reign LifterLMS Addon - Quick Start Guide

## What This Addon Provides

Reign LifterLMS Addon v2.4.1 is a comprehensive learning management system integration providing advanced course layouts, BuddyPress social learning features, custom widgets, enhanced student dashboards, and extensive customization options for creating professional online learning platforms.

**Core Features (Comprehensive):**
- 2 advanced shortcodes for courses and instructors
- 7 specialized learning widgets
- BuddyPress social learning integration
- Enhanced student dashboard with tabbed interface
- Interactive review and rating system
- Distraction-free learning mode
- Template override system

---

## Prerequisites

Required:
- ✅ WordPress 5.8+
- ✅ Reign Theme activated
- ✅ LifterLMS plugin
- ✅ Reign LifterLMS Addon license

Optional:
- BuddyPress (for social learning features)
- WooCommerce (for LifterLMS WooCommerce extension)

---

## Installation Steps

### Step 1: Install the Addon

1. **Upload via WordPress:**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   → Select reign-lifterlms-addon.zip
   → Install Now → Activate
   ```

2. **Verify Installation:**
   - Check Plugins page - "Reign LifterLMS Addon" should be active
   - LifterLMS courses should now use enhanced Reign styling

---

## Quick Setup & Testing

### Step 1: Test Basic Course Display

Add this shortcode to any page to test basic functionality:
```
[reign_lifterlms_courses]
```

### Step 2: Test Advanced Features

Try the advanced course display with slider and category filtering:
```
[reign_lifterlms_courses per_row="3" enable_slider="true" category="web-development"]
```

### Step 3: Test Instructor Display

Display instructors with social media integration:
```
[reign_lifterlms_instructors per_row="4" enable_slider="true"]
```

### Step 4: Enable BuddyPress Features (Optional)

If BuddyPress is active:
1. Check user profiles for "Courses" tabs
2. Test course enrollment activities in activity streams
3. Verify course-group integration features

---

## Key Features Overview

### 1. Advanced Course & Instructor Display

**Course Shortcode:**
- `[reign_lifterlms_courses]` - Comprehensive course listing with category filtering and slider options

**Instructor Shortcode:**
- `[reign_lifterlms_instructors]` - Professional instructor displays with social media integration

**Layout Options:**
- Grid layouts with customizable columns (1-6)
- Optional slider functionality
- Responsive design with mobile optimization

### 2. Enhanced Widget System (7 Widgets)

**Available Widgets:**
- Course Categories Widget
- Course Difficulties Widget
- Course Search Widget
- Course Listing Widget
- Membership Listing Widget
- Course Overview Widget
- Enrolled Students Widget

Add these through Appearance → Widgets.

### 3. BuddyPress Social Learning

**Activity Integration:**
```
// Automatically enabled when BuddyPress is active
// Tracks course enrollment, completion, quizzes, certificates
```

**Profile Features:**
- Courses tab in BuddyPress member profiles
- Individual activity preferences
- Course progress display in social profiles
- Learning achievements in profiles

### 4. Enhanced Student Dashboard

**Dashboard Features:**
- Two navigation styles (Style 1 & Style 2)
- Tabbed interface for organized learning
- Visual progress tracking
- Achievement and certificate displays
- Mobile-optimized dashboard

### 5. Advanced Review System

**Interactive Reviews:**
- AJAX-powered star ratings
- Detailed review analytics (1-5 star breakdown)
- Average rating calculations
- Review count displays

---

## Common Usage Examples

### Learning Platform Homepage
```
<!-- Featured Courses -->
[reign_lifterlms_courses posts_per_page="8" per_row="4" category="featured"]

<!-- All Instructors -->
[reign_lifterlms_instructors per_row="4" enable_slider="true"]

<!-- Recent Courses -->
[reign_lifterlms_courses posts_per_page="6" per_row="3"]
```

### Course Category Pages
```
[reign_lifterlms_courses category="web-development" posts_per_page="12" per_row="3"]
```

### Instructor Directory
```
[reign_lifterlms_instructors per_row="3" total="20"]
```

### Course Slider for Homepage
```
[reign_lifterlms_courses posts_per_page="6" per_row="3" enable_slider="true"]
```

---

## BuddyPress Social Learning Setup

### Enable Course Activity Tracking

1. **Automatic Activity Logging:**
   - Course enrollment activities
   - Course completion activities
   - Lesson completion tracking
   - Quiz participation (pass/fail)
   - Certificate earning notifications
   - Achievement unlocks

2. **Group Integration:**
   - Link courses to BuddyPress groups
   - Auto-enroll course students in linked groups
   - Group-specific activity feeds
   - Bulk student management

3. **Profile Features:**
   - "Courses" tab in user profiles
   - Individual activity preferences
   - Course progress visualization
   - Social learning achievements

### Test BuddyPress Features

1. Enroll in a course
2. Complete a lesson
3. Check your BuddyPress profile for courses tab
4. Verify activities appear in activity streams
5. Test group integration features

---

## Dashboard Customization Setup

### Student Dashboard Enhancement

The addon provides two dashboard navigation styles:

1. **Style 1**: Traditional dashboard layout with sidebar navigation
2. **Style 2**: Modern tabbed interface with horizontal navigation

### Dashboard Configuration

Navigate to Reign Settings → LifterLMS:

1. **Dashboard Settings:**
   - Select navigation style (Style 1 or Style 2)
   - Configure dashboard title text
   - Set items per row for different sections

2. **Layout Options:**
   - Courses per row (archive pages)
   - Memberships per row (archive pages)
   - Dashboard items per row

3. **Display Elements:**
   - Hide/show instructor tab
   - Hide/show course author
   - Hide/show course date
   - Hide/show course meta
   - Hide/show course thumbnail

---

## Template Customization Setup

### Distraction-Free Learning

Enable distraction-free mode for focused learning:

1. **Configuration:**
   ```
   Reign Settings → LifterLMS → Enable Distraction-Free Layout
   ```

2. **Features:**
   - Removes site header and footer on lesson pages
   - Minimal navigation for focus
   - Clean, distraction-free interface
   - Mobile-optimized layout

### Template Override System

**Available Templates for Override:**
- Single course pages
- Single lesson/quiz/assignment pages
- Course archive pages
- Membership archive pages
- Student dashboard sections

**Override Location:**
```
/wp-content/themes/reign-child/lifterlms/
```

---

## Performance Optimization

### Best Practices

1. **Course Display:**
   - Use reasonable posts_per_page limits (8-12)
   - Enable slider for better UX with many courses
   - Optimize course images

2. **BuddyPress Integration:**
   - Configure appropriate activity types
   - Monitor activity stream performance
   - Set reasonable profile display limits

3. **Widget Configuration:**
   - Limit widget course counts
   - Use caching for better performance
   - Optimize widget queries

---

## Troubleshooting

### Common Issues

**Shortcodes Not Working:**
1. Verify plugin is activated (v2.4.1+)
2. Check LifterLMS is properly configured
3. Ensure courses exist and are published
4. Clear all caches

**BuddyPress Features Missing:**
1. Verify BuddyPress is active and configured
2. Check activity components are enabled
3. Test with different user roles
4. Clear BuddyPress caches

**Dashboard Not Displaying:**
1. Check LifterLMS student dashboard page
2. Verify user enrollment in courses
3. Test dashboard navigation settings
4. Clear theme caches

**Templates Not Loading:**
1. Check template override locations
2. Verify file permissions
3. Clear template caches
4. Test with default settings

---

## Next Steps

For detailed configuration and advanced features:
- [Configuration Guide](03-configuration.md) - Complete settings guide
- [Course Customization](04-course-customization.md) - Advanced appearance options
- [Developer Guide](05-developer-guide.md) - Hooks, filters, and customization
- [Shortcodes Reference](06-shortcodes-reference.md) - Complete shortcode documentation

---

*Comprehensive Quick Start Guide based on complete analysis of Reign LifterLMS Addon v2.4.1*

---

### Step 4: Create Course & Membership (15 minutes)

#### A. Quick Course Creation

1. **New Course:**
   ```
   LifterLMS → Courses → Add New
   Title: "Complete [Topic] Training"
   ```

2. **Add Sections:**
   - Section 1: Getting Started
   - Section 2: Core Skills
   - Section 3: Advanced Topics

3. **Add Lessons:**
   - 3 lessons per section
   - 10-minute each
   - Mix video & text

4. **Add Quiz:**
   - End of section quiz
   - 70% passing grade

#### B. Create Membership

1. **New Membership:**
   ```
   LifterLMS → Memberships → Add New
   Title: "Premium Access"
   ```

2. **Access Settings:**
   - Include all courses
   - Monthly pricing: $29
   - Annual pricing: $290

3. **Publish**

✅ **Test:** Preview course & membership

---

### Step 5: Visual Customization (6 minutes)

```
Appearance → Customize → Reign LifterLMS
```

**Quick Styling:**
- Brand Color: Your primary
- Success Color: Green
- Button Style: Rounded
- Card Shadow: Soft
- Typography: Clean

**Enable Elements:**
- ✅ Course Ribbons
- ✅ Instructor Avatar
- ✅ Progress Bar
- ✅ Enrollment Count
- ✅ Pricing Table

**Save & Publish**

✅ **Review:** Check frontend appearance

---

## 🎉 Platform Ready! You Have:

- ✅ LMS configured
- ✅ First course created
- ✅ Membership tier set
- ✅ Customized design
- ✅ Payment ready

---

## 📅 7-Day Action Plan

### Days 1-2: Content
- [ ] Complete 3 courses
- [ ] Add course materials
- [ ] Create certificates
- [ ] Set up emails

### Days 3-4: Engagement
- [ ] Add achievements
- [ ] Create badges
- [ ] Set milestones
- [ ] Enable forums

### Days 5-7: Launch
- [ ] Test enrollment
- [ ] Process payments
- [ ] Invite beta users
- [ ] Collect feedback

---

## 🚨 Quick Solutions

**"Can't access course"**
```
Check: Enrollment status
Fix: Settings → Permalinks → Save
```

**"Payment not working"**
```
LifterLMS → Settings → Checkout
Enable payment gateway
```

**"Lessons not showing"**
```
Check lesson-course association
Verify publication status
```

---

## 💡 LifterLMS Best Practices

### Course Structure:
```
Course
├── Section (Module)
│   ├── Lesson (Video/Text)
│   ├── Assignment
│   └── Quiz
└── Certificate
```

### Pricing Models:
- **One-time:** $97-497
- **Payment Plan:** 3 × $47
- **Membership:** $29/month
- **Bundle:** Save 30%

### Engagement Features:
1. **Drip Content** - Weekly releases
2. **Prerequisites** - Structured path
3. **Achievements** - Milestone rewards
4. **Social Proof** - Reviews & ratings
5. **Community** - Discussion areas

---

## 📊 Key Metrics

### Monitor Daily:
- New enrollments
- Course progress
- Quiz completion
- Support requests

### Weekly Goals:
- 20+ enrollments
- 70% progress rate
- 4.5+ rating
- <24hr support response

---

## 🎓 Student Journey

```
Browse → Preview → Enroll → Learn → Engage → Complete → Achieve
```

Optimize each step for success!

---

## 📚 Resources

### Documentation:
- [Configuration Guide](03-configuration.md)
- [Course Builder](04-course-customization.md)
- [Developer Guide](05-developer-guide.md)

### Support:
- [Submit Ticket](https://wbcomdesigns.com/support/)
- [Video Tutorials](https://youtube.com/wbcomdesigns)
- [Community Forum](https://wbcomdesigns.com/forums/)

---

*LifterLMS Quick Start v1.0*
*40-minute setup guide*