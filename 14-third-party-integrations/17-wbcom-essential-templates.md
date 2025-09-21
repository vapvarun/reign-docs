# Wbcom Essential Templates Documentation

## Overview

Wbcom Essential (Version 4.0.0) is a premium Elementor addon plugin for Reign Theme that provides 40+ professional widgets, pre-designed templates, and seamless integrations with BuddyPress, WooCommerce, and WordPress. It extends Elementor's capabilities with specialized widgets for building community sites, social networks, and marketplaces.

## What is Wbcom Essential?

Wbcom Essential offers:
- **40+ Custom Widgets:** Specialized for BuddyPress, WooCommerce, and WordPress
- **Pre-built Templates:** Professional page and section templates via API
- **BuddyPress Widgets:** Members, Groups, Forums, Activity widgets
- **WooCommerce Widgets:** Product displays, reviews, testimonials
- **General Widgets:** Sliders, carousels, tabs, accordions, and more
- **Remote Template Library:** Cloud-based templates from demos.wbcomdesigns.com
- **Elementor 3.0+ Support:** Full compatibility with latest Elementor
- **Performance Optimized:** Smart loading and caching

## Installation

### Installing Wbcom Essential

1. **From WBcom Designs (Premium)**
   ```
   1. Purchase from wbcomdesigns.com
   2. Download wbcom-essential.zip
   3. WordPress Admin → Plugins → Add New → Upload
   4. Install and Activate
   5. Enter license key in Wbcom Essential → License
   ```

2. **Manual Installation**
   ```
   1. Upload plugin files to /wp-content/plugins/wbcom-essential/
   2. Activate through WordPress Plugins menu
   3. Elementor must be installed and activated
   ```

### Requirements

```
WordPress: 5.8+
PHP: 7.2+
Elementor: 3.0+ (Required)
Reign Theme: Recommended
License: Required for updates and support
```

### Plugin Structure

```
wbcom-essential/
├── plugins/
│   └── elementor/
│       ├── widgets/
│       │   ├── Buddypress/    # BuddyPress widgets
│       │   ├── General/       # General purpose widgets
│       │   └── WooCommerce/   # WooCommerce widgets
│       ├── templates/
│       │   ├── classes/       # Template system classes
│       │   ├── sources/       # Template API sources
│       │   └── types/         # Template types (page/section)
│       └── hooks/             # Elementor hooks
├── assets/                    # CSS, JS, Images
└── license/                   # EDD licensing system
```

## Template Library

### Accessing Templates

The template library connects to the remote API at `https://demos.wbcomdesigns.com/elementor/` to fetch templates.

**Within Elementor:**
1. Edit page with Elementor
2. Click the folder icon in the panel
3. "WBCom Essential Elementor Sections" tab appears
4. Browse and insert templates

### Template API Configuration

```php
// Template API endpoints (from config.php)
'api' => array(
    'enabled'   => true,
    'base'      => 'https://demos.wbcomdesigns.com/elementor/',
    'path'      => 'wp-json/wp/v2/wbcom-essential-elementor',
    'endpoints' => array(
        'templates'  => '/templates/',   // Get all templates
        'categories' => '/categories/',  // Get categories
        'template'   => '/template/',    // Get single template
    ),
)
```

### Available Widget Categories

#### BuddyPress Widgets
- **MembersGrid** - Display members in grid layout
- **MembersList** - List view of members
- **MemberCarousel** - Rotating member showcase
- **GroupGrid** - Groups in grid format
- **GroupsList** - Groups list view
- **GroupCarousel** - Rotating groups display
- **Forums** - bbPress forum integration
- **ForumsActivity** - Forum activity stream
- **HeaderBar** - BuddyPress header with notifications
- **DashboardIntro** - Member dashboard welcome
- **ProfileCompletion** - Profile progress widget

