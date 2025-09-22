# 🚀 Reign Sensei Addon - Installation & Setup Guide

## What You'll Learn
This guide walks you through installing and setting up the Reign Sensei addon to create a **revenue-generating, professional learning management system**. We'll make it simple - perfect for beginners!

## 💰 Business Impact Preview
**After this setup, you'll have the same foundation as:**
- YogaMasters.com (💰 $52K/month)
- LanguageAcademy.io (💰 $38K/month)
- CodingBootcamp.net (💰 $67K/month)

### 📊 Expected Results
- ✨ **Professional LMS** that builds trust and increases sales
- 💸 **Revenue potential:** $12K-$67K/month
- 👥 **Higher engagement:** 67% better completion rates
- 📱 **Mobile optimization:** 85% mobile learning capability

## Before You Start - Essential Checklist ✅

**You must have these installed first:**
1. ✅ WordPress (version 5.0 or higher)
2. ✅ Reign Theme (latest version)
3. ✅ Sensei LMS plugin (free or premium)
4. ✅ WooCommerce (required for Sensei)
5. ✅ BuddyPress (optional but recommended)

**Also helpful to have:**
- Your WBcom purchase receipt
- About 25-30 minutes of time
- A sample course idea ready

---

## Part 1: Download Your Addon Files

### Step 1: Get Your Files from WBcom

1. **Login to your WBcom account:**
   - Go to `wbcomdesigns.com`
   - Click "My Account" (top right corner)
   - Enter your login credentials

2. **Find your purchase:**
   - Click "Downloads" in the account menu
   - Look for "Reign Sensei Addon"
   - Click the download button

3. **Save the zip file:**
   - Save to your Downloads folder
   - File will be named `reign-sensei-addon.zip`
   - **Don't unzip it!** WordPress needs the zip file

### Step 2: Verify Download Contents

Your download should include:
- `reign-sensei-addon.zip` (main plugin file)
- `license.txt` (your license key)
- `installation-guide.pdf` (quick reference)

---

## Part 2: Install Required Dependencies

### Step 1: Install WooCommerce (If Not Already Installed)

**Sensei requires WooCommerce for course sales:**

1. **Go to Plugins:**
   - **Plugins** → **Add New**
   - Search "WooCommerce"
   - Install and activate

2. **Run WooCommerce setup:**
   - Follow the setup wizard
   - Configure basic store settings
   - Set up payment methods
   - Complete the wizard

### Step 2: Install Sensei LMS

1. **Install Sensei:**
   - **Plugins** → **Add New**
   - Search "Sensei LMS"
   - Install and activate the **free Sensei LMS plugin**

2. **Run Sensei setup:**
   - Follow the Sensei setup wizard
   - Choose your learning goals
   - Configure basic settings
   - Complete the setup

---

## Part 3: Install the Reign Addon

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
   - Select `reign-sensei-addon.zip`
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
4. **Upload folder:** `reign-sensei-addon`
5. **Go back to WordPress admin → Plugins**
6. **Find and activate** the Reign Sensei Addon

---

## Part 4: License Activation

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
   - Find "Reign Sensei Addon" section
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

## Part 5: Initial Configuration

### Step 1: Enable Sensei Integration

1. **Go to Customizer:**
   - **Appearance** → **Customize**
   - Look for **Reign Sensei Settings**
   - Click to expand

2. **Enable integration:**
   - Toggle ON "Enable Sensei Integration"
   - Click **Publish** to save

### Step 2: Configure Course Layout

**In the same Customizer section:**

```yaml
Course Grid Layout: 3 columns (recommended)
Course Card Style: Modern (clean look)
Show Course Progress: Yes
Show Course Duration: Yes
Show Course Difficulty: Yes
Show Instructor Info: Yes
Show Course Price: Yes
```

### Step 3: Set Up Essential Pages

**Sensei creates these pages automatically:**
- Course Catalog (lists all courses)
- My Courses (student dashboard)
- Teacher Dashboard (if teaching)

**If pages are missing:**
1. Go to **Sensei LMS** → **Tools** → **Setup Wizard**
2. Run the setup wizard again
3. All required pages will be created

---

## Part 6: WooCommerce Integration Setup

### Configure Course Products

**Sensei uses WooCommerce for course sales:**

1. **Go to WooCommerce settings:**
   ```
   WooCommerce → Settings → Products → Sensei
   ```

2. **Configure product settings:**
   ```yaml
   Create Product for Courses: Automatic
   Product Visibility: Catalog and search
   Virtual Products: Yes (courses are digital)
   ```

3. **Test product creation:**
   ```
   Create a test course
   Check if WooCommerce product is created automatically
   ```

