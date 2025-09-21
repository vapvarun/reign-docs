# Branded Login & Register Pages

## Overview

Reign Theme provides comprehensive customization options for WordPress login and registration pages, allowing you to create a branded experience that matches your site's design.

## Enabling Custom Login

### Activation

Navigate to:
```
Customizer → Branded Login & Register → WP Login / Register
```

**Enable Custom Login Screen**
- Toggle: ON/OFF
- Default: OFF
- When enabled, applies custom styling to wp-login.php

## Login Page Themes

### Available Themes

Navigate to:
```
Customizer → Branded Login & Register → Themes
```

**Theme Options:**

1. **Simple** (Default)
   - Clean, minimalist design
   - Centered login form
   - Subtle shadows
   - Mobile-optimized

2. **Split Page**
   - 50/50 layout
   - Left side: Branding/Image
   - Right side: Login form
   - Modern appearance

3. **Dark Mode**
   - Dark background
   - Light form elements
   - High contrast
   - Eye-friendly

4. **Overlay**
   - Full background image
   - Form overlay with transparency
   - Dramatic effect
   - Parallax option

## Logo Customization

### Logo Settings

```
Customizer → Branded Login & Register → WP Login / Register
```

**Logo Options:**

1. **Admin Logo Media**
   - Upload custom logo
   - Recommended: 320px width
   - Format: PNG/JPG/SVG
   - Transparent background preferred

2. **Logo URL**
   - Default: Links to homepage
   - Customizable link destination

3. **Logo Title**
   - Hover text for logo
   - Default: Site name
   - SEO-friendly text

### Logo Styling

```css
/* Applied automatically when custom logo is set */
.login h1 a {
    background-image: url(your-logo.png);
    width: 320px;
    height: 84px;
    background-size: contain;
}
```

## Background Customization

### Background Options

```
Customizer → Branded Login & Register → Background
```

**Settings:**

1. **Background Type**
   - Solid Color
   - Gradient
   - Image
   - Video (Premium)

2. **Background Image**
   - Upload image
   - Recommended: 1920x1080px minimum
   - Format: JPG/PNG
   - Optimize for web

3. **Background Position**
   - Top Left
   - Top Center
   - Top Right
   - Center Left
   - Center Center (default)
   - Center Right
   - Bottom Left
   - Bottom Center
   - Bottom Right

4. **Background Size**
   - Auto
   - Cover (recommended)
   - Contain
   - Custom

5. **Background Repeat**
   - No Repeat (default)
   - Repeat
   - Repeat-X
   - Repeat-Y

6. **Background Attachment**
   - Scroll
   - Fixed (parallax effect)

### Gradient Backgrounds

**Gradient Options:**
```css
/* Example gradient settings */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
```

Presets available:
- Purple Dream
- Ocean Blue
- Sunset Orange
- Forest Green
- Night Sky

## Form Customization

### Form Styling

```
Customizer → Branded Login & Register → Customize Login Form
```

**Form Container:**

1. **Background Color**
   - Default: White
   - Transparency option
   - Blur effect available

2. **Border Settings**
   - Border width: 0-10px
   - Border color
   - Border radius: 0-50px
   - Border style: solid/dashed/dotted

3. **Shadow Effects**
   - Box shadow intensity
   - Shadow color
   - Shadow spread
   - Elevation levels (1-5)

4. **Padding & Margins**
   - Form padding: 20-60px
   - Form width: 320-500px
   - Vertical position adjustment

### Form Fields

**Input Field Styling:**

1. **Field Appearance**
   - Background color
   - Border style
   - Border radius
   - Focus effects

2. **Typography**
   - Font family
   - Font size: 14-18px
   - Text color
   - Placeholder color

3. **Icons**
   - User icon for username
   - Lock icon for password
   - Email icon for email
   - Icon position: left/right

### Labels & Text

**Text Customization:**
- Label color
- Label size
- Label weight
- Helper text styling
- Error message styling

## Button Customization

### Button Settings

```
Customizer → Branded Login & Register → Customize Button
```

**Primary Button (Login/Register):**

1. **Colors**
   - Background color
   - Text color
   - Hover background
   - Hover text color
   - Active state colors

2. **Size & Shape**
   - Button width: Auto/Full
   - Padding: 10-20px vertical, 20-40px horizontal
   - Border radius: 0-50px
   - Height: 40-60px

3. **Typography**
   - Font family
   - Font size: 14-18px
   - Font weight: 400-700
   - Text transform: none/uppercase/lowercase
   - Letter spacing

4. **Effects**
   - Hover animations
   - Transition duration
   - Shadow on hover
   - Scale effect
   - Gradient options

### Secondary Buttons

**"Remember Me" Checkbox:**
- Custom checkbox design
- Color customization
- Size adjustment

**Links Styling:**
- "Lost your password?" link
- "Back to site" link
- Color and hover effects
- Underline options

## Login Popup

### Enable Login Popup

```
Customizer → General → Login Popup
```

**Settings:**

1. **Enable Login Popup**
   - Toggle: ON/OFF
   - Replaces page redirect with modal

2. **Trigger Options**
   - Login menu item
   - Custom button class
   - Shortcode trigger

