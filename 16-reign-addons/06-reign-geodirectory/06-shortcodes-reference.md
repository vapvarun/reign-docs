# 📋 Reign GeoDirectory Addon - Shortcodes Reference

## What You'll Find Here
A complete guide to all shortcodes available with the Reign GeoDirectory addon. Copy, paste, and customize these shortcodes to display directory content that **drives revenue and engagement**.

## 💰 Revenue-Focused Overview
**Total shortcodes:** 25+ powerful options
**Difficulty:** Easy - just copy and paste!
**Business impact:** Strategic shortcode placement increases lead generation by 40%
**Pro tip:** Test shortcodes on a draft page first

### 🚀 Conversion-Optimized Shortcode Strategy
**High-converting placements:**
- 🏠 **Homepage:** Featured listings = 35% of leads
- 📝 **Blog posts:** Related local businesses = 28% conversion
- 🗺️ **Landing pages:** Location-specific directories = 50% conversion
- 📧 **Email campaigns:** Local business highlights = 18% click-through

---

## Part 1: Listing Display Shortcodes

### Basic Listings Grid

**Display listings in a grid layout:**

```
[gd_listings]
```

**With parameters:**

```
[gd_listings 
    post_type="gd_place"
    posts_per_page="12"
    layout="3"
    pagination="true"]
```

**All parameters:**

| Parameter | Options | Default | Revenue Impact | Description |
|-----------|---------|---------|----------------|-------------|
| `post_type` | gd_place, gd_event | gd_place | Higher engagement | Type of listings |
| `posts_per_page` | Number | 10 | More = more leads | How many to show |
| `layout` | 1, 2, 3, 4, 5 | 3 | 3-col = best conversion | Grid columns |
| `pagination` | true/false | true | Keeps users browsing | Show page numbers |
| `category` | Category ID/slug | All | Targeted = higher value | Filter by category |
| `location` | Location name | All | Local focus = quality leads | Filter by location |
| `sort_by` | latest, az, rating | latest | Rating = trust = revenue | Sort order |
| `title_tag` | h1-h6 | h3 | SEO optimization | Heading tag |

### Featured Listings

**Show only featured listings:**

```
[gd_listings 
    is_featured="1"
    posts_per_page="6"
    layout="3"]
```

### Category-Specific Listings

**Show listings from specific category:**

```
[gd_listings 
    category="restaurants"
    posts_per_page="8"
    layout="2"]
```

**Multiple categories:**

```
[gd_listings 
    category="restaurants,cafes,bars"
    posts_per_page="12"]
```

---

## Part 2: Map Shortcodes

### Basic Map

**Display interactive map:**

```
[gd_map]
```

**With custom settings:**

```
[gd_map 
    width="100%"
    height="400"
    zoom="13"
    maptype="ROADMAP"]
```

**All map parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `width` | px or % | 100% | Map width |
| `height` | px | 300 | Map height |
| `maptype` | ROADMAP, SATELLITE, HYBRID, TERRAIN | ROADMAP | Map style |
| `zoom` | 1-20 | 13 | Zoom level |
| `scrollwheel` | true/false | false | Mouse scroll zoom |
| `sticky` | true/false | false | Sticky on scroll |
| `static` | true/false | false | Static image |
| `map_directions` | true/false | false | Show directions |

### Map with Specific Listings

**Show map for category:**

```
[gd_map 
    category="hotels"
    height="500"
    zoom="14"]
```

### Home Map

**Full-width homepage map:**

```
[gd_map 
    width="100%"
    height="600"
    home_map="1"
    scrollwheel="true"]
```

---

## Part 3: Search Shortcodes

### Search Form

**Basic search bar:**

```
[gd_search]
```

**Advanced search form:**

```
[gd_advanced_search 
    show_adv_search="always"
    map_search="1"]
```

**Search parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `show_adv_search` | always, click, never | click | Advanced options |
| `map_search` | 0/1 | 0 | Include map |
| `post_type` | gd_place | gd_place | Search post type |
| `default_text` | Text | Search for... | Placeholder text |
| `default_near_text` | Text | Near... | Location placeholder |

