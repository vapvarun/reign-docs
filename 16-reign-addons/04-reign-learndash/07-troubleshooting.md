# Reign LearnDash Addon - Troubleshooting Guide

## How to Use This Guide
Find your issue below and follow the solutions step by step. We start with the easiest fixes first, then progress to more advanced solutions.

---

## 🔴 Critical Issues

### "Plugin won't activate"

**Error: "Plugin could not be activated because it triggered a fatal error"**

**Solution 1: Check Requirements**
```
Required:
✅ WordPress 5.0+
✅ LearnDash LMS plugin
✅ Reign Theme
✅ PHP 7.2 or higher
```

How to verify:
1. Go to **Plugins** → Check LearnDash is active
2. Go to **Appearance** → Themes → Verify Reign is active
3. **Tools** → **Site Health** → Check PHP version

**Solution 2: Check Activation Order**

Activate in this sequence:
1. LearnDash LMS
2. Reign Theme
3. Reign LearnDash Addon

**Solution 3: Enable Debug Mode**
```php
// Add to wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```
Check `/wp-content/debug.log` for specific errors.

---

### "Courses not displaying"

**Solution 1: Clear All Caches**
```
1. Browser cache: Ctrl+F5 (PC) or Cmd+Shift+R (Mac)
2. Plugin cache: Clear all caching plugins
3. Theme cache: Customizer → make change → Publish
4. LearnDash cache: LearnDash → Settings → Advanced → Clear Cache
```

**Solution 2: Check Course Status**
1. Go to **LearnDash LMS** → **Courses**
2. Make sure courses are "Published" (not Draft)
3. Check course access settings
4. Verify course has content (lessons)

**Solution 3: Reset Permalinks**
1. **Settings** → **Permalinks**
2. Don't change anything
3. Click **Save Changes**
4. This refreshes URL structure

---

## 🎯 Course Display Issues

### "Course cards look broken"

**Solution 1: Regenerate Theme CSS**
1. **Appearance** → **Customize**
2. **Reign LearnDash Settings**
3. Change any setting slightly
4. **Publish**
5. Change back to original
6. **Publish** again

**Solution 2: Check for Plugin Conflicts**
1. Deactivate all plugins except:
   - LearnDash
   - Reign LearnDash Addon
2. Check if courses display correctly
3. Reactivate plugins one by one
4. Identify conflicting plugin

**Solution 3: Check CSS Conflicts**
```css
/* Add to Customizer → Additional CSS to fix common issues */
.ld-course-card {
    box-sizing: border-box !important;
    width: 100% !important;
}

.ld-course-grid {
    display: grid !important;
    gap: 20px !important;
}
```

---

### "Course images not showing"

**Solution 1: Check Image Requirements**
- Recommended size: 600x400px
- Format: JPG, PNG, or WebP
- Max size: 2MB
- Aspect ratio: 3:2

**Solution 2: Regenerate Thumbnails**
1. Install "Regenerate Thumbnails" plugin
2. **Tools** → **Regenerate Thumbnails**
3. Click **Regenerate All Thumbnails**
4. Wait for completion

**Solution 3: Check Featured Images**
1. Edit the course
2. Check "Featured Image" is set
3. If missing, add featured image
4. **Update** course

---

## 👥 User Access Issues

### "Students can't access courses"

**Solution 1: Check Course Access Settings**
1. Edit the course
2. **Settings** tab
3. **Course Access Settings**:
   - **Open**: Anyone can access
   - **Free**: Registration required
   - **Buy Now**: Payment required
   - **Recurring**: Subscription needed
   - **Closed**: Manual enrollment only

**Solution 2: Manual Enrollment**
1. **LearnDash LMS** → **Users**
2. Find the user
3. **Course Access** tab
4. Select courses to grant access
5. **Update User**

**Solution 3: Check User Role**
1. **Users** → Find user
2. **Edit** user
3. Make sure Role is not "Subscriber" (should be "Student" or higher)
4. **Update User**

---

### "Instructors can't create courses"

**Solution 1: Check Instructor Capabilities**
1. **LearnDash LMS** → **Settings** → **General**
2. **Course Builder** section
3. Enable "Instructors can create courses"
4. **Save Changes**

**Solution 2: Assign Instructor Role**
1. **Users** → Find user
2. **Edit** user
3. Change Role to "Instructor"
4. **Update User**

**Solution 3: Check Instructor Permissions**
```php
// Add to functions.php temporarily
add_action('init', function() {
    $role = get_role('instructor');
    if ($role) {
        $role->add_cap('edit_courses');
        $role->add_cap('publish_courses');
        $role->add_cap('delete_courses');
    }
});
```

---

## 🧮 Quiz & Assessment Problems

### "Quizzes not working properly"

**Solution 1: Check Quiz Settings**
1. Edit the quiz
2. **Settings** tab
3. Verify:
   - Passing percentage is set
   - Number of attempts allowed
   - Time limit (if any)
   - Question randomization

