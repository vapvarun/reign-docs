# SureCart Integration User Guide for Reign Theme

## Overview

SureCart is a modern e-commerce platform designed for selling digital products, subscriptions, and services. Reign Theme provides seamless integration with SureCart, enabling you to create powerful membership sites, sell courses, and manage subscriptions within your community.

## What is SureCart?

SureCart is a headless e-commerce solution that offers:
- **Subscription Management:** Recurring payments and billing
- **Digital Downloads:** Sell and deliver digital products
- **Payment Processing:** Multiple gateway support
- **Customer Portal:** Self-service account management
- **Abandoned Cart Recovery:** Automatic recovery sequences
- **Tax Automation:** Global tax calculations
- **Affiliate System:** Built-in referral tracking

## Installation & Setup

### Requirements

```
WordPress: 5.8+
PHP: 7.4+
Reign Theme: 7.0+
SureCart Plugin: Latest version
SSL Certificate: Required for payments
```

### Installation Steps

1. **Install SureCart Plugin**
   ```
   1. WordPress Admin → Plugins → Add New
   2. Search for "SureCart"
   3. Install and Activate
   4. Or download from surecart.com
   ```

2. **Initial Setup Wizard**
   ```
   SureCart → Setup Wizard
   - Connect to SureCart account
   - Configure store settings
   - Set currency and location
   - Connect payment processor
   ```

3. **API Configuration**
   ```php
   // Add to wp-config.php if needed
   define('SURECART_API_URL', 'https://api.surecart.com');
   define('SURECART_API_KEY', 'your_api_key');
   ```

## Reign Theme Integration

### Automatic Styling

Reign automatically styles SureCart elements:
- Product cards
- Checkout forms
- Customer portal
- Subscription tables
- Price displays

### Custom Templates

```php
// Override SureCart templates in child theme
reign-child/
├── surecart/
│   ├── products/
│   │   ├── single-product.php
│   │   └── product-grid.php
│   ├── checkout/
│   │   └── form-checkout.php
│   └── account/
│       └── dashboard.php
```

## Product Display

### Product Grid Shortcode

```
[surecart_products columns="3" limit="9" category="courses"]
```

**Parameters:**
- `columns`: Number of columns (1-6)
- `limit`: Products to display
- `category`: Filter by category
- `order`: ASC/DESC
- `orderby`: date/title/price

### Custom Product Layout

```php
// Custom product card
function reign_surecart_product_card($product) {
    ?>
    <div class="reign-sc-product-card">
        <div class="product-image">
            <?php if ($product->featured_image): ?>
                <img src="<?php echo esc_url($product->featured_image); ?>" alt="<?php echo esc_attr($product->name); ?>">
            <?php endif; ?>

            <?php if ($product->on_sale): ?>
                <span class="sale-badge">Sale!</span>
            <?php endif; ?>
        </div>

        <div class="product-content">
            <h3><?php echo esc_html($product->name); ?></h3>

            <div class="product-price">
                <?php if ($product->prices): ?>
                    <?php foreach ($product->prices as $price): ?>
                        <span class="price"><?php echo sc_format_price($price->amount); ?></span>
                        <?php if ($price->recurring): ?>
                            <span class="recurring">/ <?php echo $price->recurring_period; ?></span>
                        <?php endif; ?>
                    <?php endforeach; ?>
                <?php endif; ?>
            </div>

            <div class="product-excerpt">
                <?php echo wp_trim_words($product->description, 20); ?>
            </div>

            <div class="product-actions">
                <a href="<?php echo esc_url($product->permalink); ?>" class="btn-view">View Details</a>
                <button class="btn-buy" data-sc-product-id="<?php echo $product->id; ?>">Buy Now</button>
            </div>
        </div>
    </div>
    <?php
}
```

### Product Categories

```php
// Display product categories
function reign_surecart_categories() {
    $categories = surecart_get_product_categories();
    ?>
    <div class="sc-categories">
        <?php foreach ($categories as $category): ?>
            <a href="<?php echo esc_url($category->link); ?>" class="category-card">
                <?php if ($category->image): ?>
                    <img src="<?php echo esc_url($category->image); ?>" alt="<?php echo esc_attr($category->name); ?>">
                <?php endif; ?>
                <h4><?php echo esc_html($category->name); ?></h4>
                <span class="count"><?php echo $category->product_count; ?> products</span>
            </a>
        <?php endforeach; ?>
    </div>
    <?php
}
```

