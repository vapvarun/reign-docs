# Reign WCFM Addon - Store Customization Guide

## What You'll Learn
This guide will help you customize how vendor stores look and function on your marketplace. No coding experience needed - we'll walk you through each step with clear instructions.

## Quick Overview
**Time needed:** 30-45 minutes  
**Difficulty:** Easy to Moderate  
**Requirements:** WCFM and Reign theme installed

---

## Part 1: Customizing Store Appearance

### Step 1: Choose Your Store Layout

**Where to go:**
1. Login to WordPress admin
2. Navigate to **Appearance** → **Customize**
3. Click on **Reign WCFM Settings**
4. Select **Store Layout**

**Your options:**

| Layout Type | Best For | What It Looks Like |
|-------------|----------|--------------------|
| **Grid View** | Visual products | Square cards in rows |
| **List View** | Detailed info | One store per row with details |
| **Map View** | Local businesses | Interactive map with markers |

**How to choose:**
- **Grid View** → Choose this if you have stores with attractive banners/logos
- **List View** → Choose this for B2B marketplaces or service providers
- **Map View** → Choose this for local marketplaces or delivery services

### Step 2: Customize Store Cards

**What you can show/hide on each store card:**

1. **Store Banner** 
   - ✅ Turn ON if: Vendors have professional banners
   - ❌ Turn OFF if: You want a cleaner, minimal look

2. **Store Rating**
   - ✅ Turn ON if: Customer reviews are important
   - ❌ Turn OFF if: You're just starting (no reviews yet)

3. **Product Count**
   - ✅ Turn ON if: You want to show store size
   - ❌ Turn OFF if: Some vendors have few products

4. **Location Info**
   - ✅ Turn ON if: Location matters to customers
   - ❌ Turn OFF if: All vendors ship everywhere

**How to customize:**
1. Go to **Appearance** → **Customize** → **Reign WCFM**
2. Click **Store Card Elements**
3. Toggle each element ON/OFF
4. Click **Publish** to save

### Step 3: Set Your Colors

**Where to customize colors:**
1. **Appearance** → **Customize** → **Colors**
2. Look for **WCFM Colors** section

**Color settings explained:**

