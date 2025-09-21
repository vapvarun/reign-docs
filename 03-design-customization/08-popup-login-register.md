# Popup Login & Register Configuration

## Overview

Reign Theme includes built-in popup functionality for login and registration, eliminating the need for additional plugins. This creates a seamless user experience without page redirects.

## Enabling Popup Login

### Basic Setup

**Location:** `Customizer → General → Login Popup`

**Settings:**
```
Enable Login Popup: ON
Enable Register Popup: ON
Popup Trigger: Automatic
Animation Style: Fade In
Modal Background: Dark Overlay
Close on Escape: Yes
```

### Activation Methods

#### Method 1: Menu Integration
1. Go to `Appearance → Menus`
2. Add Custom Links:
   - Login: `#reign-login-popup`
   - Register: `#reign-register-popup`
3. Save menu

#### Method 2: Button Classes
```html
<!-- Login Button -->
<a href="#" class="reign-login-popup-link">Login</a>

<!-- Register Button -->
<a href="#" class="reign-register-popup-link">Sign Up</a>
```

#### Method 3: Automatic Redirect
```php
// In functions.php
add_filter('reign_login_redirect_to_popup', '__return_true');
```

## Popup Styles

### Available Styles

#### 1. Classic Modal
```css
/* Default centered modal */
.reign-login-modal-classic {
    width: 400px;
    max-width: 90%;
    padding: 40px;
    background: #ffffff;
    border-radius: 8px;
}
```

#### 2. Slide Panel
```css
/* Slides from right */
.reign-login-modal-slide {
    width: 400px;
    height: 100%;
    position: fixed;
    right: 0;
    transform: translateX(100%);
}
```

#### 3. Full Screen
```css
/* Covers entire viewport */
.reign-login-modal-fullscreen {
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
}
```

#### 4. Minimal
```css
/* No background, minimal design */
.reign-login-modal-minimal {
    background: transparent;
    box-shadow: none;
    border: 1px solid rgba(0,0,0,0.1);
}
```

## Form Configuration

### Login Form Elements

**Standard Fields:**
- Username/Email field
- Password field
- Remember Me checkbox
- Lost Password link
- Submit button

**Custom Fields:**
```php
// Add custom field to login popup
add_action('reign_login_popup_form', function() {
    ?>
    <div class="custom-field">
        <label>Security Code</label>
        <input type="text" name="security_code" />
    </div>
    <?php
});
```

### Registration Form Elements

**Default Fields:**
- Username
- Email
- Password
- Confirm Password
- Terms acceptance
- Submit button

**BuddyPress Fields:**
- Automatically includes profile fields
- xProfile field groups
- Required fields validation

## Social Login Integration

### Enable Social Login in Popup

**Supported Providers:**
- Facebook Login
- Google Sign-In
- Twitter/X
- LinkedIn
- Apple ID
- Microsoft

### Setup Social Login

#### Facebook Login
```php
// In Customizer or functions.php
$social_login_settings = array(
    'facebook_app_id' => 'YOUR_APP_ID',
    'facebook_app_secret' => 'YOUR_SECRET',
    'facebook_scope' => 'email,public_profile'
);
```

#### Google Sign-In
```php
$google_settings = array(
    'google_client_id' => 'YOUR_CLIENT_ID',
    'google_client_secret' => 'YOUR_SECRET',
    'google_scope' => 'email profile'
);
```

### Social Login Display

**Position Options:**
1. Above form fields
2. Below form fields
3. Separate tab
4. Side by side with form

**Button Styles:**
```css
/* Social login buttons */
.reign-social-login-buttons {
    display: flex;
    gap: 10px;
    margin: 20px 0;
}

.reign-social-login-btn {
    flex: 1;
    padding: 10px;
    border-radius: 4px;
}
```

## Popup Behavior

### Triggers

**Automatic Triggers:**
```javascript
// Show after time delay
reign_popup_settings = {
    trigger: 'time',
    delay: 5000 // 5 seconds
};

// Show on scroll
reign_popup_settings = {
    trigger: 'scroll',
    percentage: 50 // 50% scroll
};

// Show on exit intent
reign_popup_settings = {
    trigger: 'exit',
    sensitivity: 20
};
```

