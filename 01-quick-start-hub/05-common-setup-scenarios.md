# Common Setup Scenarios - Real-World Configurations

## Choose Your Path

This guide provides specific setup instructions for the most common types of websites built with Reign. Find your scenario and follow the tailored setup guide.

## Scenario 1: Social Community Network

### What You're Building
A Facebook-style community where members connect, share updates, join groups, and engage in discussions.

### Examples
- Hobby communities (photography, gaming, fitness)
- Professional networks (developers, designers)
- Local community platforms
- Alumni networks
- Fan communities

### Essential Setup Steps

#### Step 1: Install Core Plugins
```
Required:
✅ BuddyPress - Community features
✅ bbPress - Forum discussions
✅ RTMedia or MediaPress - Photo/video sharing

Optional:
○ BuddyPress Moderation - Content control
○ User Verification - Trusted members
○ Who's Online - Active members display
```

#### Step 2: Configure BuddyPress

**Components to Enable:**
- ✅ Extended Profiles (detailed member info)
- ✅ Activity Streams (social feed)
- ✅ Notifications (engagement alerts)
- ✅ Friend Connections (social network)
- ✅ Private Messages (direct communication)
- ✅ Groups (community spaces)

**Registration Settings:**
```
Settings → BuddyPress → Options
- ✅ Anyone can register
- ✅ Enable profile syncing
- ✅ Allow avatar uploads
- ✅ Allow cover images
```

#### Step 3: Design Configuration

**Customizer Settings:**
```
Header Style: Style 2 (Centered) - Clean social look
Layout: Wide - Maximum content space
Primary Color: Your brand color
Activity Layout: Masonry - Modern feed style
Member Cards: Grid view - Visual directory
```

**Widget Setup:**
```
Sidebar Widgets:
1. Who's Online
2. Recently Active Members
3. Popular Groups
4. Latest Activities

Footer Widgets:
1. About Community
2. Quick Links
3. Popular Topics
4. Newsletter Signup
```

#### Step 4: Create Essential Pages

**Auto-created by BuddyPress:**
- Members Directory
- Groups Directory
- Activity Feed
- Register
- Activate

**You Should Create:**
- Community Guidelines
- Privacy Policy
- Terms of Service
- FAQ
- Contact/Support

#### Step 5: Menu Structure

**Primary Menu:**
```
- Home
- Activity Feed
- Members
- Groups
- Forums
- About
  - Community Rules
  - How It Works
  - Contact Us
```

**User Menu (Logged In):**
```
- My Profile
- My Activity
- My Groups
- Messages (with count)
- Settings
- Logout
```

#### Step 6: First Content

**Welcome Activity Post:**
```
"Welcome to [Community Name]! We're excited to have you here.
Start by completing your profile, joining groups that interest you,
and introducing yourself to the community. Need help? Check our FAQ."
```

**Starter Groups:**
- Welcome & Introductions
- General Discussion
- Announcements
- Feature Requests
- [Your Topic Groups]

### Success Metrics
- 50+ members in first month
- 10+ posts daily
- 5+ active groups
- 80% profile completion rate

---

## Scenario 2: Online Learning Platform

### What You're Building
An educational site where instructors create courses, students learn, and progress is tracked.

### Examples
- Corporate training portal
- Online academy
- Skill development platform
- Certification programs
- Tutorial marketplace

### Essential Setup Steps

#### Step 1: Install LMS Plugin

**Choose One:**
```
LearnDash (Recommended):
- Most features
- Best integration with Reign
- Quiz/assignment system
- Certificate generation

Alternative Options:
- LifterLMS
- Tutor LMS
- Sensei LMS
```

#### Step 2: LMS Configuration

**LearnDash Settings:**
```
LearnDash → Settings:
- Course Grid: Enabled
- Focus Mode: Design 2
- Progress Bar: Enabled
- Course Builder: Enabled
- Video Progression: Optional
```

**Course Structure:**
```
Course
├── Section 1
│   ├── Lesson 1
│   ├── Lesson 2
│   └── Quiz 1
├── Section 2
│   ├── Lesson 3
│   ├── Assignment 1
│   └── Quiz 2
└── Final Exam
```

#### Step 3: Design Configuration

**Customizer Settings:**
```
Header: Style 4 (Transparent) - Professional look
Layout: Boxed - Focused learning
Sidebar: None - Distraction-free
Typography: Clear, readable fonts
Colors: Calm, professional palette
```

**Learning-Specific Settings:**
```
Reign Settings → LearnDash:
- Course Archive: Grid layout
- Columns: 3
- Show: Progress, difficulty, duration
- Sidebar: None for lessons
```

#### Step 4: Payment Integration

