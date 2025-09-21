# Reign WCFM Addon - Installation & Setup

## Prerequisites

Before installing Reign WCFM Addon, ensure you have:

### Required Components
1. **WordPress** 5.8 or higher
2. **Reign Theme** 7.0 or higher (activated)
3. **WooCommerce** 5.0 or higher
4. **WCFM - WooCommerce Frontend Manager** 6.5 or higher
5. **PHP** 7.4 or higher
6. **MySQL** 5.6 or higher

### Recommended Components
- **WCFM Membership** (for vendor subscriptions)
- **WCFM Ultimate** (for advanced features)
- **BuddyPress** 9.0 or higher
- **Memory Limit**: 256MB minimum
- **Max Execution Time**: 300 seconds

## Installation Methods

### Method 1: Upload via WordPress Admin

1. **Download the Plugin**
   - Login to your WBcom Designs account
   - Navigate to Downloads section
   - Download `reign-wcfm-addon.zip`

2. **Upload to WordPress**
   ```
   WordPress Admin > Plugins > Add New > Upload Plugin
   ```
   - Click "Choose File"
   - Select `reign-wcfm-addon.zip`
   - Click "Install Now"

3. **Activate the Plugin**
   - Click "Activate Plugin" after installation

### Method 2: FTP Upload

1. **Extract the ZIP file**
2. **Upload via FTP** to `/wp-content/plugins/`
3. **Activate** from WordPress Admin

## Initial Setup

### Step 1: License Activation

1. Navigate to **Reign Settings > License**
2. Enter your license key
3. Click "Activate License"

### Step 2: Configure WCFM

#### Basic WCFM Settings

1. **Navigate to WCFM > Settings**

2. **Marketplace Settings**
   ```
   Store Settings:
   ├── Store URL: /store/
   ├── Store Per Page: 12
   ├── Store Header: Enable
   └── Store Sidebar: Enable
   ```

3. **Vendor Registration**
   ```
   Registration Settings:
   ├── Enable Vendor Registration: Yes
   ├── Auto Approve Vendor: No
   ├── Email Verification: Yes
   └── Terms & Conditions: Enable
   ```

### Step 3: Configure Reign WCFM Settings

1. **Navigate to Appearance > Customize > Reign WCFM**

2. **Store Listing Layout**
   ```php
   'layout_type' => 'grid', // grid or list
   'columns' => 3,
   'show_filters' => true,
   'show_sorting' => true
   ```

3. **Vendor Dashboard**
   ```php
   'dashboard_style' => 'modern',
   'menu_position' => 'left',
   'color_scheme' => 'inherit'
   ```

### Step 4: Create Essential Pages

#### Required Pages (Auto-created by WCFM)

| Page | Shortcode | Purpose |
|------|-----------|----------|
| Store List | `[wcfm_stores]` | Vendor directory |
| Vendor Dashboard | `[wcfm_vendor_dashboard]` | Vendor management |
| Vendor Registration | `[wcfm_vendor_registration]` | Vendor signup |
| Vendor Membership | `[wcfm_vendor_membership]` | Subscription plans |

#### Manual Page Creation (if needed)

```sql
-- Create store listing page
INSERT INTO wp_posts (post_title, post_content, post_status, post_type) 
VALUES ('Stores', '[wcfm_stores]', 'publish', 'page');
```

### Step 5: Configure Commission

1. **Navigate to WCFM > Settings > Commission**

```php
// Commission settings
'commission_mode' => 'percent', // percent, fixed, or by_sales_price
'commission_percent' => 10,
'get_shipping' => 'yes',
'get_tax' => 'no',
'withdrawal_limit' => 50
```

## Vendor Dashboard Setup

### Configure Dashboard Modules

1. **WCFM > Capability**
2. Select modules for vendors:
   - Products
   - Orders  
   - Coupons
   - Reports
   - Withdrawal
   - Settings
   - Support

### Dashboard Menu Customization

```php
// Customize vendor dashboard menu
add_filter('wcfm_menus', function($menus) {
    // Reorder or modify menu items
    $custom_order = array(
        'dashboard',
        'products',
        'orders',
        'reports-sales-by-date',
        'withdrawal',
        'settings'
    );
    
    // Reorganize menus
    $new_menus = array();
    foreach ($custom_order as $key) {
        if (isset($menus[$key])) {
            $new_menus[$key] = $menus[$key];
        }
    }
    
    return $new_menus;
});
```

## BuddyPress Integration

### Enable Vendor Profile Tab

```php
// Add store tab to BuddyPress profile
add_action('bp_setup_nav', function() {
    if (!wcfm_is_vendor(bp_displayed_user_id())) {
        return;
    }
    
    bp_core_new_nav_item(array(
        'name' => __('Store', 'reign-wcfm'),
        'slug' => 'store',
        'screen_function' => 'reign_wcfm_store_screen',
        'position' => 50,
        'default_subnav_slug' => 'products'
    ));
});
```

