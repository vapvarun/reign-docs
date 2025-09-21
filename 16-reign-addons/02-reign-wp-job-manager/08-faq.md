# Reign WP Job Manager Addon - FAQ

## General Questions

### Q: What is Reign WP Job Manager Addon?
**A:** Reign WP Job Manager Addon is a premium extension that enhances WP Job Manager with beautiful layouts, advanced features, and seamless integration with the Reign WordPress theme.

### Q: Do I need WP Job Manager Pro?
**A:** No, the free version of WP Job Manager is sufficient. However, Pro add-ons like Resume Manager and Applications work seamlessly with our addon.

### Q: Is BuddyPress required?
**A:** No, BuddyPress is optional. However, it adds social features like activity streams, member profiles, and job discussions.

### Q: Can I use this with other themes?
**A:** No, this addon is specifically designed for the Reign theme and requires it to function properly.

### Q: How many job listings can I create?
**A:** There's no limit on the number of job listings you can create.

## Installation & Setup

### Q: Why is the plugin not activating?
**A:** Check these requirements:
- Reign Theme is active (v7.0+)
- WP Job Manager is installed and active
- PHP 7.4 or higher
- WordPress 5.8 or higher

### Q: How do I get updates?
**A:** Activate your license key in Reign Settings > License. Updates will appear in Plugins > Updates.

### Q: Can I use it on multiple sites?
**A:** It depends on your license:
- Single Site License: 1 site
- 5 Sites License: 5 sites
- Unlimited License: Unlimited sites

### Q: How do I migrate from another job board plugin?
**A:** We provide migration guides for:
- WP Job Board
- Simple Job Board
- WP Job Portal
Contact support for assistance.

## Features & Functionality

### Q: Can employers post jobs for free?
**A:** Yes, you can configure:
- Free job submissions
- Paid job listings (with WooCommerce)
- Subscription plans
- Featured job upgrades

### Q: How do I enable resume submissions?
**A:** Install the WP Job Manager - Resume Manager add-on. Our addon will automatically style and integrate it.

### Q: Can I customize the application process?
**A:** Yes, you can choose:
- Email applications
- External URL redirect
- Built-in application form (with Applications add-on)
- Custom forms integration

### Q: Does it support multiple locations?
**A:** Yes, jobs can have:
- Single locations
- Multiple locations (with add-on)
- Remote positions
- Location-based search with radius

### Q: Can I add custom fields to jobs?
**A:** Yes, using:
- WP Job Manager Field Editor add-on
- Custom code hooks
- ACF integration

## Customization

### Q: How do I change the layout?
**A:** Navigate to Appearance > Customize > Reign Job Manager:
- Choose between Grid, List, or Map view
- Adjust columns and spacing
- Toggle elements on/off

### Q: Can I customize the colors?
**A:** Yes, in Customizer:
- Primary and secondary colors
- Job type colors
- Button colors
- Inherit from theme settings

### Q: How do I override templates?
**A:** Copy templates from:
```
plugins/reign-wp-job-manager-addon/templates/
```
To:
```
themes/reign-theme/reign-job-manager/
```

### Q: Can I add custom CSS?
**A:** Yes, add CSS in:
- Customizer > Additional CSS
- Child theme stylesheet
- Custom CSS plugin

### Q: How do I translate the addon?
**A:** The addon is translation-ready:
1. Use Loco Translate plugin
2. Find .pot file in `/languages/`
3. Create translation
4. Save as `reign-job-manager-{locale}.po`

## Performance

### Q: Why are job listings loading slowly?
**A:** Try these optimizations:
- Reduce jobs per page (10-15)
- Enable caching plugin
- Optimize images
- Use CDN
- Enable lazy loading

### Q: How can I improve search performance?
**A:** 
- Add database indexes
- Use Elasticsearch plugin
- Enable object caching
- Limit search filters

### Q: Does it work with cache plugins?
**A:** Yes, compatible with:
- WP Super Cache
- W3 Total Cache
- WP Rocket
- LiteSpeed Cache

Exclude these pages:
- `/job-dashboard/`
- `/submit-job/`
- `/my-account/`

## Monetization

### Q: How can I charge for job listings?
**A:** Options include:
- WooCommerce Paid Listings
- Pay per post
- Subscription packages
- Featured job fees
- Resume database access

### Q: Can I offer different pricing plans?
**A:** Yes, create packages with:
- Different durations
- Number of listings
- Featured options
- Category restrictions

### Q: How do I set up recurring payments?
**A:** Use WooCommerce Subscriptions with WP Job Manager - WooCommerce Paid Listings.

## SEO & Marketing

