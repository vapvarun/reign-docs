# Reign Settings Panel - Complete Guide

## Overview
The Reign Settings panel is your central hub for theme configuration, located separately from the WordPress Customizer for advanced options and integrations.

## Accessing Reign Settings

### Location
```
WordPress Dashboard → Appearance → Reign Settings
```

Or after theme activation:
```
Admin Bar → Reign → Settings
```

## Main Settings Tabs

### 1. Getting Started Tab

#### Quick Links Section
Access commonly used settings quickly:
- **Customizer Shortcuts:**
  - General Settings
  - Header Options
  - Footer Options
  - Colors & Typography
  - BuddyPress Settings
  - WooCommerce Settings

#### System Status
Check your site's compatibility:
- PHP Version (Required: 7.4+)
- Memory Limit (Recommended: 256MB)
- Max Execution Time
- Upload Max Size
- Active Plugins
- Theme Version

#### Demo Import
**One-Click Demo Import:**
1. Choose demo style
2. Select import options:
   - ☑ Content
   - ☑ Widgets
   - ☑ Customizer Settings
   - ☑ Menus
3. Click "Import Demo"

**Note:** Demo import is for fresh installations only, not for existing sites or multisite.

### 2. License Tab

#### License Activation
**Purpose:**
- Enable automatic updates
- Access premium support
- View changelog
- Download add-ons

**Activation Process:**
```
1. Enter Purchase Code
2. Click "Activate License"
3. Green checkmark = Success
```

**License Valid For:**
- Single site installation
- Staging site (same domain)
- Development site (localhost)

### 3. BuddyPress Extender Tab

#### Community Settings
**Location:** Reign Settings → BuddyPress Extender → Community Settings

##### BP Layout Management
**Header Position Options:**
- **In the Group Cover Image:** Header inside cover
- **Below the Group Cover Image:** Traditional layout
- **Above the Group Cover Image:** Header on top

**Navigation Style:**
- Horizontal tabs
- Vertical menu
- Dropdown on mobile

##### Activity Settings
**Activity Layout:**
- **Classic:** Timeline style
- **Masonry:** Pinterest-like grid
- **Grid:** Structured boxes

**Activity Options:**
- Enable/disable activity types
- Default activity filter
- Posting permissions
- Character limit
- Media uploads (with RTMedia)

##### Members Directory
**Display Options:**
- **Layout:** Grid / List
- **Members per row:** 3 / 4 / 5
- **Default order:** Active / Newest / Alphabetical
- **Show:** Last active time, member type, cover image

##### Groups Directory
**Group Settings:**
- **Layout:** Grid / List
- **Groups per page:** 20 / 40 / 60
- **Show:** Member count, group type, activity
- **Default tab:** Newest / Active / Popular

#### Social Links Configuration
**Available Networks:**
- Facebook
- Twitter/X
- Instagram
- LinkedIn
- YouTube
- TikTok
- Custom URLs

**Display Locations:**
- Header topbar
- Footer
- User profiles
- Author box

### 4. PeepSo Extender Tab (If PeepSo Active)

#### PeepSo Integration Settings
- Profile layout options
- Activity stream configuration
- Notification settings
- Privacy controls
- Social login setup

### 5. Support Tab

#### Documentation Links
Quick access to:
- Theme documentation
- Video tutorials
- Changelog
- Support ticket system

#### Recommended Plugins
Tested and compatible plugins:
- **Essential:**
  - Kirki Framework
  - BuddyPress/BuddyBoss
  - bbPress

- **Optional:**
  - RTMedia
  - WooCommerce
  - LearnDash
  - Elementor

#### Theme Info
- Current version
- License status
- Support expiration
- Update available

## Configuration Sections

### Site Layout Settings

#### Container Width
```
Default: 1170px
Options: 960px / 1170px / 1400px / Custom
Applies to: Main content area
```

