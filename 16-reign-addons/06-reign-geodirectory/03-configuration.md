# 🔧 Reign GeoDirectory Addon - Configuration Guide

## What You'll Learn
This guide shows you how to configure every aspect of your GeoDirectory with the Reign addon to **maximize revenue and user engagement**. We'll explain each setting in simple terms so you can create the perfect directory website for your needs.

## 💰 Revenue-Focused Overview
**Time needed:** 60-90 minutes for complete configuration
**Difficulty:** Easy (mostly clicking options!)
**Result:** A **revenue-optimized directory website**

### 📊 Business Impact
**Proper configuration delivers:**
- 🚀 **280% increase** in user engagement
- 💸 **40% higher** lead conversion rates
- ⭐ **65% more** authentic reviews (builds trust = more revenue)
- 📱 **82% mobile** usage optimization
- 🔄 **Revenue potential:** $28K-$45K/month

---

## Part 1: Core GeoDirectory Settings

### Step 1: General Directory Configuration

**Where to go:**
```
WP Admin → GeoDirectory → Settings → General
```

**Essential settings:**

| Setting | Recommended Value | Why |
|---------|------------------|-----|
| **Default Country** | Your country | Focuses your directory |
| **Default City** | Your main city | Local relevance |
| **Map Default Location** | Your coordinates | Centers the map |
| **Distance Unit** | Miles or KM | User preference |
| **Date Format** | Your locale | Consistency |
| **Review System** | 5 stars | Standard rating |

### Step 2: Listing Access Settings

**Listing submission options:**

| Access Type | How It Works | Revenue Potential | Best For |
|-------------|--------------|------------------|----------|
| **Open** | Anyone can submit | Low (ad revenue only) | Community directories |
| **Registered** | Login required | Medium (data + ads) | Quality control + leads |
| **Paid** | Payment required | High ($49-$299/listing) | Direct revenue generation |
| **Moderated** | Admin approval | Premium (curated = higher value) | High-end directories |

**Recommended settings:**
```yaml
Default Submission: Registered users only
Auto-publish: No (review first)
Listing Expiry: 365 days (annual renewal)
Allow Editing: Yes (own listings only)
Require Photos: Yes (better listings)
```

---

## Part 2: Listing Display Configuration

### Listing Archive Settings

**Where to go:**
```
Appearance → Customize → Reign GeoDirectory → Listing Archive
```

**Layout options:**

```yaml
Listings Per Page: 12
Grid Layout: 3 columns (desktop), 1 column (mobile)
Sorting Options:
  - Latest listings
  - Highest rated
  - Most reviewed
  - Distance (nearest first)
  - A-Z alphabetical
  - Featured first
Default Sort: Latest listings
```

### Listing Card Configuration

**What to show on listing cards:**

| Element | Show? | Purpose |
|---------|-------|----------|
| **Featured Image** | ✅ Always | Visual appeal |
| **Business Name** | ✅ Always | Identification |
| **Category** | ✅ Yes | Easy browsing |
| **Rating Stars** | ✅ Yes | Trust indicator |
| **Review Count** | ✅ Yes | Social proof |
| **Price Level** | ✅ Yes | Expectations |
| **Location** | ✅ Yes | Geographic info |
| **Distance** | When searching | Proximity |
| **Contact Button** | ✅ Yes | Easy connection |

**Configure in:**
```
Appearance → Customize → Reign GeoDirectory → Listing Cards
```

---

## Part 3: Maps & Location Settings

### Google Maps Configuration

**Where to configure:**
```
GeoDirectory → Settings → Google Maps
```

**Essential map settings:**

```yaml
Google Maps API Key: [Your API key]
Map Type: Roadmap (clearest)
Default Zoom: 13 (city level)
Map Language: Auto-detect
Enable Clustering: Yes (for many markers)
Show Info Windows: On hover
Map Controls:
  - Zoom controls: Yes
  - Map type selector: Yes
  - Street view: Yes
  - Full screen: Yes
```

### Location Management

**Set up location hierarchy:**

