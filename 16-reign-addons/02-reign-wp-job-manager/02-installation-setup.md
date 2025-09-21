# Reign WP Job Manager Addon - Installation & Setup

## Prerequisites

Before installing Reign WP Job Manager Addon, ensure you have:

### Required Components
1. **WordPress** 5.8 or higher
2. **Reign Theme** 7.0 or higher (activated)
3. **WP Job Manager** 1.35 or higher
4. **PHP** 7.4 or higher
5. **MySQL** 5.6 or higher

### Recommended Components
- **BuddyPress** 9.0 or higher
- **Memory Limit**: 256MB minimum
- **Max Execution Time**: 300 seconds
- **Upload Max Size**: 64MB

## Installation Methods

### Method 1: Upload via WordPress Admin

1. **Download the Plugin**
   - Login to your WBcom Designs account
   - Navigate to Downloads section
   - Download `reign-wp-job-manager-addon.zip`

2. **Upload to WordPress**
   ```
   WordPress Admin > Plugins > Add New > Upload Plugin
   ```
   - Click "Choose File"
   - Select `reign-wp-job-manager-addon.zip`
   - Click "Install Now"

3. **Activate the Plugin**
   - Click "Activate Plugin" after installation
   - Or navigate to Plugins list and activate

### Method 2: FTP Upload

1. **Extract the ZIP file**
   ```
   reign-wp-job-manager-addon.zip -> reign-wp-job-manager-addon/
   ```

2. **Upload via FTP**
   ```
   /wp-content/plugins/reign-wp-job-manager-addon/
   ```

3. **Activate from WordPress Admin**
   ```
   Plugins > Installed Plugins > Reign WP Job Manager Addon > Activate
   ```

## Initial Setup

### Step 1: License Activation

1. Navigate to **Reign Settings > License**
2. Enter your license key for Reign WP Job Manager
3. Click "Activate License"

```php
// License validation endpoint
https://wbcomdesigns.com/edd-sl-api/
```

### Step 2: Configure WP Job Manager

#### Basic Settings

1. **Navigate to Job Listings > Settings**

2. **Job Listings Tab**
   ```
   Listings Per Page: 10
   Filled Positions: Hide
   Categories: Enable
   Job Types: Full Time, Part Time, Contract, Temporary
   ```

3. **Job Submission Tab**
   ```
   Account Required: Yes/No
   Approval Required: Yes (Recommended)
   Duration: 30 days
   Allow Editing: Yes
   ```

### Step 3: Create Essential Pages

#### Automatic Page Creation

The plugin creates these pages automatically:
- Jobs (`/jobs/`)
- Submit Job (`/submit-job/`)
- Job Dashboard (`/job-dashboard/`)

#### Manual Page Creation

1. **Jobs Listing Page**
   ```
   Title: Jobs
   Slug: jobs
   Shortcode: [jobs]
   ```

2. **Submit Job Page**
   ```
   Title: Post a Job
   Slug: submit-job
   Shortcode: [submit_job_form]
   ```

3. **Job Dashboard**
   ```
   Title: Job Dashboard
   Slug: job-dashboard
   Shortcode: [job_dashboard]
   ```

4. **Company Directory** (Optional)
   ```
   Title: Companies
   Slug: companies
   Shortcode: [job_companies]
   ```

### Step 4: Configure Reign Addon Settings

1. **Navigate to Appearance > Customize > Reign Job Manager**

2. **Listing Layout Settings**
   ```
   Layout Type: Grid / List
   Jobs Per Page: 12
   Show Filters: Yes
   Show Map: Yes/No
   ```

3. **Single Job Settings**
   ```
   Sidebar Position: Right / Left / None
   Show Company Info: Yes
   Show Apply Button: Yes
   Show Related Jobs: Yes
   ```

### Step 5: Menu Configuration

#### Add to Primary Menu

1. Go to **Appearance > Menus**
2. Add these items:
   - Jobs (Job Listing Page)
   - Post a Job (Submit Job Page)
   - Companies (Company Directory)
   - Job Dashboard (For logged-in users)

#### Conditional Menu Items

```php
// Show dashboard only for logged-in users
add_filter('wp_nav_menu_items', function($items, $args) {
    if (is_user_logged_in() && $args->theme_location == 'primary') {
        $items .= '<li><a href="/job-dashboard/">My Jobs</a></li>';
    }
    return $items;
}, 10, 2);
```

## Post-Installation Configuration

### 1. Set Up Email Notifications

