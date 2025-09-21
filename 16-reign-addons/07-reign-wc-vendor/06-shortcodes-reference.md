# Reign WC Vendors Addon - Shortcodes Reference

## What You'll Learn
This guide provides a complete reference for all shortcodes available in the Reign WC Vendors addon. Learn how to display vendor information anywhere on your site!

## Quick Overview  
**Usage Level:** Easy (just copy and paste!)  
**Where to use:** Pages, posts, widgets, anywhere!  
**Pro tip:** Test shortcodes on a draft page first

---

## Essential Shortcodes

### 1. Vendor List

**Display all vendors in a grid:**
```
[wcv_vendorslist]
```

**With parameters:**
```
[wcv_vendorslist 
    per_page="12" 
    columns="4" 
    orderby="registered" 
    order="DESC"
    show_products="yes"]
```

**Parameters explained:**

| Parameter | Options | Default | What It Does |
|-----------|---------|---------|---------------|
| `per_page` | Any number | 12 | Vendors per page |
| `columns` | 2, 3, 4, 6 | 3 | Grid columns |
| `orderby` | registered, name, random | registered | Sort order |
| `order` | ASC, DESC | ASC | Sort direction |
| `show_products` | yes, no | yes | Show product count |
| `pagination` | yes, no | yes | Show page numbers |

**Examples:**

```
// Show 8 newest vendors in 4 columns
[wcv_vendorslist per_page="8" columns="4" orderby="registered" order="DESC"]

// Random featured vendors without pagination
[wcv_vendorslist per_page="6" orderby="random" pagination="no"]

// Simple 2-column layout
[wcv_vendorslist columns="2"]
```

---

### 2. Vendor Dashboard

**The complete vendor control panel:**
```
[wcv_vendor_dashboard]
```

**Note:** This should only be used on the designated vendor dashboard page. It automatically shows different content based on who's logged in.

**What vendors see:**
- Product management
- Order management  
- Store settings
- Reports
- Coupons

**What non-vendors see:**
- Login prompt
- Application form link

---

### 3. Vendor Application Form

**Let people apply to become vendors:**
```
[wcv_vendor_application]
```

**Custom fields example:**
```
[wcv_vendor_application 
    show_description="yes"
    description_label="Tell us about your business"
    show_paypal="yes"
    terms_page="/vendor-terms"]
```

**Parameters:**

| Parameter | Options | Default | Purpose |
|-----------|---------|---------|----------|
| `show_description` | yes, no | yes | Business description field |
| `description_label` | Any text | "Store Description" | Field label |
| `show_paypal` | yes, no | yes | PayPal email field |
| `terms_page` | URL | /terms | Terms link |

---

### 4. Featured Vendors

**Show specific vendors:**
```
[wcv_featured_vendors vendor_ids="5,12,23"]
```

**Parameters:**

| Parameter | Options | Example | Purpose |
|-----------|---------|---------|----------|
| `vendor_ids` | Comma-separated IDs | "5,12,23" | Which vendors |
| `columns` | 2, 3, 4 | 3 | Layout columns |
| `per_page` | Number | 6 | How many to show |

**Usage examples:**

```
// Show 3 specific vendors
[wcv_featured_vendors vendor_ids="5,10,15" columns="3"]

// Featured vendors widget
[wcv_featured_vendors per_page="4" columns="2"]
```

---

## Store Display Shortcodes

### 5. Single Vendor Info

**Display one vendor's details:**
```
[wcv_vendor_info vendor_id="5"]
```

**What it shows:**
- Store name
- Logo
- Description
- Location
- Contact button

**Parameters:**

| Parameter | Required | Example | Purpose |
|-----------|----------|---------|----------|
| `vendor_id` | Yes | "5" | Which vendor |
| `show_logo` | No | "yes" | Display logo |
| `show_description` | No | "yes" | Display bio |
| `show_products` | No | "yes" | Product count |

---

### 6. Vendor Products

**Show products from specific vendor:**
```
[wcv_vendor_products vendor_id="5"]
```

**Advanced usage:**
```
[wcv_vendor_products 
    vendor_id="5"
    per_page="8"
    columns="4"
    orderby="date"
    category="electronics"]
```