**Solution 2: Check Question Format**
1. Edit quiz questions
2. Make sure:
   - Correct answers are marked
   - Point values are set
   - Answer explanations added

**Solution 3: Clear Quiz Data**
```php
// Reset quiz attempts for user (run once)
function reset_user_quiz_attempts($user_id, $quiz_id) {
    global $wpdb;
    $wpdb->delete(
        $wpdb->prefix . 'learndash_user_activity',
        array(
            'user_id' => $user_id,
            'post_id' => $quiz_id,
            'activity_type' => 'quiz'
        )
    );
}
```

---

### "Progress not updating"

**Solution 1: Complete Lesson Properly**
1. Make sure "Mark Complete" button is clicked
2. Check lesson settings require completion
3. Verify video progression settings
4. Clear browser cache

**Solution 2: Reset Progress**
1. **LearnDash LMS** → **Users**
2. Find user → **Edit**
3. **Course Progress** tab
4. **Reset Progress** for specific course
5. User can restart course

**Solution 3: Fix Database Issues**
```sql
-- Check user activity table
SELECT * FROM wp_learndash_user_activity 
WHERE user_id = [USER_ID] AND post_id = [COURSE_ID];

-- If empty, progress tracking is broken
-- Contact support with this information
```

---

## 💳 Payment & Enrollment Issues

### "Payment not processing"

**Solution 1: Check PayPal Settings**
1. **LearnDash LMS** → **Settings** → **PayPal**
2. Verify:
   - PayPal email is correct
   - Currency matches your account
   - Sandbox mode OFF (for live site)
   - IPN URL is set

**Solution 2: Test Payment Flow**
1. Use small test amount ($0.01)
2. Try different payment method
3. Check PayPal transaction logs
4. Verify email notifications

**Solution 3: WooCommerce Integration**
If using WooCommerce:
1. Install LearnDash WooCommerce addon
2. Create WooCommerce products for courses
3. Link products to courses
4. Test checkout process

---

### "Automatic enrollment not working"

**Solution 1: Check Payment Notifications**
1. **LearnDash LMS** → **Settings** → **PayPal**
2. Check "PayPal IPN URL" is set
3. In PayPal account:
   - Go to Profile → Instant Payment Notifications
   - Add your IPN URL
   - Enable IPN

**Solution 2: Manual Enrollment Process**
1. When payment confirmed
2. **Users** → Find user
3. **Course Access** tab
4. Add courses manually
5. User gets immediate access

---

## 📧 Email & Notification Issues

### "Course emails not sending"

**Solution 1: Install SMTP Plugin**
1. Install "WP Mail SMTP" plugin
2. Configure with email service:
   - Gmail
   - SendGrid
   - Mailgun
3. Send test email
4. Check delivery rates

**Solution 2: Check LearnDash Email Settings**
1. **LearnDash LMS** → **Settings** → **Emails**
2. Enable required email types:
   - Course enrollment
   - Course completion
   - Quiz results
   - Certificate earned

**Solution 3: Check Spam Folders**
- Tell users to check spam/junk
- Add your domain to whitelist
- Use professional email domain
- Avoid spam trigger words

---

## 🎨 Design & Layout Issues

### "Mobile view not working"

**Solution 1: Check Responsive Settings**
1. **Appearance** → **Customize**
2. **Reign LearnDash** → **Mobile Settings**
3. Enable "Responsive Layout"
4. Set mobile columns to 1
5. **Publish** changes

**Solution 2: Test Mobile Viewport**
1. Add to theme header.php:
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```
2. Clear cache
3. Test on real mobile device

**Solution 3: Mobile CSS Fixes**
```css
/* Add to Customizer → Additional CSS */
@media (max-width: 768px) {
    .ld-course-grid {
        grid-template-columns: 1fr !important;
    }
    
    .ld-course-card {
        margin-bottom: 20px;
    }
    
    .learndash-wrapper {
        padding: 10px;
    }
}
```

---

### "Colors not matching theme"

**Solution 1: Use Theme Customizer**
1. **Appearance** → **Customize**
2. **Colors** → **LearnDash Colors**
3. Match colors to your theme
4. **Publish** changes

**Solution 2: Custom CSS Override**
```css
/* Add to Customizer → Additional CSS */
.ld-button {
    background-color: var(--your-primary-color) !important;
}

.ld-progress-bar-fill {
    background: var(--your-accent-color) !important;
}

