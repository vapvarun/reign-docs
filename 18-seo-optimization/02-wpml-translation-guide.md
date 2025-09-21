# WPML Translation Guide for Reign Theme

## Overview

Reign Theme is fully compatible with WPML (WordPress Multilingual Plugin), allowing you to create multilingual communities, marketplaces, and social networks. This guide covers complete WPML integration, translation workflows, and best practices for multilingual sites.

## WPML Setup

### Requirements

```
WPML Multilingual CMS: Required (Core plugin)
WPML String Translation: Required
WPML Translation Management: Recommended
WPML Media Translation: Optional
Reign Theme: 7.0+
WordPress: 5.8+
PHP: 7.4+
```

### Installation Process

1. **Install WPML**
   ```
   1. Purchase WPML from wpml.org
   2. Download WPML plugins
   3. WordPress Admin → Plugins → Add New → Upload
   4. Install and activate in this order:
      - WPML Multilingual CMS
      - WPML String Translation
      - WPML Translation Management
   ```

2. **Initial Configuration**
   ```
   WPML → Languages
   - Select default language
   - Add additional languages
   - Choose language URL format:
     * Different languages in directories (recommended)
     * Language name as parameter
     * Different domain per language
   ```

3. **Reign Theme Configuration**
   ```
   WPML → Theme and Plugin Localization
   - Select "Reign Theme"
   - Scan for strings
   - Enable automatic string registration
   ```

## Language Configuration

### Adding Languages

```php
// Programmatically add languages
function reign_add_wpml_languages() {
    if (class_exists('SitePress')) {
        global $sitepress;

        // Add Spanish
        $sitepress->add_language('es', 'Spanish', 'Español', 'es_ES');

        // Add French
        $sitepress->add_language('fr', 'French', 'Français', 'fr_FR');

        // Add German
        $sitepress->add_language('de', 'German', 'Deutsch', 'de_DE');
    }
}
```

### Language Switcher

#### Header Language Switcher

```php
// Add to header
add_action('reign_header_top_bar_right', function() {
    if (function_exists('wpml_language_selector')) {
        ?>
        <div class="reign-language-switcher">
            <?php
            do_action('wpml_add_language_selector');
            // Or custom:
            reign_custom_language_switcher();
            ?>
        </div>
        <?php
    }
});

// Custom language switcher
function reign_custom_language_switcher() {
    if (!function_exists('icl_get_languages')) return;

    $languages = icl_get_languages('skip_missing=0');

    if (count($languages) > 1) {
        echo '<div class="language-dropdown">';
        echo '<button class="current-language">';
        echo ICL_LANGUAGE_NAME . ' <i class="fa fa-angle-down"></i>';
        echo '</button>';
        echo '<ul class="language-list">';

        foreach ($languages as $lang) {
            $class = $lang['active'] ? 'active' : '';
            echo '<li class="' . $class . '">';
            echo '<a href="' . $lang['url'] . '">';
            echo '<img src="' . $lang['country_flag_url'] . '" alt="' . $lang['native_name'] . '">';
            echo $lang['native_name'];
            echo '</a></li>';
        }

        echo '</ul></div>';
    }
}
```

#### Mobile Language Switcher

```css
/* Mobile language switcher */
@media (max-width: 768px) {
    .mobile-language-switcher {
        position: fixed;
        bottom: 20px;
        right: 20px;
        z-index: 9999;
    }

    .language-float-button {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        background: var(--reign-primary-color);
        display: flex;
        align-items: center;
        justify-content: center;
        box-shadow: 0 2px 10px rgba(0,0,0,0.2);
    }
}
```

## Translating Theme Elements

### Theme Strings

#### Register Custom Strings

```php
// Register theme strings for translation
add_action('init', function() {
    if (function_exists('icl_register_string')) {
        // Register custom strings
        icl_register_string('reign-theme', 'Welcome Message', 'Welcome to our community!');
        icl_register_string('reign-theme', 'Footer Copyright', '© 2024 All rights reserved');
        icl_register_string('reign-theme', 'Login Button', 'Sign In');
        icl_register_string('reign-theme', 'Register Button', 'Join Now');
    }
});

// Retrieve translated string
function reign_get_translated_string($name, $default) {
    if (function_exists('icl_t')) {
        return icl_t('reign-theme', $name, $default);
    }
    return $default;
}
```

