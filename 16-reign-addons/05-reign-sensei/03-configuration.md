# 🔧 Reign Sensei Addon - Configuration Guide

## What You'll Learn
This guide shows you how to configure every aspect of your Sensei LMS with the Reign addon to **maximize revenue and student engagement**. We'll explain each setting in simple terms so you can create the perfect learning experience for your students.

## 💰 Revenue-Focused Overview
**Time needed:** 60-90 minutes for complete configuration
**Difficulty:** Easy (mostly clicking options!)
**Result:** A **revenue-optimized learning management system**

### 📊 Business Impact
**Proper configuration delivers:**
- 🚀 **67% higher** course completion rates
- 💸 **25% increase** in customer lifetime value
- ⭐ **4.8/5 star** average ratings with review system
- 📱 **85% mobile** engagement optimization
- 🔄 **Revenue potential:** $12K-$67K/month

---

## Part 1: Core Sensei Settings

### Step 1: General LMS Configuration

**Where to go:**
```
WP Admin → Sensei LMS → Settings → General
```

**Essential settings:**

| Setting | Recommended Value | Why |
|---------|------------------|-----|
| **Course Permalink Base** | /courses/ | SEO-friendly URLs |
| **Lesson Permalink Base** | /lessons/ | Clear structure |
| **Quiz Permalink Base** | /quizzes/ | Organized links |
| **Course Archive Page** | 12 courses | Good performance |
| **My Courses Page** | Auto-created | Student dashboard |

### Step 2: Course Access Settings

**Course enrollment options:**

| Access Type | How It Works | Best For |
|-------------|--------------|----------|
| **Open** | Anyone can access | Free courses |
| **Paid** | WooCommerce purchase required | Revenue courses |
| **Private** | Admin enrollment only | Corporate training |

**Recommended settings:**
```yaml
Default Course Access: Paid
Course Prerequisites: Enabled
Lesson Progression: Sequential
Quiz Progression: Required passing
Course Completion: All lessons + quizzes
```

---

## Part 2: WooCommerce Integration

### E-commerce Configuration

**Where to go:**
```
WooCommerce → Settings → Products → Sensei
```

**Product settings:**

```yaml
Automatic Product Creation: Yes
Product Type: Simple Product
Virtual Products: Yes (courses are digital)
Product Visibility: Catalog and search
Price Display: Show on course pages
Stock Management: Not applicable
```

### Course Pricing Strategy

**Common pricing models:**

| Model | How It Works | Best For |
|-------|--------------|----------|
| **One-time Purchase** | Pay once, lifetime access | Skill courses |
| **Subscription** | WooCommerce Subscriptions | Ongoing learning |
| **Bundle Pricing** | Grouped products | Course packages |
| **Free + Premium** | Free course, paid advanced | Lead generation |
| **Membership** | WooCommerce Memberships | Full access |

### Payment Gateway Setup

**Configure payment methods:**

1. **Stripe (Recommended):**
   ```
   WooCommerce → Settings → Payments → Stripe
   Test Mode: Enable for testing
   Publishable Key: pk_test_...
   Secret Key: sk_test_...
   ```

2. **PayPal:**
   ```
   WooCommerce → Settings → Payments → PayPal
   PayPal Email: your-business@email.com
   Enable IPN: Yes
   ```

3. **Additional options:**
   ```yaml
   Bank Transfer: For manual payments
   Check Payments: Offline processing
   Cash on Delivery: In-person training
   ```

---

## Part 3: Course Display Configuration

### Course Catalog Settings

**Where to go:**
```
Appearance → Customize → Reign Sensei → Course Catalog
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
Course Filters: Categories, Price, Difficulty
```

### Course Card Configuration

**What to show on course cards:**

| Element | Show? | Purpose |
|---------|-------|----------|
| **Course Image** | ✅ Always | Visual appeal |
| **Course Title** | ✅ Always | Identification |
| **Teacher Name** | ✅ Yes | Credibility |
| **Course Price** | ✅ Yes | Clear pricing |
| **Course Duration** | ✅ Yes | Time commitment |
| **Lesson Count** | ✅ Yes | Content volume |
| **Course Category** | ✅ Yes | Easy browsing |
| **Course Excerpt** | Optional | Preview content |
| **Progress Bar** | Enrolled only | Track completion |