**For Paid Courses:**
```
WooCommerce Setup:
1. Install WooCommerce
2. Install LearnDash-WooCommerce integration
3. Configure payment gateways (Stripe/PayPal)
4. Set up course products
```

**Membership Levels:**
```
Basic: Individual course purchase
Premium: All-access pass
Corporate: Team licenses
```

#### Step 5: Create Structure

**Essential Pages:**
- Course Catalog
- My Courses (student dashboard)
- Instructor Dashboard
- Certificates
- Support/Help

**Menu Structure:**
```
Main Menu:
- Courses
  - Browse Catalog
  - Categories
  - Instructors
- My Learning
- Pricing
- About
  - How It Works
  - Success Stories
- Support
```

#### Step 6: Student Experience

**Dashboard Widgets:**
- Course Progress
- Recent Achievements
- Upcoming Assignments
- Leaderboard
- Certificates Earned

**Gamification Elements:**
- Points for completion
- Badges for achievements
- Certificates
- Progress tracking
- Leaderboards

### Success Metrics
- Course completion rate >60%
- Student satisfaction >4.5/5
- Active daily users
- Revenue per student

---

## Scenario 3: Multi-Vendor Marketplace

### What You're Building
An Amazon/Etsy-style marketplace where multiple vendors sell products through your platform.

### Examples
- Handmade crafts marketplace
- Digital products store
- Local farmers market online
- Service marketplace
- B2B wholesale platform

### Essential Setup Steps

#### Step 1: E-commerce Foundation

**Install Core Plugins:**
```
Required:
✅ WooCommerce - E-commerce engine
✅ Dokan or WC Vendors - Multi-vendor system

Choose Dokan for:
- Easier setup
- Better vendor dashboard
- Built-in reports

Choose WC Vendors for:
- More flexibility
- Commission options
- Advanced features
```

#### Step 2: Vendor Configuration

**Dokan Settings:**
```
Dokan → Settings:
- Commission: 80% vendor, 20% platform
- New vendor: Requires approval
- Product publishing: Requires review
- Vendor verification: Enabled
- Store banner: Allowed
```

**Vendor Capabilities:**
```
Can Do:
✅ Add/edit products
✅ Manage orders
✅ View reports
✅ Set shipping
✅ Communicate with customers

Cannot Do:
❌ Change commission
❌ Access admin area
❌ Edit other vendors
❌ Refund without approval
```

#### Step 3: Marketplace Design

**Customizer Settings:**
```
Header: Style 1 - Classic commerce
Shop Columns: 4 products
Sidebar: Left - For filters
Product Cards: Show rating, vendor name
Quick View: Enabled
```

**Homepage Sections:**
```
1. Hero slider - Featured products
2. Shop by category
3. Featured vendors
4. New arrivals
5. Best sellers
6. Vendor spotlight
7. Newsletter signup
```

#### Step 4: Vendor Onboarding

**Registration Process:**
```
1. Vendor applies
2. Submit documents
3. Admin reviews
4. Account approved
5. Setup wizard:
   - Store name
   - Banner/logo
   - Payment details
   - Shipping zones
   - Return policy
```

**Vendor Resources:**
```
Create:
- Vendor handbook PDF
- Product photo guidelines
- Pricing strategies
- Marketing tips
- FAQ document
```

#### Step 5: Payment Flow

**Commission Structure:**
```
Payment Gateway → Platform Account
├── Vendor Commission (80%)
│   └── Paid weekly/monthly
└── Platform Fee (20%)
    ├── Transaction fees
    ├── Platform profit
    └── Marketing budget
```

**Payout Methods:**
- PayPal mass payments
- Stripe Connect
- Bank transfer
- Store credit

#### Step 6: Trust & Safety

**Review System:**
- Product reviews
- Vendor ratings
- Verified vendor badges
- Report abuse option

**Dispute Resolution:**
- Clear return policy
- Dispute ticket system
- Admin mediation
- Refund process

### Success Metrics
- 50+ active vendors
- 500+ products listed
- <3% dispute rate
- >$10k monthly GMV

---

## Scenario 4: Membership & Subscription Site

### What You're Building
A site where users pay for exclusive access to content, community, or services.

### Examples
- Premium content library
- Coaching community
- Industry insights platform
- Fitness programs
- Private investment group

### Essential Setup Steps

#### Step 1: Membership Plugin

**Recommended Setup:**
```
Paid Memberships Pro:
- Multiple membership levels
- Content restrictions
- Payment integration
- Member directory
- Reports & analytics
```

#### Step 2: Membership Levels

**Typical Structure:**
```
Free Member:
- Basic profile
- Limited content
- Community access

Silver ($19/month):
- Full content library
- Group access
- Monthly webinars

Gold ($49/month):
- Everything in Silver
- Direct messaging
- Priority support
- Downloadable resources

Platinum ($99/month):
- Everything in Gold
- 1-on-1 coaching
- Early access
- Exclusive events
```

