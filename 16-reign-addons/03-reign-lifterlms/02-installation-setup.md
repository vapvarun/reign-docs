# Reign LifterLMS Addon - Installation & Setup (Complete)

## Overview

This guide provides comprehensive installation and setup instructions for Reign LifterLMS Addon v2.4.1, including advanced shortcode configuration, BuddyPress integration, widget setup, and dashboard customization.

## Prerequisites

**Required Components:**
1. ✅ WordPress 5.8+
2. ✅ Reign Theme (latest version)
3. ✅ LifterLMS plugin (latest version)
4. ✅ Reign LifterLMS Addon license

**Optional Components:**
- BuddyPress (for social learning features)
- WooCommerce (for LifterLMS WooCommerce extension)

## Installation Process

---

## Part 1: Download Your Addon Files

### Step 1: Get Your Files from WBcom

1. **Login to your WBcom account:**
   - Go to `wbcomdesigns.com`
   - Click "My Account" (top right corner)
   - Enter your login credentials

2. **Find your purchase:**
   - Click "Downloads" in the account menu
   - Look for "Reign LifterLMS Addon"
   - Click the download button

3. **Save the zip file:**
   - Save to your Downloads folder
   - File will be named `reign-lifterlms-addon.zip`
   - **Don't unzip it!** WordPress needs the zip file

### Step 2: Verify Download Contents

Your download should include:
- `reign-lifterlms-addon.zip` (main plugin file)
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
   - Select `reign-lifterlms-addon.zip`
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
4. **Upload folder:** `reign-lifterlms-addon`
5. **Go back to WordPress admin → Plugins**
6. **Find and activate** the Reign LifterLMS Addon

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
   - Find "Reign LifterLMS Addon" section
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

## Part 4: Initial Configuration

### Step 1: Enable LifterLMS Integration

1. **Go to Customizer:**
   - **Appearance** → **Customize**
   - Look for **Reign LifterLMS Settings**
   - Click to expand

2. **Enable integration:**
   - Toggle ON "Enable LifterLMS Integration"
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
```

### Step 3: Set Up Essential Pages

**LifterLMS creates these pages automatically:**
- Course Catalog (lists all courses)
- Student Dashboard
- Checkout Page
- My Account Page

**If pages are missing:**
1. Go to **LifterLMS** → **Settings** → **Pages**
2. Click **Install LifterLMS Pages** button
3. All required pages will be created

---

## Part 5: BuddyPress Integration (Optional)

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

3. **Enable LifterLMS-BuddyPress connection:**
   - **Appearance** → **Customize** → **Reign LifterLMS**
   - Toggle ON "BuddyPress Integration"
   - **Publish** changes

---

## Part 6: Course Display Settings

### Configure Course Cards

**Go to:** **Appearance** → **Customize** → **Reign LifterLMS** → **Course Cards**

**Essential settings:**

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Show Price** | Yes | Students need to see cost |
| **Show Duration** | Yes | Helps with planning |
| **Show Difficulty** | Yes | Sets expectations |
| **Show Progress** | Yes | Motivates completion |
| **Show Instructor** | Yes | Builds trust |
| **Show Categories** | Yes | Easy browsing |
| **Show Enrollment Count** | Optional | Social proof |

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

## Part 7: User Role Configuration

### Understanding User Roles

**LifterLMS adds these roles:**
- **Student** - Takes courses
- **Instructor** - Creates and manages courses
- **Assistant Instructor** - Helps with course management

### Configure Instructor Capabilities

1. **Go to:** **LifterLMS** → **Settings** → **General**
2. **Set instructor permissions:**
   ```yaml
   Can create courses: Yes
   Can edit own courses: Yes
   Can delete courses: No (admin only)
   Can manage students: Yes
   Can view reports: Yes
   Can issue certificates: Yes
   ```

3. **Save settings**

---

## Part 8: Email Configuration

### Set Up Course Notifications

1. **Go to:** **LifterLMS** → **Settings** → **Notifications**

2. **Enable key emails:**
   - ✅ Course enrollment confirmation
   - ✅ Course completion certificate
   - ✅ Quiz results
   - ✅ Assignment notifications
   - ✅ Lesson completion

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

## Part 9: Payment Gateway Setup

### Configure Stripe Integration

**LifterLMS includes Stripe by default:**

1. **Go to:** **LifterLMS** → **Settings** → **Checkout**
2. **Enable Stripe:**
   ```yaml
   Test Mode: Enable for testing
   Publishable Key: [from Stripe dashboard]
   Secret Key: [from Stripe dashboard]
   Currency: USD (or your currency)
   ```

### Alternative: PayPal Integration

**For PayPal payments:**
1. Install "LifterLMS PayPal" addon
2. Get PayPal API credentials
3. Configure in LifterLMS settings
4. Test with small amounts first

---

## Part 10: Mobile Optimization

### Mobile Learning Settings

**Go to:** **Appearance** → **Customize** → **Reign LifterLMS** → **Mobile**

```yaml
Mobile Layout: Stack vertically
Course Navigation: Bottom bar
Video Player: Responsive
Quiz Interface: Touch-friendly
Progress Tracking: Simplified
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