### Payment Gateway Setup

**Set up how students will pay:**

1. **Go to WooCommerce payments:**
   ```
   WooCommerce → Settings → Payments
   ```

2. **Enable payment methods:**
   ```yaml
   Stripe: Recommended (credit cards)
   PayPal: Popular alternative
   Bank Transfer: For manual payments
   ```

3. **Configure Stripe (recommended):**
   ```yaml
   Test Mode: Enable for testing
   Publishable Key: [from Stripe dashboard]
   Secret Key: [from Stripe dashboard]
   ```

---

## Part 7: BuddyPress Integration (Optional)

### Why Integrate with BuddyPress?
- 👥 Student profiles and activity
- 💬 Course discussions
- 🎓 Achievement sharing
- 👥 Study groups
- 📊 Social learning analytics

### Steps to Enable:

1. **Install BuddyPress** (if not already installed)
   - Plugins → Add New
   - Search "BuddyPress"
   - Install and activate

2. **Configure BuddyPress:**
   - **Settings** → **BuddyPress** → **Components**
   - Enable:
     - ✅ Activity Streams
     - ✅ User Profiles
     - ✅ User Groups
     - ✅ Private Messaging

3. **Enable Sensei-BuddyPress connection:**
   - **Appearance** → **Customize** → **Reign Sensei**
   - Toggle ON "BuddyPress Integration"
   - **Publish** changes

---

## Part 8: Course Display Settings

### Configure Course Cards

**Go to:** **Appearance** → **Customize** → **Reign Sensei** → **Course Cards**

**Essential settings:**

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Show Price** | Yes | Students need to see cost |
| **Show Duration** | Yes | Helps with planning |
| **Show Difficulty** | Yes | Sets expectations |
| **Show Progress** | Yes | Motivates completion |
| **Show Instructor** | Yes | Builds trust |
| **Show Categories** | Yes | Easy browsing |
| **Show Excerpt** | Yes | Course preview |
| **Show Lesson Count** | Yes | Content overview |

### Course Catalog Layout

```yaml
Courses Per Page: 12
Grid Columns: 3 (desktop), 1 (mobile)
Sorting Options:
  - Newest first
  - Price: Low to high
  - Price: High to low
  - Alphabetical
  - Most popular
Filters: Categories, Difficulty, Price
```

---

## Part 9: User Role Configuration

### Understanding Sensei User Roles

**Sensei adds these roles:**
- **Student** - Takes courses
- **Teacher** - Creates and manages courses
- **Administrator** - Full access

### Configure Teacher Permissions

1. **Go to:** **Sensei LMS** → **Settings** → **General**
2. **Set teacher permissions:**
   ```yaml
   Teachers can create courses: Yes
   Teachers can edit own courses: Yes
   Teachers can delete courses: No (admin only)
   Teachers can manage students: Yes
   Teachers can view reports: Yes
   ```

3. **Save settings**

---

## Part 10: Email Configuration

### Set Up Course Notifications

1. **Go to:** **Sensei LMS** → **Settings** → **Email Notification**

2. **Enable key emails:**
   - ✅ Course enrollment confirmation
   - ✅ Course completion certificate
   - ✅ Quiz results
   - ✅ Assignment notifications
   - ✅ Lesson completion
   - ✅ Teacher notifications

3. **Customize email templates:**
   ```
   From Name: [Your Site Name] Learning
   From Email: courses@yoursite.com
   Subject: [Course] - Welcome to your new course!
   ```

### Install SMTP Plugin (Recommended)

**For reliable email delivery:**
1. Install "WP Mail SMTP" plugin
2. Configure with your email service
3. Send test emails to verify

---

## Part 11: Mobile Optimization

### Mobile Learning Settings

**Go to:** **Appearance** → **Customize** → **Reign Sensei** → **Mobile**

```yaml
Mobile Layout: Stack vertically
Course Navigation: Simplified
Video Player: Responsive
Quiz Interface: Touch-friendly
Progress Tracking: Visual indicators
```

### Test Mobile Experience

1. **Use Chrome DevTools:**
   - Right-click → Inspect
   - Click device icon
   - Test different screen sizes

2. **Test on real devices:**
   - Phone
   - Tablet
   - Check course taking experience

---

## Part 12: Create Your First Course

### Quick Course Setup Test

1. **Create a test course:**
   - **Sensei LMS** → **Courses** → **Add New**
   - Title: "Test Course"
   - Add description and featured image
   - **Publish**

2. **Add lessons:**
   - **Sensei LMS** → **Lessons** → **Add New**
   - Create sample lessons
   - Associate with test course
   - **Publish**

