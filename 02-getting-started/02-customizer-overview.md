# Complete Customizer Options Guide

## Overview

Reign Theme uses the WordPress Customizer powered by the Kirki Framework, providing 200+ customization options organized into logical sections. All changes preview in real-time before publishing.

## Accessing the Customizer

**Methods to Access:**
1. `WordPress Admin → Appearance → Customize`
2. `Admin Bar → Customize` (when viewing site)
3. `Reign Settings → Quick Links → Customizer`

## Customizer Sections Overview

### Main Sections
1. **Site Identity** - Logo, title, favicon
2. **General** - Core theme settings
3. **Colors** - Color schemes and customization
4. **Header** - Header layouts and options
5. **Footer** - Footer configuration
6. **Branded Login & Register** - Login page customization
7. **BuddyPress** - Community settings
8. **WooCommerce** - Shop settings
9. **Blog** - Blog layouts and options
10. **Forms** - Form styling
11. **Additional CSS** - Custom CSS

## 1. Site Identity

### Site Title & Tagline
- **Site Title**: Your website name
- **Tagline**: Brief site description
- **Display Site Title**: Show/Hide toggle
- **Display Tagline**: Show/Hide toggle

### Site Icon
- **Favicon**: 512×512px minimum
- **Format**: PNG recommended
- **Used for**: Browser tab, bookmarks, mobile home screen

## 2. General Settings

### Site Logo
```
General → Site Logo
```

**Logo Options:**
- **Desktop Logo**: Main logo image
- **Mobile Logo**: Smaller mobile version
- **Retina Logo**: 2x resolution for HD displays
- **Logo Max Width**: Pixel or percentage
- **Logo Max Height**: Maintain proportions
- **Logo Alignment**: Left/Center/Right

### Site Layout
```
General → Site Layout
```

**Layout Options:**
1. **Wide Layout** (Default)
   - Full browser width
   - No side margins
   - Modern appearance

2. **Boxed Layout**
   - Fixed max width (1170px)
   - Background visible on sides
   - Classic website look

3. **Framed Layout**
   - Border around entire site
   - Unique visual style
   - Custom frame color

### Typography
```
General → Typography
```
(See Typography Settings documentation for details)

### Page Mapping
```
General → Page Mapping
```

**Assign Special Pages:**
- Login Page
- Register Page
- Terms & Conditions
- Privacy Policy
- 404 Error Page

### Dark Mode
```
General → Dark Mode
```

**Settings:**
- **Enable Dark Mode**: ON/OFF
- **Default Mode**: Light/Dark/Auto
- **Toggle Position**: Header/Fixed/Custom
- **Toggle Style**: Switch/Button/Icon
- **Save Preference**: Remember user choice

### Login Popup
```
General → Login Popup
```

**Configuration:**
- **Enable Popup**: Replace page with modal
- **Trigger**: Menu item/Button class
- **Style**: Modal/Slide/Fade
- **Social Login**: Integration options

### Sub Header
```
General → Sub Header
```

**Options:**
- **Enable Globally**: ON/OFF
- **Layout Style**: 4 styles available
- **Height**: Small/Medium/Large
- **Background**: Color/Image/Gradient
- **Show Elements**: Title/Breadcrumb/Both

### Site Performance
```
General → Site Performance
```

**Optimization:**
- **Smart Performance Mode**: Auto-optimization
- **Lazy Loading**: Images/Iframes/Videos
- **Minification**: CSS/JavaScript
- **Widget Detection**: Disable unused
- **Emoji Support**: Enable/Disable
- **jQuery Migrate**: Enable/Disable

### Custom Code
```
General → Custom Code
```

**Code Sections:**
- **Header Code**: Before `</head>`
- **Body Code**: After `<body>`
- **Footer Code**: Before `</body>`

**Use Cases:**
- Analytics tracking
- Custom meta tags
- Third-party scripts
- Verification codes

## 3. Colors

```
Appearance → Customize → Colors
```

### Color Scheme Selection
**Predefined Schemes:**
- Default
- Clean
- Dark
- Dating
- Ectoplasm
- Sunrise
- Coffee

### Color Customization
(See Color Schemes documentation for all options)

