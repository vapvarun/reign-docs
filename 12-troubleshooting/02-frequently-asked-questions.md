# Frequently Asked Questions (FAQs)

## General Questions

### What is Reign Theme?

**Answer:** Reign is a premium WordPress theme specifically designed for creating online communities, social networks, and marketplaces. It's fully compatible with BuddyPress, BuddyBoss Platform, WooCommerce, and includes 7+ demos and extensive customization options.

### Where do I purchase Reign Theme?

**Answer:** You can purchase Reign Theme directly from [WBcom Designs](https://wbcomdesigns.com/downloads/reign-theme/). We use Easy Digital Downloads (EDD) for licensing, not ThemeForest.

### What's included with my purchase?

**Answer:**
- Reign Theme files
- Child theme
- 7+ demo content
- Lifetime updates
- 6 months support (extendable to 12 months)
- Documentation access
- PSD files (on request)

### Is Reign Theme GPL licensed?

**Answer:** Yes, Reign Theme is 100% GPL licensed. You can use it on unlimited sites for you or your clients.

## Installation & Setup

### What are the minimum requirements?

**Answer:**
```
WordPress: 5.8 or higher
PHP: 7.4 or higher (8.0+ recommended)
MySQL: 5.6 or higher
Memory: 128MB minimum (256MB recommended)
Max Upload: 32MB minimum
Max Execution Time: 300 seconds
```

### How do I activate my license?

**Answer:**
1. Log in to your [WBcom Designs account](https://wbcomdesigns.com/my-account/)
2. Copy your license key
3. In WordPress: `Reign Settings → License`
4. Enter and activate your license key

### Why is my license showing as invalid?

**Answer:**
Common reasons:
- License used on maximum allowed sites
- License expired
- Typo in license key
- Firewall blocking validation

**Solution:** Contact support with your order ID.

### How do I import demo content?

**Answer:**
1. Install required plugins: `Appearance → Install Plugins`
2. Go to `Reign Settings → Demo Import`
3. Choose your demo
4. Click "Import"
5. Wait for completion (5-10 minutes)

### Why did demo import fail?

**Answer:**
Common causes:
- PHP timeout (increase max_execution_time)
- Memory limit (increase to 256MB)
- Missing required plugins
- Server blocking external requests

## Customization Questions

### How do I change the header layout?

**Answer:**
1. `Customizer → Header → Header Layout`
2. Choose from 4 layouts (V1-V4)
3. Configure settings for each layout
4. Preview and publish

### Can I use a different font?

**Answer:**
Yes! Three methods:
1. **Google Fonts:** `Customizer → Typography` (900+ fonts)
2. **System Fonts:** Performance-optimized option
3. **Custom Fonts:** Upload your own fonts

### How do I enable dark mode?

**Answer:**
1. `Customizer → General → Dark Mode`
2. Enable Dark Mode: ON
3. Choose default mode (Light/Dark/Auto)
4. Select toggle style
5. Configure colors for dark theme

### How do I change colors?

**Answer:**
1. `Customizer → Colors`
2. Choose from 7 predefined schemes OR
3. Customize individual color options
4. Use CSS variables for advanced customization

### Can I create a boxed layout?

**Answer:**
Yes! `Customizer → General → Site Layout`
- Choose "Boxed" or "Framed" layout
- Set max width
- Configure background

## BuddyPress Integration

### Is BuddyPress required?

**Answer:** No, BuddyPress is optional. Reign works as a standard WordPress theme without it, but community features require BuddyPress or BuddyBoss Platform.

### How do I set up member profiles?

**Answer:**
1. Install and activate BuddyPress
2. `Settings → BuddyPress → Components`
3. Enable Extended Profiles
4. `Users → Profile Fields` to add fields
5. Configure in `Customizer → BuddyPress`

### Can I customize the activity stream?

**Answer:** Yes! Options include:
- Layout (standard/timeline)
- Elements to display
- Load more style
- Custom activity types
- Filtering options

### How do I enable user groups?

**Answer:**
1. `Settings → BuddyPress → Components`
2. Enable "User Groups"
3. Configure in `Customizer → BuddyPress → Groups`
4. Set creation permissions

### Why aren't avatars showing?

**Answer:**
Check:
- BuddyPress settings allow avatar uploads
- Upload directory permissions (755)
- PHP GD library installed
- Avatar size settings correct

## WooCommerce Questions

### Is WooCommerce compatible?

**Answer:** Yes! Reign is 100% WooCommerce compatible with:
- Custom shop layouts
- Product page designs
- Cart/checkout styling
- Vendor marketplace support

### How do I set up a marketplace?

**Answer:**
Reign supports:
1. **Dokan** - Install Dokan + Reign Dokan Addon
2. **WCFM** - Full integration built-in
3. **WC Vendors** - Compatible out of the box

### Can I customize the shop page?

**Answer:**
Yes! `Customizer → WooCommerce`:
- Products per row (2-6)
- Sidebar position
- Product elements
- Filter styles

### How do I enable catalog mode?

**Answer:**
1. Install WooCommerce
2. `WooCommerce → Settings → Products`
3. Enable "Catalog mode"
4. Hide prices and cart functionality

## Performance Questions

### How do I improve site speed?

**Answer:**
1. Enable Smart Performance Mode: `Customizer → General → Site Performance`
2. Use a caching plugin (W3 Total Cache, WP Rocket)
3. Optimize images (WebP format)
4. Use CDN (Cloudflare recommended)
5. Minimize plugins

### What is Smart Performance Mode?

**Answer:** Smart Performance Mode automatically:
- Minifies CSS/JS
- Lazy loads images
- Defers non-critical scripts
- Removes unused features
- Optimizes database queries

### Why is my site slow?

**Answer:**
Common causes:
- Shared hosting (upgrade to VPS)
- Too many plugins (audit and remove)
- Large images (optimize/compress)
- No caching (install cache plugin)
- Database bloat (optimize tables)

### How do I enable lazy loading?

**Answer:**
Already enabled by default! Configure:
`Customizer → General → Site Performance → Lazy Loading`

## Login & Registration

### How do I enable popup login?

**Answer:**
1. `Customizer → General → Login Popup`
2. Enable Login Popup: ON
3. Add menu item with URL: `#reign-login-popup`
4. Or use class: `reign-login-popup-link`

### Can I add social login?

**Answer:**
Yes! Install one of these plugins:
- Super Socializer (free)
- Nextend Social Login
- LoginRadius

Then configure in plugin settings.

### How do I customize the login page?

**Answer:**
1. `Customizer → Branded Login & Register`
2. Choose from 5 login styles
3. Customize colors, logo, background
4. Add custom CSS if needed

### Can I redirect after login?

**Answer:**
Yes! Add to functions.php:
```php
add_filter('login_redirect', function($redirect, $request, $user) {
    return home_url('/dashboard/');
}, 10, 3);
```

## Mobile & Responsive

### Is Reign mobile responsive?

**Answer:** Yes! Reign is 100% mobile responsive with:
- Mobile-specific menu
- Touch-optimized elements
- Responsive typography
- Mobile-first approach

### How do I configure mobile menu?

**Answer:**
`Customizer → Header → Mobile Header`:
- Menu style (hamburger/text)
- Position (left/right)
- Breakpoint settings
- Mobile logo option

### Can I hide elements on mobile?

**Answer:**
Yes! Use responsive visibility classes:
```css
.hide-mobile - Hidden on mobile
.hide-tablet - Hidden on tablet
.hide-desktop - Hidden on desktop
```

## Third-Party Compatibility

### What page builders work with Reign?

**Answer:**
Fully compatible with:
- Elementor (recommended)
- Gutenberg blocks
- Beaver Builder
- Visual Composer
- Divi Builder

### Does Reign work with bbPress?

**Answer:** Yes! Full bbPress compatibility with:
- Custom forum layouts
- Styled topic pages
- User integration
- Widget support

### Can I use LearnDash?

**Answer:**
Yes! Reign supports:
- LearnDash
- LifterLMS
- LearnPress
- TutorLMS
- Sensei LMS

### What SEO plugins are compatible?

**Answer:**
All major SEO plugins:
- Yoast SEO
- RankMath
- All in One SEO
- SEOPress

## Updates & Support

### How do I update Reign Theme?

**Answer:**
Two methods:
1. **Automatic:** With active license, update via WordPress dashboard
2. **Manual:** Download from WBcom account, upload via FTP

### Will updates break my customization?

**Answer:**
No, if you use:
- Child theme for custom code
- Customizer for settings
- Custom CSS section
Never modify parent theme files directly!

### How long is support included?

**Answer:**
- 6 months included with purchase
- Extendable to 12 months
- Lifetime updates included
- Community support always free

### Where can I get help?

**Answer:**
1. [Documentation](https://docs.wbcomdesigns.com/reign/)
2. [Support tickets](https://wbcomdesigns.com/support/)
3. [Community forum](https://wbcomdesigns.com/community/)
4. [Video tutorials](https://youtube.com/wbcomdesigns)

## Troubleshooting

### Why is Customizer not loading?

**Answer:**
Solutions:
1. Increase PHP memory limit to 256MB
2. Disable all plugins except required
3. Clear browser cache
4. Check JavaScript console for errors

### Images not displaying?

**Answer:**
Check:
- File permissions (644 for files, 755 for folders)
- .htaccess file not blocking images
- Image URLs correct (http vs https)
- CDN configuration

### 404 errors on pages?

**Answer:**
Solution:
1. `Settings → Permalinks`
2. Choose "Post name"
3. Save (even without changes)
4. Clear cache

### White screen of death?

**Answer:**
1. Enable debug mode in wp-config.php
2. Check error logs
3. Increase memory limit
4. Disable plugins via FTP
5. Switch to default theme

## Advanced Questions

### Can I create custom post types?

**Answer:**
Yes! Reign styles all custom post types automatically. Use:
- Custom Post Type UI plugin
- Code in functions.php
- Toolset Types

### How do I add custom code?

**Answer:**
Best practices:
1. **PHP:** Child theme functions.php
2. **CSS:** Customizer → Additional CSS
3. **JS:** Child theme or Code Snippets plugin
4. **Header/Footer:** Customizer → General → Custom Code

### Can I translate Reign?

**Answer:**
Yes! Reign is translation-ready:
- Includes .pot file
- WPML compatible
- Polylang compatible
- Loco Translate compatible

### How do I create a child theme?

**Answer:**
1. Use included child theme OR
2. Create manually:
```
reign-child/
├── style.css (with header)
├── functions.php
└── screenshot.png
```

### Can I use Reign for client sites?

**Answer:**
Yes! GPL license allows:
- Unlimited client sites
- Commercial projects
- Reselling as part of project
- No additional fees

## Migration Questions

### How do I migrate from another theme?

**Answer:**
1. Backup your site
2. Install Reign on staging
3. Import demo close to your design
4. Recreate menus and widgets
5. Test thoroughly
6. Go live

### Will I lose my content?

**Answer:**
No! Content remains unchanged:
- Posts/pages stay same
- Users preserved
- Media library intact
Only design changes

### Can I import from BuddyBoss theme?

**Answer:**
Yes, but requires:
1. Export BuddyBoss settings
2. Map to Reign options
3. Recreate custom templates
4. Test member/group pages

## Additional Help

### Do you offer customization services?

**Answer:**
Yes! WBcom Designs offers:
- Custom development
- Theme setup
- Migration services
- Custom addons
Contact sales for quotes.

### Is there a money-back guarantee?

**Answer:**
Due to digital nature, no refunds. However:
- Extensive demos to preview
- 6 months support included
- Active community help

### Can I request new features?

**Answer:**
Yes! Submit feature requests:
- Support tickets
- Community forum
- GitHub issues
We regularly add requested features!

---

*Still have questions? Contact [support](https://wbcomdesigns.com/support/) or visit our [community forum](https://wbcomdesigns.com/community/).*