3. **Popup Style**
   - Modal
   - Slide-in
   - Fade
   - Drop-down

### Popup Configuration

**Display Options:**
- Overlay color
- Overlay opacity
- Popup width
- Animation speed
- Close button style

**Content Tabs:**
- Login
- Register
- Lost Password
- Custom content

## Community Register

### BuddyPress Registration

For BuddyPress sites:
```
Customizer → Branded Login & Register → Community Register
```

**Enhanced Registration:**
- Multi-step registration
- Profile fields during signup
- Avatar upload option
- Terms acceptance
- Email verification

### Registration Fields

**Custom Fields:**
- Add custom fields
- Field validation
- Required indicators
- Field descriptions
- Conditional logic

## Custom CSS

### Additional Styling

```
Customizer → Additional CSS
```

**Common Customizations:**

```css
/* Change login page font */
body.login {
    font-family: 'Your Font', sans-serif;
}

/* Custom form width */
#loginform {
    width: 400px !important;
}

/* Remove language switcher */
.language-switcher {
    display: none;
}

/* Custom error message styling */
.login #login_error {
    background: #ff4444;
    color: white;
    border-radius: 5px;
}

/* Success message styling */
.login .message {
    background: #44ff44;
    border-left: 4px solid #00aa00;
}
```

## Theme-Specific Classes

### Body Classes Added

Based on settings, these classes are added:

```php
// Simple theme
body.login.rg-login

// Split page with background
body.login.login-split-page.rg-login

// With custom theme
body.login.rg-login.login-{theme-name}

// Dark mode
body.login.rg-login.login-dark
```

## Security Features

### Built-in Security

**Login Protection:**
- Honeypot fields (invisible)
- Rate limiting ready
- reCAPTCHA support
- Custom login URL compatible
- Brute force protection ready

### Security Plugins Compatible

Works with:
- Wordfence
- Sucuri
- iThemes Security
- All In One WP Security
- Login LockDown

## Mobile Optimization

### Responsive Design

**Automatic Adjustments:**
- Form scales to screen
- Touch-friendly inputs
- Larger tap targets
- Optimized keyboard
- Portrait/landscape support

### Mobile-Specific Settings

```css
@media (max-width: 768px) {
    /* Mobile optimizations applied automatically */
    .login form {
        width: 90% !important;
        margin: 20px auto;
    }
}
```

## Integration Options

### Social Login

**Compatible Plugins:**
- BuddyBoss Social Login
- Super Socializer
- Nextend Social Login
- Social Login by miniOrange

**Display Options:**
- Above form
- Below form
- Separate tab
- Replace default

### SSO Integration

**Supported Systems:**
- SAML
- OAuth
- LDAP
- Active Directory
- Google Workspace

## Troubleshooting

### Common Issues

**Logo Not Showing**
- Check file upload
- Verify URL path
- Clear cache
- Check file permissions

**Styles Not Applied**
- Enable custom login toggle
- Save customizer settings
- Clear browser cache
- Check for plugin conflicts

**Background Image Issues**
- Optimize image size (<500KB)
- Use correct dimensions
- Check file format
- Verify file path

**Form Not Centered**
- Check theme selection
- Verify CSS conflicts
- Inspect custom CSS
- Reset positioning

## Best Practices

### Design Guidelines

1. **Consistency**
   - Match site branding
   - Use brand colors
   - Consistent typography
   - Maintain style guide

2. **Performance**
   - Optimize images
   - Minimize custom CSS
   - Use system fonts
   - Enable caching

3. **Accessibility**
   - Sufficient contrast
   - Clear labels
   - Keyboard navigation
   - Screen reader friendly

4. **User Experience**
   - Clear error messages
   - Helpful instructions
   - Progress indicators
   - Success feedback

## Code Snippets

### Useful Functions

**Redirect After Login:**
```php
add_filter('login_redirect', 'reign_custom_login_redirect', 10, 3);
function reign_custom_login_redirect($redirect_to, $request, $user) {
    if (isset($user->roles) && is_array($user->roles)) {
        if (in_array('subscriber', $user->roles)) {
            return home_url('/members/');
        }
    }
    return $redirect_to;
}
```

**Custom Login Message:**
```php
add_filter('login_message', 'reign_custom_login_message');
function reign_custom_login_message() {
    return '<p class="custom-message">Welcome to our community!</p>';
}
```

**Add Custom Field:**
```php
add_action('login_form', 'reign_add_custom_field');
function reign_add_custom_field() {
    ?>
    <p>
        <label>Company Code<br>
        <input type="text" name="company_code" class="input" />
        </label>
    </p>
    <?php
}
```

## Advanced Customization

### Create Custom Theme

1. Create CSS file in child theme
2. Enqueue on login page
3. Add body class
4. Override default styles

```php
// In child theme functions.php
add_action('login_enqueue_scripts', 'reign_child_login_theme');
function reign_child_login_theme() {
    wp_enqueue_style('reign-child-login',
        get_stylesheet_directory_uri() . '/login-custom.css',
        array(),
        '1.0'
    );
}
```

---

*Transform your login experience with Reign's branded login system!*