### Customizer Options

```php
// Make Customizer options translatable
add_filter('reign_customizer_options', function($options) {
    if (function_exists('icl_register_string')) {
        foreach ($options as $key => $value) {
            if (is_string($value)) {
                icl_register_string('reign-customizer', $key, $value);
                $options[$key] = icl_t('reign-customizer', $key, $value);
            }
        }
    }
    return $options;
});
```

### Menu Translation

```php
// Sync menu locations across languages
add_action('after_setup_theme', function() {
    if (class_exists('SitePress')) {
        global $sitepress;

        // Get all languages
        $languages = $sitepress->get_active_languages();

        // Sync menu locations
        foreach ($languages as $lang) {
            $menu_locations = array(
                'primary' => 'primary_' . $lang['code'],
                'footer' => 'footer_' . $lang['code'],
                'mobile' => 'mobile_' . $lang['code']
            );

            register_nav_menus($menu_locations);
        }
    }
});
```

## BuddyPress Translation

### Activity Stream

```php
// Translate activity types
add_filter('bp_activity_action_strings', function($actions) {
    if (function_exists('icl_t')) {
        foreach ($actions as $key => $action) {
            $actions[$key] = icl_t('buddypress', 'activity_' . $key, $action);
        }
    }
    return $actions;
});

// Translate activity content
add_filter('bp_get_activity_content', function($content) {
    if (function_exists('icl_object_id')) {
        // Apply WPML filters
        $content = apply_filters('wpml_translate_string', $content, 'activity_content');
    }
    return $content;
});
```

### Profile Fields

```php
// Translate xProfile fields
add_filter('bp_get_the_profile_field_name', function($field_name) {
    if (function_exists('icl_t')) {
        $field_id = bp_get_the_profile_field_id();
        return icl_t('buddypress', 'field_' . $field_id, $field_name);
    }
    return $field_name;
});

// Translate field options
add_filter('bp_get_the_profile_field_options', function($options) {
    if (function_exists('icl_t')) {
        foreach ($options as &$option) {
            $option->name = icl_t('buddypress', 'option_' . $option->id, $option->name);
        }
    }
    return $options;
});
```

### Groups

```php
// Translate group names and descriptions
add_filter('bp_get_group_name', function($name) {
    if (function_exists('icl_t')) {
        $group_id = bp_get_group_id();
        return icl_t('buddypress-groups', 'group_name_' . $group_id, $name);
    }
    return $name;
});

add_filter('bp_get_group_description', function($desc) {
    if (function_exists('icl_t')) {
        $group_id = bp_get_group_id();
        return icl_t('buddypress-groups', 'group_desc_' . $group_id, $desc);
    }
    return $desc;
});
```

## WooCommerce Translation

### Product Translation

```php
// Sync product data across translations
add_action('woocommerce_save_product', function($product_id) {
    if (class_exists('SitePress')) {
        global $sitepress;

        $trid = $sitepress->get_element_trid($product_id, 'post_product');
        $translations = $sitepress->get_element_translations($trid, 'post_product');

        foreach ($translations as $lang => $translation) {
            if ($translation->element_id != $product_id) {
                // Sync stock
                update_post_meta($translation->element_id, '_stock', get_post_meta($product_id, '_stock', true));

                // Sync price
                update_post_meta($translation->element_id, '_price', get_post_meta($product_id, '_price', true));
            }
        }
    }
});
```

### Checkout Translation

```php
// Translate checkout fields
add_filter('woocommerce_checkout_fields', function($fields) {
    if (function_exists('icl_t')) {
        foreach ($fields as $section => &$section_fields) {
            foreach ($section_fields as $key => &$field) {
                $field['label'] = icl_t('woocommerce', $key . '_label', $field['label']);
                if (isset($field['placeholder'])) {
                    $field['placeholder'] = icl_t('woocommerce', $key . '_placeholder', $field['placeholder']);
                }
            }
        }
    }
    return $fields;
});
```

## Page Builder Translation

### Elementor Integration

