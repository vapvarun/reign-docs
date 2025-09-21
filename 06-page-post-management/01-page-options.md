# Page Options & Settings

## Overview

Reign Theme provides extensive page-level customization options through both the WordPress Customizer and individual page settings, allowing you to create unique layouts for different pages.

## Page Mapping

### Essential Page Assignments

Navigate to:
```
Customizer → General → Page Mapping
```

**BuddyPress Pages:**
- Members Directory Page
- Groups Directory Page
- Activity Stream Page
- Register Page
- Activation Page

**WooCommerce Pages:**
- Shop Page
- Cart Page
- Checkout Page
- My Account Page

**Custom Pages:**
- Login Page (custom)
- 404 Error Page
- Search Results Page
- Terms & Conditions
- Privacy Policy

### Setting Page Mappings

1. Go to Page Mapping section
2. Select page from dropdown
3. Create new page if needed
4. Save and publish

## Individual Page Options

### Page Attributes

When editing any page:
```
Page Editor → Page Attributes (sidebar)
```

**Template Options:**
- Default Template
- Full Width
- Full Width - Stretched
- Left Sidebar
- Right Sidebar
- Both Sidebars
- Blank Canvas (no header/footer)

### Reign Page Settings Metabox

Located below page editor:

**Layout Settings:**

1. **Site Layout Override**
   - Default (use global)
   - Wide Layout
   - Boxed Layout

2. **Content Layout**
   - Full Width
   - Contained (1170px)
   - Narrow (960px)

3. **Sidebar Options**
   - No Sidebar
   - Left Sidebar
   - Right Sidebar
   - Both Sidebars

4. **Sidebar Selection**
   - Default Sidebar
   - Custom Sidebar (if created)
   - WooCommerce Sidebar
   - BuddyPress Sidebar

## Header Options Per Page

### Page-Specific Header Settings

**Header Display:**
- Show/Hide Header
- Transparent Header
- Sticky Header Override
- Custom Header Layout (v1-v4)

**Header Elements:**
- Show/Hide Logo
- Show/Hide Navigation
- Show/Hide Search
- Show/Hide Social Icons
- Show/Hide User Menu

**Custom Header Background:**
- Background Color
- Background Image
- Overlay Opacity
- Parallax Effect

## Sub-Header/Title Bar Options

### Sub-Header Settings

**Display Options:**
- Show/Hide Sub-header
- Layout Style (1-4 styles)
- Background Type (Color/Image/Gradient)
- Height (Small/Medium/Large/Custom)

**Title Options:**
- Show/Hide Page Title
- Custom Title Text
- Title Alignment (Left/Center/Right)
- Title Color
- Title Size

**Breadcrumb Options:**
- Show/Hide Breadcrumbs
- Breadcrumb Position
- Breadcrumb Separator
- Home Text

**Background Customization:**
- Background Color
- Background Image
- Overlay Color
- Overlay Opacity
- Parallax Scrolling

## Footer Options Per Page

### Page-Specific Footer Settings

**Footer Display:**
- Show/Hide Footer
- Show/Hide Widget Area
- Show/Hide Copyright
- Custom Footer Layout

**Footer Widgets:**
- Number of Columns (1-4)
- Custom Widget Area
- Background Override

## Content Options

### Content Width Settings

**Width Options:**
- Default (from Customizer)
- Full Width
- Wide (1400px)
- Normal (1170px)
- Narrow (960px)
- Custom (px or %)

### Padding & Margins

**Content Padding:**
- Top Padding: 0-200px
- Bottom Padding: 0-200px
- Remove All Padding (toggle)

**Content Margins:**
- Top Margin: -200px to 200px
- Bottom Margin: 0-200px

## Page Background Options

### Background Settings

**Background Type:**
1. **Solid Color**
   - Color Picker
   - Opacity Control

2. **Gradient**
   - Two Color Stops
   - Gradient Direction
   - Gradient Type (Linear/Radial)

3. **Image**
   - Upload Image
   - Position
   - Size (Cover/Contain/Auto)
   - Repeat Options
   - Attachment (Fixed/Scroll)

4. **Video**
   - YouTube/Vimeo URL
   - MP4 Upload
   - Autoplay Options
   - Mute Setting

## Special Page Types

### Homepage Options

**When Set as Homepage:**
- Remove Title Automatically
- Special Homepage Sections
- Slider Integration
- Widget Areas

**Homepage Sections:**
- Hero Section
- Featured Content
- Recent Posts
- Call to Action
- Testimonials

### Blog Page Options

**Blog Layout:**
- Grid (2-4 columns)
- List
- Masonry
- Timeline

**Post Elements:**
- Show/Hide Featured Image
- Show/Hide Meta
- Show/Hide Excerpt
- Excerpt Length
- Read More Text

