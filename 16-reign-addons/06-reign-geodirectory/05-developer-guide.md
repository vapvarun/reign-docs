# Reign GeoDirectory Addon - Developer Guide

## What You'll Learn
This guide is for developers who want to extend, customize, or integrate the Reign GeoDirectory addon with other systems. We'll cover hooks, filters, API integration, and advanced customization techniques.

## Quick Overview
**Skill level:** Intermediate to Advanced PHP/WordPress
**Time to read:** 30-45 minutes
**Prerequisites:** PHP, WordPress hooks, JavaScript basics

---

## Part 1: Architecture Overview

### How the Addon Works

**Plugin structure:**
```
reign-geodirectory-addon/
├── includes/
│   ├── class-reign-gd-loader.php
│   ├── class-reign-gd-public.php
│   ├── class-reign-gd-admin.php
│   ├── class-reign-gd-customizer.php
│   ├── class-reign-gd-buddypress.php
│   └── class-reign-gd-maps.php
├── templates/
│   ├── listings/
│   ├── maps/
│   ├── search/
│   └── widgets/
├── assets/
│   ├── css/
│   ├── js/
│   └── images/
└── reign-geodirectory-addon.php
```

### Core Components

**Main classes and their purposes:**

```php
// Main plugin class
class Reign_GeoDirectory_Addon {
    // Handles initialization
    // Loads dependencies
    // Registers hooks
}

// Public-facing functionality
class Reign_GD_Public {
    // Frontend templates
    // Listing display
    // Map rendering
    // Search functionality
}

// Admin functionality
class Reign_GD_Admin {
    // Settings pages
    // Listing management
    // Import/export tools
}

// Customizer integration
class Reign_GD_Customizer {
    // Design settings
    // Layout options
    // Color schemes
}
```

---

## Part 2: Hooks & Filters

### Action Hooks

**Key action hooks for customization:**

```php
// Before listing display
add_action('reign_gd_before_listing', 'your_function');
function your_function($listing_id) {
    // Add custom content before listing
    echo '<div class="custom-content">Special Offer!</div>';
}

// After listing display
add_action('reign_gd_after_listing', 'your_function');

// Before map render
add_action('reign_gd_before_map', 'your_function');

// After search results
add_action('reign_gd_after_search_results', 'your_function');

// On listing submission
add_action('reign_gd_listing_submitted', 'your_function', 10, 2);
function your_function($listing_id, $user_id) {
    // Send notification, update meta, etc.
}

// On review submission
add_action('reign_gd_review_submitted', 'your_function', 10, 3);
function your_function($review_id, $listing_id, $rating) {
    // Process review data
}
```

### Filter Hooks

**Modify data and output:**

```php
// Filter listing data
add_filter('reign_gd_listing_data', 'modify_listing_data', 10, 2);
function modify_listing_data($data, $listing_id) {
    // Add custom fields
    $data['custom_field'] = get_post_meta($listing_id, 'custom_value', true);
    return $data;
}

// Filter search results
add_filter('reign_gd_search_results', 'modify_search_results', 10, 2);
function modify_search_results($results, $search_params) {
    // Customize search results
    return $results;
}

// Filter map markers
add_filter('reign_gd_map_markers', 'customize_markers', 10, 1);
function customize_markers($markers) {
    foreach ($markers as &$marker) {
        $marker['icon'] = 'custom-icon-url.png';
    }
    return $markers;
}

// Filter listing card HTML
add_filter('reign_gd_listing_card_html', 'customize_card', 10, 2);
function customize_card($html, $listing_id) {
    // Modify card HTML
    return $html;
}
```

### GeoDirectory Integration Hooks

**Work with GeoDirectory core:**

```php
// Extend GeoDirectory listing query
add_filter('geodir_widget_listings_query_args', 'custom_query_args');
function custom_query_args($args) {
    // Modify query parameters
    $args['meta_key'] = 'featured';
    $args['orderby'] = 'meta_value_num';
    return $args;
}

// Customize GeoDirectory tabs
add_filter('geodir_detail_page_tab_list_extend', 'add_custom_tab');
function add_custom_tab($tabs) {
    $tabs['custom_tab'] = array(
        'heading_text' => 'Custom Info',
        'is_active_tab' => false,
        'is_display' => true,
        'tab_content' => 'custom_tab_content'
    );
    return $tabs;
}
```