## Membership Integration

### Protect Content

```php
// Restrict content to SureCart customers
function reign_restrict_to_customers($content) {
    if (!is_user_logged_in()) {
        return '<p>Please <a href="/login">login</a> to view this content.</p>';
    }

    $user_id = get_current_user_id();
    $customer = surecart_get_customer($user_id);

    if (!$customer || !$customer->has_active_subscription()) {
        return '<p>This content requires an active subscription. <a href="/pricing">View Plans</a></p>';
    }

    return $content;
}
add_filter('the_content', 'reign_restrict_to_customers');
```

### BuddyPress Integration

```php
// Add subscription status to BuddyPress profiles
add_action('bp_after_member_header', function() {
    $user_id = bp_displayed_user_id();
    $customer = surecart_get_customer($user_id);

    if ($customer && $customer->subscriptions): ?>
        <div class="member-subscription-badges">
            <?php foreach ($customer->subscriptions as $subscription): ?>
                <?php if ($subscription->status === 'active'): ?>
                    <span class="subscription-badge <?php echo esc_attr($subscription->product_id); ?>">
                        <?php echo esc_html($subscription->product_name); ?>
                    </span>
                <?php endif; ?>
            <?php endforeach; ?>
        </div>
    <?php endif;
});

// Restrict BuddyPress features based on subscription
add_filter('bp_user_can_create_groups', function($can_create) {
    $customer = surecart_get_customer(get_current_user_id());

    // Only premium members can create groups
    if (!$customer || !$customer->has_product('premium-membership')) {
        return false;
    }

    return $can_create;
});
```

## Checkout Customization

### Custom Checkout Fields

```php
// Add custom fields to checkout
add_filter('surecart_checkout_fields', function($fields) {
    $fields['company_name'] = array(
        'type' => 'text',
        'label' => 'Company Name',
        'required' => false,
        'priority' => 25
    );

    $fields['referral_source'] = array(
        'type' => 'select',
        'label' => 'How did you hear about us?',
        'options' => array(
            'search' => 'Search Engine',
            'social' => 'Social Media',
            'friend' => 'Friend',
            'other' => 'Other'
        ),
        'required' => true,
        'priority' => 100
    );

    return $fields;
});
```

### Checkout Page Styling

```css
/* Reign + SureCart checkout styling */
.sc-checkout-form {
    max-width: 600px;
    margin: 0 auto;
    padding: 30px;
    background: #fff;
    border-radius: 10px;
    box-shadow: 0 2px 20px rgba(0,0,0,0.1);
}

.sc-checkout-form .form-group {
    margin-bottom: 20px;
}

.sc-checkout-form input,
.sc-checkout-form select {
    width: 100%;
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-size: 16px;
}

.sc-checkout-form .payment-methods {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 10px;
    margin: 20px 0;
}

.sc-checkout-form .order-summary {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
    margin-bottom: 20px;
}

.sc-checkout-form .btn-purchase {
    width: 100%;
    padding: 15px;
    background: var(--reign-primary-color);
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 18px;
    cursor: pointer;
}
```

### One-Click Upsells

```php
// Add upsell after purchase
add_action('surecart_after_purchase', function($order) {
    $product_id = $order->product_id;

    // Show upsell based on purchase
    $upsells = array(
        'basic-plan' => 'premium-upgrade',
        'course-1' => 'course-bundle'
    );

    if (isset($upsells[$product_id])): ?>
        <div class="sc-upsell-offer">
            <h2>Special Offer!</h2>
            <p>Upgrade your purchase and save 30%</p>
            <button data-sc-product="<?php echo $upsells[$product_id]; ?>" class="btn-upsell">
                Upgrade Now
            </button>
        </div>
    <?php endif;
});
```

## Customer Portal

### Account Dashboard

