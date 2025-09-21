# Dark Mode Complete Configuration Guide

## Overview

Reign Theme includes a sophisticated dark mode system with automatic detection, user preferences, custom styling, and seamless transitions. The dark mode works across all theme components including BuddyPress, WooCommerce, and third-party plugins.

## Enabling Dark Mode

### Basic Setup

**Location:** `Customizer → General → Dark Mode`

**Core Settings:**
```
Enable Dark Mode: ON
Default Mode: Light/Dark/Auto
Show Toggle: Yes
Toggle Style: Switch/Button/Icon/Minimal
Save User Preference: Yes
Transition Duration: 300ms
```

### Activation Methods

#### Method 1: Customizer
1. Navigate to `Customizer → General → Dark Mode`
2. Enable Dark Mode toggle
3. Configure default behavior
4. Set toggle position
5. Publish changes

#### Method 2: Code
```php
// Enable dark mode programmatically
add_filter('reign_dark_mode_enabled', '__return_true');

// Set default to dark
add_filter('reign_dark_mode_default', function() {
    return 'dark';
});
```

## Toggle Styles

### Available Toggle Designs

#### 1. Classic Switch
```css
/* iOS-style toggle switch */
.reign-dark-toggle-switch {
    width: 60px;
    height: 30px;
    border-radius: 30px;
    background: #ccc;
    position: relative;
}

.reign-dark-toggle-switch.active {
    background: var(--reign-primary-color);
}
```

#### 2. Icon Button
```css
/* Sun/Moon icon toggle */
.reign-dark-toggle-icon {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
}
```

#### 3. Text Button
```css
/* Text-based toggle */
.reign-dark-toggle-text {
    padding: 8px 16px;
    border: 1px solid currentColor;
    border-radius: 4px;
}
```

#### 4. Minimal Dot
```css
/* Minimal indicator */
.reign-dark-toggle-minimal {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background: currentColor;
}
```

### Toggle Positions

**Available Positions:**
- Header Top Bar
- Header Main Menu
- Fixed Bottom Left
- Fixed Bottom Right
- Fixed Top Left
- Fixed Top Right
- Mobile Menu
- User Account Menu
- Custom Position (via shortcode)

**Position Settings:**
```php
// Set toggle position
add_filter('reign_dark_toggle_position', function() {
    return array(
        'location' => 'header',
        'alignment' => 'right',
        'priority' => 20
    );
});
```

## Color Schemes

### Dark Mode Color Variables

```css
/* Dark mode root variables */
[data-theme="dark"] {
    /* Background colors */
    --reign-body-bg: #1a1a1a;
    --reign-content-bg: #242424;
    --reign-sidebar-bg: #2a2a2a;
    --reign-header-bg: #1f1f1f;
    --reign-footer-bg: #161616;

    /* Text colors */
    --reign-text-primary: #e0e0e0;
    --reign-text-secondary: #b0b0b0;
    --reign-text-muted: #808080;
    --reign-heading-color: #ffffff;

    /* Border colors */
    --reign-border-color: #333333;
    --reign-border-light: #2a2a2a;
    --reign-border-dark: #404040;

    /* Component colors */
    --reign-card-bg: #2a2a2a;
    --reign-input-bg: #333333;
    --reign-button-bg: #404040;
    --reign-dropdown-bg: #2a2a2a;

    /* Accent colors */
    --reign-primary-color: #4a90e2;
    --reign-success-color: #5cb85c;
    --reign-warning-color: #f0ad4e;
    --reign-danger-color: #d9534f;
}
```

### Component-Specific Colors

#### BuddyPress Dark Mode
```css
[data-theme="dark"] {
    /* Activity stream */
    --bp-activity-bg: #2a2a2a;
    --bp-activity-border: #333333;
    --bp-activity-meta: #808080;

    /* Member cards */
    --bp-member-card-bg: #242424;
    --bp-member-card-hover: #2a2a2a;

    /* Groups */
    --bp-group-header-bg: #1f1f1f;
    --bp-group-nav-bg: #242424;
}
```