---

## Part 3: Custom Templates

### Template Override System

**How to override templates:**

1. **Copy template from plugin:**
   ```
   /plugins/reign-geodirectory-addon/templates/listings/listing-card.php
   ```

2. **Paste into theme:**
   ```
   /themes/your-theme/reign-geodirectory/listings/listing-card.php
   ```

3. **Customize as needed**

### Creating Custom Templates

**Listing card template example:**

```php
<?php
/**
 * Custom Listing Card Template
 * 
 * @package Reign_GeoDirectory
 */

// Get listing data
$listing = reign_gd_get_listing_data(get_the_ID());
$featured = $listing['featured'];
$rating = $listing['rating'];
?>

<div class="reign-gd-listing-card <?php echo $featured ? 'featured' : ''; ?>">
    <?php if (has_post_thumbnail()) : ?>
        <div class="listing-image">
            <?php the_post_thumbnail('medium'); ?>
            <?php if ($featured) : ?>
                <span class="featured-badge">Featured</span>
            <?php endif; ?>
        </div>
    <?php endif; ?>
    
    <div class="listing-content">
        <h3 class="listing-title">
            <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a>
        </h3>
        
        <?php if ($rating) : ?>
            <div class="listing-rating">
                <?php echo reign_gd_display_rating($rating); ?>
            </div>
        <?php endif; ?>
        
        <div class="listing-meta">
            <?php echo reign_gd_get_location_string($listing['location']); ?>
            <?php echo reign_gd_get_category_badges($listing['categories']); ?>
        </div>
        
        <div class="listing-excerpt">
            <?php the_excerpt(); ?>
        </div>
        
        <div class="listing-actions">
            <a href="<?php the_permalink(); ?>" class="btn-view">View Details</a>
            <?php echo reign_gd_favorite_button(get_the_ID()); ?>
        </div>
    </div>
</div>
```

### Map Template Customization

**Custom map implementation:**

```php
<?php
/**
 * Custom Map Template
 */
?>
<div id="reign-gd-map" class="custom-map-container">
    <div class="map-controls">
        <button id="map-fullscreen">Fullscreen</button>
        <button id="map-reset">Reset View</button>
    </div>
    
    <div id="map-canvas" 
         data-markers='<?php echo json_encode(reign_gd_get_markers()); ?>'
         data-center='<?php echo json_encode(reign_gd_get_map_center()); ?>'
         data-zoom='<?php echo get_option('reign_gd_default_zoom', 13); ?>'>
    </div>
    
    <div class="map-legend">
        <?php reign_gd_display_map_legend(); ?>
    </div>
</div>

<script>
jQuery(document).ready(function($) {
    // Initialize custom map
    var mapData = $('#map-canvas').data();
    
    var map = new google.maps.Map(document.getElementById('map-canvas'), {
        zoom: mapData.zoom,
        center: mapData.center,
        styles: <?php echo reign_gd_get_map_styles(); ?>
    });
    
    // Add markers
    mapData.markers.forEach(function(marker) {
        new google.maps.Marker({
            position: marker.position,
            map: map,
            title: marker.title,
            icon: marker.icon
        });
    });
});
</script>
```

---

## Part 4: AJAX Implementation

### Search Functionality

**AJAX search implementation:**

```php
// PHP handler
add_action('wp_ajax_reign_gd_search', 'handle_ajax_search');
add_action('wp_ajax_nopriv_reign_gd_search', 'handle_ajax_search');

function handle_ajax_search() {
    // Verify nonce
    if (!wp_verify_nonce($_POST['nonce'], 'reign_gd_search_nonce')) {
        wp_die('Security check failed');
    }
    
    // Get search parameters
    $keyword = sanitize_text_field($_POST['keyword']);
    $location = sanitize_text_field($_POST['location']);
    $category = intval($_POST['category']);
    $radius = intval($_POST['radius']);
    
    // Build query
    $args = array(
        'post_type' => 'gd_place',
        'posts_per_page' => 20,
        's' => $keyword,
        'meta_query' => array()
    );
    
    if ($category) {
        $args['tax_query'] = array(
            array(
                'taxonomy' => 'gd_placecategory',
                'terms' => $category
            )
        );
    }
    
    // Get results
    $query = new WP_Query($args);
    $results = array();
    
    if ($query->have_posts()) {
        while ($query->have_posts()) {
            $query->the_post();
            $results[] = array(
                'id' => get_the_ID(),
                'title' => get_the_title(),
                'url' => get_the_permalink(),
                'thumbnail' => get_the_post_thumbnail_url(get_the_ID(), 'thumbnail'),
                'location' => get_post_meta(get_the_ID(), 'location', true),
                'rating' => get_post_meta(get_the_ID(), 'rating', true)
            );
        }
        wp_reset_postdata();
    }
    
    wp_send_json_success($results);
}
```

