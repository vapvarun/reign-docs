# Social Login Integration Guide

## Overview

Reign Theme supports multiple social login providers, allowing users to register and login using their existing social media accounts. This reduces friction in the registration process and improves user engagement.

## Supported Providers

### Primary Platforms
1. **Facebook** - Most popular social login
2. **Google** - Gmail and Google Workspace accounts
3. **Twitter/X** - Twitter OAuth integration
4. **LinkedIn** - Professional network login
5. **Apple ID** - Sign in with Apple
6. **Microsoft** - Outlook and Office 365 accounts

### Additional Platforms
- Instagram
- Discord
- Twitch
- GitHub
- WordPress.com
- Amazon
- PayPal

## Plugin Integration

### Recommended Plugins

#### 1. Super Socializer (Free)
**Best for:** Basic social login needs
```
Features:
- 15+ social networks
- Social sharing
- Social commenting
- Free version available
```

#### 2. Nextend Social Login (Free/Pro)
**Best for:** Easy setup and customization
```
Features:
- Major social networks
- Button customization
- Statistics
- WooCommerce support
```

#### 3. Social Login by WPWeb
**Best for:** Advanced features
```
Features:
- 40+ providers
- Custom providers
- Two-factor auth
- Social linking
```

#### 4. LoginRadius
**Best for:** Enterprise solutions
```
Features:
- 40+ providers
- Single sign-on
- Social analytics
- Customer insights
```

## Facebook Login Setup

### Step 1: Create Facebook App