**Parameters:**

| Parameter | Options | Default | Purpose |
|-----------|---------|---------|----------|
| `vendor_id` | Number | Required | Which vendor |
| `per_page` | Number | 12 | Products shown |
| `columns` | 2, 3, 4 | 3 | Grid layout |
| `orderby` | date, price, rating | date | Sort method |
| `category` | Slug | All | Filter category |

---

### 7. Top Rated Vendors

**Show best vendors by rating:**
```
[wcv_top_rated_vendors]
```

**With options:**
```
[wcv_top_rated_vendors 
    number="10"
    min_rating="4"
    show_rating="yes"]
```

**Parameters:**

| Parameter | Options | Default | Purpose |
|-----------|---------|---------|----------|
| `number` | Any number | 5 | How many vendors |
| `min_rating` | 1-5 | 3 | Minimum stars |
| `show_rating` | yes, no | yes | Display stars |
| `show_products` | yes, no | yes | Product count |

---

## Form Shortcodes

### 8. Contact Vendor Form

**Let customers message vendors:**
```
[wcv_contact_vendor vendor_id="5"]
```

**What it includes:**
- Name field
- Email field
- Subject line
- Message box
- Anti-spam

---

### 9. Vendor Search

**Search box for finding vendors:**
```
[wcv_vendor_search]
```

**With filters:**
```
[wcv_vendor_search 
    show_category="yes"
    show_location="yes"
    placeholder="Find a vendor..."]
```

**Parameters:**

| Parameter | Options | Default | Purpose |
|-----------|---------|---------|----------|
| `show_category` | yes, no | yes | Category filter |
| `show_location` | yes, no | no | Location filter |
| `placeholder` | Text | "Search vendors" | Search hint |

---

## Widget-Ready Shortcodes

### 10. Vendor Categories

**List vendor product categories:**
```
[wcv_vendor_categories]
```

**Options:**
```
[wcv_vendor_categories 
    hide_empty="yes"
    show_count="yes"
    hierarchical="yes"]
```

---

### 11. Recent Vendors

**Newest vendor stores:**
```
[wcv_recent_vendors number="5"]
```

---

### 12. Vendor Location Map

**Show vendors on a map:**
```
[wcv_vendor_map]
```

**With settings:**
```
[wcv_vendor_map 
    zoom="10"
    height="400px"
    show_list="yes"]
```

---

## Advanced Shortcodes

### 13. Vendor Store Banner

**Display store banner:**
```
[wcv_store_banner vendor_id="5"]
```

---

### 14. Vendor Reviews

**Show vendor ratings:**
```
[wcv_vendor_reviews vendor_id="5" number="10"]
```

---

### 15. Vendor Sold By

**"Sold by" label with link:**
```
[wcv_sold_by]
```

**Use in product pages to show vendor name**

---

## Conditional Shortcodes

### 16. Show If Vendor

**Display content only to vendors:**
```
[wcv_if_vendor]
    This content only shows to approved vendors!
[/wcv_if_vendor]
```

---

### 17. Show If Customer

**Display content only to non-vendors:**
```
[wcv_if_customer]
    <a href="/become-a-vendor">Become a vendor today!</a>
[/wcv_if_customer]
```

---

## Combination Examples

### Homepage Layout

```html
<!-- Hero Section -->
<h1>Shop from Amazing Vendors</h1>
[wcv_vendor_search]

<!-- Featured Vendors -->
<h2>Featured Stores</h2>
[wcv_featured_vendors vendor_ids="5,10,15" columns="3"]

<!-- New Vendors -->
<h2>New Arrivals</h2>
[wcv_recent_vendors number="6"]

<!-- Top Rated -->
<h2>Customer Favorites</h2>
[wcv_top_rated_vendors number="6" min_rating="4"]

<!-- Call to Action -->
[wcv_if_customer]
    <div class="cta">
        <h3>Start Selling Today</h3>
        <a href="/vendor-application" class="button">Become a Vendor</a>
    </div>
[/wcv_if_customer]
```

### Vendor Directory Page