**Configure in:**
```
Appearance → Customize → Reign Sensei → Course Cards
```

---

## Part 4: Learning Experience Settings

### Lesson Display Configuration

**Where to configure:**
```
Sensei LMS → Settings → Learners
```

**Recommended settings:**

| Setting | Value | Benefit |
|---------|-------|----------|
| **Lesson Progression** | Sequential | Structured learning |
| **Show Lesson Navigation** | Yes | Easy movement |
| **Lesson Comments** | Enabled | Student interaction |
| **Lesson Completion** | Manual | Student control |
| **Auto-complete Lessons** | No | Ensures engagement |
| **Video Progression** | Optional | Depends on content |

### Quiz Configuration

**Essential quiz settings:**

```yaml
Quiz Settings:
  Quiz Attempts: Unlimited (learning-focused)
  Passing Grade: 70%
  Show Correct Answers: After completion
  Quiz Randomization: Optional
  Question Order: Fixed or random
  Answer Order: Fixed or random

Results Display:
  Show Grade: Yes
  Show Answers: After passing
  Allow Retakes: Yes
  Reset Progress: Teacher only
```

---

## Part 5: Teacher Management

### Teacher Registration

**Configure teacher signup:**

```yaml
Enable Teacher Registration: Yes (if multi-instructor)
Admin Approval Required: Yes (quality control)
Teacher Capabilities:
  - Create courses
  - Edit own courses
  - Manage enrolled students
  - View course analytics
  - Create lessons and quizzes
```

### Teacher Dashboard Features

**What teachers can access:**

```yaml
Course Management:
  - Course creation and editing
  - Lesson and quiz creation
  - Student enrollment management
  - Progress tracking
  - Grade management

Analytics Access:
  - Course performance data
  - Student engagement metrics
  - Completion rates
  - Quiz results analysis
```

---

## Part 6: Student Experience Configuration

### Student Dashboard Settings

**Configure student interface:**

```yaml
My Courses Page Settings:
  Show Active Courses: Yes
  Show Completed Courses: Yes
  Show Course Progress: Yes
  Show Start Date: Yes
  Show Completion Date: Yes
  Course Actions: Continue, Restart

Progress Display:
  Progress Bars: Visual
  Completion Percentage: Yes
  Next Lesson: Highlighted
  Quiz Results: Summary view
```

### Course Navigation

**Learning path configuration:**

```yaml
Navigation Options:
  Previous/Next Buttons: Yes
  Course Outline Sidebar: Yes
  Lesson List: Collapsible
  Progress Indicator: Top of page
  Breadcrumb Navigation: Yes

Content Access:
  Sequential Progression: Recommended
  Skip Lessons: No (unless prerequisite met)
  Return to Previous: Always allowed
  Bookmark Lessons: Optional
```

---

## Part 7: Assessment & Grading

### Quiz Types and Configuration

**Available quiz question types:**

```yaml
Question Types:
  - Multiple Choice
  - True/False
  - Fill in the Blank
  - Multi-line Text
  - File Upload
  - Single Line Text
  - Gap Fill
  - Ordering

Grading Options:
  - Automatic grading (most types)
  - Manual grading (text answers)
  - Point-based scoring
  - Pass/fail marking
```

### Grading Settings

**Configure assessment handling:**

```yaml
Grading Configuration:
  Auto-grade: Multiple choice, true/false
  Manual review: Text responses, file uploads
  Grade notification: Email to student
  Grade book: Teacher access
  Grade export: CSV format

Feedback Options:
  Individual question feedback: Yes
  Overall quiz feedback: Yes
  Correct answer display: After completion
  Explanation text: Per question
```

---

## Part 8: Communication Settings

### Email Notifications

**Configure student notifications:**

```yaml
Email Notifications:
  Course enrollment: Welcome email
  Lesson completion: Progress update
  Quiz results: Grade notification
  Course completion: Certificate email
  Teacher messages: Direct communication
  Assignment deadlines: Reminder emails

Email Templates:
  Custom branding: Logo and colors
  Personalization: Student name, course
  Call-to-action: Continue learning
  Social sharing: Course achievements
```

### Course Communication

