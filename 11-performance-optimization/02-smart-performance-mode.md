# Smart Performance Mode Documentation

## Overview

Smart Performance Mode is Reign Theme's intelligent optimization system that automatically improves website speed and performance. It analyzes your site's usage patterns and applies targeted optimizations without requiring technical knowledge.

## What is Smart Performance Mode?

Smart Performance Mode is an automated performance optimization feature that:
- **Analyzes** your site's performance bottlenecks
- **Optimizes** resources based on usage patterns
- **Adapts** to your specific content and traffic
- **Monitors** performance improvements
- **Reports** optimization results

## Activation

### Enabling Smart Performance

**Location:** `Customizer → General → Site Performance`

```
Smart Performance Mode: ON
Optimization Level: Balanced / Aggressive / Conservative
Auto-Optimize: Yes
Performance Monitoring: Yes
Debug Mode: No
```

### Quick Enable via Code

```php
// Enable Smart Performance Mode programmatically
add_filter('reign_smart_performance_enabled', '__return_true');

// Set optimization level
add_filter('reign_smart_performance_level', function() {
    return 'aggressive'; // 'conservative', 'balanced', 'aggressive'
});
```

## Core Optimizations

### 1. Asset Optimization

#### CSS Optimization
```php
// Automatic CSS minification
class Reign_CSS_Optimizer {
    public function __construct() {
        if (get_theme_mod('reign_smart_performance', true)) {
            add_filter('style_loader_tag', array($this, 'optimize_css'), 10, 2);
            add_action('wp_head', array($this, 'critical_css'), 5);
        }
    }

    public function optimize_css($tag, $handle) {
        // Minify CSS
        if (!strpos($tag, '.min.css')) {
            $tag = str_replace('.css', '.min.css', $tag);
        }

        // Defer non-critical CSS
        $critical_handles = array('reign-style', 'reign-layout');
        if (!in_array($handle, $critical_handles)) {
            $tag = str_replace("rel='stylesheet'", "rel='preload' as='style' onload=\"this.onload=null;this.rel='stylesheet'\"", $tag);
        }

        return $tag;
    }

    public function critical_css() {
        // Inline critical CSS
        $critical = get_option('reign_critical_css');
        if ($critical) {
            echo '<style id="reign-critical-css">' . $critical . '</style>';
        }
    }
}
```

#### JavaScript Optimization
```php
// Smart JS loading
class Reign_JS_Optimizer {
    private $deferred_scripts = array();

    public function __construct() {
        add_filter('script_loader_tag', array($this, 'optimize_js'), 10, 3);
        add_action('wp_footer', array($this, 'load_deferred_scripts'), 999);
    }

    public function optimize_js($tag, $handle, $src) {
        // Core scripts that should load immediately
        $critical_scripts = array('jquery', 'jquery-core', 'reign-critical');

        if (!in_array($handle, $critical_scripts)) {
            // Defer non-critical scripts
            if (!is_admin()) {
                $this->deferred_scripts[$handle] = $src;
                return ''; // Remove from initial load
            }
        }

        // Add async to third-party scripts
        if (strpos($src, home_url()) === false) {
            $tag = str_replace(' src', ' async src', $tag);
        }

        return $tag;
    }

    public function load_deferred_scripts() {
        if (!empty($this->deferred_scripts)) {
            ?>
            <script>
            window.addEventListener('load', function() {
                <?php foreach ($this->deferred_scripts as $handle => $src): ?>
                var script_<?php echo $handle; ?> = document.createElement('script');
                script_<?php echo $handle; ?>.src = '<?php echo $src; ?>';
                document.body.appendChild(script_<?php echo $handle; ?>);
                <?php endforeach; ?>
            });
            </script>
            <?php
        }
    }
}
```

### 2. Image Optimization

