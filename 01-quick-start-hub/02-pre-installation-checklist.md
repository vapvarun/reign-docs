# Pre-Installation Checklist for Reign Theme

## System Requirements Verification

Before installing Reign theme, ensure your hosting environment meets all requirements for optimal performance.

## Server Requirements

### Minimum Requirements
- **PHP Version**: 7.4 or higher
- **MySQL Version**: 5.6 or higher (MySQL 8.0 recommended)
- **WordPress Version**: 5.0 or higher
- **Memory Limit**: 128MB (256MB recommended)
- **Max Execution Time**: 30 seconds (300 recommended for imports)
- **Max Input Vars**: 1000 (3000 recommended)
- **Upload Max Filesize**: 32MB (64MB recommended)
- **Post Max Size**: 32MB (64MB recommended)

### Recommended Requirements
- **PHP Version**: 8.0 or higher
- **MySQL Version**: 8.0 or MariaDB 10.3+
- **Memory Limit**: 256MB or higher
- **HTTPS**: SSL certificate installed
- **mod_rewrite**: Apache module enabled
- **cURL**: Version 7.34 or higher
- **GD Library**: For image processing
- **XML Support**: For sitemap generation

## Hosting Environment Check

### Supported Hosting Types
- ✅ **Shared Hosting** (with adequate resources)
- ✅ **VPS (Virtual Private Server)**
- ✅ **Dedicated Server**
- ✅ **Cloud Hosting** (AWS, Google Cloud, DigitalOcean)
- ✅ **Managed WordPress Hosting**

### Recommended Hosting Providers
1. **SiteGround** - Optimized for WordPress
2. **WP Engine** - Managed WordPress hosting
3. **Kinsta** - Premium performance
4. **Cloudways** - Cloud-based flexibility
5. **DigitalOcean** - Developer-friendly

### Hosting Features to Look For
- One-click WordPress installation
- Automatic backups
- SSL certificate
- CDN integration
- Staging environment
- SSH access (for advanced users)

## WordPress Preparation

### Clean WordPress Installation
- [ ] Fresh WordPress installation completed
- [ ] Default themes can be deleted (keep one as fallback)
- [ ] Default plugins reviewed and unnecessary ones removed
- [ ] Admin email address verified
- [ ] Site timezone configured
- [ ] Permalink structure set (Post name recommended)

### Existing WordPress Site
- [ ] Complete backup created (files and database)
- [ ] All plugins updated to latest versions
- [ ] WordPress core updated
- [ ] Database optimized
- [ ] Unused themes removed
- [ ] Media library cleaned up

## Required Information & Assets

### License & Purchase Information
- [ ] Reign theme purchase code ready
- [ ] ThemeForest/purchase account access
- [ ] Download link for latest theme version

### Branding Assets
- [ ] Logo files prepared (PNG/SVG recommended)
  - Desktop logo (200x50px recommended)
  - Mobile logo (150x40px recommended)
  - Favicon (512x512px)
- [ ] Brand colors defined (hex codes)
- [ ] Typography choices made
- [ ] Social media URLs ready

### Content Preparation
- [ ] Site title and tagline decided
- [ ] Main menu structure planned
- [ ] Key pages content drafted
- [ ] User registration settings decided
- [ ] Privacy policy and terms prepared

## Plugin Compatibility Check

### Essential Plugins
- [ ] **Kirki Framework** - Required for customizer
- [ ] **BuddyPress** - For community features (optional)
- [ ] **bbPress** - For forum functionality (optional)
- [ ] **WooCommerce** - For e-commerce (optional)

### Compatible Page Builders
- [ ] Elementor (Free or Pro)
- [ ] Beaver Builder
- [ ] Divi Builder
- [ ] WPBakery Page Builder
- [ ] Gutenberg (Default block editor)

### Recommended Plugins
- [ ] **Yoast SEO** or **RankMath** - SEO optimization
- [ ] **WP Rocket** or **W3 Total Cache** - Caching
- [ ] **Imagify** or **ShortPixel** - Image optimization
- [ ] **UpdraftPlus** - Backup solution
- [ ] **Wordfence** or **Sucuri** - Security

### Potential Conflict Plugins
Review and consider alternatives for:
- Other theme-specific plugins
- Outdated customizer plugins
- Conflicting menu plugins
- Old page builder plugins
- Deprecated community plugins

## Database Preparation