**JavaScript implementation:**

```javascript
jQuery(document).ready(function($) {
    $('#reign-gd-search-form').on('submit', function(e) {
        e.preventDefault();
        
        var formData = {
            action: 'reign_gd_search',
            nonce: reign_gd_ajax.nonce,
            keyword: $('#search-keyword').val(),
            location: $('#search-location').val(),
            category: $('#search-category').val(),
            radius: $('#search-radius').val()
        };
        
        // Show loading
        $('#search-results').html('<div class="loading">Searching...</div>');
        
        $.post(reign_gd_ajax.ajax_url, formData, function(response) {
            if (response.success) {
                displayResults(response.data);
            } else {
                $('#search-results').html('<div class="error">No results found</div>');
            }
        });
    });
    
    function displayResults(results) {
        var html = '';
        
        results.forEach(function(listing) {
            html += `
                <div class="search-result">
                    <img src="${listing.thumbnail}" alt="${listing.title}">
                    <h3><a href="${listing.url}">${listing.title}</a></h3>
                    <div class="location">${listing.location}</div>
                    <div class="rating">${displayRating(listing.rating)}</div>
                </div>
            `;
        });
        
        $('#search-results').html(html);
    }
});
```

### Live Filter Updates

**Real-time filtering:**

```javascript
// Live category filter
$('.category-filter').on('change', function() {
    var selectedCategories = [];
    
    $('.category-filter:checked').each(function() {
        selectedCategories.push($(this).val());
    });
    
    $.post(reign_gd_ajax.ajax_url, {
        action: 'reign_gd_filter_listings',
        categories: selectedCategories,
        nonce: reign_gd_ajax.nonce
    }, function(response) {
        $('#listings-container').html(response.data);
        updateMap(response.markers);
    });
});

// Distance radius slider
$('#distance-slider').on('change', function() {
    var radius = $(this).val();
    
    $.post(reign_gd_ajax.ajax_url, {
        action: 'reign_gd_update_radius',
        radius: radius,
        center: getCurrentLocation(),
        nonce: reign_gd_ajax.nonce
    }, function(response) {
        updateListings(response.data);
        updateMapRadius(radius);
    });
});
```

---

## Part 5: Database Operations

### Custom Tables

**Working with GeoDirectory tables:**

```php
// Get listing details from custom table
function get_listing_details($listing_id) {
    global $wpdb;
    
    $table = $wpdb->prefix . 'geodir_gd_place_detail';
    
    $details = $wpdb->get_row(
        $wpdb->prepare(
            "SELECT * FROM $table WHERE post_id = %d",
            $listing_id
        ),
        ARRAY_A
    );
    
    return $details;
}

// Update custom fields
function update_listing_custom_field($listing_id, $field_name, $value) {
    global $wpdb;
    
    $table = $wpdb->prefix . 'geodir_gd_place_detail';
    
    $result = $wpdb->update(
        $table,
        array($field_name => $value),
        array('post_id' => $listing_id),
        array('%s'),
        array('%d')
    );
    
    return $result !== false;
}

// Bulk operations
function bulk_update_listings($category_id, $updates) {
    global $wpdb;
    
    $listing_ids = get_posts(array(
        'post_type' => 'gd_place',
        'fields' => 'ids',
        'posts_per_page' => -1,
        'tax_query' => array(
            array(
                'taxonomy' => 'gd_placecategory',
                'terms' => $category_id
            )
        )
    ));
    
    foreach ($listing_ids as $id) {
        foreach ($updates as $field => $value) {
            update_post_meta($id, $field, $value);
        }
    }
}
```

### Location Queries

**Distance-based queries:**

