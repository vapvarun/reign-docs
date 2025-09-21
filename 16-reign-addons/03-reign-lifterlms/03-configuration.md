# Reign LifterLMS Addon - Configuration Guide (Complete)

## Overview

The Reign LifterLMS Addon v2.4.1 provides extensive configuration options for learning management, BuddyPress integration, course display customization, and enhanced student dashboards. This guide covers all available settings and customization options.

## Shortcode Configuration

### [reign_lifterlms_courses] Settings

**Basic Configuration:**
```
[reign_lifterlms_courses posts_per_page="12" per_row="3"]
```

**Complete Parameter Options:**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `posts_per_page` | -1 | Any number | Number of courses to display (-1 for all) |
| `per_row` | 3 | 1-6 | Number of columns in grid layout |
| `enable_slider` | false | true, false | Enable slider/carousel functionality |
| `id` | - | Comma-separated IDs | Specific course IDs to display |
| `category` | - | Category slug | Filter by course category |

### [reign_lifterlms_instructors] Settings

**Basic Configuration:**
```
[reign_lifterlms_instructors per_row="4"]
```

**Complete Parameter Options:**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_row` | 4 | 1-6 | Number of columns for instructor display |
| `total` | - | Any number | Limit number of instructors shown |
| `enable_slider` | false | true, false | Enable slider/carousel functionality |

## BuddyPress Integration Configuration

### Activity Stream Integration

**Activity Types Configuration:**
- Course enrollment activities
- Course completion activities
- Lesson completion activities
- Quiz participation (pass/fail) activities
- Certificate earning activities
- Achievement earning activities

**Settings Location:**
```
Reign Settings → LifterLMS → BuddyPress Integration
```

### Profile Integration

**Enable BuddyPress Features:**
```
Reign Settings → LifterLMS → BuddyPress Integration
```

**Profile Integration Settings:**
- Courses tab in member profiles
- Individual activity preferences
- Course progress display in social profiles
- Learning achievements in profiles

### Group Learning Features

**Course-Group Integration:**
- Link courses to BuddyPress groups
- Auto-enroll course students in linked groups
- Group-specific activity feeds within groups
- Bulk student management processes

## Widget System Configuration

### Available Widgets (7 Types)

#### 1. Course Categories Widget

**Configuration Options:**
- Hierarchical category display
- Course count per category
- Customizable styling options

**Widget Settings:**
```
Appearance → Widgets → Course Categories Widget
Show Course Count: Yes
Hide Empty Categories: No
Order By: Name
Display Style: List
```

#### 2. Course Difficulties Widget

**Display Settings:**
- Beginner, Intermediate, Advanced filtering
- Visual difficulty indicators
- Course count per level

#### 3. Course Search Widget

**Search Features:**
- Course title search functionality
- Category filtering integration
- Advanced search options

#### 4. Course Listing Widget

**Display Options:**
- Featured courses display
- Recent courses listing
- Category-specific courses
- Customizable course counts

#### 5. Course Overview Widget

**Information Display:**
- Course details summary
- Enrollment information
- Progress indicators

#### 6. Membership Listing Widget

**Membership Features:**
- Membership plan showcases
- Pricing information display
- Feature comparisons

#### 7. Enrolled Students Widget

**Student Display:**
- Total enrolled students
- Recent enrollments
- Student avatars/profiles

## Dashboard Configuration

### Student Dashboard Enhancement

**Dashboard Navigation Styles:**
- **Style 1**: Traditional dashboard with sidebar navigation
- **Style 2**: Modern tabbed interface with horizontal navigation

**Configuration Location:**
```
Reign Settings → LifterLMS → Dashboard Settings
```

### Dashboard Layout Options

**Settings:**
- Dashboard title customization
- Items per row for different sections
- Course archive layout (courses per row)
- Membership archive layout (memberships per row)
- Dashboard items per row configuration

### Display Element Controls

**Toggle Options:**
- Hide/show instructor tab
- Hide/show course author
- Hide/show course date
- Hide/show course meta
- Hide/show course thumbnail

## Template System Configuration

### Distraction-Free Learning Mode

**Enable Distraction-Free Layout:**
```
Reign Settings → LifterLMS → Enable Distraction-Free Layout
```

**Features:**
- Removes site header and footer on lesson pages
- Minimal navigation for focused learning
- Clean, distraction-free interface
- Mobile-optimized layout

### Template Override System

**Available Templates for Override:**
- Single course page templates
- Single lesson/quiz/assignment templates
- Course archive page templates
- Membership archive page templates
- Student dashboard section templates

**Override Location:**
```
/wp-content/themes/reign-child/lifterlms/
```

## Review System Configuration

### Enhanced Course Reviews

**Review Features:**
- Interactive AJAX-powered star ratings
- Detailed rating breakdowns (1-5 star distribution)
- Average rating calculations with review counts
- BuddyPress activity stream integration for reviews

**Configuration:**
```
LifterLMS → Settings → Reviews
Enable Course Reviews: Yes
Review Moderation: Optional
Guest Reviews: Admin Choice
Review Analytics: Enabled
```

## Related Courses Configuration

### Algorithm Settings

**Relationship Factors:**
- Category-based recommendations (primary)
- Tag-based associations
- Instructor relationships
- Course difficulty level matching
- User enrollment history

**Display Configuration:**
```
Reign Settings → LifterLMS → Related Courses
Number of Related Courses: 6
Related Courses Title: "You might also like"
Display Template: Grid
Show on Course Pages: Yes
```

### Step 2: Course Access Settings

**Course enrollment options:**

| Access Type | How It Works | Best For |
|-------------|--------------|----------|
| **Open** | Anyone can access | Free courses |
| **Purchase** | Payment required | Paid courses |
| **Membership** | Subscription access | Ongoing programs |
| **Private** | Admin enrollment only | Corporate training |

**Recommended settings:**
```yaml
Default Course Access: Purchase
Course Prerequisites: Enabled
Lesson Progression: Sequential
Quiz Progression: Required passing
```

---

## Part 2: Course Display Configuration

### Course Catalog Settings

**Where to go:**
```
Appearance → Customize → Reign LifterLMS → Course Catalog
```

**Layout options:**

```yaml
Courses Per Page: 12
Grid Layout: 3 columns (desktop), 1 column (mobile)
Sorting Options:
  - Date (newest first)
  - Price (low to high)
  - Price (high to low)
  - Alphabetical
  - Most popular
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
| **Course Length** | ✅ Yes | Time commitment |
| **Difficulty Level** | ✅ Yes | Skill matching |
| **Student Count** | Optional | Social proof |
| **Course Rating** | After 5 ratings | Quality indicator |
| **Course Progress** | Enrolled only | Track completion |

