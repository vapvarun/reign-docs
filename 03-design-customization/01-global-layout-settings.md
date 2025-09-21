# Global Layout Settings - Master Your Site's Structure

## Understanding Layout Impact

Your layout settings form the foundation of your site's appearance. These global settings affect every page unless specifically overridden. Think of them as the master blueprint for your site's structure.

## Accessing Layout Controls

### Primary Location
**Customizer Method:**
```
Appearance → Customize → General → Site Layout
```

### Alternative Access
**Quick Edit:**
- Right-click any page element
- Select "Customize"
- Navigate to layout section

## Core Layout Options

### 1. Site Layout Style

#### Wide Layout (Full Width)
**When to Use:**
- Modern, spacious designs
- Photo-heavy sites
- Minimal text content
- Portfolio showcases

**Settings:**
```
Layout: Wide
Container: 100% width
Content Area: 1170px (default)
Background: Full browser width
```

**Visual Impact:**
- Content stretches edge-to-edge
- Maximum screen utilization
- Contemporary appearance
- Great for hero images

#### Boxed Layout
**When to Use:**
- Traditional blog style
- Text-heavy content
- Corporate sites
- Reading-focused platforms

**Settings:**
```
Layout: Boxed
Container: 1170px centered
Margins: Auto left/right
Background: Visible outside box
Shadow: Optional box shadow
```

**Visual Impact:**
- Defined content boundaries
- Better readability
- Classic appearance
- Background patterns visible

### 2. Container Width Settings

#### Understanding Container Width

**What It Controls:**
The maximum width of your content area, not including margins or padding.

**Default Options:**
```
Narrow: 960px - Compact, focused reading
Standard: 1170px - Balanced, versatile (default)
Wide: 1400px - Spacious, modern
Custom: Your specified width
```

#### Responsive Behavior

**How Width Adapts:**
```
Desktop (>1200px): Full container width
Laptop (992-1200px): 90% of screen
Tablet (768-991px): 85% of screen
Mobile (<768px): 95% of screen
```

**Custom Width Example:**
```css
/* If you need specific width */
.reign-container {
    max-width: 1280px !important;
}
```

### 3. Sidebar Configuration

#### Sidebar Position Options

**Right Sidebar (Default)**
```
Content: Left side (70%)
Sidebar: Right side (30%)
Best for: Standard blogs, natural reading flow
```

**Left Sidebar**
```
Sidebar: Left side (30%)
Content: Right side (70%)
Best for: Navigation-heavy sites, tools/apps
```

**No Sidebar**
```
Content: Full width (100%)
Best for: Landing pages, portfolios, focused reading
```

**Both Sidebars**
```
Left Sidebar: 20%
Content: 60%
Right Sidebar: 20%
Best for: Content-rich sites, magazines
```

#### Sidebar Width Customization

**Adjusting Proportions:**
```css
/* Custom sidebar width */
.has-sidebar .content-area {
    width: 65%; /* Instead of 70% */
}
.has-sidebar .widget-area {
    width: 35%; /* Instead of 30% */
}
```

### 4. Content Spacing

#### Padding Settings

**Global Padding:**
```
Top Padding: 60px (default)
Bottom Padding: 60px (default)
Section Spacing: 40px between elements
```

**Customizing Spacing:**
```
Customizer → General → Spacing
- Site Top Padding: 0-100px
- Site Bottom Padding: 0-100px
- Content Padding: 0-60px
- Widget Spacing: 0-40px
```

#### Margin Controls

**Element Margins:**
```
Header Margin: 0 (connected to content)
Content Margin: Auto (centered)
Footer Margin: 0 (connected to bottom)
Section Margin: 30px (between sections)
```

## Page-Specific Layouts

### Override Global Settings

**Individual Page Settings:**
1. Edit any page/post
2. Look for "Page Settings" meta box
3. Choose layout override:
   - Default (use global)
   - Full Width
   - Left Sidebar
   - Right Sidebar
   - No Sidebar

### Layout by Content Type

#### Blog Posts
```
Default: Right sidebar
Archive: Grid layout
Single: With sidebar
Category: Grid without sidebar
```

#### BuddyPress Pages
```
Activity: Full width
Members: Right sidebar
Groups: Right sidebar
Profile: No sidebar
```

#### WooCommerce Pages
```
Shop: Left sidebar (filters)
Product: Right sidebar (info)
Cart: No sidebar
Checkout: No sidebar
```

#### Custom Pages
```
Landing: No sidebar
About: Full width
Contact: Right sidebar
Services: Grid layout
```

## Advanced Layout Features

### 1. Sticky Sidebar

**Enable Sticky Sidebar:**
```javascript
// Sidebar follows scroll
Customizer → General → Layout → Sticky Sidebar: ON
```

**Benefits:**
- Always visible widgets
- Better ad visibility
- Quick navigation access
- Improved user experience

**Requirements:**
- Sidebar shorter than content
- Not recommended for mobile
- May conflict with some plugins

### 2. Content Area Background

**Background Options:**
```
Color: Solid background color
Image: Pattern or photo
Gradient: Color transitions
Transparent: Show site background
```

**Setting Background:**
```
Customizer → Colors → Content Background
- Color: #ffffff (white default)
- Image: Upload pattern/texture
- Repeat: Tile, stretch, or fixed
- Position: Center, top, custom
```

### 3. Responsive Layout Controls

#### Breakpoint Settings

**Default Breakpoints:**
```css
/* Desktop */
@media (min-width: 1200px)

/* Laptop/Tablet Landscape */
@media (min-width: 992px) and (max-width: 1199px)

/* Tablet Portrait */
@media (min-width: 768px) and (max-width: 991px)

/* Mobile */
@media (max-width: 767px)
```