## Part 11: Create Your First Course

### Quick Course Setup Test

1. **Create a test course:**
   - **Courses** → **Add New**
   - Title: "Test Course"
   - Add description and featured image
   - **Publish**

2. **Add lessons:**
   - In course editor, click **Add Lesson**
   - Create sample lessons
   - Add video or text content
   - **Publish**

3. **Add a quiz:**
   - Click **Add Quiz** in course editor
   - Create sample questions
   - Set passing grade
   - **Publish**

4. **Test enrollment:**
   - View course as logged-out user
   - Enroll in course
   - Take lessons and quiz
   - Check progress tracking

---

## Part 12: Performance Optimization

### Speed Up Your LMS

1. **Install caching plugin:**
   - WP Rocket (premium)
   - W3 Total Cache (free)
   - Configure for LifterLMS

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
- Clean up spam comments
- Remove unused plugins
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

**Solution 2: Check theme integration**
1. Ensure Reign theme is active
2. Verify addon is activated
3. Check Customizer settings

### "Students can't enroll"

**Check these settings:**
1. Course is published (not draft)
2. Course enrollment is enabled
3. Payment gateway is working
4. User registration is enabled

### "Lessons won't advance"

**Common fixes:**
1. Check lesson prerequisites
2. Verify lesson completion settings
3. Clear student progress (admin)
4. Check for JavaScript errors

### "Certificates not generating"

**Solution:**
1. **LifterLMS** → **Certificates**
2. Ensure certificate template exists
3. Associate with course
4. Test course completion

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

## Final Setup Checklist

### Before Going Live:

**Technical checklist:**
- [ ] All plugins updated
- [ ] License activated
- [ ] Test course created
- [ ] Enrollment process tested
- [ ] Emails working
- [ ] Mobile version tested
- [ ] Payment gateway tested
- [ ] Backup system working

**Content checklist:**
- [ ] Course descriptions written
- [ ] Instructor profiles complete
- [ ] Terms of service updated
- [ ] Privacy policy updated
- [ ] Refund policy created

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
Student Dashboard: yoursite.com/dashboard/
Checkout: yoursite.com/checkout/
My Account: yoursite.com/my-account/
Admin Settings: yoursite.com/wp-admin/admin.php?page=llms-settings
```

### Default Shortcodes

| Shortcode | What It Shows | Where to Use |
|-----------|---------------|---------------|
| `[lifterlms_courses]` | Course grid | Course catalog page |
| `[lifterlms_my_account]` | User dashboard | My account page |
| `[lifterlms_checkout]` | Checkout form | Checkout page |
| `[lifterlms_course_outline]` | Course content | Course pages |

---

**Need Installation Help?**  
📧 Email: support@wbcomdesigns.com  
📚 Documentation: docs.wbcomdesigns.com  
💬 Community: facebook.com/groups/wbcom  
🎥 Video tutorials available in member area