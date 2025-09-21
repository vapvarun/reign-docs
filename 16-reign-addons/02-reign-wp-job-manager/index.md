# Reign WP Job Manager Addon Documentation

## Overview
Reign WP Job Manager Addon enhances WP Job Manager with 3 custom shortcodes using "jobmate" prefix, advanced search filtering, and custom job taxonomies.

## Requirements
- WordPress 5.0+
- Reign Theme
- WP Job Manager Plugin
- WP Job Manager - Resume Manager (optional)

## Installation
1. Upload `reign-wp-job-manager-addon` to `/wp-content/plugins/`
2. Activate plugin
3. Configure in Reign Settings → Job Manager

## Features

### Custom Shortcodes (Jobmate Prefix)

#### [jobmate_job_search_filter]
Advanced job search filter form.

**Parameters:**
- `keywords` - Default search keywords (default: '')
- `location` - Default location (default: '')
- `selected_category` - Pre-selected category (default: '')
- `show_categories` - Show category filter (default: true)
- `hide_labels` - Hide form labels (default: false)
- `form_layout` - Layout style (default: 'vertical')
- `background_color` - Form background (default: '')
- `button_color` - Button color (default: '')
- `label_color` - Label color (default: '')
- `heading` - Form heading (default: '')
- `remove_border` - Remove borders (default: false)

**Example:**
```
[jobmate_job_search_filter form_layout="horizontal" show_categories="true"]
```

#### [jobmate_job_listing]
Display job listings with custom layout.

**Purpose:** Enhanced job listing display with Reign theme styling.

**Example:**
```
[jobmate_job_listing]
```

#### [jobmate_resume_listing]
Display resume listings (requires Resume Manager addon).

**Purpose:** Display candidate resumes with custom styling.

**Example:**
```
[jobmate_resume_listing]
```

### Advanced Query System
- Meta queries for job data
- Taxonomy queries for categories
- Date queries for posting dates
- Keyword length threshold filtering

### Custom Job Taxonomies
Additional categorization options beyond default WP Job Manager.

## WP Job Manager Core Shortcodes

These come from WP Job Manager (NOT Reign addon):
- `[jobs]` - Job listings
- `[job_dashboard]` - Job dashboard
- `[submit_job_form]` - Submit job
- `[job]` - Single job
- `[job_summary]` - Job summary

## Developer Reference

### Plugin Structure
```
reign-wp-job-manager-addon/
├── admin/
├── assets/
├── core/
│   ├── class-reign-wp-job-manager-customization.php
│   └── reign-wp-job-manager-addon-functions.php
├── job-manager-shortcodes/
│   └── class-jobmate-job-manager-shortcodes.php
└── reign-wp-job-manager-addon.php
```

### Hooks & Filters

#### Actions
```php
// Job listing meta
do_action('single_job_listing_meta_start');
do_action('single_job_listing_meta_end');

// Resume listing meta
do_action('reign_jobmate_single_resume_listing_meta_start');
do_action('reign_jobmate_single_resume_listing_meta_end');
```

#### Filters
```php
// Template location
apply_filters('reign_job_manager_locate_template', $template, $template_name, $template_path, $default_path);

// Job form fields
apply_filters('jobmate_job_form_fields_get_job_data', $fields, $job);

// Page IDs
apply_filters('jobmate_wpjm_get_[page]_page_id', $page_id);

// Search defaults
apply_filters('jobmate_job_manager_output_search_defaults', $defaults);

// Query filters
apply_filters('jm_job_listing_query_meta_query', $meta_query);
apply_filters('jm_job_listing_query_tax_query', $tax_query);
apply_filters('jm_job_listing_query_date_query', $date_query);
apply_filters('jm_job_listing_query_posts_per_page', $per_page);
apply_filters('jm_job_listing_default_catalog_orderby', 'date');
apply_filters('jm_job_listing_get_catalog_ordering_args', $args);

// Navigation
apply_filters('jobmate_wpjm_layered_nav_default_query_type', 'and');

// Keyword threshold
apply_filters('job_manager_get_listings_keyword_length_threshold', 2);
```

### Code Examples

#### Customize Search Defaults
```php
add_filter('jobmate_job_manager_output_search_defaults', function($defaults) {
    $defaults['show_categories'] = false;
    $defaults['form_layout'] = 'horizontal';
    return $defaults;
});
```

#### Modify Job Query
```php
add_filter('jm_job_listing_query_meta_query', function($meta_query) {
    // Add custom meta query
    return $meta_query;
});
```

#### Change Posts Per Page
```php
add_filter('jm_job_listing_query_posts_per_page', function() {
    return 20;
});
```

## Template Customization

Override templates via `reign_job_manager_locate_template` filter or copy to theme.

## Important Notes
- Uses "jobmate" prefix for shortcodes (not "reign")
- 3 custom shortcodes total
- Resume shortcode requires Resume Manager addon
- Advanced filtering capabilities
- Query customization system

## Common Issues

### Shortcodes not working
- Check "jobmate" prefix spelling
- Verify WP Job Manager active
- For resumes, check Resume Manager addon

### Search not filtering
- Check keyword length (min 2 chars)
- Verify categories enabled
- Clear cache

### Styling issues
- Ensure Reign theme active
- Check for CSS conflicts
- Verify addon activated