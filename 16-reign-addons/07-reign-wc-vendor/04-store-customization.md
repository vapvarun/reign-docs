# Reign WC Vendors Addon - Store Customization Guide

## What You'll Learn
This guide shows you how to make vendor stores look amazing! We'll customize layouts, colors, and features to match your brand perfectly. No design experience needed!

## Quick Overview
**Time needed:** 30-45 minutes  
**Difficulty:** Easy (mostly point and click!)  
**Tools needed:** Just your WordPress admin area

---

## Part 1: Store Layout Options

### Choose Your Store Design Style

**Where to go:**
```
Appearance → Customize → Reign WC Vendors → Store Layout
```

### Available Layouts Explained

| Layout Style | What It Looks Like | Best For |
|--------------|-------------------|----------|
| **Classic** | Traditional shop layout | General stores |
| **Modern** | Clean, spacious design | Fashion, tech |
| **Compact** | More products visible | Large catalogs |
| **Gallery** | Image-focused | Visual products |
| **Minimal** | Simple and fast | Services, B2B |

### Layout Components You Can Control

**Header Section:**
```yaml
Show store banner: Yes/No
Banner height: 300px (recommended)
Show store logo: Yes/No
Logo position: Left/Center/Right
Show store name: Always
Show ratings: Yes/No
Show location: Yes/No
```

**Content Area:**
```yaml
Sidebar position: Left/Right/None
Products per row: 3 or 4
Products per page: 12, 24, or 36
Show filters: Yes/No
Show sorting: Yes/No
```

---

## Part 2: Customizing Store Colors

### Brand Color Integration

**Where to set colors:**
```
Appearance → Customize → Colors → WC Vendors
```

### Color Settings Guide

| Color Element | Default | What It Affects | Tip |
|---------------|---------|-----------------|-----|
| **Primary** | Your theme color | Buttons, links | Use brand color |
| **Secondary** | Darker shade | Headers, borders | 20% darker than primary |
| **Store Header** | Light gray | Store banner overlay | Keep subtle |
| **Text on Header** | Dark gray | Readability | High contrast needed |
| **Product Cards** | White | Product backgrounds | Keep white for clean look |
| **Sale Badge** | Red | Discount labels | Red works best |
| **Rating Stars** | Gold | Review stars | Standard gold/yellow |

### Quick Color Schemes

**Professional/Corporate:**
```css
Primary: #2C3E50 (dark blue)
Secondary: #34495E (darker blue)
Accent: #3498DB (bright blue)
Sale: #E74C3C (red)
```

**Fresh/Natural:**
```css
Primary: #27AE60 (green)
Secondary: #229954 (darker green)
Accent: #52BE80 (light green)
Sale: #E67E22 (orange)
```

**Fashion/Trendy:**
```css
Primary: #8E44AD (purple)
Secondary: #7D3C98 (dark purple)
Accent: #AF7AC5 (light purple)
Sale: #E91E63 (pink)
```

---

## Part 3: Store Header Customization

### Banner Settings

**Perfect banner specifications:**
```yaml
Recommended size: 1920 x 400 pixels
File format: JPG or PNG
Max file size: 500KB
Fallback: Default pattern if no banner
```

### How Vendors Upload Banners

**Vendors do this in their dashboard:**
1. Go to **Dashboard** → **Store Settings**
2. Click **Store Banner** section
3. Click **Upload Banner**
4. Choose image (1920x400px)
5. **Save Settings**

### Store Information Display

**What to show in header:**

| Element | Show? | Why |
|---------|-------|-----|
| Store name | ✅ Always | Identity |
| Tagline | ✅ Yes | Quick description |
| Rating | After 5 reviews | Credibility |
| Location | If relevant | Local shopping |
| Verified badge | If earned | Trust |
| Social icons | Optional | Following |
| Contact button | ✅ Yes | Questions |

---

## Part 4: Product Display Settings

### Product Card Customization

**Where to configure:**
```
Appearance → Customize → Reign WC Vendors → Product Cards
```

### What to Show on Product Cards

```yaml
Product image: Always (primary)
Product title: Always
Price: Always
Sale price: When on sale
Rating: When rated
Add to cart: Always
Quick view: Optional (recommended)
Vendor name: Yes (builds trust)
Shipping info: If free shipping
Stock status: When low
```

