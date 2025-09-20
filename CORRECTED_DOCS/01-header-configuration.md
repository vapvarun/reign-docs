# Header Configuration - Complete Guide

## Overview
Reign theme provides 4 header layout versions plus mobile header options to create the perfect navigation experience for your site.

## Accessing Header Settings

### Location
```
Dashboard → Appearance → Customize → Header
```

Or via Reign Settings:
```
Dashboard → Appearance → Reign Settings → Getting Started
```

## Header Layout Versions

### Header Version 1 (Default)
**Description:** Logo center with menu below
- **Best for:** Classic websites, blogs
- **Features:**
  - Centered logo
  - Full-width menu below
  - Optional topbar
  - Sticky header support

### Header Version 2
**Description:** Logo left, menu right
- **Best for:** Business sites, standard layouts
- **Features:**
  - Logo on left side
  - Menu aligned right
  - User menu integration
  - Search option

### Header Version 3
**Description:** Logo and menu in line
- **Best for:** Modern sites, minimal design
- **Features:**
  - Inline layout
  - Compact design
  - Space-efficient
  - Mobile-friendly

### Header Version 4
**Description:** Logo right, menu left
- **Best for:** Unique layouts, RTL sites
- **Features:**
  - Reversed layout
  - Menu on left
  - Logo on right
  - Different visual flow

## Header Components

### 1. Top Bar Configuration
**Location:** Customize → Header → Top Bar

**Options:**
- Enable/Disable topbar
- Add social links
- Contact information
- Custom HTML/Text
- Background color
- Text color

**Example Setup:**
```
Email: info@site.com | Phone: +1234567890 | [Social Icons]
```

### 2. Main Header Settings

#### Logo Configuration
**Location:** Customize → General → Site Identity

**Logo Options:**
- **Regular Logo:** Main site logo
- **Mobile Logo:** Smaller version for mobile devices
- **Sticky Header Logo:** Appears when scrolling

**Recommended Sizes:**
- Desktop Logo: 200px × 50px
- Mobile Logo: 150px × 40px
- Sticky Logo: 180px × 35px

#### Sticky Header
**Location:** Customize → Header → Sticky Header

**Settings:**
```
Enable Sticky Header: Yes/No
Sticky Header Style: Same as main / Custom
Custom Background Color: [Color picker]
Custom Logo: [Upload option]
Sticky Header Height: [Pixels]
Shadow Effect: Yes/No
```

### 3. Mobile Header

#### Mobile Menu Style
**Location:** Customize → Header → Mobile Header

**Options:**
- **Hamburger Icon Style:**
  - 3 Lines (Classic)
  - 3 Dots
  - Custom Icon

- **Menu Animation:**
  - Slide from left
  - Slide from right
  - Dropdown
  - Full screen overlay

- **Mobile Menu Background:**
  - Color options
  - Transparency settings
  - Blur background

### 4. Header Menu Configuration

#### Menu Font Style & Color
**Location:** Customize → General → Typography → Header Main Menu

**Typography Settings:**
- Font Family (Google Fonts)
- Font Size (px/em/rem)
- Font Weight (300-900)
- Text Transform (None/Uppercase/Lowercase/Capitalize)
- Letter Spacing
- Line Height

**Color Settings:**
- Menu Text Color
- Menu Hover Color
- Active Menu Color
- Submenu Background
- Submenu Text Color

## BuddyPress Header Integration

### BuddyPress Header Icons
**Location:** Dashboard → Reign Settings → BuddyPress → Header Icons

**Available Icons:**
- Notifications bubble
- Messages count
- Friend requests
- Profile dropdown
- Activity updates

**Configuration:**
```
Show Notifications: Yes/No
Show Messages: Yes/No
Show Friend Requests: Yes/No
Icon Style: Default/Custom
Count Display: Number/Dot
```

### User Menu in Header
**When Logged In:**
- Profile avatar
- Dropdown with:
  - My Profile
  - Activity
  - Messages
  - Settings
  - Logout

**When Logged Out:**
- Login button
- Register button
- Or popup modal

## Header Transparency Options

### Transparent Header Setup
**Use Cases:**
- Hero sections
- Landing pages
- Full-screen images

**Settings:**
```
Enable Transparent Header: Yes/No
Apply to: All pages / Specific pages
Background on Scroll: Color/Gradient
Text Color: Light/Dark
```

## Search in Header

### Search Bar Options
**Location:** Customize → Header → Search

**Settings:**
- **Search Style:**
  - Icon only (expands on click)
  - Search bar visible
  - Modal popup

- **Search Scope:**
  - All content
  - Posts only
  - Products only
  - Members only
  - Groups only

## Header for Different Pages

### Page-Specific Headers
You can set different header styles for:
- Homepage
- Blog pages
- Shop pages
- BuddyPress pages
- Single posts
- Archive pages

**How to Set:**
1. Edit the specific page
2. Look for "Header Settings" meta box
3. Choose header version
4. Save changes

## Responsive Behavior

### Breakpoints
```
Desktop: > 1024px - Full header
Tablet: 768-1024px - Simplified header
Mobile: < 768px - Mobile menu
```

### Mobile-Specific Settings
- Hide/show elements
- Adjust logo size
- Change menu style
- Modify spacing

## Common Header Customizations

### Adding Custom HTML to Header
```php
// Add to child theme functions.php
add_action('reign_header_top', function() {
    echo '<div class="custom-header-text">Welcome!</div>';
});
```

### Custom Header CSS
```css
/* Add to Customize → Additional CSS */
.reign-header {
    background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
}
.main-navigation a {
    color: #ffffff !important;
}
```

## Troubleshooting Header Issues

### Header Not Sticky
**Check:**
1. Sticky header enabled in Customizer
2. No JavaScript errors
3. Clear cache
4. Check theme version

### Logo Not Showing
**Solutions:**
1. Check file format (PNG/JPG/SVG)
2. Verify file size < 2MB
3. Clear browser cache
4. Check logo display settings

### Menu Not Responsive
**Fixes:**
1. Check mobile menu settings
2. Verify menu assignment
3. Clear cache
4. Check for plugin conflicts

### Header Overlapping Content
**Solutions:**
```css
/* Add padding to content */
.site-content {
    padding-top: 100px; /* Adjust based on header height */
}
```

## Best Practices

### Do's
✅ Test all header versions before choosing
✅ Optimize logo images for web
✅ Keep menu items concise
✅ Test on multiple devices
✅ Use sticky header for better UX

### Don'ts
❌ Overcrowd header with too many elements
❌ Use very large logos
❌ Create too many menu levels
❌ Ignore mobile experience
❌ Forget to test sticky behavior

## Related Settings
- Menu Configuration
- Typography Settings
- Color Schemes
- Mobile Menu
- User Account Menu

---

**Need Help?** Check the video tutorial on header customization or contact support for specific header layout questions.