# Reign GeoDirectory Addon - Installation & Setup Guide

## What You'll Learn
This guide walks you through installing and setting up the Reign GeoDirectory addon to create a powerful directory website with beautiful listings and maps. We'll make it simple - perfect for beginners!

## Before You Start - Essential Checklist ✅

**You must have these installed first:**
1. ✅ WordPress (version 5.0 or higher)
2. ✅ Reign Theme (latest version)
3. ✅ GeoDirectory plugin (free or premium)
4. ✅ BuddyPress (optional but recommended)

**Also helpful to have:**
- Your WBcom purchase receipt
- About 25-30 minutes of time
- Sample listings ready to add

---

## Part 1: Download Your Addon Files

### Step 1: Get Your Files from WBcom

1. **Login to your WBcom account:**
   - Go to `wbcomdesigns.com`
   - Click "My Account" (top right corner)
   - Enter your login credentials

2. **Find your purchase:**
   - Click "Downloads" in the account menu
   - Look for "Reign GeoDirectory Addon"
   - Click the download button

3. **Save the zip file:**
   - Save to your Downloads folder
   - File will be named `reign-geodirectory-addon.zip`
   - **Don't unzip it!** WordPress needs the zip file

### Step 2: Verify Download Contents

Your download should include:
- `reign-geodirectory-addon.zip` (main plugin file)
- `license.txt` (your license key)
- `installation-guide.pdf` (quick reference)

---

## Part 2: Install GeoDirectory Plugin

### Step 1: Install GeoDirectory Core

**GeoDirectory is required for the addon to work:**

1. **Go to Plugins:**
   - **Plugins** → **Add New**
   - Search "GeoDirectory"
   - Install and activate the **GeoDirectory plugin**

2. **Run GeoDirectory setup:**
   - Follow the setup wizard
   - Choose your directory type
   - Configure basic settings
   - Import sample data (optional)

### Step 2: Install Recommended Extensions

**Popular GeoDirectory extensions:**

| Extension | What It Does | Recommended For |
|-----------|--------------|-----------------|
| **Location Manager** | Manage countries/regions | Most sites |
| **Advance Search** | Enhanced search filters | Better UX |
| **Events** | Add events to listings | Entertainment sites |
| **Payment Manager** | Paid listings | Revenue generation |
| **Review Manager** | Advanced reviews | Trust building |

---

## Part 3: Install the Reign Addon

### Method 1: WordPress Admin Upload (Recommended)

1. **Access your WordPress admin:**
   ```
   yoursite.com/wp-admin
   ```

2. **Navigate to plugins:**
   - Click **Plugins** in the left sidebar
   - Click **Add New** at the top
   - Click **Upload Plugin** button

3. **Upload your file:**
   - Click **Choose File**
   - Select `reign-geodirectory-addon.zip`
   - Click **Install Now**
   - Wait for "Plugin installed successfully"

4. **Activate the plugin:**
   - Click **Activate Plugin**
   - You'll see a success message

### Method 2: FTP Upload (If Method 1 Fails)

**Use this if you get file size errors:**

1. **Unzip the file on your computer**
2. **Connect via FTP to your site**
3. **Navigate to:** `/wp-content/plugins/`
4. **Upload folder:** `reign-geodirectory-addon`
5. **Go back to WordPress admin → Plugins**
6. **Find and activate** the Reign GeoDirectory Addon

---

## Part 4: License Activation

### Why License Activation is Important
- 🔄 Enables automatic updates
- 🛡️ Access to support
- ✨ Unlocks all premium features
- 🔒 Security patches

### Steps to Activate License:

1. **Find your license key:**
   - Check your purchase email
   - Or login to WBcom account → Licenses
   - Copy the license key (format: XXXX-XXXX-XXXX-XXXX)

2. **Enter in WordPress:**
   - Go to **Reign Settings** → **License**
   - Find "Reign GeoDirectory Addon" section
   - Paste your license key
   - Click **Activate License**

3. **Confirm activation:**
   - Look for green "Active" status
   - If you see red, double-check the key

**License Troubleshooting:**

| Problem | Solution |
|---------|----------|
| "Invalid license" | Remove spaces, check for typos |
| "Already activated" | Deactivate on old site first |
| "Expired license" | Renew at wbcomdesigns.com |
| "Site URL mismatch" | Ensure www/non-www matches |

---

## Part 5: Initial Configuration

### Step 1: Enable GeoDirectory Integration

1. **Go to Customizer:**
   - **Appearance** → **Customize**
   - Look for **Reign GeoDirectory Settings**
   - Click to expand

2. **Enable integration:**
   - Toggle ON "Enable GeoDirectory Integration"
   - Click **Publish** to save

### Step 2: Configure Directory Layout

**In the same Customizer section:**

```yaml
Listing Grid Layout: 3 columns (recommended)
Listing Card Style: Modern (clean look)
Show Listing Features: Yes
Show Rating Stars: Yes
Show Pricing: Yes
Show Location: Yes
Enable Map Integration: Yes
```

