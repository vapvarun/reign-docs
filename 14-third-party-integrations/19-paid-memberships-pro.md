# Paid Memberships Pro Integration

## What is Paid Memberships Pro?

Paid Memberships Pro (PMPro) is a comprehensive membership management plugin for WordPress that allows you to create subscription-based websites. It provides flexible membership levels, payment gateway integration, content restriction, and member management tools.

## What Reign Theme Offers

Reign Theme provides deep PMPro integration with:

### 1. **Custom Pricing Display**
- Enhanced price formatting with clear separation of initial and recurring payments
- Responsive pricing cards with modern design
- Custom CSS classes for styling flexibility
- Intuitive billing cycle display

### 2. **BuddyPress Integration**
- Member level badges in profiles
- Restricted group access based on membership
- Activity stream filtering by membership level
- Private messaging restrictions

### 3. **Customizer Options**
Located at **Appearance > Customize > Plugins Support > Paid Memberships Pro**:

```
PMPro Settings:
├── Pricing Table Style
├── Membership Badge Display
├── Restriction Message Styling
└── Account Page Layout
```

## Configuration Guide

### Step 1: Install and Configure PMPro

1. Install Paid Memberships Pro from WordPress repository
2. Navigate to **Memberships > Settings**
3. Configure essential settings:
   - Payment Gateway (Stripe, PayPal, etc.)
   - Email Settings
   - Page Settings

### Step 2: Create Membership Levels

Navigate to **Memberships > Membership Levels**:

```
Example Level Setup:
├── Basic ($9/month)
├── Premium ($19/month)
└── VIP ($49/month)
```

### Step 3: Configure Reign Theme Settings

The theme automatically enhances PMPro display:

```php
// Automatic price formatting applied by theme
// Located at: inc/plugins-support/class-rtm-pmpro-customization.php

class RTM_PMPRO_Customization {
    // Custom price text formatting
    public function rtm_pmpro_level_cost_text() {
        // Enhanced price display logic
    }
}
```

## Pricing Display Features

### Enhanced Price Formatting

The theme transforms standard PMPro pricing into beautiful displays:

**Before (Standard PMPro):**
```
"The price for membership is $19.00 now and then $19.00 per Month."
```

**After (With Reign Theme):**
```html
<div class="rtm-pmpro-now-price">$19.00</div>
<div class="rtm-pmpro-recurring-price">$19.00 per Month</div>
```

### Pricing Table Styles

```css
/* Custom pricing classes applied by theme */
.rtm-pmpro-now-price {
    /* Initial payment styling */
    font-size: 2em;
    font-weight: bold;
}

.rtm-pmpro-recurring-price {
    /* Recurring payment styling */
    color: var(--reign-secondary-color);
    margin-top: 10px;
}
```

### Billing Cycle Display

The theme intelligently formats various billing scenarios:

| Scenario | Display Format |
|----------|---------------|
| One-time payment | **$99.00** (Lifetime) |
| Monthly recurring | **$19.00** per Month |
| Annual recurring | **$199.00** per Year |
| Trial period | **Free for 7 days** then $19/month |
| Limited billing | **$19.00** per Month for 12 more Months |

## Member Account Pages

### Enhanced Account Dashboard

The theme provides styled layouts for:

1. **Membership Status**: Clear current level display
2. **Billing Information**: Organized payment history
3. **Update Options**: Easy upgrade/downgrade interface
4. **Invoices**: Downloadable invoice history

### Profile Integration

Members see enhanced profile features:

```
Profile Enhancements:
├── Membership Badge
├── Join Date
├── Expiration Status
└── Exclusive Content Access
```

## Content Restriction

### Restriction Messages

Customizable restriction notices:

```php
// Custom restriction message
add_filter( 'pmpro_non_member_text_filter', function( $text ) {
    return '<div class="reign-restricted-content">
        <h3>Premium Content</h3>
        <p>This content requires a membership.</p>
        <a href="/membership-levels" class="button">View Plans</a>
    </div>';
});
```

### Partial Content Display

Show teasers for non-members:

```php
// In your template
if ( pmpro_hasMembershipLevel() ) {
    // Full content
} else {
    // Teaser content
    echo '<div class="content-preview">...</div>';
}
```

## BuddyPress Features

### Member Directory Integration

Filter members by membership level:

```php
// Automatic integration with member loops
// Shows membership badges in directory
```

### Group Access Control

Restrict groups to specific membership levels:

1. Install **PMPro BuddyPress Add-on**
2. Configure group restrictions
3. Theme automatically styles restriction notices

### Activity Stream Enhancement

- Membership level indicators
- Exclusive activity posts
- Premium content highlights

## Customization Options

### Theme Customizer Settings

Navigate to **Appearance > Customize > Plugins Support > PMPro**:

| Setting | Description | Options |
|---------|-------------|---------|
| Price Display Style | How prices are formatted | Modern / Classic |
| Badge Position | Where badges appear | Before Name / After Name |
| Restriction Style | How restricted content appears | Blur / Hide / Message |
| Account Page Layout | Member account page style | Tabs / Accordion |