### Product Grid Options

**Desktop display:**
- 4 columns: Best for simple products
- 3 columns: Best for detailed products
- 2 columns: Best for complex products

**Mobile display:**
- 2 columns: Small products
- 1 column: Detailed view

---

## Part 5: Store Sidebar Widgets

### Available Widgets

**Where to add widgets:**
```
Appearance → Widgets → Vendor Store Sidebar
```

### Essential Widgets to Add

**1. Store Information Widget**
```yaml
What it shows:
  - Store logo
  - Store name
  - Member since date
  - Total products
  - Ships from location
```

**2. Store Categories**
```yaml
What it shows:
  - Product categories
  - Product count per category
  - Expandable tree view
```

**3. Store Policies**
```yaml
What it shows:
  - Shipping policy
  - Return policy  
  - Payment methods
  - Processing time
```

**4. Contact Vendor**
```yaml
What it shows:
  - Contact form
  - Response time
  - Online status
```

**5. Store Reviews**
```yaml
What it shows:
  - Average rating
  - Recent reviews
  - Review breakdown
```

### Widget Order (Recommended)

1. Store Information (build trust)
2. Store Categories (navigation)
3. Best Sellers (social proof)
4. Store Policies (transparency)
5. Contact Vendor (support)
6. Recent Reviews (credibility)

---

## Part 6: Store Tabs Configuration

### Setting Up Store Tabs

**Where to configure:**
```
WC Vendors → Settings → Display → Store Tabs
```

### Available Tabs

| Tab Name | Default Content | When to Use |
|----------|----------------|-------------|
| **Products** | Product grid | Always on |
| **About** | Store story | Always recommended |
| **Policies** | Terms, shipping | Important for trust |
| **Reviews** | Customer feedback | After 5+ reviews |
| **Contact** | Inquiry form | Always helpful |

### Custom Tabs

**Add custom tabs for:**
- FAQ (frequent questions)
- Size Guide (clothing)
- Care Instructions (handmade)
- Wholesale Info (B2B)
- Certifications (organic, etc)

**How to add custom tab:**
1. Install "Custom Product Tabs" plugin
2. Go to **Products** → **Tabs**
3. Create new tab
4. Assign to vendor stores

---

## Part 7: Mobile Store Experience

### Mobile-Specific Settings

**Where to configure:**
```
Appearance → Customize → Reign WC Vendors → Mobile
```

### Mobile Optimizations

```yaml
Mobile menu style: Bottom bar
Products per row: 2
Sticky add to cart: Yes
One-tap checkout: Enable
Swipe galleries: Yes
Collapsible filters: Yes
Infinite scroll: Optional
```

### Touch-Friendly Features

**Enable these for mobile:**
- Large tap targets (44px minimum)
- Swipe between products
- Pull to refresh
- Sticky headers
- Quick view popup
- One-thumb navigation

---

## Part 8: Store Search & Filters

### Search Configuration

**Search options to enable:**
```yaml
Search in: Product titles + descriptions
Auto-suggest: After 3 characters
Search history: Save last 5
Popular searches: Show top 10
No results: Show suggestions
```

### Filter Options

**Essential filters:**

| Filter Type | Options | Priority |
|-------------|---------|----------|
| Price range | Slider or inputs | High |
| Categories | Checkboxes | High |
| Ratings | Stars (4+ stars) | Medium |
| Availability | In stock only | High |
| Shipping | Free shipping | Medium |
| Condition | New/Used | Low |

### Sort Options

**Let customers sort by:**
- Newest first
- Price: Low to high
- Price: High to low  
- Most popular
- Best rated
- Most reviewed

---

## Part 9: Store SEO Optimization

### SEO Settings for Stores

**Help stores rank in Google:**

```yaml
Store URL format: /vendors/store-name/
Title template: [Store Name] | [Product Category] | [Site Name]
Meta description: [Store Tagline] - Shop [Main Products] at [Site Name]
```

### What Vendors Should Add

**In their store settings:**
1. **Store title** (60 characters max)
2. **Meta description** (155 characters)
3. **Keywords** (5-10 relevant terms)
4. **Store tagline** (catchy phrase)

**Example:**
```
Title: Sarah's Handmade Jewelry
Tagline: Unique designs crafted with love
Description: Discover beautiful handmade jewelry including 
custom rings, necklaces, and earrings. Each piece tells a story.
Keywords: handmade jewelry, custom rings, artisan necklaces
```