```html
<h1>Our Vendors</h1>

<!-- Search Bar -->
[wcv_vendor_search show_category="yes" show_location="yes"]

<!-- Vendor Grid -->
[wcv_vendorslist per_page="12" columns="4" orderby="name"]
```

### Individual Vendor Page

```html
<!-- Store Header -->
[wcv_store_banner vendor_id="5"]
[wcv_vendor_info vendor_id="5"]

<!-- Products -->
<h2>Products</h2>
[wcv_vendor_products vendor_id="5" columns="4"]

<!-- Reviews -->
<h2>Customer Reviews</h2>
[wcv_vendor_reviews vendor_id="5" number="5"]

<!-- Contact -->
<h2>Contact This Vendor</h2>
[wcv_contact_vendor vendor_id="5"]
```

### Sidebar Widgets

```html
<!-- Widget 1: Categories -->
<h3>Shop by Category</h3>
[wcv_vendor_categories show_count="yes"]

<!-- Widget 2: Top Vendors -->
<h3>Top Rated</h3>
[wcv_top_rated_vendors number="5"]

<!-- Widget 3: New Vendors -->
<h3>New Stores</h3>
[wcv_recent_vendors number="5"]
```

---

## Styling Shortcodes

### Basic CSS Classes

**All shortcodes use these classes:**

```css
.wcv-wrapper { /* Main wrapper */ }
.wcv-vendor-card { /* Vendor cards */ }
.wcv-product-grid { /* Product grids */ }
.wcv-form { /* Forms */ }
.wcv-button { /* Buttons */ }
```

### Custom Styling Example

```css
/* Make vendor cards fancy */
.wcv-vendor-card {
    border: 2px solid #eee;
    border-radius: 10px;
    padding: 20px;
    transition: all 0.3s;
}

.wcv-vendor-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 5px 20px rgba(0,0,0,0.1);
}

/* Style the search bar */
.wcv-vendor-search {
    background: #f5f5f5;
    padding: 30px;
    border-radius: 5px;
    margin-bottom: 30px;
}

/* Featured vendor badges */
.wcv-featured-badge {
    background: gold;
    color: white;
    padding: 5px 10px;
    border-radius: 20px;
    font-size: 12px;
}
```

---

## Troubleshooting Shortcodes

### Common Issues

**"Shortcode not working"**
- Check spelling exactly
- Make sure quotes are straight ("), not curly
- Verify vendor IDs exist
- Check plugin is activated

**"Layout looks broken"**
- Clear cache
- Check theme compatibility
- Try different column numbers
- Add custom CSS if needed

**"No vendors showing"**
- Verify vendors are approved
- Check vendor products are published
- Ensure proper permissions

**"Forms not sending"**
- Configure email settings
- Check spam folder
- Verify SMTP setup

---

## Performance Tips

### Optimize Heavy Shortcodes

```
// Instead of this (loads everything):
[wcv_vendorslist per_page="100"]

// Use this (pagination):
[wcv_vendorslist per_page="12" pagination="yes"]

// Cache widget areas with many shortcodes
Use caching plugins to cache pages with multiple shortcodes
```

---

## Pro Tips

### Mix and Match

1. **Landing Pages**: Combine multiple shortcodes for rich pages
2. **Widgets**: Use simple shortcodes in sidebars
3. **Conditionals**: Show different content to vendors vs customers
4. **Testing**: Always test on staging site first

### Mobile Optimization

```
// Use fewer columns on mobile
[wcv_vendorslist columns="4"] // Shows as 2 on mobile

// Simplify forms
[wcv_vendor_search show_category="no" show_location="no"] // Cleaner on mobile
```

---

## Quick Copy Reference

### Most Used Shortcodes

```
// Vendor list
[wcv_vendorslist]

// Dashboard
[wcv_vendor_dashboard]

// Application
[wcv_vendor_application]

// Search
[wcv_vendor_search]

// Featured
[wcv_featured_vendors vendor_ids="5,10,15"]

// Products
[wcv_vendor_products vendor_id="5"]

// Contact
[wcv_contact_vendor vendor_id="5"]
```

---

**Need Help with Shortcodes?**  
📧 Email: support@wbcomdesigns.com  
📚 More examples: docs.wbcomdesigns.com  
💬 Forum: wbcomdesigns.com/support