**Configure in:**
```
Appearance → Customize → Reign LifterLMS → Course Cards
```

---

## Part 3: Student Experience Settings

### Student Dashboard Configuration

**Dashboard sections to enable:**

```yaml
My Courses: Yes (enrolled courses)
My Achievements: Yes (earned certificates)
My Memberships: Yes (if using memberships)
Order History: Yes (purchase records)
Account Settings: Yes (profile management)
Notifications: Yes (course updates)
```

### Lesson Display Settings

**Where to configure:**
```
LifterLMS → Settings → Courses
```

**Recommended settings:**

| Setting | Value | Benefit |
|---------|-------|----------|
| **Lesson Progression** | Sequential | Structured learning |
| **Show Lesson Navigation** | Yes | Easy movement |
| **Lesson Comments** | Enabled | Student interaction |
| **Lesson Completion** | Manual | Student control |
| **Auto-Advance** | Optional | Hands-free learning |
| **Video Progression** | Enabled | Ensure viewing |

### Quiz Configuration

**Essential quiz settings:**

```yaml
Quiz Attempts: 3 maximum
Passing Grade: 70%
Show Correct Answers: After completion
Quiz Timer: Course dependent
Question Randomization: Enabled
Result Display: Percentage + Pass/Fail
```

---

## Part 4: Payment & Enrollment

