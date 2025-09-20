# Essential Settings Tour - Your Complete Guide

## Welcome to Your Reign Theme Dashboard

After installing Reign, you have two main control centers for customizing your site. This tour will help you understand where everything is and what each setting does.

## The Two Control Centers

### 1. WordPress Customizer
**Access:** Appearance → Customize
- Live preview of changes
- Visual editing interface
- Instant updates
- Mobile/tablet preview

### 2. Reign Settings Panel
**Access:** Appearance → Reign Settings
- Advanced configurations
- Plugin integrations
- Performance settings
- License management

## Quick Navigation Map

```
Your WordPress Admin
├── Appearance
│   ├── Customize (Visual Settings)
│   │   ├── General
│   │   ├── Header
│   │   ├── Footer
│   │   ├── Colors
│   │   └── [More Options]
│   └── Reign Settings (Advanced)
│       ├── Getting Started
│       ├── BuddyPress Options
│       └── Support
└── Settings
    └── [Various Plugin Settings]
```

## Part 1: WordPress Customizer Tour

### Accessing the Customizer

1. **Method 1: Admin Bar**
   - Look at top of your site (when logged in)
   - Click "Customize"

2. **Method 2: Dashboard**
   - Go to Appearance → Customize

3. **Method 3: Quick Edit**
   - Hover over any element with edit icon
   - Click to jump to that setting

### General Settings Section

**Location:** Customize → General

#### Site Identity
**What You'll Find:**
- **Logo Upload** - Your brand image
  - Desktop logo (recommended: 200x50px)
  - Mobile logo (different size for phones)
  - Sticky header logo (shows when scrolling)
- **Site Icon** - Browser tab icon (favicon)
- **Site Title** - Your website name
- **Tagline** - Brief site description

**Real Example:**
If you run "FitLife Community":
- Logo: Your FitLife logo
- Title: "FitLife Community"
- Tagline: "Your Journey to Wellness Starts Here"

#### Site Layout
**What You'll Find:**
- **Layout Style**
  - Wide (full width)
  - Boxed (contained with background)
- **Container Width** - How wide your content appears
  - Default: 1170px
  - Can adjust for wider screens
- **Sidebar Position**
  - Right sidebar (most common)
  - Left sidebar
  - No sidebar (full width content)

**When to Use What:**
- **Wide Layout**: Modern, spacious feel
- **Boxed Layout**: Classic, focused content
- **No Sidebar**: Landing pages, full focus

### Header Configuration

**Location:** Customize → Header

#### Header Styles (7 Options)

**Style 1: Default**
- Logo left, menu right
- Best for: Standard websites
- User loves: Familiar layout

**Style 2: Centered**
- Logo center, menu below
- Best for: Elegant brands
- User loves: Symmetrical design

**Style 3: Logo Middle**
- Menu splits around logo
- Best for: Unique branding
- User loves: Distinctive look

**Style 4: Transparent**
- Header over hero image
- Best for: Visual impact
- User loves: Modern aesthetic

**Style 5: Left Align**
- Everything aligned left
- Best for: Minimalist sites
- User loves: Clean simplicity

**Style 6: Right Align**
- Everything aligned right
- Best for: RTL languages
- User loves: Alternative layout

**Style 7: Sticky Only**
- Header appears on scroll
- Best for: Content focus
- User loves: More screen space

#### Sticky Header Options

**Enable Sticky Header**
- Header follows as you scroll
- Keeps navigation accessible
- Can have different logo size

**Sticky Header Settings:**
- Background color (can differ from main)
- Logo size adjustment
- Shadow effect
- Transparency options

### Footer Customization

**Location:** Customize → Footer

#### Footer Widget Areas

**Widget Columns:**
- **1 Column** - Single centered area
- **2 Columns** - Two equal sections
- **3 Columns** - Three sections (popular)
- **4 Columns** - Maximum sections