```php
// Make Elementor content translatable
add_filter('elementor/frontend/the_content', function($content) {
    if (function_exists('icl_object_id') && is_singular()) {
        global $post;
        $translated_id = icl_object_id($post->ID, $post->post_type, true);

        if ($translated_id != $post->ID) {
            // Get translated Elementor data
            $elementor_data = get_post_meta($translated_id, '_elementor_data', true);
            if ($elementor_data) {
                $content = Elementor\Plugin::instance()->frontend->get_builder_content($translated_id);
            }
        }
    }
    return $content;
});
```

### Gutenberg Blocks

```php
// Register block strings for translation
add_action('init', function() {
    if (function_exists('register_block_type')) {
        register_block_type('reign/custom-block', array(
            'attributes' => array(
                'title' => array(
                    'type' => 'string',
                    'source' => 'text',
                    'selector' => '.block-title',
                    'translation' => true // Mark for translation
                ),
                'content' => array(
                    'type' => 'string',
                    'source' => 'html',
                    'selector' => '.block-content',
                    'translation' => true
                )
            )
        ));
    }
});
```

## RTL Support

### RTL Languages

```php
// Add RTL support for specific languages
add_action('wp_head', function() {
    if (function_exists('is_rtl') && is_rtl()) {
        ?>
        <style>
        /* RTL overrides */
        body.rtl {
            direction: rtl;
            text-align: right;
        }

        .rtl .reign-header-v1 .site-branding {
            float: right;
        }

        .rtl .reign-header-v1 .main-navigation {
            float: left;
        }

        .rtl .activity-list {
            padding-right: 0;
            padding-left: 20px;
        }
        </style>
        <?php
    }
});

// Check if current language is RTL
function reign_is_rtl_language() {
    $rtl_languages = array('ar', 'he', 'fa', 'ur');
    $current_lang = ICL_LANGUAGE_CODE;
    return in_array($current_lang, $rtl_languages);
}
```

## SEO Optimization

### Hreflang Tags

```php
// Add hreflang tags
add_action('wp_head', function() {
    if (function_exists('icl_get_languages')) {
        $languages = icl_get_languages('skip_missing=0');

        foreach ($languages as $lang) {
            echo '<link rel="alternate" hreflang="' . $lang['language_code'] . '" href="' . $lang['url'] . '" />' . "\n";
        }

        // x-default
        $default_lang = icl_get_default_language();
        echo '<link rel="alternate" hreflang="x-default" href="' . $languages[$default_lang]['url'] . '" />' . "\n";
    }
});
```

### Translated Sitemaps

```php
// Add translations to sitemap
add_filter('wpseo_sitemap_url', function($url, $post) {
    if (function_exists('icl_object_id')) {
        $languages = icl_get_languages('skip_missing=0');

        foreach ($languages as $lang) {
            if ($lang['language_code'] != ICL_LANGUAGE_CODE) {
                $translated_id = icl_object_id($post->ID, $post->post_type, false, $lang['language_code']);

                if ($translated_id) {
                    $translated_url = get_permalink($translated_id);
                    // Add to sitemap
                    echo '<url>';
                    echo '<loc>' . $translated_url . '</loc>';
                    echo '<xhtml:link rel="alternate" hreflang="' . $lang['language_code'] . '" href="' . $translated_url . '" />';
                    echo '</url>';
                }
            }
        }
    }
    return $url;
}, 10, 2);
```

## Translation Workflow

### String Translation Process

1. **Scan for Strings**
   ```
   WPML → String Translation
   - Click "Scan themes for strings"
   - Select "Reign Theme"
   - Scan
   ```

2. **Translate Strings**
   ```
   - Filter by domain: "reign-theme"
   - Click on string to translate
   - Enter translations for each language
   - Save
   ```

3. **Auto-translate**
   ```php
   // Enable auto-translation
   add_filter('wpml_st_auto_translate', '__return_true');

   // Set auto-translation service
   add_filter('wpml_st_translation_service', function() {
       return 'google'; // or 'microsoft', 'deepl'
   });
   ```

### Content Translation

```php
// Duplicate content to all languages
function reign_duplicate_to_languages($post_id) {
    if (class_exists('SitePress')) {
        global $sitepress;

        $post = get_post($post_id);
        $languages = $sitepress->get_active_languages();
        $default_language = $sitepress->get_default_language();

        foreach ($languages as $lang) {
            if ($lang['code'] != $default_language) {
                $sitepress->make_duplicate($post_id, $lang['code']);
            }
        }
    }
}
```