#### WooCommerce Dark Mode
```css
[data-theme="dark"] {
    /* Product cards */
    --wc-product-bg: #2a2a2a;
    --wc-product-hover: #333333;

    /* Cart/Checkout */
    --wc-form-bg: #242424;
    --wc-table-bg: #2a2a2a;

    /* Prices */
    --wc-price-color: #5cb85c;
    --wc-sale-color: #d9534f;
}
```

## Auto Detection

### System Preference Detection

```javascript
// Detect system dark mode preference
if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
    document.documentElement.setAttribute('data-theme', 'dark');
}

// Listen for system changes
window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', e => {
    const newTheme = e.matches ? 'dark' : 'light';
    reign_set_theme(newTheme);
});
```

### Time-Based Switching

```php
// Auto dark mode based on time
add_filter('reign_dark_mode_auto', function() {
    $hour = date('G');
    return ($hour >= 19 || $hour <= 6) ? 'dark' : 'light';
});
```

### Location-Based (with API)

```javascript
// Switch based on sunrise/sunset
async function setThemeByLocation() {
    const position = await getCurrentPosition();
    const sunTimes = await getSunriseSunset(position.latitude, position.longitude);

    const now = new Date();
    const theme = (now > sunTimes.sunset || now < sunTimes.sunrise) ? 'dark' : 'light';
    reign_set_theme(theme);
}
```

## User Preferences

### Saving Preferences

```javascript
// Save user preference
function reign_save_theme_preference(theme) {
    // Cookie method
    document.cookie = `reign_theme=${theme};path=/;max-age=31536000`;

    // LocalStorage method
    localStorage.setItem('reign_theme', theme);

    // Database method (for logged-in users)
    if (reign_ajax.user_id) {
        jQuery.ajax({
            url: reign_ajax.ajaxurl,
            type: 'POST',
            data: {
                action: 'save_theme_preference',
                theme: theme,
                user_id: reign_ajax.user_id
            }
        });
    }
}
```

### Loading Preferences

```php
// Load user preference
add_action('init', function() {
    if (is_user_logged_in()) {
        $theme = get_user_meta(get_current_user_id(), 'reign_theme_preference', true);
    } else {
        $theme = $_COOKIE['reign_theme'] ?? 'auto';
    }

    wp_localize_script('reign-dark-mode', 'reign_theme_preference', $theme);
});
```

## Custom Styling

### Override Dark Mode Styles

```css
/* Custom dark mode overrides */
[data-theme="dark"] .custom-element {
    background: #custom-dark-bg;
    color: #custom-dark-text;
}

/* Exclude element from dark mode */
.no-dark-mode {
    background: white !important;
    color: black !important;
}
```

### Component Exceptions

```php
// Exclude specific elements
add_filter('reign_dark_mode_exclude', function($selectors) {
    $selectors[] = '.keep-light';
    $selectors[] = '#special-section';
    return $selectors;
});
```

## Transitions

### Smooth Theme Switching

```css
/* Transition all theme changes */
* {
    transition: background-color 0.3s ease,
                color 0.3s ease,
                border-color 0.3s ease;
}

/* Prevent transition on page load */
.no-transitions * {
    transition: none !important;
}
```

```javascript
// Smooth transition implementation
function reign_switch_theme(theme) {
    document.body.classList.add('theme-transitioning');

    setTimeout(() => {
        document.documentElement.setAttribute('data-theme', theme);
    }, 10);

    setTimeout(() => {
        document.body.classList.remove('theme-transitioning');
    }, 310);
}
```

## Image Handling

### Dark Mode Images

```html
<!-- Picture element for theme-specific images -->
<picture>
    <source srcset="logo-dark.png" media="(prefers-color-scheme: dark)">
    <img src="logo-light.png" alt="Logo">
</picture>
```

### CSS Image Filters

```css
/* Adjust images for dark mode */
[data-theme="dark"] img {
    opacity: 0.9;
}

[data-theme="dark"] .invert-in-dark {
    filter: invert(1) hue-rotate(180deg);
}

/* Dim bright images */
[data-theme="dark"] .dim-image {
    filter: brightness(0.8) contrast(1.2);
}
```