1. Go to [developers.facebook.com](https://developers.facebook.com)
2. Click "My Apps" → "Create App"
3. Choose "Consumer" type
4. Fill app details:
```
App Name: Your Site Name
App Contact Email: your@email.com
App Purpose: Authentication
```

### Step 2: Configure Facebook Login

1. Add Facebook Login product
2. Settings → Basic:
```
App ID: [Generated automatically]
App Secret: [Generated automatically]
App Domains: yourdomain.com
```

3. Facebook Login → Settings:
```
Valid OAuth Redirect URIs:
- https://yourdomain.com/wp-login.php
- https://yourdomain.com/wp-admin/admin-ajax.php
- https://yourdomain.com/?loginSocial=facebook
```

### Step 3: WordPress Configuration

```php
// In functions.php or plugin settings
define('FACEBOOK_APP_ID', 'your_app_id');
define('FACEBOOK_APP_SECRET', 'your_app_secret');
```

**Permissions Required:**
- email
- public_profile
- user_friends (optional)

## Google Sign-In Setup

### Step 1: Google Cloud Console

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create new project or select existing
3. Enable Google+ API

### Step 2: Create OAuth Credentials

1. APIs & Services → Credentials
2. Create Credentials → OAuth Client ID
3. Configure consent screen:
```
Application Type: Web application
Name: Your Site Login
Authorized JavaScript origins: https://yourdomain.com
Authorized redirect URIs:
- https://yourdomain.com/wp-login.php
- https://yourdomain.com/?loginSocial=google
```

### Step 3: Implementation

```php
// Google OAuth settings
$google_config = array(
    'client_id' => 'your_client_id.apps.googleusercontent.com',
    'client_secret' => 'your_client_secret',
    'redirect_uri' => site_url('?loginSocial=google'),
    'scope' => 'email profile'
);
```

## Twitter/X Login Setup

### Step 1: Twitter Developer Portal

1. Visit [developer.twitter.com](https://developer.twitter.com)
2. Create new app
3. User authentication settings:
```
App permissions: Read
Type of App: Web App
Callback URLs: https://yourdomain.com/?loginSocial=twitter
Website URL: https://yourdomain.com
```

### Step 2: Get API Keys

```
API Key: [Generated]
API Secret Key: [Generated]
Bearer Token: [Generated]
```

### Step 3: Configure in WordPress

```php
// Twitter OAuth settings
define('TWITTER_CONSUMER_KEY', 'your_api_key');
define('TWITTER_CONSUMER_SECRET', 'your_api_secret');
```

## LinkedIn Login Setup

### Step 1: LinkedIn Developer Portal

1. Go to [linkedin.com/developers](https://www.linkedin.com/developers)
2. Create app:
```
App Name: Your Site
Company: Your Company
Privacy Policy URL: Required
Logo: Required (300x300)
```

### Step 2: Auth Settings

Products → Sign In with LinkedIn:
```
Redirect URLs:
- https://yourdomain.com/wp-login.php
- https://yourdomain.com/?loginSocial=linkedin
```

### Step 3: Scopes Required

```
r_liteprofile - Basic profile
r_emailaddress - Email address
```

## Apple ID Setup

### Requirements

1. Apple Developer Account ($99/year)
2. HTTPS required
3. Privacy policy required

### Step 1: Create App ID

1. Certificates, Identifiers & Profiles
2. Create new App ID
3. Enable "Sign In with Apple"

### Step 2: Create Service ID

```
Description: Your Site Login
Identifier: com.yourcompany.webapp
Sign In with Apple: Enable
```

### Step 3: Configure Domains

```
Domain: yourdomain.com
Return URLs: https://yourdomain.com/?loginSocial=apple
```

## Plugin Configuration

### Using Nextend Social Login

#### Installation
```bash
1. Plugins → Add New
2. Search "Nextend Social Login"
3. Install and Activate
4. Settings → Nextend Social Login
```

#### Provider Setup
```php
// Each provider configuration
Facebook:
- App ID: [Your App ID]
- App Secret: [Your Secret]
- Redirect URL: Auto-generated

Google:
- Client ID: [Your Client ID]
- Client Secret: [Your Secret]
- Redirect URL: Auto-generated
```

### Using Super Socializer

#### Basic Configuration
```
1. Super Socializer → Basic Configuration
2. Enable Social Login: Yes
3. Select Providers: Check desired
4. Enter API credentials for each
```

#### Advanced Settings
```php
// Customize login behavior
add_filter('heateor_ss_login_user_roles', function($roles) {
    $roles[] = 'subscriber'; // Default role
    return $roles;
});
```

## Display Options

### Login Page Integration

#### Above Login Form
```php
add_action('login_form', 'reign_social_login_buttons');
function reign_social_login_buttons() {
    echo do_shortcode('[nextend_social_login]');
}
```

#### Below Login Form
```php
add_action('login_footer', 'reign_social_login_buttons');
```

### Registration Page

```php
add_action('register_form', function() {
    ?>
    <div class="social-login-register">
        <h3>Or register with:</h3>
        <?php echo do_shortcode('[social_login_buttons]'); ?>
    </div>
    <?php
});
```

### Popup Integration

```javascript
// Add to popup forms
jQuery(document).ready(function($) {
    $('.reign-login-popup-form').append(
        '<div class="social-login-popup">' +
        '<?php echo do_shortcode("[social_login]"); ?>' +
        '</div>'
    );
});
```

### Shortcodes

```
[nextend_social_login] - Nextend buttons
[super_socializer_login] - Super Socializer
[loginradius_login] - LoginRadius
[oa_social_login] - OneAll
```

## Button Customization

### CSS Styling

```css
/* Social login container */
.social-login-container {
    margin: 20px 0;
    text-align: center;
}

/* Individual buttons */
.social-login-btn {
    display: inline-block;
    margin: 5px;
    padding: 10px 20px;
    border-radius: 5px;
    text-decoration: none;
    transition: all 0.3s;
}

/* Facebook button */
.social-login-facebook {
    background: #1877f2;
    color: white;
}

.social-login-facebook:hover {
    background: #166fe5;
}

/* Google button */
.social-login-google {
    background: #fff;
    color: #3c4043;
    border: 1px solid #dadce0;
}

.social-login-google:hover {
    background: #f8f9fa;
}

/* Twitter button */
.social-login-twitter {
    background: #1da1f2;
    color: white;
}

/* LinkedIn button */
.social-login-linkedin {
    background: #0077b5;
    color: white;
}
```

### Button Layout Options

#### Horizontal Layout
```css
.social-login-buttons {
    display: flex;
    justify-content: center;
    gap: 10px;
}
```

#### Vertical Layout
```css
.social-login-buttons-vertical {
    display: flex;
    flex-direction: column;
    max-width: 300px;
    margin: 0 auto;
}
```

#### Grid Layout
```css
.social-login-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
}
```

## User Data Mapping

### Profile Field Mapping

```php
// Map social data to WordPress user
add_filter('social_login_user_data', function($user_data, $provider) {
    switch($provider) {
        case 'facebook':
            $user_data['first_name'] = $social_data['first_name'];
            $user_data['last_name'] = $social_data['last_name'];
            $user_data['user_url'] = $social_data['link'];
            break;

        case 'google':
            $user_data['first_name'] = $social_data['given_name'];
            $user_data['last_name'] = $social_data['family_name'];
            break;
    }
    return $user_data;
}, 10, 2);
```

### BuddyPress Integration

```php
// Map to BuddyPress xProfile fields
add_action('social_login_user_created', function($user_id, $social_data) {
    if (function_exists('xprofile_set_field_data')) {
        xprofile_set_field_data('Facebook URL', $user_id, $social_data['facebook_url']);
        xprofile_set_field_data('Twitter Handle', $user_id, $social_data['twitter_handle']);
    }
}, 10, 2);
```

## Account Linking

### Link Existing Accounts

```php
// Allow users to link social accounts
add_action('show_user_profile', 'reign_social_account_linking');
add_action('edit_user_profile', 'reign_social_account_linking');

function reign_social_account_linking($user) {
    ?>
    <h2>Social Account Connections</h2>
    <table class="form-table">
        <tr>
            <th>Facebook</th>
            <td>
                <?php if (get_user_meta($user->ID, 'facebook_id', true)): ?>
                    Connected <a href="?disconnect=facebook">Disconnect</a>
                <?php else: ?>
                    <a href="?connect=facebook">Connect</a>
                <?php endif; ?>
            </td>
        </tr>
    </table>
    <?php
}
```

### Unlink Accounts

```php
// Handle disconnection
add_action('init', function() {
    if (isset($_GET['disconnect'])) {
        $provider = sanitize_text_field($_GET['disconnect']);
        delete_user_meta(get_current_user_id(), $provider . '_id');
        wp_redirect(remove_query_arg('disconnect'));
        exit;
    }
});
```

## Security Considerations

### Best Practices

1. **SSL/HTTPS Required**
```php
// Force SSL for social login
if (!is_ssl() && isset($_GET['loginSocial'])) {
    wp_redirect(str_replace('http:', 'https:', get_permalink()));
    exit;
}
```

2. **Nonce Verification**
```php
// Verify social login requests
add_action('social_login_before_auth', function() {
    if (!wp_verify_nonce($_GET['_wpnonce'], 'social-login')) {
        wp_die('Security check failed');
    }
});
```

3. **Email Verification**
```php
// Require email verification for social signups
add_filter('social_login_require_email_verification', '__return_true');
```

4. **Rate Limiting**
```php
// Limit social login attempts
$attempts = get_transient('social_login_attempts_' . $_SERVER['REMOTE_ADDR']);
if ($attempts > 10) {
    wp_die('Too many attempts. Please try again later.');
}
```

## GDPR Compliance

### Consent Management

```php
// Add consent checkbox
add_action('social_login_before_button', function() {
    ?>
    <label>
        <input type="checkbox" name="gdpr_consent" required>
        I agree to the privacy policy and terms of service
    </label>
    <?php
});
```

### Data Storage

```php
// Minimal data storage
add_filter('social_login_store_data', function($data) {
    // Store only essential data
    return array(
        'email' => $data['email'],
        'name' => $data['name'],
        'provider' => $data['provider']
    );
});
```

## Troubleshooting

### Common Issues

#### "App Not Set Up" Error
**Solution:**
1. Verify app is in production mode
2. Check all required fields filled
3. Ensure privacy policy URL valid

#### Redirect URI Mismatch
**Solution:**
1. Exact match required (https vs http)
2. Include trailing slash if needed
3. Check for www vs non-www

#### Email Not Provided
**Solution:**
```php
// Request email permission
add_filter('social_login_facebook_scope', function($scope) {
    return $scope . ',email';
});
```

#### User Already Exists
**Solution:**
```php
// Link to existing user by email
add_filter('social_login_link_existing_user', '__return_true');
```

### Debug Mode

```php
// Enable debug logging
define('SOCIAL_LOGIN_DEBUG', true);

// Log social login events
add_action('social_login_before_auth', function($provider) {
    if (SOCIAL_LOGIN_DEBUG) {
        error_log('Social login attempt: ' . $provider);
    }
});
```

## Analytics Tracking

### Google Analytics

```javascript
// Track social login events
gtag('event', 'login', {
    method: 'facebook'
});
```

### Custom Tracking

```php
// Track in database
add_action('social_login_success', function($user_id, $provider) {
    update_user_meta($user_id, 'signup_method', $provider);
    update_user_meta($user_id, 'signup_date', current_time('mysql'));
});
```

---

*For popup integration, see the Popup Login & Register guide.*