#### General Widgets
- **Accordion** - Expandable content sections
- **Branding** - Logo and site identity
- **Countdown** - Event countdown timer
- **DropdownButton** - Button with dropdown menu
- **FlipBox** - Animated flip cards
- **Heading** - Advanced heading styles
- **LoginForm** - Custom login/register form
- **NotificationArea** - Alert notifications
- **PortfolioGrid** - Portfolio showcase
- **PostCarousel** - Blog posts carousel
- **PostSlider** - Featured posts slider
- **PostsRevolution** - Advanced post display
- **PostTimeline** - Chronological posts
- **PostsTicker** - News ticker
- **PricingTable** - Pricing plans display
- **ProgressBar** - Animated progress bars
- **Shape** - Decorative shapes
- **SiteLogo** - Dynamic site logo
- **Slider** - Content slider
- **SmartMenu** - Advanced navigation
- **Tabs** - Tabbed content
- **TeamCarousel** - Team members showcase
- **Testimonial** - Single testimonial
- **TestimonialCarousel** - Multiple testimonials
- **TextRotator** - Animated text
- **Timeline** - Events timeline

#### WooCommerce Widgets
- **AddBanner** - Product promotional banner
- **CustomerReview** - Customer reviews display
- **ProductTab** - Tabbed product display
- **UniversalProduct** - Flexible product layout
- **WcTestimonial** - Product testimonials

## Using Widgets

### Widget Implementation

All widgets extend `\Elementor\Widget_Base` and are registered in the `wbcom-elements` category.

#### Example: Members Grid Widget

```php
namespace WBCOM_ESSENTIAL\ELEMENTOR\Widgets\Buddypress;

class MembersGrid extends \Elementor\Widget_Base {

    public function get_name() {
        return 'wbcom-members-grid';
    }

    public function get_title() {
        return esc_html__( 'Members Grid', 'wbcom-essential' );
    }

    public function get_categories() {
        return array( 'wbcom-elements' );
    }

    // Widget controls for customization
    protected function register_controls() {
        $this->add_control(
            'type',
            array(
                'label'   => esc_html__( 'Sort', 'wbcom-essential' ),
                'type'    => Controls_Manager::SELECT,
                'default' => 'newest',
                'options' => array(
                    'newest'  => __( 'Newest', 'wbcom-essential' ),
                    'active'  => __( 'Recently Active', 'wbcom-essential' ),
                    'popular' => __( 'Most Popular', 'wbcom-essential' ),
                    'online'  => __( 'Online', 'wbcom-essential' ),
                    'random'  => __( 'Random', 'wbcom-essential' ),
                )
            )
        );
    }
}
```

### Using Templates from API

Templates are fetched from the remote API and can be inserted directly into Elementor:

1. **In Elementor Editor**
   - Click the folder icon
   - Select "WBCom Essential Elementor Sections"
   - Templates load from API
   - Click "Insert" to add to page

2. **Template Types**
   - **Page Templates**: Complete page layouts
   - **Section Templates**: Reusable content blocks

### Importing Sections

```javascript
// Import section via AJAX
jQuery(document).on('click', '.wbcom-import-section', function(e) {
    e.preventDefault();

    var sectionId = jQuery(this).data('section-id');

    jQuery.ajax({
        url: wbcom_ajax.ajaxurl,
        type: 'POST',
        data: {
            action: 'wbcom_import_section',
            section_id: sectionId,
            _ajax_nonce: wbcom_ajax.nonce
        },
        success: function(response) {
            if (response.success) {
                // Section HTML returned
                jQuery('.page-content').append(response.data.html);
            }
        }
    });
});
```

## Template Customization

### Global Styling

```php
// Apply Reign theme colors to templates
add_filter('wbcom_template_styles', function($styles) {
    $primary_color = get_theme_mod('reign_site_primary_color', '#3498db');
    $secondary_color = get_theme_mod('reign_site_secondary_color', '#2c3e50');

    $styles = str_replace('#primary-color#', $primary_color, $styles);
    $styles = str_replace('#secondary-color#', $secondary_color, $styles);

    return $styles;
});
```

### Dynamic Content

