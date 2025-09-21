# MediaPress Integration

## What is MediaPress?

MediaPress is a powerful media gallery plugin that transforms BuddyPress and BuddyBoss communities into media-rich social platforms. It enables users to upload, organize, and share photos, videos, audio files, and documents within their profiles, groups, and activity streams.

## What Reign Theme Offers

Reign Theme provides seamless MediaPress integration with:

### 1. **Enhanced Activity Stream Display**
- Custom media grid layouts in activity streams
- Responsive photo galleries with intelligent column distribution
- Support for photo counts exceeding 5+ items with overlay indicators
- Optimized media viewing experience

### 2. **Media Type Support**
- **Photos**: Grid and carousel layouts with lightbox support
- **Videos**: Embedded video players with responsive sizing
- **Audio**: Clean audio player integration
- **Documents**: Organized document listings with download links

### 3. **Customizer Options**
Located at **Appearance > Customize > Plugins Support > MediaPress**:

```
Media View Settings:
├── Enhanced Media View (Toggle)
├── Grid Layout Options
├── Activity Stream Display
└── Gallery Styling
```

## Configuration Guide

### Step 1: Install and Activate MediaPress

1. Install MediaPress from WordPress repository or MediaPress Pro
2. Navigate to **MediaPress > Settings**
3. Configure basic settings:
   - Enable for Members
   - Enable for Groups
   - Set storage preferences

### Step 2: Configure Reign Theme Settings

Navigate to **Appearance > Customize > Plugins Support > MediaPress**:

```php
// Theme automatically applies these optimizations
$reign_mpp_media_view = get_theme_mod( 'reign_mpp_media_view', true );
```

**Available Options:**

| Setting | Description | Default |
|---------|-------------|---------|
| Enhanced Media View | Enable Reign's custom media layouts | Enabled |
| Column Layout | Auto-adjusts based on media count | Auto |
| Lightbox Integration | Enable media lightbox | Enabled |

### Step 3: Media Display Configuration

The theme provides intelligent media distribution:

- **1-2 photos**: Full width display
- **3 photos**: Three-column grid
- **4 photos**: 2x2 grid layout
- **5+ photos**: Special layout with "+X more" overlay

## Features and Functionality

### Activity Stream Integration

```php
// Automatically handled by theme
// Located at: inc/plugins-support/mediapress/class-rtm-mpp-customization.php

class RTM_MPP_Customization {
    // Custom media injection for activity streams
    public function reign_mpp_activity_inject_attached_media_html() {
        // Intelligent photo grid generation
        // Responsive column calculation
        // Overlay for 5+ photos
    }
}
```

### Responsive Media Grids

The theme automatically applies responsive classes:

```css
.reign-mpp-container {
    /* Base container styling */
}

.post-row.column-1 { /* Single media */ }
.post-row.column-2 { /* Two media items */ }
.post-row.column-3 { /* Three media items */ }
.post-row.column-4 { /* Four media items */ }
.post-row.column-5 { /* Five or more items */ }
```

### Gallery Layouts

**Supported Gallery Views:**
- Grid View (default)
- List View
- Playlist View (audio/video)
- Slideshow View

## User Profile Integration

### Profile Media Tab

Users can manage their media directly from their profiles:

1. **Upload Media**: Drag-and-drop interface
2. **Create Galleries**: Organize media into collections
3. **Privacy Controls**: Public, Friends, or Private
4. **Media Activity**: Automatic activity stream updates

### Group Media Support

Groups can have dedicated media galleries:

- Group admins can manage media settings
- Members can contribute based on permissions
- Shared galleries for collaborative content

## Styling Customization

### Custom CSS Classes

```css
/* MediaPress Container */
.mpp-container { }

/* Activity Media */
.mpp-activity-media-list { }

/* Media Types */
.mpp-media-photo { }
.mpp-media-video { }
.mpp-media-audio { }
.mpp-media-doc { }

/* Overlay for 5+ photos */
.more-photos-overlay {
    position: absolute;
    background: rgba(0,0,0,0.7);
    color: #fff;
}
```

### Theme Compatibility

Reign automatically applies:
- Consistent styling with theme colors
- Responsive breakpoints
- RTL support
- Dark mode compatibility

## Advanced Configuration

### Hooks and Filters

```php
// Modify media grid columns
add_filter( 'reign_mpp_grid_columns', function( $columns, $count ) {
    // Custom column logic
    return $columns;
}, 10, 2 );

// Customize media display
add_action( 'reign_before_mpp_media', function() {
    // Add custom content before media
});
```

### Performance Optimization

The theme includes optimizations:

1. **Lazy Loading**: Images load on scroll
2. **Thumbnail Optimization**: Multiple sizes for different views
3. **CDN Support**: Compatible with CDN services
4. **Cache Integration**: Works with caching plugins

## Troubleshooting

### Common Issues

#### Media Not Displaying in Activity
**Solution**:
1. Check MediaPress settings
2. Verify **Appearance > Customize > Plugins Support > MediaPress**
3. Clear cache

#### Gallery Layout Issues
**Solution**:
1. Ensure theme is updated
2. Check for CSS conflicts
3. Disable conflicting plugins

#### Upload Errors
**Solution**:
1. Verify file size limits
2. Check server upload settings
3. Review MediaPress storage settings

### Debug Mode

Enable debug logging:

```php
// In wp-config.php
define( 'MPPD_DEBUG', true );
```

## Best Practices

### Media Organization

1. **Create Logical Galleries**: Group related content
2. **Use Descriptive Titles**: Help users find media
3. **Set Appropriate Privacy**: Control visibility
4. **Optimize Before Upload**: Compress images/videos

### Performance Tips

1. **Image Optimization**: Use optimized formats (WebP)
2. **Video Hosting**: Consider external hosting for large videos
3. **Regular Cleanup**: Remove unused media
4. **CDN Integration**: Use CDN for media delivery

## Integration with Other Plugins

### Compatible Plugins

- **rtMedia**: Can work alongside with proper configuration
- **WP Smush**: Auto-optimize uploaded images
- **ShortPixel**: Image compression
- **Cloudflare**: CDN and optimization

### Activity Plus Integration

MediaPress works seamlessly with BuddyPress Activity Plus for enhanced posting options.

## Developer Reference

### File Locations

```
Theme Files:
├── inc/plugins-support/mediapress/
│   └── class-rtm-mpp-customization.php
├── assets/css/
│   └── mediapress-styles.css (auto-generated)
└── template-parts/
    └── mediapress/ (override templates)
```

### Template Overrides

To customize MediaPress templates:

1. Copy from: `plugins/mediapress/templates/`
2. Paste to: `reign-theme/mediapress/`
3. Modify as needed

## Support Resources

- **MediaPress Documentation**: [mediapress.io/docs](https://mediapress.io/docs)
- **Reign Theme Support**: [wbcomdesigns.com/support](https://wbcomdesigns.com/support)
- **Community Forums**: Active community help
- **Video Tutorials**: Available in member area

## Conclusion

The Reign Theme's MediaPress integration creates a rich multimedia experience for your community. With intelligent layouts, responsive design, and extensive customization options, users can share and interact with media content seamlessly within your BuddyPress or BuddyBoss platform.