```php
function get_listings_within_radius($lat, $lng, $radius_km) {
    global $wpdb;
    
    $table = $wpdb->prefix . 'geodir_gd_place_detail';
    
    $sql = "
        SELECT 
            post_id,
            post_title,
            latitude,
            longitude,
            ( 6371 * acos( 
                cos( radians(%f) ) * 
                cos( radians( latitude ) ) * 
                cos( radians( longitude ) - radians(%f) ) + 
                sin( radians(%f) ) * 
                sin( radians( latitude ) ) 
            ) ) AS distance
        FROM $table
        HAVING distance < %f
        ORDER BY distance
        LIMIT 50
    ";
    
    $results = $wpdb->get_results(
        $wpdb->prepare($sql, $lat, $lng, $lat, $radius_km)
    );
    
    return $results;
}
```

---

## Part 6: REST API Integration

### Custom Endpoints

**Register API endpoints:**

```php
add_action('rest_api_init', 'reign_gd_register_api_endpoints');

function reign_gd_register_api_endpoints() {
    // Get listings endpoint
    register_rest_route('reign-gd/v1', '/listings', array(
        'methods' => 'GET',
        'callback' => 'reign_gd_get_listings_api',
        'permission_callback' => '__return_true',
        'args' => array(
            'category' => array(
                'sanitize_callback' => 'absint'
            ),
            'location' => array(
                'sanitize_callback' => 'sanitize_text_field'
            ),
            'page' => array(
                'default' => 1,
                'sanitize_callback' => 'absint'
            )
        )
    ));
    
    // Single listing endpoint
    register_rest_route('reign-gd/v1', '/listing/(?P<id>\d+)', array(
        'methods' => 'GET',
        'callback' => 'reign_gd_get_listing_api',
        'permission_callback' => '__return_true'
    ));
    
    // Submit review endpoint
    register_rest_route('reign-gd/v1', '/review', array(
        'methods' => 'POST',
        'callback' => 'reign_gd_submit_review_api',
        'permission_callback' => 'is_user_logged_in'
    ));
}

// Callback functions
function reign_gd_get_listings_api($request) {
    $params = $request->get_params();
    
    $args = array(
        'post_type' => 'gd_place',
        'posts_per_page' => 20,
        'paged' => $params['page']
    );
    
    if (!empty($params['category'])) {
        $args['tax_query'] = array(
            array(
                'taxonomy' => 'gd_placecategory',
                'terms' => $params['category']
            )
        );
    }
    
    $query = new WP_Query($args);
    $listings = array();
    
    if ($query->have_posts()) {
        while ($query->have_posts()) {
            $query->the_post();
            $listings[] = reign_gd_format_listing_for_api(get_the_ID());
        }
        wp_reset_postdata();
    }
    
    return rest_ensure_response(array(
        'listings' => $listings,
        'total' => $query->found_posts,
        'pages' => $query->max_num_pages
    ));
}
```

### Mobile App Integration

**API for mobile apps:**

```php
// Authentication endpoint
register_rest_route('reign-gd/v1', '/auth', array(
    'methods' => 'POST',
    'callback' => 'reign_gd_authenticate_user',
    'permission_callback' => '__return_true'
));

function reign_gd_authenticate_user($request) {
    $username = $request->get_param('username');
    $password = $request->get_param('password');
    
    $user = wp_authenticate($username, $password);
    
    if (is_wp_error($user)) {
        return new WP_Error('auth_failed', 'Invalid credentials', array('status' => 401));
    }
    
    // Generate token
    $token = wp_generate_password(32, false);
    update_user_meta($user->ID, 'api_token', $token);
    
    return rest_ensure_response(array(
        'token' => $token,
        'user' => array(
            'id' => $user->ID,
            'name' => $user->display_name,
            'email' => $user->user_email
        )
    ));
}

// Validate token for protected endpoints
function reign_gd_validate_token($request) {
    $token = $request->get_header('X-Auth-Token');
    
    if (!$token) {
        return false;
    }
    
    $users = get_users(array(
        'meta_key' => 'api_token',
        'meta_value' => $token
    ));
    
    return !empty($users);
}
```

---

## Part 7: Performance Optimization

### Caching Strategies

**Implement caching:**

