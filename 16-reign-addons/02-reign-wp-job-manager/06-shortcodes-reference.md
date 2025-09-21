# Reign WP Job Manager Addon - Shortcode Reference

## Job Listing Shortcodes

### [jobs] - Display Job Listings

**Description:** Display job listings with filters and pagination.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `per_page` | Number of jobs per page | 10 | `per_page="12"` |
| `orderby` | Sort jobs by | date | `orderby="title"` |
| `order` | Sort order | DESC | `order="ASC"` |
| `show_filters` | Show filter bar | true | `show_filters="false"` |
| `show_categories` | Show category filter | true | `show_categories="false"` |
| `show_job_types` | Show job type filter | true | `show_job_types="false"` |
| `show_pagination` | Show pagination | true | `show_pagination="false"` |
| `show_more` | Enable load more | false | `show_more="true"` |
| `categories` | Specific categories | - | `categories="12,15,18"` |
| `job_types` | Specific job types | - | `job_types="full-time,part-time"` |
| `location` | Filter by location | - | `location="New York"` |
| `keywords` | Filter by keywords | - | `keywords="developer"` |
| `featured` | Show only featured | false | `featured="true"` |
| `filled` | Show filled positions | false | `filled="true"` |
| `layout` | Layout style | grid | `layout="list"` |

**Examples:**

```shortcode
// Basic job listings
[jobs]

// 12 jobs per page with filters
[jobs per_page="12" show_filters="true"]

// Specific category in list layout
[jobs categories="15" layout="list"]

// Featured jobs only
[jobs featured="true" per_page="6"]

// Jobs in specific location
[jobs location="San Francisco" job_types="full-time"]
```

### [job] - Display Single Job

**Description:** Display a specific job listing.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `id` | Job post ID | - | `id="123"` |

**Example:**

```shortcode
[job id="123"]
```

### [job_summary] - Job Summary Card

**Description:** Display a summary card for a specific job.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `id` | Job post ID | - | `id="123"` |
| `width` | Card width | 100% | `width="300px"` |
| `align` | Alignment | left | `align="center"` |

**Example:**

```shortcode
[job_summary id="123" width="400px" align="center"]
```

## Job Submission Shortcodes

### [submit_job_form] - Job Submission Form

**Description:** Display the job submission form for employers.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `force_registration` | Require registration | false | `force_registration="true"` |
| `job_id` | Edit existing job | - | `job_id="123"` |

**Examples:**

```shortcode
// New job submission
[submit_job_form]

// Edit existing job
[submit_job_form job_id="123"]

// Require registration
[submit_job_form force_registration="true"]
```

### [job_dashboard] - Employer Dashboard

**Description:** Display the employer's job management dashboard.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `posts_per_page` | Jobs per page | 25 | `posts_per_page="10"` |

**Example:**

```shortcode
[job_dashboard posts_per_page="15"]
```

## Company Shortcodes

### [job_companies] - Company Directory

**Description:** Display a directory of companies.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `per_page` | Companies per page | 12 | `per_page="20"` |
| `orderby` | Sort by | name | `orderby="job_count"` |
| `order` | Sort order | ASC | `order="DESC"` |
| `show_letters` | Show A-Z filter | false | `show_letters="true"` |
| `show_categories` | Show categories | true | `show_categories="false"` |

**Examples:**

```shortcode
// Basic company directory
[job_companies]

// With A-Z filter
[job_companies show_letters="true" per_page="20"]

// Sorted by job count
[job_companies orderby="job_count" order="DESC"]
```

### [company_jobs] - Company's Job Listings

**Description:** Display jobs from a specific company.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `company` | Company name | - | `company="Acme Corp"` |
| `company_id` | Company user ID | - | `company_id="45"` |
| `per_page` | Jobs per page | 10 | `per_page="15"` |

**Examples:**

```shortcode
// Jobs by company name
[company_jobs company="Google"]

// Jobs by company ID
[company_jobs company_id="45" per_page="20"]
```

## Search & Filter Shortcodes

### [jobs_search] - Advanced Search Form

**Description:** Display an advanced job search form.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `show_keywords` | Show keyword field | true | `show_keywords="false"` |
| `show_location` | Show location field | true | `show_location="false"` |
| `show_categories` | Show category dropdown | true | `show_categories="false"` |
| `show_job_types` | Show job types | true | `show_job_types="false"` |
| `show_salary` | Show salary range | false | `show_salary="true"` |

**Example:**

```shortcode
[jobs_search show_salary="true"]
```

### [job_filter] - Job Filter Bar

**Description:** Display a standalone filter bar.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `show_search` | Show search field | true | `show_search="false"` |
| `taxonomies` | Taxonomies to filter | all | `taxonomies="job_listing_category"` |

**Example:**

```shortcode
[job_filter show_search="true" taxonomies="job_listing_category,job_listing_type"]
```

