# Reign WC Vendors Addon - Configuration Guide (Complete)

## Overview

The Reign WC Vendors Addon v2.4.1 provides extensive configuration options for marketplace management, BuddyPress integration, Google Maps location services, and advanced vendor customization. This guide covers all available settings and customization options.

## Vendor Display Configuration

### Shortcode Configuration

#### [reign-wcvendors-sellers] Settings

**Basic Configuration:**
```
[reign-wcvendors-sellers per_page="12" orderby="top_rated" show_search="yes"]
```

**Complete Parameter Options:**

| Parameter | Default | Options | Description |
|-----------|---------|---------|-------------|
| `per_page` | 10 | Any number | Vendors displayed per page |
| `orderby` | most_recent | most_recent, total_orders, random, top_rated, most_reviewed | Vendor sorting method |
| `show_search` | yes | yes, no | Enable search functionality |
| `show_location` | no | yes, no | Enable location-based filtering |
| `location_radius` | 50 | Any number (km) | Search radius for location filtering |
| `show_address` | no | yes, no | Display vendor addresses |
| `show_phone` | no | yes, no | Display vendor phone numbers |
| `show_rating` | yes | yes, no | Display vendor ratings |
| `template` | default | default, compact, detailed | Display template style |

### Store Header Layout Configuration

#### Layout Options (4 Available)

1. **Layout One** - Basic vendor header with essential information
2. **Layout Two** - Enhanced header with cover images and banners
3. **Layout Three** - Professional layout with verification badges
4. **Layout Four** - Advanced layout with social integration

**Configuration Location:**
```
Appearance → Customize → Reign WC Vendors → Single Store Settings
```

## BuddyPress Integration Configuration

### Store Profile Integration

**Enable BuddyPress Features:**
```
Reign Settings → WC Vendors → BuddyPress Integration
```

**Profile Integration Settings:**
- Store tab in member profiles
- Vendor information display
- Store product showcases
- Social messaging integration

### Favorite Products System Configuration

**Enable Favorites System:**
- Automatic heart icons on product pages
- AJAX add/remove functionality
- Favorites tab in user profiles
- Compatible with BuddyPress, BuddyBoss, and PeepSo

**Configuration Options:**
```
Reign Settings → WC Vendors → Favorite Products
Enable: Yes
Display Style: Heart Icon
Profile Integration: Yes
```

### Activity Stream Integration

**Activity Types Configuration:**
- Product creation activities
- Order placement activities
- Product review activities
- Social vendor interactions

**Settings Location:**
```
Reign Settings → WC Vendors → Activity Integration
```

## Google Maps Integration Configuration

### API Configuration

**Required Google APIs:**
1. Maps JavaScript API
2. Geocoding API
3. Places API (optional for enhanced features)

**Setup Location:**
```
Reign Settings → WC Vendors → Google Maps
API Key: [Your Google Maps API Key]
Enable Location Search: Yes
Default Radius: 50km
```

### Location-Based Features

**Vendor Location Services:**
- Distance-based vendor search
- Store location display on vendor pages
- Interactive maps for vendor addresses
- Radius-based filtering in vendor listings

**Configuration Example:**
```
[reign-wcvendors-sellers show_location="yes" location_radius="25" show_address="yes"]
```

## Widget System Configuration

### Available Widgets (3 Types)

#### 1. REIGN Vendor Profile Widget

**Configuration Options:**
- Store information display
- Contact details and hours
- Total sales and registration date
- Store address and phone

**Widget Settings:**
```
Appearance → Widgets → REIGN Vendor Profile Widget
Title: Store Information
Show Store Icon: Yes
Show Contact Info: Yes
Show Opening Hours: Yes
Show Registration Date: Yes
```

#### 2. REIGN WC Vendors List Widget

**Display Settings:**
- Number of vendors to display
- Store icons and "Visit Store" links
- Sorting options
- Layout style (grid/list)

**Configuration:**
```
Number of Vendors: 5
Order By: Top Rated
Show Store Icons: Yes
Show Visit Store Button: Yes
Template: Compact
```

#### 3. REIGN Shop Owner Widget

**Profile Elements:**
- Owner profile image and details
- Vendor messaging integration
- Registration and contact info
- Social media links

## Advanced Template Configuration

### Template Override System