#### Sidebar Configuration
```
Position: Left / Right / No Sidebar
Width: 25% / 30% / 35%
Sticky: Enable / Disable
Mobile: Hide / Show below content
```

### Typography Management

#### Global Font Settings
**Body Font:**
- Font Family (600+ Google Fonts)
- Font Size (14-18px recommended)
- Line Height (1.5-1.8)
- Font Weight (300-700)

**Heading Fonts:**
- H1-H6 individual control
- Consistent or varied fonts
- Size hierarchy
- Weight options

### Color Scheme Configuration

#### Predefined Schemes
1. **Reign Clean:** Default blue theme
2. **Reign Dark:** Dark mode ready
3. **Reign Minimal:** Black and white
4. **Custom:** Your colors

#### Color Options
- Primary Color
- Secondary Color
- Link Color
- Link Hover
- Text Color
- Heading Color

### Page Mapping

#### Essential Pages
Map these WordPress pages:
- **Login Page:** Custom login design
- **Register Page:** Registration form
- **404 Page:** Not found page
- **Terms Page:** Terms of service
- **Privacy Page:** Privacy policy

### Custom Code Injection

#### Header Code
```html
<!-- Analytics, fonts, meta tags -->
<script>
// Your header scripts
</script>
```

#### Footer Code
```html
<!-- Tracking pixels, chat widgets -->
<script>
// Your footer scripts
</script>
```

## Integration Settings

### WooCommerce Integration
When WooCommerce is active:
- Shop layout options
- Product display settings
- Cart configuration
- Checkout customization

### LearnDash Integration
When LearnDash is active:
- Course layout
- Lesson sidebar
- Progress bar style
- Certificate display

### bbPress Integration
When bbPress is active:
- Forum layout
- Topic display
- User signatures
- Reply threading

## Mobile Specific Settings

### Mobile Menu Configuration
- **Style:** Hamburger / Dots / Custom
- **Position:** Left / Right / Center
- **Animation:** Slide / Fade / None
- **Background:** Solid / Gradient / Image

### Mobile Optimization
- Hide elements on mobile
- Adjust font sizes
- Simplify navigation
- Touch-friendly buttons

## Performance Settings

### Optimization Options
- **Lazy Loading:** Images, videos, iframes
- **Minification:** CSS, JavaScript
- **Disable:** Emojis, embeds
- **Defer:** JavaScript loading
- **Cache:** Compatible with major plugins

## Import/Export Settings

### Export Theme Settings
1. Go to Reign Settings
2. Click "Export Settings"
3. Download JSON file
4. Save for backup

### Import Settings
1. Click "Import Settings"
2. Upload JSON file
3. Review changes
4. Apply settings

## Troubleshooting Common Issues

### Settings Not Saving
**Check:**
1. File permissions (755/644)
2. PHP memory limit
3. mod_security rules
4. JavaScript errors

### BuddyPress Options Missing
**Verify:**
1. BuddyPress is activated
2. Components enabled
3. Pages assigned
4. Permalinks flushed

### Demo Import Fails
**Solutions:**
1. Increase PHP max_execution_time
2. Increase memory_limit
3. Import in smaller chunks
4. Check server timeout

## Best Practices

### Regular Maintenance
✅ Backup settings monthly
✅ Update theme regularly
✅ Test changes on staging
✅ Document customizations
✅ Monitor performance

### Optimization Tips
✅ Use child theme for custom code
✅ Optimize images before upload
✅ Limit active plugins
✅ Regular database cleanup
✅ Use caching plugin

## Frequently Asked Questions

**Q: Difference between Customizer and Reign Settings?**
A: Customizer for visual changes with live preview, Reign Settings for advanced configuration and integrations.

**Q: Can I reset settings?**
A: Yes, use "Reset to Defaults" button in each section or complete reset in Support tab.

**Q: Settings not appearing?**
A: Clear browser cache, check plugin conflicts, verify theme version is latest.

---

**Need More Help?** Access video tutorials in the Support tab or submit a support ticket with your license key.