# Reign WP Job Manager Addon - Configuration Guide

## Theme Customizer Settings

### Access Customizer Options

```
Appearance > Customize > Reign Job Manager Settings
```

## Job Listing Configuration

### Layout Options

#### Grid Layout Settings

```php
// Customizer settings
'reign_job_listing_layout' => array(
    'type'    => 'select',
    'choices' => array(
        'grid' => 'Grid View',
        'list' => 'List View',
        'map'  => 'Map View'
    ),
    'default' => 'grid'
)
```

**Grid Configuration:**

| Setting | Options | Default | Description |
|---------|---------|---------|-------------|
| Columns Desktop | 2, 3, 4 | 3 | Jobs per row on desktop |
| Columns Tablet | 1, 2 | 2 | Jobs per row on tablet |
| Columns Mobile | 1 | 1 | Jobs per row on mobile |
| Items Per Page | 9, 12, 15, 18 | 12 | Jobs shown per page |
| Card Style | Classic, Modern, Minimal | Modern | Job card design style |

### Job Card Elements

Toggle display of elements in job listings:

```
Customizer > Reign Job Manager > Job Card Elements
```

- ✓ **Company Logo** - Company branding
- ✓ **Job Title** - Position title
- ✓ **Company Name** - Employer name
- ✓ **Job Location** - Geographic location
- ✓ **Job Type** - Full-time, Part-time, etc.
- ✓ **Salary Range** - Compensation info
- ✓ **Posted Date** - Listing date
- ✓ **Application Deadline** - Closing date
- ✓ **Featured Badge** - Premium listings
- ✓ **Apply Button** - Quick apply CTA

## Single Job Page Configuration

### Job Page Layout

```php
'reign_job_single_layout' => array(
    'classic'  => 'Classic Layout',
    'modern'   => 'Modern Layout',
    'sidebar'  => 'With Sidebar',
    'fullwidth' => 'Full Width'
)
```

### Sidebar Configuration

```php
// Sidebar position options
'reign_job_sidebar_position' => array(
    'left'  => 'Left Sidebar',
    'right' => 'Right Sidebar', 
    'none'  => 'No Sidebar'
)
```

**Available Widgets:**
- Company Information
- Job Details
- Similar Jobs
- Company Jobs
- Application Form
- Share Buttons
- Job Location Map

### Job Information Display

```php
'reign_job_display_settings' => array(
    'show_company_info'    => true,
    'show_application_form' => true,
    'show_related_jobs'    => true,
    'show_share_buttons'   => true,
    'show_job_map'        => true,
    'show_salary_info'    => true
)
```

## Company Profile Settings

### Company Page Layout

```php
// Company profile customization
'reign_company_profile' => array(
    'show_banner'      => true,
    'show_logo'        => true,
    'show_description' => true,
    'show_website'     => true,
    'show_social'      => true,
    'show_job_count'   => true,
    'show_founded'     => true,
    'show_size'        => true
)
```

### Company Directory Settings

```
Customizer > Reign Job Manager > Company Directory
```

| Setting | Description | Options |
|---------|-------------|----------|
| Layout | Directory layout style | Grid / List |
| Companies Per Page | Number to display | 12, 16, 20, 24 |
| Sort By | Default sorting | Name / Jobs / Date |
| Show Filters | Display filter options | Yes / No |
| Show Search | Enable company search | Yes / No |

## Search & Filter Configuration

### Search Bar Settings

```php
'reign_job_search_fields' => array(
    'keyword'  => array(
        'enabled' => true,
        'placeholder' => 'Job title, keywords, or company'
    ),
    'location' => array(
        'enabled' => true,
        'placeholder' => 'City, state, or zip code',
        'radius' => true
    ),
    'category' => array(
        'enabled' => true,
        'multiple' => true
    )
)
```

### Advanced Filters

```php
'reign_job_filters' => array(
    'job_type'     => true,  // Full-time, Part-time
    'salary_range' => true,  // Salary filter
    'experience'   => true,  // Experience level
    'posted_date'  => true,  // Date posted
    'remote'       => true,  // Remote options
    'benefits'     => true   // Job benefits
)
```

## Application Settings

### Application Methods

```php
'reign_job_application_method' => array(
    'email'    => 'Email Application',
    'url'      => 'External URL',
    'internal' => 'Internal Form'
)
```

### Application Form Fields

```php
// Customize application form
'reign_application_fields' => array(
    'resume'       => 'required',
    'cover_letter' => 'optional',
    'portfolio'    => 'optional',
    'linkedin'     => 'optional',
    'references'   => 'hidden'
)
```

## Color Customization

### Job Listing Colors

```css
/* Customizer color settings */
--reign-job-primary: #2c3e50;
--reign-job-secondary: #3498db;
--reign-job-accent: #27ae60;
--reign-job-featured: #e74c3c;
--reign-job-border: #ecf0f1;
```