```php
// Cache listing data
function get_cached_listing($listing_id) {
    $cache_key = 'reign_gd_listing_' . $listing_id;
    $cached = wp_cache_get($cache_key, 'reign_gd');
    
    if ($cached === false) {
        $listing = reign_gd_get_listing_data($listing_id);
        wp_cache_set($cache_key, $listing, 'reign_gd', 3600);
        return $listing;
    }
    
    return $cached;
}

// Clear cache on update
add_action('save_post_gd_place', 'clear_listing_cache');
function clear_listing_cache($post_id) {
    wp_cache_delete('reign_gd_listing_' . $post_id, 'reign_gd');
    
    // Clear related caches
    wp_cache_delete('reign_gd_markers', 'reign_gd');
    wp_cache_delete('reign_gd_search_' . md5('latest'), 'reign_gd');
}

// Cache map markers
function get_cached_markers($args = array()) {
    $cache_key = 'reign_gd_markers_' . md5(serialize($args));
    $markers = wp_cache_get($cache_key, 'reign_gd');
    
    if ($markers === false) {
        $markers = reign_gd_generate_markers($args);
        wp_cache_set($cache_key, $markers, 'reign_gd', 1800);
    }
    
    return $markers;
}
```

### Database Optimization

**Optimize queries:**

```php
// Use proper indexes
function optimize_listing_queries() {
    global $wpdb;
    
    // Add index for location queries
    $wpdb->query("
        ALTER TABLE {$wpdb->prefix}geodir_gd_place_detail 
        ADD INDEX idx_location (latitude, longitude)
    ");
    
    // Add index for rating queries
    $wpdb->query("
        ALTER TABLE {$wpdb->prefix}geodir_gd_place_detail 
        ADD INDEX idx_rating (overall_rating)
    ");
}

// Batch processing
function process_listings_in_batches($callback, $batch_size = 100) {
    $offset = 0;
    
    while (true) {
        $listings = get_posts(array(
            'post_type' => 'gd_place',
            'posts_per_page' => $batch_size,
            'offset' => $offset,
            'fields' => 'ids'
        ));
        
        if (empty($listings)) {
            break;
        }
        
        foreach ($listings as $listing_id) {
            call_user_func($callback, $listing_id);
        }
        
        $offset += $batch_size;
        
        // Prevent memory issues
        wp_cache_flush();
    }
}
```

---

## Part 8: Integration Examples

### BuddyPress Integration

**Add listings to activity stream:**

```php
// Record listing activity
add_action('geodir_after_save_listing', 'record_listing_activity', 10, 2);

function record_listing_activity($post_id, $post) {
    if (!function_exists('bp_activity_add')) {
        return;
    }
    
    $user_id = get_current_user_id();
    $listing_url = get_permalink($post_id);
    $listing_title = get_the_title($post_id);
    
    bp_activity_add(array(
        'user_id' => $user_id,
        'type' => 'new_listing',
        'action' => sprintf(
            '%s added a new listing: <a href="%s">%s</a>',
            bp_core_get_userlink($user_id),
            $listing_url,
            $listing_title
        ),
        'content' => $post->post_excerpt,
        'primary_link' => $listing_url,
        'item_id' => $post_id
    ));
}

// Add listings tab to member profile
add_action('bp_setup_nav', 'add_listings_profile_tab');

function add_listings_profile_tab() {
    bp_core_new_nav_item(array(
        'name' => 'Listings',
        'slug' => 'listings',
        'screen_function' => 'display_member_listings',
        'position' => 50,
        'default_subnav_slug' => 'my-listings'
    ));
}

function display_member_listings() {
    add_action('bp_template_content', 'show_member_listings');
    bp_core_load_template('buddypress/members/single/plugins');
}

function show_member_listings() {
    $user_id = bp_displayed_user_id();
    
    $listings = get_posts(array(
        'post_type' => 'gd_place',
        'author' => $user_id,
        'posts_per_page' => -1
    ));
    
    if ($listings) {
        echo '<div class="member-listings">';
        foreach ($listings as $listing) {
            // Display listing card
            reign_gd_display_listing_card($listing->ID);
        }
        echo '</div>';
    } else {
        echo '<p>No listings found.</p>';
    }
}
```

### WooCommerce Integration

**Sell featured listings:**