### Payment Gateway Setup

**Stripe Integration** (Built-in)

**Where to configure:**
```
LifterLMS → Settings → Checkout
```

**Settings:**
```yaml
Test Mode: Enable for testing
Stripe Publishable Key: [from Stripe dashboard]
Stripe Secret Key: [from Stripe dashboard]
Currency: USD (or your currency)
Capture Method: Automatic
```

**PayPal Integration** (With addon)

**Benefits:**
- Widely accepted
- Easy setup
- International support
- Buyer protection

**Setup:**
1. Install LifterLMS PayPal addon
2. Get PayPal API credentials
3. Configure payment settings
4. Test payment flow

### Pricing Strategies

**Common pricing models:**

| Model | How It Works | Best For |
|-------|--------------|----------|
| **One-time Purchase** | Pay once, lifetime access | Skill courses |
| **Access Plans** | Multiple pricing options | Flexible access |
| **Membership Plans** | Recurring subscription | Ongoing learning |
| **Payment Plans** | Installment payments | High-value courses |
| **Free Courses** | No payment required | Lead generation |

---

## Part 5: User Roles & Permissions

### Understanding LifterLMS Roles

**Default user roles:**

| Role | Capabilities | Use Case |
|------|--------------|----------|
| **Student** | Take courses, view progress | Course learners |
| **Instructor** | Create courses, manage students | Course creators |
| **Assistant Instructor** | Help with course management | Teaching assistants |
| **LMS Manager** | Manage LMS settings | LMS administrators |

### Configure Instructor Permissions

**Where to set:**
```
LifterLMS → Settings → General → User Roles
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

### Membership Management

**For subscription-based learning:**

```yaml
Membership Levels:
  - Basic: Access to free courses
  - Premium: Access to paid courses
  - VIP: Access to all content + bonuses

Membership Features:
  - Drip content release
  - Exclusive courses
  - Priority support
  - Community access
```

---

## Part 6: Certificates & Achievements

### Certificate Configuration

**Where to set up:**
```
LifterLMS → Certificates
```

**Certificate settings:**

```yaml
Automatic Issuance: Yes
Download Format: PDF
Certificate Design: Custom template
Include Information:
  - Student name
  - Course title
  - Completion date
  - Instructor signature
  - Unique certificate ID
  - QR code verification
```

### Achievement System

**Set up badges and awards:**

1. **Enable achievements:**
   - **LifterLMS** → **Achievements**
   - Create achievement templates
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
Content Dripping: Enable scheduled release
Prerequisites: Require previous completion
Membership Restrictions: Member-only access
Time-based Access: Expire after period
Device Limits: 3 devices per user
IP Restrictions: For corporate training
```

### Video Protection

**For video courses:**

```yaml
Video Hosting: Vimeo Pro or Wistia
DRM Protection: Enable if available
Playback Controls: Limited speed options
Download Prevention: Disable right-click
Watermarks: Add branding
Chapters: Break into sections
```

---

## Part 8: Assessment Configuration

### Quiz Settings Deep Dive

**Advanced quiz options:**

```yaml
Question Types Available:
  - Multiple Choice
  - True/False
  - Picture Choice
  - Fill in the Blank
  - Scale
  - Free Choice

Grading Options:
  - Automatic grading
  - Manual review
  - Weighted scoring
  - Partial credit
  - Negative marking
```

### Assignment Configuration

**If using assignments:**

```yaml
File Upload Types: PDF, DOC, DOCX, TXT, JPG, PNG
Max File Size: 10MB
Submission Deadline: Set per assignment
Late Submissions: Allow with penalty
Instructor Review: Required
Rubric Grading: Enable detailed feedback
Peer Review: Optional student evaluation
```