**Template Files Available for Override:**
- `store-header.php` - Store header layouts
- `vendor-list.php` - Vendor listing display
- `vendor-sold-by.php` - Vendor information display
- `single-store.php` - Individual store pages

**Override Location:**
```
/wp-content/themes/reign-child/wc-vendors/templates/
```

### Customizer Integration

**Customizer Panels (3 Main Sections):**

#### 1. Vendors List Settings
```
Appearance → Customize → Reign WC Vendors → Vendors List
```
- Vendor rating display toggle
- Contact information visibility
- Search functionality settings
- Pagination style options

#### 2. Single Store Settings
```
Appearance → Customize → Reign WC Vendors → Single Store
```
- Store header layout selection
- Banner and cover image settings
- Vendor information display options
- Contact form configuration

#### 3. Single Product Settings
```
Appearance → Customize → Reign WC Vendors → Single Product
```
- Vendor information on product pages
- Product header integration
- Social sharing options
- Review system integration

## Vendor Verification System Configuration

### Trust Indicators Setup

**Verification Badge System:**
- Manual verification by admin
- Automatic verification criteria
- Visual verification badges
- Trust indicator display

**Configuration Options:**
```
WC Vendors → Settings → Vendors → Verification
Enable Verification: Yes
Verification Criteria: Manual Admin Approval
Badge Display: On Store Cards and Headers
Badge Style: Professional
```

### Verification Requirements

**Manual Verification Process:**
1. Document verification
2. Identity confirmation
3. Business license check
4. Payment method verification
5. Store quality review

## Performance Optimization Configuration

### Caching Settings

**Optimization Options:**
```
Reign Settings → WC Vendors → Performance
Enable Vendor Caching: Yes
Cache Duration: 1 hour
Lazy Load Images: Yes
Minify CSS/JS: Yes
```

### Mobile Optimization

**Responsive Configuration:**
- Mobile-first design approach
- Touch-friendly interface elements
- Optimized loading for mobile devices
- Progressive image loading

**Settings:**
```
Mobile Optimization: Enabled
Touch Interface: Enhanced
Image Loading: Progressive
Responsive Breakpoints: Auto
```

## Search and Filtering Configuration

### Advanced Search Settings

**AJAX Search Configuration:**
```
Reign Settings → WC Vendors → Search
Enable AJAX Search: Yes
Search Placeholder: "Search vendors..."
Enable Smart Suggestions: Yes
Search Categories: Yes
Search by Location: Yes
```

### Filter Options Configuration

**Available Filters:**
- Category filtering
- Location-based filtering
- Rating-based filtering
- Verification status filtering
- Product count filtering

**Filter Display Options:**
```
Show Category Filter: Yes
Show Location Filter: Yes (if Google Maps enabled)
Show Rating Filter: Yes
Show Verification Filter: Yes
Filter Style: Dropdown
Enable Multi-Select: Yes
```

## Commission Configuration

### Understanding Commissions First

**What are commissions?**
- The percentage you keep from each sale
- Example: 20% commission = you keep $20 from a $100 sale
- Vendor gets the rest (80% = $80)

### Step 1: Set Your Commission Rate

**Where to go:**
```
WP Admin → WC Vendors → Settings → Commission
```

**Your options explained:**

| Commission Type | How It Works | Best For |
|----------------|--------------|----------|
| **Percentage** | Take a % of each sale | Most marketplaces (recommended) |
| **Fixed Amount** | Take same $ amount per sale | Low-price items |
| **Percentage + Fixed** | Both % and $ fee | Cover transaction costs |

**Recommended settings:**
```yaml
Commission Type: Percentage
Default Rate: 20% (you keep 20%)
Vendor Gets: 80%
```

### Step 2: Advanced Commission Rules

**Set different rates for:**

1. **By Product Category**
   - Electronics: 15% (lower margin)
   - Clothing: 25% (higher margin)
   - Digital: 30% (no shipping)

2. **By Vendor Level**
   - New vendors: 25%
   - Established: 20%
   - Premium: 15%

3. **By Sales Volume**
   - Under $1000/month: 25%
   - $1000-5000: 20%
   - Over $5000: 15%

**How to set category rates:**
1. Go to **Products** → **Categories**
2. Edit a category
3. Find "Commission Rate" field
4. Enter percentage (without % sign)
5. **Update**

---

## Part 2: Payment Configuration

### Step 1: Choose Payment Schedule