### Database Optimization
- [ ] Remove post revisions
- [ ] Clean spam comments
- [ ] Delete transient options
- [ ] Optimize database tables
- [ ] Remove unused tables from old plugins

### Database Backup
- [ ] Full database backup completed
- [ ] Backup stored off-site
- [ ] Restore process tested
- [ ] Database credentials documented

## Security Checklist

### Basic Security
- [ ] Strong admin password set
- [ ] Admin username changed from "admin"
- [ ] File permissions correct (755 for folders, 644 for files)
- [ ] wp-config.php protected
- [ ] XML-RPC disabled if not needed
- [ ] File editing disabled in WordPress admin

### SSL & HTTPS
- [ ] SSL certificate installed
- [ ] Force HTTPS redirect configured
- [ ] Mixed content issues resolved
- [ ] SSL certificate expiry noted

## Performance Baseline

### Current Performance Metrics
Document your site's current performance (if existing site):
- [ ] Page load time: ___ seconds
- [ ] Google PageSpeed score: ___/100
- [ ] GTmetrix grade: ___
- [ ] Number of HTTP requests: ___
- [ ] Total page size: ___ MB

### Performance Goals
- [ ] Target load time defined
- [ ] Performance budget set
- [ ] CDN requirements assessed
- [ ] Caching strategy planned

## Development Environment

### Local Development (Optional)
- [ ] Local development environment ready (XAMPP/Local/Docker)
- [ ] Staging site available
- [ ] Version control set up (Git)
- [ ] Deployment process defined

### Browser Testing Setup
- [ ] Chrome/Edge (latest version)
- [ ] Firefox (latest version)
- [ ] Safari (if on Mac)
- [ ] Mobile browsers ready for testing

## Team & Access Preparation

### Team Members
- [ ] Administrator accounts planned
- [ ] Editor/Author roles defined
- [ ] Moderator roles planned (for community)
- [ ] Vendor roles planned (for marketplace)

### Access Credentials
- [ ] Hosting control panel access
- [ ] FTP/SFTP credentials
- [ ] Database access (phpMyAdmin)
- [ ] Email accounts configured
- [ ] CDN account (if using)

## Migration Checklist (If Applicable)

### From Another Theme
- [ ] Content audit completed
- [ ] Custom code documented
- [ ] Shortcodes identified
- [ ] Custom post types noted
- [ ] Widget configurations documented
- [ ] Menu structures exported

### Domain/Hosting Migration
- [ ] DNS records documented
- [ ] Email settings backed up
- [ ] SSL certificate ready for transfer
- [ ] Redirects planned
- [ ] Downtime window scheduled

## Support Resources

### Documentation Access
- [ ] Reign documentation bookmarked
- [ ] Support ticket system access verified
- [ ] Community forum account created
- [ ] Video tutorial playlist saved

### Emergency Contacts
- [ ] Hosting support contact
- [ ] Developer contact (if applicable)
- [ ] Theme support ticket system
- [ ] Backup restoration process documented

## Final Pre-Installation Steps

### Immediate Before Installation
1. **Clear all caches** (if existing site)
2. **Create fresh backup**
3. **Note current plugin versions**
4. **Document current settings**
5. **Schedule installation time** (low traffic period)

### Communication Plan
- [ ] User notification prepared (if existing site)
- [ ] Maintenance mode message ready
- [ ] Team members informed
- [ ] Testing plan communicated

## Installation Readiness Score

Rate your readiness (check all that apply):
- [ ] All server requirements met
- [ ] Backup completed and tested
- [ ] License key ready
- [ ] Brand assets prepared
- [ ] Content strategy defined
- [ ] Plugin compatibility verified
- [ ] Security measures in place
- [ ] Performance baseline documented
- [ ] Support resources accessible
- [ ] Team briefed and ready

**Score: ___/10**

✅ **9-10**: Excellent! Proceed with installation
⚠️ **6-8**: Good, but review unchecked items
❌ **Below 6**: Additional preparation recommended

## Quick Reference Commands

### Check PHP Version
```bash
php -v
```

### Check MySQL Version
```sql
SELECT VERSION();
```

### Increase PHP Memory Limit (wp-config.php)
```php
define('WP_MEMORY_LIMIT', '256M');
```

### Enable Debug Mode (wp-config.php)
```php
define('WP_DEBUG', true);
define('WP_DEBUG_LOG', true);
define('WP_DEBUG_DISPLAY', false);
```

---

**Ready to Install?** Once you've completed this checklist, proceed to the 5-Minute Setup Guide for quick installation.