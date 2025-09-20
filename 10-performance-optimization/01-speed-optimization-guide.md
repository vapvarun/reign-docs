# Speed Optimization Guide for Reign Theme

## Overview

Reign theme includes built-in performance features and supports advanced optimization techniques to ensure fast page load times and excellent user experience.

## Smart Performance Mode

### Enabling Smart Performance

**Location:** Appearance → Customize → General → Site Performance

**Features:**
```
✓ Smart Widget Detection
✓ Conditional Asset Loading
✓ Plugin-Specific Optimization
✓ Lazy Loading
✓ Script Deferring
```

### How It Works

The theme automatically:
- Detects active widgets per page
- Loads only required CSS/JS
- Optimizes 22+ plugin integrations
- Eliminates unnecessary database queries

## Asset Loading Optimization

### CSS Optimization

#### Minification
```
Enable CSS Minification: ✓
Combine CSS Files: ✓
Remove Unused CSS: ✓
Inline Critical CSS: ✓
```

#### CSS Loading Strategy
1. **Critical CSS** - Inline above-fold styles
2. **Main CSS** - Async load main stylesheet
3. **Component CSS** - Load only when needed
4. **Print CSS** - Load only for printing

### JavaScript Optimization

#### Script Management
```
Minify JavaScript: ✓
Combine JS Files: ✓
Defer JavaScript: ✓
Remove jQuery Migrate: ✓
```

#### Loading Strategies
- **Defer** - Non-critical scripts
- **Async** - Independent scripts
- **Inline** - Critical small scripts
- **Footer** - Non-essential scripts

## Image Optimization

### Lazy Loading

**Enable for:**
```
✓ Images
✓ Iframes
✓ Videos
✓ Background Images
```

**Settings:**
```
Offset: 100px (start loading before visible)
Placeholder: Blur / Color / None
Exclude: First 2 images (above fold)
```

### Image Formats

**Recommended Formats:**
- **WebP** - 25-35% smaller than JPEG
- **AVIF** - Next-gen format
- **SVG** - For icons and logos

**Implementation:**
```html
<picture>
  <source srcset="image.avif" type="image/avif">
  <source srcset="image.webp" type="image/webp">
  <img src="image.jpg" alt="Description">
</picture>
```

### Image Sizing

**Responsive Images:**
```
Thumbnail: 150x150
Medium: 300x300
Large: 1024x1024
Full: Original
Custom: As needed
```

## Database Optimization

### Query Optimization

**Reduce Queries:**
1. Enable object caching
2. Optimize widget queries
3. Limit post revisions
4. Clean transients regularly

**Database Cleanup:**
```sql
-- Clean revisions
DELETE FROM wp_posts WHERE post_type = 'revision';

-- Clean transients
DELETE FROM wp_options WHERE option_name LIKE '%_transient_%';

-- Optimize tables
OPTIMIZE TABLE wp_posts, wp_postmeta, wp_options;
```

### Transient Management

**Best Practices:**
- Set appropriate expiration
- Clear expired transients
- Use object cache
- Monitor transient size

## Caching Strategy

### Browser Caching

**.htaccess Configuration:**
```apache
# Browser Caching
<IfModule mod_expires.c>
ExpiresActive On
ExpiresByType image/jpg "access 1 year"
ExpiresByType image/jpeg "access 1 year"
ExpiresByType image/gif "access 1 year"
ExpiresByType image/png "access 1 year"
ExpiresByType image/webp "access 1 year"
ExpiresByType text/css "access 1 month"
ExpiresByType text/javascript "access 1 month"
</IfModule>
```

### Page Caching

**Recommended Plugins:**
1. **WP Rocket** - Premium, comprehensive
2. **W3 Total Cache** - Free, powerful
3. **WP Super Cache** - Simple, effective
4. **LiteSpeed Cache** - Server-level

### Object Caching

**Options:**
- Redis (recommended)
- Memcached
- APCu
- Database (fallback)

## CDN Integration

### Setting Up CDN

**Popular CDNs:**
- Cloudflare (free tier)
- Amazon CloudFront
- KeyCDN
- BunnyCDN

**Configuration:**
```
CDN URL: https://cdn.example.com
File Types: CSS, JS, Images, Fonts
Exclude: Admin, Dynamic Content
```

### CDN Benefits
- Global distribution
- Reduced server load
- Faster delivery
- DDoS protection

## Font Optimization

### Font Loading

