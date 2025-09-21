# Reign WCFM Addon - Configuration Guide

## Overview

The Reign WCFM Addon works automatically with WCFM once installed. Configuration options are minimal and focused on BuddyPress integration and store layout.

## Configuration Options (Verified)

### Access Settings

```
Reign Settings → WCFM
```

### General Settings

**Mark Products As Favourite**
- Enable/disable favorite products feature
- When enabled, users can mark products as favorites
- Favorites appear in user profiles (requires BuddyPress)

**Display Store Tab** (requires BuddyPress)
- Shows "Store" tab in vendor profiles
- Displays vendor's products in their profile
- Only appears for users who are vendors

**Create Product Activity** (requires BuddyPress)
- Posts activity when vendors create products
- Requires BuddyPress Activity component
- Disabled automatically if BuddyBoss product activities are enabled

**Add Review Activity** (requires BuddyPress)
- Posts activity when products are reviewed
- Integrates with WooCommerce review system
- Requires BuddyPress Activity component

**Order Activity** (requires BuddyPress)
- Posts activity when orders are placed
- Shows purchase activities in feeds
- Requires BuddyPress Activity component

### Store Settings

**Single Store Layout**
- Layout 1 - Default store layout
- Layout 2 - Alternative store layout
- Changes apply to all WCFM store pages

## BuddyPress Integration Setup

### Required Components

For BuddyPress features to work:

1. **BuddyPress must be active**
2. **Required components:**
   - Members (for profile tabs)
   - Activity (for activity streams)

### Feature Configuration

1. **Enable Desired Features:**
   - Go to Reign Settings → WCFM
   - Check boxes for features you want
   - Save settings

2. **Test Features:**
   - Create test vendor account
   - Check profile for "Store" tab
   - Test favorite products functionality
   - Verify activities appear in feeds

## Template Customization

### Override Templates

Copy templates from plugin to theme for customization:

**From:**
```
/wp-content/plugins/reign-wcfm-addon/templates/
```

**To:**
```
/wp-content/themes/your-theme/wcfm/
```

### Available Templates

- Store header layouts
- Store listing pages
- Store detail pages

## Common Configuration Tasks

### Enable All BuddyPress Features

1. Go to Reign Settings → WCFM
2. Enable these options:
   - Mark Products As Favourite
   - Display Store Tab
   - Create Product Activity
   - Add Review Activity
   - Order Activity

### Switch Store Layout

1. Go to Reign Settings → WCFM
2. Under Store Settings
3. Select Layout 1 or Layout 2
4. Save settings

### Disable Activity Streams

1. Go to Reign Settings → WCFM
2. Uncheck activity options:
   - Create Product Activity
   - Add Review Activity
   - Order Activity

---

*Configuration guide verified against Reign WCFM Addon v1.8.3 source code*