# SEO Optimization Complete Guide

## Overview

Search Engine Optimization is crucial for your Reign theme website's visibility. This guide covers technical SEO, content optimization, and best practices for ranking higher in search results.

## Technical SEO Foundation

### Site Structure

**URL Structure:**
```
Best Practices:
✓ example.com/category/post-name
✓ example.com/products/product-name
✓ example.com/courses/course-name

Avoid:
✗ example.com/?p=123
✗ example.com/2024/01/01/post
✗ example.com/very/deep/nested/structure/page
```

**Permalink Settings:**
```
Settings → Permalinks
Recommended: /%category%/%postname%/
Or: /%postname%/
```

### XML Sitemaps

**Generate Sitemaps:**
```xml
<!-- Main sitemap index -->
<?xml version="1.0" encoding="UTF-8"?>
<sitemapindex xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <sitemap>
        <loc>https://site.com/sitemap-posts.xml</loc>
    </sitemap>
    <sitemap>
        <loc>https://site.com/sitemap-pages.xml</loc>
    </sitemap>
    <sitemap>
        <loc>https://site.com/sitemap-products.xml</loc>
    </sitemap>
</sitemapindex>
```

**Submit to Search Engines:**
1. Google Search Console
2. Bing Webmaster Tools
3. Yandex Webmaster

### Robots.txt Configuration

```
User-agent: *
Disallow: /wp-admin/
Allow: /wp-admin/admin-ajax.php
Disallow: /wp-login.php
Disallow: /wp-register.php
Disallow: /?s=
Disallow: /search/
Disallow: /tag/
Disallow: /author/
Allow: /wp-content/uploads/

# BuddyPress specific
Disallow: /members/*/settings/
Disallow: /members/*/messages/

# WooCommerce specific
Disallow: /cart/
Disallow: /checkout/
Disallow: /my-account/

Sitemap: https://yoursite.com/sitemap.xml
```

### Schema Markup

**Organization Schema:**
```json
{
    "@context": "https://schema.org",
    "@type": "Organization",
    "name": "Your Site Name",
    "url": "https://yoursite.com",
    "logo": "https://yoursite.com/logo.png",
    "sameAs": [
        "https://facebook.com/yoursite",
        "https://twitter.com/yoursite",
        "https://linkedin.com/company/yoursite"
    ]
}
```

**Article Schema:**
```php
function reign_add_article_schema() {
    if (is_single()) {
        ?>
        <script type="application/ld+json">
        {
            "@context": "https://schema.org",
            "@type": "Article",
            "headline": "<?php the_title(); ?>",
            "author": {
                "@type": "Person",
                "name": "<?php the_author(); ?>"
            },
            "datePublished": "<?php echo get_the_date('c'); ?>",
            "dateModified": "<?php echo get_the_modified_date('c'); ?>",
            "image": "<?php the_post_thumbnail_url(); ?>",
            "publisher": {
                "@type": "Organization",
                "name": "<?php bloginfo('name'); ?>",
                "logo": {
                    "@type": "ImageObject",
                    "url": "<?php echo get_theme_mod('site_logo'); ?>"
                }
            }
        }
        </script>
        <?php
    }
}
add_action('wp_head', 'reign_add_article_schema');
```

## Page Speed Optimization

### Core Web Vitals

**LCP (Largest Contentful Paint):**
```
Target: < 2.5 seconds
Optimizations:
✓ Optimize hero images
✓ Preload critical resources
✓ Use CDN
✓ Minimize server response time
```

**FID (First Input Delay):**
```
Target: < 100 milliseconds
Optimizations:
✓ Minimize JavaScript
✓ Remove unused JS
✓ Defer non-critical JS
✓ Use web workers
```

**CLS (Cumulative Layout Shift):**
```
Target: < 0.1
Optimizations:
✓ Set image dimensions
✓ Reserve space for ads
✓ Avoid inserting content above existing content
✓ Use CSS transforms for animations
```

### Image Optimization

**Best Practices:**
```html
<!-- Responsive images with SEO -->
<img
    src="image.jpg"
    alt="Descriptive alt text with keywords"
    title="Image title"
    width="800"
    height="600"
    loading="lazy"
    srcset="image-400.jpg 400w,
            image-800.jpg 800w,
            image-1200.jpg 1200w"
    sizes="(max-width: 400px) 100vw,
           (max-width: 800px) 100vw,
           1200px"
>
```

**WebP Format:**
```html
<picture>
    <source srcset="image.webp" type="image/webp">
    <source srcset="image.jpg" type="image/jpeg">
    <img src="image.jpg" alt="SEO friendly description">
</picture>
```

## Content Optimization

### Title Tags