#### Step 3: Content Restriction

**Protection Rules:**
```
Content Types:
- Free: Blog posts, basic guides
- Silver: Video tutorials, templates
- Gold: Courses, toolkits
- Platinum: Coaching calls, strategies

Restriction Messages:
"This content is exclusive to [Level] members.
Upgrade your membership to access."
```

#### Step 4: Payment Setup

**Gateway Configuration:**
```
Stripe/PayPal:
- Recurring payments
- Trial periods (7 days)
- Discount codes
- Failed payment retry
- Cancellation handling
```

**Pricing Strategies:**
- Monthly vs Annual (20% discount)
- First month special
- Referral discounts
- Limited-time offers

#### Step 5: Member Experience

**Member Dashboard:**
```
Welcome Section:
- Membership status
- Renewal date
- Quick stats

Content Access:
- My courses
- Exclusive content
- Downloads
- Upcoming events

Community:
- Member directory
- Private groups
- Direct messages
```

#### Step 6: Retention Features

**Keep Members Engaged:**
- Weekly new content
- Member-only events
- Exclusive community
- Progress tracking
- Achievement badges
- Member spotlights

### Success Metrics
- <5% monthly churn
- >30% annual renewals
- >50% login weekly
- Positive testimonials

---

## Scenario 5: Business/Corporate Website

### What You're Building
A professional website representing your company, services, and brand.

### Examples
- Agency website
- Consulting firm
- SaaS company
- Local business
- Professional services

### Essential Setup Steps

#### Step 1: Professional Design

**Theme Configuration:**
```
Header: Style 3 - Logo prominent
Footer: 4 columns - Maximum info
Typography: Professional (Montserrat/Open Sans)
Colors: Brand colors
Layout: Wide and modern
```

#### Step 2: Essential Pages

**Core Business Pages:**
```
Homepage:
- Hero with CTA
- Services overview
- Why choose us
- Testimonials
- Recent work
- Contact CTA

About:
- Company story
- Mission/vision
- Team members
- Awards/certifications
- Company culture

Services:
- Service catalog
- Process explanation
- Pricing (if applicable)
- Case studies
- FAQ

Contact:
- Contact form
- Office locations
- Business hours
- Support options
```

#### Step 3: Lead Generation

**Contact Forms:**
```
Contact Form 7 or WPForms:
- General inquiry
- Quote request
- Support ticket
- Newsletter signup
- Career applications
```

**Call-to-Actions:**
- "Get Free Consultation"
- "Download Our Guide"
- "Schedule Demo"
- "Get Quote"

#### Step 4: Trust Building

**Social Proof Elements:**
- Client logos
- Testimonials slider
- Case studies
- Success metrics
- Industry certifications
- Awards & recognition

#### Step 5: SEO Foundation

**On-Page Optimization:**
- Yoast SEO configuration
- Meta descriptions
- Schema markup
- XML sitemap
- Page speed optimization
- Mobile responsiveness

#### Step 6: Analytics & Tracking

**Setup Tracking:**
- Google Analytics 4
- Google Tag Manager
- Conversion tracking
- Heatmap tool (Hotjar)
- Form analytics

### Success Metrics
- <3 second load time
- >2 minute average session
- <40% bounce rate
- Steady lead flow

---

## Quick Decision Helper

### Choose Social Community If:
- Building around shared interests
- User-generated content is key
- Connections between members matter
- Discussion is primary activity

### Choose Learning Platform If:
- Selling knowledge/skills
- Need progress tracking
- Structured content delivery
- Certification important

### Choose Marketplace If:
- Multiple sellers needed
- Physical/digital products
- Commission-based model
- Vendor management required

### Choose Membership If:
- Recurring revenue model
- Exclusive content/access
- Tiered benefits
- Community + content

### Choose Business Site If:
- Showcasing services
- Lead generation focus
- Brand presence priority
- B2B communications

## Universal Best Practices

### Launch Preparation
1. **Soft Launch** - Friends and family first
2. **Beta Testing** - Limited user group
3. **Feedback Loop** - Gather and implement
4. **Content Ready** - Have 30 days of content
5. **Support Ready** - FAQ and help docs

### Post-Launch Checklist
- [ ] Analytics working
- [ ] Emails sending
- [ ] Payments processing
- [ ] Mobile tested
- [ ] Speed optimized
- [ ] Backups scheduled
- [ ] Security configured
- [ ] SEO basics done
- [ ] Legal pages added
- [ ] Support system ready

---

**Ready to Build?** Choose your scenario above and follow the specific setup guide. Remember, you can always combine features from different scenarios to create your unique platform!