**What to Put in Each:**
- Column 1: About text/logo
- Column 2: Quick links
- Column 3: Contact info
- Column 4: Newsletter signup

#### Copyright Section

**Available Variables:**
- `{site_title}` - Your site name
- `{year}` - Current year (auto-updates)
- `{theme_author}` - Theme credit

**Example:**
```
© {year} {site_title}. All rights reserved. | Privacy | Terms
```
Shows as: © 2024 FitLife Community. All rights reserved. | Privacy | Terms

### Color Settings

**Location:** Customize → Colors

#### Primary Color Scheme

**Main Colors:**
- **Primary Color** - Main brand color
  - Used for: Buttons, links, accents
  - Example: Your brand blue #0073e6

- **Secondary Color** - Supporting color
  - Used for: Hover states, highlights
  - Example: Darker blue #0056b3

- **Text Color** - Main content
  - Default: Dark gray #333333
  - For readability

- **Background Color** - Page background
  - Default: White #ffffff
  - Can use light gray for depth

#### Dark Mode (If Enabled)

**Auto-Switch Options:**
- Time-based (night/day)
- User preference
- System setting follow

**Dark Mode Colors:**
- Background: Dark gray/black
- Text: Light gray/white
- Accents: Adjusted for contrast

### Typography Settings

**Location:** Customize → Typography

#### Font Families

**Heading Font:**
- Choose from 800+ Google Fonts
- Or use system fonts (faster)
- Affects all titles (H1-H6)

**Body Font:**
- For paragraphs and content
- Prioritize readability
- Popular: Open Sans, Roboto, Lato

#### Font Sizes

**Desktop Sizes:**
- H1: 36px (main titles)
- H2: 30px (section heads)
- H3: 24px (subsections)
- Body: 16px (content)

**Mobile Adjustments:**
- Automatically scales down
- Can customize separately
- Maintains readability

## Part 2: Reign Settings Panel

### Getting Started Tab

**Location:** Appearance → Reign Settings → Getting Started

**Quick Links Section:**
- One-click access to common tasks
- Import demos
- Documentation links
- Video tutorials

**System Status:**
- ✅ Green = Good
- 🟡 Yellow = Could improve
- 🔴 Red = Needs attention

### BuddyPress Configuration

**Location:** Appearance → Reign Settings → BuddyPress

#### Activity Settings

**Activity Layout:**
- **Classic** - Traditional timeline
- **Masonry** - Pinterest style
- **Grid** - Organized boxes

**Activity Filters:**
- Show/hide activity types
- Default filter selection
- Auto-refresh interval

#### Member Directory

**Display Options:**
- **Grid View** - Photo cards
- **List View** - Detailed rows
- Members per page (12, 24, 36)
- Default sort order

**Member Card Shows:**
- Avatar/cover image
- Name and username
- Last active time
- Friend/follow button
- Message button

#### Groups Directory

**Group Display:**
- Layout style (grid/list)
- Information shown
- Join button placement
- Member count display

### WooCommerce Settings

**Location:** When WooCommerce is active

#### Shop Page

**Products Display:**
- Columns (3, 4, 5)
- Products per page
- Sidebar position
- Quick view enabled

**Product Cards Show:**
- Image
- Title
- Price
- Rating
- Add to cart button

#### Single Product

**Layout Options:**
- Image position
- Gallery style
- Related products count
- Review display

## Part 3: Essential Plugin Settings

### Required: Kirki Framework

**What It Does:**
- Powers the customizer
- No configuration needed
- Auto-activates with theme

### Recommended: BuddyPress

**First-Time Setup:**
1. **Components**
   - Go to Settings → BuddyPress
   - Enable needed components:
     - ✅ Activity Streams
     - ✅ Members
     - ✅ Groups
     - ✅ Private Messages

2. **Pages**
   - BuddyPress creates pages automatically
   - Assign pages for:
     - Members directory
     - Groups directory
     - Activity stream
     - Register page