#### Lazy Loading
```php
// Smart image lazy loading
class Reign_Image_Optimizer {
    public function __construct() {
        add_filter('the_content', array($this, 'add_lazy_loading'));
        add_filter('post_thumbnail_html', array($this, 'lazy_load_thumbnails'));
        add_action('wp_head', array($this, 'lazy_load_css'));
    }

    public function add_lazy_loading($content) {
        if (!is_feed() && !is_admin()) {
            $content = preg_replace_callback('/<img([^>]+)>/i', function($matches) {
                $img = $matches[0];

                // Skip if already has loading attribute
                if (strpos($img, 'loading=') !== false) {
                    return $img;
                }

                // Add native lazy loading
                $img = str_replace('<img', '<img loading="lazy"', $img);

                // Add data-src for JavaScript fallback
                $img = preg_replace('/src="([^"]+)"/i', 'src="data:image/svg+xml,%3Csvg xmlns=\'http://www.w3.org/2000/svg\' viewBox=\'0 0 1 1\'%3E%3C/svg%3E" data-src="$1"', $img);

                // Add lazy class
                $img = str_replace('<img', '<img class="lazy-load"', $img);

                return $img;
            }, $content);
        }
        return $content;
    }

    public function lazy_load_css() {
        ?>
        <style>
        img.lazy-load {
            opacity: 0;
            transition: opacity 0.3s;
        }
        img.lazy-load.loaded {
            opacity: 1;
        }
        </style>
        <?php
    }
}
```

#### WebP Conversion
```php
// Automatic WebP serving
add_filter('wp_generate_attachment_metadata', function($metadata, $attachment_id) {
    if (!reign_is_smart_performance_enabled()) {
        return $metadata;
    }

    $file = get_attached_file($attachment_id);
    $info = pathinfo($file);

    // Convert to WebP
    if (in_array($info['extension'], array('jpg', 'jpeg', 'png'))) {
        $webp_file = $info['dirname'] . '/' . $info['filename'] . '.webp';

        // Use GD or Imagick to convert
        if (extension_loaded('imagick')) {
            $image = new Imagick($file);
            $image->setImageFormat('webp');
            $image->setImageCompressionQuality(85);
            $image->writeImage($webp_file);
        } elseif (function_exists('imagewebp')) {
            $image = imagecreatefromstring(file_get_contents($file));
            imagewebp($image, $webp_file, 85);
            imagedestroy($image);
        }
    }

    return $metadata;
}, 10, 2);
```

### 3. Database Optimization

#### Query Optimization
```php
// Smart query caching
class Reign_Query_Optimizer {
    private $query_cache = array();

    public function __construct() {
        add_filter('posts_request', array($this, 'cache_queries'), 10, 2);
        add_action('save_post', array($this, 'clear_query_cache'));
        add_action('deleted_post', array($this, 'clear_query_cache'));
    }

    public function cache_queries($request, $query) {
        if (!is_admin() && !$query->is_singular()) {
            $cache_key = md5($request);

            // Check cache
            if (isset($this->query_cache[$cache_key])) {
                return $this->query_cache[$cache_key];
            }

            // Check transient cache
            $cached = get_transient('reign_query_' . $cache_key);
            if ($cached !== false) {
                $this->query_cache[$cache_key] = $cached;
                return $cached;
            }

            // Store in transient
            set_transient('reign_query_' . $cache_key, $request, 5 * MINUTE_IN_SECONDS);
        }

        return $request;
    }

    public function clear_query_cache() {
        global $wpdb;
        $wpdb->query("DELETE FROM {$wpdb->options} WHERE option_name LIKE '_transient_reign_query_%'");
    }
}
```

#### Autoloaded Options
```php
// Optimize autoloaded options
add_action('init', function() {
    if (!reign_is_smart_performance_enabled()) return;

    // Options that don't need to be autoloaded
    $no_autoload = array(
        'reign_performance_report',
        'reign_cache_stats',
        'reign_optimization_log'
    );

    foreach ($no_autoload as $option) {
        $value = get_option($option);
        if ($value !== false) {
            delete_option($option);
            add_option($option, $value, '', 'no');
        }
    }
});
```

### 4. Widget & Sidebar Optimization

