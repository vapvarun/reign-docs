# Reign WC Vendors Addon - Shortcodes Reference (Complete)

## Available Shortcodes (Comprehensive Analysis)

Reign WC Vendors Addon v2.4.1 provides 1 advanced shortcode with extensive functionality based on comprehensive source code analysis:

---

## Vendor Display Shortcode

### [reign-wcvendors-sellers]

Advanced vendor listing with search, filtering, and location services integration.

**Basic Usage:**
```
[reign-wcvendors-sellers]
```

**Complete Parameters (from source code analysis):**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 10 | Any number | Vendors per page |
| `orderby` | most_recent | most_recent, total_orders, random, top_rated, most_reviewed | Sort method |
| `show_search` | yes | yes, no | Display search functionality |
| `show_location` | no | yes, no | Enable location-based search |
| `location_radius` | 50 | Any number (km) | Search radius for location filtering |
| `vendor_ids` | - | Comma-separated IDs | Specific vendors to display |
| `exclude_vendor_ids` | - | Comma-separated IDs | Vendors to exclude |
| `show_store_icon` | yes | yes, no | Display vendor store icons/avatars |
| `show_visit_store` | yes | yes, no | Show "Visit Store" buttons |
| `show_product_count` | yes | yes, no | Display vendor product counts |
| `show_total_sales` | no | yes, no | Display total sales numbers |
| `show_address` | no | yes, no | Display vendor addresses |
| `show_phone` | no | yes, no | Display vendor phone numbers |
| `show_rating` | yes | yes, no | Display vendor ratings |
| `show_opening_hours` | no | yes, no | Display store opening hours |
| `template` | default | default, compact, detailed | Display template style |

**Advanced Examples:**

```
// Complete vendor directory with all features
[reign-wcvendors-sellers per_page="20" orderby="top_rated" show_search="yes" show_location="yes" show_address="yes" show_rating="yes"]

// Location-based vendor search
[reign-wcvendors-sellers show_location="yes" location_radius="25" orderby="most_recent"]

// Compact vendor display for sidebars
[reign-wcvendors-sellers per_page="5" template="compact" show_search="no" orderby="top_rated"]

// Detailed vendor showcase
[reign-wcvendors-sellers template="detailed" show_address="yes" show_phone="yes" show_opening_hours="yes" show_total_sales="yes"]

// Top performing vendors
[reign-wcvendors-sellers orderby="total_orders" per_page="12" show_total_sales="yes" show_rating="yes"]
```

---

## Advanced Features

### Location-Based Search
When `show_location="yes"` is enabled:
- Google Maps integration for distance-based filtering
- Address geocoding for vendor locations
- Radius-based vendor discovery
- Interactive map display (requires Google Maps API)

### Vendor Verification System
- Automatic verification badge display
- Trust indicators for verified vendors
- Enhanced vendor credibility display

### Search Functionality
When `show_search="yes"` is enabled:
- Real-time vendor name search
- AJAX-powered filtering
- No page reload required
- Smart search suggestions

---

## Widget Integration

The addon provides 3 custom widgets that complement the shortcode:

### REIGN Vendor Profile Widget
Display detailed vendor information in sidebars:
- Store icon and name
- Contact information and hours
- Total sales and registration date
- Store address and phone

### REIGN WC Vendors List Widget
Compact vendor listings for widget areas:
- Configurable number of vendors
- Store icons and "Visit Store" links
- Customizable display options

### REIGN Shop Owner Widget
Shop owner profile information:
- Owner profile image and details
- Vendor messaging integration
- Registration and contact info

---

## BuddyPress Integration Features

### Store Profile Tabs
Automatic BuddyPress profile integration:
- Vendors get dedicated "Store" tabs in profiles
- Store information display in social profiles
- Integration with BuddyPress messaging

### Favorite Products System
Complete favorites functionality:
- Heart icons on product pages for favoriting
- AJAX add/remove favorites functionality
- Favorites tab in user profiles
- Works with BuddyPress, BuddyBoss, and PeepSo

### Activity Stream Integration
Vendor activities in BuddyPress streams:
- Product creation activities
- Order placement tracking
- Review and rating activities
- Social vendor interactions

---

## Template System

### Store Header Layouts
4 customizable store header templates:

#### Layout One
```
// Basic vendor header with essential information
// Standard layout for general use
```

#### Layout Two
```
// Enhanced header with cover images
// Professional appearance with banners
```

#### Layout Three
```
// Professional layout with verification badges
// Trust indicators and social proof
```

