# Reign WCFM Addon - Quick Start Guide

## What This Addon Provides

Reign WCFM Addon enhances WCFM Marketplace with Reign theme integration, providing:

**Core Features (Verified):**
- BuddyPress integration with store tabs and favorite products
- Theme styling for WCFM elements
- Activity stream integration for products, reviews, and orders
- Store layout options (2 layouts available)
- Template override system

---

## Prerequisites

Required:
- ✅ WordPress 4.0+
- ✅ Reign Theme activated
- ✅ WooCommerce plugin active
- ✅ WCFM Marketplace plugin installed

Optional:
- BuddyPress (for social features)

---

## Installation Steps

### Step 1: Install the Addon

1. **Upload via WordPress:**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   → Select reign-wcfm-addon.zip
   → Install Now → Activate
   ```

2. **Verify Installation:**
   - Check Plugins page - "Reign WCFM Addon" should be active
   - WCFM stores should now use Reign theme styling

### Step 2: Configure Settings

The addon works automatically with WCFM. Available customization:

**Reign Settings → WCFM (verified options):**

1. **General Settings:**
   - Mark Products As Favourite (enable/disable)
   - Display Store Tab (for BuddyPress vendor profiles)
   - Create Product Activity (BuddyPress activity streams)
   - Add Review Activity (review activities in feeds)
   - Order Activity (purchase activities in feeds)

2. **Store Settings:**
   - Single Store Layout: Layout 1 or Layout 2

---

## Available Features

### BuddyPress Integration (when BuddyPress is active)

#### For Customers:
- **Favourite Products Tab** - Save and view favorite products in profile
- **Activity Feeds** - See product creation, reviews, and order activities

#### For Vendors:
- **Store Tab** - Display vendor's products in their profile
- **Activity Streams** - Vendor activities appear in feeds

### Store Enhancements

#### Visual Improvements:
- Reign theme styling applied to all WCFM elements
- 2 store layout options available
- Responsive design improvements

#### Template System:
- Custom template overrides
- Enhanced store displays
- Mobile-optimized layouts

---

## Quick Test

### Verify Installation Works

1. **Check Store Pages:**
   - Visit existing WCFM store pages
   - Should display with Reign theme styling

2. **Test BuddyPress Features (if BP active):**
   - Check vendor profiles for "Store" tab
   - Enable favorite products and test functionality
   - Enable activities and create test product

3. **Verify Layout Options:**
   - Go to Reign Settings → WCFM → Store Settings
   - Switch between Layout 1 and Layout 2
   - Visit store page to see changes

---

## Common Usage

### Using with BuddyPress

1. **Enable Integration:**
   - Go to Reign Settings → WCFM
   - Enable desired BuddyPress features
   - Configure activity settings

2. **For Vendors:**
   - Vendor profiles will show "Store" tab
   - Products, reviews, and orders create activities
   - Store information visible in profile

3. **For Customers:**
   - Can mark products as favorites
   - View favorites in profile "Favourite" tab
   - See marketplace activities in feeds

### Store Customization

1. **Choose Layout:**
   - Reign Settings → WCFM → Store Settings
   - Select Layout 1 or Layout 2
   - Changes apply to all store pages

2. **Template Overrides:**
   - Copy files from plugin to theme
   - Customize as needed for your brand

---

## Troubleshooting

### Settings Not Saving
1. Clear all caches
2. Check theme settings are saved
3. Verify plugin is properly activated

### BuddyPress Features Missing
1. Verify BuddyPress is active
2. Check user roles and capabilities
3. Enable required BuddyPress components

### Styling Issues
1. Clear cache
2. Verify Reign theme is active
3. Check for CSS conflicts

---

## Next Steps

For detailed configuration and customization:
- [Configuration Guide](03-configuration.md) - Theme settings
- [Store Customization](04-store-customization.md) - Appearance options
- [Developer Guide](05-developer-guide.md) - Hooks and filters

---

*Quick Start Guide verified against Reign WCFM Addon v1.8.3 source code*