3. **Settings**
   - Registration: Open/Closed
   - Avatar uploads: Enable
   - Cover images: Enable
   - Friend connections: Enable

### Optional: WooCommerce

**Initial Configuration:**
1. Run setup wizard
2. Set currency and location
3. Configure payment methods
4. Set up shipping zones
5. Add sample products

## Common Setting Combinations

### For a Social Community

**Essential Settings:**
```
Header: Style 2 (Centered)
Layout: Wide
Sidebar: Right
BuddyPress: All components
Registration: Open
Activity: Grid layout
```

### For an Online Store

**Essential Settings:**
```
Header: Style 1 (Classic)
WooCommerce: Enabled
Shop Columns: 4
Sidebar: Left (for filters)
Quick View: Enabled
```

### For a Learning Platform

**Essential Settings:**
```
Header: Style 4 (Transparent)
Layout: Boxed
Sidebar: None (focus on content)
LearnDash: Integrated
Progress Bar: Visible
```

### For a Business Site

**Essential Settings:**
```
Header: Style 3 (Logo middle)
Footer: 4 columns
Colors: Brand matched
Typography: Professional fonts
Contact forms: Enabled
```

## Mobile-Specific Settings

### Responsive Controls

**Breakpoints:**
- Desktop: 1024px and up
- Tablet: 768px to 1023px
- Mobile: Below 768px

**Mobile Menu:**
- Hamburger icon style
- Slide direction (left/right)
- Background color
- Close on click outside

**Mobile Logo:**
- Separate smaller logo
- Centered or left aligned
- Size adjustment

## Performance Settings

### Speed Optimization

**Location:** Reign Settings → Performance

**Lazy Loading:**
- Images load as needed
- Reduces initial load time
- Enable for: Images, videos, iframes

**Minification:**
- CSS compression
- JavaScript compression
- HTML optimization

**Disable Unused Features:**
- Emoji scripts (if not needed)
- Embed scripts
- Dashboard widgets

## Setting Priority Guide

### Day 1: Must Configure
1. ✅ Upload logo
2. ✅ Set site title/tagline
3. ✅ Choose header style
4. ✅ Set primary colors
5. ✅ Configure menus

### Week 1: Should Configure
1. 📝 Footer content
2. 📝 Typography settings
3. 📝 Sidebar preferences
4. 📝 Widget areas
5. 📝 Social links

### Month 1: Nice to Have
1. 💡 Performance tweaks
2. 💡 Advanced colors
3. 💡 Custom CSS
4. 💡 Third-party integrations
5. 💡 SEO optimization

## Troubleshooting Settings

### Changes Not Showing?

1. **Clear Cache**
   - Browser cache (Ctrl+F5)
   - Plugin cache (if using)
   - CDN cache (if using)

2. **Check Publish Status**
   - Click "Publish" in customizer
   - Not just "Save Draft"

3. **Verify Setting Location**
   - Some settings in customizer
   - Others in Reign Settings
   - Plugin settings separate

### Setting Grayed Out?

**Possible Reasons:**
- Required plugin not active
- Conflicting setting elsewhere
- License not activated
- PHP version too low

### Can't Find a Setting?

**Search Strategies:**
1. Use customizer search box
2. Check Reign Settings panel
3. Look in plugin settings
4. Consult documentation
5. Ask support

## Pro Tips for Settings

### Speed Up Customization
- Use keyboard shortcuts
- Shift+Click for new tab
- Drag to reorder sections

### Test Before Publishing
- Use preview button
- Check mobile view
- Test different pages
- Verify in incognito mode

### Backup Settings
- Export customizer settings
- Save before major changes
- Document custom CSS
- Screenshot configurations

## Getting Help

### Built-in Help
- Hover over (?) icons
- Read setting descriptions
- Check tooltips

### External Resources
- Documentation site
- Video tutorials
- Community forum
- Support tickets

---

**Settings Configured?** Excellent! Your site is now personalized. Next, explore specific features or start adding content to bring your community to life!