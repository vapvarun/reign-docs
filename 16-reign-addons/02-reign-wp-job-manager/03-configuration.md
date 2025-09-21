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

## Complete Reign WP Job Manager Settings

### Main Settings Location

**Access all Reign WP Job Manager settings:**
```
WP Admin > Reign Settings > WP Job Manager
```

### License Configuration

#### Add License

**Activate your license key:**
```
Reign Settings > License > WP Job Manager Addon
```

License activation is required for:
- Future updates of Reign WP Job Manager Addon
- Latest bug fixes and security patches
- WordPress compatibility updates
- Premium support access
- Access to JobMate theme features

#### Upgrade License

**License upgrade options:**
- Single site → 5 sites
- 5 sites → Unlimited sites
- Annual → Lifetime

### System Requirements

**Minimum requirements:**
- WordPress 5.0+
- Reign Theme (latest version)
- WP Job Manager Plugin (free or paid)
- PHP 7.2+
- Memory: 256MB

**Recommended:**
- PHP 8.0+
- Memory: 512MB
- MySQL 5.7+
- SSL Certificate for applications

### Map Settings Configuration

**Configure job location maps:**
```
Reign Settings > WP Job Manager > Map Settings
```

**Map Features:**
- Google Maps API integration
- OpenStreetMap support
- Radius search functionality
- Cluster markers for multiple jobs
- Custom map styles
- Geolocation support

```php
// Map configuration example
'reign_job_map_config' => array(
    'provider' => 'google', // or 'openstreetmap'
    'api_key' => 'YOUR_API_KEY',
    'enable_clusters' => true,
    'default_radius' => 25, // miles
    'auto_locate' => true
)
```

### Resume Archive Page Customization

**Configure resume listings:**
```
Reign Settings > WP Job Manager > Resume Settings
```

**Resume Display Options:**
- Grid layout (2, 3, 4 columns)
- List layout with details
- Card-based design
- Candidate information display
- Skills and experience highlight
- Download resume option

```php
// Resume archive settings
'reign_resume_archive' => array(
    'layout' => 'grid',
    'columns' => 3,
    'show_photo' => true,
    'show_skills' => true,
    'show_experience' => true,
    'enable_download' => false
)
```

### Job and Resume Layout Settings

#### Job Listing Layout

**Customize job listing appearance:**
```
Reign Settings > WP Job Manager > Job Listing Layout
```

Layout options:
- **Classic** - Traditional job board style
- **Modern** - Card-based with hover effects
- **Minimal** - Clean, text-focused design
- **Map View** - Split screen with map

#### Single Job Layout

**Single job page configuration:**
```
Reign Settings > WP Job Manager > Single Job Layout
```

Features:
- Header style (banner/compact)
- Sidebar position
- Related jobs display
- Application method
- Social sharing buttons

#### Resume Listing Layout

**Configure resume displays:**
```
Reign Settings > WP Job Manager > Resume Listing Layout
```

Options:
- Display format (grid/list)
- Information shown
- Contact details visibility
- Download permissions

#### Single Resume Layout

**Single resume page setup:**
```
Reign Settings > WP Job Manager > Single Resume Layout
```

Configuration:
- Layout style
- Contact form integration
- Skills visualization
- Experience timeline
- Portfolio section

### Sidebars and Widget Areas

**Available widget areas:**
```
Appearance > Widgets
```

**Reign WP Job Manager Sidebars:**
- **Job Listing Sidebar** - Shows on job archive
- **Single Job Sidebar** - Shows on job pages
- **Resume Sidebar** - Shows on resume pages
- **Company Sidebar** - Shows on company profiles
- **Dashboard Sidebar** - Shows in user dashboard

**Available Widgets:**
- Reign: Job Search
- Reign: Featured Jobs
- Reign: Recent Jobs
- Reign: Job Categories
- Reign: Job Types
- Reign: Company List
- Reign: Resume Search
- Reign: Job Stats

### JobMate Theme Integration

#### Getting Started With JobMate

**JobMate is a specialized job board theme that extends Reign:**
```
Reign Settings > JobMate Options
```

JobMate Features:
- Pre-built job board layouts
- Advanced search functionality
- Employer dashboard
- Candidate dashboard
- Application tracking
- Job alerts system

#### JobMate Installation

**Install JobMate child theme:**
1. Download JobMate from your account
2. Install as WordPress theme
3. Activate JobMate child theme
4. Import demo content
5. Configure JobMate settings

#### Installing Demo Content