### User Conditions

**Display Rules:**
- Show only to logged out users
- Show once per session
- Show based on referrer
- Show on specific pages

```php
// Conditional display
add_filter('reign_show_login_popup', function($show) {
    if (is_page('special-offer')) {
        return true;
    }
    return $show;
});
```

## Customization

### CSS Customization

```css
/* Popup container */
.reign-login-popup-container {
    background: rgba(0,0,0,0.8);
    z-index: 999999;
}

/* Popup modal */
.reign-login-popup-modal {
    background: #ffffff;
    border-radius: 10px;
    box-shadow: 0 10px 40px rgba(0,0,0,0.2);
}

/* Form styling */
.reign-popup-form input {
    width: 100%;
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-bottom: 15px;
}

/* Submit button */
.reign-popup-submit {
    width: 100%;
    padding: 12px 24px;
    background: var(--reign-primary-color);
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}
```

### Template Override

Create custom popup templates:

```php
// In child theme
reign-child/
├── template-parts/
│   └── popup/
│       ├── login-form.php
│       └── register-form.php
```

**login-form.php:**
```php
<?php
/**
 * Custom Login Popup Template
 */
?>
<div class="custom-login-popup">
    <h2><?php _e('Welcome Back', 'reign'); ?></h2>

    <form id="reign-login-form" action="<?php echo esc_url(site_url('wp-login.php', 'login_post')); ?>" method="post">

        <?php do_action('reign_before_login_fields'); ?>

        <input type="text" name="log" placeholder="<?php _e('Username or Email', 'reign'); ?>" required>
        <input type="password" name="pwd" placeholder="<?php _e('Password', 'reign'); ?>" required>

        <label>
            <input type="checkbox" name="rememberme" value="forever">
            <?php _e('Remember Me', 'reign'); ?>
        </label>

        <?php do_action('reign_after_login_fields'); ?>

        <button type="submit"><?php _e('Login', 'reign'); ?></button>

        <?php wp_nonce_field('ajax-login-nonce', 'security'); ?>
    </form>

    <div class="popup-footer">
        <a href="#" class="switch-to-register"><?php _e('Create Account', 'reign'); ?></a>
        <a href="<?php echo wp_lostpassword_url(); ?>"><?php _e('Lost Password?', 'reign'); ?></a>
    </div>
</div>
```

## AJAX Handling

### Login AJAX

```javascript
// Custom AJAX login
jQuery(document).on('submit', '#reign-login-form', function(e) {
    e.preventDefault();

    var form = jQuery(this);
    var data = form.serialize() + '&action=reign_ajax_login';

    jQuery.ajax({
        url: reign_ajax.ajaxurl,
        type: 'POST',
        data: data,
        success: function(response) {
            if (response.success) {
                window.location.reload();
            } else {
                alert(response.data.message);
            }
        }
    });
});
```

### Registration AJAX

```php
// Handle AJAX registration
add_action('wp_ajax_nopriv_reign_ajax_register', 'reign_handle_ajax_registration');
function reign_handle_ajax_registration() {
    // Verify nonce
    if (!wp_verify_nonce($_POST['security'], 'ajax-register-nonce')) {
        wp_send_json_error(array('message' => 'Security check failed'));
    }

    // Create user
    $user_id = wp_create_user(
        sanitize_user($_POST['username']),
        $_POST['password'],
        sanitize_email($_POST['email'])
    );

    if (is_wp_error($user_id)) {
        wp_send_json_error(array('message' => $user_id->get_error_message()));
    }

    // Auto login
    wp_set_current_user($user_id);
    wp_set_auth_cookie($user_id);

    wp_send_json_success(array(
        'message' => 'Registration successful',
        'redirect' => home_url()
    ));
}
```

## Advanced Features

### Two-Factor Authentication