#### Widget Caching
```php
// Cache widget output
class Reign_Widget_Cache {
    public function __construct() {
        add_filter('widget_display_callback', array($this, 'cache_widget_output'), 10, 3);
        add_action('save_post', array($this, 'clear_widget_cache'));
    }

    public function cache_widget_output($instance, $widget, $args) {
        if (is_admin() || !reign_is_smart_performance_enabled()) {
            return $instance;
        }

        $cache_key = 'reign_widget_' . md5($widget->id . serialize($instance));
        $cached_output = get_transient($cache_key);

        if ($cached_output === false) {
            ob_start();
            $widget->widget($args, $instance);
            $cached_output = ob_get_clean();
            set_transient($cache_key, $cached_output, HOUR_IN_SECONDS);
        }

        echo $cached_output;
        return false; // Prevent default widget display
    }

    public function clear_widget_cache() {
        global $wpdb;
        $wpdb->query("DELETE FROM {$wpdb->options} WHERE option_name LIKE '_transient_reign_widget_%'");
    }
}
```

### 5. BuddyPress Optimization

#### Activity Stream Optimization
```php
// Optimize BuddyPress queries
add_filter('bp_activity_get_where_conditions', function($where, $args) {
    if (!reign_is_smart_performance_enabled()) {
        return $where;
    }

    // Add index hints for better performance
    global $wpdb;
    $bp = buddypress();

    // Optimize date queries
    if (!empty($args['since'])) {
        $where['since'] = $wpdb->prepare(
            "a.date_recorded > %s",
            $args['since']
        );
    }

    return $where;
}, 10, 2);

// Cache member queries
add_filter('bp_core_get_users', function($users, $args) {
    if (!reign_is_smart_performance_enabled()) {
        return $users;
    }

    $cache_key = 'reign_bp_users_' . md5(serialize($args));
    $cached = get_transient($cache_key);

    if ($cached === false) {
        set_transient($cache_key, $users, 15 * MINUTE_IN_SECONDS);
    } else {
        return $cached;
    }

    return $users;
}, 10, 2);
```

## Advanced Features

### Resource Hints

```php
// Add resource hints for better performance
add_action('wp_head', function() {
    if (!reign_is_smart_performance_enabled()) return;

    // DNS Prefetch
    $domains = array(
        '//fonts.googleapis.com',
        '//fonts.gstatic.com',
        '//www.google-analytics.com',
        '//connect.facebook.net'
    );

    foreach ($domains as $domain) {
        echo '<link rel="dns-prefetch" href="' . $domain . '">' . "\n";
    }

    // Preconnect
    echo '<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>' . "\n";

    // Preload critical resources
    $critical_resources = array(
        get_theme_file_uri('/assets/css/critical.min.css') => 'style',
        get_theme_file_uri('/assets/fonts/main.woff2') => 'font'
    );

    foreach ($critical_resources as $resource => $as) {
        $type = $as === 'font' ? ' type="font/woff2" crossorigin' : '';
        echo '<link rel="preload" href="' . $resource . '" as="' . $as . '"' . $type . '>' . "\n";
    }
}, 1);
```

### Adaptive Loading

```javascript
// Adaptive resource loading based on connection
class AdaptiveLoader {
    constructor() {
        this.connection = navigator.connection || navigator.mozConnection || navigator.webkitConnection;
        this.init();
    }

    init() {
        if (this.connection) {
            this.loadBasedOnConnection();
            this.connection.addEventListener('change', () => this.loadBasedOnConnection());
        }
    }

    loadBasedOnConnection() {
        const effectiveType = this.connection.effectiveType;
        const saveData = this.connection.saveData;

        document.body.className = document.body.className.replace(/connection-\S+/g, '');
        document.body.classList.add('connection-' + effectiveType);

        if (saveData || effectiveType === 'slow-2g' || effectiveType === '2g') {
            // Low quality mode
            this.enableLowQualityMode();
        } else if (effectiveType === '3g') {
            // Medium quality mode
            this.enableMediumQualityMode();
        } else {
            // High quality mode
            this.enableHighQualityMode();
        }
    }

    enableLowQualityMode() {
        // Disable autoplay
        document.querySelectorAll('video').forEach(video => {
            video.autoplay = false;
            video.preload = 'none';
        });

        // Load low-res images
        document.querySelectorAll('img[data-lowsrc]').forEach(img => {
            img.src = img.dataset.lowsrc;
        });

        // Disable animations
        document.body.classList.add('reduce-motion');
    }

    enableMediumQualityMode() {
        // Standard quality
        document.querySelectorAll('img[data-src]').forEach(img => {
            img.src = img.dataset.src;
        });
    }

    enableHighQualityMode() {
        // Load high-res images
        document.querySelectorAll('img[data-highsrc]').forEach(img => {
            img.src = img.dataset.highsrc;
        });

        // Enable all features
        document.body.classList.add('high-quality');
    }
}

// Initialize
document.addEventListener('DOMContentLoaded', () => new AdaptiveLoader());
```

