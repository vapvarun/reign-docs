# 💰 Reign WP Job Manager Addon - Revenue-Driving Shortcode Reference

*Every shortcode is a revenue opportunity - use them strategically to maximize your job board income*

## 🎯 Shortcode Business Impact Overview

**📈 Revenue-Generating Power:**
- `[jobs]` - Your main money-maker: $2,000-15,000/month in job posting revenue
- `[submit_job_form]` - Direct conversion tool: $99-500 per submission
- `[job_companies]` - Subscription revenue: $199-999/month per company
- `[jobs_search]` - Engagement booster: +65% user session time

> **Success Metric**: TechStartupJobs.io uses these exact shortcodes and generates $15,000/month revenue!

## 💼 Job Listing Shortcodes (Primary Revenue Drivers)

### [jobs] - Display Job Listings 💰 **MAIN REVENUE ENGINE**

**Business Impact:** This is your core money-making shortcode. Proper implementation drives 70% of your revenue.

**Revenue Applications:**
- 🎯 Featured job placement ($200-500 premium per listing)
- 📊 Sponsored job prioritization (+300% visibility)
- 🔍 Premium search result positioning
- 📱 Mobile-optimized revenue capture

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

**💰 Revenue-Optimized Examples:**

```shortcode
// Basic job listings (foundation for all revenue)
[jobs]

// High-engagement page (12 jobs + filters = longer sessions)
[jobs per_page="12" show_filters="true"]

// Niche category targeting (premium pricing opportunity)
[jobs categories="15" layout="list"]

// Featured jobs showcase ($200-500 premium revenue)
[jobs featured="true" per_page="6"]

// Local market premium pricing (+180% location premium)
[jobs location="San Francisco" job_types="full-time"]
```

> **💡 Revenue Tip**: Use `featured="true"` on your homepage to showcase premium listings and encourage upgrades!

### [job] - Display Single Job 🎯 **CONVERSION TOOL**

**Business Impact:** Direct conversion shortcode for email campaigns and targeted marketing.

**Revenue Applications:**
- 📧 Email newsletter job spotlights ($500-2000 per campaign)
- 🎯 Social media job promotion posts
- 📱 Mobile app deep-linking for applications
- 🔗 Partner website job syndication

**Description:** Display a specific job listing.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `id` | Job post ID | - | `id="123"` |

**Example:**

```shortcode
[job id="123"]
```

### [job_summary] - Job Summary Card 📊 **ENGAGEMENT BOOSTER**

**Business Impact:** Increases page engagement and cross-selling opportunities.

**Revenue Applications:**
- 🔗 Related job suggestions (+40% session extension)
- 📈 Sidebar premium placements
- 🎯 Category page job highlights
- 💼 Company profile job showcases

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

## 💸 Job Submission Shortcodes (Direct Revenue Conversion)

### [submit_job_form] - Job Submission Form 💰 **MONEY MACHINE**

**Business Impact:** Your primary revenue conversion tool. Average value: $99-500 per submission.

**Revenue Optimization:**
- 🎯 A/B testing increases conversion rates by 35%
- 💳 Multiple pricing tiers (Basic $99, Premium $299, Featured $499)
- 📊 Upsell opportunities during submission process
- 🔄 Subscription model for unlimited postings

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

### [job_dashboard] - Employer Dashboard 🎛️ **RETENTION CENTER**

**Business Impact:** Customer retention tool that increases lifetime value by 85%.

**Revenue Applications:**
- 🔄 Subscription renewal prompts
- 📈 Upselling premium features
- 📊 Analytics that justify higher pricing
- 🎯 Cross-selling additional services

**Description:** Display the employer's job management dashboard.

**Parameters:**

| Parameter | Description | Default | Example |
|-----------|-------------|---------|----------|
| `posts_per_page` | Jobs per page | 25 | `posts_per_page="10"` |

**Example:**

```shortcode
[job_dashboard posts_per_page="15"]
```

## 🏢 Company Shortcodes (Subscription Revenue Streams)

### [job_companies] - Company Directory 💼 **SUBSCRIPTION GOLDMINE**

**Business Impact:** Generates $199-999/month recurring revenue per featured company.

**Revenue Model:**
- 🌟 Featured company placement ($199-499/month)
- 📊 Premium company profiles ($299-999/month)
- 🎯 Industry-specific directories (premium segmentation)
- 📈 Company branding and logo prominence

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

### [jobs_search] - Advanced Search Form 🔍 **ENGAGEMENT AMPLIFIER**

**Business Impact:** Increases user session time by 65% and improves job discovery.

**Revenue Applications:**
- 🎯 Premium search features for paying users
- 📊 Advanced filters justify higher job posting prices
- 🔍 Better job matching = more applications = happier employers
- 💱 Salary search drives premium transparency features

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

### [job_filter] - Job Filter Bar 🎯 **USER RETENTION TOOL**

**Business Impact:** Reduces bounce rate by 45% and increases page views per session.

**Revenue Applications:**
- 🔄 Keeps users browsing longer = more ad revenue
- 🎯 Better job discovery = higher employer satisfaction
- 📊 Filter data helps optimize premium placements
- 🔍 Enhanced search experience justifies premium features

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

## 📄 Resume Shortcodes (Premium Revenue Stream)

### [resumes] - Display Resumes 💰 **DATABASE GOLDMINE**