| Color Setting | What It Changes | Recommended Color |
|---------------|-----------------|-------------------|
| **Primary Color** | Buttons, links | Your brand color |
| **Store Header** | Top of store pages | Darker shade of primary |
| **Rating Stars** | Review stars | Yellow/Gold (#FFB400) |
| **Sale Badge** | Discount labels | Red (#FF0000) |
| **Online Indicator** | Shows vendor is online | Green (#00D084) |

**Pro tip:** Keep colors consistent with your main site theme!

---

## Part 2: Individual Store Page Setup

### Step 1: Store Header Style

**Choose how the top of vendor stores look:**

1. **Classic Header**
   - Banner at top
   - Store info below
   - Best for: Traditional marketplaces

2. **Modern Overlay**
   - Store info over banner
   - Looks contemporary
   - Best for: Fashion, creative products

3. **Minimal Header**
   - No banner, just essentials
   - Clean and fast
   - Best for: B2B or professional services

**How to change:**
```
Appearance → Customize → Reign WCFM → Store Header Style
```

### Step 2: Store Sidebar Options

**What can appear in the store sidebar:**

- **Store Information** - Address, phone, email
- **Store Hours** - Opening times
- **Product Categories** - What they sell
- **Best Sellers** - Popular products
- **Store Policies** - Shipping, returns
- **Contact Form** - Customer inquiries

**How to set up:**
1. Go to **Appearance** → **Widgets**
2. Find **WCFM Store Sidebar**
3. Drag widgets you want into this area
4. Arrange in order you prefer

### Step 3: Store Tabs Configuration

**What tabs can appear on store pages:**

| Tab Name | What It Shows | When to Enable |
|----------|---------------|----------------|
| **Products** | Store's items | Always enable |
| **About** | Store description | Enable for storytelling |
| **Policies** | Terms, shipping | Enable for trust |
| **Reviews** | Customer feedback | Enable after getting reviews |
| **Contact** | Inquiry form | Enable for B2B |

**To enable/disable tabs:**
1. Go to **WCFM** → **Settings** → **Store**
2. Find **Store Tab Manager**
3. Check/uncheck tabs you want
4. Click **Save**

---

## Part 3: Mobile Store Experience

### Making Stores Mobile-Friendly

**Automatic mobile optimizations:**
- ✅ Menus become hamburger menu
- ✅ Images resize automatically
- ✅ Touch-friendly buttons
- ✅ Simplified checkout

**Settings to check:**

1. **Mobile Products Per Row**
   ```
   Appearance → Customize → Reign WCFM → Mobile Settings
   Set to: 1 or 2 products per row
   ```

2. **Mobile Menu Style**
   ```
   Choose: Bottom navigation bar (easier to reach)
   ```

3. **Mobile Filters**
   ```
   Enable: Collapsible filters (saves space)
   ```

---

## Part 4: Vendor Dashboard Customization

### Step 1: Dashboard Color Scheme

**Make vendor dashboard match your brand:**

1. Go to **WCFM** → **Settings** → **Dashboard Colorizer**
2. Set these colors:
   - **Header Background**: Your brand color
   - **Menu Background**: Slightly darker
   - **Menu Text**: White or light color
   - **Content Background**: White or light gray

### Step 2: Dashboard Menu Items

**What vendors see in their dashboard:**

**Essential items (always show):**
- Dashboard (overview)
- Products
- Orders
- Store Settings

**Optional items (show based on your marketplace):**
- Coupons - If you allow vendor promotions
- Reports - For data-driven vendors
- Enquiries - For customer questions
- Support - If you offer vendor support

**To customize menu:**
1. Go to **WCFM** → **Capability**
2. Click **Vendor** user role
3. Check/uncheck menu items
4. Save changes

### Step 3: Dashboard Widgets

**What information widgets to show:**

| Widget | Shows | Enable If |
|--------|-------|----------|
| **Sales Stats** | Revenue graphs | Vendors need analytics |
| **Order Stats** | Recent orders | Always enable |
| **Top Products** | Best sellers | Helpful for vendors |
| **Reviews** | Recent feedback | Quality matters |
| **Announcements** | Your messages | You send updates |

---

## Part 5: Store SEO & Social Features

### SEO Settings for Better Google Rankings

**For each store:**
1. Vendors go to **Dashboard** → **Store Settings** → **SEO**
2. They should fill in:
   - **SEO Title**: Store name + what they sell
   - **Meta Description**: 1-2 sentences about their store
   - **Keywords**: Products they sell

**Example:**
```
Title: Sarah's Handmade Jewelry - Custom Rings & Necklaces
Description: Beautiful handcrafted jewelry made with love. Custom designs available.
Keywords: handmade jewelry, custom rings, artisan necklaces
```

### Social Media Integration

**Let vendors add social links:**
1. In vendor dashboard → **Settings** → **Social**
2. Add fields for:
   - Facebook page
   - Instagram profile
   - Twitter/X handle
   - Pinterest boards

**These appear as:**
- Icons in store header
- Links in store sidebar
- Share buttons on products

---

## Part 6: Quick Customization Recipes

### Recipe 1: Professional B2B Marketplace

```yaml
Layout: List View
Sidebar: Left side
Show: Company info, certificates, policies
Hide: Social media, reviews initially
Colors: Conservative (blues, grays)
Header: Minimal style
```

### Recipe 2: Trendy Fashion Marketplace

```yaml
Layout: Grid View
Sidebar: None (full width)
Show: Large banners, Instagram feed, reviews
Hide: Detailed policies
Colors: Bold and vibrant
Header: Modern overlay
```

### Recipe 3: Local Food Marketplace

```yaml
Layout: Map View
Sidebar: Right side
Show: Location, delivery areas, hours
Hide: Social media
Colors: Fresh (greens, oranges)
Header: Classic with hours visible
```

---

## Common Customization Tasks

### Task: "I want to add a verified badge to trusted vendors"

**Steps:**
1. Install **WCFM Verification** addon
2. Go to **WCFM** → **Vendors**
3. Click on vendor → **Verification**
4. Mark as verified
5. Badge appears automatically

### Task: "I want different layouts for different vendor types"

**Solution:**
1. Use **WCFM Groups** addon
2. Create vendor groups (e.g., Premium, Standard)
3. Assign different capabilities per group
4. Premium vendors get more features

### Task: "I want to feature certain vendors"

**How to:**
1. Go to **WCFM** → **Vendors**
2. Click **Quick Edit** on vendor
3. Check **Featured Vendor**
4. They appear first in listings

---

## Troubleshooting Store Display

### Problem: "Store looks broken on mobile"

**Fix:**
1. Clear cache (both browser and site)
2. Check **Appearance** → **Customize** → **Mobile Settings**
3. Ensure responsive mode is ON
4. Test in Chrome DevTools mobile view

### Problem: "Store banner not showing"

**Fix:**
1. Check image size (recommended: 1920x400px)
2. Verify file type (JPG or PNG)
3. Check vendor has uploaded banner
4. Clear CDN cache if using one

### Problem: "Colors not applying"

**Fix:**
1. Click **Publish** in Customizer (not just Save)
2. Clear all caches
3. Check for custom CSS conflicts
4. Try in private/incognito browser

---

## Best Practices Summary

### Do's ✅
- Keep design consistent across all stores
- Make important info visible immediately
- Test on mobile devices regularly
- Use high-quality images
- Keep load times under 3 seconds

### Don'ts ❌
- Don't overcrowd store pages
- Don't use too many colors
- Don't hide contact information
- Don't forget mobile users
- Don't skip SEO settings

---

## Next Steps

**Now that your stores look great:**
1. [Set up vendor payments](05-developer-guide.md)
2. [Configure commissions](03-configuration.md)
3. [Test the customer journey](07-troubleshooting.md)
4. [Launch your marketplace!](08-faq.md)

---

**Need Help?**  
📧 Email: support@wbcomdesigns.com  
📚 Docs: docs.wbcomdesigns.com  
💬 Forum: wbcomdesigns.com/support