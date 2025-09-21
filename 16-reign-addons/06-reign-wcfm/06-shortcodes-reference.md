# Reign WCFM Addon - Shortcodes Reference

## Important Note

**The Reign WCFM Addon does NOT add any custom shortcodes.** This addon focuses on enhancing WCFM's integration with Reign theme through:
- BuddyPress profile integration
- Activity stream support
- Enhanced styling
- Template overrides

All shortcodes come from the WCFM core plugin itself.

---

## WCFM Core Plugin Shortcodes

These shortcodes are provided by WCFM Marketplace plugin and are styled/enhanced by Reign theme:

### Store Listing Shortcodes

#### [wcfm_stores]
**Display vendor store listings:**
```
[wcfm_stores]
[wcfm_stores per_page="12" has_product="yes"]
```

### Store Information Shortcodes

#### [wcfm_store_info]
**Display store information:**
```
[wcfm_store_info id="vendor_id"]
```

#### [wcfm_inquiry]
**Store inquiry form:**
```
[wcfm_inquiry]
```

#### [wcfm_follow]
**Store follow button:**
```
[wcfm_follow]
```

---

## What Reign WCFM Addon Provides

Instead of shortcodes, the Reign WCFM addon enhances WCFM through:

### 1. BuddyPress Integration
- Adds "Store" tab to user profiles
- Shows vendor products in profile
- Displays favorite products

### 2. Activity Stream Integration
- Posts activity when products are created
- Posts activity for product reviews
- Formats activities with proper links

### 3. Template Enhancements
- Custom store layout templates
- Enhanced store grid displays
- Mobile-optimized views

### 4. Styling
- Reign theme styling for all WCFM elements
- Responsive design improvements
- Color scheme integration

---

## Developer Hooks (Actual)

The Reign WCFM addon provides these filters:

```php
// Format product review activity
add_filter('reign_wcfm_format_activity_action_product_review', function($action, $activity) {
    // Customize review activity format
    return $action;
}, 10, 2);

// Format product creation activity
add_filter('reign_wcfm_format_activity_action_product_create', function($action, $activity) {
    // Customize product creation activity
    return $action;
}, 10, 2);

// Customize favorite products tab name
add_filter('reign_wcfm_favourite_product_tab_name', function($name) {
    return __('My Favorites', 'textdomain');
});

// Customize vendor store tab name
add_filter('reign_wcfm_vendor_store_tab_name', function($name) {
    return __('Vendor Shop', 'textdomain');
});
```

---

## Using WCFM with Reign Theme

### Step 1: Install Required Plugins
1. Install and activate WCFM Marketplace
2. Install and activate Reign WCFM Addon
3. Configure WCFM settings

### Step 2: Use WCFM Core Shortcodes
Place WCFM's built-in shortcodes in your pages:
- Store listing page: `[wcfm_stores]`
- Vendor dashboard: Use WCFM's default pages

### Step 3: Enable BuddyPress Integration
1. Go to Reign Settings → WCFM
2. Enable BuddyPress integration
3. Configure activity settings

---

## Common Misconceptions

❌ **Wrong:** "Reign WCFM addon provides store listing shortcodes"
✅ **Right:** WCFM core provides shortcodes; Reign addon enhances display

❌ **Wrong:** "Use [reign_wcfm_stores] to display vendors"
✅ **Right:** Use [wcfm_stores] from WCFM core plugin

❌ **Wrong:** "Reign WCFM addon is required for shortcodes"
✅ **Right:** Reign WCFM addon enhances styling and adds BuddyPress integration

---

## Support

For WCFM shortcodes documentation:
- See [WCFM official documentation](https://wclovers.com/knowledgebase/)
- WCFM shortcodes work without Reign addon
- Reign addon enhances appearance and integration

For Reign WCFM addon support:
- Contact WBcom Designs support
- Focus on BuddyPress integration issues
- Report styling/display problems