### Component-Specific Colors

```php
'job_type_colors' => array(
    'full-time'  => '#27ae60',
    'part-time'  => '#3498db',
    'contract'   => '#e67e22',
    'temporary'  => '#9b59b6',
    'internship' => '#f39c12'
)
```

## Typography Settings

### Font Configuration

```php
'reign_job_typography' => array(
    'job_title' => array(
        'font-family' => 'inherit',
        'font-size'   => '24px',
        'font-weight' => '600',
        'line-height' => '1.4'
    ),
    'company_name' => array(
        'font-family' => 'inherit',
        'font-size'   => '16px',
        'font-weight' => '500'
    )
)
```

## BuddyPress Integration Settings

### Profile Integration

```php
// Enable jobs tab in BuddyPress profile
'reign_job_bp_integration' => true,

// Tab settings
'reign_job_bp_settings' => array(
    'show_applied_jobs'  => true,
    'show_saved_jobs'    => true,
    'show_job_alerts'    => true,
    'show_resume'        => true,
    'show_cover_letter'  => true
)
```

### Activity Stream Integration

```php
// Activity types
'reign_job_activities' => array(
    'new_job_posted'     => true,
    'job_applied'        => true,
    'resume_updated'     => true,
    'job_saved'          => false,
    'company_followed'   => true
)
```

## Email Notification Settings

### Email Templates

```php
'reign_job_emails' => array(
    'new_application' => array(
        'enabled' => true,
        'subject' => 'New application for {job_title}',
        'recipient' => 'employer'
    ),
    'application_received' => array(
        'enabled' => true,
        'subject' => 'Application received for {job_title}',
        'recipient' => 'applicant'
    ),
    'job_approved' => array(
        'enabled' => true,
        'subject' => 'Your job listing is live',
        'recipient' => 'employer'
    )
)
```

## Map Configuration

### Google Maps Settings

```php
'reign_job_map_settings' => array(
    'api_key'      => 'YOUR_GOOGLE_MAPS_API_KEY',
    'default_zoom' => 10,
    'map_type'     => 'roadmap',
    'cluster'      => true,
    'style'        => 'custom' // or 'default'
)
```

### Map Styling

```javascript
// Custom map style
const mapStyle = [
    {
        "featureType": "all",
        "elementType": "geometry",
        "stylers": [{"color": "#f5f5f5"}]
    },
    // Additional styling...
];
```

## Performance Settings

### Caching Options

```php
'reign_job_cache' => array(
    'job_listings'    => 3600,  // 1 hour
    'company_data'    => 7200,  // 2 hours
    'search_results'  => 1800,  // 30 minutes
    'related_jobs'    => 3600   // 1 hour
)
```

### Optimization Settings

```php
'reign_job_optimization' => array(
    'lazy_load_images'   => true,
    'ajax_pagination'    => true,
    'minify_css'        => true,
    'combine_scripts'   => true
)
```

## Mobile Settings

### Mobile-Specific Options

```php
'reign_job_mobile' => array(
    'simplified_filters' => true,
    'touch_friendly'     => true,
    'swipe_navigation'   => true,
    'compact_view'       => true,
    'quick_apply'        => true
)
```

## SEO Configuration

### Meta Tags Settings

```php
'reign_job_seo' => array(
    'job_title_format'   => '%job_title% - %company% | %site_name%',
    'meta_description'   => true,
    'schema_markup'      => true,
    'og_tags'           => true,
    'twitter_cards'     => true
)
```

## Import/Export Settings

### Backup Configuration

```bash
# Export settings
wp option get reign_job_settings --format=json > job-settings.json

# Import settings
wp option update reign_job_settings --format=json < job-settings.json
```

## Advanced Configuration

### Custom Post Status

```php
// Add custom job statuses
add_filter('job_manager_job_statuses', function($statuses) {
    $statuses['on_hold'] = _x('On Hold', 'job status', 'reign');
    $statuses['filled'] = _x('Position Filled', 'job status', 'reign');
    return $statuses;
});
```

### Custom Fields

```php
// Add custom fields to jobs
add_filter('job_manager_job_listing_data_fields', function($fields) {
    $fields['_job_benefits'] = array(
        'label' => 'Benefits',
        'type' => 'textarea',
        'placeholder' => 'List job benefits'
    );
    return $fields;
});
```

## Troubleshooting Configuration

### Debug Mode

```php
// Enable debug mode
define('REIGN_JOB_DEBUG', true);

// Log configuration issues
if (REIGN_JOB_DEBUG) {
    error_log('Reign Job Config: ' . print_r($config, true));
}
```

## Next Steps

- [Job Listing Customization](04-job-listing-customization.md) - Customize job displays
- [Developer Guide](05-developer-guide.md) - Advanced development
- [Shortcode Reference](06-shortcodes-reference.md) - Available shortcodes
- [Troubleshooting](07-troubleshooting.md) - Common issues