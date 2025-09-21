# Reign TutorLMS Addon - Course Customization Guide

## What You'll Learn
This guide shows you how to make your courses look stunning and provide an engaging learning experience. We'll customize layouts, colors, and features to match your brand and captivate your students.

## Quick Overview
**Time needed:** 45-60 minutes
**Difficulty:** Easy (visual customization)
**Tools needed:** WordPress Customizer

---

## Part 1: Course Layout Options

### Choose Your Course Display Style

**Where to customize:**
```
Appearance → Customize → Reign TutorLMS → Course Layout
```

### Available Layout Styles

| Layout Style | What It Looks Like | Best For |
|--------------|-------------------|----------|
| **Grid View** | Cards in neat rows | Visual learners |
| **List View** | Detailed rows | Information-rich |
| **Masonry** | Pinterest-style | Mixed content types |
| **Featured** | Hero course + grid | Homepage highlights |
| **Carousel** | Sliding course cards | Limited space |

### Course Card Layouts

**Design options:**

```yaml
Card Style:
  - Modern (clean and minimal)
  - Classic (traditional design)
  - Compact (information-dense)
  - Visual (image-focused)
  - Professional (business-like)

Card Content:
  - Course thumbnail
  - Title and description
  - Instructor information
  - Price and enrollment
  - Progress bar (enrolled students)
  - Duration and difficulty
  - Student ratings and reviews
  - Category badges
```

---

## Part 2: Course Catalog Customization

### Catalog Page Layout

**Configure main course listing:**

```yaml
Courses Per Page: 12 (optimal for performance)
Grid Columns:
  - Desktop: 3 columns
  - Tablet: 2 columns
  - Mobile: 1 column

Sorting Options:
  - Date published (newest first)
  - Price: Low to high
  - Price: High to low
  - Alphabetical A-Z
  - Most popular
  - Highest rated
  - Student count
  - Duration
```

### Course Filtering System

**Add helpful filters:**

| Filter Type | Options | Benefits |
|-------------|---------|----------|
| **Category** | Subject areas | Easy browsing |
| **Difficulty** | Beginner, Intermediate, Advanced | Skill matching |
| **Duration** | Under 5 hours, 5-20 hours, 20+ hours | Time planning |
| **Price** | Free, Under $50, $50-$200, $200+ | Budget filtering |
| **Rating** | 4+ stars, 3+ stars | Quality assurance |
| **Instructor** | By teacher name | Follow favorites |
| **Language** | Multiple languages | Global audience |
| **Format** | Video, Text, Interactive | Learning style |

**Enable in Customizer:**
```
Appearance → Customize → Reign TutorLMS → Course Filters
```

---

## Part 3: Individual Course Page Design

### Course Header Customization

**Header elements to include:**

```yaml
Course Hero Section:
  - Course preview video or image
  - Course title and subtitle
  - Instructor photo and bio
  - Enrollment/purchase button
  - Course rating display
  - Social sharing buttons

Course Meta Info:
  - Price and any discounts
  - Total duration estimate
  - Difficulty level indicator
  - Student enrollment count
  - Last updated date
  - Language options
  - Certificate availability
  - Course materials count
```

### Course Content Layout

**Organize course information:**

**Left Sidebar (Course Info):**
- Course progress tracker
- Lesson navigation menu
- Course materials download
- Prerequisites information
- What you'll learn
- Certificate details
- Instructor contact

**Main Content Area:**
- Course description
- Course curriculum display
- Student reviews section
- FAQ section
- Course announcements
- Related courses

**Right Sidebar (Additional):**
- Enrollment/purchase widget
- Course sharing options
- Similar courses
- Instructor's other courses
- Recent student activity
- Course statistics

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
  - Course index dropdown
  - Lesson bookmarking

Content Area:
  - Video player (responsive)
  - Text content formatting
  - Downloadable resources
  - Interactive elements
  - Student notes section
  - Discussion area
