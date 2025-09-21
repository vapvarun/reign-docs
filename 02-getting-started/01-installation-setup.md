# Installation & Setup Guide

## Prerequisites

### System Requirements
- WordPress 5.0 or higher
- PHP 7.2 or higher
- MySQL 5.6 or higher
- Memory Limit: 128MB minimum (256MB recommended)
- Max Execution Time: 30 seconds minimum
- Upload Max Filesize: 32MB minimum

### Browser Compatibility
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Installation Methods

### Method 1: WordPress Admin Installation

1. **Purchase and Download**
   - Purchase Reign Theme from [WBcom Designs](https://wbcomdesigns.com/downloads/reign-buddypress-theme/)
   - Download the theme ZIP file from your account

2. **Upload Theme**
   ```
   WordPress Admin → Appearance → Themes → Add New → Upload Theme
   Choose File: reign-theme.zip
   Click "Install Now"
   ```

3. **Activate Theme**
   - After installation completes, click "Activate"
   - You'll be redirected to Reign Settings

### Method 2: FTP Installation

1. **Extract Files**
   - Unzip reign-theme.zip on your computer
   - You'll get a folder named "reign-theme"

2. **Upload via FTP**
   ```
   Connect to your server via FTP
   Navigate to: /wp-content/themes/
   Upload the "reign-theme" folder
   ```

3. **Activate in WordPress**
   - Go to Appearance → Themes
   - Find Reign Theme and click "Activate"

## Initial Setup Wizard

### Automatic Redirect
After theme activation, you'll be automatically redirected to:
```
Admin → Reign Settings → Get Started
```

### License Activation

1. **Navigate to License Section**
   ```
   Reign Settings → License
   ```

2. **Enter License Key**
   - Find your license key in WBcom Designs → My Account
   - Enter the key in the license field
   - Click "Activate License"

3. **License Benefits**
   - Automatic theme updates
   - Premium support access
   - Addon compatibility
   - Extended features

## Required Plugins

### Install Required Plugins

The theme will prompt you to install required plugins:

1. **Kirki Customizer Framework**
   - Required for theme customization
   - Auto-installs with theme

2. **Reign Core** (if available)
   - Extended functionality
   - Custom post types
   - Additional widgets

### Recommended Plugins

Based on your site type, install:

**For Community Sites:**
- BuddyPress or BuddyBoss Platform
- bbPress (for forums)
- BuddyPress Member Types

**For E-commerce:**
- WooCommerce
- Dokan/WCFM/WC Vendors (for marketplaces)

**For Learning Platforms:**
- LearnDash/LifterLMS/TutorLMS/Sensei
- Corresponding Reign addon

## Demo Data Import

### Option 1: One-Click Demo Import

1. **Install Demo Importer Plugin**
   ```
   Plugins → Add New
   Search: "Wbcom Essential"
   Install and Activate
   ```

2. **Import Demo Content**
   ```
   Reign Settings → Demo Installation
   Choose demo style
   Click "Import"
   ```

3. **What Gets Imported**
   - Sample pages
   - Menu structure
   - Widget configuration
   - Customizer settings
   - Sample posts/products

### Option 2: Manual Setup

Create essential pages manually:
- Home
- About
- Contact
- Blog
- Shop (if using WooCommerce)
- Members (if using BuddyPress)
- Groups (if using BuddyPress)
- Activity (if using BuddyPress)

## Theme Configuration

### Step 1: Site Identity

```
Customizer → Site Identity
```

- **Site Title**: Your website name
- **Tagline**: Brief description
- **Site Icon**: Favicon (512×512px recommended)

### Step 2: Logo Setup

```
Customizer → General → Site Logo
```

- **Desktop Logo**: Upload main logo
- **Mobile Logo**: Upload mobile version
- **Logo Width**: Set maximum width
- **Logo Height**: Set maximum height

### Step 3: Menu Configuration

1. **Create Menus**
   ```
   Appearance → Menus
   Create new menu → Name it "Primary Menu"
   Add pages/categories/custom links
   ```

2. **Assign Menu Locations**
   - Primary Menu
   - Top Menu (optional)
   - Mobile Menu
   - Footer Menu

### Step 4: Homepage Setup

```
Settings → Reading
```

Choose display option:
- **Static Page**: Select your homepage
- **Latest Posts**: Blog-style homepage

## Basic Customization

### Color Scheme

```
Customizer → Colors
```

Choose from predefined schemes:
- Default
- Clean
- Dark
- Dating
- Ectoplasm
- Sunrise
- Coffee

### Typography

```
Customizer → General → Typography
```

Configure:
- Body Font Family
- Heading Font Family
- Font Sizes
- Line Heights
- Font Weights

### Site Layout

```
Customizer → General → Site Layout
```

Options:
- **Wide**: Full-width layout
- **Boxed**: Contained layout with background
- **Compact**: Narrow content area

## Performance Settings

### Enable Performance Mode

```
Customizer → General → Site Performance
```

- **Smart Performance Mode**: Enable
- **Lazy Loading**: Enable for images
- **Minification**: Enable CSS/JS minification
- **Widget Detection**: Auto-disable unused widgets

## Troubleshooting

### Common Issues

**White Screen After Activation**
- Increase PHP memory limit to 256MB
- Check PHP version (must be 7.2+)
- Disable all plugins and reactivate

**Customizer Not Loading**
- Ensure Kirki is installed and active
- Clear browser cache
- Check for JavaScript errors

**Demo Import Fails**
- Increase max_execution_time to 300
- Increase memory_limit to 256MB
- Import in smaller chunks

**Missing Styling**
- Regenerate CSS in Customizer
- Clear cache (browser and server)
- Check file permissions (755 for folders, 644 for files)

## Next Steps

After successful installation:

1. **Configure Header**: Choose from 4 header layouts
2. **Setup Footer**: Configure footer widgets and layout
3. **Page Mapping**: Assign special pages
4. **Install Addons**: Add functionality with Reign addons
5. **Customize Further**: Explore all customizer options

## Getting Help

### Documentation
- In-dashboard documentation
- Online docs: [docs.wbcomdesigns.com](https://docs.wbcomdesigns.com)

### Support Channels
- **Premium Support**: Via WBcom account
- **Community Forum**: WordPress.org forums
- **Video Tutorials**: YouTube channel
- **Knowledge Base**: Help articles

## Update Process

### Automatic Updates
With active license:
1. Dashboard notification appears
2. Click "Update Now"
3. Theme updates automatically

### Manual Updates
1. Download latest version from account
2. Upload via FTP (overwrite existing)
3. Clear cache

## Backup Recommendations

Before major changes:
1. **Full Site Backup**: Use UpdraftPlus/BackWPup
2. **Database Backup**: Export via phpMyAdmin
3. **Theme Settings**: Export Customizer settings
4. **Child Theme**: Preserve customizations

---

*Your Reign theme is now installed and ready for customization!*