### Shop Page Options

**WooCommerce Specific:**
- Products Per Page
- Column Count (2-6)
- Show/Hide Sidebar
- Show/Hide Filters
- Product Display Type

### Landing Page Options

**Landing Page Features:**
- Hide Header/Footer
- Full Screen Sections
- Custom Scripts
- Conversion Tracking
- A/B Testing Support

## Mobile-Specific Options

### Responsive Settings

**Mobile Layout:**
- Force Full Width on Mobile
- Hide Elements on Mobile
- Mobile-Specific Sidebar
- Touch Gestures

**Mobile Header:**
- Sticky on Mobile (toggle)
- Simplified Navigation
- Mobile Logo Override

**Mobile Footer:**
- Simplified Footer
- Mobile-Only Widgets
- Click to Call Button

## SEO Page Options

### SEO Settings

**Meta Options:**
- Custom Meta Title
- Meta Description
- Meta Keywords
- Robots Meta (index/noindex)
- Canonical URL

**Social Media:**
- OG Title
- OG Description
- OG Image
- Twitter Card Type

## Advanced Page Options

### Custom CSS/JS

**Page-Specific Code:**
```
Page Editor → Custom CSS/JS (metabox)
```

**Custom CSS:**
```css
/* This CSS only applies to this page */
.page-id-123 .custom-element {
    /* styles */
}
```

**Custom JavaScript:**
```javascript
// This JS only runs on this page
jQuery(document).ready(function($) {
    // Custom code
});
```

### Page Classes

**Add Body Classes:**
- Custom class names
- Applied to body tag
- For styling hooks

**Example:**
```php
// Added classes appear as:
<body class="custom-class-1 custom-class-2">
```

## Page Performance Options

### Optimization Settings

**Asset Loading:**
- Disable Unnecessary Scripts
- Disable Unnecessary Styles
- Lazy Load Images
- Preload Critical Assets

**Cache Settings:**
- Cache This Page
- Cache Duration
- Exclude from Cache
- Clear Cache on Update

## Page Restrictions

### Access Control

**Visibility Options:**
- Public
- Private (logged-in users)
- Password Protected
- Members Only
- Specific User Roles

**Membership Restrictions:**
- Membership Level Required
- Redirect URL for Non-Members
- Custom Message

## Page Builder Integration

### Elementor Options
- Elementor Canvas
- Elementor Full Width
- Hide Title Toggle
- Container Width

### Gutenberg Options
- Wide Alignment Support
- Full Width Blocks
- Block Spacing
- Color Palette

### Other Builders
- Beaver Builder Support
- Divi Integration
- Visual Composer
- Oxygen Builder

## Conditional Display

### Display Rules

**Show/Hide Based On:**
- User Login Status
- User Role
- Device Type
- Date/Time
- URL Parameters
- Referrer

**Example Rules:**
```
IF user_logged_in AND user_role = 'subscriber'
    THEN show_custom_content
ELSE show_default_content
```

## Page Revisions

### Revision Settings

**Tracking Changes:**
- Auto-save Intervals
- Revision History
- Compare Revisions
- Restore Previous Version

**Revision Management:**
- Limit Number of Revisions
- Clear Old Revisions
- Revision Authors
- Change Notes

## Bulk Page Options

### Bulk Edit Features

**Apply to Multiple Pages:**
1. Select pages in Pages list
2. Choose Bulk Actions → Edit
3. Apply settings:
   - Template
   - Parent Page
   - Status
   - Author

## Page Duplication

### Duplicate Page Options

**Clone Settings:**
- Duplicate Content
- Duplicate Settings
- Duplicate Metadata
- Create as Draft

**Use Cases:**
- A/B Testing
- Similar Page Layouts
- Template Creation
- Backup Purposes

## Best Practices

### Page Organization

1. **Logical Hierarchy**
   - Parent/Child relationships
   - Clear URL structure
   - Consistent naming

2. **Template Usage**
   - Create reusable templates
   - Consistent layouts
   - Template organization

3. **Performance**
   - Optimize images
   - Minimize custom code
   - Use caching wisely

4. **Mobile First**
   - Test all options on mobile
   - Responsive images
   - Touch-friendly elements

## Troubleshooting

### Common Issues

**Settings Not Applying:**
- Check template hierarchy
- Clear cache
- Check for conflicts
- Verify user permissions

**Layout Breaking:**
- Check sidebar settings
- Verify content width
- Inspect custom CSS
- Disable plugins

**Mobile Issues:**
- Check responsive settings
- Test real devices
- Verify viewport meta
- Check media queries

---

*Unlock the full potential of your pages with Reign's comprehensive page options!*