```

### Video Player Customization

**For video-based courses:**

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Player Theme** | Dark professional | Easy on eyes |
| **Playback Speed** | 0.5x to 2x | Student preference |
| **Auto-play Next** | Optional | User choice |
| **Chapter Markers** | Yes | Easy navigation |
| **Subtitles** | Yes | Accessibility |
| **Quality Options** | Auto + manual | Bandwidth adaptation |
| **Download Option** | Limited | Content protection |
| **Video Resume** | Yes | Continue watching |

### Lesson Sidebar Content

**What to show in lesson sidebar:**

```yaml
Course Navigation:
  - Clickable lesson list
  - Completion status icons
  - Lesson duration display
  - Lock incomplete lessons
  - Progress percentage
  - Topic organization

Learning Tools:
  - Take notes feature
  - Bookmark lessons
  - Q&A for this lesson
  - Rate lesson
  - Report issues
  - Share lesson

Resources:
  - Download materials
  - External links
  - Additional reading
  - Practice exercises
  - Related videos
```

---

## Part 5: Quiz & Assessment Design

### Quiz Interface Customization

**Make quizzes engaging:**

```yaml
Quiz Design:
  - Clean, focused layout
  - Progress bar (questions remaining)
  - Timer display (if timed)
  - Question counter
  - Clear answer options
  - Helpful instructions
  - Review mode

Interaction Elements:
  - Large, touch-friendly buttons
  - Hover effects on options
  - Immediate visual feedback
  - Smooth transitions
  - Clear submit button
  - Save progress option
  - Hint system (optional)
```

### Results Page Design

**Show results effectively:**

```yaml
Results Display:
  - Pass/fail status (prominent)
  - Score percentage
  - Points earned
  - Time taken
  - Correct answers count
  - Performance feedback
  - Next steps guidance
  - Retake option (if allowed)
  - Certificate download
  - Social sharing
```

---

## Part 6: Student Dashboard Customization

### Dashboard Layout Options

**Customize student experience:**

```yaml
Dashboard Sections:
  - Welcome message
  - Course progress cards
  - Recent activity feed
  - Upcoming deadlines
  - Achievement showcase
  - Quick actions menu
  - Learning statistics
  - Recommended courses
  - Wishlist display
  - Purchase history
```

### Instructor Dashboard

**For course creators:**

```yaml
Instructor Sections:
  - Course performance metrics
  - Student progress overview
  - Recent enrollments
  - Quiz results summary
  - Q&A management
  - Revenue tracking
  - Course creation tools
  - Analytics dashboard
  - Announcement center
  - Student messaging
```

---

## Part 7: Color Scheme & Branding

### Brand Color Integration

**Where to set colors:**
```
Appearance → Customize → Colors → TutorLMS
```

**Key color elements:**

| Element | Purpose | Recommendation |
|---------|---------|----------------|
| **Primary Color** | Buttons, links | Your brand color |
| **Secondary Color** | Headers, accents | Complementary shade |
| **Success Color** | Completion, passing | Green (#28a745) |
| **Warning Color** | Alerts, pending | Amber (#ffc107) |
| **Danger Color** | Errors, failing | Red (#dc3545) |
| **Info Color** | Information, tips | Blue (#17a2b8) |
| **Text Color** | Content readability | Dark gray (#333) |
| **Background** | Page background | Light neutral (#f8f9fa) |

### Typography Settings

**Choose readable fonts:**

```yaml
Headings:
  - Font: Sans-serif (Inter, Roboto)
  - Course titles: 28-32px
  - Lesson titles: 24-28px
  - Section headers: 20-24px
  - Widget titles: 18-20px

Body Text:
  - Font: Sans-serif for screen
  - Size: 16-18px (mobile-friendly)
  - Line height: 1.6 (readability)
  - Color: Dark gray (not pure black)
  - Letter spacing: Normal
```

---

## Part 8: Mobile Learning Experience

### Mobile-Specific Customizations

**Optimize for mobile learning:**

```yaml
Mobile Layout:
  - Single column design
  - Large tap targets (44px min)
  - Simplified navigation
  - Touch-friendly video player
  - Easy-to-read text size
  - Thumb-friendly buttons
  - Swipe gestures