### Step 3: Set Up Essential Pages

**GeoDirectory creates these pages automatically:**
- Listings page (all listings)
- Add Listing page (submit new listings)
- Search page (advanced search)
- Location pages (browse by area)

**If pages are missing:**
1. Go to **GeoDirectory** → **Settings** → **General**
2. **Page Setup** section
3. Select appropriate pages for each function
4. **Save Changes**

---

## Part 6: Google Maps Setup

### Configure Maps API

**GeoDirectory requires Google Maps API for maps:**

1. **Get Google Maps API Key:**
   - Go to Google Cloud Console
   - Create new project or select existing
   - Enable Maps JavaScript API
   - Create credentials (API key)
   - Copy the API key

2. **Add API key to GeoDirectory:**
   ```
   GeoDirectory → Settings → Google Maps
   Paste API key in "Google Maps API Key" field
   Save Changes
   ```

3. **Test map functionality:**
   - Create test listing
   - Check if map displays correctly
   - Verify location search works

### Map Display Options

**Configure map settings:**

```yaml
Default Map Type: Roadmap
Map Zoom Level: 13
Show Map on Listing Page: Yes
Show Map on Detail Page: Yes
Enable Street View: Yes
Map Height: 300px (desktop), 200px (mobile)
```

---

## Part 7: BuddyPress Integration (Optional)

### Why Integrate with BuddyPress?
- 👥 User profiles with listings
- 💬 Community discussions
- 📊 Activity feeds for listings
- 👥 User connections
- 🎯 Social sharing of listings

### Steps to Enable:

1. **Install BuddyPress** (if not already installed)
   - Plugins → Add New
   - Search "BuddyPress"
   - Install and activate

2. **Configure BuddyPress:**
   - **Settings** → **BuddyPress** → **Components**
   - Enable:
     - ✅ Activity Streams
     - ✅ User Profiles
     - ✅ User Groups
     - ✅ Private Messaging

3. **Enable GeoDirectory-BuddyPress connection:**
   - **Appearance** → **Customize** → **Reign GeoDirectory**
   - Toggle ON "BuddyPress Integration"
   - **Publish** changes

---

## Part 8: Listing Display Settings

### Configure Listing Cards

**Go to:** **Appearance** → **Customize** → **Reign GeoDirectory** → **Listing Cards**

**Essential settings:**

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Show Featured Image** | Yes | Visual appeal |
| **Show Business Name** | Yes | Identification |
| **Show Category** | Yes | Easy browsing |
| **Show Rating** | Yes | Trust building |
| **Show Price/Cost** | Yes | Clear expectations |
| **Show Location** | Yes | Geographic context |
| **Show Description** | Excerpt | Preview content |
| **Show Contact Info** | Limited | Privacy balance |

### Listing Archive Layout

```yaml
Listings Per Page: 12
Grid Columns: 3 (desktop), 1 (mobile)
Sorting Options:
  - Newest first
  - Rating: High to low
  - Distance: Near to far
  - Alphabetical
  - Featured first
Filters: Category, Location, Price, Rating
```

---

## Part 9: User Role Configuration

### Understanding GeoDirectory User Roles

**GeoDirectory adds these capabilities:**
- **Subscriber** - Can submit listings (if enabled)
- **Contributor** - Can manage own listings
- **Author** - Can publish listings
- **Editor** - Can manage all listings
- **Administrator** - Full directory control

### Configure Submission Permissions

1. **Go to:** **GeoDirectory** → **Settings** → **General**
2. **Set user permissions:**
   ```yaml
   Who can submit listings: Registered users
   Auto-publish listings: No (for quality control)
   Allow guest submissions: Optional
   Require login to view: Optional
   ```

3. **Save settings**

---

## Part 10: Categories & Fields Setup

### Create Listing Categories

1. **Go to:** **GeoDirectory** → **Places** → **Categories**

2. **Add main categories:**
   ```yaml
   Example categories:
   - Restaurants & Food
   - Shopping & Retail
   - Health & Medical
   - Automotive
   - Entertainment
   - Professional Services
   - Real Estate
   ```

3. **Configure category settings:**
   - Upload category icons
   - Set category colors
   - Add descriptions
   - Configure custom fields per category

### Customize Listing Fields

**Common useful fields:**

| Field Type | Example Use | Best For |
|------------|-------------|----------|
| **Text** | Business name, tagline | Basic info |
| **Textarea** | Description, features | Detailed info |
| **URL** | Website, social media | Contact info |
| **Email** | Contact email | Communication |
| **Phone** | Phone number | Direct contact |
| **File** | Menu, brochure | Documents |
| **Select** | Cuisine type, services | Categories |
| **Checkbox** | Amenities, features | Multiple options |

---

## Part 11: Search & Filter Setup

### Configure Advanced Search

1. **Install Advanced Search extension** (if available)

2. **Configure search fields:**
   ```yaml
   Search by:
   - Keyword/business name
   - Category
   - Location/distance
   - Price range
   - Rating
   - Custom fields
   ```

