# Understanding Reign Architecture - How Your Theme Works

## The Big Picture

Think of Reign as a sophisticated framework that sits on top of WordPress, enhancing and extending its capabilities specifically for community and social websites. This guide helps you understand how everything connects.

## Theme Foundation

### What Makes Reign Special

**Traditional WordPress Theme:**
```
WordPress Core
└── Basic Theme
    └── Your Content
```

**Reign Theme Architecture:**
```
WordPress Core
├── Reign Framework
│   ├── Enhanced Templates
│   ├── Community Features
│   ├── Performance Optimization
│   └── Extended Customization
├── Plugin Integrations
│   ├── BuddyPress Enhancement
│   ├── WooCommerce Styling
│   └── Page Builder Compatibility
└── Your Unique Site
```

### Core Components Explained

#### 1. The Template System

**How Reign Displays Content:**

When someone visits your site, Reign follows this process:
1. Checks what type of page (blog, profile, shop, etc.)
2. Looks for specific template file
3. Applies your customizations
4. Renders the final page

**Template Priority (Hierarchy):**
```
Child Theme (if exists)
    ↓ (overrides)
Reign Theme Templates
    ↓ (overrides)
Plugin Templates
    ↓ (overrides)
WordPress Default
```

**Real Example:**
When viewing a BuddyPress profile:
1. First checks: child-theme/buddypress/members/single/home.php
2. Then checks: reign-theme/buddypress/members/single/home.php
3. Then checks: plugins/buddypress/templates/members/single/home.php
4. Uses first one found

#### 2. The Customizer Framework

**Kirki Integration:**
Reign uses Kirki to provide advanced customizer controls:

```
Your Settings → Kirki Processing → CSS Generation → Live Preview
```

**How Settings Apply:**
1. You change a color in customizer
2. Kirki processes the change
3. Generates optimized CSS
4. Applies without page reload
5. Saves to database when published

#### 3. The Hook System

**What Are Hooks?**
Hooks are connection points where you can add or modify functionality without editing theme files.

**Action Hooks Example:**
```
reign_before_header → Add announcement bar
reign_after_header → Add breadcrumbs
reign_before_content → Add welcome message
reign_after_content → Add related posts
```

**Filter Hooks Example:**
```
reign_header_class → Modify header CSS classes
reign_sidebar_position → Change sidebar location
reign_footer_text → Customize footer copyright
```

## File Structure Deep Dive

### Root Directory Files

```
reign-theme/
├── style.css           → Theme information & base styles
├── functions.php       → Theme initialization & features
├── index.php          → Fallback template
├── header.php         → Site header template
├── footer.php         → Site footer template
├── sidebar.php        → Default sidebar template
└── screenshot.png     → Theme preview image
```

### The /inc Directory - Theme Brain

```
/inc/
├── /core/             → Core functionality
│   ├── class-reign-theme.php      → Main theme class
│   ├── class-reign-customizer.php → Customizer setup
│   └── class-reign-walker-nav.php → Menu enhancements
├── /plugins/          → Plugin integrations
│   ├── buddypress.php      → BuddyPress enhancements
│   ├── woocommerce.php     → WooCommerce support
│   └── elementor.php       → Elementor compatibility
├── /widgets/          → Custom widgets
├── /lib/              → Third-party libraries
└── /admin/            → Admin functionality
```

### The /assets Directory - Resources

```
/assets/
├── /css/              → Stylesheets
│   ├── main.css           → Primary styles
│   ├── responsive.css     → Mobile styles
│   └── /vendors/          → Third-party CSS
├── /js/               → JavaScript files
│   ├── main.js            → Theme functionality
│   ├── customizer.js      → Live preview scripts
│   └── /vendors/          → Third-party scripts
├── /images/           → Theme images
└── /fonts/            → Custom fonts
```

### The /template-parts Directory

```
/template-parts/
├── /content/          → Post format templates
│   ├── content.php         → Standard post
│   ├── content-video.php   → Video post format
│   └── content-gallery.php → Gallery format
├── /header/           → Header variations
├── /footer/           → Footer variations
└── /sidebar/          → Sidebar variations
```

## How Reign Handles Different Content

### Blog Posts

**Process Flow:**
1. Request arrives for blog post
2. Reign checks post format (standard, video, gallery)
3. Loads appropriate template from /template-parts/content/
4. Applies layout settings (sidebar position)
5. Includes comments if enabled
6. Renders complete page

### BuddyPress Pages

**Community Content Flow:**
1. BuddyPress generates initial content
2. Reign applies custom templates from /buddypress/
3. Adds theme-specific styling
4. Integrates with theme layout
5. Maintains consistent design

### WooCommerce Shop

**E-commerce Flow:**
1. WooCommerce provides base shop functionality
2. Reign overrides templates in /woocommerce/
3. Applies custom product layouts
4. Adds theme-specific features (quick view, wishlist)
5. Maintains responsive design

## Performance Architecture

### How Reign Stays Fast

#### 1. Conditional Loading
```
Only loads what's needed:
- WooCommerce CSS → Only on shop pages
- BuddyPress JS → Only on community pages
- Forum styles → Only on bbPress pages
```