```php
// Replace template placeholders with dynamic content
add_filter('wbcom_template_content', function($content) {
    // Member count
    if (function_exists('bp_get_total_member_count')) {
        $content = str_replace('[member_count]', bp_get_total_member_count(), $content);
    }

    // Group count
    if (function_exists('groups_get_total_group_count')) {
        $content = str_replace('[group_count]', groups_get_total_group_count(), $content);
    }

    // Site name
    $content = str_replace('[site_name]', get_bloginfo('name'), $content);

    // Login URL
    $content = str_replace('[login_url]', wp_login_url(), $content);

    return $content;
});
```

### Template Hooks

```php
// Before template render
add_action('wbcom_before_template_render', function($template) {
    // Add custom wrapper
    echo '<div class="reign-template-wrapper">';
});

// After template render
add_action('wbcom_after_template_render', function($template) {
    echo '</div>';

    // Add custom scripts
    ?>
    <script>
    jQuery(document).ready(function($) {
        // Initialize template components
        $('.wbcom-slider').slick();
        $('.wbcom-counter').countUp();
    });
    </script>
    <?php
});
```

## Section Library

### Hero Sections

```html
<!-- Hero Style 1: Full Width with CTA -->
<section class="wbcom-hero-1">
    <div class="container">
        <div class="row align-items-center">
            <div class="col-lg-6">
                <h1>Build Your Community</h1>
                <p>Connect, share, and grow together</p>
                <a href="#" class="btn btn-primary">Get Started</a>
                <a href="#" class="btn btn-outline">Learn More</a>
            </div>
            <div class="col-lg-6">
                <img src="hero-image.jpg" alt="Hero">
            </div>
        </div>
    </div>
</section>
```

### Feature Sections

```php
// Dynamic feature grid
function wbcom_feature_grid($features) {
    ?>
    <section class="wbcom-features">
        <div class="container">
            <div class="row">
                <?php foreach ($features as $feature): ?>
                    <div class="col-lg-4 col-md-6">
                        <div class="feature-card">
                            <div class="feature-icon">
                                <i class="<?php echo esc_attr($feature['icon']); ?>"></i>
                            </div>
                            <h3><?php echo esc_html($feature['title']); ?></h3>
                            <p><?php echo esc_html($feature['description']); ?></p>
                        </div>
                    </div>
                <?php endforeach; ?>
            </div>
        </div>
    </section>
    <?php
}
```

### Testimonials

```javascript
// Testimonial slider initialization
class TestimonialSlider {
    constructor() {
        this.initSlider();
    }

    initSlider() {
        jQuery('.wbcom-testimonials').slick({
            dots: true,
            infinite: true,
            speed: 500,
            slidesToShow: 3,
            slidesToScroll: 1,
            autoplay: true,
            autoplaySpeed: 5000,
            responsive: [
                {
                    breakpoint: 1024,
                    settings: {
                        slidesToShow: 2
                    }
                },
                {
                    breakpoint: 768,
                    settings: {
                        slidesToShow: 1
                    }
                }
            ]
        });
    }
}
```

### Call-to-Action

```css
/* CTA section styles */
.wbcom-cta {
    background: linear-gradient(135deg, var(--reign-primary-color) 0%, var(--reign-secondary-color) 100%);
    padding: 80px 0;
    text-align: center;
    color: white;
}

.wbcom-cta h2 {
    font-size: 3em;
    margin-bottom: 20px;
}

.wbcom-cta .btn-group {
    display: flex;
    gap: 20px;
    justify-content: center;
    margin-top: 30px;
}

.wbcom-cta .btn {
    padding: 15px 40px;
    font-size: 18px;
    border-radius: 50px;
}
```

## Widget Features

### BuddyPress Widget Controls

Each BuddyPress widget includes extensive customization options:

