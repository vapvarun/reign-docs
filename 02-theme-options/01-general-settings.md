# General Settings - Complete Configuration Guide

## Overview

General Settings control the fundamental appearance and behavior of your Reign theme. These settings form the foundation of your site's design and user experience.

## Accessing General Settings

### Method 1: WordPress Customizer
```
Dashboard → Appearance → Customize → General
```

### Method 2: Reign Settings Panel
```
Dashboard → Appearance → Reign Settings → General Tab
```

### Method 3: Quick Access
- When logged in, hover over any element
- Click the edit pencil icon
- Navigate to General Settings

## Site Identity Configuration

### Logo Setup

#### Primary Logo
**Location:** Customize → General → Site Identity → Logo

**Specifications:**
- **Recommended Size:** 200px × 50px
- **Format:** PNG (transparent) or SVG (scalable)
- **File Size:** Under 100KB for optimal loading

**Upload Process:**
1. Click "Select Logo"
2. Choose from Media Library or Upload New
3. Crop if needed (optional)
4. Click "Select"
5. Preview appears instantly

#### Mobile Logo
**Purpose:** Smaller logo for mobile devices

**When to Use Different Mobile Logo:**
- Desktop logo too wide for mobile
- Need simplified version for small screens
- Want mobile-specific branding

**Settings:**
```
Mobile Logo: Enable
Upload Mobile Logo: [Select Image]
Mobile Logo Height: 40px (default)
```

#### Sticky Header Logo
**Purpose:** Logo that appears when header is sticky

**Use Cases:**
- Smaller logo when scrolling
- Different color for contrast
- Simplified version for minimal header

**Configuration:**
```
Sticky Logo: Enable
Upload Sticky Logo: [Select Image]
Sticky Logo Height: 35px
```

### Site Title & Tagline

#### Site Title
**What It Is:** Your website's name

**Where It Appears:**
- Browser tab
- Search results
- When logo not set
- Site header (optional)

**Best Practices:**
- Keep under 60 characters
- Include brand name
- Make it memorable
- Consider SEO keywords

#### Tagline
**What It Is:** Brief description of your site

**Examples:**
- "Your Community for Creative Professionals"
- "Learn, Connect, Grow Together"
- "The Marketplace for Handmade Goods"

**Display Options:**
```
□ Display Site Title
□ Display Tagline
□ Display Site Title and Tagline in Header
```

### Site Icon (Favicon)

**What It Is:** Small icon in browser tabs

**Requirements:**
- Size: 512px × 512px minimum
- Format: PNG or ICO
- Square image
- Clear at small sizes

**Where It Appears:**
- Browser tabs
- Bookmark icons
- Mobile home screens
- Browser history

## Layout Configuration

### Global Layout Style

#### Wide Layout
```
Setting: Layout → Wide
Effect: Content spans full browser width
Container: 100% width with max-width constraint
Best For: Modern, spacious designs
```

**When to Choose Wide:**
- Photography portfolios
- Video content
- Modern business sites
- Landing pages

#### Boxed Layout
```
Setting: Layout → Boxed
Effect: Content in centered box
Container: Fixed width with margins
Background: Visible outside content area
Best For: Traditional, focused designs
```

**When to Choose Boxed:**
- Text-heavy blogs
- News sites
- Corporate sites
- Classic designs

### Container Width

**Default Options:**
```
960px  - Narrow (Better for reading)
1170px - Standard (Balanced)
1400px - Wide (Modern, spacious)
Custom - Your specific width
```

**Custom Width Setup:**
```
Container Width: Custom
Custom Width Value: 1280px
Unit: px / % / vw
```

**Responsive Behavior:**
| Screen Size | Container Behavior |
|------------|-------------------|
| >1400px | Full container width |
| 1200-1400px | 95% of screen |
| 992-1199px | 90% of screen |
| 768-991px | 85% of screen |
| <768px | 95% of screen |

### Content Area Settings

#### Content Padding
**Top/Bottom Padding:**
```
Content Top Padding: 60px (default)
Content Bottom Padding: 60px (default)
Range: 0-100px
```

**Use Cases for Different Padding:**
- **0px:** Hero sections, full-bleed images
- **30px:** Compact, content-heavy sites
- **60px:** Standard spacing (recommended)
- **100px:** Luxury, minimalist designs