#### Mobile Layout Overrides

**Mobile-Specific Settings:**
```
Mobile Sidebar: Hidden by default
Mobile Container: 95% width
Mobile Padding: Reduced (20px)
Mobile Font Size: Adjusted for readability
```

**Force Mobile Layout:**
```css
/* Always show mobile layout */
@media (max-width: 991px) {
    .sidebar { display: none !important; }
    .content-area { width: 100% !important; }
}
```

## Layout Templates

### Pre-configured Layouts

#### Magazine Layout
```
Configuration:
- Boxed layout
- Both sidebars
- Grid post display
- Multiple widget areas
- Featured content sections
```

#### Business Layout
```
Configuration:
- Wide layout
- No sidebar on homepage
- Right sidebar on blog
- Full-width sections
- Call-to-action areas
```

#### Community Layout
```
Configuration:
- Wide layout
- Dynamic sidebars
- Activity-based widgets
- Member-focused areas
- Group sections
```

#### Shop Layout
```
Configuration:
- Wide layout
- Left sidebar for filters
- Grid product display
- Quick view enabled
- Mini cart visible
```

## Common Layout Combinations

### Classic Blog Setup
```
Layout: Boxed
Container: 1170px
Sidebar: Right
Background: Light gray (#f5f5f5)
Content BG: White
Use Case: Traditional blog, news site
```

### Modern Portfolio
```
Layout: Wide
Container: 1400px
Sidebar: None
Background: White
Padding: Minimal (20px)
Use Case: Creative showcase, photography
```

### E-Learning Platform
```
Layout: Wide
Container: 1200px
Sidebar: Left (course navigation)
Background: Soft blue gradient
Padding: Generous (60px)
Use Case: Online courses, tutorials
```

### Social Network
```
Layout: Wide
Container: 1170px
Sidebar: Right (activity widgets)
Background: Light theme
Padding: Standard (40px)
Use Case: Community, forums
```

## Performance Considerations

### Layout Impact on Speed

**Faster Layouts:**
- No sidebar (fewer widgets)
- Wide layout (less CSS)
- Minimal padding (less rendering)
- Single column (simpler DOM)

**Slower Layouts:**
- Both sidebars (more widgets)
- Complex backgrounds
- Multiple columns
- Heavy widget areas

### Optimization Tips

**For Best Performance:**
1. Limit sidebar widgets to 5-7
2. Use CSS backgrounds over images
3. Minimize custom spacing
4. Avoid too many layout changes
5. Test mobile layout separately

## Troubleshooting Layout Issues

### Content Overflow

**Problem:** Content extends beyond container
```css
/* Solution */
.site-content {
    overflow: hidden;
    word-wrap: break-word;
}
```

### Sidebar Dropping Below Content

**Problem:** Sidebar appears under content
**Causes:**
- Content too wide
- Float clearing issues
- Responsive breakpoint

**Solution:**
```css
/* Force sidebar position */
.content-area {
    max-width: 70%;
    float: left;
}
.widget-area {
    max-width: 30%;
    float: right;
}
```

### Uneven Spacing

**Problem:** Inconsistent gaps between elements
**Solution:**
1. Check global spacing settings
2. Look for custom CSS conflicts
3. Verify plugin styles
4. Reset to defaults and reconfigure

### Mobile Layout Breaking

**Problem:** Layout doesn't adapt on mobile
**Checks:**
1. Viewport meta tag present
2. Responsive CSS loading
3. JavaScript errors
4. Cache cleared

## Layout Best Practices

### Do's
- ✅ Test layouts on multiple devices
- ✅ Consider content type for layout choice
- ✅ Use consistent spacing throughout
- ✅ Optimize for primary user device
- ✅ Keep mobile experience priority

### Don'ts
- ❌ Use fixed widths for responsive sites
- ❌ Ignore mobile layout testing
- ❌ Overcomplicate with multiple sidebars
- ❌ Forget about print layout
- ❌ Mix layout styles inconsistently

## Custom Layout Code

### Adding Custom Layouts

**Register New Layout:**
```php
// Add to child theme functions.php
add_filter('reign_layout_options', 'custom_layout_options');
function custom_layout_options($layouts) {
    $layouts['custom-wide'] = __('Custom Wide Layout', 'reign');
    return $layouts;
}
```

**Apply Custom Layout:**
```php
// Set layout for specific pages
add_filter('reign_page_layout', 'apply_custom_layout');
function apply_custom_layout($layout) {
    if (is_page('special-page')) {
        return 'custom-wide';
    }
    return $layout;
}
```

## Quick Reference

### Layout Decision Tree

```
Is it text-heavy?
├─ Yes → Boxed layout with sidebar
└─ No → Is it visual content?
    ├─ Yes → Wide layout, no sidebar
    └─ No → Is it e-commerce?
        ├─ Yes → Wide with left sidebar
        └─ No → Standard with right sidebar
```

### Recommended Settings by Site Type

| Site Type | Layout | Container | Sidebar | Padding |
|-----------|---------|-----------|----------|----------|
| Blog | Boxed | 1170px | Right | 40px |
| Portfolio | Wide | 1400px | None | 20px |
| Shop | Wide | 1170px | Left | 30px |
| Community | Wide | 1170px | Right | 40px |
| Corporate | Boxed | 1170px | Right | 50px |
| Magazine | Boxed | 1400px | Both | 30px |

---

**Layout Configured?** Perfect! Your site structure is now optimized. Next, customize colors and typography to match your brand identity.