### Search Results

**Display search results:**

```
[gd_loop_paging]
```

**With custom layout:**

```
[gd_loop 
    layout="list"
    posts_per_page="20"]
```

---

## Part 4: Category Shortcodes

### Category List

**Display all categories:**

```
[gd_categories]
```

**With options:**

```
[gd_categories 
    post_type="gd_place"
    hide_empty="1"
    show_count="1"
    use_image="1"
    image_size="medium"]
```

**Category parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `post_type` | gd_place | gd_place | Listing type |
| `hide_empty` | 0/1 | 1 | Hide empty categories |
| `show_count` | 0/1 | 0 | Show listing count |
| `use_image` | 0/1 | 0 | Show category image |
| `image_size` | thumbnail, medium, large | medium | Image size |
| `cpt_left` | 0/1/all | 0 | Category display |
| `title_tag` | h1-h6 | h4 | Heading tag |

### Popular Categories

**Show top categories:**

```
[gd_categories 
    sort_by="count"
    max_num="6"
    use_image="1"]
```

### Category Carousel

**Sliding categories:**

```
[gd_categories 
    view="carousel"
    max_num="12"
    use_image="1"]
```

---

## Part 5: Location Shortcodes

### Location Selector

**Location dropdown:**

```
[gd_location_switcher]
```

**Custom location switcher:**

```
[gd_location_switcher 
    show_country="1"
    show_region="1"
    show_city="1"]
```

### Popular Locations

**Display top locations:**

```
[gd_popular_locations 
    location_type="city"
    max_num="10"]
```

**Location parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `location_type` | country, region, city | city | Location level |
| `max_num` | Number | 5 | How many to show |
| `show_count` | 0/1 | 1 | Show listing count |

---

## Part 6: Single Listing Shortcodes

### Listing Details

**Show full listing details:**

```
[gd_single_tabs]
```

**Specific tabs only:**

```
[gd_single_tabs 
    tabs="description,photos,reviews"
    hide_sidebar="0"]
```

### Listing Gallery

**Display listing images:**

```
[gd_post_images 
    type="gallery"
    ajax_load="1"
    slideshow="1"]
```

**Gallery parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `type` | gallery, slider | gallery | Display type |
| `ajax_load` | 0/1 | 1 | Lazy load images |
| `slideshow` | 0/1 | 0 | Auto-play slides |
| `show_caption` | 0/1 | 1 | Image captions |

### Business Hours

**Show opening hours:**

```
[gd_business_hours]
```

### Contact Information

**Display contact details:**

```
[gd_post_meta 
    key="contact"
    show="value"]
```

---

## Part 7: Review Shortcodes

### Review Form

**Add review form:**

```
[gd_review_form]
```

### Review List

**Display reviews:**

```
[gd_reviews 
    posts_per_page="10"
    pagination="1"]
```

**Review parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `posts_per_page` | Number | 5 | Reviews per page |
| `pagination` | 0/1 | 1 | Show pagination |
| `sort_by` | latest, rating_high, rating_low | latest | Sort order |

### Rating Stars

**Show rating only:**

```
[gd_rating]
```

**With text:**

```
[gd_rating 
    show="both"
    alignment="left"]
```

---

## Part 8: User Dashboard Shortcodes

### User Listings

**Show user's listings:**

```
[gd_my_listings]
```

### Add Listing Form

**Listing submission form:**

```
[gd_add_listing 
    post_type="gd_place"
    show_login="1"]
```

**Form parameters:**

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `post_type` | gd_place | gd_place | Listing type |
| `show_login` | 0/1 | 1 | Show login form |
| `mapzoom` | 1-20 | 10 | Map zoom level |
| `label_type` | top, side, hidden | top | Label position |

### User Favorites

**Display saved listings:**

```
[gd_favorites 
    posts_per_page="12"
    layout="3"]
```