#### Content Background
```
Background Type:
○ Color (solid color)
○ Image (pattern/photo)
○ Gradient (color blend)
○ Transparent (inherit)

Background Color: #ffffff
Background Image: [Upload]
Background Repeat: No Repeat / Repeat / Repeat-X / Repeat-Y
Background Position: Center / Top / Bottom / Custom
Background Attachment: Scroll / Fixed
Background Size: Auto / Cover / Contain
```

## Sidebar Configuration

### Global Sidebar Position

#### Right Sidebar (Default)
```
Layout: Content (70%) | Sidebar (30%)
Reading Flow: Natural left-to-right
Best For: Blogs, standard sites
```

#### Left Sidebar
```
Layout: Sidebar (30%) | Content (70%)
Navigation: Sidebar acts as navigation
Best For: Documentation, tools
```

#### No Sidebar
```
Layout: Content (100%)
Focus: Maximum content width
Best For: Landing pages, portfolios
```

#### Both Sidebars
```
Layout: Left (25%) | Content (50%) | Right (25%)
Complexity: High information density
Best For: Magazine sites, portals
```

### Sidebar Behavior

#### Sticky Sidebar
```
Setting: Sidebar → Sticky Sidebar
Effect: Sidebar follows scroll
Requirements:
- Sidebar shorter than content
- Not on mobile
- JavaScript enabled
```

**Enable Sticky:**
```
Sticky Sidebar: ✓ Enable
Offset from Top: 100px (accounts for header)
Offset from Bottom: 50px (spacing from footer)
```

#### Sidebar on Mobile
```
Mobile Sidebar Display:
○ Hide on Mobile (default)
○ Show Below Content
○ Toggle Button
○ Off-canvas Slide
```

## Sub-Header Configuration

### Sub-Header Display
```
Enable Sub-Header: ✓
Position: Below Header / Above Header
Height: 50px (adjustable)
Background: Color / Image / Gradient
```

### Sub-Header Content

#### Breadcrumbs
```
Show Breadcrumbs: ✓
Breadcrumb Style:
○ Default (Home > Category > Post)
○ With Icons
○ Minimal (Category / Post)

Breadcrumb Separator: > / → / | / •
Include Home: ✓
```

#### Page Title in Sub-Header
```
Display Page Title: ✓
Title Alignment: Left / Center / Right
Title Typography:
- Font Size: 24px
- Font Weight: 600
- Text Transform: None / Uppercase / Capitalize
```

## Login/Register Settings

### Login Popup Configuration

#### Enable Login Popup
```
Login Style:
○ Redirect to Login Page
○ Popup Modal (recommended)
○ Slide Panel
```

#### Popup Settings
```
Popup Width: 400px
Popup Position: Center / Top
Background Overlay: ✓
Close on Click Outside: ✓
Show Remember Me: ✓
Show Lost Password: ✓
```

### Registration Options

#### Registration Form Fields
```
Default Fields:
✓ Username (required)
✓ Email (required)
✓ Password (required)

Additional Fields:
□ First Name
□ Last Name
□ Display Name
□ Terms Acceptance
```

#### After Registration
```
Redirect After Registration:
○ Stay on Same Page
○ Go to Profile
○ Go to Dashboard
○ Custom URL: [___________]
```

## 404 Page Settings

### 404 Page Configuration
```
404 Page Title: "Oops! Page Not Found"
404 Message: "The page you're looking for doesn't exist."
Show Search Box: ✓
Show Recent Posts: ✓
Show Categories: □
Custom 404 Page: [Select Page]
```

### 404 Page Suggestions
```
Suggested Links:
✓ Homepage
✓ Blog
✓ Contact
□ Shop
□ Community
```

## Preloader Settings

### Enable Preloader
```
Show Preloader: ✓
Preloader Style:
○ Spinning Circle
○ Progress Bar
○ Custom Image
○ Text Loading

Preloader Duration: Auto / Fixed (seconds)
Background Color: #ffffff
Loader Color: #primary-color
```

### Custom Preloader
```
Custom Image: [Upload GIF/SVG]
Image Size: 100px
Show Loading Text: ✓
Loading Text: "Loading..."
```

## Scroll to Top

