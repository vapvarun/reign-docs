# Reign LearnDash Addon - Course Customization Guide

## What You'll Learn
This guide shows you how to make your courses look amazing and provide the best learning experience. We'll customize layouts, colors, and features to match your brand and engage your students.

## Quick Overview
**Time needed:** 45-60 minutes  
**Difficulty:** Easy (visual customization)  
**Tools needed:** WordPress Customizer

---

## Part 1: Course Layout Options

### Choose Your Course Display Style

**Where to customize:**
```
Appearance → Customize → Reign LearnDash → Course Layout
```

### Available Layout Styles

| Layout Style | What It Looks Like | Best For |
|--------------|-------------------|----------|
| **Grid View** | Cards in rows | Visual courses |
| **List View** | One per row with details | Professional training |
| **Masonry** | Pinterest-style layout | Mixed content sizes |
| **Carousel** | Sliding course cards | Homepage features |
| **Category Tabs** | Organized by subject | Multi-topic platforms |

### Course Card Layouts

**Design options:**

```yaml
Card Style:
  - Modern (clean lines)
  - Classic (traditional)
  - Minimal (simple)
  - Detailed (lots of info)

Card Content:
  - Course image (always)
  - Title and description
  - Instructor info
  - Price and enrollment
  - Progress bar (for enrolled)
  - Difficulty and duration
```

---

## Part 2: Course Archive Customization

### Archive Page Layout

**Configure main course listing:**

```yaml
Courses Per Page: 12 (good balance)
Grid Columns: 
  - Desktop: 3 columns
  - Tablet: 2 columns  
  - Mobile: 1 column

Sorting Options:
  - Newest first
  - Price: Low to high
  - Price: High to low
  - Alphabetical A-Z
  - Most popular
  - Highest rated
  - By category
```

### Course Filtering System

**Add helpful filters:**

| Filter Type | Options | Benefits |
|-------------|---------|----------|
| **Category** | Subject areas | Easy browsing |
| **Difficulty** | Beginner, Intermediate, Advanced | Skill matching |
| **Duration** | Under 2 hours, 2-10 hours, 10+ hours | Time planning |
| **Price** | Free, Under $50, $50-$100, $100+ | Budget filtering |
| **Format** | Video, Text, Mixed | Learning preference |
| **Instructor** | By teacher name | Follow favorites |

**Enable in Customizer:**
```
Appearance → Customize → Reign LearnDash → Course Filters
```

---

## Part 3: Individual Course Page Design

### Course Header Customization

**Header elements to include:**

```yaml
Course Banner: 
  - Hero image or video
  - Course title overlay
  - Instructor photo
  - Enrollment button

Course Info:
  - Price and discount
  - Duration estimate
  - Difficulty level
  - Student count
  - Rating and reviews
  - Last updated date
```

### Course Content Layout

**Organize course information:**

**Left Sidebar (Course Info):**
- Enrollment button
- Course progress
- Course materials
- Prerequisites
- What you'll learn
- Certificate info

**Main Content Area:**
- Course description
- Curriculum/lessons
- Instructor bio
- Student reviews
- FAQs

**Right Sidebar (Related):**
- Similar courses
- Instructor's other courses
- Student testimonials
- Social sharing

---

## Part 4: Lesson Page Customization

### Lesson Display Options

**Configure lesson layout:**

```yaml
Lesson Navigation:
  - Course outline sidebar
  - Previous/Next buttons
  - Progress indicator
  - "Mark Complete" button

Content Area:
  - Video player (if video lesson)
  - Text content
  - Downloadable materials
  - Assignment instructions
  - Discussion area
```

### Video Player Customization

**For video-based courses:**

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Player Style** | Modern dark theme | Professional look |
| **Playback Speed** | 0.5x to 2x | Student preference |
| **Auto-advance** | Optional | Depends on content |
| **Chapter markers** | Yes | Easy navigation |
| **Transcript** | Yes | Accessibility |
| **Notes feature** | Yes | Better learning |

### Lesson Sidebar Content

**What to show in lesson sidebar:**

```yaml
Course Progress:
  - Overall completion %
  - Current lesson
  - Lessons remaining
  - Time estimate

Course Navigation:
  - Clickable lesson list
  - Lock incomplete lessons
  - Show lesson duration
  - Mark completion status

Additional Features:
  - Download materials
  - Take notes
  - Ask questions
  - Rate lesson
```

