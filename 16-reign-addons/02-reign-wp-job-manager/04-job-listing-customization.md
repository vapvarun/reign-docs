# Reign WP Job Manager Addon - Job Listing Customization

## Job Listing Layouts

### Grid Layout Customization

#### Basic Grid Structure

```html
<!-- Grid layout structure -->
<div class="reign-job-listings grid-layout">
    <div class="job-card">
        <div class="company-logo"></div>
        <div class="job-content">
            <h3 class="job-title"></h3>
            <div class="company-name"></div>
            <div class="job-meta"></div>
        </div>
        <div class="job-actions"></div>
    </div>
</div>
```

#### Custom CSS for Grid

```css
/* Grid customization */
.reign-job-listings.grid-layout {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
}

.job-card {
    background: #fff;
    border-radius: 8px;
    padding: 25px;
    transition: transform 0.3s, box-shadow 0.3s;
}

.job-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 30px rgba(0,0,0,0.1);
}

/* Featured job styling */
.job-card.featured {
    border: 2px solid var(--reign-primary-color);
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: #fff;
}
```

### List Layout Customization

#### List Structure

```html
<!-- List layout structure -->
<div class="reign-job-listings list-layout">
    <article class="job-listing-item">
        <div class="job-listing-left">
            <img class="company-logo" />
        </div>
        <div class="job-listing-center">
            <h3 class="job-title"></h3>
            <div class="job-details"></div>
        </div>
        <div class="job-listing-right">
            <button class="apply-button"></button>
        </div>
    </article>
</div>
```

#### List Styling

```css
/* List view customization */
.reign-job-listings.list-layout .job-listing-item {
    display: flex;
    align-items: center;
    padding: 20px;
    border-bottom: 1px solid #e0e0e0;
    transition: background 0.3s;
}

.job-listing-item:hover {
    background: #f8f9fa;
}

.job-listing-left {
    flex: 0 0 80px;
}

.job-listing-center {
    flex: 1;
    padding: 0 20px;
}

.job-listing-right {
    flex: 0 0 auto;
}
```

## Job Card Components

### Company Logo Display

```php
// Customize company logo
add_filter('reign_job_company_logo', function($logo_html, $post) {
    $company_logo = get_the_company_logo($post, 'thumbnail');
    
    if (!$company_logo) {
        // Fallback to company initial
        $company_name = get_the_company_name($post);
        $initial = strtoupper(substr($company_name, 0, 1));
        
        return '<div class="company-logo-placeholder" data-initial="' . $initial . '"></div>';
    }
    
    return $company_logo;
}, 10, 2);
```

```css
/* Logo placeholder styling */
.company-logo-placeholder {
    width: 60px;
    height: 60px;
    background: linear-gradient(135deg, #667eea, #764ba2);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    font-size: 24px;
    font-weight: bold;
}

.company-logo-placeholder::before {
    content: attr(data-initial);
}
```

### Job Meta Information

```php
// Customize job meta display
function reign_custom_job_meta($post_id) {
    $meta_items = array();
    
    // Location
    $location = get_the_job_location($post_id);
    if ($location) {
        $meta_items[] = '<span class="job-location"><i class="fas fa-map-marker-alt"></i> ' . $location . '</span>';
    }
    
    // Job Type
    $job_types = wp_get_post_terms($post_id, 'job_listing_type');
    if ($job_types) {
        foreach ($job_types as $type) {
            $meta_items[] = '<span class="job-type job-type-' . $type->slug . '">' . $type->name . '</span>';
        }
    }
    
    // Salary
    $salary = get_post_meta($post_id, '_job_salary', true);
    if ($salary) {
        $meta_items[] = '<span class="job-salary"><i class="fas fa-dollar-sign"></i> ' . $salary . '</span>';
    }
    
    // Posted Date
    $posted = human_time_diff(get_post_time('U', false, $post_id), current_time('timestamp')) . ' ago';
    $meta_items[] = '<span class="job-posted"><i class="far fa-clock"></i> ' . $posted . '</span>';
    
    return '<div class="job-meta">' . implode(' ', $meta_items) . '</div>';
}
```

### Featured Badge