### Q: Is it SEO friendly?
**A:** Yes, features include:
- Schema markup
- Meta tags
- XML sitemap support
- Clean URLs
- Open Graph tags

### Q: Does it work with Yoast SEO?
**A:** Yes, full compatibility with:
- Yoast SEO
- RankMath
- All in One SEO
- SEOPress

### Q: Can I share jobs on social media?
**A:** Yes, built-in sharing for:
- Facebook
- Twitter
- LinkedIn
- WhatsApp
- Email

## Troubleshooting

### Q: Jobs are not displaying
**A:** Check:
1. Jobs are published
2. Permalinks are saved
3. Shortcode is correct
4. No plugin conflicts

### Q: Emails are not sending
**A:** Solutions:
1. Configure SMTP
2. Check spam folder
3. Verify email settings
4. Test with WP Mail SMTP plugin

### Q: Map is not showing
**A:** Verify:
1. Google Maps API key is added
2. Required APIs are enabled
3. Domain is authorized
4. No JavaScript errors

### Q: Filters not working
**A:** Check:
1. AJAX is enabled
2. JavaScript is loading
3. No conflicts
4. Nonce is valid

## Integration

### Q: Does it work with Elementor?
**A:** Yes, through:
- WP Job Manager widgets
- Shortcode widget
- Custom Elementor widgets (Pro)

### Q: Can I integrate with CRM?
**A:** Yes, compatible with:
- HubSpot
- Salesforce
- Zoho
- Via Zapier webhooks

### Q: Does it support multi-language?
**A:** Yes, works with:
- WPML
- Polylang
- TranslatePress
- Loco Translate

### Q: Can I import jobs from Indeed/LinkedIn?
**A:** Yes, using:
- WP Job Manager - Job Aggregator add-on
- WP All Import
- Custom import scripts

## Support

### Q: How do I get support?
**A:** Support channels:
1. Email: support@wbcomdesigns.com
2. Support forum (with license)
3. Documentation site
4. Video tutorials

### Q: Is there documentation?
**A:** Yes:
- This documentation
- Video tutorials
- Code examples
- API reference

### Q: Do you offer customization services?
**A:** Yes, contact us for:
- Custom development
- Installation service
- Migration assistance
- Training sessions

## Best Practices

### Q: How should I structure job categories?
**A:** Recommendations:
- Keep categories broad (5-15)
- Use tags for specifics
- Hierarchical structure
- Industry-standard terms

### Q: What's the optimal number of jobs per page?
**A:** Recommended:
- Desktop: 12-15
- Mobile: 8-10
- With sidebar: 9-12
- Map view: 20-30

### Q: How often should jobs expire?
**A:** Common durations:
- Standard: 30 days
- Premium: 60 days
- Featured: 14 days
- Urgent: 7 days

### Q: Should I moderate job submissions?
**A:** Yes, for:
- Quality control
- Spam prevention
- Policy compliance
- Trust building

## Updates & Compatibility

### Q: How often is the addon updated?
**A:** Regular updates include:
- Monthly maintenance
- Quarterly features
- Security patches as needed
- Compatibility updates

### Q: Is it compatible with WordPress 6.x?
**A:** Yes, tested with:
- WordPress 6.0-6.5
- PHP 7.4-8.2
- MySQL 5.7-8.0

### Q: Will it work with Gutenberg?
**A:** Yes, supports:
- Block editor
- Classic editor
- Custom blocks (coming soon)

### Q: What about REST API?
**A:** Full REST API support for:
- Job listings
- Applications
- Companies
- Custom endpoints

## Migration

### Q: Can I migrate from the old version?
**A:** Yes, automatic migration for:
- Settings
- Templates
- Custom fields
- Database structure

### Q: How do I backup before updating?
**A:** Backup:
1. Database (jobs, applications)
2. Custom templates
3. Uploads folder
4. Settings export

### Q: Can I rollback updates?
**A:** Yes:
1. Keep previous version ZIP
2. Deactivate current
3. Upload previous version
4. Restore database if needed

## Legal & Compliance

### Q: Is it GDPR compliant?
**A:** Yes, features:
- Data export
- Data deletion
- Cookie consent
- Privacy policy tools

### Q: Can I add terms of service?
**A:** Yes, add:
- Registration terms
- Job posting terms
- Application terms
- Privacy policy

### Q: How do I handle inappropriate content?
**A:** Tools include:
- Content moderation
- Report system
- Word blacklist
- User blocking

---

**Still have questions?**
Contact our support team at support@wbcomdesigns.com or visit our documentation site.

**Next Steps:**
- [Installation Guide](02-installation-setup.md)
- [Configuration Guide](03-configuration.md)
- [Troubleshooting](07-troubleshooting.md)