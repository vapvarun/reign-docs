# Reign LearnDash Addon - Complete Installation & Setup Guide

## 🏗️ Building Your Online Academy Foundation

This guide walks you through installing and setting up your Reign LearnDash Addon step-by-step. By the end, you'll have a fully functional online learning platform with beautiful course displays, social features, and professional design.

## 📋 Before You Start (Requirements Check)

### ✅ Required Components (Must Have These First)
1. **WordPress 4.0+** *(Most hosting providers have this)*
2. **Reign Theme** activated *(Your academy's beautiful foundation)*
3. **LearnDash LMS plugin** active *(The learning engine)*
4. **Reign LearnDash Addon** *(From your WBcom account)*

### 🎁 Optional Components (Nice to Have)
- **BuddyPress** - Adds social learning features and student community
- **WooCommerce** - For advanced payment processing
- **MailChimp** - For student email marketing

*Missing something? Links to get everything are provided below!*

---

---

## 🚀 Installation Process (15 minutes)

### Step 1: Get Your Addon (5 minutes)

**Option A: Download from WBcom Account**
1. **Login to** [WBcom Designs Account](https://wbcomdesigns.com/my-account/)
2. **Navigate to** Downloads → Reign LearnDash Addon
3. **Download** the `reign-learndash-addon.zip` file

**Option B: Already have the file?** Perfect! Continue to Step 2.

---

### Step 2: Install via WordPress (5 minutes)

**Easy Installation Method:**
1. **Go to** WordPress Admin → Plugins → Add New → Upload Plugin
2. **Choose file** and select your `reign-learndash-addon.zip`
3. **Click** "Install Now"
4. **Click** "Activate" when installation completes

**Alternative: FTP Installation** *(For developers)*
```
1. Extract the ZIP file
2. Upload folder to: /wp-content/plugins/reign-learndash-addon/
3. Activate from WordPress Admin → Plugins
```

**✅ Success Check:** You should see "Reign LearnDash Addon" in your active plugins list.

---

### Step 3: Verify Everything Works (5 minutes)

**Quick Functionality Test:**
1. **Create test page:** Pages → Add New → Title it "Test Courses"
2. **Add this shortcode:**
   ```
   [modern_courses]
   ```
3. **Publish and view** - You should see beautiful course displays!

**✅ Milestone:** Your learning platform is installed and working!

---

---

## 🎯 Initial Configuration (10 minutes)

### Configure Your Course Archive Pages

**Purpose:** Make your course catalog look professional and organized.

1. **Navigate to** Appearance → Customize
2. **Find** LearnDash Groups settings (if available)
3. **Configure these essential options:**

   **Display Settings:**
   - ✅ Archive title: "Our Courses" or "Academy"
   - ✅ Columns: 3 (perfect for desktop viewing)
   - ✅ Template: "Premium" (best conversion rates)

   **Features to Enable:**
   - ✅ Search bar (helps students find courses)
   - ✅ Filters (category, price, level)
   - ✅ Sorting (popular, newest, price)
   - ✅ Pagination (12-16 courses per page)

---

### Create Your Main Course Pages

**Course Catalog Page (Essential):**
```
[modern_courses]
```
**Pro version with all features:**
```
[modern_courses per_page="12" columns="3" template="premium" udemy_style="yes"]
```

**Learning Groups Page (For Community):**
```
[modern_groups]
```
**Enhanced with member display:**
```
[modern_groups columns="4" show_search="yes" show_members="yes"]
```

**Business Tip:** These pages are your main revenue drivers - make them prominent in your menu!

---

---

## ✅ Test Your Academy (5 minutes)

**Success Checklist - Make sure everything works:**

### Course Display Test
- [ ] **Visit** `/courses/` - Should look professional with Reign styling ✅
- [ ] **Check** course cards - Reviews, prices, and instructors visible ✅
- [ ] **Test** on mobile - Everything responsive and touch-friendly ✅

### Shortcode Functionality
- [ ] **Create test page** with `[modern_courses]` ✅
- [ ] **View page** - Courses display beautifully ✅
- [ ] **Try filters** - Search and sorting work ✅

### Design Consistency
- [ ] **Colors match** your Reign theme ✅
- [ ] **Fonts consistent** throughout ✅
- [ ] **Mobile layout** works perfectly ✅

**🎉 All green? Perfect! Your academy is ready for students!**

---

---

## 🚨 Troubleshooting (If Something's Wrong)

### Problem: Shortcodes Show as Text
**Quick fixes (90% success rate):**
- ✅ **Verify addon is activated** (check Plugins page)
- ✅ **Ensure you have courses** (create at least 1 test course)
- ✅ **Test simple shortcode** `[modern_courses]`
- ✅ **Clear all caches** (browser + WordPress)

### Problem: Courses Look Plain/Unstyled
**Solutions:**
- ✅ **Clear browser cache** (Ctrl+F5 or Cmd+Shift+R)
- ✅ **Confirm Reign theme is active** (not just installed)
- ✅ **Deactivate other** course-related plugins temporarily
- ✅ **Check for** JavaScript errors (F12 → Console)

### Problem: Pages Not Found (404 Errors)
**Fix in 30 seconds:**
- ✅ **Go to** Settings → Permalinks
- ✅ **Click** "Save Changes" (refreshes URLs)
- ✅ **Test again** - usually fixes it!

---

---

## 🚀 What's Next?

### Immediate Next Steps:
1. **[Complete Configuration](03-configuration.md)** - Fine-tune all academy settings
2. **[Customize Course Appearance](04-course-customization.md)** - Match your brand perfectly
3. **[Master All Shortcodes](06-shortcodes-reference.md)** - Unlock advanced features

### Business Setup:
- Create your first course
- Set up pricing and payment
- Configure student enrollment
- Plan your course launch

### Growth Features:
- Add BuddyPress for social learning
- Enable course reviews for social proof
- Set up email marketing
- Create student certificates

---

## 🆘 Need More Help?

- **[FAQ](08-faq.md)** - Common questions and answers
- **[Troubleshooting Guide](07-troubleshooting.md)** - Fix specific issues
- **[Developer Guide](05-developer-guide.md)** - Advanced customization
- **[Support](mailto:support@wbcomdesigns.com)** - Contact our team

---

*🏗️ Installation Complete! Your online academy foundation is solid and ready to grow.*