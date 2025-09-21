# Reign WCFM Addon - Installation & Setup

## Prerequisites

Required:
- ✅ WordPress 4.0+
- ✅ Reign Theme (activated)
- ✅ WooCommerce
- ✅ WCFM plugin

Optional:
- BuddyPress (for social features)

---

## Installation

### Step 1: Install the Plugin

1. **Upload via WordPress Admin:**
   ```
   WordPress Admin → Plugins → Add New → Upload Plugin
   → Select reign-wcfm-addon.zip
   → Install Now → Activate
   ```

2. **Alternative: FTP Upload**
   ```
   Extract ZIP → Upload to /wp-content/plugins/reign-wcfm-addon/
   Activate from WordPress Admin
   ```

### Step 2: Verify Installation

1. **Check Plugin Status:**
   - Go to Plugins page
   - "Reign WCFM Addon" should be active

2. **Test Integration:**
   - Visit WCFM store pages
   - Should display with Reign theme styling

---

## Configuration

### Basic Settings

The addon works automatically with WCFM. For customization:

1. **Go to Reign Settings → WCFM**
2. **Configure available options:**

#### General Settings:
- **Mark Products As Favourite** - Enable favorite products feature
- **Display Store Tab** - Show store tab in vendor profiles (requires BuddyPress)
- **Create Product Activity** - Post activities when products are created
- **Add Review Activity** - Post activities for product reviews
- **Order Activity** - Post activities for purchases

#### Store Settings:
- **Single Store Layout** - Choose Layout 1 or Layout 2

### BuddyPress Integration (Optional)

If BuddyPress is active:

1. **Enable Features:**
   - Check desired activity options
   - Enable store and favorite tabs

2. **Verify BuddyPress Components:**
   - Activity component must be active for activities
   - Members component required for profile tabs

---

## Verification

### Test the Installation

1. **Store Pages:**
   - Visit WCFM store pages
   - Should use enhanced Reign styling

2. **BuddyPress Features (if active):**
   - Check vendor profiles for "Store" tab
   - Test favorite products functionality
   - Verify activities appear in feeds

3. **Settings:**
   - Switch between store layouts
   - Test activity generation
   - Verify styling changes

---

## Troubleshooting

### Common Issues

#### Plugin Not Activating
1. Verify all required plugins are active
2. Check Reign theme is activated
3. Ensure sufficient server resources

#### Features Not Working
1. Clear all caches
2. Check plugin activation status
3. Verify BuddyPress components are active

#### Styling Issues
1. Clear cache
2. Check theme conflicts
3. Verify CSS files are loading

---

## Next Steps

- [Configuration Guide](03-configuration.md) - Detailed settings
- [Store Customization](04-store-customization.md) - Appearance options
- [Developer Guide](05-developer-guide.md) - Hooks and filters

---

*Installation guide verified against Reign WCFM Addon v1.8.3 source code*