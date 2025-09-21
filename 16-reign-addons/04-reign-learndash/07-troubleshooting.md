# Reign LearnDash Addon - Troubleshooting

## Common Issues

### Shortcodes Not Working

#### Shortcodes Not Displaying
1. Verify plugin is activated
2. Check LearnDash is properly configured
3. Ensure courses/groups exist and are published
4. Clear cache

#### Shortcode Parameters Not Working
1. Check parameter spelling and syntax
2. Verify parameter values are supported
3. Test with basic shortcode first: `[modern_courses]`

### Styling Issues

#### Templates Not Using Reign Styling
1. Clear browser cache
2. Clear site cache
3. Verify Reign theme is active
4. Check for CSS conflicts

#### Archive Pages Not Enhanced
1. Ensure LearnDash is properly installed
2. Check permalink settings
3. Clear cache and test again

### Template Issues

#### Custom Templates Not Loading
1. Verify template file location
2. Check file permissions
3. Clear cache

#### Archive Customization Not Showing
1. Go to Appearance → Customize
2. Look for LearnDash Groups settings
3. Verify BuddyPress components if using social features

## Performance Issues

### Slow Loading Shortcodes
1. Limit `per_page` to reasonable numbers (12-24)
2. Use specific filters instead of showing all content
3. Optimize course/group images

### Memory Issues
1. Check PHP memory limit
2. Optimize database queries
3. Use caching plugins

---

*Troubleshooting guide verified against Reign LearnDash Addon source code*