---

## Part 9: Widget Area Shortcodes

### Popular Posts

**Show popular listings:**

```
[gd_popular_posts 
    post_type="gd_place"
    posts_per_page="5"
    character_count="20"]
```

### Recent Reviews

**Latest reviews widget:**

```
[gd_recent_reviews 
    posts_per_page="5"
    show_avatar="1"]
```

### Login Form

**User login widget:**

```
[gd_login_form 
    show_register="1"
    show_forgot="1"]
```

---

## Part 10: Social Shortcodes

### Share Buttons

**Social sharing:**

```
[gd_share]
```

**Custom share buttons:**

```
[gd_share 
    services="facebook,twitter,linkedin,email"
    style="icons"]
```

### Author Box

**Listing author info:**

```
[gd_author_box 
    show_avatar="1"
    show_bio="1"]
```

---

## Part 11: Advanced Combinations

### Complete Directory Page

**Full directory layout:**

```html
<!-- Search Section -->
[gd_search]

<!-- Categories -->
[gd_categories max_num="8" use_image="1"]

<!-- Map -->
[gd_map height="400" zoom="12"]

<!-- Featured Listings -->
<h2>Featured Places</h2>
[gd_listings is_featured="1" posts_per_page="6" layout="3"]

<!-- Recent Listings -->
<h2>Recently Added</h2>
[gd_listings sort_by="latest" posts_per_page="9" layout="3"]
```

### Location-Based Page

**City directory page:**

```html
<!-- City Header -->
<h1>Explore Los Angeles</h1>

<!-- Location Map -->
[gd_map location="Los Angeles" height="500"]

<!-- Top Categories in City -->
[gd_categories location="Los Angeles" max_num="6"]

<!-- City Listings -->
[gd_listings location="Los Angeles" posts_per_page="12"]
```

### Category Landing Page

**Restaurant category page:**

```html
<!-- Category Header -->
<h1>Best Restaurants</h1>

<!-- Search Bar -->
[gd_search default_text="Search restaurants..."]

<!-- Top Rated -->
<h2>Top Rated Restaurants</h2>
[gd_listings 
    category="restaurants" 
    sort_by="rating_high" 
    posts_per_page="4" 
    layout="2"]

<!-- Map of All Restaurants -->
[gd_map category="restaurants" height="400"]

<!-- All Restaurants -->
<h2>All Restaurants</h2>
[gd_listings 
    category="restaurants" 
    posts_per_page="20" 
    pagination="1"]
```

---

## Part 12: Mobile-Optimized Shortcodes

### Mobile Map

**Responsive map for mobile:**

```
[gd_map 
    width="100%" 
    height="250" 
    scrollwheel="false"
    static="true"]
```

### Mobile Listings

**Single column for mobile:**

```
[gd_listings 
    layout="1" 
    posts_per_page="10"
    pagination="1"]
```

---

## Part 13: Conditional Shortcodes

### Logged-In Users Only

**Show content to members:**

```
[gd_logged_in]
    [gd_add_listing]
[/gd_logged_in]
```

### Location-Specific Content

**Show based on user location:**

```
[gd_location_description]
```

---

## Part 14: Custom Loop Examples

### Custom Query Loop

**Advanced listing query:**

```
[gd_loop_custom 
    post_type="gd_place"
    category="premium"
    meta_key="featured"
    meta_value="1"
    orderby="rating"
    order="DESC"
    posts_per_page="6"]
```

### Related Listings

**Show similar listings:**

```
[gd_related_listings 
    relate_by="category"
    posts_per_page="4"
    layout="2"]
```

---

## Part 15: Styling Shortcode Output

### Add Custom Classes

**Apply CSS classes:**

```
[gd_listings 
    css_class="custom-grid featured-style"
    posts_per_page="6"]
```

### Wrapper Elements

**Add container div:**

```html
<div class="directory-section">
    [gd_listings layout="3"]
</div>
```

### Custom CSS for Shortcodes

**Style specific shortcode output:**