## 4. Header Settings

### Header Layout
```
Header → Header Layout
```

**4 Header Versions:**
1. **Header V1** - Classic horizontal
2. **Header V2** - Centered logo
3. **Header V3** - Logo left, menu right
4. **Header V4** - Logo above menu

### Header General
```
Header → Header General
```

**Settings:**
- **Sticky Header**: Enable/Disable
- **Sticky Animation**: Slide/Fade/None
- **Header Width**: Full/Contained
- **Header Height**: 60px-150px

### Top Bar
```
Header → Top Bar
```

**Configuration:**
- **Enable Top Bar**: ON/OFF
- **Left Content**: Text/Menu/Social
- **Right Content**: Text/Menu/Login
- **Mobile Display**: Show/Hide

### Main Header
```
Header → Main Header
```

**Options:**
- **Background**: Color/Image/Transparent
- **Menu Alignment**: Left/Center/Right
- **Menu Style**: Default/Button/Underline
- **Search Icon**: Show/Hide
- **Cart Icon**: Show/Hide (WooCommerce)
- **Notification Icon**: Show/Hide (BuddyPress)

### Mobile Header
```
Header → Mobile Header
```

**Mobile Settings:**
- **Breakpoint**: When mobile kicks in
- **Mobile Logo**: Different from desktop
- **Menu Style**: Hamburger/Text/Both
- **Menu Position**: Left/Right
- **Sticky Mobile**: Enable/Disable

### Header Layouts Detail

#### Header V1 Features
- Traditional layout
- Logo left
- Menu center/right
- All elements inline

#### Header V2 Features
- Centered design
- Logo center top
- Menu below logo
- Symmetrical layout

#### Header V3 Features
- Modern minimal
- Logo far left
- Menu far right
- Clean appearance

#### Header V4 Features
- Stacked layout
- Large logo area
- Full-width menu
- Professional look

## 5. Footer Settings

### Footer Layout
```
Footer → Footer Layout
```

**Layout Options:**
- **Columns**: 1-4 columns
- **Column Widths**: Equal/Custom
- **Widget Areas**: Assign widgets

### Footer Widgets
```
Footer → Footer Widgets
```

**Configuration:**
- **Enable Widgets Area**: ON/OFF
- **Background**: Color/Image/Gradient
- **Padding**: Top/Bottom
- **Widget Spacing**: Adjust gaps

### Footer Copyright
```
Footer → Footer Copyright
```

**Settings:**
- **Copyright Text**: Custom text
- **Show Year**: Auto-update year
- **Layout**: Left/Center/Right/Two Column
- **Social Icons**: Show/Hide
- **Back to Top**: Enable/Disable

### Footer Menu
```
Footer → Footer Menu
```

**Options:**
- **Enable Footer Menu**: ON/OFF
- **Menu Selection**: Choose menu
- **Alignment**: Left/Center/Right
- **Separator**: |, /, •, none

## 6. Blog Settings

### Blog Layout
```
Blog → Blog Layout
```

**Layout Options:**
1. **Standard** - Traditional blog
2. **Grid** - 2-4 columns
3. **Masonry** - Pinterest style
4. **List** - Compact view
5. **Timeline** - Chronological

### Blog Elements
```
Blog → Blog Elements
```

**Show/Hide Elements:**
- Featured Image
- Post Title
- Post Meta (author, date, category)
- Post Excerpt
- Read More Button
- Post Tags
- Share Buttons
- Author Bio
- Related Posts
- Comments

### Single Post
```
Blog → Single Post
```

**Single Post Options:**
- **Layout**: Sidebar/Full width
- **Featured Image**: Show/Hide/Banner
- **Meta Position**: Above/Below title
- **Share Position**: Top/Bottom/Float
- **Navigation**: Previous/Next posts
- **Related Posts**: Number and layout

### Archive Pages
```
Blog → Archive Pages
```

**Archive Settings:**
- **Layout**: Same as blog or custom
- **Posts Per Page**: Override default
- **Pagination**: Numbers/Load More/Infinite
- **Category Description**: Show/Hide
- **Author Bio**: Show/Hide

## 7. BuddyPress Settings