**Best Practices:**
```html
<!-- Format: Primary Keyword - Secondary Keyword | Brand Name -->
<title>WordPress Theme Development - Reign Theme Guide | YourSite</title>

<!-- Length: 50-60 characters -->
<!-- Include primary keyword -->
<!-- Make it compelling -->
```

**Dynamic Titles:**
```php
function reign_seo_title($title) {
    if (is_home()) {
        return get_bloginfo('name') . ' - ' . get_bloginfo('description');
    }
    if (is_category()) {
        return single_cat_title('', false) . ' - ' . get_bloginfo('name');
    }
    if (is_product()) {
        global $post;
        return $post->post_title . ' - Buy Online | ' . get_bloginfo('name');
    }
    return $title;
}
add_filter('pre_get_document_title', 'reign_seo_title');
```

### Meta Descriptions

**Optimal Length:** 150-160 characters
```php
function reign_meta_description() {
    $description = '';

    if (is_single()) {
        $description = get_the_excerpt();
    } elseif (is_page()) {
        $description = get_post_meta(get_the_ID(), '_meta_description', true);
    } elseif (is_category()) {
        $description = category_description();
    } elseif (is_home()) {
        $description = get_bloginfo('description');
    }

    if ($description) {
        echo '<meta name="description" content="' . esc_attr($description) . '">';
    }
}
add_action('wp_head', 'reign_meta_description');
```

### Header Tags Hierarchy

**Proper Structure:**
```html
<h1>Main Page Title (One per page)</h1>
    <h2>Main Section</h2>
        <h3>Subsection</h3>
            <h4>Sub-subsection</h4>
    <h2>Another Main Section</h2>
        <h3>Another Subsection</h3>
```

### Internal Linking

**Best Practices:**
```php
// Automatic internal linking
function reign_auto_internal_links($content) {
    $keywords = array(
        'BuddyPress' => '/buddypress-guide/',
        'WooCommerce' => '/woocommerce-setup/',
        'performance' => '/speed-optimization/',
    );

    foreach ($keywords as $keyword => $link) {
        $content = str_replace(
            $keyword,
            '<a href="' . $link . '">' . $keyword . '</a>',
            $content
        );
    }

    return $content;
}
add_filter('the_content', 'reign_auto_internal_links');
```

## BuddyPress SEO

### Member Profiles

**SEO-Friendly URLs:**
```
Before: site.com/members/?user=john
After: site.com/members/john/
```

**Member Meta Tags:**
```php
function reign_bp_member_meta() {
    if (bp_is_user()) {
        $user = bp_get_displayed_user();
        ?>
        <meta property="og:title" content="<?php echo $user->display_name; ?> - Member Profile">
        <meta property="og:description" content="<?php echo bp_get_member_profile_data('field=Bio'); ?>">
        <meta property="og:image" content="<?php echo bp_get_displayed_user_avatar('type=full'); ?>">
        <meta property="og:url" content="<?php echo bp_displayed_user_domain(); ?>">
        <?php
    }
}
add_action('wp_head', 'reign_bp_member_meta');
```

### Groups SEO

**Group Visibility:**
```php
// Control group indexing
function reign_bp_group_robots() {
    if (bp_is_group()) {
        $group = groups_get_current_group();
        if ($group->status != 'public') {
            echo '<meta name="robots" content="noindex, nofollow">';
        }
    }
}
add_action('wp_head', 'reign_bp_group_robots');
```

## WooCommerce SEO

### Product Optimization

**Product Schema:**
```json
{
    "@context": "https://schema.org",
    "@type": "Product",
    "name": "Product Name",
    "description": "Product description",
    "image": "product-image.jpg",
    "sku": "SKU123",
    "offers": {
        "@type": "Offer",
        "price": "29.99",
        "priceCurrency": "USD",
        "availability": "https://schema.org/InStock"
    },
    "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.5",
        "reviewCount": "24"
    }
}
```

**Category Pages:**
```php
// Optimize category pages
function reign_woo_category_seo() {
    if (is_product_category()) {
        $term = get_queried_object();
        $meta_title = get_term_meta($term->term_id, 'meta_title', true);
        $meta_desc = get_term_meta($term->term_id, 'meta_description', true);

        if ($meta_title) {
            add_filter('woocommerce_page_title', function() use ($meta_title) {
                return $meta_title;
            });
        }
    }
}
add_action('init', 'reign_woo_category_seo');
```

## Mobile SEO

### Mobile-First Indexing

**Responsive Meta Tag:**
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**Mobile Optimization Checklist:**
```
✓ Responsive design
✓ Touch-friendly buttons (48px minimum)
✓ Readable font size (16px minimum)
✓ No horizontal scrolling
✓ Fast mobile page speed
✓ Accessible menus
✓ Optimized images
```