```php
// Enhance customer dashboard
add_action('surecart_account_dashboard', function() {
    $customer = surecart_get_current_customer();
    ?>
    <div class="reign-sc-dashboard">
        <div class="dashboard-stats">
            <div class="stat-card">
                <h4>Total Spent</h4>
                <p><?php echo sc_format_price($customer->lifetime_value); ?></p>
            </div>
            <div class="stat-card">
                <h4>Active Subscriptions</h4>
                <p><?php echo count($customer->active_subscriptions); ?></p>
            </div>
            <div class="stat-card">
                <h4>Downloads Available</h4>
                <p><?php echo count($customer->downloads); ?></p>
            </div>
        </div>

        <!-- Quick Actions -->
        <div class="dashboard-actions">
            <a href="/account/subscriptions" class="action-card">
                <i class="fas fa-credit-card"></i>
                <span>Manage Subscriptions</span>
            </a>
            <a href="/account/downloads" class="action-card">
                <i class="fas fa-download"></i>
                <span>My Downloads</span>
            </a>
            <a href="/account/invoices" class="action-card">
                <i class="fas fa-file-invoice"></i>
                <span>Invoices</span>
            </a>
            <a href="/account/payment-methods" class="action-card">
                <i class="fas fa-wallet"></i>
                <span>Payment Methods</span>
            </a>
        </div>
    </div>
    <?php
});
```

### Subscription Management

```php
// Custom subscription cards
function reign_subscription_card($subscription) {
    ?>
    <div class="subscription-card">
        <div class="subscription-header">
            <h3><?php echo esc_html($subscription->product_name); ?></h3>
            <span class="status <?php echo esc_attr($subscription->status); ?>">
                <?php echo ucfirst($subscription->status); ?>
            </span>
        </div>

        <div class="subscription-details">
            <p>Next payment: <?php echo date('M d, Y', strtotime($subscription->next_payment_date)); ?></p>
            <p>Amount: <?php echo sc_format_price($subscription->amount); ?>/<?php echo $subscription->period; ?></p>
        </div>

        <div class="subscription-actions">
            <?php if ($subscription->status === 'active'): ?>
                <button class="btn-pause" data-subscription="<?php echo $subscription->id; ?>">Pause</button>
                <button class="btn-cancel" data-subscription="<?php echo $subscription->id; ?>">Cancel</button>
            <?php elseif ($subscription->status === 'paused'): ?>
                <button class="btn-resume" data-subscription="<?php echo $subscription->id; ?>">Resume</button>
            <?php endif; ?>
            <a href="/account/subscription/<?php echo $subscription->id; ?>" class="btn-manage">Manage</a>
        </div>
    </div>
    <?php
}
```

## Abandoned Cart Recovery

### Email Template

```php
// Custom abandoned cart email
add_filter('surecart_abandoned_cart_email', function($email, $cart) {
    $products = $cart->get_products();

    ob_start();
    ?>
    <div style="font-family: Arial, sans-serif; max-width: 600px; margin: 0 auto;">
        <h2>You left something behind!</h2>
        <p>Hi <?php echo $cart->customer_name; ?>,</p>
        <p>You have items waiting in your cart:</p>

        <table style="width: 100%; border-collapse: collapse;">
            <?php foreach ($products as $product): ?>
                <tr>
                    <td style="padding: 10px; border-bottom: 1px solid #eee;">
                        <?php if ($product->image): ?>
                            <img src="<?php echo $product->image; ?>" style="width: 80px;">
                        <?php endif; ?>
                    </td>
                    <td style="padding: 10px;">
                        <h4><?php echo $product->name; ?></h4>
                        <p><?php echo sc_format_price($product->price); ?></p>
                    </td>
                </tr>
            <?php endforeach; ?>
        </table>

        <div style="text-align: center; margin: 30px 0;">
            <a href="<?php echo $cart->recovery_url; ?>"
               style="background: #4CAF50; color: white; padding: 15px 30px; text-decoration: none; border-radius: 5px;">
                Complete Your Purchase
            </a>
        </div>

        <!-- Add incentive -->
        <div style="background: #f0f0f0; padding: 20px; border-radius: 5px;">
            <h3>🎁 Special Offer</h3>
            <p>Complete your purchase in the next 24 hours and get 10% off!</p>
            <p>Use code: <strong>COMEBACK10</strong></p>
        </div>
    </div>
    <?php
    return ob_get_clean();
}, 10, 2);
```