```php
// Create WooCommerce product for featured listing
function create_featured_listing_product() {
    $product = new WC_Product_Simple();
    $product->set_name('Featured Listing Upgrade');
    $product->set_regular_price(29.99);
    $product->set_virtual(true);
    $product->save();
    
    update_option('reign_gd_featured_product_id', $product->get_id());
}

// Process purchase
add_action('woocommerce_order_status_completed', 'activate_featured_listing');

function activate_featured_listing($order_id) {
    $order = wc_get_order($order_id);
    $featured_product_id = get_option('reign_gd_featured_product_id');
    
    foreach ($order->get_items() as $item) {
        if ($item->get_product_id() == $featured_product_id) {
            $listing_id = get_post_meta($order_id, 'listing_id', true);
            
            if ($listing_id) {
                update_post_meta($listing_id, 'featured', 1);
                update_post_meta($listing_id, 'featured_expires', 
                    date('Y-m-d', strtotime('+30 days')));
            }
        }
    }
}
```

---

## Part 9: Advanced Customization

### Custom Map Styles

**Implement custom Google Maps styling:**

```php
function reign_gd_custom_map_styles() {
    $styles = '
    [
        {
            "featureType": "water",
            "elementType": "geometry",
            "stylers": [{"color": "#e9e9e9"}, {"lightness": 17}]
        },
        {
            "featureType": "landscape",
            "elementType": "geometry",
            "stylers": [{"color": "#f5f5f5"}, {"lightness": 20}]
        },
        {
            "featureType": "road.highway",
            "elementType": "geometry.fill",
            "stylers": [{"color": "#ffffff"}, {"lightness": 17}]
        },
        {
            "featureType": "poi",
            "elementType": "geometry",
            "stylers": [{"color": "#f5f5f5"}, {"lightness": 21}]
        }
    ]';
    
    return $styles;
}

add_filter('reign_gd_map_styles', 'reign_gd_custom_map_styles');
```

### Custom Fields Implementation

**Add complex custom fields:**

```php
// Register custom field
function register_opening_hours_field() {
    if (!function_exists('geodir_custom_field_save')) {
        return;
    }
    
    $field = array(
        'post_type' => 'gd_place',
        'field_type' => 'text',
        'data_type' => 'TEXT',
        'admin_title' => 'Opening Hours',
        'site_title' => 'Opening Hours',
        'htmlvar_name' => 'opening_hours',
        'is_active' => 1,
        'for_admin_use' => 0,
        'default_value' => '',
        'show_in' => '[detail],[listing]',
        'is_required' => 0
    );
    
    geodir_custom_field_save($field);
}

// Custom field display
add_filter('geodir_custom_field_output_text_var_opening_hours', 
    'display_opening_hours', 10, 3);

function display_opening_hours($html, $location, $field) {
    $value = geodir_get_cf_value($field['id']);
    
    if ($value) {
        $hours = json_decode($value, true);
        
        $html = '<div class="opening-hours">';
        foreach ($hours as $day => $times) {
            $html .= sprintf(
                '<div class="day-hours"><span>%s:</span> %s</div>',
                $day,
                $times
            );
        }
        $html .= '</div>';
    }
    
    return $html;
}
```

---

## Part 10: Debugging & Development Tools

### Debug Functions

**Helpful debugging utilities:**

```php
// Debug logger
function reign_gd_debug($message, $data = null) {
    if (WP_DEBUG && WP_DEBUG_LOG) {
        $log_message = '[Reign GD Debug] ' . $message;
        
        if ($data !== null) {
            $log_message .= ' - Data: ' . print_r($data, true);
        }
        
        error_log($log_message);
    }
}

// Query monitor
function reign_gd_monitor_queries() {
    add_action('shutdown', function() {
        global $wpdb;
        
        $queries = $wpdb->queries;
        $slow_queries = array();
        
        foreach ($queries as $query) {
            if ($query[1] > 0.5) { // Queries taking > 0.5s
                $slow_queries[] = array(
                    'sql' => $query[0],
                    'time' => $query[1],
                    'caller' => $query[2]
                );
            }
        }
        
        if (!empty($slow_queries)) {
            reign_gd_debug('Slow queries detected', $slow_queries);
        }
    });
}

// Performance profiler
class Reign_GD_Profiler {
    private static $timers = array();
    
    public static function start($name) {
        self::$timers[$name] = microtime(true);
    }
    
    public static function end($name) {
        if (isset(self::$timers[$name])) {
            $time = microtime(true) - self::$timers[$name];
            reign_gd_debug("Profile: $name took {$time}s");
            unset(self::$timers[$name]);
            return $time;
        }
        return false;
    }
}

// Usage example
Reign_GD_Profiler::start('listing_query');
// ... your code ...
Reign_GD_Profiler::end('listing_query');
```