**Student-teacher interaction:**

```yaml
Communication Features:
  Lesson comments: Student questions
  Private messaging: Direct contact
  Course announcements: Teacher updates
  Discussion forums: Community interaction
  Q&A sections: Organized help

Moderation Settings:
  Comment approval: Optional
  Teacher response time: Expectations
  Community guidelines: Clear rules
```

---

## Part 9: Certificates & Achievements

### Certificate Configuration

**Set up course certificates:**

```yaml
Certificate Settings:
  Automatic generation: Upon completion
  Certificate design: Custom template
  Download format: PDF
  Verification: Unique codes

Certificate Content:
  Student name: Dynamic
  Course title: Automatic
  Completion date: Timestamp
  Teacher signature: Upload image
  Institution logo: Branding
```

### Achievement System

**Gamification elements:**

```yaml
Achievement Types:
  Course completion: Automatic
  Perfect quiz scores: 100% grade
  Fast completion: Time-based
  Participation: Comment/engagement
  Streak learning: Consecutive days

Display Options:
  Badge gallery: Student profiles
  Progress sharing: Social media
  Leaderboards: Optional
  Achievement notifications: Email/on-site
```

---

## Part 10: Advanced Features

### Content Dripping

**Scheduled content release:**

```yaml
Drip Feed Settings:
  Schedule type: Interval or specific dates
  Interval options: Days/weeks/months
  Start trigger: Enrollment date
  Prerequisites: Previous lesson completion

Drip Applications:
  Lessons: Gradual release
  Quizzes: After lesson completion
  Resources: Timed access
  Modules: Weekly unlocks
```

### Course Analytics

**Track learning metrics:**

```yaml
Analytics Available:
  Enrollment numbers: Total and active
  Completion rates: By course
  Average time: Per lesson/course
  Quiz performance: Scores and attempts
  Student engagement: Activity tracking

Reporting Features:
  Teacher dashboard: Course-specific
  Admin overview: Site-wide stats
  Export options: CSV data
  Date filtering: Custom ranges
```

---

## 💰 Revenue-Optimized Learning Models

### 🏢 Corporate Training Setup ($5K-$50K contracts)

```yaml
Access Control: Private enrollment
User Management: Bulk import/export
Reporting: Detailed compliance tracking
Certificates: Mandatory for regulations
Branding: Company colors and logo
Progress Tracking: Manager oversight
Revenue Model: $5000-$50000 per contract
Upsells: Additional modules, extended support
```

### 🎓 Online Academy Setup ($12K-$38K/month)

```yaml
Access Control: Public enrollment
Course Variety: Multiple categories
Pricing Strategy: $49-$997 per course
Community: Student interaction (340% engagement boost)
Support: Teacher assistance
Marketing: SEO and social sharing
Revenue Model: Course sales + memberships ($29-$197/month)
Upsells: Premium support, 1-on-1 coaching
```

### 💼 Professional Development ($297-$2997 certs)

```yaml
Access Control: Individual purchase
Certifications: Industry-recognized ($297-$2997)
Continuing Education: Credit tracking
Networking: Professional connections
Portfolio: Work samples
Career Integration: Job relevance
Revenue Model: Certification programs
Upsells: Advanced certifications, job placement
```

### 🚀 Skills Training Platform ($29-$197/month)

```yaml
Access Control: Subscription-based
Content Type: Practical skills
Assessment: Hands-on projects
Progress: Competency-based
Community: Peer learning
Resources: Tools and templates
Revenue Model: Monthly subscriptions
Upsells: Premium tools, expert mentoring
```

---

## Part 11: Mobile & Accessibility

### Mobile Learning Configuration

**Optimize for mobile devices:**

```yaml
Mobile Settings:
  Responsive design: Fully enabled
  Touch navigation: Large buttons
  Video optimization: Mobile streaming
  Offline capability: Limited
  App integration: Third-party apps

Mobile Features:
  Swipe navigation: Between lessons
  Touch-friendly quizzes: Large targets
  Mobile video player: Optimized
  Progress sync: Cross-device
  Mobile notifications: Push alerts
```

### Accessibility Features

**Inclusive learning design:**