## Resume Shortcodes (If Resume Add-on Installed)

### [resumes] - Display Resumes

**Description:** Display candidate resumes.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `per_page` | Resumes per page | 10 | `per_page="12"` |
| `show_filters` | Show filters | true | `show_filters="false"` |
| `show_categories` | Show categories | true | `show_categories="false"` |
| `show_pagination` | Show pagination | true | `show_pagination="false"` |

**Example:**

```shortcode
[resumes per_page="12" show_filters="true"]
```

### [submit_resume_form] - Resume Submission

**Description:** Display resume submission form.

**Example:**

```shortcode
[submit_resume_form]
```

### [candidate_dashboard] - Candidate Dashboard

**Description:** Display candidate's resume management dashboard.

**Example:**

```shortcode
[candidate_dashboard]
```

## Statistical Shortcodes

### [job_stats] - Job Statistics

**Description:** Display job listing statistics.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `show_total` | Show total jobs | true | `show_total="false"` |
| `show_categories` | Show by category | false | `show_categories="true"` |
| `show_types` | Show by type | false | `show_types="true"` |
| `show_locations` | Show by location | false | `show_locations="true"` |

**Example:**

```shortcode
[job_stats show_categories="true" show_types="true"]
```

### [job_count] - Job Count

**Description:** Display total number of jobs.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `category` | Specific category | - | `category="15"` |
| `type` | Specific job type | - | `type="full-time"` |
| `location` | Specific location | - | `location="Boston"` |

**Examples:**

```shortcode
// Total jobs
[job_count]

// Jobs in category
[job_count category="15"]

// Full-time jobs in Boston
[job_count type="full-time" location="Boston"]
```

## Map Shortcodes

### [jobs_map] - Jobs Map View

**Description:** Display jobs on an interactive map.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `height` | Map height | 400px | `height="500px"` |
| `zoom` | Initial zoom level | 10 | `zoom="12"` |
| `center` | Center location | - | `center="New York, NY"` |
| `categories` | Filter categories | - | `categories="12,15"` |

**Example:**

```shortcode
[jobs_map height="500px" zoom="11" center="San Francisco, CA"]
```

## Custom Combination Examples

### Job Board Page

```shortcode
[jobs_search]
[jobs per_page="15" show_filters="false" layout="list"]
```

### Company Profile Page

```shortcode
[company_jobs company="Acme Corp" per_page="10"]
[job_stats show_total="true"]
```

### Location-Based Directory

```shortcode
[jobs_map height="400px" center="Los Angeles, CA"]
[jobs location="Los Angeles" per_page="20"]
```

## Conditional Display

### Using Shortcodes in PHP

```php
// In template file
echo do_shortcode('[jobs per_page="12"]');

// With dynamic parameters
$location = get_user_meta(get_current_user_id(), 'location', true);
echo do_shortcode('[jobs location="' . esc_attr($location) . '"]');

// Conditional display
if (is_user_logged_in()) {
    echo do_shortcode('[job_dashboard]');
} else {
    echo do_shortcode('[jobs]');
}
```

## Creating Custom Shortcodes

### Example: Featured Companies

```php
function reign_featured_companies_shortcode($atts) {
    $atts = shortcode_atts(array(
        'number' => 5,
        'orderby' => 'name'
    ), $atts);
    
    // Get featured companies
    $companies = get_users(array(
        'role' => 'employer',
        'number' => $atts['number'],
        'orderby' => $atts['orderby'],
        'meta_query' => array(
            array(
                'key' => 'featured_employer',
                'value' => 'yes'
            )
        )
    ));
    
    ob_start();
    
    if ($companies) {
        echo '<div class="featured-companies">';
        foreach ($companies as $company) {
            // Display company
            echo '<div class="company-item">';
            echo get_avatar($company->ID, 60);
            echo '<h4>' . esc_html($company->display_name) . '</h4>';
            echo '</div>';
        }
        echo '</div>';
    }
    
    return ob_get_clean();
}
add_shortcode('featured_companies', 'reign_featured_companies_shortcode');
```

## Performance Tips

1. **Cache Output**: Cache shortcode output for better performance
2. **Limit Results**: Use `per_page` parameter to limit results
3. **Lazy Load**: Enable lazy loading for images
4. **AJAX Loading**: Use `show_more="true"` instead of pagination

## Troubleshooting Shortcodes

### Common Issues

1. **Shortcode not rendering**: Check if plugin is active
2. **No results showing**: Verify post status and parameters
3. **Styling issues**: Check theme compatibility
4. **Performance slow**: Reduce per_page value

## Next Steps

- [Troubleshooting](07-troubleshooting.md) - Common issues and solutions
- [FAQ](08-faq.md) - Frequently asked questions
- [Developer Guide](05-developer-guide.md) - Advanced customization