```php
// Common controls for BuddyPress widgets
$this->add_control(
    'max_item',
    [
        'label' => __( 'Number of Members', 'wbcom-essential' ),
        'type' => Controls_Manager::NUMBER,
        'default' => 10,
        'min' => 1,
        'max' => 100,
    ]
);

$this->add_control(
    'columns',
    [
        'label' => __( 'Columns', 'wbcom-essential' ),
        'type' => Controls_Manager::SELECT,
        'default' => '3',
        'options' => [
            '2' => '2',
            '3' => '3',
            '4' => '4',
            '5' => '5',
            '6' => '6',
        ],
    ]
);

$this->add_control(
    'member_type',
    [
        'label' => __( 'Member Type', 'wbcom-essential' ),
        'type' => Controls_Manager::SELECT,
        'default' => 'all',
        'options' => wbcom_essential_get_member_types(),
    ]
);
```

### Styling Controls

Widgets include comprehensive styling options:

```php
// Typography controls
$this->add_group_control(
    Group_Control_Typography::get_type(),
    [
        'name' => 'title_typography',
        'label' => __( 'Typography', 'wbcom-essential' ),
        'selector' => '{{WRAPPER}} .member-name',
    ]
);

// Background controls
$this->add_group_control(
    Group_Control_Background::get_type(),
    [
        'name' => 'card_background',
        'label' => __( 'Background', 'wbcom-essential' ),
        'types' => [ 'classic', 'gradient' ],
        'selector' => '{{WRAPPER}} .member-card',
    ]
);
```

## License Management

### EDD License System

Wbcom Essential uses Easy Digital Downloads (EDD) for license management:

```php
// License configuration (from loader.php)
define( 'WBCOM_ESSENTIAL_STORE_URL', 'https://wbcomdesigns.com' );
define( 'WBCOM_ESSENTIAL_ITEM_ID', 1545975 );
define( 'WBCOM_ESSENTIAL_ITEM_NAME', 'Wbcom Essential' );
```

### License Activation

1. **Navigate to:** Wbcom Essential → License
2. **Enter license key** from your WBcom Designs account
3. **Activate** to enable updates and support

### License Validation

```php
// License validation happens via EDD API
class WBCOM_ESSENTIAL_License_Manager {
    public function validate_license($license_key) {
        $api_params = array(
            'edd_action' => 'activate_license',
            'license'    => $license_key,
            'item_id'    => WBCOM_ESSENTIAL_ITEM_ID,
            'url'        => home_url()
        );

        $response = wp_remote_post(WBCOM_ESSENTIAL_STORE_URL, array(
            'body' => $api_params
        ));

        return json_decode(wp_remote_retrieve_body($response));
    }
}
```

## Performance Optimization

### Template Caching

```php
// Cache imported templates
add_filter('wbcom_cache_template', function($template_data) {
    $cache_key = 'wbcom_template_' . $template_data['id'];
    $cached = get_transient($cache_key);

    if ($cached === false) {
        // Process template
        $processed = wbcom_process_template($template_data);
        set_transient($cache_key, $processed, DAY_IN_SECONDS);
        return $processed;
    }

    return $cached;
});
```

### Lazy Load Templates

```javascript
// Lazy load template sections
class LazyTemplateLoader {
    constructor() {
        this.observer = null;
        this.init();
    }

    init() {
        this.observer = new IntersectionObserver(
            (entries) => this.handleIntersection(entries),
            { rootMargin: '100px' }
        );

        document.querySelectorAll('.wbcom-lazy-section').forEach(section => {
            this.observer.observe(section);
        });
    }

    handleIntersection(entries) {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                this.loadSection(entry.target);
                this.observer.unobserve(entry.target);
            }
        });
    }

    loadSection(section) {
        const templateId = section.dataset.templateId;

        fetch(`/wp-json/wbcom/v1/template/${templateId}`)
            .then(response => response.json())
            .then(data => {
                section.innerHTML = data.content;
                section.classList.remove('wbcom-lazy-section');
                section.classList.add('wbcom-loaded');
            });
    }
}
```

## Widget Usage Examples

### BuddyPress Members Grid