**Where to go:**
```
WC Vendors → Settings → Payments
```

**Payment schedule options:**

| Schedule | Pros | Cons | Best For |
|----------|------|------|----------|
| **Instant** | Vendors happy | No dispute time | Not recommended |
| **Daily** | Fast payments | More work | Digital products |
| **Weekly** | Good balance | Standard choice | Most marketplaces |
| **Biweekly** | Less admin work | Vendors wait longer | Established sites |
| **Monthly** | Minimal admin | Vendors may complain | B2B markets |
| **Manual** | Full control | Time consuming | Starting out |

**Recommended starter setting:**
```yaml
Payment Schedule: Weekly
Payment Day: Monday
Minimum Payout: $50
Hold Period: 7 days
```

### Step 2: Payment Methods Setup

**Available payment methods:**

1. **PayPal Adaptive Payments** (Recommended)
   - Automatic payments
   - Instant transfers
   - 2.9% + $0.30 per transaction
   
   **Setup:**
   ```
   API Username: [from PayPal]
   API Password: [from PayPal]
   API Signature: [from PayPal]
   Application ID: [from PayPal]
   ```

2. **Stripe Connect**
   - Professional option
   - Better for US/EU
   - 2.9% + $0.30 per transaction
   
3. **Manual Payments**
   - Bank transfer
   - Check
   - Cash
   - You handle everything

### Step 3: Payment Settings

**Configure these important settings:**

```yaml
Minimum Payout Amount: $50
  Why: Reduces small transaction fees

Maximum Payout Amount: $10,000
  Why: Fraud protection

Hold Period: 7 days
  Why: Time to handle disputes

Show Payment History: Yes
  Why: Transparency for vendors
```

---

## Part 3: Vendor Capabilities

### What Vendors Can Do

**Where to go:**
```
WC Vendors → Settings → Capabilities
```

### Essential Permissions

**Products Section:**

| Permission | Enable? | Why |
|------------|---------|-----|
| Submit products | ✅ Yes | Core feature |
| Edit products | ✅ Yes | Fix mistakes |
| Delete products | ⚠️ Maybe | Risky |
| Publish instantly | ❌ No | Review first |
| Manage inventory | ✅ Yes | Stock control |
| Set sale prices | ✅ Yes | Run promotions |

**Orders Section:**

| Permission | Enable? | Why |
|------------|---------|-----|
| View orders | ✅ Yes | See their sales |
| Export orders | ✅ Yes | Their records |
| Update order status | ⚠️ Maybe | Depends on trust |
| View customer details | ⚠️ Maybe | Privacy concern |
| Add order notes | ✅ Yes | Communication |

**Coupons Section:**

| Permission | Enable? | Why |
|------------|---------|-----|
| Create coupons | ✅ Yes | Marketing tool |
| Set maximum discount | ✅ Yes | Protect margins |
| Free shipping coupons | ⚠️ Maybe | Affects profits |

**Reports Section:**

| Permission | Enable? | Why |
|------------|---------|-----|
| View own sales | ✅ Yes | Track performance |
| View commission | ✅ Yes | Transparency |
| Export reports | ✅ Yes | Tax purposes |
| View other vendors | ❌ No | Competition |

---

## Part 4: Product Management Settings

### Product Approval Workflow

**Where to go:**
```
WC Vendors → Settings → Products
```

**Approval options:**

| Setting | What It Means | Recommended |
|---------|---------------|-------------|
| **Auto approve** | Products go live instantly | No - quality control |
| **Admin approval** | You review everything | Yes - for new sites |
| **Trusted vendor** | Some auto, some manual | Yes - for established |

**Recommended workflow:**
```yaml
New Vendors: Require approval for first 10 products
Established: Auto-approve after 30 days
Premium: Always auto-approve
Edits: Always require approval
```

### Product Limits

**Set reasonable limits:**

```yaml
Products per vendor:
  Starter: 50 products
  Standard: 200 products
  Premium: Unlimited

Gallery images: 8 per product
Product categories: 3 maximum
Tags: 10 maximum
```

### Product Types Allowed

| Product Type | Allow? | Considerations |
|--------------|--------|----------------|
| Simple | ✅ Yes | Basic products |
| Variable | ✅ Yes | Size/color options |
| Grouped | ⚠️ Maybe | Can be confusing |
| External | ❌ No | Links elsewhere |
| Digital | ✅ Yes | Downloads |
| Virtual | ✅ Yes | Services |