```php
// Add featured badge
add_action('reign_job_card_badge', function($post_id) {
    if (is_position_featured($post_id)) {
        echo '<div class="featured-badge">';
        echo '<i class="fas fa-star"></i> Featured';
        echo '</div>';
    }
    
    // Urgent badge
    $deadline = get_post_meta($post_id, '_application_deadline', true);
    if ($deadline && strtotime($deadline) - current_time('timestamp') < 7 * DAY_IN_SECONDS) {
        echo '<div class="urgent-badge">Urgent</div>';
    }
});
```

## Search & Filter Bar

### Advanced Search Form

```php
function reign_job_search_form() {
    ?>
    <form class="reign-job-search-form" method="get" action="<?php echo job_manager_get_permalink('jobs'); ?>">
        <div class="search-row">
            <div class="search-field keyword-field">
                <input type="text" name="search_keywords" placeholder="Job title, keywords, or company" />
            </div>
            <div class="search-field location-field">
                <input type="text" name="search_location" placeholder="Location" />
                <select name="search_radius" class="radius-select">
                    <option value="">Exact location</option>
                    <option value="5">Within 5 miles</option>
                    <option value="10">Within 10 miles</option>
                    <option value="25">Within 25 miles</option>
                    <option value="50">Within 50 miles</option>
                </select>
            </div>
            <div class="search-submit">
                <button type="submit" class="search-button">
                    <i class="fas fa-search"></i> Search Jobs
                </button>
            </div>
        </div>
        
        <div class="advanced-filters">
            <button type="button" class="toggle-filters">
                <i class="fas fa-filter"></i> Advanced Filters
            </button>
            <div class="filter-panel">
                <!-- Job Type -->
                <div class="filter-group">
                    <label>Job Type</label>
                    <?php
                    $job_types = get_terms('job_listing_type');
                    foreach ($job_types as $type) {
                        echo '<label><input type="checkbox" name="job_types[]" value="' . $type->slug . '"> ' . $type->name . '</label>';
                    }
                    ?>
                </div>
                
                <!-- Categories -->
                <div class="filter-group">
                    <label>Category</label>
                    <?php
                    job_manager_dropdown_categories(array(
                        'show_option_all' => 'All Categories',
                        'hierarchical' => 1,
                        'name' => 'search_categories',
                        'class' => 'job-category-dropdown'
                    ));
                    ?>
                </div>
                
                <!-- Salary Range -->
                <div class="filter-group">
                    <label>Salary Range</label>
                    <div class="salary-slider" data-min="0" data-max="200000"></div>
                    <div class="salary-inputs">
                        <input type="number" name="salary_min" placeholder="Min" />
                        <input type="number" name="salary_max" placeholder="Max" />
                    </div>
                </div>
            </div>
        </div>
    </form>
    <?php
}
```

## Single Job Page Customization

### Job Header Section

```php
function reign_job_header() {
    global $post;
    ?>
    <div class="job-header">
        <div class="job-header-content">
            <div class="company-branding">
                <?php the_company_logo('large'); ?>
            </div>
            <div class="job-info">
                <h1 class="job-title"><?php the_title(); ?></h1>
                <div class="company-details">
                    <span class="company-name">
                        <a href="<?php echo get_the_company_website(); ?>">
                            <?php the_company_name(); ?>
                        </a>
                    </span>
                    <span class="job-location">
                        <i class="fas fa-map-marker-alt"></i>
                        <?php the_job_location(); ?>
                    </span>
                </div>
                <div class="job-highlights">
                    <?php
                    $salary = get_post_meta($post->ID, '_job_salary', true);
                    if ($salary) {
                        echo '<span class="highlight-item"><i class="fas fa-dollar-sign"></i> ' . $salary . '</span>';
                    }
                    
                    $job_types = wp_get_post_terms($post->ID, 'job_listing_type');
                    foreach ($job_types as $type) {
                        echo '<span class="highlight-item job-type-' . $type->slug . '">' . $type->name . '</span>';
                    }
                    ?>
                </div>
            </div>
            <div class="job-actions">
                <?php get_job_manager_template('job-application.php'); ?>
                <button class="save-job" data-job-id="<?php echo $post->ID; ?>">
                    <i class="far fa-heart"></i> Save
                </button>
            </div>
        </div>
    </div>
    <?php
}
```