3. **Search display options:**
   ```yaml
   Search widget locations:
   - Header
   - Sidebar
   - Homepage
   - Dedicated search page
   ```

### Location-Based Features

**Set up location hierarchy:**

```yaml
Location Structure:
  Country: United States
    State: California
      City: Los Angeles
        Neighborhood: Hollywood
```

**Enable location features:**
- Auto-detect user location
- Distance-based search
- Location-specific pages
- Local SEO optimization

---

## Part 12: Create Your First Listing

### Quick Listing Setup Test

1. **Create a test listing:**
   - **GeoDirectory** → **Places** → **Add New**
   - Fill in required fields
   - Add location and map marker
   - Upload images
   - **Publish**

2. **Test frontend submission:**
   - Go to "Add Listing" page
   - Submit listing as regular user
   - Check submission workflow
   - Verify admin approval process

3. **Test search and display:**
   - Search for your test listing
   - Check listing detail page
   - Verify map integration
   - Test contact forms

---

## Part 13: Payment Setup (Optional)

### Configure Paid Listings

**If using Payment Manager extension:**

1. **Install Payment Manager:**
   - Get from GeoDirectory website
   - Install and activate

2. **Set up pricing:**
   ```yaml
   Listing Types:
   - Free: Basic listing
   - Featured: $20/month
   - Premium: $50/month
   - Top Listing: $100/month
   ```

3. **Configure payment gateways:**
   - PayPal
   - Stripe
   - Bank transfer
   - Other processors

---

## Part 14: Performance Optimization

### Speed Up Your Directory

1. **Install caching plugin:**
   - WP Rocket (premium)
   - W3 Total Cache (free)
   - Configure for GeoDirectory

2. **Optimize images:**
   - Compress listing images
   - Use WebP format
   - Enable lazy loading

3. **Map optimization:**
   - Limit map API calls
   - Use map clustering
   - Cache location data

### Database Optimization

```yaml
Regular tasks:
- Clean up spam listings
- Remove expired listings
- Optimize location data
- Clear map cache
- Update search indexes
```

---

## Troubleshooting Common Issues

### "Maps not displaying"

**Solution 1: Check API key**
1. Verify Google Maps API key is correct
2. Check API key permissions
3. Ensure billing is enabled on Google account
4. Test with fresh API key

**Solution 2: Check settings**
1. **GeoDirectory** → **Settings** → **Google Maps**
2. Verify all map settings
3. Test with default settings

### "Listings not showing"

**Check these settings:**
1. Listings are published (not draft)
2. Category assignments correct
3. Location data is complete
4. Cache is cleared

### "Search not working"

**Common fixes:**
1. Rebuild search indexes
2. Check search form configuration
3. Verify location hierarchy
4. Clear all caches

### "User submissions failing"

**Solution:**
1. Check user permissions
2. Verify required fields
3. Test file upload limits
4. Check form validation

---

## Security Checklist

### Protect Your Directory

**Essential security steps:**
- [ ] SSL certificate installed
- [ ] Strong admin passwords
- [ ] Regular backups scheduled
- [ ] Security plugin installed
- [ ] User registration monitored
- [ ] Listing moderation enabled
- [ ] Regular updates applied

---

## Final Setup Checklist

### Before Going Live:

**Technical checklist:**
- [ ] All plugins updated
- [ ] License activated
- [ ] Test listing created
- [ ] Maps working correctly
- [ ] Search functionality tested
- [ ] Mobile version tested
- [ ] User submission tested
- [ ] Backup system working

**Content checklist:**
- [ ] Categories created
- [ ] Sample listings added
- [ ] Location hierarchy set up
- [ ] Terms of service updated
- [ ] Privacy policy updated
- [ ] Submission guidelines created

---

## What's Next?

### Your directory is installed! Now:

1. **[Configure Your Directory →](03-configuration.md)**
   - Listing settings
   - User permissions
   - Payment options

2. **[Customize Listing Display →](04-listing-customization.md)**
   - Design listing pages
   - Customize layouts
   - Add branding

3. **[Create Your First Listings →](08-faq.md)**
   - Content planning
   - Category setup
   - User management

---

## Quick Reference

### Important URLs After Setup

```
Listings: yoursite.com/places/
Add Listing: yoursite.com/add-listing/
Search: yoursite.com/search/
Locations: yoursite.com/location/
Categories: yoursite.com/category/
Admin Settings: yoursite.com/wp-admin/edit.php?post_type=gd_place&page=geodirectory
```

### Default Shortcodes

| Shortcode | What It Shows | Where to Use |
|-----------|---------------|--------------|
| `[gd_listings]` | Listing grid | Homepage, category pages |
| `[gd_add_listing]` | Submission form | Add listing page |
| `[gd_search]` | Search form | Header, sidebar |
| `[gd_map]` | Interactive map | Any page |

---

**Need Installation Help?**
📧 Email: support@wbcomdesigns.com
📚 Documentation: docs.wbcomdesigns.com
💬 Community: facebook.com/groups/wbcom
🎥 Video tutorials available in member area