### Custom CSS Classes

```css
/* Membership Levels */
.pmpro-level-1 { /* Basic */ }
.pmpro-level-2 { /* Premium */ }
.pmpro-level-3 { /* VIP */ }

/* Pricing Elements */
.rtm-pmpro-pricing-card { }
.rtm-pmpro-featured { }
.rtm-pmpro-discount { }

/* Member Badges */
.reign-member-badge { }
.reign-member-badge-vip { }
```

## Payment Gateway Styling

### Checkout Page Enhancement

The theme provides optimized checkout layouts:

1. **Single Column**: Mobile-friendly
2. **Two Column**: Desktop optimized
3. **Progressive**: Step-by-step process

### Supported Gateways

Fully styled support for:
- Stripe
- PayPal
- Authorize.net
- Braintree
- 2Checkout

## Advanced Features

### Hooks and Filters

```php
// Customize price display
add_filter( 'reign_pmpro_price_format', function( $format, $level ) {
    // Custom formatting logic
    return $format;
}, 10, 2 );

// Add custom profile fields
add_action( 'reign_pmpro_profile_fields', function( $user_id ) {
    // Display custom member data
});
```

### Conditional Content

```php
// Show content based on level
if ( pmpro_hasMembershipLevel( array( 1, 2 ) ) ) {
    // Premium content
}

// Check specific capabilities
if ( current_user_can( 'pmpro_content' ) ) {
    // Restricted content
}
```

## Email Templates

### Enhanced Email Designs

The theme includes styled email templates:

1. **Welcome Emails**: Branded design
2. **Renewal Notices**: Clear CTAs
3. **Expiration Warnings**: Urgent styling
4. **Receipt Emails**: Professional invoices

## Troubleshooting

### Common Issues

#### Pricing Not Displaying Correctly
**Solution**:
1. Clear theme cache
2. Check PMPro version (2.0+ required)
3. Verify Customizer settings

#### Member Badges Not Showing
**Solution**:
1. Enable in **Customize > PMPro > Show Badges**
2. Check BuddyPress integration
3. Verify member levels

#### Checkout Page Styling Issues
**Solution**:
1. Disable conflicting plugins
2. Check payment gateway settings
3. Use theme's default checkout page

### Debug Mode

Enable debugging:

```php
// In wp-config.php
define( 'PMPRO_DEBUG', true );
define( 'PMPRO_DEBUG_EMAIL', true );
```

## Best Practices

### Membership Structure

1. **Clear Level Names**: Basic, Premium, VIP
2. **Logical Pricing**: Progressive value
3. **Trial Periods**: Encourage sign-ups
4. **Grace Periods**: Retain members

### Content Strategy

1. **Gradual Restriction**: Don't lock everything
2. **Value Communication**: Show what's included
3. **Free Content**: Maintain public value
4. **Exclusive Perks**: Member-only benefits

## Integration with Other Plugins

### Compatible Add-ons

- **PMPro BuddyPress**: Full integration
- **PMPro WooCommerce**: Member discounts
- **PMPro bbPress**: Forum restrictions
- **PMPro Events**: Member-only events

### Reign Addons Support

Works seamlessly with:
- BuddyPress Maps
- BuddyPress Polls
- Live Reactions
- User Stories

## Performance Optimization

### Caching Considerations

```php
// Exclude member pages from cache
$excluded_pages = array(
    '/membership-account/',
    '/membership-checkout/',
    '/membership-confirmation/'
);
```

### Database Optimization

- Regular membership audit
- Clean expired members
- Optimize order tables

## Developer Reference

### File Locations

```
Theme Files:
├── inc/plugins-support/
│   └── class-rtm-pmpro-customization.php
├── assets/css/
│   └── pmpro-styles.css
└── template-parts/
    └── pmpro/ (override templates)
```

### Template Overrides

To customize PMPro templates:

1. Copy from: `plugins/paid-memberships-pro/pages/`
2. Paste to: `reign-theme/paid-memberships-pro/`
3. Modify as needed

### Custom Membership Levels

```php
// Add custom level features
add_action( 'pmpro_membership_level_before_content', function( $level ) {
    if ( $level->id == 3 ) { // VIP level
        echo '<span class="vip-badge">Most Popular</span>';
    }
});
```

## Support Resources

- **PMPro Documentation**: [paidmembershipspro.com/docs](https://www.paidmembershipspro.com/documentation/)
- **Reign Theme Support**: [wbcomdesigns.com/support](https://wbcomdesigns.com/support)
- **Community Forums**: Active community help
- **Video Tutorials**: Available in member area

## Conclusion

The Reign Theme's Paid Memberships Pro integration creates a professional membership site with enhanced styling, seamless BuddyPress integration, and extensive customization options. The combination delivers a complete membership solution with beautiful design and powerful functionality for monetizing your community.