---

## Part 9: Communication Settings

### Notification System

**Configure student notifications:**

```yaml
Email Notifications:
  - Course enrollment
  - Lesson completion
  - Quiz results
  - Certificate earned
  - Payment confirmations
  - Course announcements

In-App Notifications:
  - New content available
  - Assignment due dates
  - Quiz reminders
  - Achievement unlocked
```

### Discussion Features

**Course interaction:**

```yaml
Lesson Comments: Enable student questions
Course Forums: Create discussion spaces
Private Messaging: Student-instructor communication
Group Discussions: Cohort-based learning
Q&A Sections: Organized question handling
```

---

## Part 10: Analytics & Reporting

### Progress Tracking

**What to track:**

```yaml
Student Progress:
  - Course completion percentage
  - Time spent per lesson
  - Quiz attempts and scores
  - Last activity date
  - Engagement metrics

Course Analytics:
  - Enrollment numbers
  - Completion rates
  - Popular content
  - Drop-off points
  - Revenue tracking
```

### Reporting Options

**Available reports:**
- Student progress reports
- Course performance analytics
- Revenue and sales reports
- Engagement statistics
- Certificate issuance records

**Export formats:**
- CSV files for Excel
- PDF summaries
- Email reports
- Dashboard widgets

---

## Part 11: Mobile Learning Configuration

### Mobile App Integration

**LifterLMS mobile app features:**

```yaml
Offline Content: Download lessons
Push Notifications: Course updates
Progress Sync: Real-time updates
Mobile Payments: In-app purchases
Video Streaming: Optimized playback
```

### Mobile Web Optimization

```yaml
Responsive Design: Enabled
Touch-Friendly: Large buttons
Mobile Navigation: Simplified menus
Video Controls: Touch-optimized
Quick Actions: One-tap operations
```

---

## Part 12: SEO & Marketing Configuration

### Course SEO Settings

**Help courses rank in search:**

```yaml
SEO Plugin: Yoast or RankMath
Course URLs: /courses/course-name/
Meta Descriptions: Compelling summaries
Schema Markup: Course structured data
Sitemap: Include course pages
```

### Social Sharing

```yaml
Share Buttons: Course and lesson pages
Open Graph: Course images and descriptions
Twitter Cards: Course previews
LinkedIn: Professional course sharing
```

---

## Configuration for Different Learning Models

### Corporate Training Setup

```yaml
Access: Private (admin enrollment)
Groups: Department-based
Reporting: Detailed compliance tracking
Certificates: Required for regulations
Branding: Company colors and logo
Integrations: HR systems
```

### Online Academy Setup

```yaml
Access: Mixed (free and paid)
Progression: Structured learning paths
Certificates: Industry-recognized
Community: Student interaction
Mentorship: Instructor support
Career Services: Job placement help
```

### Professional Development

```yaml
Access: Individual purchase
Certificates: CEU credits
Pacing: Self-directed
Networking: Peer connections
Portfolio: Work samples
Continuing Education: Ongoing learning
```

### Hobby Learning Platform

```yaml
Access: Mix of free and affordable
Progression: Flexible pacing
Community: Strong peer support
Creativity: Project sharing
Inspiration: Success showcases
Fun: Gamification elements
```

---

## Quick Settings Reference

### Most Important Setting Locations

```
General: LifterLMS → Settings → General
Courses: LifterLMS → Settings → Courses  
Checkout: LifterLMS → Settings → Checkout
Notifications: LifterLMS → Settings → Notifications
Display: Appearance → Customize → Reign LifterLMS
Pages: LifterLMS → Settings → Pages
```

### Recommended Starter Settings

```yaml
Course Access: Purchase required
Lesson Progression: Sequential
Quiz Passing: 70%
Certificates: Automatic issuance
Reports: Enabled
Mobile: Responsive design
SEO: Optimized
Security: Content protected
```

