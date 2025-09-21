# Reign LearnDash Addon - Configuration Guide

## What You'll Learn
This guide shows you how to configure every aspect of your LearnDash LMS with the Reign addon. We'll explain each setting in simple terms so you can make the right choices for your learning platform.

## Quick Overview
**Time needed:** 60-90 minutes for complete configuration  
**Difficulty:** Easy (mostly clicking options!)  
**Result:** A fully configured learning management system

---

## Part 1: Core LearnDash Settings

### Step 1: General LMS Configuration

**Where to go:**
```
WP Admin → LearnDash LMS → Settings → General
```

**Essential settings:**

| Setting | Recommended Value | Why |
|---------|------------------|-----|
| **Course Builder** | Course Builder | Easier course creation |
| **Shared Course Steps** | Enabled | Share lessons between courses |
| **Course Navigation Widget** | Enabled | Better navigation |
| **Lesson Video Progression** | Enabled | Ensure students watch videos |
| **Quiz Result Points** | Enabled | Show quiz scores |
| **Statistics Widgets** | Enabled | Track progress |

### Step 2: Course Access Settings

**Course progression options:**

| Access Type | How It Works | Best For |
|-------------|--------------|----------|
| **Open** | Anyone can access | Free courses |
| **Buy Now** | Payment required | Paid courses |
| **Recurring** | Subscription model | Ongoing access |
| **Closed** | Admin enrollment only | Private training |

**Recommended settings:**
```yaml
Default Access Mode: Buy Now
Course Prerequisites: Enabled
Lesson Progression: Linear (students must complete in order)
Quiz Progression: Required (must pass to continue)
```

---

## Part 2: Course Display Configuration

### Course Archive Settings

**Where to go:**
```
Appearance → Customize → Reign LearnDash → Course Archive
```

**Layout options:**

```yaml
Courses Per Page: 12
Grid Layout: 3 columns (desktop), 1 column (mobile)
Sorting Options:
  - Newest first
  - Price: Low to high
  - Price: High to low
  - Alphabetical
  - Most enrolled
  - Highest rated
```

### Course Card Configuration

**What to show on course cards:**

| Element | Show? | Purpose |
|---------|-------|----------|
| **Course Image** | ✅ Always | Visual appeal |
| **Course Title** | ✅ Always | Identification |
| **Instructor Name** | ✅ Yes | Credibility |
| **Course Price** | ✅ Yes | Clear pricing |
| **Course Duration** | ✅ Yes | Time commitment |
| **Difficulty Level** | ✅ Yes | Skill matching |
| **Student Count** | Optional | Social proof |
| **Course Rating** | After 5 ratings | Quality indicator |
| **Course Progress** | Enrolled only | Track completion |

**Configure in:**
```
Appearance → Customize → Reign LearnDash → Course Cards
```

---

## Part 3: User Experience Settings

### Student Dashboard Configuration

**Dashboard sections to enable:**

```yaml
User Profile: Yes (show progress)
My Courses: Yes (enrolled courses)
Course Progress: Yes (completion status)
Achievements: Yes (certificates, badges)
Assignments: Yes (if using assignments)
Quiz Results: Yes (performance tracking)
Discussion Forums: Yes (if using bbPress)
```

### Lesson Display Settings

**Where to configure:**
```
LearnDash LMS → Settings → Lessons
```

**Recommended settings:**

| Setting | Value | Benefit |
|---------|-------|----------|
| **Lesson Progression** | Linear | Structured learning |
| **Show Lesson List** | Yes | Clear navigation |
| **Lesson Comments** | Enabled | Student interaction |
| **Lesson Timer** | Optional | Focus sessions |
| **Video Progression** | Enabled | Ensure completion |
| **Auto-Complete** | After timer | Automatic progress |

### Quiz Configuration

**Essential quiz settings:**

```yaml
Quiz Attempts: 3 maximum
Passing Grade: 70%
Show Correct Answers: After completion
Quiz Timer: Course dependent
Question Randomization: Enabled
Result Display: Percentage + Letter grade
```

---

## Part 4: Payment & Enrollment

### Payment Gateway Setup

**Option 1: PayPal Integration**

**Where to configure:**
```
LearnDash LMS → Settings → PayPal
```