### Dynamic Image Switching

```javascript
// Switch images based on theme
document.querySelectorAll('[data-theme-src]').forEach(img => {
    const theme = document.documentElement.getAttribute('data-theme');
    const srcData = JSON.parse(img.dataset.themeSrc);
    img.src = srcData[theme] || srcData['light'];
});
```

## Plugin Compatibility

### Elementor Dark Mode

```css
/* Elementor sections */
[data-theme="dark"] .elementor-section {
    --e-section-bg: #1a1a1a;
}

[data-theme="dark"] .elementor-widget {
    --e-widget-bg: #2a2a2a;
}
```

### Contact Form 7

```css
/* Form fields */
[data-theme="dark"] .wpcf7 input,
[data-theme="dark"] .wpcf7 textarea {
    background: #333333;
    color: #e0e0e0;
    border-color: #444444;
}
```

### Yoast SEO

```css
/* Admin bar */
[data-theme="dark"] #wpadminbar {
    background: #1a1a1a;
}
```

## Advanced Features

### Custom Toggle Component

```php
// Create custom toggle
function reign_custom_dark_toggle() {
    ?>
    <div class="custom-dark-toggle" id="customDarkToggle">
        <span class="toggle-icon sun">☀️</span>
        <span class="toggle-slider"></span>
        <span class="toggle-icon moon">🌙</span>
    </div>
    <script>
    document.getElementById('customDarkToggle').addEventListener('click', function() {
        const currentTheme = document.documentElement.getAttribute('data-theme');
        const newTheme = currentTheme === 'dark' ? 'light' : 'dark';
        reign_set_theme(newTheme);
    });
    </script>
    <?php
}
```

### Theme Sync Across Tabs

```javascript
// Sync theme across browser tabs
window.addEventListener('storage', function(e) {
    if (e.key === 'reign_theme') {
        document.documentElement.setAttribute('data-theme', e.newValue);
    }
});
```

### A/B Testing Dark Mode

```php
// A/B test dark mode adoption
function reign_dark_mode_ab_test() {
    if (!isset($_COOKIE['reign_ab_group'])) {
        $group = rand(0, 1) ? 'control' : 'test';
        setcookie('reign_ab_group', $group, time() + MONTH_IN_SECONDS);
    }

    if ($_COOKIE['reign_ab_group'] === 'test') {
        add_filter('reign_dark_mode_default', function() {
            return 'dark';
        });
    }
}
```

## Performance Optimization

### CSS Loading Strategy

```php
// Load dark mode CSS conditionally
add_action('wp_enqueue_scripts', function() {
    if (isset($_COOKIE['reign_theme']) && $_COOKIE['reign_theme'] === 'dark') {
        wp_enqueue_style('reign-dark-mode', get_template_directory_uri() . '/dark-mode.css');
    }
});
```

### Prevent FOUC (Flash of Unstyled Content)

```html
<!-- In <head> before any CSS -->
<script>
(function() {
    var theme = localStorage.getItem('reign_theme') || 'auto';
    if (theme === 'auto') {
        theme = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    }
    document.documentElement.setAttribute('data-theme', theme);
})();
</script>
```

### Lazy Load Dark Styles

```javascript
// Load dark styles only when needed
function loadDarkStyles() {
    if (!document.getElementById('dark-mode-styles')) {
        const link = document.createElement('link');
        link.id = 'dark-mode-styles';
        link.rel = 'stylesheet';
        link.href = '/wp-content/themes/reign/css/dark-mode.css';
        document.head.appendChild(link);
    }
}
```

## Accessibility

### ARIA Attributes

```html
<!-- Toggle button accessibility -->
<button
    class="reign-dark-toggle"
    role="switch"
    aria-checked="false"
    aria-label="Toggle dark mode"
>
    <span class="sr-only">Toggle dark mode</span>
</button>
```

### Contrast Ratios

