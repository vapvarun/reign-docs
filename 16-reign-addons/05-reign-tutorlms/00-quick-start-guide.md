# Reign TutorLMS Addon - Quick Start Guide

## What This Addon Provides

Reign TutorLMS Addon v2.0.0 is a comprehensive theme integration extension that transforms TutorLMS into a social learning platform with enhanced course displays, multi-platform profile integration (BuddyPress/BuddyBoss/PeepSo), AJAX progress tracking, and advanced course management features.

**Core Features (Comprehensive):**
- **2 Enhanced Shortcodes**: [reign_tutor_course] and [reign_course_categories] with 25+ parameters each
- **Multi-Platform Profile Integration**: Automatic "My Courses" tabs for BuddyPress, BuddyBoss, and PeepSo
- **AJAX Progress Tracking**: Real-time course progress visualization without page refresh
- **Context-Aware Displays**: Smart user detection (profile owner vs logged-in user)
- **Advanced Course Filtering**: Status-based filtering (all, completed, in_progress, not_started)
- **Responsive Grid Layouts**: 1-6 column layouts with mobile optimization
- **Professional Category Showcases**: Visual category displays with course counts
- **Social Learning Features**: Course sharing in social profiles and activity streams

---

## Prerequisites

**Required Components:**
- ✅ WordPress 5.8+
- ✅ Reign Theme (latest version)
- ✅ TutorLMS plugin (latest version)
- ✅ Valid Reign TutorLMS Addon license

**Optional for Enhanced Features:**
- BuddyPress/BuddyBoss (for social profile integration)
- PeepSo (for PeepSo profile integration)
- Elementor/WPBakery (for page builder compatibility)

---

## 🎯 Quick Setup Steps

### Step 1: Install Addon (4 minutes)

1. **Download from WBcom:**
   ```
   WBcom Account → Downloads → Reign TutorLMS Addon
   Save: reign-tutorlms-addon.zip
   ```

2. **Install in WordPress:**
   ```
   Plugins → Add New → Upload Plugin
   → Choose File → Select ZIP → Install Now → Activate
   ```

3. **Verify Installation:**
   ```
   Plugins → Installed Plugins
   → Look for "Reign TutorLMS Addon" (Active)
   ```

✅ **Success:** Green "Active" status visible

---

### Step 2: Activate License (2 minutes)

1. **Get License Key:**
   ```
   WBcom Account → Licenses → TutorLMS Addon
   Copy: XXXX-XXXX-XXXX-XXXX
   ```

2. **Activate in WordPress:**
   ```
   Reign Settings → License Tab
   → TutorLMS Addon Section → Paste Key → Activate License
   ```

3. **Verify Activation:**
   ```
   Status: "Active" (green indicator)
   Updates: Enabled automatically
   ```

✅ **Success:** License shows "Active" status

---

### Step 3: Configure TutorLMS Integration (10 minutes)

#### A. TutorLMS Basic Setup
```
Tutor LMS → Settings → General
```
Essential settings:
- Course Permalink: `/courses/`
- Lesson Permalink: `/lessons/`
- Enable Q&A: Yes
- Enable Reviews: Yes
- Course Market: Yes

#### B. Reign TutorLMS Integration
```
Customizer → Reign TutorLMS Settings
```

**Course Display Settings:**
```yaml
Grid Layout: 3 columns (desktop), 1 (mobile)
Card Style: Modern with progress bars
Show Elements: Price, Lessons, Duration, Progress
Enable AJAX: Yes (for progress tracking)
Profile Integration: Auto-detect platforms
```

#### C. Social Platform Integration
```
Reign Settings → Social Integration
```
**Auto-Configuration:**
- BuddyPress: Auto-detected → "My Courses" tab
- PeepSo: Auto-detected → Profile integration
- Standard: Fallback integration

✅ **Test:** View /courses/ page and user profiles

---

### Step 4: Test Course Display & Social Integration (12 minutes)

#### A. Create Test Course
1. **Add Course:**
   ```
   Tutor LMS → Add New Course
   Title: "Social Learning Test Course"
   ```

2. **Course Builder:**
   - Add Topic: "Introduction Module"
   - Add 3 Lessons: "Lesson 1", "Lesson 2", "Lesson 3"
   - Add 1 Quiz: "Module Quiz"
   - Set Duration: 2 hours

3. **Advanced Settings:**
   - Price: Free (for testing)
   - Enable Reviews: Yes
   - Maximum Students: 100
   - Certificate: Yes

#### B. Test Social Integration
1. **Profile Integration Test:**
   ```
   Visit any user profile → Look for "My Courses" tab
   BuddyPress: Should auto-appear
   PeepSo: Check profile navigation
   ```

2. **Progress Tracking Test:**
   - Enroll in test course
   - Complete one lesson
   - Check AJAX progress update
   - Verify profile display