### AMP Implementation

**AMP Setup:**
```php
// Add AMP support
function reign_amp_support() {
    add_theme_support('amp', array(
        'paired' => true,
        'nav_menu_toggle' => array(
            'nav_container_class' => 'mobile-navigation',
        ),
        'nav_menu_dropdown' => array(
            'sub_menu_button_class' => 'dropdown-toggle',
        ),
    ));
}
add_action('after_setup_theme', 'reign_amp_support');
```

## Local SEO

### NAP Consistency

**Name, Address, Phone:**
```json
{
    "@context": "https://schema.org",
    "@type": "LocalBusiness",
    "name": "Business Name",
    "address": {
        "@type": "PostalAddress",
        "streetAddress": "123 Main St",
        "addressLocality": "City",
        "addressRegion": "State",
        "postalCode": "12345",
        "addressCountry": "US"
    },
    "telephone": "+1-555-555-5555",
    "openingHours": "Mo-Fr 09:00-17:00",
    "geo": {
        "@type": "GeoCoordinates",
        "latitude": "40.7128",
        "longitude": "-74.0060"
    }
}
```

## International SEO

### Hreflang Tags

**Multi-language Setup:**
```html
<link rel="alternate" hreflang="en" href="https://site.com/">
<link rel="alternate" hreflang="es" href="https://site.com/es/">
<link rel="alternate" hreflang="fr" href="https://site.com/fr/">
<link rel="alternate" hreflang="x-default" href="https://site.com/">
```

**WPML Integration:**
```php
function reign_wpml_hreflang() {
    if (function_exists('icl_get_languages')) {
        $languages = icl_get_languages('skip_missing=0');
        foreach ($languages as $lang) {
            echo '<link rel="alternate" hreflang="' . $lang['language_code'] . '" href="' . $lang['url'] . '">';
        }
    }
}
add_action('wp_head', 'reign_wpml_hreflang');
```

## SEO Plugins Integration

### Yoast SEO

**Custom Integration:**
```php
// Customize Yoast breadcrumbs
add_filter('wpseo_breadcrumb_links', function($links) {
    if (bp_is_user()) {
        $links[] = array(
            'text' => 'Members',
            'url' => bp_get_members_directory_permalink(),
        );
    }
    return $links;
});
```

### Rank Math

**Custom Settings:**
```php
// Add custom variables
add_filter('rank_math/vars/replacements', function($vars) {
    $vars['custom_var'] = array(
        'name' => 'Custom Variable',
        'description' => 'Custom variable description',
        'variable' => 'custom_var',
        'example' => 'example_value',
    );
    return $vars;
});
```

## Monitoring & Analytics

### Google Search Console

**Key Metrics to Monitor:**
```
- Search queries
- Click-through rate (CTR)
- Average position
- Index coverage
- Mobile usability
- Core Web Vitals
```

### Google Analytics 4

**Enhanced Tracking:**
```javascript
// Track custom events
gtag('event', 'course_enrollment', {
    'course_name': 'Course Title',
    'course_id': '123',
    'value': 99.00
});

gtag('event', 'member_signup', {
    'method': 'email'
});
```

## SEO Checklist

### On-Page SEO
- [ ] Unique title tags (50-60 chars)
- [ ] Meta descriptions (150-160 chars)
- [ ] H1 tag (one per page)
- [ ] Proper heading hierarchy
- [ ] Alt text for images
- [ ] Internal linking
- [ ] External linking to authority sites
- [ ] URL optimization
- [ ] Schema markup
- [ ] Open Graph tags

### Technical SEO
- [ ] XML sitemap
- [ ] Robots.txt
- [ ] 404 error handling
- [ ] 301 redirects
- [ ] Canonical URLs
- [ ] SSL certificate
- [ ] Mobile responsiveness
- [ ] Page speed optimization
- [ ] Core Web Vitals
- [ ] Crawl budget optimization

### Content SEO
- [ ] Keyword research
- [ ] Content length (1000+ words)
- [ ] Readability
- [ ] Unique content
- [ ] Fresh content updates
- [ ] FAQ sections
- [ ] User engagement metrics
- [ ] Social sharing buttons

## Best Practices

1. **Content Quality** - Focus on user value
2. **Page Speed** - Aim for <3 seconds load time
3. **Mobile First** - Design for mobile users
4. **User Experience** - Low bounce rate, high dwell time
5. **Regular Updates** - Keep content fresh
6. **Link Building** - Quality over quantity
7. **Local Citations** - NAP consistency
8. **Social Signals** - Share worthy content