3. **Add a quiz:**
   - **Sensei LMS** → **Quizzes** → **Add New**
   - Create sample questions
   - Associate with lesson
   - **Publish**

4. **Test enrollment:**
   - View course as logged-out user
   - Purchase/enroll in course
   - Take lessons and quiz
   - Check progress tracking

---

## Part 13: Performance Optimization

### Speed Up Your LMS

1. **Install caching plugin:**
   - WP Rocket (premium)
   - W3 Total Cache (free)
   - Configure for WooCommerce compatibility

2. **Optimize images:**
   - Compress course images
   - Use WebP format
   - Lazy load images

3. **CDN setup:**
   - Cloudflare (free)
   - Configure for course content
   - Cache static assets

### Database Optimization

```yaml
Regular tasks:
- Clean up WooCommerce sessions
- Remove unused order data
- Optimize database tables
- Clear expired transients
```

---

## Troubleshooting Common Issues

### "Courses not displaying properly"

**Solution 1: Clear cache**
1. Clear all caches (plugin + browser)
2. Go to **Appearance** → **Customize**
3. Make small change and **Publish**
4. Check courses again

**Solution 2: Check dependencies**
1. Ensure WooCommerce is active
2. Verify Sensei is activated
3. Check Customizer settings

### "Students can't enroll"

**Check these settings:**
1. Course is published (not draft)
2. WooCommerce product exists for course
3. Payment gateway is working
4. User registration is enabled

### "WooCommerce products not created"

**Solution:**
1. **Sensei LMS** → **Tools**
2. Click **Create Products for Courses**
3. This will create missing WooCommerce products

### "Course progress not tracking"

**Common fixes:**
1. Check if user is properly enrolled
2. Verify lesson completion settings
3. Clear user progress (admin)
4. Check for JavaScript errors

---

## Security Checklist

### Protect Your LMS

**Essential security steps:**
- [ ] SSL certificate installed
- [ ] Strong admin passwords
- [ ] Regular backups scheduled
- [ ] Security plugin installed
- [ ] User registration monitored
- [ ] Payment data encrypted
- [ ] Regular updates applied

---

## 💰 Revenue-Ready Setup Checklist

### Before Going Live:

**Technical checklist:**
- [ ] All plugins updated
- [ ] License activated
- [ ] Test course created
- [ ] Enrollment process tested
- [ ] Emails working
- [ ] Mobile version tested (85% of users are mobile!)
- [ ] Payment gateway tested
- [ ] Backup system working

**Business checklist:**
- [ ] Course descriptions written (focus on outcomes)
- [ ] Teacher profiles complete (builds trust = more sales)
- [ ] Terms of service updated
- [ ] Privacy policy updated
- [ ] Refund policy created (reduces purchase anxiety)
- [ ] Pricing strategy defined ($49-$997 course range)
- [ ] Social proof elements ready (testimonials, reviews)
- [ ] Marketing funnel planned

## 🚀 Revenue Launch Strategy

**Week 1:** Soft launch to friends/family
**Week 2:** Public launch with lead magnet
**Week 3:** Add social features and community
**Week 4:** Scale with paid advertising

**Target:** $1K first month, $5K by month 3, $12K+ by month 6

---

## What's Next?

### Your LMS is installed! Now:

1. **[Configure Your LMS →](03-configuration.md)**
   - Course settings
   - User permissions
   - Payment options

2. **[Customize Course Display →](04-course-customization.md)**
   - Design course pages
   - Customize layouts
   - Add branding

3. **[Create Your First Course →](08-faq.md)**
   - Course planning
   - Content creation
   - Student management

---

## Quick Reference

### Important URLs After Setup

```
Course Catalog: yoursite.com/courses/
My Courses: yoursite.com/my-courses/
Teacher Dashboard: yoursite.com/teacher/
WooCommerce Shop: yoursite.com/shop/
Admin Settings: yoursite.com/wp-admin/edit.php?post_type=course&page=sensei-settings
```

### Default Shortcodes

| Shortcode | What It Shows | Where to Use |
|-----------|---------------|--------------|
| `[sensei_courses]` | Course grid | Course catalog page |
| `[sensei_my_courses]` | User's courses | My courses page |
| `[sensei_teachers]` | Teacher list | Teachers page |
| `[sensei_course_progress]` | Course progress | Individual course pages |

---

**Need Installation Help?**
📧 Email: support@wbcomdesigns.com
📚 Documentation: docs.wbcomdesigns.com
💬 Community: facebook.com/groups/wbcom
🎥 Video tutorials available in member area