---

## Part 5: Store Settings

### Vendor Store Pages

**Where to go:**
```
WC Vendors → Settings → Display
```

### Store URL Structure

**Choose your URL format:**

| Format | Example | Best For |
|--------|---------|----------|
| `/vendors/store-name/` | yoursite.com/vendors/johns-store/ | Clean URLs |
| `/store/store-name/` | yoursite.com/store/johns-store/ | Short |
| `/shop/store-name/` | yoursite.com/shop/johns-store/ | E-commerce feel |

### Store Display Options

```yaml
Store Header: Show
  - Banner image
  - Store logo  
  - Store name
  - Rating stars

Store Sidebar: Right
  - Store info widget
  - Product categories
  - Store policies
  - Contact form

Products per page: 12
Product layout: Grid
Columns: 3
```

### Store Information Fields

**What vendors can display:**

| Field | Required? | Visible? |
|-------|-----------|----------|
| Store name | ✅ Yes | Always |
| Description | ✅ Yes | Store page |
| Address | Optional | If provided |
| Phone | Optional | If provided |
| Email | ✅ Yes | Contact form |
| Social media | Optional | As icons |
| Store policies | Recommended | Tab |

---

## Part 6: Email Configuration

### Email Notifications Setup

**Where to go:**
```
WooCommerce → Settings → Emails
```

### Vendor Emails to Enable

**For vendors:**

| Email | When Sent | Enable? |
|-------|-----------|---------||
| New order | Customer orders | ✅ Yes |
| Order cancelled | Order cancelled | ✅ Yes |
| Product approved | Admin approves | ✅ Yes |
| Product rejected | Admin rejects | ✅ Yes |
| Commission paid | Payment sent | ✅ Yes |
| Store review | New review | ✅ Yes |

**For admin:**

| Email | When Sent | Enable? |
|-------|-----------|---------||
| New vendor application | Someone applies | ✅ Yes |
| New product submission | Vendor adds product | ✅ Yes |
| Withdrawal request | Vendor wants payment | ✅ Yes |
| Vendor report | Issues reported | ✅ Yes |

### Email Templates

**Customize key emails:**

1. **Welcome Email** (when approved)
   ```
   Subject: Welcome to [Marketplace Name]!
   
   Hi [Vendor Name],
   
   Your vendor account is approved!
   
   Next steps:
   1. Set up your store
   2. Add products
   3. Start selling
   
   Dashboard: [Dashboard Link]
   
   Need help? Reply to this email.
   ```

2. **First Sale Email**
   ```
   Subject: Congratulations on your first sale!
   
   Great news! You just made your first sale.
   
   Order: #[Order Number]
   Amount: $[Amount]
   Commission: $[Commission]
   
   Keep up the great work!
   ```

---

## Part 7: Tax Configuration

### Tax Responsibility

**Where to go:**
```
WC Vendors → Settings → Tax
```

**Who handles taxes?**

| Option | What It Means | Best For |
|--------|---------------|----------|
| **Marketplace** | You handle all taxes | Small, local |
| **Vendors** | They handle their taxes | Recommended |
| **Split** | Share responsibility | Complex |

**Recommended setting:**
```yaml
Tax Liability: Vendor
Give vendors tax settings: Yes
Show tax fields: Yes
Tax reports: Enable
```

---

## Part 8: Shipping Configuration

### Shipping Methods

**Where to go:**
```
WC Vendors → Settings → Shipping
```

### Who Ships Products?

| Method | How It Works | Best For |
|--------|--------------|----------|
| **Vendor ships** | Each vendor handles | Most marketplaces |
| **You ship all** | Centralized shipping | FBA model |
| **Mixed** | Depends on product | Flexible |

### Vendor Shipping Options

```yaml
Allow vendor shipping: Yes
Vendors set rates: Yes
Shipping types allowed:
  - Flat rate ✅
  - Free shipping ✅
  - Local pickup ✅
  - Table rate ✅
  
National shipping only: No (allow international)
Require tracking: Recommended
```

---

## Part 9: Registration Settings

### Vendor Application Form

**Where to go:**
```
WC Vendors → Settings → Registration
```

### Required Fields

**Essential information:**