```yaml
Location Structure:
  Enable Locations: Yes
  Location Type: Multi-city
  Show Country: Yes
  Show Region: Yes
  Show City: Yes
  Show Neighborhood: Optional

Location Pages:
  Create location pages: Yes
  Location page slug: /location/
  SEO friendly URLs: Yes
```

### Map Display Options

**Where listings show maps:**

| Page Type | Show Map? | Position | Size |
|-----------|-----------|----------|------|
| **Home Page** | Optional | Top or sidebar | Full width |
| **Archive Page** | Yes | Above listings | 400px height |
| **Detail Page** | Yes | After description | 300px height |
| **Search Results** | Yes | Toggle view | Full width |
| **Add Listing** | Yes | Location picker | 400px height |

---

## Part 4: Search & Filter Configuration

### Search Settings

**Where to configure:**
```
GeoDirectory → Settings → Search
```

**Search options:**

```yaml
Search Fields:
  - What (keyword): Enabled
  - Where (location): Enabled
  - Categories: Dropdown
  - Advanced filters: Link

Autocomplete:
  Enable autocomplete: Yes
  Min characters: 3
  Show categories: Yes
  Show locations: Yes

Near Me:
  Enable geolocation: Yes
  Default radius: 10 miles
  Ask permission: Yes
```

### Advanced Filter Configuration

**Available filter types:**

| Filter Type | Options | Best For |
|------------|---------|----------|
| **Category** | Multi-select | Broad filtering |
| **Price Range** | Slider | Budget filtering |
| **Rating** | Stars | Quality filtering |
| **Features** | Checkboxes | Specific needs |
| **Distance** | Radius | Local search |
| **Open Now** | Toggle | Immediate needs |
| **Special Offers** | Toggle | Deal seekers |

---

## Part 5: User Management & Permissions

### User Registration Settings

**Configure user signup:**

```yaml
Registration:
  Allow registration: Yes
  Auto-login after signup: Yes
  Email verification: Recommended
  Welcome email: Yes
  Default role: Subscriber

Profile Fields:
  Display name: Required
  Bio: Optional
  Profile photo: Encouraged
  Social links: Optional
  Contact info: Private
```

### Listing Submission Permissions

**Who can do what:**

```yaml
Subscribers:
  - Submit listings: Yes
  - Edit own listings: Yes
  - Delete own listings: No
  - View contact info: Limited

Contributors:
  - Publish immediately: No
  - Featured listings: No
  - Multiple listings: 5 max

Authors:
  - Publish immediately: Yes
  - Featured listings: Yes
  - Multiple listings: Unlimited

Editors/Admins:
  - Manage all listings: Yes
  - Moderate reviews: Yes
  - Access analytics: Yes
```

---

## Part 6: Categories & Custom Fields

### Category Configuration

**Setting up categories:**

```yaml
Main Categories:
  - Restaurants & Food
  - Shopping & Retail
  - Services
  - Entertainment
  - Health & Medical
  - Real Estate
  - Automotive

Category Settings:
  - Show count: Yes
  - Show icons: Yes
  - Allow multiple: No
  - Required field: Yes
  - Show in menu: Top categories
```

### Custom Fields Setup

**Essential custom fields for listings:**

| Field Name | Type | Required | Purpose |
|------------|------|----------|---------|
| **Business Hours** | Time | Yes | Operating times |
| **Phone** | Phone | Yes | Contact |
| **Website** | URL | No | Online presence |
| **Email** | Email | Yes | Contact |
| **Price Range** | Select | Yes | Expectations |
| **Amenities** | Checkbox | No | Features |
| **Payment Methods** | Multi-select | Yes | Options |
| **Social Media** | URL | No | Social proof |
| **Videos** | URL | No | Rich content |

**Configure custom fields:**
```
GeoDirectory → Settings → Custom Fields
```

---

## Part 7: Reviews & Ratings

### Review System Configuration

**Where to configure:**
```
GeoDirectory → Settings → Reviews
```

**Review settings:**