## Affiliate Integration

### Affiliate Dashboard

```php
// Add to BuddyPress profile
add_action('bp_setup_nav', function() {
    if (!surecart_is_affiliate_enabled()) return;

    bp_core_new_nav_item(array(
        'name' => 'Affiliate Program',
        'slug' => 'affiliate',
        'screen_function' => 'reign_affiliate_screen',
        'position' => 100,
        'default_subnav_slug' => 'dashboard'
    ));
});

function reign_affiliate_screen() {
    add_action('bp_template_content', 'reign_affiliate_content');
    bp_core_load_template('members/single/plugins');
}

function reign_affiliate_content() {
    $user_id = bp_displayed_user_id();
    $affiliate = surecart_get_affiliate($user_id);

    if (!$affiliate): ?>
        <div class="affiliate-signup">
            <h2>Join Our Affiliate Program</h2>
            <p>Earn 30% commission on every sale!</p>
            <button class="btn-join-affiliate">Become an Affiliate</button>
        </div>
    <?php else: ?>
        <div class="affiliate-dashboard">
            <div class="affiliate-stats">
                <div class="stat">
                    <h4>Total Earnings</h4>
                    <p><?php echo sc_format_price($affiliate->total_earnings); ?></p>
                </div>
                <div class="stat">
                    <h4>Pending Commission</h4>
                    <p><?php echo sc_format_price($affiliate->pending_commission); ?></p>
                </div>
                <div class="stat">
                    <h4>Total Referrals</h4>
                    <p><?php echo $affiliate->total_referrals; ?></p>
                </div>
            </div>

            <div class="affiliate-link">
                <h3>Your Referral Link</h3>
                <input type="text" value="<?php echo esc_url($affiliate->referral_link); ?>" readonly>
                <button class="copy-link">Copy Link</button>
            </div>

            <div class="affiliate-materials">
                <h3>Marketing Materials</h3>
                <!-- Banners, email templates, etc. -->
            </div>
        </div>
    <?php endif;
}
```

## Webhooks & Automation

### Webhook Handlers

```php
// Handle SureCart webhooks
add_action('rest_api_init', function() {
    register_rest_route('reign/v1', '/surecart-webhook', array(
        'methods' => 'POST',
        'callback' => 'handle_surecart_webhook',
        'permission_callback' => '__return_true'
    ));
});

function handle_surecart_webhook($request) {
    $event = $request->get_param('event');
    $data = $request->get_param('data');

    switch ($event) {
        case 'order.created':
            do_action('reign_surecart_order_created', $data);
            break;

        case 'subscription.created':
            do_action('reign_surecart_subscription_created', $data);
            break;

        case 'subscription.cancelled':
            do_action('reign_surecart_subscription_cancelled', $data);
            break;

        case 'customer.created':
            do_action('reign_surecart_customer_created', $data);
            break;
    }

    return new WP_REST_Response('Webhook received', 200);
}
```

### Automation Examples

```php
// Grant BuddyPress membership level
add_action('reign_surecart_order_created', function($order) {
    if ($order->product_id === 'premium-membership') {
        $user_id = email_exists($order->customer_email);

        if ($user_id) {
            // Add to premium group
            groups_join_group(PREMIUM_GROUP_ID, $user_id);

            // Update user meta
            update_user_meta($user_id, 'membership_level', 'premium');
            update_user_meta($user_id, 'membership_expires', strtotime('+1 year'));

            // Grant capabilities
            $user = new WP_User($user_id);
            $user->add_cap('premium_member');
        }
    }
});

// Send welcome course email
add_action('reign_surecart_order_created', function($order) {
    $course_products = array('course-beginner', 'course-advanced', 'course-bundle');

    if (in_array($order->product_id, $course_products)) {
        // Get course access details
        $course_data = get_course_by_product($order->product_id);

        // Send welcome email
        wp_mail(
            $order->customer_email,
            'Welcome to ' . $course_data->title,
            reign_get_course_welcome_email($course_data, $order),
            array('Content-Type: text/html; charset=UTF-8')
        );

        // Enroll in LearnDash course
        if (function_exists('ld_update_course_access')) {
            $user_id = email_exists($order->customer_email);
            ld_update_course_access($user_id, $course_data->learndash_id);
        }
    }
});
```

