# Reign Sensei Addon - Troubleshooting Guide

## What You'll Find Here
This guide helps you solve common issues with the Reign Sensei addon quickly and easily. We've organized solutions by symptom, so you can find exactly what you need without reading everything.

## Quick Problem Finder 🔍

**Jump to your issue:**
- [Installation Problems](#installation-problems)
- [WooCommerce Integration Issues](#woocommerce-integration-issues)
- [Course Display Issues](#course-display-issues)
- [Student Enrollment Problems](#student-enrollment-problems)
- [Payment & Checkout Issues](#payment--checkout-issues)
- [Quiz & Assessment Issues](#quiz--assessment-issues)
- [Teacher Dashboard Problems](#teacher-dashboard-problems)
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

2. **Verify required plugins are installed:**
   ```
   Required:
   - Sensei LMS (free or premium)
   - WooCommerce (required for Sensei)
   - Reign Theme (active)
   ```

3. **Check plugin order:**
   ```
   Install order:
   1. WooCommerce first
   2. Sensei LMS second
   3. Reign Sensei addon last
   ```

4. **Check for plugin conflicts:**
   - Deactivate all other plugins
   - Try activating Reign Sensei addon
   - If it works, reactivate plugins one by one

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

### "Missing dependencies error"

**Error message:** "Please install WooCommerce and Sensei LMS"

**Solution:**
1. **Install WooCommerce:**
   - Plugins → Add New → Search "WooCommerce"
   - Install and activate

2. **Install Sensei LMS:**
   - Plugins → Add New → Search "Sensei LMS"
   - Install and activate

3. **Run setup wizards:**
   - Complete WooCommerce setup
   - Complete Sensei setup
   - Then activate Reign addon

---

## WooCommerce Integration Issues

### "Course products not created automatically"

**This is the most common issue with Sensei:**

**Quick fix:**
1. **Go to:** **Sensei LMS** → **Tools**
2. **Click:** "Create Products for Courses"
3. **Wait for completion**
4. **Check:** WooCommerce → Products

**Manual creation:**
1. **Create WooCommerce product:**
   - Products → Add New
   - Product type: Simple Product
   - Virtual: Yes
   - Downloadable: No

2. **Link to course:**
   - In product editor
   - Product Data → Sensei
   - Select course from dropdown
   - Save product

### "Students can't purchase courses"

**Check these settings:**

1. **WooCommerce store setup:**
   ```
   WooCommerce → Settings → General
   Store address and currency configured
   ```

2. **Payment gateways enabled:**
   ```
   WooCommerce → Settings → Payments
   At least one payment method enabled
   ```

3. **Product visibility:**
   ```
   Edit Product → Catalog visibility
   Set to "Shop and search results"
   ```

4. **Course-product link:**
   ```
   Verify course has associated WooCommerce product
   Check product is published
   ```

### "Course access not granted after purchase"

**Troubleshooting steps:**

1. **Check order status:**
   ```
   WooCommerce → Orders
   Order should be "Completed" or "Processing"
   ```

2. **Verify course enrollment:**
   ```
   Sensei LMS → Students
   Check if student appears in course
   ```

3. **Manual enrollment:**
   ```
   Edit Course → Students
   Add student manually if needed
   ```

4. **Check enrollment hooks:**
   ```php
   // Add to functions.php for debugging
   add_action('woocommerce_order_status_completed', function($order_id) {
       error_log('Order completed: ' . $order_id);
   });
   ```

---

## Course Display Issues

### "Courses not showing on page"

**Quick checks:**

1. **Verify courses exist:**
   ```
   Sensei LMS → Courses
   Check courses are published
   ```

2. **Check shortcode spelling:**
   ```
   Correct: [sensei_courses]
   Common mistakes: [sensei_course] [sensei-courses]
   ```

3. **Clear all caches:**
   - WooCommerce cache
   - Plugin cache
   - Browser cache (Ctrl+F5)
   - CDN cache

4. **Test with default theme:**
   - Switch to Twenty Twenty-Three temporarily
   - Check if courses display
   - If yes, it's a theme conflict

### "Course layout looks broken"

**CSS conflict solutions:**

1. **Check browser console:**
   - Right-click → Inspect Element
   - Look for red error messages
   - Note any CSS conflicts

2. **Add temporary CSS fix:**
   ```css
   /* Go to Appearance → Customize → Additional CSS */
   .sensei-course-container {
       display: grid !important;
       grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)) !important;
       gap: 20px !important;
   }

   .sensei-course {
       margin-bottom: 0 !important;
       width: 100% !important;
   }
   ```

3. **Reset addon settings:**
   - **Appearance** → **Customize** → **Reign Sensei**
   - Reset to default values
   - **Publish** changes

### "Course images not displaying"

**Common fixes:**

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

**Check enrollment workflow:**

1. **Course publication status:**
   ```
   Course must be "Published", not "Draft"
   Check: Sensei LMS → Courses
   ```

2. **WooCommerce product exists:**
   ```
   Check: Products → All Products
   Course should have associated product
   ```

3. **User registration enabled:**
   ```
   Settings → General → Membership
   ✅ "Anyone can register" checked
   ```

4. **WooCommerce checkout working:**
   ```
   Test purchasing any WooCommerce product
   Verify checkout process works
   ```

### "Enrollment button not working"

**Step-by-step debugging:**

1. **Check JavaScript console:**
   - Right-click enrollment button → Inspect
   - Look for JavaScript errors
   - Common issue: jQuery conflicts

2. **Test WooCommerce add to cart:**
   ```
   Try adding product to cart directly
   Check if cart functionality works
   ```

3. **Verify button shortcode:**
   ```
   Correct: [sensei_course_button course_id="123"]
   Replace 123 with actual course ID
   ```

4. **Check user permissions:**
   ```
   Test with different user roles
   Verify registration process
   ```

### "Students losing progress"

**Causes and solutions:**

| Cause | Solution |
|-------|----------|
| Cache plugin issues | Exclude user pages from caching |
| Database problems | Run database repair |
| Plugin conflicts | Deactivate conflicting plugins |
| WooCommerce conflicts | Check order status processing |

**Prevent progress loss:**
```php
// Add to functions.php
add_filter('sensei_user_quiz_grade', function($grade, $quiz_id, $user_id) {
    // Log quiz grades for debugging
    error_log("Quiz grade: $grade for user $user_id, quiz $quiz_id");
    return $grade;
}, 10, 3);
```

---

## Payment & Checkout Issues

### "WooCommerce checkout not working"

**Checkout troubleshooting:**

1. **Check WooCommerce pages:**
   ```
   WooCommerce → Status → Tools
   "Create default WooCommerce pages"
   ```

2. **Verify payment gateways:**
   ```
   WooCommerce → Settings → Payments
   Enable at least one payment method
   ```

3. **Test with simple product:**
   ```
   Create simple WooCommerce product
   Test checkout process
   If it works, issue is course-specific
   ```

### "Stripe/PayPal not working"

**Payment gateway debugging:**

1. **Check API credentials:**
   ```
   WooCommerce → Settings → Payments → Stripe
   Verify API keys are correct
   Test mode vs Live mode
   ```

2. **Enable payment logs:**
   ```
   WooCommerce → Status → Logs
   Enable payment gateway logging
   ```

3. **Test with test cards:**
   ```
   Stripe test card: 4242 4242 4242 4242
   Any future expiry, any CVC
   ```

### "Students charged but not enrolled"

**Emergency fix:**
1. **Manual enrollment:**
   - Sensei LMS → Students
   - Add student to course manually
   - Send access information

2. **Check order processing:**
   ```
   WooCommerce → Orders
   Verify order status is "Completed"
   Check order notes for errors
   ```

3. **Verify automation:**
   ```php
   // Check if enrollment hooks are working
   add_action('woocommerce_order_status_completed', function($order_id) {
       $order = wc_get_order($order_id);
       foreach ($order->get_items() as $item) {
           $product_id = $item->get_product_id();
           $course_id = Sensei_WC::get_course_id_by_product_id($product_id);
           if ($course_id) {
               error_log("Should enroll in course: $course_id");
           }
       }
   });
   ```

---

## Quiz & Assessment Issues

### "Quiz questions not displaying"

**Troubleshooting steps:**

1. **Check quiz setup:**
   ```
   Edit Quiz → Questions
   Ensure questions are added and published
   ```

2. **Verify quiz-lesson association:**
   ```
   Edit Lesson → Quiz
   Quiz should be selected
   ```

3. **Check question types:**
   ```
   Sensei supports:
   - Multiple Choice
   - True/False
   - Gap Fill
   - Multi Line
   - Single Line
   - File Upload
   ```

### "Quiz scores not saving"

**Database and settings issues:**

1. **Check database tables:**
   ```
   wp_sensei_user_answers
   wp_comments (for quiz grades)
   ```

2. **Increase PHP limits:**
   ```php
   // In wp-config.php
   ini_set('max_execution_time', 300);
   ini_set('max_input_vars', 3000);
   ```

3. **Test quiz submission:**
   ```
   Take quiz as test user
   Check database for saved answers
   Verify grading process
   ```

### "Quiz grading not working"

**Grading troubleshooting:**

1. **Check auto-grading settings:**
   ```
   Edit Quiz → Quiz Settings
   Auto-grade: Enabled for multiple choice
   ```

2. **Manual grading:**
   ```
   Sensei LMS → Grading
   Review ungraded quizzes
   Grade manually if needed
   ```

3. **Verify pass mark:**
   ```
   Edit Quiz → Pass mark percentage
   Should be set (e.g., 70%)
   ```

---

## Teacher Dashboard Problems

### "Teacher dashboard not accessible"

**Permission issues:**

1. **Check user role:**
   ```
   Users → All Users
   User must have "Teacher" role
   ```

2. **Verify teacher capabilities:**
   ```
   Sensei LMS → Settings → General
   Teacher role permissions enabled
   ```

3. **Test with administrator:**
   ```
   Login as admin
   Check if teacher features work
   ```

### "Teachers can't create courses"

**Capability troubleshooting:**

1. **Check Sensei settings:**
   ```
   Sensei LMS → Settings → General
   "Allow teachers to create courses" enabled
   ```

2. **Verify user permissions:**
   ```
   Add custom capability if needed:
   $user = get_user_by('ID', $teacher_id);
   $user->add_cap('manage_sensei');
   ```

3. **Test course creation:**
   ```
   Login as teacher
   Try creating test course
   Check for error messages
   ```

---

## Performance Issues

### "Site loading slowly after activation"

**Optimization steps:**

1. **Install caching plugin:**
   ```
   Recommended: WP Rocket, W3 Total Cache
   Configure for WooCommerce compatibility
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

### "WooCommerce performance issues"

**E-commerce optimization:**

1. **Disable unused WooCommerce features:**
   ```
   WooCommerce → Settings → Advanced
   Disable features you don't need
   ```

2. **Optimize product queries:**
   ```
   Limit products per page
   Use product caching
   Optimize database queries
   ```

3. **CDN for assets:**
   ```
   Use Cloudflare or similar
   Cache static assets
   Serve images globally
   ```

### "Database performance problems"

**Query optimization:**

1. **Add database indexes:**
   ```sql
   -- Add indexes for common queries
   CREATE INDEX idx_sensei_course_meta ON wp_postmeta(meta_key, meta_value(10));
   CREATE INDEX idx_wc_product_meta ON wp_postmeta(meta_key, meta_value(10));
   ```

2. **Clean up old data:**
   ```
   Remove old cart sessions
   Clean expired transients
   Optimize database tables
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
       .sensei-course-container {
           grid-template-columns: 1fr !important;
       }
   }
   ```

### "Mobile checkout issues"

**WooCommerce mobile problems:**

1. **Test checkout flow:**
   ```
   Complete purchase on mobile
   Check all form fields work
   Verify payment processing
   ```

2. **Optimize checkout:**
   ```
   Simplify checkout fields
   Use mobile-friendly payment methods
   Test on different devices
   ```

### "Touch interactions not working"

**Mobile usability fixes:**

1. **Increase touch targets:**
   ```css
   .sensei-course-action {
       min-height: 44px;
       min-width: 44px;
       padding: 12px 24px;
   }
   ```

2. **Improve navigation:**
   ```
   Simplified mobile menu
   Large, thumb-friendly buttons
   Clear visual hierarchy
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
   Appearance → Customize → Reign Sensei
   Enable BuddyPress integration
   ```

3. **Activity feed issues:**
   ```php
   // Add to functions.php
   add_action('sensei_user_course_end', function($user_id, $course_id) {
       if (function_exists('bp_activity_add')) {
           bp_activity_add(array(
               'user_id' => $user_id,
               'action' => sprintf('%s completed course %s',
                   bp_core_get_user_displayname($user_id),
                   get_the_title($course_id)
               ),
               'component' => 'sensei'
           ));
       }
   }, 10, 2);
   ```

### "WooCommerce theme conflicts"

**E-commerce styling issues:**

1. **Check template overrides:**
   ```
   WooCommerce → Status → System Status
   Look for template override conflicts
   ```

2. **Test with default theme:**
   ```
   Switch to Storefront theme
   Test course purchasing
   If it works, it's a theme issue
   ```

3. **CSS conflicts:**
   ```
   Check for conflicting WooCommerce styles
   Use browser inspector to debug
   ```

---

## Emergency Quick Fixes

### "Site completely broken"

**When everything stops working:**

1. **Deactivate addon via FTP:**
   ```
   Connect to site via FTP
   Navigate to: /wp-content/plugins/
   Rename: reign-sensei-addon to reign-sensei-addon-disabled
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
   Find specific error messages
   ```

### "WooCommerce database corruption"

**Data recovery steps:**

1. **Restore from backup:**
   ```
   Use most recent backup
   Before addon activation if possible
   ```

2. **Repair WooCommerce:**
   ```
   WooCommerce → Status → Tools
   Run repair tools
   Clear all cache
   ```

3. **Recreate course-product links:**
   ```
   Sensei LMS → Tools
   "Create Products for Courses"
   Manually link if needed
   ```

---

## Prevention Tips

### Regular Maintenance

**Weekly tasks:**
- [ ] Check for plugin updates
- [ ] Test course enrollment process
- [ ] Verify WooCommerce orders
- [ ] Monitor site performance

**Monthly tasks:**
- [ ] Database optimization
- [ ] Backup verification
- [ ] Security scan
- [ ] User experience testing
- [ ] Clear old cart sessions

### Monitoring Setup

**Tools to install:**
- Uptime monitoring (UptimeRobot)
- Performance monitoring (Query Monitor)
- WooCommerce status monitoring
- Error logging (Log Viewer)

---

## Getting Additional Help

### Before Contacting Support

**Information to gather:**

1. **Environment details:**
   ```
   WordPress version:
   Reign theme version:
   Sensei LMS version:
   WooCommerce version:
   PHP version:
   ```

2. **Error details:**
   ```
   Exact error message:
   When error occurs:
   Steps to reproduce:
   WooCommerce order details:
   ```

3. **Recent changes:**
   ```
   New plugins installed:
   WooCommerce settings changed:
   Course/product modifications:
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
6. Test WooCommerce separately

---

## Common Error Messages

### Quick Error Reference

| Error Message | Likely Cause | Quick Fix |
|---------------|--------------|-----------|
| "Course not found" | Course deleted or unpublished | Check course status |
| "Product not found" | WooCommerce product missing | Recreate course products |
| "Permission denied" | User role issue | Check user capabilities |
| "Payment failed" | Gateway configuration | Check payment settings |
| "Enrollment failed" | WooCommerce-Sensei link broken | Manual enrollment |

---

**Quick Reference:**
Most issues stem from WooCommerce integration problems. Always check WooCommerce setup first, then Sensei configuration, then addon settings.