---

## Testing Your Configuration

### Essential Tests Before Launch

1. **Create test student account**
2. **Purchase/enroll in test course**
3. **Complete lesson progression**
4. **Take quiz and achieve certificate**
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
Image Optimization: Compress course assets
Database: Regular maintenance
Hosting: LMS-optimized servers
Video: External hosting (Vimeo/Wistia)
```

---

## Complete Reign LifterLMS Settings

### Main Settings Location

**Access all Reign LifterLMS settings:**
```
WP Admin → Reign Settings → LifterLMS
```

### License Configuration

#### Add License

**Activate your license:**
```
Reign Settings → License → LifterLMS Addon
```

License activation required for:
- Automatic updates
- Bug fixes
- Security patches
- WordPress compatibility
- Premium support access

#### Upgrade License

**Available upgrades:**
- Single site → 5 sites
- 5 sites → Unlimited
- Annual → Lifetime

### General Settings

#### General Setting Options

**Configure core options:**
```
Reign Settings → LifterLMS → General Settings
```

Key settings:
- Course catalog display
- Student dashboard
- Progress tracking
- Certificate display
- Achievement badges

#### Account Settings

**Configure user accounts:**
```
LifterLMS → Settings → Accounts
```

Options:
- Registration fields
- Login redirect
- Dashboard tabs
- Privacy settings
- Data export

### Course Configuration

#### Global Course Settings

**Set course defaults:**
```
Reign Settings → LifterLMS → Global Course Settings
```

Settings:
- Course progression
- Lesson dripping
- Video autoplay
- Course reviews
- Social sharing

#### Course Archive Page

**Style course listing:**
```
Reign Settings → LifterLMS → Course Archive Page
```

Layout options:
- Grid/List view
- Columns (2, 3, 4)
- Items per page
- Sort options
- Filter display

#### Single Course Page

**Style individual course pages:**
```
Reign Settings → LifterLMS → Single Course Page
```

Customizations:
- Layout style
- Sidebar position
- Syllabus display
- Instructor info
- Reviews section

#### Course Builder

**Advanced course creation:**
```
LifterLMS → Course Builder
```

Features:
- Drag-drop interface
- Section organization
- Lesson ordering
- Quiz placement
- Prerequisite setup

#### How to Add New Course

**Create a course:**
1. Go to LifterLMS → Courses
2. Click "Add New Course"
3. Enter title and description
4. Use Course Builder
5. Add sections and lessons
6. Configure access settings
7. Publish course

#### Reorder Lessons or Sections

**How to reorganize content:**
1. Open Course Builder
2. Drag sections to reorder
3. Drag lessons within sections
4. Use arrows for fine control
5. Save changes

### Related Courses

#### How Admin Can Set Related Courses

**Configure course relationships:**
```
Reign Settings → LifterLMS → Related Courses
```

Options:
- Auto-suggest by category
- Manual selection
- Based on tags
- By instructor
- Skill progression

### Membership Configuration

#### Membership Settings

**Configure memberships:**
```
LifterLMS → Settings → Memberships
```

Settings:
- Membership levels
- Access restrictions
- Payment plans
- Trial periods
- Expiration rules

#### Style Membership Listing Page

**Customize membership display:**
```
Reign Settings → LifterLMS → Membership Listing
```

Options:
- Pricing tables
- Feature comparison
- Highlight popular
- Custom badges
- Call-to-action buttons

#### Style Single Membership Page

**Individual membership pages:**
```
Reign Settings → LifterLMS → Single Membership
```

Customizations:
- Layout template
- Course list display
- Pricing display
- Benefits section
- FAQs

### Checkout & Payment

#### Checkout Page Settings

**Configure checkout:**
```
LifterLMS → Settings → Checkout
```

Options:
- Field requirements
- Payment gateways
- Coupon codes
- Terms acceptance
- Order confirmation

### Engagement Features

#### Engagements Settings

**Set up automations:**
```
LifterLMS → Settings → Engagements
```

Engagement types:
- Certificates
- Achievements
- Email triggers
- Course tracks
- Automation rules

#### Create a Certificate

**How to create certificates:**
1. Go to LifterLMS → Certificates
2. Click "Add New"
3. Design certificate template
4. Add merge codes
5. Set award conditions
6. Assign to courses

#### Create an Achievement

**How to create achievements:**
1. Go to LifterLMS → Achievements
2. Click "Add New"
3. Design badge
4. Set criteria
5. Configure points
6. Assign to activities

### Quiz Configuration

#### Quiz Review System

**Access quiz reviews:**
```
LifterLMS → Reporting → Quizzes
```

Features:
- Student attempts
- Answer review
- Grade adjustments
- Feedback provision
- Statistics

### Notifications

#### Notification Settings

**Configure notifications:**
```
LifterLMS → Settings → Notifications
```

Notification types:
- Enrollment confirmations
- Course completions
- Quiz results
- Certificate awards
- Payment receipts

### Integration Settings

#### Integration Setting

**Third-party integrations:**
```
LifterLMS → Settings → Integrations
```

Available integrations:
- Payment gateways
- Email services
- CRM systems
- Analytics tools
- Marketing platforms

#### LifterLMS BuddyPress Integration

**Enable BP features:**
```
Reign Settings → LifterLMS → BuddyPress Integration
```

Features:
- Course tab in profiles
- Achievement display
- Social learning
- Group courses
- Activity stream

### Widgets & Shortcodes

#### LifterLMS Extra Widgets

**How to set widgets:**
```
Appearance → Widgets → LifterLMS Sidebar
```

Available widgets:
- Course progress
- Course syllabus
- Student dashboard
- Course instructors
- Pricing table

#### Reign LifterLMS Shortcodes

**Available shortcodes:**

```
[reign_lifterlms_courses
    number="6"
    columns="3"
    category=""]