### Development Commands

**WP-CLI commands:**

```php
// Register CLI commands
if (defined('WP_CLI') && WP_CLI) {
    WP_CLI::add_command('reign-gd', 'Reign_GD_CLI_Commands');
}

class Reign_GD_CLI_Commands {
    /**
     * Import listings from CSV
     * 
     * @synopsis <file> [--dry-run]
     */
    public function import($args, $assoc_args) {
        $file = $args[0];
        $dry_run = isset($assoc_args['dry-run']);
        
        if (!file_exists($file)) {
            WP_CLI::error("File not found: $file");
        }
        
        $csv = array_map('str_getcsv', file($file));
        $headers = array_shift($csv);
        
        foreach ($csv as $row) {
            $data = array_combine($headers, $row);
            
            if ($dry_run) {
                WP_CLI::line("Would import: " . $data['title']);
            } else {
                $post_id = wp_insert_post(array(
                    'post_title' => $data['title'],
                    'post_content' => $data['description'],
                    'post_type' => 'gd_place',
                    'post_status' => 'publish'
                ));
                
                if ($post_id) {
                    WP_CLI::success("Imported: " . $data['title']);
                }
            }
        }
    }
    
    /**
     * Rebuild search index
     */
    public function reindex() {
        WP_CLI::line("Rebuilding search index...");
        
        $listings = get_posts(array(
            'post_type' => 'gd_place',
            'posts_per_page' => -1,
            'fields' => 'ids'
        ));
        
        $progress = WP_CLI\Utils\make_progress_bar(
            'Indexing listings', 
            count($listings)
        );
        
        foreach ($listings as $listing_id) {
            reign_gd_update_search_index($listing_id);
            $progress->tick();
        }
        
        $progress->finish();
        WP_CLI::success("Reindexed " . count($listings) . " listings");
    }
}
```

---

## Best Practices

### Code Standards

```php
/**
 * Follow WordPress coding standards
 * 
 * @param int $listing_id The listing post ID
 * @param array $args Optional arguments
 * @return array Formatted listing data
 */
function reign_gd_get_formatted_listing($listing_id, $args = array()) {
    // Validate input
    if (!$listing_id || !is_numeric($listing_id)) {
        return false;
    }
    
    // Set defaults
    $defaults = array(
        'include_meta' => true,
        'include_reviews' => false
    );
    
    $args = wp_parse_args($args, $defaults);
    
    // Sanitize and escape
    $listing_id = absint($listing_id);
    
    // Use proper hooks
    $data = apply_filters(
        'reign_gd_before_get_listing', 
        array(), 
        $listing_id
    );
    
    // ... rest of function
    
    return $data;
}
```

### Security Practices

```php
// Always sanitize input
$user_input = sanitize_text_field($_POST['input']);

// Always escape output
echo esc_html($variable);
echo esc_attr($attribute);
echo esc_url($url);

// Use nonces for forms
wp_nonce_field('reign_gd_action', 'reign_gd_nonce');

// Check capabilities
if (!current_user_can('edit_posts')) {
    wp_die('Unauthorized');
}

// Prepare database queries
$wpdb->prepare("SELECT * FROM table WHERE id = %d", $id);
```

---

## Resources

### Developer Documentation

- **GeoDirectory Codex:** geodirectory.com/docs/
- **WordPress Developer:** developer.wordpress.org
- **Reign Theme Docs:** docs.wbcomdesigns.com

### Support Channels

- **Developer Forum:** wbcomdesigns.com/support
- **GitHub Issues:** github.com/wbcomdesigns
- **Stack Overflow:** Tag with `geodirectory`

---

**Need Development Help?**
📧 Email: dev@wbcomdesigns.com
💻 Custom development available
🎯 Code review services
📚 Advanced training workshops