---

## Part 10: Social Media Integration

### Social Features

**Where to enable:**
```
WC Vendors → Settings → Social
```

### Social Media Links

**Let vendors add:**
- Facebook page
- Instagram profile
- Twitter/X account
- Pinterest boards
- YouTube channel
- TikTok account

**Display as:**
- Icons in store header
- Widget in sidebar
- Footer links

### Social Sharing

**Enable sharing buttons for:**
- Individual products
- Store page
- Special offers

**Share platforms:**
- Facebook
- Twitter/X
- Pinterest
- WhatsApp
- Email

---

## Part 11: Special Store Features

### Store Badges

**Types of badges:**

| Badge | Criteria | Visual |
|-------|----------|--------|
| **New** | Less than 30 days | Green |
| **Featured** | Admin selected | Gold star |
| **Verified** | Confirmed identity | Blue check |
| **Top Seller** | High sales | Trophy |
| **Fast Shipper** | Quick dispatch | Lightning |

### Store Promotions

**Promotional banners:**
- Sale announcement bar
- Free shipping threshold
- Limited time offers
- New product alerts
- Holiday specials

### Store Hours Display

**For local/service vendors:**
```yaml
Show hours: Yes
Format: Mon-Fri: 9am-5pm
Timezone: Local
Holiday hours: Customizable
Closed message: "We'll be back at [time]"
```

---

## Quick Customization Recipes

### Recipe 1: Fashion Marketplace

```yaml
Layout: Gallery style
Columns: 4 products
Sidebar: None (full width)
Filters: Size, Color, Brand
Badges: New, Sale, Trending
Colors: Black and white minimal
```

### Recipe 2: Farmers Market

```yaml
Layout: Classic
Columns: 3 products
Sidebar: Left with location
Filters: Organic, Local, Season
Badges: Certified, Local, Fresh
Colors: Green and earth tones
```

### Recipe 3: Handmade Crafts

```yaml
Layout: Modern
Columns: 3 products
Sidebar: Right with artist info
Filters: Material, Color, Size
Badges: Handmade, Custom, Unique
Colors: Warm and inviting
```

### Recipe 4: B2B Wholesale

```yaml
Layout: Compact list
Columns: List view
Sidebar: Filters on left
Filters: MOQ, Price tier, Stock
Badges: Bulk, In Stock, New
Colors: Professional blue/gray
```

---

## Troubleshooting Display Issues

### Common Problems & Solutions

**"Store looks different than preview"**
- Clear all caches
- Check theme version
- Disable conflicting plugins
- Reset permalinks

**"Images not showing correctly"**
- Check image sizes (1920x400 banner)
- Regenerate thumbnails
- Check file permissions
- CDN cache refresh

**"Mobile view broken"**
- Update theme
- Check responsive settings
- Test in real device
- Clear mobile cache

**"Widgets not appearing"**
- Check widget areas
- Verify sidebar is enabled
- Check user permissions
- Clear widget cache

---

## Best Practices

### Do's ✅
- Keep design consistent
- Use high-quality images
- Make navigation simple
- Show trust signals
- Optimize for speed
- Test on mobile

### Don'ts ❌
- Don't overcrowd pages
- Don't use too many fonts
- Don't hide important info
- Don't forget mobile users
- Don't skip image optimization
- Don't ignore loading speed

---

## Performance Tips

### Image Optimization

```yaml
Banner: Max 500KB
Product images: Max 200KB
Thumbnails: Max 50KB
Format: WebP where possible
Lazy loading: Enable
```

### Speed Improvements

1. **Use caching** (WP Rocket)
2. **CDN for images** (Cloudflare)
3. **Minimize plugins**
4. **Optimize database**
5. **Compress images** (ShortPixel)

---

## Next Steps

**Your stores look great! Now:**

1. **[Add Developer Features →](05-developer-guide.md)**
2. **[Create Shortcodes →](06-shortcodes-reference.md)**
3. **[Fix Any Issues →](07-troubleshooting.md)**
4. **[Launch Your Marketplace →](08-faq.md)**

---

**Need Design Help?**  
📧 Email: support@wbcomdesigns.com  
🎨 Customization service available  
💬 Forum: wbcomdesigns.com/support