#### 2. Asset Optimization
```
Automatic optimization:
- CSS minification
- JavaScript compression
- Image lazy loading
- Font preloading
```

#### 3. Smart Caching
```
Built-in caching support:
- Fragment caching for dynamic content
- Transient API usage
- Database query optimization
- Compatible with cache plugins
```

## Customization Architecture

### Three Levels of Customization

#### Level 1: Theme Options (No Code)
```
Customizer → Visual Changes → Instant Preview
Examples:
- Colors, fonts, layouts
- Header styles
- Widget areas
- Menu positions
```

#### Level 2: Child Theme (Safe Code)
```
Child Theme → Override Templates → Preserve Updates
Examples:
- Custom page templates
- Modified layouts
- Additional functionality
- Custom styling
```

#### Level 3: Hooks & Filters (Advanced)
```
Functions.php → Add Code → Extend Functionality
Examples:
- Custom post types
- New features
- Third-party integrations
- Advanced modifications
```

## Database Structure

### How Reign Stores Settings

**WordPress Options Table:**
```
reign_options → All customizer settings (serialized)
reign_license → License activation data
reign_version → Current theme version
reign_install_date → First activation date
```

**Theme Mods:**
```
theme_mods_reign → Customizer modifications
widget_reign_* → Widget configurations
nav_menu_locations → Menu assignments
```

## Update System

### How Updates Work

**Update Check Process:**
1. Daily check for updates (if licensed)
2. Compares version numbers
3. Shows update notice if available
4. One-click update through dashboard
5. Preserves all customizations

**What Gets Updated:**
- Theme files
- Template improvements
- Security patches
- New features
- Bug fixes

**What's Preserved:**
- Your customizer settings
- Child theme modifications
- Database content
- Upload directory files
- Custom CSS

## Security Architecture

### Built-in Security Features

**Data Sanitization:**
- All inputs sanitized
- Database queries prepared
- Output properly escaped
- Nonces for forms

**File Security:**
- Direct file access prevented
- Sensitive files protected
- Proper file permissions
- No executable uploads

## Plugin Integration System

### How Reign Detects Plugins

**Detection Process:**
```php
// Reign checks if plugin is active
if (class_exists('BuddyPress')) {
    // Load BuddyPress-specific features
    // Apply BuddyPress templates
    // Add BuddyPress styling
}
```

**Integration Levels:**

**Basic Integration:**
- Styling compatibility
- Layout consistency
- Responsive design

**Deep Integration:**
- Custom templates
- Enhanced features
- Optimized performance
- Unified design

## Troubleshooting Architecture Issues

### Common Architecture Questions

**Q: Why don't my changes show?**
A: Check this cascade:
1. Cache (browser, plugin, server)
2. Child theme overriding
3. Plugin conflict
4. Incorrect template file

**Q: Which file controls what?**
A: Quick reference:
- Header appearance: header.php + customizer
- Menu structure: WordPress menus + walker class
- Post layout: template-parts/content-*.php
- Sidebar: sidebar.php + widgets

**Q: How do I find which template is used?**
A: Enable debug mode:
```php
// Add to wp-config.php
define('WP_DEBUG', true);

// Install "What The File" plugin
// Shows current template in admin bar
```

## Best Practices

### Working with Reign Architecture

**Do:**
- ✅ Use child theme for modifications
- ✅ Leverage built-in hooks
- ✅ Follow WordPress coding standards
- ✅ Test updates on staging first
- ✅ Keep customizations documented

**Don't:**
- ❌ Edit parent theme files directly
- ❌ Modify core WordPress files
- ❌ Bypass security functions
- ❌ Ignore update notifications
- ❌ Mix PHP in content areas

## Developer Resources

### Useful Functions

**Check Reign Version:**
```php
$theme = wp_get_theme();
$version = $theme->get('Version');
```

**Check Active Layout:**
```php
$layout = get_theme_mod('reign_site_layout', 'wide');
```

**Add Custom Hook:**
```php
add_action('reign_before_content', 'my_custom_function');
function my_custom_function() {
    echo '<div>Custom content</div>';
}
```

## Understanding Load Priority

### Page Load Sequence

1. **WordPress Core** initializes
2. **Plugins** load (alphabetically)
3. **Reign Theme** loads
4. **Child Theme** loads (if exists)
5. **Customizer Settings** apply
6. **Custom CSS** applies last

### Style Priority (Specificity)

1. Inline styles (highest)
2. Child theme styles
3. Custom CSS (customizer)
4. Reign theme styles
5. Plugin styles
6. WordPress default (lowest)

## Performance Monitoring

### Key Metrics to Watch

**Frontend Performance:**
- Page load time < 3 seconds
- First contentful paint < 1.5s
- Total page size < 3MB
- HTTP requests < 50

**Backend Performance:**
- Admin load time < 5 seconds
- Database queries < 100
- Memory usage < 128MB
- PHP execution < 30 seconds

---

**Understanding Complete?** Now you know how Reign works under the hood! This knowledge helps you customize effectively and troubleshoot issues quickly.