.ld-course-card {
    border-color: var(--your-border-color) !important;
}
```

---

## ⚠️ Common Error Messages

### Error Dictionary

| Error Message | Meaning | Quick Fix |
|--------------|---------|------------|
| "Course not found" | Invalid course ID | Check course exists and is published |
| "Access denied" | User lacks permission | Check enrollment or course access |
| "Quiz submission failed" | Form validation error | Clear cache, try again |
| "Certificate generation failed" | Missing certificate template | Create certificate in LearnDash |
| "Payment validation failed" | PayPal/payment issue | Check payment gateway settings |
| "User not enrolled" | Missing course access | Manually enroll user |

---

## 🔧 Advanced Debugging

### Enable LearnDash Debug Mode

```php
// Add to wp-config.php
define('LEARNDASH_DEBUG', true);
define('LEARNDASH_SCRIPT_DEBUG', true);
```

### Check Database Tables

```sql
-- Verify LearnDash tables exist
SHOW TABLES LIKE '%learndash%';

-- Should see:
-- wp_learndash_user_activity
-- wp_learndash_user_activity_meta
-- Plus others
```

### Test User Capabilities

```php
// Check what user can do
$user = wp_get_current_user();
if (learndash_is_instructor($user->ID)) {
    echo 'User is instructor';
}
if (learndash_is_student()) {
    echo 'User is student';
}
```

---

## 🎯 Quick Fix Checklist

### Try These First (in order):

1. [ ] Clear all caches (browser + plugin)
2. [ ] Reset permalinks (Settings → Permalinks → Save)
3. [ ] Update LearnDash and addons
4. [ ] Switch to default WordPress theme temporarily
5. [ ] Deactivate other plugins temporarily
6. [ ] Check PHP error log
7. [ ] Increase PHP memory limit
8. [ ] Re-save LearnDash settings
9. [ ] Check course/user permissions
10. [ ] Test with fresh user account

---

## 🔄 Reset Procedures

### Reset Course Progress

**For individual user:**
1. **LearnDash LMS** → **Users**
2. Edit user
3. **Course Progress** tab
4. **Reset** for specific course

**For all users (dangerous!):**
```sql
-- BACKUP FIRST!
DELETE FROM wp_learndash_user_activity 
WHERE post_id = [COURSE_ID];
```

### Reset Quiz Attempts

```php
// Reset all quiz attempts for a user
function reset_all_quiz_attempts($user_id) {
    global $wpdb;
    $wpdb->delete(
        $wpdb->prefix . 'learndash_user_activity',
        array(
            'user_id' => $user_id,
            'activity_type' => 'quiz'
        )
    );
}
```

### Complete Plugin Reset

```sql
-- EXTREME: Remove all LearnDash data
-- BACKUP EVERYTHING FIRST!
DROP TABLE wp_learndash_user_activity;
DROP TABLE wp_learndash_user_activity_meta;
DELETE FROM wp_options WHERE option_name LIKE 'learndash_%';
DELETE FROM wp_usermeta WHERE meta_key LIKE 'learndash_%';
```

---

## 📞 Getting Support

### Before Contacting Support

**Gather this information:**
1. WordPress version
2. LearnDash version
3. Reign theme version
4. PHP version
5. Error messages (exact text)
6. When problem started
7. Recent changes made
8. Steps to reproduce

### Support Template

```
Subject: [LearnDash Issue] Brief description

Environment:
- WordPress: [version]
- LearnDash: [version]
- Reign Theme: [version]
- PHP: [version]
- Hosting: [provider]

Issue:
[Describe what's wrong]

Steps to reproduce:
1. [First step]
2. [Second step]
3. [What happens]

What I've tried:
- [Solution 1]
- [Solution 2]

Error message:
[Paste exact error]

URL where issue occurs:
[Link to page]

Screenshots: [Attached]
```

### Contact Support

- 📧 Email: support@wbcomdesigns.com
- 🌐 Forum: wbcomdesigns.com/support
- 📝 Ticket: Open from your account
- ⏱️ Response: 24-48 hours
- 📚 Documentation: docs.wbcomdesigns.com

---

## 💡 Prevention Tips

### Avoid Future Issues

1. **Regular maintenance:**
   - Weekly plugin updates
   - Monthly full backups
   - Quarterly performance checks

2. **Testing protocol:**
   - Test on staging site first
   - Check one update at a time
   - Verify course functionality after changes

3. **Monitoring:**
   - Check error logs weekly
   - Monitor course completion rates
   - Track user complaints

4. **Best practices:**
   - Don't modify plugin files directly
   - Use child theme for customizations
   - Keep PHP and WordPress updated
   - Regular database optimization

---

## 🚑 Emergency Recovery

### Site Completely Broken

1. **Via FTP/File Manager:**
   ```
   Rename: /plugins/reign-learndash-addon/
   To: /plugins/reign-learndash-addon-disabled/
   ```

2. **Restore from backup:**
   - Use your most recent backup
   - Test one change at a time

3. **Contact emergency support:**
   - Include "URGENT" in subject
   - Provide FTP access if needed
   - Describe what was changed

---

**Still Having Issues?**

Don't panic! Most LearnDash issues have simple solutions. Work through this guide systematically, and contact support if you need help.

🌟 Remember: A well-configured LMS is worth the troubleshooting effort!