### Job Content Tabs

```php
function reign_job_tabs() {
    ?>
    <div class="job-tabs">
        <ul class="tab-nav">
            <li class="active"><a href="#description">Description</a></li>
            <li><a href="#requirements">Requirements</a></li>
            <li><a href="#benefits">Benefits</a></li>
            <li><a href="#company">About Company</a></li>
            <li><a href="#apply">How to Apply</a></li>
        </ul>
        
        <div class="tab-content">
            <div id="description" class="tab-pane active">
                <?php the_content(); ?>
            </div>
            
            <div id="requirements" class="tab-pane">
                <?php echo get_post_meta(get_the_ID(), '_job_requirements', true); ?>
            </div>
            
            <div id="benefits" class="tab-pane">
                <?php echo get_post_meta(get_the_ID(), '_job_benefits', true); ?>
            </div>
            
            <div id="company" class="tab-pane">
                <?php the_company_description(); ?>
            </div>
            
            <div id="apply" class="tab-pane">
                <?php get_job_manager_template('job-application.php'); ?>
            </div>
        </div>
    </div>
    <?php
}
```

## Company Profile Customization

### Company Header

```php
function reign_company_header($company_id) {
    ?>
    <div class="company-profile-header">
        <div class="company-banner" style="background-image: url('<?php echo get_company_banner($company_id); ?>')">
            <div class="banner-overlay"></div>
        </div>
        <div class="company-info-bar">
            <div class="company-logo">
                <?php echo get_company_logo($company_id, 'large'); ?>
            </div>
            <div class="company-details">
                <h1><?php echo get_company_name($company_id); ?></h1>
                <div class="company-meta">
                    <span class="industry"><?php echo get_company_industry($company_id); ?></span>
                    <span class="size"><?php echo get_company_size($company_id); ?> employees</span>
                    <span class="location"><?php echo get_company_location($company_id); ?></span>
                </div>
            </div>
            <div class="company-actions">
                <button class="follow-company" data-company="<?php echo $company_id; ?>">
                    Follow
                </button>
                <a href="<?php echo get_company_website($company_id); ?>" class="website-link">
                    Visit Website
                </a>
            </div>
        </div>
    </div>
    <?php
}
```

## Mobile Responsiveness

### Mobile-Specific Styles

```css
/* Mobile optimization */
@media (max-width: 768px) {
    /* Grid to single column */
    .reign-job-listings.grid-layout {
        grid-template-columns: 1fr;
        gap: 15px;
    }
    
    /* Simplified job cards */
    .job-card {
        padding: 15px;
    }
    
    /* Stack elements */
    .job-listing-item {
        flex-direction: column;
        text-align: center;
    }
    
    /* Touch-friendly buttons */
    .apply-button,
    .save-job {
        min-height: 44px;
        font-size: 16px;
        width: 100%;
    }
    
    /* Collapsible filters */
    .advanced-filters {
        position: fixed;
        bottom: 0;
        left: 0;
        right: 0;
        background: #fff;
        transform: translateY(100%);
        transition: transform 0.3s;
    }
    
    .advanced-filters.active {
        transform: translateY(0);
    }
}
```

## Performance Optimization

### Lazy Loading Implementation

```javascript
// Lazy load job listings
(function($) {
    var lazyLoadJobs = function() {
        $('.job-card img').each(function() {
            if ($(this).offset().top < window.innerHeight + window.pageYOffset + 500) {
                var src = $(this).data('src');
                if (src) {
                    $(this).attr('src', src).removeAttr('data-src');
                }
            }
        });
    };
    
    $(window).on('scroll', lazyLoadJobs);
    lazyLoadJobs();
})(jQuery);
```

## Next Steps

- [Developer Guide](05-developer-guide.md) - Advanced development
- [Shortcode Reference](06-shortcodes-reference.md) - Available shortcodes
- [Troubleshooting](07-troubleshooting.md) - Common issues
- [FAQ](08-faq.md) - Frequently asked questions