# Reign Dokan Addon - Installation & Setup

## Prerequisites

Before installing Reign Dokan Addon, ensure you have:

### Required Components
1. **WordPress** 5.8 or higher
2. **Reign Theme** 7.0 or higher (activated)
3. **WooCommerce** 5.0 or higher
4. **Dokan** (Free or Pro) 3.0 or higher
5. **PHP** 7.4 or higher
6. **MySQL** 5.6 or higher

### Recommended Components
- **BuddyPress** 9.0 or higher
- **Memory Limit**: 256MB minimum
- **Max Execution Time**: 300 seconds
- **Upload Max Size**: 64MB

## Installation Methods

### Method 1: Upload via WordPress Admin

1. **Download the Plugin**
   - Login to your WBcom Designs account
   - Navigate to Downloads section
   - Download `reign-dokan-addon.zip`

2. **Upload to WordPress**
   ```
   WordPress Admin > Plugins > Add New > Upload Plugin
   ```
   - Click "Choose File"
   - Select `reign-dokan-addon.zip`
   - Click "Install Now"

3. **Activate the Plugin**
   - Click "Activate Plugin" after installation
   - Or navigate to Plugins list and activate

### Method 2: FTP Upload

1. **Extract the ZIP file**
   ```
   reign-dokan-addon.zip -> reign-dokan-addon/
   ```

2. **Upload via FTP**
   ```
   /wp-content/plugins/reign-dokan-addon/
   ```

3. **Activate from WordPress Admin**
   ```
   Plugins > Installed Plugins > Reign Dokan Addon > Activate
   ```

### Method 3: WP-CLI Installation

```bash
# Upload the plugin
wp plugin install /path/to/reign-dokan-addon.zip

# Activate the plugin
wp plugin activate reign-dokan-addon
```

## Initial Setup

### Step 1: License Activation

1. Navigate to **Reign Settings > License**
2. Enter your license key
3. Click "Activate License"

```php
// License validation endpoint
https://wbcomdesigns.com/edd-sl-api/
```

**Note**: License activation enables:
- Automatic updates
- Premium support
- All features

### Step 2: Basic Configuration

#### Configure Dokan Settings

1. **Navigate to Dokan > Settings**

2. **General Settings**
   ```
   Selling Options:
   ☑ Enable New Vendor Registration
   ☑ New Vendor Enable Selling
   ☐ Disable Vendor Verification
   ```

3. **Store Settings**
   ```
   Store URL: /store/
   Store Listing: ☑ Enable
   Store Layout: Select "Reign Custom Layout"
   ```

#### Configure Reign Addon Settings

1. **Navigate to Appearance > Customize > Reign Dokan**

2. **Store Listing Settings**
   ```
   Layout Type: Grid / List
   Stores Per Page: 12
   Column Count: 3 (Desktop) / 2 (Tablet) / 1 (Mobile)
   ```

3. **Store Page Settings**
   ```
   Header Style: Classic / Modern
   Sidebar Position: Left / Right / None
   Product Display: Grid / List
   ```

### Step 3: Create Essential Pages

The addon requires these pages:

#### Automatic Page Creation
```php
// The plugin creates these pages automatically
- Store Listing (/stores/)
- Vendor Dashboard (/dashboard/)
- My Orders (/my-orders/)
```

#### Manual Page Creation (if needed)

1. **Store Listing Page**
   ```
   Title: Stores
   Slug: stores
   Shortcode: [dokan-stores]
   ```

2. **Vendor Dashboard**
   ```
   Title: Vendor Dashboard  
   Slug: dashboard
   Shortcode: [dokan-dashboard]
   ```

### Step 4: Menu Configuration

#### Add to Primary Menu

1. Go to **Appearance > Menus**
2. Add these items:
   - Stores (Store Listing Page)
   - Become a Vendor (Registration)
   - Vendor Dashboard (Conditional)

#### BuddyPress Integration Menu

```php
// Add to BuddyPress member menu
add_action('bp_member_options_nav', function() {
    if (dokan_is_user_seller(bp_displayed_user_id())) {
        echo '<li><a href="'.dokan_get_store_url(bp_displayed_user_id()).'">View Store</a></li>';
    }
});
```

## Post-Installation Tasks

### 1. Configure Permalinks

```
Settings > Permalinks
Select: Post name (/%postname%/)
Save Changes
```

### 2. Set Up Email Templates

1. Navigate to **Dokan > Settings > Email**
2. Configure vendor email notifications
3. Test email delivery

### 3. Configure Payment Methods

```
WooCommerce > Settings > Payments
Enable payment gateways:
- PayPal
- Stripe  
- Bank Transfer
```

### 4. Set Commission Rates

```
Dokan > Settings > Selling Options
Commission Type: Percentage / Fixed
Admin Commission: 10% (example)
```

## Verification Steps

### Test Installation

1. **Check Plugin Status**
   ```php
   if (is_plugin_active('reign-dokan-addon/reign-dokan-addon.php')) {
       echo 'Reign Dokan Addon is active';
   }
   ```

2. **Verify Template Loading**
   - Visit `/stores/` - Should show custom layout
   - Check store page - Should use Reign templates

3. **Test Vendor Registration**
   - Register as vendor
   - Access vendor dashboard
   - Create test product

### Common Installation Issues

#### Issue: Templates Not Loading

**Solution:**
```php
// Add to functions.php temporarily
add_filter('dokan_locate_template', function($template, $name) {
    error_log('Loading template: ' . $name);
    return $template;
}, 10, 2);
```

#### Issue: Styles Not Applied

**Solution:**
1. Clear cache (browser and server)
2. Regenerate CSS in Customizer
3. Check for CSS conflicts

#### Issue: 404 on Store Pages

**Solution:**
1. Go to Settings > Permalinks
2. Click "Save Changes" (flushes rewrite rules)
3. Clear cache

## Database Changes

The addon creates/modifies these database elements:

### Custom Tables
```sql
-- No custom tables created
-- Uses existing WooCommerce/Dokan tables
```

### Options Added
```php
reign_dokan_addon_version
reign_dokan_layout_type
reign_dokan_store_header_style
reign_dokan_sidebar_position
```

### User Meta
```php
dokan_enable_selling
dokan_store_name
dokan_store_url
```

## Performance Optimization

### Recommended Caching

```php
// Exclude these pages from cache
/dashboard/*
/my-account/*
/checkout/*
/cart/*
```

### Database Optimization

```sql
-- Add indexes for better performance
ALTER TABLE wp_usermeta 
ADD INDEX idx_dokan_seller (meta_key(20), meta_value(10));
```

## Security Considerations

### File Permissions

```bash
# Correct permissions
find reign-dokan-addon/ -type d -exec chmod 755 {} \;
find reign-dokan-addon/ -type f -exec chmod 644 {} \;
```

### Security Headers

```php
// Add to .htaccess in plugin folder
<FilesMatch "\.(php|php3|php4|php5|phtml|pl|py|jsp|asp|sh|cgi)$">
    Order Deny,Allow
    Deny from all
</FilesMatch>
```

## Uninstallation

### Safe Uninstall Process

1. **Backup Database**
2. **Deactivate Plugin**
3. **Delete Plugin** (optional)

### Data Cleanup (Optional)

```php
// Remove plugin options
delete_option('reign_dokan_addon_version');
delete_option('reign_dokan_layout_type');
// ... other options
```

## Next Steps

- [Configuration Guide](03-configuration.md) - Detailed configuration options
- [Store Customization](04-store-customization.md) - Customize vendor stores
- [Troubleshooting](06-troubleshooting.md) - Common issues and solutions