**Import JobMate demo data:**
```
Reign Settings > Demo Import > JobMate
```

Demo includes:
- Sample job listings
- Company profiles
- Resume examples
- Page templates
- Widget configurations
- Menu structures

### Search Filter Configuration

**Advanced search setup:**
```
Reign Settings > WP Job Manager > Search Filters
```

**Filter Options:**
```php
'reign_job_search_filters' => array(
    'keywords' => array(
        'enabled' => true,
        'autocomplete' => true
    ),
    'location' => array(
        'enabled' => true,
        'radius_search' => true,
        'geolocation' => true
    ),
    'category' => array(
        'enabled' => true,
        'hierarchical' => true,
        'multiple' => true
    ),
    'job_type' => array(
        'enabled' => true,
        'checkboxes' => true
    ),
    'salary' => array(
        'enabled' => true,
        'range_slider' => true
    ),
    'date_posted' => array(
        'enabled' => true,
        'options' => array('24h', '3days', '7days', '30days')
    )
)
```

### Shortcode Extensions

**Enhanced shortcode options:**
```
Reign Settings > WP Job Manager > Shortcodes
```

Additional parameters:
- `layout="modern"` - Use Reign layouts
- `columns="3"` - Grid columns
- `featured_first="true"` - Prioritize featured
- `show_filters="true"` - Display filters
- `ajax_loading="true"` - AJAX pagination

### API Reference Integration

**Developer API access:**
```php
// Get Reign Job Manager instance
$reign_jobs = Reign_WP_Job_Manager::get_instance();

// Custom job query
$jobs = $reign_jobs->get_jobs(array(
    'posts_per_page' => 10,
    'featured' => true,
    'location' => 'New York'
));

// Add custom job fields
add_filter('reign_job_fields', function($fields) {
    $fields['custom_field'] = array(
        'label' => 'Custom Field',
        'type' => 'text'
    );
    return $fields;
});
```

### Hook Usage Guide

**Available hooks:**
```php
// Before job listing
do_action('reign_before_job_listing');

// After job listing
do_action('reign_after_job_listing');

// Job card customization
add_action('reign_job_card_footer', function($job_id) {
    // Add custom content
});

// Filter job query
add_filter('reign_job_query_args', function($args) {
    // Modify query
    return $args;
});
```

### Features Overview

**Complete feature list:**
- Modern job board layouts
- Advanced search and filtering
- Google Maps integration
- Resume management
- Company profiles
- Application tracking
- Email notifications
- BuddyPress integration
- Ajax-powered interactions
- Mobile responsive design
- SEO optimized
- Translation ready
- RTL support
- Multisite compatible

### Developer FAQ

**Common developer questions:**

Q: How to override templates?
A: Copy templates from `/plugins/reign-wp-job-manager/templates/` to `/themes/reign-child/reign-job-manager/`

Q: How to add custom job fields?
A: Use the `job_manager_job_listing_data_fields` filter

Q: How to modify job queries?
A: Use the `reign_job_query_args` filter

Q: How to customize email templates?
A: Override templates in theme or use filters

### Frequently Asked Questions - End Users

**Common user questions:**

Q: How do I post a job?
A: Go to Dashboard > Post a Job, fill the form and submit

Q: Can candidates apply without registration?
A: Yes, if enabled in settings

Q: How to feature a job listing?
A: Select "Feature this listing" when posting or edit existing job

Q: Can I import jobs from Indeed/LinkedIn?
A: Yes, using compatible import plugins

### Additional Features

#### BuddyPress Job Manager Integration

**Enhanced BuddyPress features:**
- Jobs tab in user profiles
- Job activity in streams
- Private messaging for applications
- Group job boards
- Member job recommendations

#### Notification System

**Job notification settings:**
```php
'reign_job_notifications' => array(
    'new_application' => true,
    'job_approved' => true,
    'job_expired' => true,
    'resume_submitted' => true,
    'daily_job_alerts' => true
)
```

#### Backend Configuration

**Admin panel setup:**
```
WP Admin > Jobs > Settings
```

Configure:
- Submission settings
- Listing duration
- Moderation rules
- Application methods
- Email notifications
- Payment integration

## Next Steps

- [Job Listing Customization](04-job-listing-customization.md) - Customize job displays
- [Developer Guide](05-developer-guide.md) - Advanced development
- [Shortcode Reference](06-shortcodes-reference.md) - Available shortcodes
- [Troubleshooting](07-troubleshooting.md) - Common issues
- [FAQ](08-faq.md) - Frequently asked questions