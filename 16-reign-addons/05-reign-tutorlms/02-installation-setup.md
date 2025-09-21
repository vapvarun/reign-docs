# Reign TutorLMS Addon - Installation & Setup

## Overview

This guide provides comprehensive installation and setup instructions for Reign TutorLMS Addon v2.0.0, including multi-platform profile integration (BuddyPress/PeepSo), advanced shortcode configuration, AJAX progress tracking, and social learning features.

## Prerequisites

**Required Components:**
1. ✅ WordPress 5.8+
2. ✅ Reign Theme (latest version)
3. ✅ TutorLMS plugin (latest version)
4. ✅ Valid Reign TutorLMS Addon license

**Optional for Enhanced Features:**
- BuddyPress/BuddyBoss (for social profile integration)
- PeepSo (for PeepSo profile integration)
- Elementor/WPBakery (for page builder compatibility)

---

## Part 1: Download Your Addon Files

### Step 1: Get Your Files from WBcom

1. **Login to your WBcom account:**
   - Go to `wbcomdesigns.com`
   - Click "My Account" (top right corner)
   - Enter your login credentials

2. **Find your purchase:**
   - Click "Downloads" in the account menu
   - Look for "Reign TutorLMS Addon"
   - Click the download button

3. **Save the zip file:**
   - Save to your Downloads folder
   - File will be named `reign-tutorlms-addon.zip`
   - **Don't unzip it!** WordPress needs the zip file

### Step 2: Verify Download Contents

Your download should include:
- `reign-tutorlms-addon.zip` (main plugin file)
- `license.txt` (your license key)
- `installation-guide.pdf` (quick reference)

---

## Part 2: Install the Addon

### Method 1: WordPress Admin Upload (Recommended)

1. **Access your WordPress admin:**
   ```
   yoursite.com/wp-admin
   ```

2. **Navigate to plugins:**
   - Click **Plugins** in the left sidebar
   - Click **Add New** at the top
   - Click **Upload Plugin** button

3. **Upload your file:**
   - Click **Choose File**
   - Select `reign-tutorlms-addon.zip`
   - Click **Install Now**
   - Wait for "Plugin installed successfully"

4. **Activate the plugin:**
   - Click **Activate Plugin**
   - You'll see a success message

### Method 2: FTP Upload (If Method 1 Fails)

**Use this if you get file size errors:**

1. **Unzip the file on your computer**
2. **Connect via FTP to your site**
3. **Navigate to:** `/wp-content/plugins/`
4. **Upload folder:** `reign-tutorlms-addon`
5. **Go back to WordPress admin → Plugins**
6. **Find and activate** the Reign TutorLMS Addon

---

## Part 3: License Activation

### Why License Activation is Important
- 🔄 Enables automatic updates
- 🛡️ Access to support
- ✨ Unlocks all premium features
- 🔒 Security patches

### Steps to Activate License:

1. **Find your license key:**
   - Check your purchase email
   - Or login to WBcom account → Licenses
   - Copy the license key (format: XXXX-XXXX-XXXX-XXXX)

2. **Enter in WordPress:**
   - Go to **Reign Settings** → **License**
   - Find "Reign TutorLMS Addon" section
   - Paste your license key
   - Click **Activate License**

3. **Confirm activation:**
   - Look for green "Active" status
   - If you see red, double-check the key

**License Troubleshooting:**

| Problem | Solution |
|---------|----------|
| "Invalid license" | Remove spaces, check for typos |
| "Already activated" | Deactivate on old site first |
| "Expired license" | Renew at wbcomdesigns.com |
| "Site URL mismatch" | Ensure www/non-www matches |

---

## Part 4: TutorLMS Integration Setup

### Step 1: Configure TutorLMS Basic Settings

1. **Go to TutorLMS Settings:**
   - **TutorLMS** → **Settings** → **General**
   - Configure basic TutorLMS options

2. **Essential TutorLMS settings:**
   ```yaml
   Course Permalink: /courses/
   Lesson Permalink: /lessons/
   Enable Course Marketplace: Yes
   Enable Course Q&A: Yes
   Enable Course Reviews: Yes
   Course Completion: Auto (or manual)
   ```

### Step 2: Enable Reign TutorLMS Integration

1. **Go to Customizer:**
   - **Appearance** → **Customize**
   - Look for **Reign TutorLMS Settings**
   - Click to expand

