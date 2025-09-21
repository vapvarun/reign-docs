# Reign TutorLMS Addon - Configuration Guide

## What You'll Learn
This guide shows you how to configure every aspect of your TutorLMS with the Reign addon. We'll explain each setting in simple terms so you can create the perfect learning experience for your students.

## Quick Overview
**Time needed:** 60-90 minutes for complete configuration
**Difficulty:** Easy (mostly clicking options!)
**Result:** A fully configured learning management system

---

## Part 1: Core TutorLMS Settings

### Step 1: General LMS Configuration

**Where to go:**
```
WP Admin → TutorLMS → Settings → General
```

**Essential settings:**

| Setting | Recommended Value | Why |
|---------|------------------|-----|
| **Course Permalink** | /courses/ | SEO-friendly URLs |
| **Lesson Permalink** | /lessons/ | Clear structure |
| **Course Archive Page** | 12 courses | Good performance |
| **Pagination** | Enabled | Better navigation |
| **Load TutorLMS CSS** | Enabled | Proper styling |
| **Load TutorLMS JS** | Enabled | Interactive features |

### Step 2: Course Access Settings

**Course enrollment options:**

| Access Type | How It Works | Best For |
|-------------|--------------|----------|
| **Free** | Anyone can access | Lead generation |
| **Paid** | Payment required | Revenue courses |
| **Subscription** | Recurring access | Ongoing programs |
| **Private** | Admin enrollment only | Corporate training |

**Recommended settings:**
```yaml
Default Course Access: Paid
Course Prerequisites: Enabled
Lesson Progression: Sequential
Quiz Progression: Required passing
Course Review: After completion
```

---

## Part 2: Course Display Configuration

### Course Catalog Settings

**Where to go:**
```
Appearance → Customize → Reign TutorLMS → Course Catalog
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
  - Student count
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
| **Category Badge** | ✅ Yes | Easy browsing |

**Configure in:**
```
Appearance → Customize → Reign TutorLMS → Course Cards
```

---

## Part 3: Student Experience Settings

### Student Dashboard Configuration

**Dashboard sections to enable:**

```yaml
My Courses: Yes (enrolled courses)
My Profile: Yes (student information)
My Quiz Attempts: Yes (quiz history)
Question & Answer: Yes (course Q&A)
My Assignments: Yes (submitted work)
Purchase History: Yes (if monetization enabled)
Wishlist: Yes (saved courses)
Reviews: Yes (course reviews)
Zoom Meetings: Yes (if using Zoom integration)
```

### Lesson Display Settings

**Where to configure:**
```
TutorLMS → Settings → Course
```

**Recommended settings:**

| Setting | Value | Benefit |
|---------|-------|----------|
| **Lesson Progression** | Sequential | Structured learning |
| **Show Lesson Navigation** | Yes | Easy movement |
| **Lesson Comments** | Enabled | Student interaction |
| **Lesson Completion** | Automatic | Better tracking |
| **Video Progression** | Enabled | Ensure viewing |
| **Auto Load Next Content** | Optional | Seamless flow |

### Quiz Configuration

**Essential quiz settings:**

```yaml
Quiz Attempts: 10 maximum (generous for learning)
Passing Grade: 80%
Show Correct Answers: After completion
Quiz Timer: Course dependent
Question Randomization: Enabled
Hide Quiz Result: No (transparency)
Feedback Mode: Default
```

---

## Part 4: Instructor Management

### Instructor Registration

**Configure instructor signup:**

```yaml
Enable Instructor Registration: Yes
Admin Approval Required: Yes (quality control)
Instructor Commission: 70% (competitive rate)
Minimum Withdrawal Amount: $50
Instructor Profile Completion: Required
```

### Instructor Capabilities

**What instructors can do:**

```yaml
Course Management:
  - Create unlimited courses
  - Edit own courses
  - Manage course content
  - View student progress
  - Issue certificates

Student Interaction:
  - Respond to Q&A
  - Grade assignments
  - Send announcements
  - View course reviews

Analytics Access:
  - Course performance data
  - Student engagement metrics
  - Revenue tracking
  - Withdrawal history