✅ **Success:** Course shows in profile, progress tracks in real-time

---

### Step 5: Advanced Shortcode Setup (7 minutes)

#### A. Course Display Shortcodes
1. **Create Advanced Course Grid:**
   ```
   [reign_tutor_course columns="3" show_progress="yes"
   my_courses="yes" order="date" layout="grid"]
   ```

2. **Profile-Specific Display:**
   ```
   [reign_tutor_course user_context="profile_owner"
   show_progress="yes" course_status="in_progress"]
   ```

#### B. Category Showcase
1. **Course Categories Grid:**
   ```
   [reign_course_categories columns="4" show_count="yes"
   show_image="yes" layout="grid"]
   ```

#### C. Customize Appearance
```
Appearance → Customize → Reign TutorLMS
```

**Enhanced Settings:**
- Course Grid: 3 columns with AJAX
- Progress Bars: Animated with percentages
- Profile Integration: Auto-enabled
- Mobile Layout: Responsive stack

✅ **Result:** Modern course displays with social integration

---

## 🎉 Success! Your Social LMS Has:

- ✅ **TutorLMS Integrated** with Reign theme enhancement
- ✅ **Social Learning Platform** with BuddyPress/PeepSo integration
- ✅ **AJAX Progress Tracking** in real-time
- ✅ **Enhanced Course Displays** with modern layouts
- ✅ **Profile Integration** showing "My Courses" tabs
- ✅ **Advanced Shortcodes** with 25+ parameters
- ✅ **Context-Aware Features** detecting user contexts
- ✅ **Mobile-Optimized Learning** experience

---

## 📅 Week 1 Social Learning Roadmap

### Days 1-3: Content & Social Setup
- [ ] Create 5 comprehensive courses with social elements
- [ ] Test BuddyPress/PeepSo profile integration
- [ ] Configure AJAX progress tracking
- [ ] Set up advanced shortcode displays
- [ ] Test context-aware course filtering

### Days 4-7: Community & Launch
- [ ] Configure social learning notifications
- [ ] Set up instructor social profiles
- [ ] Enable course sharing in activity streams
- [ ] Test mobile social learning experience
- [ ] Launch with social community features

---

## 🚨 Quick Fixes

**"My Courses tab not showing in profile"**
```
Check: BuddyPress/PeepSo is active
Verify: Addon license is active
Clear: All caches and refresh
```

**"AJAX progress not updating"**
```
Check: JavaScript console for errors
Verify: WordPress AJAX enabled
Test: Different browser/incognito
```

**"Shortcodes not working"**
```
Verify: [reign_tutor_course] syntax
Check: All required parameters
Test: Simple version first
```

---

## 💡 Social Learning Tips

### Maximize Social Integration:
- **Profile Engagement**: Use "My Courses" tabs for student showcases
- **Progress Sharing**: Enable course completion in activity streams
- **Context Awareness**: Show different content for profile owners vs visitors
- **Community Building**: Connect courses with BuddyPress groups
- **Mobile Learning**: Optimize for mobile social learning

### Advanced Shortcode Usage:
- **Personalized Displays**: Use `user_context="profile_owner"`
- **Progress Filtering**: Filter by `course_status="in_progress"`
- **AJAX Enhancement**: Enable `show_progress="yes"` for real-time updates
- **Layout Optimization**: Use responsive `columns="3"` for grids

---

## 📊 Track Social Learning Success

### Weekly Social Metrics:
- **Course Enrollments**: ___ (track via profiles)
- **Progress Completion**: ___% (AJAX tracking)
- **Profile Engagement**: ___ visits to "My Courses"
- **Social Sharing**: ___ activity stream posts
- **Platform Integration**: BuddyPress __ / PeepSo __

### Advanced Analytics:
- **Context-Aware Views**: Profile owner vs visitor views
- **Mobile Learning**: Mobile completion rate ____%
- **Shortcode Usage**: Grid vs list vs custom displays

---

## 📚 Learn More

- [Advanced Configuration](03-configuration.md) - Social integration settings
- [Shortcode Reference](06-shortcodes-reference.md) - All 25+ parameters
- [Course Customization](04-course-customization.md) - Layout and design options
- [Developer Guide](05-developer-guide.md) - Custom integrations
- [Get Support](https://wbcomdesigns.com/support/) - Technical assistance

---

## 🚀 Quick Reference

### Essential Shortcodes:
```
[reign_tutor_course columns="3" show_progress="yes"]
[reign_course_categories columns="4" show_count="yes"]
```

### Social Platforms Supported:
- ✅ BuddyPress + BuddyBoss
- ✅ PeepSo Community
- ✅ Standard WordPress profiles

---

*35-minute comprehensive social LMS setup*