```css
/* Ensure WCAG AA compliance */
[data-theme="dark"] {
    /* Minimum 4.5:1 for normal text */
    --text-on-dark: #e0e0e0; /* 11.5:1 on #1a1a1a */

    /* Minimum 3:1 for large text */
    --heading-on-dark: #ffffff; /* 15.3:1 on #1a1a1a */

    /* UI elements 3:1 minimum */
    --border-on-dark: #666666; /* 3.1:1 on #1a1a1a */
}
```

### Keyboard Support

```javascript
// Keyboard shortcut for toggle
document.addEventListener('keydown', function(e) {
    // Ctrl/Cmd + Shift + D
    if ((e.ctrlKey || e.metaKey) && e.shiftKey && e.key === 'D') {
        e.preventDefault();
        reign_toggle_theme();
    }
});
```

## Testing Dark Mode

### Browser Testing

```javascript
// Force dark mode for testing
document.documentElement.setAttribute('data-theme', 'dark');

// Test system preference
window.matchMedia('(prefers-color-scheme: dark)').matches;

// Emulate in DevTools
// Chrome: Settings > Preferences > Appearance > Theme
// Firefox: about:config > ui.systemUsesDarkTheme
```

### Automated Testing

```javascript
// Cypress test example
describe('Dark Mode', () => {
    it('should toggle dark mode', () => {
        cy.visit('/');
        cy.get('.reign-dark-toggle').click();
        cy.get('html').should('have.attr', 'data-theme', 'dark');
    });

    it('should save preference', () => {
        cy.get('.reign-dark-toggle').click();
        cy.reload();
        cy.get('html').should('have.attr', 'data-theme', 'dark');
    });
});
```

## Troubleshooting

### Common Issues

#### Dark Mode Not Working
**Solutions:**
1. Check if enabled in Customizer
2. Clear all caches
3. Check JavaScript console
4. Verify CSS is loading

#### Images Too Dark/Bright
**Solutions:**
```css
/* Adjust image brightness */
[data-theme="dark"] img {
    filter: brightness(0.85);
}
```

#### Flash on Page Load
**Solution:**
Add inline script in `<head>` before CSS loads

#### Transitions Not Smooth
**Solutions:**
1. Check transition CSS
2. Reduce properties being transitioned
3. Use will-change property

## Code Snippets

### Force Dark Mode for User Role

```php
// Force dark mode for admins
add_filter('reign_dark_mode_default', function($mode) {
    if (current_user_can('administrator')) {
        return 'dark';
    }
    return $mode;
});
```

### Schedule-Based Dark Mode

```php
// Business hours light, after hours dark
add_filter('reign_theme_mode', function() {
    $hour = current_time('G');
    $day = current_time('w');

    // Mon-Fri 9-17 = light
    if ($day >= 1 && $day <= 5 && $hour >= 9 && $hour < 17) {
        return 'light';
    }
    return 'dark';
});
```

### Custom Dark Mode Class

```javascript
class ReignDarkMode {
    constructor() {
        this.theme = this.getSavedTheme();
        this.init();
    }

    init() {
        this.applyTheme();
        this.bindEvents();
        this.watchSystemPreference();
    }

    getSavedTheme() {
        return localStorage.getItem('reign_theme') || 'auto';
    }

    applyTheme() {
        let theme = this.theme;
        if (theme === 'auto') {
            theme = this.getSystemPreference();
        }
        document.documentElement.setAttribute('data-theme', theme);
    }

    toggle() {
        const current = document.documentElement.getAttribute('data-theme');
        const newTheme = current === 'dark' ? 'light' : 'dark';
        this.setTheme(newTheme);
    }

    setTheme(theme) {
        this.theme = theme;
        localStorage.setItem('reign_theme', theme);
        this.applyTheme();
    }

    getSystemPreference() {
        return window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
    }

    bindEvents() {
        document.querySelectorAll('[data-toggle-dark-mode]').forEach(el => {
            el.addEventListener('click', () => this.toggle());
        });
    }

    watchSystemPreference() {
        window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', () => {
            if (this.theme === 'auto') {
                this.applyTheme();
            }
        });
    }
}

// Initialize
new ReignDarkMode();
```

---

*For color customization options, see the Color Scheme Configuration guide.*