2. **Enable integration:**
   - Toggle ON "Enable TutorLMS Integration"
   - Click **Publish** to save

---

## Part 5: Multi-Platform Profile Integration

### BuddyPress/BuddyBoss Integration

**If you have BuddyPress or BuddyBoss installed:**

1. **Automatic Detection:**
   - The addon automatically detects BuddyPress/BuddyBoss
   - Creates "My Courses" tab in user profiles
   - Enables context-aware course displays

2. **Configure BuddyPress Integration:**
   ```
   Customizer → Reign TutorLMS → BuddyPress Settings
   ```

   **Settings:**
   - Profile Tab Name: "My Courses"
   - Show Progress Bars: Yes
   - Context Detection: Automatic
   - Activity Integration: Yes

### PeepSo Integration

**If you have PeepSo installed:**

1. **Automatic PeepSo Detection:**
   - The addon detects PeepSo automatically
   - Integrates with PeepSo profile system
   - Adds course display to profiles

2. **Configure PeepSo Integration:**
   ```
   Customizer → Reign TutorLMS → PeepSo Settings
   ```

   **Settings:**
   - Profile Integration: Enabled
   - Course Display: Grid layout
   - Progress Tracking: AJAX enabled

---

## Part 6: Configure Course Display Settings

### Step 1: Course Grid Layout

**Go to:** **Appearance** → **Customize** → **Reign TutorLMS** → **Course Display**

**Recommended settings:**

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Grid Columns** | 3 (desktop), 1 (mobile) | Optimal viewing |
| **Show Progress** | Yes | Student motivation |
| **Show Duration** | Yes | Helps planning |
| **Show Instructor** | Yes | Builds trust |
| **Show Price** | Yes | Transparency |
| **AJAX Loading** | Yes | Better UX |

### Step 2: Advanced Display Options

```yaml
Course Card Style: Modern with shadows
Progress Bar Style: Animated
Responsive Layout: Auto-stack on mobile
Loading Animation: Fade in
Hover Effects: Enabled
```

---

## Part 7: AJAX Progress Tracking Setup

### Enable Real-Time Progress

1. **Configure AJAX Settings:**
   ```
   Customizer → Reign TutorLMS → AJAX Settings
   ```

2. **Essential AJAX options:**
   - Enable AJAX Progress: Yes
   - Progress Update Frequency: Real-time
   - Loading Indicators: Yes
   - Error Handling: Graceful fallback

### Test AJAX Functionality

1. **Create test course and enroll**
2. **Complete a lesson**
3. **Verify progress updates without page refresh**
4. **Check profile display updates**

---

## Part 8: Context-Aware Display Configuration

### Understanding Context Detection

The addon intelligently detects:
- **Profile Owner**: Shows their own courses
- **Profile Visitor**: Shows public course information
- **Logged-in User**: Shows enrollment status
- **Guest User**: Shows public course catalog

### Configure Context Settings

```
Customizer → Reign TutorLMS → Context Detection
```

**Settings:**
- Auto-detect User Context: Yes
- Profile Owner Display: Full course list with progress
- Visitor Display: Public courses only
- Guest Display: Course catalog
- Privacy Controls: Respect user settings

---

## Part 9: Shortcode Configuration

### Essential Shortcodes Setup

1. **Course Display Shortcode:**
   ```
   [reign_tutor_course columns="3" show_progress="yes"
   layout="grid" my_courses="yes"]
   ```

2. **Category Display Shortcode:**
   ```
   [reign_course_categories columns="4" show_count="yes"
   show_image="yes" layout="grid"]
   ```

### Advanced Shortcode Usage

**Profile-specific display:**
```
[reign_tutor_course user_context="profile_owner"
show_progress="yes" course_status="in_progress"]
```

**Filter by completion status:**
```
[reign_tutor_course course_status="completed"
order="completion_date" layout="list"]
```

---

## Part 10: Mobile Optimization

### Mobile Learning Settings

**Go to:** **Appearance** → **Customize** → **Reign TutorLMS** → **Mobile**

```yaml
Mobile Layout: Stack vertically
Touch Optimization: Enabled
Swipe Gestures: Yes for course navigation
Mobile Progress: Simplified display
Font Sizes: Larger for mobile
Button Sizing: Touch-friendly
```

### Test Mobile Experience