Mobile Features:
  - Swipe between lessons
  - Pull-to-refresh content
  - Offline content capability
  - Progressive loading
  - Quick course search
  - Voice search (if supported)
```

### Touch-Friendly Elements

**Mobile optimization details:**

```yaml
Button Sizes: Minimum 44px touch target
Spacing: 16px between clickable elements
Scrolling: Smooth momentum scrolling
Zoom: Pinch-to-zoom for content
Orientation: Support both orientations
Keyboard: Mobile-optimized forms
Navigation: Thumb-reach friendly
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
  - Learning streaks
  - Points system
  - Leaderboards

Reward System:
  - Badges for milestones
  - Certificates for completion
  - Course completion rewards
  - Perfect quiz scores
  - Participation awards
  - Social recognition
```

### Social Learning Features

**With BuddyPress integration:**

```yaml
Community Features:
  - Student profiles
  - Course activity feeds
  - Study groups
  - Discussion forums
  - Peer connections
  - Mentorship matching
  - Course alumni network
```

---

## Part 10: Content Enhancement

### Rich Media Integration

**Enhance course content:**

```yaml
Supported Media:
  - HD video content
  - Interactive PDFs
  - Audio lessons/podcasts
  - Image galleries
  - Presentation slides
  - Interactive quizzes
  - External tool embeds
  - 360° virtual tours
  - Interactive simulations
```

### Downloadable Resources

**Provide valuable materials:**

```yaml
Resource Types:
  - PDF worksheets
  - Audio files
  - Video downloads (limited)
  - Templates and tools
  - Code samples
  - Reading lists
  - Quick reference guides
  - Bonus materials
  - Software files
  - Project files
```

---

## Part 11: Accessibility Features

### Make Learning Accessible

**Accessibility improvements:**

```yaml
Visual Accessibility:
  - High contrast mode
  - Scalable text options
  - Alt text for images
  - Clear focus indicators
  - Screen reader support
  - Color-blind friendly palette
  - Large cursor support

Audio/Video Accessibility:
  - Closed captions
  - Transcripts
  - Audio descriptions
  - Keyboard navigation
  - Speed controls
  - Pause/play shortcuts
  - Volume controls
```

---

## Quick Customization Recipes

### Recipe 1: Corporate Training Platform

```yaml
Style: Professional and formal
Colors: Company brand colors (blues/grays)
Layout: List view with detailed info
Features: Compliance tracking, mandatory completion
Navigation: Structured progression
Assessments: Rigorous testing
Reporting: Detailed analytics
Branding: Corporate identity
```

### Recipe 2: Creative Skills Academy

```yaml
Style: Visual and inspiring
Colors: Bright creative palette
Layout: Grid with large images
Features: Portfolio submissions
Navigation: Flexible exploration
Assessments: Project-based
Community: Strong peer interaction
Showcasing: Student work galleries
```

### Recipe 3: Professional Certification

```yaml
Style: Authoritative and structured
Colors: Conservative professional
Layout: Organized curriculum view
Features: CEU tracking, compliance
Navigation: Sequential modules
Assessments: Rigorous testing
Certification: Industry-recognized
Proctoring: Secure testing
```

### Recipe 4: Language Learning Hub

```yaml
Style: Friendly and encouraging
Colors: Warm and motivating
Layout: Progress-focused design
Features: Speaking practice, flashcards
Navigation: Skill-based progression
Assessments: Interactive exercises
Community: Language exchange
Gamification: Streaks and levels
```

---

## Advanced Customization

### Custom CSS Snippets

**Add to Customizer → Additional CSS:**

```css
/* Custom course card hover effect */
.tutor-course-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 15px 35px rgba(0,0,0,0.1);
    transition: all 0.3s ease;
}

/* Custom progress bar styling */
.tutor-progress-bar {
    background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
    border-radius: 20px;
    height: 12px;
}