```php
// Using the Members Grid widget in a template
if (class_exists('\WBCOM_ESSENTIAL\ELEMENTOR\Widgets\Buddypress\MembersGrid')) {
    // Widget is available
    // Can be added via Elementor interface
}

// Shortcode usage (if available)
[wbcom_members_grid type="active" max_item="12" columns="4"]
```

### HeaderBar Widget Features

The HeaderBar widget includes:
- BuddyPress notifications dropdown
- Messages dropdown
- Cart dropdown (WooCommerce)
- User profile menu
- Custom navigation

### Post Display Widgets

Multiple post display options:
- **PostCarousel** - Sliding carousel of posts
- **PostSlider** - Featured post slider
- **PostTimeline** - Chronological timeline
- **PostsTicker** - News ticker style
- **PostsRevolution** - Advanced animations

## Updates & Maintenance

### Automatic Updates

Updates are managed through the EDD updater system:

```php
// EDD updater checks for updates
class WBCOM_ESSENTIAL_License_Updater {
    public function __construct() {
        // Check for updates every 12 hours
        add_action('admin_init', array($this, 'check_for_updates'));
    }

    public function check_for_updates() {
        $updater = new EDD_SL_Plugin_Updater(
            WBCOM_ESSENTIAL_STORE_URL,
            WBCOM_ESSENTIAL_FILE,
            array(
                'version' => WBCOM_ESSENTIAL_VERSION,
                'license' => get_option('wbcom_essential_license_key'),
                'item_id' => WBCOM_ESSENTIAL_ITEM_ID,
                'author'  => 'WBcom Designs',
                'beta'    => false,
            )
        );
    }
}
```

## Troubleshooting

### Common Issues

#### Elementor Not Detected

If you see "WBcom Essential requires Elementor" notice:
1. Install Elementor from wordpress.org/plugins/elementor
2. Activate Elementor before Wbcom Essential
3. Ensure Elementor version is 3.0+

#### Templates Not Loading from API

```php
// Check API connectivity
$api_url = 'https://demos.wbcomdesigns.com/elementor/wp-json/wp/v2/wbcom-essential-elementor/templates/';
$response = wp_remote_get($api_url, array('timeout' => 60));

if (is_wp_error($response)) {
    error_log('API Error: ' . $response->get_error_message());
}
```

#### Widget Not Appearing

1. Check widget category is registered:
   - Look for "Wbcom Elements" in Elementor panel
2. Verify BuddyPress/WooCommerce is active for respective widgets
3. Clear Elementor cache: Elementor → Tools → Regenerate CSS

#### License Issues

```php
// Debug license status
$license_data = get_option('wbcom_essential_license_status');
if ($license_data && $license_data->license !== 'valid') {
    // License is invalid or expired
    error_log('License Status: ' . $license_data->license);
}
```

## Best Practices

### 1. Widget Performance

```php
// Use transients for expensive queries in widgets
public function render() {
    $cache_key = 'wbcom_members_' . md5(serialize($this->get_settings()));
    $members = get_transient($cache_key);

    if (false === $members) {
        // Expensive query
        $members = bp_core_get_users($args);
        set_transient($cache_key, $members, HOUR_IN_SECONDS);
    }

    // Render members
}
```

### 2. Responsive Design

All widgets include responsive controls:
- Desktop/Tablet/Mobile column settings
- Breakpoint-specific styling
- Touch-friendly interfaces

### 3. Compatibility

- Always check for function existence before using BuddyPress/WooCommerce functions
- Use proper namespacing: `WBCOM_ESSENTIAL\ELEMENTOR`
- Follow Elementor widget development standards

## Support & Documentation

- **Documentation:** [wbcomdesigns.com/docs](https://wbcomdesigns.com/docs)
- **Support:** [wbcomdesigns.com/support](https://wbcomdesigns.com/support)
- **Updates:** Automatic with valid license
- **Compatibility:** Reign Theme + Elementor 3.0+

---

*Wbcom Essential extends Elementor with powerful widgets specifically designed for Reign Theme community sites.*