## Performance Optimization

### Cache Management

```php
// Clear WPML cache
add_action('reign_clear_cache', function() {
    if (class_exists('WPML_Cache_Factory')) {
        $cache = new WPML_Cache_Factory();
        $cache->get('wpml_cache')->flush_group_cache();
    }
});

// Language-specific cache
function reign_get_language_cache($key) {
    $lang = ICL_LANGUAGE_CODE;
    $cache_key = $key . '_' . $lang;
    return get_transient($cache_key);
}
```

### Query Optimization

```php
// Optimize multilingual queries
add_filter('posts_join', function($join, $query) {
    if (!is_admin() && class_exists('SitePress')) {
        global $wpdb, $sitepress;

        // Only join translations table when necessary
        if ($query->get('suppress_filters')) {
            return $join;
        }

        $current_language = $sitepress->get_current_language();
        $join .= " LEFT JOIN {$wpdb->prefix}icl_translations t
                  ON {$wpdb->posts}.ID = t.element_id
                  AND t.element_type = CONCAT('post_', {$wpdb->posts}.post_type)
                  AND t.language_code = '{$current_language}'";
    }
    return $join;
}, 10, 2);
```

## Common Issues & Solutions

### Language Switcher Not Showing

```php
// Fix language switcher
add_action('init', function() {
    if (!has_action('wpml_add_language_selector')) {
        function wpml_add_language_selector() {
            do_action('wpml_language_selector');
        }
    }
});
```

### Missing Translations

```php
// Fallback to default language
add_filter('wpml_translate_string', function($string, $context, $name) {
    if (empty($string) && function_exists('icl_get_default_language')) {
        $default_lang = icl_get_default_language();
        $string = icl_t($context, $name, $string, $default_lang);
    }
    return $string;
}, 10, 3);
```

### Broken URLs

```php
// Fix translated URLs
add_filter('wpml_permalink', function($url, $lang) {
    // Ensure proper URL structure
    if (strpos($url, '/' . $lang . '/') === false) {
        $url = str_replace(home_url(), home_url($lang), $url);
    }
    return $url;
}, 10, 2);
```

## Testing Translations

### Automated Testing

```php
// Test translations exist
function test_wpml_translations() {
    $test_strings = array(
        'Welcome Message' => 'reign-theme',
        'Login Button' => 'reign-theme',
        'Register Button' => 'reign-theme'
    );

    $languages = icl_get_languages();
    $missing = array();

    foreach ($test_strings as $string => $domain) {
        foreach ($languages as $lang) {
            $translation = icl_t($domain, $string, $string, $lang['code']);
            if ($translation == $string && $lang['code'] != 'en') {
                $missing[] = $string . ' (' . $lang['code'] . ')';
            }
        }
    }

    return $missing;
}
```

### Language Testing Checklist

```php
// Checklist for testing
function reign_wpml_checklist() {
    $checks = array(
        'WPML Active' => class_exists('SitePress'),
        'String Translation Active' => defined('WPML_ST_VERSION'),
        'Languages Configured' => count(icl_get_languages()) > 1,
        'Menu Locations Synced' => has_nav_menu('primary'),
        'Theme Strings Registered' => wpml_st_get_string_id('reign-theme', 'Welcome Message'),
        'RTL Support' => file_exists(get_template_directory() . '/rtl.css')
    );

    return $checks;
}
```

## Best Practices

### 1. Use Context

```php
// Always provide context for translations
__('Button', 'reign'); // Bad
__('Login Button', 'reign'); // Good
__('Header Login Button', 'reign'); // Better
```

### 2. Avoid Concatenation

```php
// Bad
$message = __('Welcome', 'reign') . ' ' . $username;

// Good
$message = sprintf(__('Welcome %s', 'reign'), $username);
```

### 3. Register All Strings

```php
// Register all dynamic strings
add_action('init', function() {
    $dynamic_strings = get_option('reign_dynamic_strings', array());

    foreach ($dynamic_strings as $string) {
        icl_register_string('reign-dynamic', sanitize_title($string), $string);
    }
});
```

---

*For more internationalization options, see the Theme Settings documentation.*