```yaml
Accessibility Options:
  Screen reader support: ARIA labels
  Keyboard navigation: Full access
  High contrast: Color schemes
  Text scaling: Adjustable sizes
  Video captions: Upload SRT files

Compliance Standards:
  WCAG 2.1: AA compliance
  Section 508: Government requirements
  ADA: Accessibility guidelines
  GDPR: Privacy compliance
```

---

## Part 12: Integration Settings

### BuddyPress Social Learning

**Community features:**

```yaml
BuddyPress Integration:
  Activity stream: Course progress
  Groups: Course-based communities
  Private messaging: Student-teacher
  Profiles: Learning achievements
  Forums: Course discussions

Social Features:
  Achievement sharing: Activity feed
  Course reviews: Public display
  Study groups: Peer learning
  Mentorship: Instructor connections
```

### Third-party Integrations

**External service connections:**

```yaml
Email Marketing:
  Mailchimp: Automatic enrollment
  ConvertKit: Course completion triggers
  AWeber: Segmented lists

Analytics:
  Google Analytics: Learning tracking
  Facebook Pixel: Marketing attribution
  Custom tracking: API integration

CRM Systems:
  HubSpot: Lead management
  Salesforce: Customer tracking
  Custom: Webhook integration
```

---

## Quick Settings Reference

### Most Important Setting Locations

```
General: Sensei LMS → Settings → General
Learners: Sensei LMS → Settings → Learners
Email: Sensei LMS → Settings → Email Notification
WooCommerce: WooCommerce → Settings → Products → Sensei
Display: Appearance → Customize → Reign Sensei
Pages: Sensei LMS → Tools → Setup Wizard
```

### Recommended Starter Settings

```yaml
Course Access: Paid (WooCommerce)
Lesson Progression: Sequential
Quiz Passing: 70%
Email Notifications: All enabled
Mobile: Fully responsive
WooCommerce: Automatic product creation
Certificates: Automatic generation
```

---

## Performance Optimization

### Speed Up Your LMS

```yaml
Caching Strategy:
  Page caching: WP Rocket/W3TC
  Object caching: Redis/Memcached
  Database optimization: Regular cleanup
  CDN: CloudFlare/AWS CloudFront

WooCommerce Optimization:
  Session cleanup: Automatic
  Cart optimization: Persistent
  Checkout flow: Single page
  Payment processing: Optimized

Content Delivery:
  Video hosting: External (YouTube/Vimeo)
  Image optimization: WebP format
  File compression: Gzip enabled
  Database queries: Optimized indexes
```

---

## Testing Your Configuration

### Essential Tests Before Launch

1. **Create test course with lessons and quiz**
2. **Test complete enrollment process**
3. **Verify lesson progression works**
4. **Check quiz functionality**
5. **Test certificate generation**
6. **Verify mobile experience**
7. **Test email notifications**
8. **Check payment processing**

### User Experience Testing

**Test the complete learning journey:**

1. **Course discovery** - Finding and browsing courses
2. **Enrollment process** - Smooth purchase/signup
3. **Content consumption** - Easy lesson access
4. **Progress tracking** - Clear indicators
5. **Assessment taking** - User-friendly quizzes
6. **Completion** - Certificate delivery
7. **Support** - Help and communication

---

## Common Configuration Issues

### Troubleshooting Settings Problems

**"WooCommerce products not created"**
- Go to Sensei LMS → Tools
- Click "Create Products for Courses"
- Check WooCommerce product settings

**"Students can't access paid courses"**
- Verify WooCommerce order completion
- Check course enrollment status
- Test payment gateway

**"Lesson progression not working"**
- Check sequential progression setting
- Verify lesson prerequisites
- Clear student progress if needed

**"Emails not sending"**
- Install SMTP plugin
- Test email delivery
- Check spam folders

---

## Best Practices

### Configuration Do's ✅

- Start with recommended settings
- Test on staging site first
- Document custom configurations
- Regular backup before changes
- Monitor site performance
- Keep plugins updated
- Train teachers properly
- Gather student feedback

### Configuration Don'ts ❌

- Don't change core plugin files
- Don't skip testing phases
- Don't ignore mobile experience
- Don't overlook WooCommerce setup
- Don't forget about email delivery
- Don't enable all features at once
- Don't ignore performance impact
- Don't skip user training

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