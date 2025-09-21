# Reign Dokan Addon - Store Customization Guide

## Store Appearance Settings

### Store Banner Customization

#### Banner Dimensions
```css
/* Recommended banner sizes */
.dokan-store-banner {
    Desktop: 1920x400px
    Tablet: 1024x300px  
    Mobile: 768x200px
}
```

#### Banner Overlay Options
```php
// Customizer settings
'reign_dokan_banner_overlay' => array(
    'none' => 'No Overlay',
    'gradient' => 'Gradient Overlay',
    'solid' => 'Solid Color Overlay',
    'pattern' => 'Pattern Overlay'
)
```

### Store Logo/Avatar

#### Logo Settings
- **Recommended Size**: 150x150px
- **Format**: PNG with transparency or JPG
- **Position Options**: Left, Center, Overlay on banner

```css
/* Custom logo styling */
.reign-store-logo {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    border: 5px solid #fff;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}
```

### Store Information Display

#### Information Blocks
```php
// Enable/disable store info sections
'store_info_display' => array(
    'store_name' => true,
    'store_rating' => true,
    'store_address' => true,
    'store_phone' => true,
    'store_email' => false,
    'social_links' => true,
    'store_timing' => true,
    'vendor_biography' => true
)
```

## Product Display Customization

### Grid Layout Options

```php
// Product grid configuration
'product_grid_settings' => array(
    'columns_desktop' => 4,
    'columns_tablet' => 3,
    'columns_mobile' => 2,
    'products_per_page' => 12,
    'show_pagination' => true,
    'show_sorting' => true,
    'show_filters' => true
)
```

### Product Card Elements

```css
/* Product card customization */
.reign-product-card {
    /* Elements to show/hide */
    --show-sale-badge: block;
    --show-rating: block;
    --show-price: block;
    --show-add-to-cart: block;
    --show-quick-view: block;
}
```

## Widget Areas Customization

### Available Widget Areas

1. **Store Header Widgets**
   - Above store banner
   - Below store banner
   - Inside store header

2. **Store Sidebar Widgets**
   - Primary sidebar
   - Secondary sidebar
   - Filter sidebar

3. **Store Footer Widgets**
   - Before products
   - After products

### Custom Widget Implementation

```php
// Register store widget area
function reign_dokan_register_store_widgets() {
    register_sidebar(array(
        'name' => __('Store Header', 'reign-dokan'),
        'id' => 'reign-store-header',
        'before_widget' => '<div class="reign-store-widget">',
        'after_widget' => '</div>',
        'before_title' => '<h3 class="widget-title">',
        'after_title' => '</h3>'
    ));
}
add_action('widgets_init', 'reign_dokan_register_store_widgets');
```

## Color Scheme Customization

### Store-Specific Colors

```php
// Individual store color settings
function reign_dokan_store_colors($vendor_id) {
    $colors = array(
        'primary_color' => get_user_meta($vendor_id, 'store_primary_color', true),
        'secondary_color' => get_user_meta($vendor_id, 'store_secondary_color', true),
        'accent_color' => get_user_meta($vendor_id, 'store_accent_color', true)
    );
    
    return wp_parse_args($colors, array(
        'primary_color' => '#3498db',
        'secondary_color' => '#2ecc71',
        'accent_color' => '#e74c3c'
    ));
}
```

### Dynamic CSS Generation

```php
// Generate store-specific CSS
function reign_dokan_store_dynamic_css($vendor_id) {
    $colors = reign_dokan_store_colors($vendor_id);
    
    $css = "
        .store-{$vendor_id} {
            --store-primary: {$colors['primary_color']};
            --store-secondary: {$colors['secondary_color']};
            --store-accent: {$colors['accent_color']};
        }
        
        .store-{$vendor_id} .dokan-btn {
            background-color: var(--store-primary);
        }
        
        .store-{$vendor_id} .product-price {
            color: var(--store-accent);
        }
    ";
    
    wp_add_inline_style('reign-dokan-style', $css);
}
```

## Store Navigation Customization

### Store Tabs Configuration

```php
// Customize store tabs
add_filter('dokan_store_tabs', function($tabs, $vendor_id) {
    // Add custom tab
    $tabs['custom'] = array(
        'title' => __('Special Offers', 'reign-dokan'),
        'url' => dokan_get_store_url($vendor_id) . 'offers'
    );
    
    // Remove tab
    unset($tabs['terms']);
    
    // Reorder tabs
    $new_order = array('products', 'custom', 'reviews');
    $tabs = array_merge(array_flip($new_order), $tabs);
    
    return $tabs;
}, 10, 2);
```

### Custom Tab Content

```php
// Display custom tab content
add_action('dokan_store_tab_content', function($tab, $vendor_id) {
    if ($tab === 'custom') {
        Reign_Dokan_Templates::get_template('store/tab-offers.php', array(
            'vendor_id' => $vendor_id
        ));
    }
}, 10, 2);
```

## Mobile Responsiveness

### Mobile-Specific Styling

```css
/* Mobile optimizations */
@media (max-width: 768px) {
    /* Simplified header */
    .reign-store-header-mobile {
        padding: 15px;
        text-align: center;
    }
    
    /* Stack elements */
    .store-info-row {
        flex-direction: column;
    }
    
    /* Touch-friendly buttons */
    .dokan-btn {
        min-height: 44px;
        font-size: 16px;
    }
    
    /* Simplified navigation */
    .store-tabs {
        overflow-x: auto;
        white-space: nowrap;
    }
}
```

### Mobile Menu Configuration