## Reporting & Analytics

### Sales Dashboard

```php
// Add sales stats to admin dashboard
add_action('wp_dashboard_setup', function() {
    wp_add_dashboard_widget(
        'reign_surecart_stats',
        'SureCart Sales Overview',
        'reign_surecart_dashboard_widget'
    );
});

function reign_surecart_dashboard_widget() {
    $stats = surecart_get_stats(array(
        'period' => 'last_30_days'
    ));
    ?>
    <div class="surecart-stats">
        <div class="stat-row">
            <span>Total Revenue:</span>
            <strong><?php echo sc_format_price($stats->revenue); ?></strong>
        </div>
        <div class="stat-row">
            <span>Total Orders:</span>
            <strong><?php echo $stats->order_count; ?></strong>
        </div>
        <div class="stat-row">
            <span>Active Subscriptions:</span>
            <strong><?php echo $stats->active_subscriptions; ?></strong>
        </div>
        <div class="stat-row">
            <span>Conversion Rate:</span>
            <strong><?php echo $stats->conversion_rate; ?>%</strong>
        </div>

        <canvas id="surecart-sales-chart"></canvas>

        <script>
        // Chart.js implementation
        new Chart(document.getElementById('surecart-sales-chart'), {
            type: 'line',
            data: {
                labels: <?php echo json_encode($stats->chart_labels); ?>,
                datasets: [{
                    label: 'Sales',
                    data: <?php echo json_encode($stats->chart_data); ?>,
                    borderColor: 'rgb(75, 192, 192)',
                    tension: 0.1
                }]
            }
        });
        </script>
    </div>
    <?php
}
```

## Troubleshooting

### Common Issues

#### Products Not Displaying

```php
// Debug product display
add_action('init', function() {
    if (isset($_GET['debug_surecart'])) {
        $products = surecart_get_products();

        echo '<pre>';
        print_r($products);
        echo '</pre>';

        // Check API connection
        $api_status = surecart_test_api_connection();
        echo 'API Status: ' . ($api_status ? 'Connected' : 'Failed');
    }
});
```

#### Checkout Errors

```php
// Log checkout errors
add_action('surecart_checkout_error', function($error) {
    error_log('SureCart Checkout Error: ' . $error->getMessage());

    // Display user-friendly message
    wp_die('There was an error processing your order. Please try again or contact support.');
});
```

#### Webhook Issues

```php
// Verify webhook signature
function verify_surecart_webhook($request) {
    $signature = $request->get_header('X-SureCart-Signature');
    $payload = $request->get_body();

    $expected = hash_hmac('sha256', $payload, SURECART_WEBHOOK_SECRET);

    return hash_equals($expected, $signature);
}
```

## Performance Optimization

### Caching

```php
// Cache product data
function reign_get_surecart_products_cached() {
    $cache_key = 'reign_surecart_products';
    $products = get_transient($cache_key);

    if (false === $products) {
        $products = surecart_get_products();
        set_transient($cache_key, $products, HOUR_IN_SECONDS);
    }

    return $products;
}

// Clear cache on product update
add_action('surecart_product_updated', function() {
    delete_transient('reign_surecart_products');
});
```

### Lazy Loading

```javascript
// Lazy load product images
document.addEventListener('DOMContentLoaded', function() {
    const productImages = document.querySelectorAll('.sc-product-image[data-src]');

    const imageObserver = new IntersectionObserver(function(entries, observer) {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const img = entry.target;
                img.src = img.dataset.src;
                img.classList.add('loaded');
                observer.unobserve(img);
            }
        });
    });

    productImages.forEach(img => imageObserver.observe(img));
});
```

---

*For more e-commerce features, see the WooCommerce Integration guide.*