```
Job Listings > Settings > Email Notifications
```

Configure emails for:
- New job submission
- Job approved
- Job expired
- New application

### 2. Configure Application Method

```php
// Application methods
- Email: Direct email to employer
- URL: External application link
- Form: Built-in application form
```

### 3. Set Up Google Maps (Optional)

1. Get Google Maps API Key
2. Add to **Job Listings > Settings > Google Maps API Key**
3. Enable map view in listings

### 4. Configure Resume Manager (If installed)

```
Resumes > Settings
```

Set up:
- Resume submission
- Resume visibility
- Contact details visibility

## BuddyPress Integration Setup

### Enable Job Activity

```php
// Add to functions.php
add_filter('reign_job_bp_activity', '__return_true');

// Activity types enabled
- New job posted
- Job application submitted
- Resume updated
```

### Add Job Tab to Profiles

```php
function reign_add_job_profile_tab() {
    bp_core_new_nav_item(array(
        'name' => 'Jobs',
        'slug' => 'jobs',
        'screen_function' => 'reign_job_profile_screen',
        'position' => 40
    ));
}
add_action('bp_setup_nav', 'reign_add_job_profile_tab');
```

## Performance Optimization

### 1. Database Indexes

```sql
-- Add indexes for better performance
ALTER TABLE wp_posts 
ADD INDEX idx_job_listing (post_type, post_status, post_date);

ALTER TABLE wp_postmeta 
ADD INDEX idx_job_meta (meta_key(20), meta_value(50));
```

### 2. Caching Configuration

```php
// Exclude dynamic pages from cache
$excluded_urls = array(
    '/job-dashboard/',
    '/submit-job/',
    '/my-account/',
);
```

### 3. Image Optimization

```php
// Optimize company logos
add_filter('job_manager_company_logo_size', function() {
    return array(300, 300);
});
```

## Security Configuration

### 1. File Upload Settings

```php
// Restrict file types for applications
add_filter('job_manager_mime_types', function($mimes) {
    return array(
        'pdf' => 'application/pdf',
        'doc' => 'application/msword',
        'docx' => 'application/vnd.openxmlformats-officedocument.wordprocessingml.document'
    );
});
```

### 2. User Capabilities

```php
// Set proper capabilities
$employer_caps = array(
    'edit_job_listing',
    'read_job_listing',
    'delete_job_listing',
    'edit_job_listings',
    'publish_job_listings',
);
```

## Verification Steps

### Test Installation

1. **Check Plugin Status**
   ```php
   if (class_exists('WP_Job_Manager')) {
       echo 'WP Job Manager is active';
   }
   if (function_exists('reign_job_manager_init')) {
       echo 'Reign addon is active';
   }
   ```

2. **Test Job Submission**
   - Submit a test job
   - Check approval process
   - Verify email notifications

3. **Test Job Search**
   - Search by keyword
   - Filter by category
   - Test location search

## Common Installation Issues

### Issue: Pages Not Created

**Solution:**
1. Go to **Job Listings > Settings**
2. Click "Generate Pages" button
3. Or create pages manually with shortcodes

### Issue: Styles Not Applied

**Solution:**
1. Clear browser cache
2. Regenerate CSS in Customizer
3. Check for plugin conflicts

### Issue: Jobs Not Displaying

**Solution:**
1. Check job status (published)
2. Verify shortcode usage
3. Check theme compatibility

## Migration from Other Job Plugins

### Import Jobs

```php
// Basic import function
function import_jobs_from_other_plugin() {
    $old_jobs = get_posts(array(
        'post_type' => 'old_job_type',
        'posts_per_page' => -1
    ));
    
    foreach ($old_jobs as $job) {
        $new_job = array(
            'post_title' => $job->post_title,
            'post_content' => $job->post_content,
            'post_type' => 'job_listing',
            'post_status' => 'publish'
        );
        
        $new_id = wp_insert_post($new_job);
        
        // Migrate meta data
        update_post_meta($new_id, '_job_location', get_post_meta($job->ID, 'old_location', true));
        update_post_meta($new_id, '_company_name', get_post_meta($job->ID, 'old_company', true));
    }
}
```

## Next Steps

- [Configuration Guide](03-configuration.md) - Detailed settings
- [Job Listing Customization](04-job-listing-customization.md) - Customize displays
- [Shortcode Reference](06-shortcodes-reference.md) - Available shortcodes
- [Troubleshooting](07-troubleshooting.md) - Common issues