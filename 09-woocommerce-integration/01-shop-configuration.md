# WooCommerce Shop Configuration

## Overview

Reign theme provides deep WooCommerce integration with custom layouts, styling options, and enhanced features for building professional online stores.

## Initial Setup

### Installing WooCommerce

1. Go to Plugins → Add New
2. Search for "WooCommerce"
3. Install and Activate
4. Run WooCommerce Setup Wizard
5. Configure basic settings

### Theme Compatibility

Reign automatically detects WooCommerce and:
- Loads WooCommerce styles
- Enables shop layouts
- Adds cart/account to header
- Activates product widgets

## Shop Page Layout

### Accessing Shop Settings

**Location:** Appearance → Customize → WooCommerce → Shop Page

### Product Grid Options

#### Columns Layout
```
Desktop Columns: 3 (default) / 4 / 5 / 6
Tablet Columns: 2 / 3
Mobile Columns: 1 / 2
```

#### Products Per Page
```
Default: 12
Options: 9, 12, 15, 18, 24, 30
Custom: Set any number
```

### Shop Sidebar

**Sidebar Position:**
- No Sidebar (full width)
- Left Sidebar
- Right Sidebar (default)

**Shop Widgets:**
- Product Categories
- Price Filter
- Product Search
- Filter by Attributes
- Recently Viewed

## Product Display Settings

### Product Card Layout

**Card Elements:**
```
✓ Product Image
✓ Product Title
✓ Price
✓ Rating
✓ Add to Cart Button
□ Quick View
□ Wishlist Button
□ Compare Button
```

### Image Settings

**Image Hover Effects:**
1. **None** - Static image
2. **Zoom** - Zoom on hover
3. **Flip** - Show second image
4. **Fade** - Fade to second image

**Image Aspect Ratio:**
```
Square (1:1)
Portrait (3:4)
Landscape (4:3)
Custom Ratio
```

## Single Product Page

### Product Layout Options

**Location:** Customize → WooCommerce → Single Product

**Layouts Available:**
1. **Default** - Standard WooCommerce
2. **Wide** - Full-width images
3. **Sticky Info** - Sticky product info
4. **Vertical Gallery** - Vertical thumbnails

### Product Gallery

**Gallery Settings:**
```
Gallery Position: Left / Right / Bottom
Thumbnail Columns: 4 / 5 / 6
Enable Zoom: Yes / No
Enable Lightbox: Yes / No
Enable Slider: Yes / No
```

### Product Information Tabs

**Default Tabs:**
- Description
- Additional Information
- Reviews

**Custom Tabs:**
```php
add_filter('woocommerce_product_tabs', function($tabs) {
    $tabs['custom_tab'] = array(
        'title' => 'Custom Info',
        'priority' => 40,
        'callback' => 'custom_tab_content'
    );
    return $tabs;
});
```

## Cart Page Customization

### Cart Layout

**Options:**
- Standard Layout
- Two Column Layout
- Minimalist Layout

### Cart Features

```
✓ Update Cart Button
✓ Continue Shopping Button
✓ Clear Cart Option
✓ Coupon Field
✓ Shipping Calculator
```

### Mini Cart (Header)

**Mini Cart Settings:**
```
Display: Icon / Icon + Count / Icon + Total
Position: Header Right
Style: Dropdown / Slide Panel
Show on: Hover / Click
```

## Checkout Configuration

### Checkout Layout

**Layout Options:**
1. **One Column** - Linear flow
2. **Two Column** - Form left, order right
3. **Accordion** - Step by step
4. **Multi-Step** - Progress bar

### Checkout Fields

**Field Management:**
```
Billing Fields: Standard + Custom
Shipping Fields: Optional
Order Notes: Enable/Disable
Terms Checkbox: Required
```

## My Account Page

### Account Dashboard

**Sections:**
- Dashboard Overview
- Orders History
- Downloads
- Addresses
- Account Details
- Logout

### Custom Endpoints

Add custom account pages:
```php
function reign_account_menu_items($items) {
    $items['custom-endpoint'] = 'Custom Section';
    return $items;
}
add_filter('woocommerce_account_menu_items', 'reign_account_menu_items');
```

## Product Categories

### Category Display

**Category Layout:**
```
Grid View: 3/4 columns
List View: With descriptions
Masonry: Variable heights
```

### Category Image

**Image Settings:**
- Show category image
- Image position: Top/Left
- Image size: Thumbnail/Full

## Multi-Vendor Support

### Dokan Integration

**Features:**
- Vendor dashboard
- Vendor stores
- Commission management
- Product management

### WC Vendors

**Features:**
- Vendor registration
- Store pages
- Vendor widgets
- Commission settings

### WCFM Marketplace

**Features:**
- Frontend manager
- Analytics dashboard
- Membership levels
- Store SEO

## Payment Methods

### Supported Gateways

**Default:**
- Direct Bank Transfer
- Check Payments
- Cash on Delivery
- PayPal Standard

**Additional:**
- Stripe
- Square
- Amazon Pay
- Google Pay
- Apple Pay

## Shipping Configuration

### Shipping Zones

**Setup:**
1. WooCommerce → Settings → Shipping
2. Add shipping zones
3. Configure methods
4. Set rates

### Shipping Methods

**Available Methods:**
- Flat Rate
- Free Shipping
- Local Pickup
- Table Rate (plugin)

## Product Filters

### Ajax Filters

**Filter Types:**
- Price Range
- Attributes
- Categories
- Tags
- Ratings
- Availability

### Filter Position

**Layout Options:**
- Sidebar (default)
- Above products
- Off-canvas panel
- Horizontal bar

## Quick View Feature

### Enable Quick View

**Settings:**
```
Enable Quick View: Yes
Trigger: Button/Icon
Modal Size: Medium/Large
Content: Gallery + Info
```

### Quick View Content

**Include:**
- Product Images
- Title & Price
- Short Description
- Add to Cart
- Product Meta

## Wishlist Integration

### Wishlist Features

**Options:**
- Guest Wishlist
- Multiple Lists
- Share Lists
- Email Notifications

### Wishlist Display

**Locations:**
- Product Cards
- Single Product
- Header Icon
- Account Page

## Performance Optimization

### Speed Improvements

1. **Lazy Load** - Product images
2. **Ajax Cart** - No page reload
3. **Cache** - Product queries
4. **CDN** - Image delivery
5. **Minify** - CSS/JS files

### Database Optimization

- Regular cleanup
- Index optimization
- Transient management
- Session handling

## SEO for Products

### Product SEO

**Elements:**
- SEO-friendly URLs
- Rich snippets
- Schema markup
- Meta descriptions
- Alt tags

### Category SEO

- Category descriptions
- Breadcrumbs
- Canonical URLs
- XML sitemap

## Troubleshooting

### Common Issues

#### Products Not Showing
- Check shop page setting
- Verify product visibility
- Clear cache
- Check permalinks

#### Cart Not Updating
- Check Ajax settings
- Verify JavaScript
- Test without plugins
- Clear browser cache

#### Checkout Errors
- Verify payment gateway
- Check SSL certificate
- Test form validation
- Review error logs

## Best Practices

1. **Product Images** - Consistent sizes, optimized
2. **Descriptions** - Clear, SEO-friendly
3. **Categories** - Logical structure
4. **Reviews** - Enable and moderate
5. **Mobile** - Test thoroughly
6. **Performance** - Monitor speed
7. **Security** - SSL, updates
8. **Backups** - Regular backups