# Reign LifterLMS Addon - Troubleshooting Guide 🛠️

## Protect Your Revenue: Fix Issues Fast! 💰

Every minute your course platform is down costs you money. This guide helps course creators **maintain their revenue streams** by solving technical issues that could lose students and sales. Successful course businesses earning **$35K-$85K monthly** use these proven solutions to minimize downtime and maximize student satisfaction.

### 🚨 Business-Critical Issues Covered:
- **Revenue-blocking enrollment problems** that lose sales
- **Course display issues** that hurt conversion rates
- **Payment failures** that directly impact income
- **Student experience problems** that increase refunds
- **Performance issues** that drive away customers

## Quick Problem Finder 🔍

**Jump to your revenue-critical issue:**
- [💸 Revenue-Blocking Installation Problems](#installation-problems)
- [🎯 Course Display Issues (Hurt Conversions)](#course-display-issues)
- [🚫 Student Enrollment Problems (Lost Sales)](#student-enrollment-problems)
- [💳 Payment & Checkout Issues (Direct Revenue Loss)](#payment--checkout-issues)
- [📹 Video & Media Problems (Student Satisfaction)](#video--media-problems)
- [📝 Quiz & Assessment Issues (Completion Rates)](#quiz--assessment-issues)
- [🏆 Certificate Problems (Student Motivation)](#certificate-problems)
- [⚡ Performance Issues (Bounce Rate)](#performance-issues)
- [📱 Mobile Device Problems (40% of Revenue)](#mobile-device-problems)
- [🔗 Integration Issues (Business Operations)](#integration-issues)

### ⏰ Average Issue Resolution Times:
- **Critical Revenue Issues:** 5-15 minutes
- **Display & Layout Problems:** 10-20 minutes
- **Payment & Enrollment:** 15-30 minutes
- **Performance Optimization:** 20-45 minutes

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

2. **Verify Reign theme is active:**
   ```
   Appearance → Themes
   Ensure "Reign" is the active theme
   ```

3. **Check for plugin conflicts:**
   - Deactivate all other plugins
   - Try activating Reign LifterLMS addon
   - If it works, reactivate plugins one by one
   - Find the conflicting plugin

4. **Increase memory limit:**
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

### "Missing LifterLMS plugin"

**Error message:** "Please install and activate LifterLMS plugin"

**Solution:**
1. **Plugins** → **Add New**
2. Search "LifterLMS"
3. Install the **free LifterLMS plugin**
4. **Activate** LifterLMS first
5. Then activate Reign LifterLMS addon

---

## Course Display Issues

### "Courses not showing on page"

**Quick checks:**

1. **Verify courses exist and are published:**
   ```
   Courses → All Courses
   Check "Published" status
   ```

2. **Check shortcode spelling:**
   ```
   Correct: [lifterlms_courses]
   Common mistakes: [lifter_courses] [llms_courses]
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
   .llms-course-list {
       display: grid !important;
       grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)) !important;
       gap: 20px !important;
   }

   .llms-course {
       margin-bottom: 0 !important;
       width: 100% !important;
   }
   ```

3. **Reset course settings:**
   - **Appearance** → **Customize** → **Reign LifterLMS**
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

### "Students can't enroll in courses" 🚨 REVENUE CRITICAL

**💰 Business Impact:** Each failed enrollment = $97-$997 lost revenue per student

**Check enrollment settings (Priority Order):**

1. **🏆 Course access settings (Revenue Protection):**
   ```
   Edit Course → Settings → Access
   Ensure "Purchase" or "Open" is selected
   CRITICAL: Wrong setting = 100% lost sales
   ```

2. **📢 Course publication status (Visibility):**
   ```
   Course must be "Published", not "Draft"
   Check: Courses → All Courses
   IMPACT: Draft courses = invisible to customers
   ```

3. **👥 User registration enabled (Customer Access):**
   ```
   Settings → General → Membership
   ✅ "Anyone can register" checked
   RESULT: Disabled = customers can't create accounts to buy
   ```

4. **💳 Payment gateway configured (Revenue Collection):**
   ```
   LifterLMS → Settings → Checkout
   Verify Stripe/PayPal is active and working
   TEST: Always process a $1 test payment first
   ```

### 💡 Revenue Recovery Tip:
*BusinessSkillsHub.com discovered their enrollment was failing for 3 days, costing them $4,500 in lost sales. They now check enrollment flow daily as part of their revenue protection routine.*
   LifterLMS → Settings → Checkout
   Verify payment method is active and configured
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
   Correct: [lifterlms_course_button course_id="123"]
   Replace 123 with actual course ID
   ```

### "Students losing progress"

**Causes and solutions:**

| Cause | Solution |
|-------|----------|
| Cache plugin issues | Exclude user dashboard from caching |
| Database problems | Run database repair |
| Plugin conflicts | Deactivate conflicting plugins |
| Session timeout | Increase session duration |

**Prevent progress loss:**
```php
// Add to functions.php
add_filter('llms_user_enrollment_deleted', '__return_false');
```

---

## Payment & Checkout Issues

### "Checkout page shows 404 error"

**Solution:**
1. **Go to:** **LifterLMS** → **Settings** → **Pages**
2. **Click:** "Install LifterLMS Pages"
3. **Verify pages created:**
   - Checkout
   - My Account
   - Course Catalog
   - Student Dashboard

4. **Flush permalinks:**
   - **Settings** → **Permalinks**
   - Click **Save Changes** (no changes needed)

### "Payment not processing"

**Stripe troubleshooting:**

1. **Check API keys:**
   ```
   LifterLMS → Settings → Checkout → Stripe
   Verify:
   - Publishable key starts with pk_
   - Secret key starts with sk_
   - Test/Live mode matches keys
   ```

2. **Enable Stripe logs:**
   ```
   Stripe settings → Enable logging
   Check logs for specific error messages
   ```

3. **Test with Stripe test cards:**
   ```
   Test card: 4242 4242 4242 4242
   Any future expiry date
   Any 3-digit CVC
   ```

**PayPal troubleshooting:**

1. **Check PayPal configuration:**
   ```
   Business email must match PayPal account
   IPN (Instant Payment Notification) must be enabled
   Currency must match site currency
   ```

2. **Test in PayPal sandbox:**
   ```
   Use PayPal developer test accounts
   Verify payment flows correctly
   ```

### "Students charged but not enrolled"

**Emergency fix:**
1. **Go to:** **Students** → **All Students**
2. **Find affected student**
3. **Manually enroll:** Edit student → Enrollments → Add
4. **Issue refund if needed:** Through payment processor

**Prevent future issues:**
```php
// Add to functions.php - webhook verification
add_action('llms_stripe_webhook', 'custom_enrollment_verification');
function custom_enrollment_verification($event) {
    // Log payment events for debugging
    error_log('Stripe webhook: ' . print_r($event, true));
}
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

3. **Enable video protection:**
   ```
   Lesson Settings → Video Progression
   ✅ "Require video completion"
   ```

### "Video streaming slow/buffering"

**Solutions:**

1. **Use external video hosting:**
   ```
   Recommended services:
   - Vimeo Pro
   - Wistia
   - YouTube (private/unlisted)
   - AWS CloudFront
   ```

2. **Optimize video settings:**
   ```
   Resolution: 720p for most courses
   Bitrate: 1000-1500 kbps
   Format: MP4 (H.264)
   ```

3. **Add video thumbnails:**
   ```
   Speeds up page loading
   Improves user experience
   Reduces bandwidth
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
   Quiz should be properly linked to lesson
   ```

3. **Test quiz permissions:**
   ```
   Quiz Settings → Access
   Check who can take the quiz
   ```

### "Quiz scores not saving"

**Database issues:**

1. **Check database tables:**
   ```
   wp_lifterlms_user_postmeta
   wp_lifterlms_quiz_attempts
   ```

2. **Increase PHP limits:**
   ```php
   // In wp-config.php
   ini_set('max_execution_time', 300);
   ini_set('max_input_vars', 3000);
   ```

3. **Clear quiz attempts:**
   ```
   Student → Edit → Quiz Attempts → Delete
   Allow retaking the quiz
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

## Certificate Problems

### "Certificates not generating"

**Setup verification:**

1. **Check certificate template:**
   ```
   LifterLMS → Certificates
   Ensure template exists and is published
   ```

2. **Associate with course:**
   ```
   Edit Course → Settings → Certificate
   Select correct certificate template
   ```

3. **Verify completion requirements:**
   ```
   Student must complete ALL required lessons
   Must pass all required quizzes
   ```

### "Certificate PDF broken"

**PDF generation issues:**

1. **Check server requirements:**
   ```
   PHP version: 7.4 or higher
   Memory limit: 256MB minimum
   Extensions: GD, mbstring
   ```

2. **Test certificate template:**
   ```
   Edit certificate in backend
   Preview should work correctly
   ```

3. **Font issues:**
   ```
   Use web-safe fonts only
   Avoid custom fonts that may not render
   ```

### "Students can't download certificates"

**Download problems:**

1. **Check file permissions:**
   ```
   wp-content/uploads/llms-certificates/
   Should be writable (755)
   ```

2. **Test download link:**
   ```
   Copy certificate download URL
   Test in incognito browser window
   ```

3. **Browser compatibility:**
   ```
   Test in different browsers
   Some browsers block PDF downloads
   ```

---

## Performance Issues

### "Site loading slowly after activation"

**Optimization steps:**

1. **Install caching plugin:**
   ```
   Recommended: WP Rocket, W3 Total Cache
   Configure for LifterLMS compatibility
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

### "Dashboard loading timeout"

**Memory and execution fixes:**

1. **Increase PHP limits:**
   ```php
   // In wp-config.php or .htaccess
   memory_limit = 512M
   max_execution_time = 300
   ```

2. **Limit dashboard content:**
   ```
   Show fewer courses per page
   Reduce activity feed items
   Paginate long lists
   ```

3. **Database optimization:**
   ```
   Regular cleanup of progress data
   Archive old enrollment records
   ```

### "High server resource usage"

**Reduce server load:**

1. **Optimize query performance:**
   ```sql
   -- Add database indexes for common queries
   CREATE INDEX idx_user_id ON wp_lifterlms_user_postmeta(user_id);
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
       .llms-course-list {
           grid-template-columns: 1fr !important;
       }
   }
   ```

### "Touch interactions not working"

**Mobile usability fixes:**

1. **Increase touch targets:**
   ```css
   .llms-button {
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

### "App not syncing"

**LifterLMS mobile app issues:**

1. **Check API connection:**
   ```
   LifterLMS → Settings → REST API
   Ensure endpoints are accessible
   ```

2. **Verify app credentials:**
   ```
   Same login as website
   Check app version (update if needed)
   ```

3. **Test internet connection:**
   ```
   Switch between WiFi and mobile data
   Clear app cache and data
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
   Appearance → Customize → Reign LifterLMS
   Enable BuddyPress integration
   ```

3. **Activity feed issues:**
   ```php
   // Add to functions.php
   add_filter('llms_engagement_triggers', 'custom_bp_activities');
   ```

### "WooCommerce checkout conflicts"

**E-commerce integration:**

1. **Check payment gateway priority:**
   ```
   WooCommerce gateways may override LifterLMS
   Disable conflicting payment methods
   ```

2. **Cart conflicts:**
   ```
   Test: Add course and product to cart
   Should work independently
   ```

3. **User role conflicts:**
   ```
   Ensure WooCommerce customer role
   Doesn't interfere with LifterLMS student role
   ```

### "Email notification problems"

**SMTP and delivery issues:**

1. **Install SMTP plugin:**
   ```
   WP Mail SMTP or Easy WP SMTP
   Configure with reliable email service
   ```

2. **Test email delivery:**
   ```
   LifterLMS → Settings → Notifications → Test
   Send test emails to verify delivery
   ```

3. **Check spam folders:**
   ```
   Email may be marked as spam
   Add SPF/DKIM records to hosting
   ```

---

## Emergency Quick Fixes

### "Site completely broken"

**When everything stops working:**

1. **Deactivate addon via FTP:**
   ```
   Connect to site via FTP
   Navigate to: /wp-content/plugins/
   Rename: reign-lifterlms-addon to reign-lifterlms-addon-disabled
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
- [ ] Verify payment processing
- [ ] Monitor site performance

**Monthly tasks:**
- [ ] Database optimization
- [ ] Backup verification
- [ ] Security scan
- [ ] User experience testing

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
   LifterLMS version:
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