1. **Use Chrome DevTools:**
   - Right-click → Inspect
   - Click device icon
   - Test different screen sizes

2. **Test on real devices:**
   - Phone and tablet
   - Check course enrollment process
   - Verify progress tracking
   - Test profile integration

---

## Part 11: Performance Optimization

### Speed Up Your LMS

1. **Install caching plugin:**
   - Configure to exclude AJAX requests
   - Cache course catalog pages
   - Exclude user profile pages

2. **Optimize for TutorLMS:**
   ```yaml
   Cache Exclusions:
   - /courses/ (if dynamic)
   - User profile pages
   - Course progress AJAX calls
   - Enrollment processes
   ```

### Database Optimization

**Regular maintenance tasks:**
- Clean expired progress data
- Optimize course enrollment tables
- Remove orphaned course data
- Clear temporary AJAX data

---

## Part 12: Security Configuration

### Protect Your LMS

**Essential security steps:**
- [ ] SSL certificate for course pages
- [ ] Secure payment processing
- [ ] User data protection
- [ ] Course content protection
- [ ] Profile privacy controls
- [ ] AJAX request validation

**Configure privacy settings:**
```
TutorLMS → Settings → Privacy
```
- Course enrollment privacy
- Progress sharing controls
- Profile visibility settings

---

## Part 13: Create Test Content

### Quick Course Setup Test

1. **Create a test course:**
   - **Courses** → **Add New**
   - Title: "Social Learning Test Course"
   - Add description and featured image
   - **Publish**

2. **Add lessons and content:**
   - Add 3 lessons with video/text content
   - Create a quiz
   - Set course pricing (free for testing)

3. **Test all integrations:**
   - Enroll in course
   - Complete lessons
   - Check progress in profile
   - Test AJAX updates
   - Verify context detection

---

## Troubleshooting Common Issues

### "My Courses tab not showing"

**Solution:**
1. Verify BuddyPress/PeepSo is active
2. Check addon license activation
3. Clear all caches
4. Deactivate/reactivate addon

### "AJAX progress not updating"

**Solution:**
1. Check browser console for JavaScript errors
2. Verify WordPress AJAX is enabled
3. Test with default theme
4. Check server AJAX configuration

### "Shortcodes not working"

**Solution:**
1. Verify shortcode syntax
2. Check required parameters
3. Test with minimal parameters
4. Ensure TutorLMS is active

### "Context detection failing"

**Solution:**
1. Clear user sessions
2. Test with different user roles
3. Check privacy settings
4. Verify profile URLs

---

## Final Setup Checklist

### Before Going Live:

**Technical checklist:**
- [ ] All plugins updated
- [ ] License activated and valid
- [ ] Test course created and functional
- [ ] Profile integration working
- [ ] AJAX progress tracking active
- [ ] Mobile experience tested
- [ ] Shortcodes configured
- [ ] Context detection working
- [ ] Backup system active

**Content checklist:**
- [ ] Course categories set up
- [ ] Instructor profiles complete
- [ ] Course pricing configured
- [ ] Privacy policy updated
- [ ] Terms of service updated

---

## What's Next?

### Your enhanced TutorLMS is installed! Now:

1. **[Advanced Configuration →](03-configuration.md)**
   - Social integration settings
   - Profile customization
   - AJAX optimization

2. **[Shortcode Reference →](06-shortcodes-reference.md)**
   - All shortcode parameters
   - Advanced usage examples
   - Context-aware displays

3. **[Course Customization →](04-course-customization.md)**
   - Layout customization
   - Progress visualization
   - Mobile optimization

---

## Quick Reference

### Important URLs After Setup

```
Course Catalog: yoursite.com/courses/
Student Dashboard: yoursite.com/dashboard/
User Profiles: yoursite.com/members/[username]/courses/
Admin Settings: yoursite.com/wp-admin/admin.php?page=tutor_settings
```

### Essential Shortcodes

| Shortcode | Purpose | Example |
|-----------|---------|---------|
| `[reign_tutor_course]` | Display courses | Profile/page course grids |
| `[reign_course_categories]` | Show categories | Course category showcase |

---

**Need Installation Help?**
📧 Email: support@wbcomdesigns.com
📚 Documentation: docs.wbcomdesigns.com
💬 Community: facebook.com/groups/wbcom
🎥 Video tutorials available in member area