```

### Instructor Dashboard Features

**Enable these sections:**

```yaml
Dashboard Overview: Yes
My Courses: Yes
Create Course: Yes
Announcements: Yes
Quiz Attempts: Yes
Assignments: Yes
Question & Answer: Yes
Analytics: Yes
Earnings: Yes (if monetization enabled)
Withdrawals: Yes (if monetization enabled)
Settings: Yes
```

---

## Part 5: Monetization Configuration

### Choose Monetization Method

**Available options:**

| Method | Pros | Cons | Best For |
|--------|------|------|----------|
| **TutorLMS Built-in** | Simple setup | Basic features | Small operations |
| **WooCommerce** | Advanced features | More complex | Professional sites |
| **Easy Digital Downloads** | Digital focus | Less e-commerce | Digital products only |

### WooCommerce Integration (Recommended)

**Setup steps:**

1. **Install WooCommerce:**
   ```
   Plugins → Add New → WooCommerce
   Install and activate
   ```

2. **Enable in TutorLMS:**
   ```
   TutorLMS → Settings → Monetization
   Select "WooCommerce"
   Save Changes
   ```

3. **Configure WooCommerce:**
   ```yaml
   Currency: Your local currency
   Payment Gateways: Stripe, PayPal
   Tax Settings: As per your location
   Shipping: Not needed for courses
   ```

### Pricing Strategies

**Common pricing models:**

| Model | How It Works | Best For |
|-------|--------------|----------|
| **One-time Purchase** | Pay once, lifetime access | Skill courses |
| **Subscription** | Recurring payment | Ongoing learning |
| **Bundle Pricing** | Multiple courses together | Course packages |
| **Tiered Pricing** | Different access levels | Flexible options |
| **Free + Premium** | Free basic, paid advanced | Lead generation |

---

## Part 6: Assessment & Grading

### Quiz Settings Deep Dive

**Advanced quiz options:**

```yaml
Question Types Available:
  - Multiple Choice
  - True/False
  - Fill in the Blanks
  - Short Answer
  - Matching
  - Image Matching
  - Image Answering
  - Ordering

Grading Options:
  - Automatic grading (most types)
  - Manual grading (short answer)
  - Weighted scoring
  - Partial credit
  - Time-based scoring
```

### Assignment Configuration

**Assignment settings:**

```yaml
File Upload Types: PDF, DOC, DOCX, TXT, JPG, PNG
Max File Size: 10MB
Submission Deadline: Set per assignment
Late Submissions: Allow with notification
Instructor Review: Required
Point System: Numeric or letter grades
Feedback: Text comments + file attachments
```

### Certificate Management

**Certificate settings:**

```yaml
Certificate Generation: Automatic
Template Design: Customizable
Include Information:
  - Student name
  - Course title
  - Completion date
  - Instructor signature
  - Unique certificate ID
  - QR code (with pro addon)
```

---

## Part 7: Communication Settings

### Notification System

**Configure student notifications:**

```yaml
Email Notifications:
  - Course enrollment
  - Lesson completion
  - Quiz results
  - Assignment grades
  - Certificate earned
  - Course announcements
  - Q&A responses
  - Reminder emails

Frontend Notifications:
  - New announcements
  - Assignment deadlines
  - Quiz availability
  - Achievement unlocked
```

### Q&A System

**Course interaction:**

```yaml
Enable Q&A: Yes
Who Can Ask: Enrolled students only
Who Can Answer: Instructors + students (optional)
Email Notifications: Yes
Anonymous Questions: No (encourages engagement)
Upvoting: Yes (highlight best questions)
```

### Announcement System

**Course updates:**

```yaml
Instructor Announcements: Enabled
Email Notifications: Yes
Frontend Display: Course dashboard
Student Response: Comments allowed
Announcement Archive: Keep all
```

---

## Part 8: Content Protection

### Lesson Protection Settings

**Prevent content theft:**

```yaml
Course Content Access: After enrollment only
Video Protection: Right-click disabled
Content Dripping: Schedule release dates
Prerequisites: Require previous completion
Device Limits: 3 devices per user (with addon)
IP Restrictions: For corporate training
```

### Video Protection

**For video courses:**

```yaml
Video Hosting: YouTube, Vimeo, Self-hosted
Autoplay: Disabled (user choice)
Download Prevention: Enabled
Playback Speed: Allow 0.5x to 2x
Video Progression: Track watch time
Video Resume: Continue from last position
```

---

## Part 9: Mobile & Responsive Settings

### Mobile Learning Configuration

**Optimize for mobile:**

```yaml
Responsive Design: Fully enabled
Touch-Friendly Controls: Large buttons
Mobile Navigation: Simplified
Video Player: Mobile-optimized
Quiz Interface: Touch-friendly
Progress Tracking: Visual indicators
Offline Capabilities: With PWA addon
```

### Mobile-Specific Features

```yaml
Mobile App Integration: Available
Push Notifications: Course updates
Offline Content: Download lessons
Responsive Images: Auto-resize
Mobile Video: Optimized streaming
Touch Gestures: Swipe navigation
```

---

## Part 10: Social Learning Features

### BuddyPress Integration

**Community features:**

```yaml
Activity Feed Integration: Course completions
Profile Integration: Show courses taken
Group Integration: Study groups
Private Messaging: Student-instructor
Social Sharing: Course achievements
Leaderboards: Course rankings (with addon)
```

### Social Sharing

**Enable sharing options:**

```yaml
Share Courses: Facebook, Twitter, LinkedIn
Share Achievements: Social media
Course Reviews: Public display
Student Profiles: Course showcase
Progress Sharing: Optional
```

---

## Part 11: Analytics & Reporting

### Course Analytics

**Track important metrics:**

```yaml
Course Performance:
  - Enrollment numbers
  - Completion rates
  - Average time spent
  - Quiz performance
  - Student engagement
  - Revenue generated

Student Analytics:
  - Individual progress
  - Time spent learning
  - Quiz attempts and scores
  - Assignment submissions
  - Course completion dates