/* Custom button styling */
.tutor-btn-primary {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border: none;
    border-radius: 25px;
    padding: 15px 30px;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 1px;
}

/* Course grid animations */
.tutor-course-card {
    transition: all 0.3s ease;
    border-radius: 12px;
    overflow: hidden;
}

/* Mobile-specific adjustments */
@media (max-width: 768px) {
    .tutor-course-grid {
        grid-template-columns: 1fr;
        gap: 20px;
    }

    .tutor-lesson-sidebar {
        position: static;
        width: 100%;
    }
}

/* Quiz styling */
.tutor-quiz-question {
    background: #f8f9fa;
    padding: 24px;
    border-radius: 12px;
    margin-bottom: 20px;
    border-left: 4px solid #667eea;
}

/* Video player customization */
.tutor-video-player {
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 8px 25px rgba(0,0,0,0.1);
}
```

### Template Overrides

**For advanced customization:**

1. **Copy template files** from plugin to theme
2. **Create folder** `/tutor/` in your theme
3. **Copy templates** you want to modify
4. **Customize** while preserving structure

**Common template files:**
```
tutor/single-course.php
tutor/archive-course.php
tutor/dashboard/dashboard.php
tutor/single-lesson.php
tutor/quiz/quiz.php
```

---

## Performance Optimization

### Speed Up Course Pages

```yaml
Image Optimization:
  - Compress course images (WebP format)
  - Lazy load images
  - Use CDN for media
  - Optimize video thumbnails
  - Progressive JPEG loading

Caching Strategy:
  - Cache course catalog pages
  - Exclude user dashboards
  - Minify CSS/JS
  - Combine files where possible
  - Database query optimization

Content Delivery:
  - External video hosting
  - Enable browser caching
  - Optimize database queries
  - Regular cache cleanup
  - Image sprite techniques
```

---

## Testing Your Customizations

### Cross-Device Testing

**Test on multiple devices:**

1. **Desktop computers** (1920px, 1366px, 1024px)
2. **Tablets** (iPad, Android tablets, Surface)
3. **Smartphones** (iPhone, Android phones)
4. **Different browsers** (Chrome, Firefox, Safari, Edge)

### User Experience Testing

**Test the complete learning journey:**

1. **Course discovery** - Finding relevant courses
2. **Enrollment process** - Smooth signup/purchase
3. **Content consumption** - Easy lesson navigation
4. **Progress tracking** - Clear indicators
5. **Assessment taking** - User-friendly quizzes
6. **Completion** - Satisfying conclusion
7. **Social interaction** - Q&A and community

---

## Common Customization Issues

### Troubleshooting Design Problems

**"Courses look broken after changes"**
- Clear all caches (browser + site)
- Check browser console for errors
- Verify CSS conflicts
- Test with default theme

**"Mobile view not responsive"**
- Check viewport meta tag
- Verify responsive settings
- Test CSS media queries
- Clear mobile-specific cache

**"Videos not displaying properly"**
- Check video format compatibility
- Verify hosting service settings
- Test on different browsers
- Check mobile video settings

**"Quiz layout broken"**
- Verify quiz template files
- Check CSS conflicts
- Test different question types
- Clear quiz cache

---

## Best Practices

### Design Do's ✅

- Keep layouts clean and uncluttered
- Use consistent spacing throughout
- Make buttons large enough for touch
- Ensure excellent color contrast
- Test on real devices frequently
- Prioritize content readability
- Make navigation intuitive
- Optimize for fast loading
- Use progressive enhancement
- Follow accessibility guidelines

### Design Don'ts ❌

- Don't use too many different fonts
- Don't make text too small for mobile
- Don't hide important course information
- Don't auto-play videos with sound
- Don't ignore accessibility requirements
- Don't overuse animations
- Don't neglect loading performance
- Don't forget about offline scenarios
- Don't make navigation too complex
- Don't ignore browser compatibility

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
🌐 Showcase: wbcomdesigns.com/tutor-showcase