[reign_lifterlms_memberships
    number="3"
    columns="3"]

[reign_lifterlms_my_courses]

[reign_lifterlms_instructors]
```

### Customizer Settings

#### How Customizer Settings Work

**For courses, lessons, and topics:**
```
Appearance → Customize → Reign LifterLMS
```

Customizable elements:
- Colors and fonts
- Layout options
- Progress bar styles
- Button designs
- Mobile settings

### Template Overrides

#### Which Template Files are Overridden

**Templates modified by addon:**
- `course-list.php`
- `single-course.php`
- `lesson.php`
- `membership-list.php`
- `checkout.php`
- `myaccount.php`

**Override location:**
```
/themes/reign-child/lifterlms/
```

### System Requirements

**Minimum requirements:**
- WordPress 5.0+
- Reign Theme (latest)
- LifterLMS 4.0+
- PHP 7.2+
- Memory: 256MB

**Recommended:**
- PHP 8.0+
- Memory: 512MB
- MySQL 5.7+
- SSL Certificate

### Additional Features

#### Plugin Installation

**How to install:**
1. Upload plugin ZIP
2. Activate plugin
3. Enter license key
4. Configure settings
5. Import sample courses (optional)

#### Filters for Learnmate LifterLMS

**Available filters:**
```php
// Customize course grid
apply_filters('learnmate_course_grid_columns', 3);

// Modify course meta
apply_filters('learnmate_course_meta_display', $meta);

// Custom enrollment text
apply_filters('learnmate_enrollment_text', $text);
```

## Advanced Configuration

### Custom Fields

**Add extra information:**
- Course prerequisites
- Learning outcomes
- Industry certifications
- Skill levels gained
- Time commitments

### Automation Rules

**Set up automatic actions:**
- Enroll in follow-up courses
- Send congratulations emails
- Award bonus content
- Trigger marketing campaigns
- Update user profiles

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