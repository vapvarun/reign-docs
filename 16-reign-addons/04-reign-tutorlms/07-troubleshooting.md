# Reign TutorLMS Addon - Troubleshooting Guide

## What You'll Find Here
This guide helps you solve common issues with the Reign TutorLMS addon quickly and easily. We've organized solutions by symptom, so you can find exactly what you need without reading everything.

## Quick Problem Finder 🔍

**Jump to your issue:**
- [Installation Problems](#installation-problems)
- [Course Display Issues](#course-display-issues)
- [Student Enrollment Problems](#student-enrollment-problems)
- [Payment & Checkout Issues](#payment--checkout-issues)
- [Video & Media Problems](#video--media-problems)
- [Quiz & Assessment Issues](#quiz--assessment-issues)
- [Frontend Course Builder Issues](#frontend-course-builder-issues)
- [Dashboard Problems](#dashboard-problems)
- [Performance Issues](#performance-issues)
- [Mobile Device Problems](#mobile-device-problems)
- [Integration Issues](#integration-issues)

---

## Installation Problems

### "Plugin won't activate"

**Symptoms:**
- Error message when clicking "Activate"
- Plugin appears grayed out
- WordPress admin becomes inaccessible

**Solution Steps:**

1. **Check WordPress version:**
   ```
   Requirement: WordPress 5.0 or higher
   Your version: Admin → Dashboard → At a Glance
   ```

2. **Verify TutorLMS is installed:**
   ```
   Required: TutorLMS plugin (free or premium)
   Check: Plugins → Installed Plugins
   ```

3. **Verify Reign theme is active:**
   ```
   Appearance → Themes
   Ensure "Reign" is the active theme
   ```

4. **Check for plugin conflicts:**
   - Deactivate all other plugins
   - Try activating Reign TutorLMS addon
   - If it works, reactivate plugins one by one
   - Find the conflicting plugin

5. **Increase memory limit:**
   ```php
   // Add to wp-config.php
   ini_set('memory_limit', '256M');
   ```

### "License won't activate"

**Common causes and fixes:**

| Error Message | Cause | Solution |
|---------------|-------|----------|
| "Invalid license key" | Typo in license | Copy-paste exactly, remove spaces |
| "Already activated" | Used on another site | Deactivate from old site first |
| "Site URL mismatch" | www/non-www difference | Match exactly with purchase |
| "Expired license" | License needs renewal | Renew at wbcomdesigns.com |

**Step-by-step license fix:**
1. Copy license key from purchase email
2. **Reign Settings** → **License**
3. Clear the license field completely
4. Paste new license (no extra spaces)
5. Click **Activate License**
6. Look for green "Active" status

### "Missing TutorLMS dependency"

**Error message:** "Please install and activate TutorLMS plugin"

**Solution:**
1. **Plugins** → **Add New**
2. Search "TutorLMS"
3. Install the **TutorLMS plugin** (free version works)
4. **Activate** TutorLMS first
5. Then activate Reign TutorLMS addon

---

## Course Display Issues

### "Courses not showing on page"

**Quick checks:**

1. **Verify courses exist and are published:**
   ```
   TutorLMS → Courses → All Courses
   Check "Published" status
   ```

2. **Check shortcode spelling:**
   ```
   Correct: [tutor_course]
   Common mistakes: [tutor_courses] [tutor-course]
   ```

3. **Clear all caches:**
   - Plugin cache (if using caching plugin)
   - Browser cache (Ctrl+F5)
   - CDN cache (if using Cloudflare)

4. **Test with default theme:**
   - Switch to Twenty Twenty-Three theme temporarily
   - Check if courses display correctly
   - If yes, it's a theme conflict

### "Course layout looks broken"

**Symptoms:**
- Courses overlapping
- Strange spacing
- Mobile layout broken

**CSS conflict solutions:**

1. **Check browser console:**
   - Right-click → Inspect Element
   - Look for red error messages
   - Note any CSS conflicts

2. **Add temporary CSS fix:**
   ```css
   /* Go to Appearance → Customize → Additional CSS */
   .tutor-courses-wrap {
       display: grid !important;
       grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)) !important;
       gap: 20px !important;
   }

   .tutor-course {
       margin-bottom: 0 !important;
       width: 100% !important;
   }
   ```

3. **Reset course settings:**
   - **Appearance** → **Customize** → **Reign TutorLMS**
   - Reset to default values
   - **Publish** changes

### "Course images not displaying"

**Fixes:**

1. **Check image requirements:**
   ```
   Recommended size: 600x400 pixels
   Format: JPG, PNG, WebP
   Max file size: 2MB
   ```

2. **Regenerate thumbnails:**
   - Install "Regenerate Thumbnails" plugin
   - Run regeneration for all images

3. **Check file permissions:**
   ```
   wp-content/uploads/ should be 755
   Image files should be 644
   ```

---

## Student Enrollment Problems

### "Students can't enroll in courses"

**Check enrollment settings:**

1. **Course publication status:**
   ```
   Course must be "Published", not "Draft"
   Check: TutorLMS → Courses → All Courses
   ```

2. **Course enrollment enabled:**
   ```
   Edit Course → Settings
   Ensure enrollment is enabled
   ```

3. **User registration enabled:**
   ```
   Settings → General → Membership
   ✅ "Anyone can register" checked
   ```

4. **Monetization configured (if paid):**
   ```
   TutorLMS → Settings → Monetization
   Verify payment method is active
   ```

### "Enrollment button not working"

**Step-by-step debugging:**

1. **Check JavaScript console:**
   - Right-click enrollment button → Inspect
   - Look for JavaScript errors
   - Common issue: jQuery conflicts

2. **Test as logged-out user:**
   - Open incognito/private browser window
   - Try enrolling as new user
   - Check if login prompt appears

3. **Verify button shortcode:**
   ```
   Correct: [tutor_course_enroll_btn course_id="123"]
   Replace 123 with actual course ID
   ```

4. **Check course access settings:**
   ```
   Edit Course → Settings → General
   Verify course access is not set to "Private"
   ```

### "Students losing progress"

**Causes and solutions:**

| Cause | Solution |
|-------|----------|
| Cache plugin issues | Exclude student dashboard from caching |
| Database problems | Run database repair |
| Plugin conflicts | Deactivate conflicting plugins |
| Session timeout | Increase session duration |

**Prevent progress loss:**
```php
// Add to functions.php
add_filter('tutor_course_complete_data_for_js', '__return_false');
```

---

## Payment & Checkout Issues

### "Payment not processing"

**For TutorLMS built-in monetization:**

1. **Check monetization settings:**
   ```
   TutorLMS → Settings → Monetization
   Verify correct method is selected
   ```

2. **Test payment flow:**
   ```
   Create test course with small price
   Try purchasing as different user
   Check payment completion
   ```

**For WooCommerce integration:**

1. **Verify WooCommerce setup:**
   ```
   WooCommerce → Settings → Payments
   Check payment gateway status
   ```

2. **Check product creation:**
   ```
   Products → All Products
   Verify course products are created
   ```

3. **Test WooCommerce flow:**
   ```
   Add course to cart
   Complete checkout process
   Verify enrollment after payment
   ```

### "Students charged but not enrolled"

**Emergency fix:**
1. **Go to:** **TutorLMS** → **Students**
2. **Find affected student**
3. **Manually enroll:** Edit student → Enrollments → Add
4. **Issue refund if needed:** Through payment processor

**Prevent future issues:**
```php
// Add to functions.php - webhook verification
add_action('woocommerce_order_status_completed', 'verify_tutor_enrollment');
function verify_tutor_enrollment($order_id) {
    // Custom enrollment verification logic
    error_log('Order completed: ' . $order_id);
}
```

### "Course price not showing"

**Common fixes:**

1. **Check course monetization:**
   ```
   Edit Course → Settings
   Verify price is set correctly
   ```

2. **Verify shortcode:**
   ```
   [tutor_course_price course_id="123"]
   ```

3. **Check currency settings:**
   ```
   TutorLMS → Settings → Monetization
   Verify currency is set correctly
   ```

---

## Video & Media Problems

### "Videos not playing"

**Quick fixes:**

1. **Check video format:**
   ```
   Supported: MP4, WebM, OGV
   Recommended: MP4 with H.264 codec
   ```

2. **Test video URL directly:**
   - Copy video URL from lesson
   - Paste in new browser tab
   - Should play directly

3. **Check video embedding:**
   ```
   YouTube: Use embed URL format
   Vimeo: Use embed URL format
   Self-hosted: Check file permissions
   ```

### "Video streaming slow/buffering"

**Solutions:**

1. **Use external video hosting:**
   ```
   Recommended services:
   - YouTube (private/unlisted)
   - Vimeo Pro
   - Wistia
   - AWS CloudFront
   ```

2. **Optimize video settings:**
   ```
   Resolution: 720p for most courses
   Bitrate: 1000-1500 kbps
   Format: MP4 (H.264)
   ```

3. **Add video CDN:**
   ```
   CloudFlare for global delivery
   Reduces server load
   Improves streaming speed
   ```

### "Video controls not working"

**Fix video player issues:**

1. **Update browser:**
   - Ensure latest Chrome/Firefox/Safari
   - Clear browser cache

2. **Disable conflicting plugins:**
   ```
   Common conflicts:
   - Other video plugins
   - Optimization plugins
   - Security plugins blocking video
   ```

3. **Check mobile compatibility:**
   ```
   iOS: Requires specific video formats
   Android: Test across different devices
   ```

---

## Quiz & Assessment Issues

### "Quiz questions not displaying"

**Troubleshooting steps:**

1. **Check quiz setup:**
   ```
   Edit Quiz → Questions
   Ensure questions are added and saved
   ```

2. **Verify quiz association:**
   ```
   Course → Curriculum
   Quiz should be properly linked to topic/lesson
   ```

3. **Test quiz permissions:**
   ```
   Quiz Settings → Access
   Check who can take the quiz
   ```

4. **Check question types:**
   ```
   Ensure question types are supported
   Test with simple multiple choice first
   ```

### "Quiz scores not saving"

**Database issues:**

1. **Check database tables:**
   ```
   wp_tutor_quiz_attempts
   wp_tutor_quiz_attempt_answers
   ```

2. **Increase PHP limits:**
   ```php
   // In wp-config.php
   ini_set('max_execution_time', 300);
   ini_set('max_input_vars', 3000);
   ```

3. **Clear quiz cache:**
   ```
   Delete any quiz-related transients
   Clear object cache if using
   ```

### "Quiz timer not working"

**Timer troubleshooting:**

1. **Check timezone settings:**
   ```
   Settings → General → Timezone
   Should match your location
   ```

2. **Test JavaScript:**
   ```
   Browser console should show no errors
   Timer should countdown visibly
   ```

3. **Server time sync:**
   ```
   Contact hosting provider
   Ensure server time is accurate
   ```

---

## Frontend Course Builder Issues

### "Course builder not loading"

**Frontend builder problems:**

1. **Check frontend settings:**
   ```
   TutorLMS → Settings → Course
   Enable "Frontend Course Builder"
   ```

2. **Verify user permissions:**
   ```
   User must have "instructor" role
   Check user capabilities
   ```

3. **Test with default theme:**
   ```
   Switch to Twenty Twenty-Three
   Test course builder functionality
   ```

4. **Check JavaScript errors:**
   ```
   Open browser console
   Look for JavaScript conflicts
   ```

### "Can't upload media in frontend"

**Media upload issues:**

1. **Check file permissions:**
   ```
   wp-content/uploads/ should be writable
   Check folder permissions (755)
   ```

2. **Verify upload limits:**
   ```php
   // Check current limits
   upload_max_filesize
   post_max_size
   max_execution_time
   ```

3. **Test file formats:**
   ```
   Allowed: JPG, PNG, MP4, PDF
   Check specific file isn't corrupted
   ```

### "Course preview not working"

**Preview functionality:**

1. **Check course status:**
   ```
   Course must be "Published"
   Not "Draft" or "Private"
   ```

2. **Verify preview settings:**
   ```
   Edit Course → Settings
   Enable "Public Course Preview"
   ```

3. **Test permalink structure:**
   ```
   Settings → Permalinks
   Use "Post name" structure
   ```

---

## Dashboard Problems

### "Student dashboard blank"

**Dashboard display issues:**

1. **Check dashboard page:**
   ```
   TutorLMS → Tools → Pages
   Verify dashboard page exists
   ```

2. **Test dashboard shortcode:**
   ```
   [tutor_dashboard]
   Add to test page
   ```

3. **Check user enrollment:**
   ```
   User must be enrolled in at least one course
   Test with enrolled student account
   ```

### "Instructor dashboard missing features"

**Feature access problems:**

1. **Verify user role:**
   ```
   Users → All Users
   User must have "Instructor" role
   ```

2. **Check instructor settings:**
   ```
   TutorLMS → Settings → Instructor
   Verify capabilities are enabled
   ```

3. **Test with fresh instructor:**
   ```
   Create new instructor account
   Test dashboard functionality
   ```

### "Dashboard loading slowly"

**Performance optimization:**

1. **Limit dashboard content:**
   ```
   Show fewer courses per page
   Paginate long lists
   Reduce activity feed items
   ```

2. **Enable caching:**
   ```
   Use page caching plugin
   Exclude user-specific pages
   ```

3. **Optimize database:**
   ```
   Clean up old data
   Optimize database tables
   ```

---

## Performance Issues

### "Site loading slowly after activation"

**Optimization steps:**

1. **Install caching plugin:**
   ```
   Recommended: WP Rocket, W3 Total Cache
   Configure for TutorLMS compatibility
   ```

2. **Optimize database:**
   ```
   Install: WP-Optimize plugin
   Clean up: Spam, revisions, orphaned data
   ```

3. **Image optimization:**
   ```
   Compress course images
   Use WebP format
   Enable lazy loading
   ```

### "High server resource usage"

**Reduce server load:**

1. **Optimize query performance:**
   ```sql
   -- Add database indexes for common queries
   CREATE INDEX idx_tutor_enrollments ON wp_tutor_enrollments(course_id, user_id);
   ```

2. **Use object caching:**
   ```
   Redis or Memcached
   Reduces database queries
   ```

3. **CDN for media files:**
   ```
   Cloudflare or AWS CloudFront
   Serves images/videos globally
   ```

### "Dashboard timeout issues"

**Memory and execution fixes:**

1. **Increase PHP limits:**
   ```php
   // In wp-config.php or .htaccess
   memory_limit = 512M
   max_execution_time = 300
   ```

2. **Optimize large data queries:**
   ```
   Limit course lists
   Paginate student lists
   Cache complex calculations
   ```

---

## Mobile Device Problems

### "Mobile layout broken"

**Responsive design fixes:**

1. **Check viewport meta tag:**
   ```html
   <meta name="viewport" content="width=device-width, initial-scale=1">
   ```

2. **Test responsive breakpoints:**
   ```
   Use Chrome DevTools
   Test: 320px, 768px, 1024px widths
   ```

3. **Mobile-specific CSS:**
   ```css
   @media (max-width: 768px) {
       .tutor-courses-wrap {
           grid-template-columns: 1fr !important;
       }
   }
   ```

### "Touch interactions not working"

**Mobile usability fixes:**

1. **Increase touch targets:**
   ```css
   .tutor-btn {
       min-height: 44px;
       min-width: 44px;
       padding: 12px 24px;
   }
   ```

2. **Fix video player:**
   ```
   Ensure HTML5 video player
   Test on iOS and Android
   ```

3. **Improve navigation:**
   ```
   Simplified mobile menu
   Thumb-friendly button placement
   ```

### "Mobile course taking issues"

**Learning experience problems:**

1. **Video playback:**
   ```
   Test full-screen video
   Check orientation lock
   Verify video controls work
   ```

2. **Quiz interface:**
   ```
   Large answer buttons
   Clear question text
   Easy navigation
   ```

3. **Progress tracking:**
   ```
   Visible progress indicators
   Clear completion status
   Easy lesson navigation
   ```

---

## Integration Issues

### "BuddyPress conflicts"

**Community integration problems:**

1. **Check component compatibility:**
   ```
   BuddyPress → Settings → Components
   Ensure Activity Streams is enabled
   ```

2. **Fix profile integration:**
   ```
   Appearance → Customize → Reign TutorLMS
   Enable BuddyPress integration
   ```

3. **Activity feed issues:**
   ```php
   // Add to functions.php
   add_filter('tutor_course_complete_to_bp_activity', '__return_true');
   ```

### "WooCommerce checkout conflicts"

**E-commerce integration:**

1. **Check product sync:**
   ```
   TutorLMS → Tools → Product Sync
   Sync courses with WooCommerce
   ```

2. **Cart conflicts:**
   ```
   Test: Add course to cart
   Complete checkout process
   Verify enrollment
   ```

3. **Payment gateway issues:**
   ```
   Test different payment methods
   Check gateway logs
   Verify webhook settings
   ```

### "Zoom integration problems"

**Live class issues:**

1. **Check API credentials:**
   ```
   TutorLMS → Settings → Zoom
   Verify API key and secret
   ```

2. **Meeting creation fails:**
   ```
   Test API connection
   Check timezone settings
   Verify meeting permissions
   ```

3. **Students can't join:**
   ```
   Check meeting links
   Verify enrollment status
   Test meeting timing
   ```

---

## Emergency Quick Fixes

### "Site completely broken"

**When everything stops working:**

1. **Deactivate addon via FTP:**
   ```
   Connect to site via FTP
   Navigate to: /wp-content/plugins/
   Rename: reign-tutorlms-addon to reign-tutorlms-addon-disabled
   ```

2. **Enable WordPress debug:**
   ```php
   // Add to wp-config.php
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   ```

3. **Check error logs:**
   ```
   Look in: /wp-content/debug.log
   Find the specific error causing issues
   ```

### "Database corruption"

**Data recovery steps:**

1. **Restore from backup:**
   ```
   Use most recent backup
   Before addon activation if possible
   ```

2. **Repair database:**
   ```
   phpMyAdmin → Database → Repair
   Or use WP-CLI: wp db repair
   ```

3. **Reinstall addon:**
   ```
   Delete addon files
   Download fresh copy
   Reinstall and reconfigure
   ```

---

## Prevention Tips

### Regular Maintenance

**Weekly tasks:**
- [ ] Check for plugin updates
- [ ] Test course enrollment process
- [ ] Verify video playback
- [ ] Monitor site performance

**Monthly tasks:**
- [ ] Database optimization
- [ ] Backup verification
- [ ] Security scan
- [ ] User experience testing
- [ ] Clear old quiz attempts

### Monitoring Setup

**Tools to install:**
- Uptime monitoring (UptimeRobot)
- Performance monitoring (Query Monitor)
- Error logging (Log Viewer)
- Backup automation (UpdraftPlus)

---

## Getting Additional Help

### Before Contacting Support

**Information to gather:**

1. **Environment details:**
   ```
   WordPress version:
   Reign theme version:
   TutorLMS version:
   PHP version:
   Server type:
   ```

2. **Error details:**
   ```
   Exact error message:
   When error occurs:
   Steps to reproduce:
   Browser/device:
   ```

3. **Recent changes:**
   ```
   New plugins installed:
   Settings changed:
   Content added:
   ```

### Support Channels

**Fastest resolution:**
📧 **Email:** support@wbcomdesigns.com
📚 **Documentation:** docs.wbcomdesigns.com
💬 **Community:** facebook.com/groups/wbcom
🎥 **Video help:** Member portal training section

### Self-Help Resources

**Debug like a pro:**
1. Enable debug mode
2. Check browser console
3. Test with default theme
4. Deactivate other plugins
5. Clear all caches
6. Test on different device

---

**Quick Reference:**
Most issues are solved by clearing cache, checking plugin conflicts, or verifying settings. When in doubt, test with minimal setup first!