**Settings:**
```yaml
PayPal Email: your-paypal@email.com
Currency: USD (or your local currency)
Country: Your country code
Sandbox Mode: Enable for testing
NotifyURL: Auto-generated
ReturnURL: Thank you page
CancelURL: Course page
```

**Option 2: WooCommerce Integration** (Recommended)

**Benefits:**
- More payment gateways
- Better checkout experience
- Advanced e-commerce features
- Detailed sales reports

**Setup:**
1. Install WooCommerce
2. Go to **LearnDash LMS** → **Add-ons**
3. Enable **WooCommerce Integration**
4. Configure product creation

### Pricing Strategies

**Common pricing models:**

| Model | How It Works | Best For |
|-------|--------------|----------|
| **One-time Purchase** | Pay once, lifetime access | Skill courses |
| **Subscription** | Monthly/yearly recurring | Ongoing programs |
| **Tiered Pricing** | Different access levels | Comprehensive programs |
| **Bundle Pricing** | Multiple courses together | Course series |
| **Free + Premium** | Basic free, advanced paid | Lead generation |

---

## Part 5: User Roles & Permissions

### Understanding LearnDash Roles

**Default user roles:**

| Role | Capabilities | Use Case |
|------|--------------|----------|
| **Student** | Take courses, view progress | Course learners |
| **Instructor** | Create courses, manage students | Course creators |
| **Group Leader** | Manage assigned groups | Team leaders |
| **Administrator** | Full access | Site owners |

### Configure Instructor Permissions

**Where to set:**
```
LearnDash LMS → Settings → General → Course Builder
```

**Instructor capabilities:**

```yaml
Can Create Courses: Yes
Can Edit Own Courses: Yes
Can Delete Courses: No (admin only)
Can Manage Students: Yes (enrolled in their courses)
Can View Reports: Yes (own courses only)
Can Issue Certificates: Yes
Can Create Quizzes: Yes
Can Moderate Comments: Yes
```

### Group Management Settings

**For corporate training:**

```yaml
Group Leaders Can:
  - Enroll users in group courses
  - View group progress reports
  - Assign courses to group
  - Export group data
  - Communicate with group members
```

---

## Part 6: Certificates & Awards

### Certificate Configuration

**Where to set up:**
```
LearnDash LMS → Certificates
```

**Certificate settings:**

```yaml
Automatic Issuance: Yes
Download Format: PDF
Certificate Template: Custom design
Include Information:
  - Student name
  - Course title
  - Completion date
  - Instructor signature
  - Unique certificate ID
```

### Badges & Achievements

**Set up achievement system:**

1. **Enable badges:**
   - Install "BadgeOS" plugin
   - Configure achievement types
   - Set earning criteria

2. **Common achievements:**
   - Course completion
   - Quiz mastery (90%+ score)
   - Perfect attendance
   - Fast learner
   - Community participation

---

## Part 7: Content Protection

### Lesson Protection Settings

**Prevent content theft:**

```yaml
Disable Right-Click: Enabled
Disable Text Selection: Enabled
Watermark Videos: Recommended
Login Required: Always
IP Address Tracking: For suspicious activity
Device Limits: 3 devices per user
```

### Video Protection

**For video courses:**

```yaml
Video Hosting: Vimeo Pro or Wistia
DRM Protection: Enabled
Playback Speed Control: Limited
Skip Prevention: Enabled
Download Prevention: Enabled
Time-based Access: Optional
```

---

## Part 8: Assessment Configuration

### Quiz Settings Deep Dive

**Advanced quiz options:**

```yaml
Question Types Enabled:
  - Multiple Choice
  - True/False
  - Fill in the Blank
  - Essay
  - Ordering
  - Matching
  - Image Choice

Grading Options:
  - Automatic grading (non-essay)
  - Manual review (essay questions)
  - Partial credit
  - Negative scoring
```

### Assignment Configuration

**If using assignments:**

```yaml
File Upload Types: PDF, DOC, DOCX, TXT
Max File Size: 10MB
Submission Deadline: Course dependent
Late Submissions: Penalty or block
Instructor Review: Required
Rubric Grading: Enabled
```

---

## Part 9: Communication Settings

### Course Forums Integration

**With bbPress plugin:**

```yaml
Course Forums: Enabled
Forum per Course: Yes
Student Participation: Encouraged
Instructor Moderation: Yes
Anonymous Posts: No
Email Notifications: Yes
```

### Private Messaging

**Student-instructor communication:**