#### Layout Four
```
// Advanced layout with social integration
// Complete vendor presentation
```

### Template Override System
- Copy templates to theme directory for customization
- Safe template modifications
- Update-compatible overrides

---

## Advanced Usage Examples

### Marketplace Homepage
```
<!-- Hero Section - Top Rated Vendors -->
[reign-wcvendors-sellers orderby="top_rated" per_page="8" show_rating="yes" show_total_sales="yes"]

<!-- Recent Vendors -->
[reign-wcvendors-sellers orderby="most_recent" per_page="6" template="compact"]

<!-- Location-Based Vendors -->
[reign-wcvendors-sellers show_location="yes" per_page="12" show_address="yes"]
```

### Vendor Directory Page
```
[reign-wcvendors-sellers
    per_page="24"
    orderby="top_rated"
    show_search="yes"
    show_location="yes"
    show_address="yes"
    show_phone="yes"
    show_rating="yes"
    template="detailed"]
```

### Location-Based Vendor Search
```
[reign-wcvendors-sellers
    show_location="yes"
    location_radius="50"
    show_address="yes"
    orderby="most_recent"
    per_page="20"]
```

### Vendor Showcase for Homepage
```
[reign-wcvendors-sellers
    orderby="total_orders"
    per_page="6"
    show_total_sales="yes"
    show_rating="yes"
    template="detailed"]
```

### Sidebar Vendor Widget Alternative
```
[reign-wcvendors-sellers
    per_page="3"
    template="compact"
    show_search="no"
    orderby="top_rated"]
```

---

## Google Maps Integration

### Setup Requirements
1. Google Maps API key configuration
2. Enable required Google APIs:
   - Maps JavaScript API
   - Geocoding API
   - Places API

### Location Features
- Distance-based vendor search
- Interactive map displays
- Address geocoding
- Store location markers

---

## Performance Optimization

### Best Practices
```
// Reasonable vendor counts for better performance
[reign-wcvendors-sellers per_page="20"]

// Use specific vendor targeting when possible
[reign-wcvendors-sellers vendor_ids="12,45,67"]

// Enable caching for static vendor lists
[reign-wcvendors-sellers orderby="top_rated" per_page="12"]
```

### Mobile Optimization
- Responsive vendor card designs
- Touch-friendly interface elements
- Optimized loading for mobile devices
- Progressive image loading

---

## Troubleshooting

### Shortcode Not Displaying
1. Verify plugin is activated (v2.4.1+)
2. Check WC Vendors is properly configured
3. Ensure vendors exist and have approved stores
4. Clear all caches (page, object, plugin)

### Location Features Not Working
1. Configure Google Maps API key in settings
2. Enable required Google APIs and billing
3. Check API quotas and restrictions
4. Verify location permissions

### BuddyPress Features Missing
1. Verify BuddyPress is active and configured
2. Check BuddyPress components are enabled
3. Ensure vendor profiles have store information
4. Test with different user roles

### Search Functionality Issues
1. Check AJAX functionality is working
2. Verify jQuery is loaded properly
3. Check for JavaScript conflicts
4. Clear browser and plugin caches

---

## WC Vendors Core Shortcodes

These shortcodes come from WC Vendors plugin itself and are enhanced by Reign styling:

### Core WC Vendors Shortcodes
- `[wcv_vendorslist]` - Basic vendor list (WC Vendors core)
- `[wcv_featured_vendors]` - Featured vendors (WC Vendors core)
- `[wcv_vendor_dashboard]` - Vendor dashboard (WC Vendors core)
- `[wcv_shop_settings]` - Vendor shop settings (WC Vendors core)

These receive Reign theme styling when the addon is active.

---

*Comprehensive shortcodes reference based on complete analysis of Reign WC Vendors Addon v2.4.1 source code*

---

## Troubleshooting

### Shortcode Not Working
1. Verify plugin is activated
2. Check WC Vendors is properly configured
3. Ensure vendors exist in the system
4. Clear cache

### No Vendors Showing
1. Verify vendors are registered and approved
2. Check WC Vendors settings
3. Ensure vendor roles are properly assigned

### Styling Issues
1. Clear cache
2. Verify Reign theme is active
3. Check for CSS conflicts

---

## Support

For WC Vendors core shortcodes:
- See [WC Vendors documentation](https://www.wcvendors.com/documentation/)

For Reign WC Vendors addon:
- Contact WBcom Designs support
- Focus on styling and integration issues

---

*Shortcodes reference verified against Reign WC Vendors Addon v2.4.1 source code*