---

## Part 5: Quiz & Assessment Design

### Quiz Interface Customization

**Make quizzes engaging:**

```yaml
Quiz Design:
  - Clean, distraction-free layout
  - Progress bar showing questions left
  - Timer display (if timed)
  - Question counter
  - Clear answer options

Interaction Elements:
  - Large, touch-friendly buttons
  - Hover effects on options
  - Immediate feedback
  - Encouraging animations
  - Clear submit button
```

### Results Page Design

**Show results clearly:**

```yaml
Results Display:
  - Pass/fail status
  - Score percentage
  - Correct vs incorrect
  - Time taken
  - Comparison to average
  - Next steps
  - Retake option (if allowed)
```

---

## Part 6: User Dashboard Customization

### Student Dashboard Layout

**Customize student experience:**

```yaml
Dashboard Sections:
  - Welcome message
  - Course progress overview
  - Recently accessed
  - Upcoming assignments
  - Achievements/certificates
  - Learning statistics
  - Recommended courses
```

### Instructor Dashboard

**For course creators:**

```yaml
Instructor Sections:
  - Course analytics
  - Student progress
  - Recent enrollments
  - Quiz results
  - Student messages
  - Revenue tracking
  - Quick course creation
```

---

## Part 7: Color Scheme & Branding

### Brand Color Integration

**Where to set colors:**
```
Appearance → Customize → Colors → LearnDash
```

**Key color elements:**

| Element | Purpose | Recommendation |
|---------|---------|----------------|
| **Primary Color** | Buttons, links | Your brand color |
| **Secondary Color** | Headers, accents | Complementary shade |
| **Progress Color** | Completion bars | Green (success feeling) |
| **Text Color** | Content readability | Dark gray, not black |
| **Background** | Page background | Light, neutral |
| **Card Background** | Course cards | White or very light |

### Typography Settings

**Choose readable fonts:**

```yaml
Headings: Sans-serif (modern)
Body Text: Sans-serif (readability)
Sizes:
  - Course titles: 24-28px
  - Lesson titles: 20-24px
  - Body text: 16-18px
  - Small text: 14px
```

---

## Part 8: Mobile Learning Experience

### Mobile-Specific Customizations

**Optimize for mobile learning:**

```yaml
Mobile Layout:
  - Single column design
  - Large tap targets
  - Simplified navigation
  - Touch-friendly video player
  - Easy-to-read text

Mobile Features:
  - Swipe between lessons
  - Offline content access
  - Progress sync
  - Push notifications
  - Quick actions
```

### Touch-Friendly Elements

**Make mobile learning easy:**

```yaml
Button Sizes: Minimum 44px touch target
Spacing: Adequate between clickable elements
Scrolling: Smooth, momentum scrolling
Zoom: Pinch-to-zoom for detailed content
Orientation: Support both portrait/landscape
```

---

## Part 9: Interactive Features

### Gamification Elements

**Add engagement features:**

```yaml
Progress Tracking:
  - Visual progress bars
  - Completion percentages
  - Milestone celebrations
  - Achievement badges
  - Leaderboards (optional)

Reward System:
  - Points for completion
  - Badges for achievements
  - Certificates for courses
  - Social sharing
  - Success animations
```

### Social Learning Features

**If using BuddyPress integration:**

```yaml
Community Features:
  - Student profiles
  - Course activity feeds
  - Discussion groups
  - Peer connections
  - Study groups
  - Mentorship matching
```

---

## Part 10: Content Enhancement

### Rich Media Integration

**Enhance course content:**

```yaml
Supported Media:
  - HD video content
  - Interactive PDFs
  - Audio lessons
  - Image galleries
  - Presentation slides
  - Interactive elements
  - External tool embedding
```

### Downloadable Resources

**Provide valuable materials:**

```yaml
Resource Types:
  - PDF worksheets
  - Audio files
  - Video downloads (limited)
  - Templates and tools
  - Reading lists
  - Quick reference guides
```

---

## Part 11: Accessibility Features

### Make Learning Accessible

**Accessibility improvements:**