### Back to Top Button
```
Enable Back to Top: ✓
Button Style:
○ Circle
○ Square
○ Rounded Square

Button Position: Bottom Right / Bottom Left
Show After Scrolling: 300px
Icon: ↑ / ⬆ / Custom Icon
```

### Button Styling
```
Background Color: #primary
Icon Color: #ffffff
Hover Background: #secondary
Button Size: 40px
Opacity: 0.8
```

## Custom Code Injection

### Header Code
**Location:** General → Custom Code → Header

**Use For:**
- Google Analytics
- Facebook Pixel
- Custom meta tags
- Font imports
- Third-party scripts

**Example:**
```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

### Footer Code
**Location:** General → Custom Code → Footer

**Use For:**
- Chat widgets
- Tracking pixels
- Custom JavaScript
- Third-party widgets

### Custom CSS
**Location:** General → Custom CSS

**Best Practices:**
- Use specific selectors
- Add !important sparingly
- Comment your code
- Test on mobile

**Example:**
```css
/* Custom button style */
.site-button {
    background: linear-gradient(45deg, #667eea 0%, #764ba2 100%);
    padding: 15px 30px;
    border-radius: 25px;
}
```

## Performance Settings

### Optimization Options
```
General Performance:
✓ Lazy Load Images
✓ Lazy Load Iframes
✓ Disable Emojis
✓ Disable Embeds
□ Disable XML-RPC
□ Remove Query Strings
```

### Script Management
```
jQuery Loading:
○ In Header (default)
○ In Footer (faster)
○ Don't Load (if not needed)

Combine Scripts: ✓
Minify CSS: ✓
Minify JavaScript: ✓
```

## Maintenance Mode

### Enable Maintenance
```
Maintenance Mode: ○ Off ○ On
Who Can Access:
✓ Administrators
□ Editors
□ Logged-in Users
```

### Maintenance Page
```
Maintenance Title: "Site Under Maintenance"
Maintenance Message: "We're updating our site. Check back soon!"
Expected Time: "Back online in 2 hours"
Show Contact: ✓
Contact Email: support@example.com
```

## Save Settings

### Publishing Changes

#### Save Draft vs Publish
- **Save Draft:** Preview changes without applying
- **Publish:** Apply changes immediately
- **Schedule:** Set changes to go live later

#### Reset Options
```
Reset Section: Reset only current section
Reset All: Reset all general settings
Restore Defaults: Factory reset
```

## Troubleshooting General Settings

### Changes Not Appearing

**Check These:**
1. Clear browser cache (Ctrl+F5)
2. Clear site cache (plugin/server)
3. Ensure "Publish" not "Save Draft"
4. Check if child theme overriding
5. Verify no CSS conflicts

### Logo Not Showing

**Solutions:**
1. Check image format (PNG/JPG/SVG)
2. Verify file size (<2MB)
3. Clear cache
4. Check logo display settings
5. Inspect for CSS hiding logo

### Layout Breaking

**Common Fixes:**
1. Reset container width to default
2. Check sidebar settings
3. Verify responsive breakpoints
4. Disable conflicting plugins
5. Clear all caches

## Best Practices

### Do's
✅ Test changes in customizer preview
✅ Use appropriate image sizes
✅ Keep consistent spacing
✅ Optimize images before upload
✅ Regular backup before major changes

### Don'ts
❌ Use huge image files
❌ Overuse custom code
❌ Ignore mobile view
❌ Skip testing after changes
❌ Mix multiple layout styles

## Quick Reference

### Recommended Settings by Site Type

| Site Type | Layout | Container | Sidebar | Padding |
|-----------|---------|-----------|----------|----------|
| Blog | Boxed/Wide | 1170px | Right | 60px |
| Portfolio | Wide | 1400px | None | 30px |
| Community | Wide | 1170px | Right | 60px |
| Shop | Wide | 1170px | Left | 40px |
| Corporate | Boxed | 1170px | Right | 60px |

### Performance Impact

| Setting | Performance Impact |
|---------|-------------------|
| Preloader | Slight delay |
| Lazy Loading | Improves speed |
| Sticky Sidebar | Minimal impact |
| Custom Fonts | Can slow loading |
| Background Images | Depends on size |

---

**Need More Help?** Check the related articles on Header Configuration, Footer Settings, and Typography & Colors for complete theme customization.