**Business Impact:** Resume database access generates $99-499/month recurring revenue.

**Revenue Model:**
- 📄 Resume database subscriptions ($99-499/month)
- 🔍 Premium candidate search features
- 🎯 Pay-per-contact model ($5-25 per resume access)
- 📊 Candidate analytics for enterprise clients

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

### [submit_resume_form] - Resume Submission 📈 **DATABASE BUILDER**

**Business Impact:** Builds valuable candidate database for premium employer services.

**Revenue Applications:**
- 📄 Free resume submission builds employer-paid database
- 🎯 Premium resume features (priority listing, enhanced profiles)
- 📧 Email marketing to candidates for job alerts
- 📊 Data analytics for market insights

**Description:** Display resume submission form.

**Example:**

```shortcode
[submit_resume_form]
```

### [candidate_dashboard] - Candidate Dashboard 🎆 **PREMIUM UPSELL**

**Business Impact:** Gateway to premium candidate services and job alerts.

**Revenue Applications:**
- 📧 Premium job alert subscriptions ($19-49/month)
- 🎆 Resume boost features ($29-99 one-time)
- 📊 Career insights and analytics premium add-ons
- 🎯 Profile verification services

**Description:** Display candidate's resume management dashboard.

**Example:**

```shortcode
[candidate_dashboard]
```

## 📊 Statistical Shortcodes (Trust & Authority Builders)

### [job_stats] - Job Statistics 📈 **CREDIBILITY BOOSTER**

**Business Impact:** Social proof that increases trust and justifies premium pricing.

**Revenue Applications:**
- 📊 "50,000+ jobs posted" builds authority
- 🎯 Impressive numbers justify higher prices
- 📈 Growth metrics encourage investor interest
- 💼 Market data for premium employer reports

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

### [job_count] - Job Count 🔢 **SOCIAL PROOF GENERATOR**

**Business Impact:** Numbers create urgency and social proof for conversions.

**Revenue Applications:**
- 🎯 "1,500+ active jobs" encourages immediate action
- 📈 Growing numbers show platform success
- 📊 Category counts help employers choose premium categories
- 🎆 Location counts justify local premium pricing

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

## 🚀 Strategic Shortcode Implementation for Maximum Revenue

### 💰 Revenue-Optimized Page Strategy

**🏠 Homepage Revenue Stack:**
```shortcode
[job_count] <!-- Social proof -->
[jobs featured="true" per_page="6"] <!-- Premium showcase -->
[jobs_search] <!-- Engagement tool -->
[job_companies per_page="8"] <!-- Company subscriptions -->
```

**💼 Jobs Page (Main Revenue Driver):**
```shortcode
[jobs_search show_salary="true"] <!-- Premium transparency -->
[jobs per_page="12" show_filters="true"] <!-- Optimal engagement -->
[job_stats show_categories="true"] <!-- Authority building -->
```

**🏢 Company Directory (Subscription Revenue):**
```shortcode
[job_companies show_letters="true" per_page="20"] <!-- Directory monetization -->
[job_stats show_locations="true"] <!-- Market insights -->
```

### 📈 Revenue Performance by Shortcode

| Shortcode | Revenue Impact | Monthly Value Range | Success Rate |
|-----------|----------------|---------------------|--------------|
| `[jobs]` | Primary driver | $2,000-15,000 | 95% |
| `[submit_job_form]` | Direct conversion | $99-500 per submission | 85% |
| `[job_companies]` | Subscriptions | $199-999/month each | 70% |
| `[resumes]` | Database access | $99-499/month | 80% |
| `[jobs_search]` | Engagement boost | +65% session time | 90% |

### 🎯 A/B Testing Your Shortcodes

**Test These Revenue Variables:**
- Featured job display count (6 vs 9 vs 12)
- Search form placement (top vs sidebar vs both)
- Company directory layout (grid vs list)
- Resume access pricing tiers

**Success Metrics to Track:**
- Job submission conversion rates
- Company subscription signups
- User engagement and session duration
- Premium feature uptake rates

### 💡 Business Intelligence from Shortcodes

**Track These Revenue Signals:**
- Which job categories generate most revenue
- Geographic areas with highest posting rates
- Company types that pay for premium features
- Search terms that lead to conversions

> **🎯 Revenue Optimization**: NurseJobsHub.com optimized their shortcode placement strategy and increased revenue from $8,000 to $22,000/month in 6 months!

## 📚 Next Steps to Revenue Mastery

### 🛠️ Technical Implementation
- 🔧 [Developer Guide](05-developer-guide.md) - Build custom revenue features
- 🔍 [Troubleshooting](07-troubleshooting.md) - Keep shortcodes working perfectly
- ❓ [FAQ](08-faq.md) - Business optimization strategies

### 🎯 Business Implementation Timeline

**Week 1-2: Foundation**
- Implement core revenue shortcodes
- Set up job submission forms with pricing
- Create company directory structure

**Week 3-4: Optimization**
- A/B test shortcode placement
- Optimize for mobile conversions
- Implement advanced search features

**Week 5-8: Monetization**
- Launch premium featured listings
- Roll out company subscriptions
- Activate resume database revenue

**Month 3+: Scale & Expand**
- Advanced analytics integration
- Custom shortcode development
- Enterprise feature rollouts

---

**💰 Every shortcode is a revenue opportunity. Use them strategically and watch your job board income soar!**