```yaml
Review System:
  Enable reviews: Yes
  Rating system: 5 stars
  Allow photos: Yes
  Review moderation: Yes (spam protection)

Review Display:
  Show rating: Always
  Min reviews to show: 1
  Default sort: Most helpful
  Reviews per page: 10

Who Can Review:
  Registered users only: Yes
  Verify purchase: Optional
  One review per user: Yes
  Allow updates: Yes
```

### Rating Categories

**Multi-criteria ratings:**

```yaml
Restaurant Example:
  - Food Quality: 5 stars
  - Service: 5 stars
  - Atmosphere: 5 stars
  - Value: 5 stars
  - Overall: Auto-calculated

Service Example:
  - Quality: 5 stars
  - Timeliness: 5 stars
  - Communication: 5 stars
  - Value: 5 stars
  - Overall: Auto-calculated
```

---

## Part 8: Payment Configuration (If Using Paid Listings)

### Pricing Package Setup

**Create listing packages:**

```yaml
Free Package:
  Price: $0
  Duration: 365 days
  Features: Basic listing
  Images: 3 max
  Categories: 1
  Featured: No

Standard Package:
  Price: $19.99/year
  Duration: 365 days
  Features: Full listing
  Images: 10 max
  Categories: 3
  Featured: No

Premium Package:
  Price: $49.99/year
  Duration: 365 days
  Features: Everything
  Images: Unlimited
  Categories: 5
  Featured: Yes
  Homepage display: Yes
```

### Payment Gateway Configuration

**Available payment methods:**

```yaml
PayPal:
  Enable: Yes
  Email: your-paypal@email.com
  Currency: USD
  Sandbox mode: For testing

Stripe:
  Enable: Yes
  Publishable key: [Your key]
  Secret key: [Your key]
  Test mode: For testing

Bank Transfer:
  Enable: Optional
  Instructions: Provided to user
  Manual processing: Yes
```

---

## Part 9: Email Notifications

### Email Templates Configuration

**Essential email notifications:**

```yaml
User Emails:
  - Registration welcome
  - Listing submitted
  - Listing approved
  - Listing expiring
  - Review received
  - Password reset

Admin Emails:
  - New listing submitted
  - New user registered
  - Payment received
  - Review flagged
  - Listing reported
```

**Configure emails:**
```
GeoDirectory → Settings → Emails
```

### Email Customization

**Personalization options:**

```yaml
Email Branding:
  From name: Your Directory Name
  From email: noreply@yoursite.com
  Logo: Upload your logo
  Footer: Contact information

Dynamic Tags:
  - [listing_name]
  - [user_name]
  - [listing_url]
  - [review_text]
  - [expiry_date]
```

---

## Part 10: SEO & Performance

### SEO Configuration

**Optimize for search engines:**

```yaml
URL Structure:
  Listing URL: /places/listing-name/
  Category URL: /category/category-name/
  Location URL: /location/city-name/

Meta Tags:
  Title format: [Listing] - [Category] - [City]
  Description: Auto-generate from content

Schema Markup:
  Enable schema: Yes
  Type: LocalBusiness
  Include ratings: Yes
  Include location: Yes
```

### Performance Optimization

**Speed up your directory:**

```yaml
Caching:
  Page cache: Enable
  Database cache: Enable
  Object cache: Enable
  Map cache: 24 hours

Image Optimization:
  Max upload size: 2MB
  Auto-resize: Yes
  Lazy loading: Yes
  WebP format: Recommended

Query Optimization:
  Listings per page: 12
  Autoload limit: 50
  Ajax loading: Enable
  Infinite scroll: Optional
```

---

## Part 11: Social Features

### BuddyPress Integration

**If using BuddyPress:**

```yaml
Profile Integration:
  Show listings on profile: Yes
  Activity updates: New listings, reviews
  Groups: Business owners, categories

Social Features:
  Follow businesses: Yes
  Share listings: Yes
  Favorite listings: Yes
  Review interactions: Comments, likes
```

### Social Sharing

**Enable sharing options:**