```yaml
Visual Accessibility:
  - High contrast options
  - Large text options
  - Alt text for images
  - Clear focus indicators
  - Screen reader support

Audio/Video Accessibility:
  - Closed captions
  - Transcripts
  - Audio descriptions
  - Keyboard navigation
  - Speed controls
```

---

## Quick Customization Recipes

### Recipe 1: Corporate Training Platform

```yaml
Style: Professional and clean
Colors: Company brand colors
Layout: Grid view with detailed cards
Features: Progress tracking, certificates
Navigation: Linear progression
Assessments: Mandatory quizzes
```

### Recipe 2: Creative Skills Academy

```yaml
Style: Visual and inspiring
Colors: Bright and creative
Layout: Masonry with large images
Features: Portfolio submissions
Navigation: Flexible exploration
Assessments: Project-based
```

### Recipe 3: Professional Certification

```yaml
Style: Authoritative and structured
Colors: Conservative blues/grays
Layout: List view with details
Features: CEU tracking, compliance
Navigation: Sequential modules
Assessments: Rigorous testing
```

### Recipe 4: Hobby Learning Hub

```yaml
Style: Friendly and approachable
Colors: Warm and inviting
Layout: Grid with community features
Features: Social sharing, discussions
Navigation: Self-paced exploration
Assessments: Optional, encouraging
```

---

## Advanced Customization

### Custom CSS Snippets

**Add to Customizer → Additional CSS:**

```css
/* Custom course card hover effect */
.ld-course-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
    transition: all 0.3s ease;
}

/* Custom progress bar color */
.ld-progress-bar {
    background: linear-gradient(90deg, #4CAF50, #8BC34A);
    border-radius: 10px;
}

/* Custom button styling */
.ld-button {
    background: #your-brand-color;
    border-radius: 5px;
    padding: 15px 30px;
    font-weight: 600;
}
```

### Template Overrides

**For advanced customization:**

1. **Copy template files** from plugin to theme
2. **Modify layouts** in theme folder
3. **Preserve updates** by using child theme

---

## Performance Optimization

### Speed Up Course Pages

```yaml
Image Optimization:
  - Compress course images
  - Use WebP format
  - Lazy load images
  - CDN for video content

Caching:
  - Cache course pages
  - Exclude user-specific content
  - Minify CSS/JS
  - Combine files
```

---

## Testing Your Customizations

### Cross-Device Testing

**Test on multiple devices:**

1. **Desktop computers** (various screen sizes)
2. **Tablets** (iPad, Android tablets)
3. **Smartphones** (iPhone, Android phones)
4. **Different browsers** (Chrome, Firefox, Safari, Edge)

### User Experience Testing

**Test the complete learning journey:**

1. **Course discovery** - Finding courses
2. **Enrollment process** - Easy signup
3. **Content consumption** - Smooth learning
4. **Progress tracking** - Clear indicators
5. **Assessment taking** - User-friendly quizzes
6. **Completion** - Satisfying conclusion

---

## Common Customization Issues

### Troubleshooting Design Problems

**"Courses look broken after changes"**
- Clear all caches
- Check browser console for errors
- Verify CSS conflicts
- Test with default theme

**"Mobile view not responsive"**
- Check viewport meta tag
- Verify responsive settings
- Test CSS media queries
- Clear mobile cache

**"Colors not applying"**
- Clear customizer cache
- Check CSS specificity
- Verify color codes
- Test with browser inspector

---

## Best Practices

### Design Do's ✅

- Keep layouts clean and uncluttered
- Use consistent spacing throughout
- Make buttons large enough for touch
- Ensure good color contrast
- Test on real devices
- Prioritize readability
- Make navigation intuitive

### Design Don'ts ❌

- Don't use too many fonts
- Don't make text too small
- Don't hide important information
- Don't use auto-playing videos
- Don't ignore mobile users
- Don't forget accessibility
- Don't overuse animations

---

## Next Steps

**Your courses look amazing! Now:**

1. **[Add Developer Features →](05-developer-guide.md)**
2. **[Create Course Content →](08-faq.md)**
3. **[Launch Your LMS →](07-troubleshooting.md)**

---

**Need Design Help?**  
📧 Email: support@wbcomdesigns.com  
🎨 Custom design service available  
💬 Forum: wbcomdesigns.com/support  
🎥 Design tutorials in member area