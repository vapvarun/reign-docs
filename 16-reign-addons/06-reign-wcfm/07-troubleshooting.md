# Reign WCFM Addon - Troubleshooting

## Common Issues

### Plugin Installation Issues

#### Plugin Not Activating
1. **Check Requirements:**
   - Verify Reign theme is active
   - Ensure WooCommerce is installed and active
   - Confirm WCFM plugin is installed and active

2. **Error Messages:**
   - Plugin shows deactivation notice if requirements not met
   - Check WordPress admin notices for specific issues

#### Features Not Working
1. **Clear Caches:**
   - Clear browser cache
   - Clear site cache (if caching plugin active)
   - Clear object cache

2. **Check Plugin Status:**
   - Verify plugin is active in Plugins page
   - Ensure no plugin conflicts

### BuddyPress Integration Issues

#### Store Tab Not Showing
1. **Verify Requirements:**
   - BuddyPress must be active
   - User must be a vendor
   - "Display Store Tab" setting must be enabled

2. **Check Settings:**
   - Go to Reign Settings → WCFM
   - Enable "Display Store Tab"
   - Save settings

#### Favorite Products Not Working
1. **Check Configuration:**
   - Verify "Mark Products As Favourite" is enabled
   - Ensure user is logged in
   - Check BuddyPress is active

2. **Test Functionality:**
   - Try marking a product as favorite
   - Check user profile for "Favourite" tab
   - Verify products appear in tab

#### Activities Not Showing
1. **Component Requirements:**
   - BuddyPress Activity component must be active
   - Check Components in BuddyPress Settings

2. **Settings Check:**
   - Verify activity options are enabled in Reign Settings → WCFM
   - Ensure activities aren't disabled by other plugins

### Store Display Issues

#### Layout Not Changing
1. **Check Settings:**
   - Go to Reign Settings → WCFM → Store Settings
   - Verify layout selection is saved
   - Clear cache after changes

2. **Template Issues:**
   - Check for theme template overrides
   - Verify no CSS conflicts

### Performance Issues

#### Slow Loading
1. **Optimization:**
   - Enable caching
   - Optimize images
   - Check server resources

2. **Debug:**
   - Disable other plugins temporarily
   - Switch to default theme to test
   - Check error logs

### Styling Issues

#### Styles Not Applied
1. **Clear Cache:**
   - Browser cache
   - Site cache
   - CSS cache

2. **Check Conflicts:**
   - Verify Reign theme is active
   - Look for CSS conflicts in browser inspector
   - Check for plugin conflicts

#### BuddyPress Styling Issues
1. **Theme Compatibility:**
   - Ensure BuddyPress templates are compatible
   - Check for template overrides
   - Verify BuddyPress styling

## Getting Help

### Before Contacting Support

**Gather Information:**
- WordPress version
- Reign theme version
- WCFM plugin version
- BuddyPress version (if used)
- Plugin version
- Error messages
- Steps to reproduce issue

### Support Channels

**WBcom Designs Support:**
- Email: support@wbcomdesigns.com
- Include detailed description
- Provide system information
- Attach screenshots if helpful

---

*Troubleshooting guide verified against Reign WCFM Addon v1.8.3 source code*