## Performance Monitoring

### Real User Monitoring (RUM)

```javascript
// Performance monitoring
class PerformanceMonitor {
    constructor() {
        this.metrics = {};
        this.init();
    }

    init() {
        // Navigation Timing
        window.addEventListener('load', () => {
            const perfData = performance.getEntriesByType('navigation')[0];

            this.metrics = {
                dns: perfData.domainLookupEnd - perfData.domainLookupStart,
                tcp: perfData.connectEnd - perfData.connectStart,
                ttfb: perfData.responseStart - perfData.requestStart,
                download: perfData.responseEnd - perfData.responseStart,
                domInteractive: perfData.domInteractive - perfData.fetchStart,
                domComplete: perfData.domComplete - perfData.fetchStart,
                loadComplete: perfData.loadEventEnd - perfData.fetchStart
            };

            this.reportMetrics();
        });

        // Core Web Vitals
        this.measureWebVitals();
    }

    measureWebVitals() {
        // Largest Contentful Paint
        new PerformanceObserver((list) => {
            const entries = list.getEntries();
            const lastEntry = entries[entries.length - 1];
            this.metrics.lcp = lastEntry.renderTime || lastEntry.loadTime;
        }).observe({entryTypes: ['largest-contentful-paint']});

        // First Input Delay
        new PerformanceObserver((list) => {
            const entry = list.getEntries()[0];
            this.metrics.fid = entry.processingStart - entry.startTime;
        }).observe({entryTypes: ['first-input']});

        // Cumulative Layout Shift
        let clsValue = 0;
        new PerformanceObserver((list) => {
            for (const entry of list.getEntries()) {
                if (!entry.hadRecentInput) {
                    clsValue += entry.value;
                }
            }
            this.metrics.cls = clsValue;
        }).observe({entryTypes: ['layout-shift']});
    }

    reportMetrics() {
        // Send metrics to server
        if (navigator.sendBeacon) {
            navigator.sendBeacon('/wp-admin/admin-ajax.php', JSON.stringify({
                action: 'reign_performance_metrics',
                metrics: this.metrics,
                url: window.location.href,
                timestamp: Date.now()
            }));
        }
    }
}

// Initialize monitoring
if (window.performance && window.PerformanceObserver) {
    new PerformanceMonitor();
}
```

### Performance Dashboard

```php
// Display performance metrics in admin
add_action('admin_menu', function() {
    add_submenu_page(
        'reign-settings',
        'Performance Report',
        'Performance',
        'manage_options',
        'reign-performance',
        'reign_performance_dashboard'
    );
});

function reign_performance_dashboard() {
    $metrics = get_option('reign_performance_metrics', array());
    ?>
    <div class="wrap">
        <h1>Performance Dashboard</h1>

        <div class="performance-cards">
            <div class="card">
                <h3>Page Load Time</h3>
                <div class="metric"><?php echo $metrics['avg_load_time'] ?? 'N/A'; ?>s</div>
                <div class="trend <?php echo $metrics['load_trend'] ?? ''; ?>"></div>
            </div>

            <div class="card">
                <h3>Core Web Vitals</h3>
                <ul>
                    <li>LCP: <?php echo $metrics['lcp'] ?? 'N/A'; ?>s</li>
                    <li>FID: <?php echo $metrics['fid'] ?? 'N/A'; ?>ms</li>
                    <li>CLS: <?php echo $metrics['cls'] ?? 'N/A'; ?></li>
                </ul>
            </div>

            <div class="card">
                <h3>Optimization Status</h3>
                <ul>
                    <li>CSS Minified: <?php echo $metrics['css_minified'] ? '✓' : '✗'; ?></li>
                    <li>JS Deferred: <?php echo $metrics['js_deferred'] ? '✓' : '✗'; ?></li>
                    <li>Images Optimized: <?php echo $metrics['images_optimized'] ? '✓' : '✗'; ?></li>
                    <li>Cache Enabled: <?php echo $metrics['cache_enabled'] ? '✓' : '✗'; ?></li>
                </ul>
            </div>
        </div>

        <div class="performance-graph">
            <canvas id="performance-chart"></canvas>
        </div>

        <div class="optimization-suggestions">
            <h2>Optimization Suggestions</h2>
            <?php reign_get_optimization_suggestions(); ?>
        </div>
    </div>
    <?php
}
```