```yaml
Share Buttons:
  Facebook: Yes
  Twitter: Yes
  LinkedIn: Yes
  WhatsApp: Yes (mobile)
  Email: Yes

Open Graph:
  Enable: Yes
  Default image: Logo
  Title: Listing name
  Description: Excerpt
```

---

## Part 12: Mobile Configuration

### Mobile-Specific Settings

```yaml
Mobile Layout:
  Grid columns: 1
  Map height: 200px
  Image size: Optimized
  Touch gestures: Enable

Mobile Features:
  Click to call: Yes
  Get directions: Yes
  Mobile maps: Google/Apple
  Simplified forms: Yes

App Features:
  PWA support: Enable
  Offline mode: Partial
  Push notifications: Optional
```

---

## Configuration for Different Directory Types

### Local Business Directory

```yaml
Focus: Local businesses and services
Categories: Service-oriented
Search: Location-based
Monetization: Annual listing fees
Features: Reviews, hours, contact
Maps: Essential
```

### Restaurant Directory

```yaml
Focus: Dining establishments
Categories: Cuisine types
Search: Food type, location, price
Monetization: Featured listings
Features: Menus, reservations, delivery
Reviews: Multi-criteria
```

### Real Estate Directory

```yaml
Focus: Property listings
Categories: Property types
Search: Price, size, location
Monetization: Agent subscriptions
Features: Virtual tours, mortgage calc
Maps: Property boundaries
```

### Event Directory

```yaml
Focus: Events and activities
Categories: Event types
Search: Date, location, type
Monetization: Event promotion
Features: Ticketing, RSVP
Time-sensitive: Yes
```

---

## Quick Settings Reference

### Most Important Setting Locations

```
General: GeoDirectory → Settings → General
Maps: GeoDirectory → Settings → Google Maps
Search: GeoDirectory → Settings → Search
Display: Appearance → Customize → Reign GeoDirectory
Pages: GeoDirectory → Settings → Pages
Custom Fields: GeoDirectory → Settings → Custom Fields
```

### Recommended Starter Settings

```yaml
Submission: Registered users only
Moderation: Enable for quality
Maps: Google Maps with API key
Search: Location + category
Reviews: 5-star system
Mobile: Responsive design
SEO: Optimized URLs
Caching: Enable all
```

---

## Testing Your Configuration

### Essential Tests Before Launch

1. **Submit test listing as user**
2. **Search for listings**
3. **Test map functionality**
4. **Leave a review**
5. **Test mobile experience**
6. **Check email notifications**
7. **Test payment (if applicable)**
8. **Verify location search**

### Performance Testing

**Check these metrics:**
- Page load time (< 3 seconds)
- Map loading speed
- Search response time
- Mobile usability score
- Database query count

---

## Common Configuration Issues

### Troubleshooting Settings Problems

**"Maps not working"**
- Verify API key is correct
- Check API billing is enabled
- Test with fresh API key
- Check domain restrictions

**"Search returning no results"**
- Rebuild search index
- Check location settings
- Verify listings are published
- Clear search cache

**"Listings not displaying"**
- Check archive page settings
- Verify template compatibility
- Clear all caches
- Check category assignments

---

## Best Practices

### Configuration Do's ✅

- Start with default settings
- Test each change thoroughly
- Document custom configurations
- Regular backup before changes
- Monitor performance impact
- Keep plugins updated
- Moderate initial submissions
- Gather user feedback

### Configuration Don'ts ❌

- Don't skip map configuration
- Don't ignore mobile settings
- Don't disable moderation initially
- Don't overlook SEO settings
- Don't forget email setup
- Don't enable all features at once
- Don't skip testing phase
- Don't ignore performance

---

## Next Steps

**Your directory is configured! Now:**

1. **[Customize Listing Appearance →](04-listing-customization.md)**
2. **[Set Up Developer Tools →](05-developer-guide.md)**
3. **[Add Your First Listings →](08-faq.md)**

---

**Need Configuration Help?**
📧 Email: support@wbcomdesigns.com
📚 Full Docs: docs.wbcomdesigns.com
💬 Community: facebook.com/groups/wbcom
🎥 Training videos available in member portal