| Field | Required? | Why |
|-------|-----------|-----|
| Store name | ✅ Yes | Identify vendor |
| Description | ✅ Yes | About their store |
| Email | ✅ Yes | Communication |
| PayPal email | ✅ Yes | Payments |
| Phone | Optional | Support |
| Address | Optional | Local laws |
| Tax ID | Depends | Legal requirement |

### Application Questions

**Add custom fields:**

1. **What will you sell?** (required)
2. **Previous experience?** (optional)
3. **Expected monthly sales?** (optional)
4. **How did you hear about us?** (optional)

### Terms & Conditions

```yaml
Require terms agreement: Yes
Terms page: Link to your terms
Privacy policy: Link to policy
Vendor agreement: Custom page
```

---

## Part 10: Advanced Settings

### SEO Settings

**Help vendors rank in Google:**

```yaml
Vendor store title: [Store Name] - [Marketplace Name]
Meta description: Vendor can customize
Store URL structure: /vendors/store-name/
Add schema markup: Yes
Sitemap inclusion: Yes
```

### Security Settings

**Protect your marketplace:**

```yaml
Require email verification: Yes
Manual vendor approval: Yes (initially)
Limit login attempts: 5
Two-factor authentication: Optional
File upload restrictions: jpg, png, pdf only
Maximum file size: 5MB
```

### Performance Settings

**Keep site fast:**

```yaml
Lazy load vendor images: Yes
Cache vendor pages: 1 hour
Minify vendor CSS: Yes
CDN for vendor images: Recommended
Limit API calls: 100 per hour
```

---

## Settings Checklist

### Before Launch Checklist

**Essential settings:**
- [ ] Commission rate set
- [ ] Payment method configured
- [ ] Email templates customized
- [ ] Terms page created
- [ ] Test vendor created
- [ ] Test purchase made
- [ ] Emails working
- [ ] Payment tested

**Security check:**
- [ ] SSL certificate active
- [ ] Strong passwords
- [ ] Backup system running
- [ ] Terms accepted requirement

**Legal compliance:**
- [ ] Privacy policy updated
- [ ] Terms include marketplace
- [ ] Tax settings correct
- [ ] Age verification (if needed)

---

## Configuration for Different Business Models

### Handmade/Crafts Marketplace

```yaml
Commission: 15-20%
Approval: Manual (quality control)
Products: Limited to 100
Photos: High quality required
Shipping: Vendor handles
Returns: 14 days
```

### Digital Products Marketplace

```yaml
Commission: 30-40%
Approval: Automated
Products: Unlimited
File types: PDF, ZIP, MP3
Shipping: None (digital)
Refunds: 30 days
```

### B2B Wholesale Marketplace

```yaml
Commission: 5-10%
Approval: Manual verification
Minimum order: $500
Pricing: Tiered/bulk
Payment terms: NET 30
Shipping: Freight
```

### Local Services Marketplace

```yaml
Commission: 20-25%
Approval: Background check
Bookings: Calendar system
Payment: After service
Reviews: Required
Location: Radius-based
```

---

## Complete Reign WC Vendors Settings

### Main Settings Location

**Access all Reign WC Vendors settings:**
```
WP Admin > Reign Settings > WC Vendors
```

### License Configuration

#### Add License

**Activate your license:**
```
Reign Settings > License > WC Vendors Addon
```

License activation required for:
- Automatic updates
- Security patches
- Premium support
- New features
- Compatibility updates

#### Upgrade License

**Available upgrades:**
- Single site → 5 sites
- 5 sites → Unlimited
- Annual → Lifetime

### BuddyPress Integration

#### Configure BuddyPress Integration

**Enable BP features:**
```
Reign Settings > WC Vendors > BuddyPress Integration
```

Features:
- Vendor tab in BP profiles
- Product listings in profile
- Store information display
- Activity stream integration
- Social vendor features

#### BP Activity on Product Creation

**Enable product activities:**
```
Reign Settings > WC Vendors > Create Product Activity
```

When enabled:
- Activity posted when vendor adds product
- Shows product image and price
- Links to product page
- Appears in activity stream

#### Product Review Activity

**Enable review activities:**
```
Reign Settings > WC Vendors > Product Review Activity
```

Features:
- Activity when customer reviews
- Shows rating stars
- Review excerpt displayed
- Links to full review

### Page Mapping

#### How to Map WC Vendors Pages