## Configuration Options

### Performance Levels

#### Conservative Mode
```php
// Minimal optimizations for compatibility
add_filter('reign_performance_config', function($config) {
    return array(
        'minify_css' => true,
        'minify_js' => false,
        'defer_js' => false,
        'lazy_load' => true,
        'critical_css' => false,
        'webp' => false,
        'cache_widgets' => true,
        'optimize_db' => false
    );
});
```

#### Balanced Mode (Default)
```php
// Good balance of speed and compatibility
add_filter('reign_performance_config', function($config) {
    return array(
        'minify_css' => true,
        'minify_js' => true,
        'defer_js' => true,
        'lazy_load' => true,
        'critical_css' => true,
        'webp' => true,
        'cache_widgets' => true,
        'optimize_db' => true
    );
});
```

#### Aggressive Mode
```php
// Maximum performance optimizations
add_filter('reign_performance_config', function($config) {
    return array(
        'minify_css' => true,
        'minify_js' => true,
        'defer_js' => true,
        'lazy_load' => true,
        'critical_css' => true,
        'webp' => true,
        'cache_widgets' => true,
        'optimize_db' => true,
        'remove_emojis' => true,
        'disable_embeds' => true,
        'limit_revisions' => 3,
        'disable_pingbacks' => true,
        'remove_query_strings' => true
    );
});
```

## Troubleshooting

### Common Issues

#### JavaScript Errors After Enabling

```php
// Exclude specific scripts from optimization
add_filter('reign_performance_exclude_scripts', function($excluded) {
    $excluded[] = 'critical-plugin-script';
    $excluded[] = 'payment-gateway';
    return $excluded;
});
```

#### Broken Layout

```php
// Exclude critical CSS from optimization
add_filter('reign_performance_critical_styles', function($critical) {
    $critical[] = 'theme-layout';
    $critical[] = 'grid-system';
    return $critical;
});
```

#### Images Not Loading

```javascript
// Fallback for lazy loading
document.addEventListener('DOMContentLoaded', function() {
    // Check if native lazy loading is supported
    if (!('loading' in HTMLImageElement.prototype)) {
        // Fallback to JavaScript solution
        const images = document.querySelectorAll('img[loading="lazy"]');
        const imageObserver = new IntersectionObserver((entries, observer) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    const img = entry.target;
                    img.src = img.dataset.src;
                    observer.unobserve(img);
                }
            });
        });

        images.forEach(img => imageObserver.observe(img));
    }
});
```

## Best Practices

### 1. Test Before Production

```php
// Enable testing mode
define('REIGN_PERFORMANCE_TEST', true);

// Test specific optimizations
add_filter('reign_performance_test_features', function() {
    return array('critical_css', 'defer_js');
});
```

### 2. Monitor Impact

```php
// Log performance changes
add_action('reign_performance_applied', function($optimizations) {
    error_log('Performance optimizations applied: ' . json_encode($optimizations));
});
```

### 3. Gradual Rollout

```php
// Enable for specific user roles first
add_filter('reign_performance_enabled_for_user', function($enabled) {
    if (current_user_can('administrator')) {
        return true;
    }
    return false;
});
```

---

*For additional performance tips, see the Speed Optimization Guide.*