### Activity Stream Integration

```php
// Enable WCFM activities
add_filter('reign_wcfm_bp_activities', '__return_true');

// Activity types
$activity_types = array(
    'new_product',
    'new_coupon',
    'store_update',
    'product_review'
);
```

## Payment Gateway Setup

### Configure Vendor Payouts

1. **WCFM > Settings > Withdrawal**

2. **Payment Methods**
   - PayPal
   - Stripe Connect
   - Bank Transfer
   - Payoneer

3. **Withdrawal Settings**
   ```php
   'withdrawal_mode' => 'by_request', // or 'by_schedule'
   'withdrawal_schedule' => 'weekly',
   'minimum_withdrawal' => 50,
   'withdrawal_charges' => 2 // fixed or percent
   ```

## Email Configuration

### Setup Email Templates

1. **WCFM > Settings > Email**

2. Configure notifications:
   - New vendor registration
   - Product approval
   - New order
   - Withdrawal request
   - Commission invoice

### Custom Email Template

```php
// Customize vendor welcome email
add_filter('wcfm_email_content_wrapper', function($content, $email_type) {
    if ($email_type == 'vendor_new_account') {
        // Custom email template
        $content = '<div class="reign-email-wrapper">' . $content . '</div>';
    }
    return $content;
}, 10, 2);
```

## Performance Optimization

### Database Optimization

```sql
-- Add indexes for better performance
ALTER TABLE wp_wcfm_marketplace_orders 
ADD INDEX idx_vendor_order (vendor_id, order_id);

ALTER TABLE wp_wcfm_marketplace_store_taxonomies 
ADD INDEX idx_vendor_tax (vendor_id, taxonomy);
```

### Caching Configuration

```php
// Cache vendor data
define('WCFM_CACHE_TIME', 3600); // 1 hour

// Exclude pages from cache
$excluded_pages = array(
    '/store-manager/',
    '/vendor-dashboard/',
    '/my-account/',
    '/checkout/'
);
```

## Security Configuration

### File Upload Settings

```php
// Restrict vendor uploads
add_filter('wcfm_file_upload_types', function($types) {
    return array(
        'jpg', 'jpeg', 'png', 'gif', // Images
        'pdf', 'doc', 'docx', // Documents
        'mp4', 'webm' // Videos
    );
});

// Set upload size limit
add_filter('wcfm_file_upload_size', function() {
    return 5 * 1024 * 1024; // 5MB
});
```

### Capability Management

```php
// Restrict vendor capabilities
add_filter('wcfm_capability_options', function($capabilities) {
    // Disable specific capabilities
    $capabilities['manage_booking'] = 'no';
    $capabilities['view_commission'] = 'yes';
    $capabilities['sm_delete_product'] = 'no';
    
    return $capabilities;
});
```

## Membership Setup (Optional)

### Configure Membership Plans

1. **WCFM > Memberships > Add New**

2. **Plan Settings**
   ```
   Basic Plan:
   ├── Price: $19/month
   ├── Product Limit: 50
   ├── Commission: 15%
   └── Features: Basic support
   
   Premium Plan:
   ├── Price: $49/month
   ├── Product Limit: Unlimited
   ├── Commission: 10%
   └── Features: Priority support
   ```

### Subscription Integration

```php
// WooCommerce Subscriptions integration
add_action('wcfm_membership_registration', function($member_id, $plan_id) {
    // Create subscription
    $subscription = wcs_create_subscription(array(
        'customer_id' => $member_id,
        'billing_period' => 'month',
        'billing_interval' => 1
    ));
}, 10, 2);
```

## Troubleshooting Installation

### Common Issues

#### Vendor Dashboard Not Loading
```php
// Check if WCFM is active
if (!function_exists('wcfm_is_vendor')) {
    // WCFM not active or installed
}

// Flush rewrite rules
flush_rewrite_rules();
```

#### Commission Not Calculating
```php
// Debug commission
add_action('wcfm_commission_added', function($commission_id, $order_id) {
    error_log('Commission ID: ' . $commission_id);
    error_log('Order ID: ' . $order_id);
}, 10, 2);
```

## Verification Steps

1. **Test Vendor Registration**
   - Register new vendor
   - Verify email
   - Access dashboard

2. **Test Product Creation**
   - Add new product
   - Set pricing
   - Publish product

3. **Test Order Process**
   - Place test order
   - Check commission
   - Verify notifications

4. **Test Withdrawal**
   - Request withdrawal
   - Admin approval
   - Payment processing

## Next Steps

- [Configuration Guide](03-configuration.md) - Detailed settings
- [Store Customization](04-store-customization.md) - Customize vendor stores
- [Developer Guide](05-developer-guide.md) - Advanced development
- [Troubleshooting](07-troubleshooting.md) - Common issues