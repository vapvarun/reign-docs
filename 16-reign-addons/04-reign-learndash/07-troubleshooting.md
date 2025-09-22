# Reign LearnDash Addon - Troubleshooting Guide

## 🆘 Quick Fix Your Learning Platform Issues

Don't panic! Most issues can be fixed in minutes. This guide walks you through solutions to common problems with clear, simple steps. No technical expertise required!

---

## 🔴 Critical Issues (Fix First!)

### "My shortcodes show as plain text!"

**What's happening:** You see `[modern_courses]` instead of beautiful course displays.

**2-Minute Fix:**
1. ✅ **Check plugin is active** - Plugins page → "Reign LearnDash Addon" should say "Deactivate"
2. ✅ **Verify you have courses** - LearnDash → Courses → Need at least 1 published course
3. ✅ **Test simple shortcode** - Try just `[modern_courses]` with no parameters
4. ✅ **Clear all caches** - Browser (Ctrl+F5) + WordPress cache plugins

**Success Rate:** 95% fixed with these steps!

### "Courses look plain/ugly!"

**What's wrong:** No beautiful Reign styling on your courses.

**Quick Solutions:**
1. 🧹 **Clear browser cache** - Press Ctrl+F5 (Windows) or Cmd+Shift+R (Mac)
2. 🧹 **Clear WordPress cache** - Deactivate cache plugins temporarily
3. ✅ **Confirm Reign is active** - Appearance → Themes → Reign should be active
4. 🔍 **Check for conflicts** - Deactivate other LMS plugins temporarily

**Pro Tip:** 70% of styling issues are just cache problems!

---

## 🟡 Display & Layout Issues

### "My custom templates won't load!"

**Fix Template Loading:**
1. 📁 **Check file location** - Must be in `/your-theme/learndash/`
2. 🔐 **Verify permissions** - Files need 644 permissions
3. 🧹 **Clear all caches** - Both browser and server
4. 📝 **Check file names** - Must match exactly (case-sensitive)

### "Course archive pages look wrong!"

**Customize Archive Pages:**
1. 🎨 **Go to** Appearance → Customize
2. 🔍 **Find** LearnDash Groups settings
3. ⚙️ **Configure** columns, templates, filters
4. 💾 **Save & publish** changes

---

## ⚡ Performance Problems

### "My site is running slow!"

**Speed Optimization Checklist:**

**Quick Wins (Do These First):**
- 📊 Show only 12-16 courses per page (not 50!)
- 🖼️ Optimize images (use Smush or similar)
- 💾 Enable caching plugin (WP Rocket recommended)
- 🔄 Use lazy loading for images

**Advanced Optimizations:**
```
[modern_courses
    per_page="12"              # Optimal number
    enable_lazy_loading="yes"  # Load images as needed
    cache_duration="3600"]     # 1-hour cache
```

### "Out of memory errors!"

**Memory Solutions:**
1. **Increase PHP memory** - Add to wp-config.php:
   ```php
   define('WP_MEMORY_LIMIT', '256M');
   ```
2. **Optimize queries** - Use specific categories, not all courses
3. **Better hosting** - Upgrade if on cheap shared hosting

---

## 👥 BuddyPress/Social Features Issues

### "Social features not showing!"

**Enable Social Learning:**
1. ✅ **Install BuddyPress** - Plugins → Add New → BuddyPress
2. ✅ **Activate components** - Settings → BuddyPress → Components
3. ✅ **Enable activity streams** - Must be checked
4. ✅ **Enable user groups** - For course groups
5. 🔄 **Refresh permalinks** - Settings → Permalinks → Save

### "Course tabs missing from profiles!"

**Fix Profile Tabs:**
1. 👤 **Check user role** - Must have course access
2. 📚 **Verify enrollment** - User must be enrolled in courses
3. 🔄 **Clear BuddyPress cache** - Often fixes it
4. 🧪 **Test with admin account** - Rules out permission issues

---

## ⭐ Review System Problems

### "Reviews not appearing!"

**Enable Course Reviews:**
1. ⚙️ **Check settings** - Reviews must be enabled
2. 👤 **User permissions** - Only enrolled users can review
3. ✅ **Course setting** - Individual courses must allow reviews
4. 🧹 **Clear review cache** - If using caching plugins

### "Star ratings not showing!"

**Fix Rating Display:**
```
[modern_courses
    show_reviews="yes"        # Must be yes
    template="premium"]       # Premium/detailed show ratings best
```

---

## 🔧 Advanced Troubleshooting

### Debug Mode (For Developers)

**Enable WordPress Debug:**
```php
// Add to wp-config.php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

**Check error log:** `/wp-content/debug.log`

### Common Error Messages

**"Fatal error: Allowed memory size..."**
- Solution: Increase PHP memory limit to 256M

**"Warning: Cannot modify header information..."**
- Solution: Remove whitespace before <?php tags

**"404 Page not found on course pages"**
- Solution: Refresh permalinks (Settings → Permalinks → Save)

---

## 📞 Still Need Help?

### Before Contacting Support:

**Gather This Information:**
```
✅ WordPress version: ____
✅ Reign theme version: ____
✅ LearnDash version: ____
✅ Addon version: ____
✅ Error messages: ____
✅ What you were doing when it broke: ____
```

### Get Support:
- 📧 **Email:** support@wbcomdesigns.com
- 📚 **Docs:** Check other guides first
- 💬 **Response time:** Usually within 24 hours

---

## 💡 Prevention Tips

### Avoid Future Issues:
1. **Always backup** before updates
2. **Test on staging** first if possible
3. **Update regularly** but not on Friday!
4. **Monitor performance** with Query Monitor plugin
5. **Document customizations** for future reference

---

*🛠️ Most issues are solved by clearing cache or checking settings!*