**Configure vendor pages:**
```
WC Vendors > Settings > General > Page Setup
```

Pages to map:
- **Vendor Dashboard** - Main vendor panel
- **Shop Settings** - Store configuration
- **Orders Page** - Order management
- **Vendors List** - All vendors page
- **Terms Page** - Vendor agreement

### Store Settings Management

#### How to Manage Store Settings for Vendors

**Configure what vendors can control:**
```
WC Vendors > Settings > Capabilities
```

Store settings vendors can manage:
- Store name and description
- Store banner and logo
- Social media links
- Store policies
- Vacation mode
- SEO settings

### Widget Configuration

#### Setup Reign WC Vendors Widget

**Add vendor widgets:**
```
Appearance > Widgets > WC Vendors Sidebar
```

**Available widgets:**
- **Reign: Vendor List** - Display vendors
- **Shop Owner Widget** - Store owner info
- **Vendors Profile Widget** - Vendor details
- **Seller List** - Featured sellers

#### Vendor List Widget

**Configuration options:**
- Layout style (grid/list)
- Number of vendors
- Sort order
- Show featured only
- Enable pagination

#### Shop Owner Widget

**Display options:**
- Owner avatar
- Store name
- Contact button
- Social links
- Store rating

#### Vendors Profile Widget

**Profile elements:**
- Vendor bio
- Location
- Member since
- Total products
- Average rating

### Shortcode Configuration

#### Seller List Shortcode

**Display vendor list:**
```
[wcv_vendorlist
    per_page="12"
    columns="3"
    orderby="registered"
    order="DESC"
    show_products="yes"]
```

Parameters:
- `per_page` - Vendors per page
- `columns` - Grid columns
- `orderby` - Sort field
- `order` - Sort direction
- `show_products` - Display products

### Store Layout Configuration

#### Store Listing Layout

**Configure vendor list page:**
```
Reign Settings > WC Vendors > Store Listing Layout
```

Layout options:
- **Grid View** - Card-based layout
- **List View** - Detailed information
- **Map View** - Location-based
- **Mixed View** - Combination

#### Single Store Page UI

**Customize vendor store pages:**
```
Reign Settings > WC Vendors > Single Store Page UI
```

Customization options:
- Header style
- Banner position
- Product layout
- Sidebar widgets
- Contact form
- Store tabs

### Template Overrides

#### Which Template Files are Overridden

**Templates modified by addon:**
- `dashboard.php` - Vendor dashboard
- `store-header.php` - Store header
- `vendor-list.php` - Vendor listing
- `vendor-sold-by.php` - Vendor info
- `orders.php` - Order management

**Override location:**
```
/themes/reign-child/wc-vendors/
```

### PeepSo Integration (Optional)

#### Integration with PeepSo

**If using PeepSo:**
```
PeepSo > Configuration > WC Vendors
```

Features:
- Vendor profiles in PeepSo
- Activity stream integration
- Social vendor features
- Product showcases

### Additional Features

#### Vendor Capabilities

Manage what vendors can do:
- Add/edit products
- View orders
- Manage coupons
- Upload files
- Set shipping rates
- Export data

#### Commission Reports

Available reports:
- Sales by vendor
- Commission earned
- Top selling products
- Vendor performance
- Payout history

## Quick Settings Reference

### Most Important Settings Locations

```
Commission: WC Vendors → Settings → Commission
Payments: WC Vendors → Settings → Payments  
Capabilities: WC Vendors → Settings → Capabilities
Products: WC Vendors → Settings → Products
Emails: WooCommerce → Settings → Emails
Shipping: WC Vendors → Settings → Shipping
```

### Default Recommended Settings

```yaml
Commission: 20%
Payment: Weekly via PayPal
Approval: Manual for new vendors
Minimum payout: $50
Product limit: 100 for free
Shipping: Vendor responsibility
Tax: Vendor responsibility
Returns: 14 days
```

---

## Next Steps

**Your marketplace is configured! Now:**

1. **[Customize Store Appearance →](04-store-customization.md)**
2. **[Set Up Developer Tools →](05-developer-guide.md)**
3. **[Test Everything →](07-troubleshooting.md)**

---

**Need Help?**  
📧 Email: support@wbcomdesigns.com  
📚 Full Docs: docs.wbcomdesigns.com  
💬 Community: facebook.com/groups/wbcom