```

### Reporting Options

**Available reports:**

```yaml
Instructor Reports:
  - Course performance
  - Student progress
  - Revenue tracking
  - Quiz results
  - Assignment grades

Admin Reports:
  - Site-wide analytics
  - Instructor performance
  - Popular courses
  - Revenue summaries
  - Student engagement
```

---

## Part 12: Advanced Features

### Zoom Integration

**Live classes setup:**

```yaml
Zoom API: Connect your account
Meeting Scheduling: Integrated calendar
Automatic Recording: Save sessions
Meeting Links: Auto-generated
Attendance Tracking: Automatic
Meeting Replay: Available to students
```

### Multi-Instructor Courses

**Collaborative teaching:**

```yaml
Multiple Instructors: Per course
Revenue Sharing: Automatic split
Content Permissions: Shared editing
Student Management: Shared access
Communication: Instructor coordination
```

### Prerequisite System

**Learning paths:**

```yaml
Course Prerequisites: Require previous courses
Lesson Prerequisites: Sequential learning
Quiz Prerequisites: Pass to continue
Assignment Prerequisites: Submit to advance
Skill-based Prerequisites: Competency levels
```

---

## Configuration for Different Learning Models

### Online Academy Setup

```yaml
Access: Mixed (free intro, paid advanced)
Progression: Structured learning paths
Certificates: Industry-recognized
Community: Strong student interaction
Support: Instructor mentorship
Career Services: Job placement assistance
```

### Corporate Training Setup

```yaml
Access: Private (admin enrollment)
Groups: Department-based learning
Reporting: Detailed compliance tracking
Certificates: Required for regulations
Branding: Company colors and logo
Integrations: HR systems
```

### Professional Development

```yaml
Access: Individual purchase
Certificates: CEU credits
Pacing: Self-directed learning
Networking: Peer connections
Portfolio: Work sample submissions
Continuing Education: Ongoing programs
```

### Creative Skills Platform

```yaml
Access: Project-based pricing
Progression: Portfolio building
Community: Peer feedback system
Showcases: Student work galleries
Mentorship: One-on-one guidance
Challenges: Creative competitions
```

---

## Quick Settings Reference

### Most Important Setting Locations

```
General: TutorLMS → Settings → General
Course: TutorLMS → Settings → Course
Instructor: TutorLMS → Settings → Instructor
Monetization: TutorLMS → Settings → Monetization
Email: TutorLMS → Settings → Email Notification
Display: Appearance → Customize → Reign TutorLMS
Tools: TutorLMS → Tools
```

### Recommended Starter Settings

```yaml
Course Access: Paid (with free trial)
Lesson Progression: Sequential
Quiz Passing: 80%
Certificates: Automatic issuance
Instructor Registration: Admin approval
Mobile: Fully responsive
SEO: Optimized permalinks
Security: Content protected
```

---

## Performance Optimization

### Speed Up Your LMS

```yaml
Caching Strategy:
  - Page caching enabled
  - Exclude user dashboards
  - Cache course catalogs
  - Optimize database queries

Image Optimization:
  - Compress course images
  - Use WebP format
  - Lazy load content
  - CDN for media files

Database Management:
  - Regular cleanup
  - Optimize tables
  - Remove spam data
  - Archive old records
```

### Content Delivery

```yaml
Video Hosting: External (YouTube, Vimeo)
Image CDN: Cloudflare or similar
File Downloads: Optimized delivery
Database Queries: Cached results
API Calls: Rate limited and cached
```

---

## Testing Your Configuration

### Essential Tests Before Launch

1. **Create test student account**
2. **Purchase/enroll in test course**
3. **Complete lesson progression**
4. **Take quiz and achieve certificate**
5. **Test instructor features**
6. **Check mobile experience**
7. **Verify email notifications**
8. **Test payment processing**

### User Experience Testing

**Test the complete learning journey:**

1. **Course discovery** - Finding relevant courses
2. **Enrollment process** - Smooth signup/purchase
3. **Content consumption** - Easy lesson navigation
4. **Progress tracking** - Clear indicators
5. **Assessment taking** - User-friendly quizzes
6. **Completion** - Satisfying conclusion
7. **Community interaction** - Q&A and discussions

---

## Common Configuration Issues

### Troubleshooting Settings Problems

**"Courses not showing properly"**
- Clear all caches
- Check permalink settings
- Verify course publication status
- Test with default theme

**"Students can't enroll"**
- Check enrollment settings
- Verify payment gateway
- Test user registration
- Review course access settings

**"Instructor dashboard broken"**
- Verify user role assignments
- Check instructor capabilities
- Clear browser cache
- Test with different browsers

---

## Best Practices

### Configuration Do's ✅

- Start with recommended settings
- Test changes on staging site
- Document custom configurations
- Regular backup before changes
- Monitor site performance
- Keep plugins updated
- Train instructors properly
- Gather student feedback

### Configuration Don'ts ❌

- Don't change core plugin files
- Don't skip testing phases
- Don't ignore mobile experience
- Don't overlook security settings
- Don't forget about backups
- Don't enable all features at once
- Don't ignore performance impact
- Don't forget instructor training

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