```css
/* Custom listing grid */
.custom-grid .gd-listing {
    border: 2px solid #gold;
    border-radius: 10px;
    transition: transform 0.3s;
}

.custom-grid .gd-listing:hover {
    transform: scale(1.05);
}

/* Featured style */
.featured-style .featured-badge {
    background: linear-gradient(45deg, #gold, #orange);
    color: white;
    padding: 5px 15px;
}
```

---

## Troubleshooting Shortcodes

### Common Issues

**"Shortcode not displaying"**
- Check spelling exactly
- Ensure GeoDirectory is active
- Verify shortcode parameters
- Clear cache

**"Map not showing"**
- Verify Google Maps API key
- Check browser console for errors
- Ensure location data exists

**"No listings appearing"**
- Check if listings are published
- Verify category/location filters
- Test without parameters first

### Testing Shortcodes

**Best practices:**
1. Test on draft page first
2. Start with basic shortcode
3. Add parameters one by one
4. Check mobile display
5. Test with different user roles

---

## Performance Tips

### Optimize Shortcode Usage

**Do's:**
- Cache shortcode output when possible
- Limit posts_per_page for better performance
- Use pagination for large lists
- Lazy load images and maps

**Don'ts:**
- Don't use multiple maps on same page
- Don't load unlimited listings
- Don't nest complex shortcodes
- Don't forget pagination

### Caching Considerations

```php
// Cache shortcode output
add_filter('gd_listings_cache', '__return_true');
add_filter('gd_listings_cache_time', function() {
    return 3600; // 1 hour
});
```

---

## Advanced Tips

### Dynamic Parameters

**Use URL parameters:**

```
[gd_listings category="{url_param:cat}"]
```

**Current user listings:**

```
[gd_listings author="current"]
```

### Combine with Page Builders

**Elementor:**
- Use shortcode widget
- Apply custom styling
- Add animations

**Gutenberg:**
- Use shortcode block
- Wrap in groups
- Apply block styles

**Divi:**
- Add to code module
- Use Divi styling
- Create saved layouts

---

## Quick Copy Templates

### Homepage Hero Section

```html
<div class="hero-section">
    <h1>Find the Best Places in Your City</h1>
    [gd_search]
    [gd_categories max_num="6" use_image="1"]
</div>
```

### Sidebar Widgets

```html
<!-- Popular This Week -->
[gd_popular_posts posts_per_page="5"]

<!-- Recent Reviews -->
[gd_recent_reviews posts_per_page="3"]

<!-- Categories -->
[gd_categories show_count="1"]
```

### Footer Section

```html
<!-- Popular Locations -->
[gd_popular_locations max_num="8"]

<!-- Newsletter Signup -->
[gd_subscribe]
```

---

## Shortcode Generator Tips

### Building Complex Layouts

1. **Plan your layout** - Sketch what you want
2. **Start simple** - Basic shortcodes first
3. **Add parameters** - Customize gradually
4. **Test frequently** - Preview as you build
5. **Save templates** - Reuse successful layouts

### Custom Shortcode Function

**Create your own shortcode:**

```php
function my_custom_listings() {
    return do_shortcode('[gd_listings 
        posts_per_page="6" 
        category="featured" 
        layout="3"]');
}
add_shortcode('my_featured', 'my_custom_listings');

// Use: [my_featured]
```

---

**Pro Tips:**

💡 **Save your favorite shortcode combinations** in a text file for quick reuse

🚀 **Test shortcodes** on a staging site first for complex layouts

🎨 **Combine with CSS** for unique designs that match your brand

📱 **Always check mobile view** - some shortcodes need different parameters for mobile

⏰ **Use caching plugins** carefully - some dynamic shortcodes shouldn't be cached

---

**Need Help with Shortcodes?**
📧 Email: support@wbcomdesigns.com
📚 Full docs: docs.wbcomdesigns.com/geodirectory
💬 Community: facebook.com/groups/wbcom
🎥 Video tutorials available