```yaml
Private Messages: Enabled
Message Notifications: Email + Dashboard
Instructor Response Time: 24-48 hours
File Attachments: Limited types
Message History: Preserved
```

---

## Part 10: Reports & Analytics

### Progress Tracking

**What to track:**

```yaml
Student Progress:
  - Course completion percentage
  - Time spent per lesson
  - Quiz attempts and scores
  - Last activity date
  - Certificate status

Course Analytics:
  - Enrollment numbers
  - Completion rates
  - Average scores
  - Popular content
  - Drop-off points
```

### Export Options

**Data export formats:**
- CSV files for Excel
- PDF reports
- Email summaries
- API integration

---

## Part 11: Mobile Learning Configuration

### Mobile App Settings

**If using LearnDash mobile app:**

```yaml
Offline Content: Limited lessons
Push Notifications: Course updates
App Branding: Your logo and colors
In-App Purchases: Course enrollment
Progress Sync: Real-time
```

### Mobile Web Optimization

```yaml
Responsive Design: Enabled
Touch-Friendly: Quiz interfaces
Mobile Video: Optimized streaming
Offline Reading: PDF downloads
Mobile Navigation: Simplified
```

---

## Part 12: SEO & Marketing Configuration

### Course SEO Settings

**Help courses rank in Google:**

```yaml
SEO Plugin: Yoast or RankMath
Course URLs: /courses/course-name/
Meta Descriptions: Compelling course summaries
Schema Markup: Course structured data
Sitemap Inclusion: Enabled
```

### Social Sharing

```yaml
Share Buttons: Course pages
Open Graph: Course images and descriptions
Twitter Cards: Course previews
LinkedIn Integration: Professional courses
```

---

## Configuration for Different Learning Models

### Corporate Training Setup

```yaml
Access: Closed (admin enrollment)
Groups: Department-based
Reporting: Detailed completion tracking
Certificates: Required for compliance
Forum: Internal discussions
Branding: Company colors and logo
```

### Online School Setup

```yaml
Access: Paid enrollment
Progression: Semester-based
Grading: Letter grades
Assignments: Heavy use
Forums: Class discussions
Calendar: Semester scheduling
```

### Professional Development

```yaml
Access: Individual purchase
Certificates: CEU credits
Self-paced: Flexible timing
Practical: Hands-on projects
Networking: Peer connections
Portfolio: Work samples
```

### Hobby/Interest Courses

```yaml
Access: Mix of free and paid
Progression: Self-paced
Community: Strong forums
Creativity: Project sharing
Casual: Low pressure
Inspiration: Success stories
```

---

## Quick Settings Reference

### Most Important Setting Locations

```
General: LearnDash LMS → Settings → General
Courses: LearnDash LMS → Settings → Courses  
Lessons: LearnDash LMS → Settings → Lessons
Quizzes: LearnDash LMS → Settings → Quizzes
Display: Appearance → Customize → Reign LearnDash
Payments: LearnDash LMS → Settings → PayPal
```

### Recommended Starter Settings

```yaml
Course Access: Buy Now
Lesson Progression: Linear
Quiz Passing: 70%
Certificates: Automatic
Reports: Enabled
Mobile: Responsive
SEO: Optimized
Security: Protected
```

---

## Testing Your Configuration

### Essential Tests Before Launch

1. **Create test student account**
2. **Enroll in test course**
3. **Complete lesson progression**
4. **Take quiz and get certificate**
5. **Test payment process**
6. **Check mobile experience**
7. **Verify email notifications**
8. **Test instructor dashboard**

---

## Performance Optimization

### Speed Up Your LMS

```yaml
Caching: WP Rocket or W3 Total Cache
CDN: Cloudflare for global delivery
Image Optimization: Compress course images
Database: Regular cleanup
Hosting: LMS-optimized servers
Video: External hosting (Vimeo/Wistia)
```

---

## Next Steps

**Your LMS is configured! Now:**

1. **[Customize Course Appearance →](04-course-customization.md)**
2. **[Set Up Developer Tools →](05-developer-guide.md)**
3. **[Create Your First Course →](08-faq.md)**

---

**Need Configuration Help?**  
📧 Email: support@wbcomdesigns.com  
📚 Full Docs: docs.wbcomdesigns.com  
💬 Community: facebook.com/groups/wbcom  
🎥 Training videos available in member portal