```javascript
// Mobile menu toggle
(function($) {
    $('.reign-store-mobile-menu-toggle').on('click', function() {
        $('.reign-store-sidebar').toggleClass('active');
        $('body').toggleClass('store-sidebar-open');
    });
})(jQuery);
```

## Advanced Customization

### Custom Store Templates

```php
// Use different template for premium vendors
add_filter('dokan_store_template', function($template, $vendor_id) {
    if (get_user_meta($vendor_id, 'premium_vendor', true) === 'yes') {
        $premium_template = locate_template('reign-dokan/premium-store.php');
        if ($premium_template) {
            return $premium_template;
        }
    }
    return $template;
}, 10, 2);
```

### Store-Specific Scripts

```php
// Load vendor-specific JavaScript
function reign_dokan_vendor_scripts() {
    if (dokan_is_store_page()) {
        $vendor_id = get_query_var('author');
        
        // Check for vendor custom script
        $custom_js = get_user_meta($vendor_id, 'store_custom_js', true);
        
        if ($custom_js) {
            wp_add_inline_script('reign-dokan-script', $custom_js);
        }
    }
}
add_action('wp_enqueue_scripts', 'reign_dokan_vendor_scripts');
```

## Store SEO Optimization

### Meta Tags Customization

```php
// Customize store meta tags
add_filter('dokan_store_meta_tags', function($meta, $vendor_id) {
    $store = dokan()->vendor->get($vendor_id);
    
    $meta['description'] = $store->get_shop_description();
    $meta['og:title'] = $store->get_shop_name() . ' - ' . get_bloginfo('name');
    $meta['og:image'] = $store->get_banner();
    $meta['twitter:card'] = 'summary_large_image';
    
    return $meta;
}, 10, 2);
```

### Schema Markup

```php
// Add LocalBusiness schema
function reign_dokan_store_schema($vendor_id) {
    $store = dokan()->vendor->get($vendor_id);
    
    $schema = array(
        '@context' => 'https://schema.org',
        '@type' => 'Store',
        'name' => $store->get_shop_name(),
        'url' => $store->get_shop_url(),
        'logo' => $store->get_avatar(),
        'address' => $store->get_address(),
        'telephone' => $store->get_phone()
    );
    
    echo '<script type="application/ld+json">' . json_encode($schema) . '</script>';
}
add_action('dokan_store_header_info_fields', 'reign_dokan_store_schema');
```

## Social Features Integration

### Social Links Display

```php
// Display social links
function reign_dokan_social_links($vendor_id) {
    $social_links = array(
        'facebook' => get_user_meta($vendor_id, 'dokan_facebook', true),
        'twitter' => get_user_meta($vendor_id, 'dokan_twitter', true),
        'instagram' => get_user_meta($vendor_id, 'dokan_instagram', true),
        'linkedin' => get_user_meta($vendor_id, 'dokan_linkedin', true)
    );
    
    echo '<div class="reign-store-social">';
    foreach ($social_links as $network => $url) {
        if ($url) {
            echo '<a href="' . esc_url($url) . '" class="social-' . $network . '" target="_blank">';
            echo '<i class="fab fa-' . $network . '"></i>';
            echo '</a>';
        }
    }
    echo '</div>';
}
```

### Share Buttons

```php
// Add share functionality
function reign_dokan_share_buttons($vendor_id) {
    $store = dokan()->vendor->get($vendor_id);
    $url = $store->get_shop_url();
    $title = $store->get_shop_name();
    
    $share_links = array(
        'facebook' => 'https://www.facebook.com/sharer/sharer.php?u=' . $url,
        'twitter' => 'https://twitter.com/intent/tweet?url=' . $url . '&text=' . $title,
        'linkedin' => 'https://www.linkedin.com/sharing/share-offsite/?url=' . $url,
        'whatsapp' => 'https://wa.me/?text=' . $title . ' ' . $url
    );
    
    Reign_Dokan_Templates::get_template('store/share-buttons.php', array(
        'links' => $share_links
    ));
}
```

## Performance Optimization

### Lazy Loading Implementation

```javascript
// Lazy load store products
(function($) {
    var lazyLoadProducts = function() {
        $('.reign-product-card img').each(function() {
            if ($(this).offset().top < window.innerHeight + window.pageYOffset + 500) {
                var src = $(this).data('src');
                if (src) {
                    $(this).attr('src', src).removeAttr('data-src');
                }
            }
        });
    };
    
    $(window).on('scroll', lazyLoadProducts);
    lazyLoadProducts();
})(jQuery);
```

### Cache Store Data

```php
// Cache vendor data
function reign_dokan_get_cached_vendor_data($vendor_id) {
    $cache_key = 'reign_vendor_' . $vendor_id;
    $data = get_transient($cache_key);
    
    if (!$data) {
        $vendor = dokan()->vendor->get($vendor_id);
        $data = array(
            'name' => $vendor->get_shop_name(),
            'logo' => $vendor->get_avatar(),
            'banner' => $vendor->get_banner(),
            'rating' => $vendor->get_rating(),
            'products' => $vendor->get_product_count()
        );
        
        set_transient($cache_key, $data, HOUR_IN_SECONDS);
    }
    
    return $data;
}
```

## Troubleshooting Store Display

### Common Issues

1. **Store banner not displaying**
   - Check image dimensions
   - Verify file permissions
   - Clear cache

2. **Products not loading**
   - Check vendor product permissions
   - Verify query parameters
   - Review error logs

3. **Styling not applied**
   - Check CSS specificity
   - Verify customizer settings
   - Inspect browser console

## Next Steps

- [Troubleshooting Guide](06-troubleshooting.md) - Common issues and solutions
- [Developer Guide](05-developer-guide.md) - Advanced customization
- [FAQ](07-faq.md) - Frequently asked questions