### Members
```
BuddyPress → Members
```

**Member Directory:**
- **Layout**: Grid/List
- **Members Per Page**: 12-50
- **Default Order**: Active/Newest/Alphabetical
- **Show Filters**: Yes/No

### Groups
```
BuddyPress → Groups
```

**Group Settings:**
- **Layout**: Grid/List
- **Cover Image**: Enable/Disable
- **Group Types**: Show/Hide
- **Creation Steps**: Customize

### Activity
```
BuddyPress → Activity
```

**Activity Stream:**
- **Layout**: Standard/Timeline
- **Load More**: Button/Infinite
- **Commenting**: Enable/Disable
- **Favorites**: Show/Hide

### Profiles
```
BuddyPress → Profiles
```

**Profile Options:**
- **Cover Image Size**: Height setting
- **Avatar Style**: Square/Round
- **Tab Order**: Rearrange
- **Default Tab**: Activity/Profile/Friends

## 8. WooCommerce Settings

### Shop Page
```
WooCommerce → Shop Page
```

**Shop Layout:**
- **Products Per Row**: 2-6
- **Products Per Page**: 9-30
- **Sidebar**: Left/Right/None
- **Filters**: Top/Sidebar/Off-canvas

### Product Page
```
WooCommerce → Product Page
```

**Single Product:**
- **Gallery Style**: Default/Slider/Grid
- **Zoom**: Enable/Disable
- **Related Products**: Number to show
- **Tabs**: Show/Hide/Accordion

### Cart & Checkout
```
WooCommerce → Cart & Checkout
```

**Checkout Options:**
- **Layout**: One page/Multi-step
- **Fields**: Required/Optional
- **Coupons**: Show/Hide
- **Order Notes**: Enable/Disable

## 9. Forms Settings

### Form Styling
```
Forms → Form Styling
```

**Global Form Styles:**
- **Input Style**: Default/Modern/Classic
- **Border Radius**: 0-30px
- **Border Width**: 0-5px
- **Focus Effect**: Glow/Border/Shadow

### Contact Forms
```
Forms → Contact Forms
```

**Integration with:**
- Contact Form 7
- WPForms
- Gravity Forms
- Ninja Forms

## 10. Additional CSS

### Custom CSS
```
Additional CSS
```

**Features:**
- Syntax highlighting
- Error checking
- Live preview
- CSS variables support
- Media queries

**Example:**
```css
/* Your custom CSS */
.custom-class {
    property: value;
}

@media (max-width: 768px) {
    /* Mobile styles */
}
```

## Import/Export Settings

### Export Customizer Settings

1. Install Customizer Export/Import plugin
2. `Customizer → Export/Import`
3. Click "Export"
4. Save .dat file

### Import Settings

1. `Customizer → Export/Import`
2. Choose .dat file
3. Click "Import"
4. Preview changes
5. Publish

## Customizer Tips

### Best Practices

1. **Preview First**
   - Make changes
   - Preview thoroughly
   - Test responsive
   - Then publish

2. **Backup Settings**
   - Export before major changes
   - Save configurations
   - Document changes

3. **Performance**
   - Don't overuse custom CSS
   - Optimize images
   - Limit font variations

4. **Organization**
   - Work section by section
   - Keep notes
   - Test incrementally

### Keyboard Shortcuts

- `Shift + Click`: Open links in preview
- `Escape`: Close open panels
- `Tab`: Navigate fields

### Troubleshooting

**Customizer Won't Load:**
- Increase PHP memory
- Disable plugins
- Clear browser cache
- Check JavaScript errors

**Changes Not Saving:**
- Check permissions
- Increase max_input_vars
- Clear server cache
- Check ModSecurity

**Preview Not Updating:**
- Hard refresh (Ctrl+F5)
- Clear browser cache
- Check for JS errors
- Disable cache plugins

## Device Preview

### Responsive Testing

**Preview Modes:**
- Desktop (default)
- Tablet (portrait/landscape)
- Mobile (portrait/landscape)

**Testing Features:**
- Real dimensions
- Touch simulation
- Orientation change
- Menu behavior

---

*Master your site's appearance with Reign's comprehensive Customizer options!*