```php
// Add 2FA to popup login
add_action('reign_after_login_fields', function() {
    ?>
    <div class="two-factor-field" style="display:none;">
        <input type="text" name="auth_code" placeholder="Enter 6-digit code">
    </div>
    <?php
});
```

### reCAPTCHA Integration

```php
// Add reCAPTCHA
add_action('reign_after_register_fields', function() {
    ?>
    <div class="g-recaptcha" data-sitekey="YOUR_SITE_KEY"></div>
    <?php
});
```

### Email Verification

```php
// Require email verification
add_filter('reign_registration_requires_verification', '__return_true');

// Custom verification message
add_filter('reign_verification_message', function($message) {
    return 'Please check your email to verify your account.';
});
```

## Popup Events

### JavaScript Hooks

```javascript
// Before popup opens
document.addEventListener('reign_before_popup_open', function(e) {
    console.log('Popup opening:', e.detail.type);
});

// After popup opens
document.addEventListener('reign_after_popup_open', function(e) {
    // Custom tracking
    gtag('event', 'popup_open', {
        'popup_type': e.detail.type
    });
});

// After successful login
document.addEventListener('reign_login_success', function(e) {
    console.log('User logged in:', e.detail.user);
});

// After successful registration
document.addEventListener('reign_register_success', function(e) {
    console.log('User registered:', e.detail.user_id);
});
```

## Mobile Optimization

### Responsive Design

```css
@media (max-width: 768px) {
    .reign-login-popup-modal {
        width: 90%;
        max-width: none;
        margin: 20px auto;
    }

    .reign-social-login-buttons {
        flex-direction: column;
    }

    .reign-popup-form input {
        font-size: 16px; /* Prevent zoom */
    }
}
```

### Touch Gestures

```javascript
// Swipe to close on mobile
var touchStartY = 0;
document.querySelector('.reign-popup-modal').addEventListener('touchstart', function(e) {
    touchStartY = e.touches[0].clientY;
});

document.querySelector('.reign-popup-modal').addEventListener('touchend', function(e) {
    var touchEndY = e.changedTouches[0].clientY;
    if (touchEndY - touchStartY > 100) {
        // Swipe down - close popup
        reign_close_popup();
    }
});
```

## Troubleshooting

### Common Issues

#### Popup Not Opening
**Solutions:**
1. Check JavaScript console for errors
2. Verify jQuery is loaded
3. Clear cache
4. Check z-index conflicts

#### Social Login Not Working
**Solutions:**
1. Verify API credentials
2. Check redirect URIs
3. Enable required APIs
4. Test in incognito mode

#### Form Not Submitting
**Solutions:**
1. Check nonce verification
2. Verify AJAX URL
3. Check required fields
4. Review server response

### Debug Mode

```php
// Enable debug logging
define('REIGN_POPUP_DEBUG', true);

// Log popup events
add_action('reign_popup_login_attempt', function($username) {
    if (REIGN_POPUP_DEBUG) {
        error_log('Login attempt: ' . $username);
    }
});
```

## Performance

### Optimization Tips

1. **Lazy Load Popup**
```javascript
// Load popup only when needed
document.querySelector('.reign-login-link').addEventListener('click', function() {
    if (!window.reignPopupLoaded) {
        loadPopupAssets();
        window.reignPopupLoaded = true;
    }
});
```

2. **Minimize CSS**
- Use critical CSS inline
- Load full styles async

3. **Cache Forms**
- Store form HTML in sessionStorage
- Reduce server requests

## Security

### Best Practices

1. **Nonce Verification**
```php
// Always verify nonces
wp_verify_nonce($_POST['_wpnonce'], 'reign-login');
```

2. **Rate Limiting**
```php
// Limit login attempts
add_filter('reign_login_attempts_allowed', function() {
    return 5; // Max 5 attempts per hour
});
```

3. **SSL/HTTPS**
- Always use HTTPS for login
- Force SSL for admin

4. **Input Sanitization**
```php
// Sanitize all inputs
$username = sanitize_user($_POST['username']);
$email = sanitize_email($_POST['email']);
```

---

*For social login setup details, see the Social Login Integration guide.*