**Strategies:**
```css
/* Preload critical fonts */
<link rel="preload" href="font.woff2" as="font" crossorigin>

/* Font-display swap */
@font-face {
  font-family: 'CustomFont';
  font-display: swap;
  src: url('font.woff2') format('woff2');
}
```

### Font Subsetting

**Include Only Used Characters:**
- Latin subset for English
- Remove unused glyphs
- Separate icon fonts

## Critical CSS

### Generating Critical CSS

**Process:**
1. Identify above-fold content
2. Extract required CSS
3. Inline in `<head>`
4. Load remaining CSS async

**Tools:**
- Critical (npm package)
- Penthouse
- Critical CSS Generator

## Core Web Vitals

### Metrics to Monitor

#### LCP (Largest Contentful Paint)
**Target:** < 2.5 seconds
**Optimization:**
- Optimize images
- Reduce server response time
- Eliminate render-blocking resources

#### FID (First Input Delay)
**Target:** < 100 milliseconds
**Optimization:**
- Minimize JavaScript
- Break up long tasks
- Use web workers

#### CLS (Cumulative Layout Shift)
**Target:** < 0.1
**Optimization:**
- Set image dimensions
- Reserve space for ads
- Avoid inserting content above existing content

## Plugin-Specific Optimization

### BuddyPress
```
✓ Disable unused components
✓ Limit activity stream items
✓ Cache member queries
✓ Optimize avatar sizes
```

### WooCommerce
```
✓ Limit products per page
✓ Disable cart fragments (if not needed)
✓ Optimize product images
✓ Use transients for complex queries
```

### Elementor
```
✓ Disable unused widgets
✓ Optimize DOM output
✓ Enable improved asset loading
✓ Disable Google Fonts (use system)
```

## Server Optimization

### PHP Configuration

**Recommended Settings:**
```ini
memory_limit = 256M
max_execution_time = 300
max_input_vars = 3000
post_max_size = 64M
upload_max_filesize = 64M
```

### PHP Version
- Minimum: PHP 7.4
- Recommended: PHP 8.1+
- Benefits: 30% faster execution

### Server Software
- **Apache** - with mod_rewrite, mod_expires
- **Nginx** - with FastCGI cache
- **LiteSpeed** - with LSCache

## Monitoring Performance

### Tools for Testing

**Online Tools:**
- Google PageSpeed Insights
- GTmetrix
- WebPageTest
- Lighthouse (Chrome DevTools)

**WordPress Plugins:**
- Query Monitor
- P3 Plugin Performance Profiler
- WP Performance Score Booster

### Key Metrics

**Monitor:**
- Page Load Time
- Time to First Byte (TTFB)
- Total Page Size
- Number of Requests
- Core Web Vitals

## Advanced Techniques

### Preloading & Prefetching

```html
<!-- DNS Prefetch -->
<link rel="dns-prefetch" href="//fonts.googleapis.com">

<!-- Preconnect -->
<link rel="preconnect" href="https://fonts.gstatic.com">

<!-- Prefetch -->
<link rel="prefetch" href="page2.html">

<!-- Preload -->
<link rel="preload" href="style.css" as="style">
```

### Resource Hints

**Implementation:**
```php
function reign_resource_hints($hints, $relation_type) {
    if ('dns-prefetch' === $relation_type) {
        $hints[] = 'https://fonts.googleapis.com';
        $hints[] = 'https://www.google-analytics.com';
    }
    return $hints;
}
add_filter('wp_resource_hints', 'reign_resource_hints', 10, 2);
```

## Troubleshooting

### Common Issues

#### Slow Initial Load
- Check hosting quality
- Review plugin count
- Optimize database
- Enable caching

#### High TTFB
- Upgrade hosting
- Use page caching
- Optimize database queries
- Check DNS resolution

#### Layout Shifts
- Set image dimensions
- Avoid dynamic content injection
- Use CSS transforms for animations

## Best Practices Checklist

### Essential Optimizations
- [ ] Enable Smart Performance Mode
- [ ] Configure caching plugin
- [ ] Optimize images (WebP/compression)
- [ ] Enable lazy loading
- [ ] Minify CSS/JS
- [ ] Set up CDN
- [ ] Optimize database
- [ ] Use latest PHP version
- [ ] Monitor Core Web Vitals
- [ ] Regular performance audits

### Advanced Optimizations
- [ ] Implement Critical CSS
- [ ] Configure object caching
- [ ] Use resource hints
- [ ] Optimize fonts
- [ ] Enable HTTP/2
- [ ] Configure browser caching
- [ ] Implement service workers
- [ ] Use edge caching