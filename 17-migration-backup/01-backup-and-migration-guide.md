# Backup and Migration Complete Guide

## Overview

Proper backup and migration procedures are essential for maintaining your Reign theme website. This guide covers backup strategies, migration methods, and disaster recovery procedures.

## Backup Strategies

### What to Backup

**Essential Components:**
```
1. Database
   - All WordPress tables
   - BuddyPress tables
   - WooCommerce data
   - Custom plugin tables

2. Files
   - /wp-content/uploads/
   - /wp-content/themes/reign-theme/
   - /wp-content/themes/reign-child/
   - /wp-content/plugins/
   - wp-config.php
   - .htaccess

3. Settings
   - Customizer settings
   - Widget configurations
   - Menu structures
   - Plugin settings
```

### Backup Methods

#### Method 1: Manual Backup

**Database Backup via phpMyAdmin:**
```sql
-- Export all tables
SELECT * FROM information_schema.tables
WHERE table_schema = 'your_database_name';

-- Export with options
mysqldump -u username -p database_name > backup.sql
```

**Files Backup via FTP:**
```bash
# Using command line
wget -r -l inf -np ftp://user:pass@server/path/

# Or using rsync
rsync -avz /source/path/ /backup/path/
```

#### Method 2: Plugin-Based Backup

**UpdraftPlus Configuration:**
```php
// Optimal settings
$backup_settings = array(
    'interval' => 'daily',
    'retain' => 30,
    'include_database' => true,
    'include_uploads' => true,
    'include_themes' => true,
    'include_plugins' => true,
    'remote_storage' => 'google_drive',
);
```

**BackWPup Settings:**
```
Job Configuration:
✓ Database backup
✓ File backup
✓ List of installed plugins
✓ Database optimization
Schedule: Daily at 3 AM
Destination: S3 / Dropbox / FTP
```

#### Method 3: Server-Level Backup

**cPanel Backup:**
```
1. Login to cPanel
2. Files → Backup Wizard
3. Select "Full Backup"
4. Choose destination
5. Generate backup
```

**Command Line Backup:**
```bash
#!/bin/bash
# Backup script

DATE=$(date +%Y%m%d)
BACKUP_DIR="/backup/$DATE"

# Create backup directory
mkdir -p $BACKUP_DIR

# Backup database
mysqldump -u root -p database_name > $BACKUP_DIR/database.sql

# Backup files
tar -czf $BACKUP_DIR/files.tar.gz /path/to/wordpress/

# Backup to remote
rsync -avz $BACKUP_DIR remote_server:/remote/backup/
```

### Backup Schedule

**Recommended Schedule:**
```
Database: Daily
Uploads: Weekly
Full Site: Monthly
Before Updates: Always
Before Major Changes: Always
```

**Automated Backup Cron:**
```bash
# Daily database backup at 2 AM
0 2 * * * /usr/bin/mysqldump -u user -ppassword database > /backup/db_$(date +\%Y\%m\%d).sql

# Weekly files backup on Sunday
0 3 * * 0 tar -czf /backup/files_$(date +\%Y\%m\%d).tar.gz /var/www/html/

# Monthly full backup
0 4 1 * * /scripts/full_backup.sh
```

## Migration Process

### Pre-Migration Checklist

```
□ Full backup completed
□ Document current settings
□ Note active plugins
□ Record customizations
□ Test on staging first
□ Maintenance mode ready
□ DNS propagation time considered
□ SSL certificate prepared
□ Email settings documented
```

### Migration Methods

#### Method 1: All-in-One Migration

**Using All-in-One WP Migration:**
```
Export Process:
1. Install plugin on source site
2. Export → File/URL
3. Advanced options:
   - Do not export spam comments
   - Do not export post revisions
   - Replace URLs if needed

Import Process:
1. Install plugin on destination
2. Import → Upload file
3. Proceed with warnings
4. Update permalinks
```

#### Method 2: Manual Migration

**Step-by-Step Process:**

**1. Export Database:**
```sql
-- Export with extended inserts
mysqldump --extended-insert --complete-insert
    --single-transaction --routines --triggers
    -u username -p database_name > export.sql
```

**2. Prepare Database for Import:**
```sql
-- Update URLs in SQL file
UPDATE wp_options SET option_value =
    REPLACE(option_value, 'http://old-domain.com', 'https://new-domain.com')
WHERE option_name = 'home' OR option_name = 'siteurl';

UPDATE wp_posts SET guid =
    REPLACE(guid, 'http://old-domain.com', 'https://new-domain.com');

UPDATE wp_posts SET post_content =
    REPLACE(post_content, 'http://old-domain.com', 'https://new-domain.com');

UPDATE wp_postmeta SET meta_value =
    REPLACE(meta_value, 'http://old-domain.com', 'https://new-domain.com');
```

**3. Transfer Files:**
```bash
# Using rsync
rsync -avz --progress source_server:/path/ destination_server:/path/

# Using SCP
scp -r /source/path/ user@destination:/destination/path/

# Using FTP
lftp -u user,password server << EOF
mirror --reverse --delete --verbose /local/path /remote/path
EOF
```

**4. Update Configuration:**
```php
// wp-config.php changes
define('DB_NAME', 'new_database');
define('DB_USER', 'new_user');
define('DB_PASSWORD', 'new_password');
define('DB_HOST', 'new_host');

// Update salts
define('AUTH_KEY', 'new_generated_key');
define('SECURE_AUTH_KEY', 'new_generated_key');
// ... etc

// Update paths if needed
define('WP_HOME', 'https://new-domain.com');
define('WP_SITEURL', 'https://new-domain.com');
```

#### Method 3: Staging to Production

**Staging Environment Setup:**
```
1. Create subdomain: staging.yoursite.com
2. Clone production site
3. Test all changes
4. Push to production
```

**Push to Production:**
```bash
# Using WP CLI
wp search-replace 'staging.site.com' 'site.com' --all-tables
wp cache flush
wp rewrite flush
```

### BuddyPress Migration Specifics

**BuddyPress Tables:**
```sql
-- Essential BP tables to migrate
wp_bp_activity
wp_bp_activity_meta
wp_bp_friends
wp_bp_groups
wp_bp_groups_groupmeta
wp_bp_groups_members
wp_bp_messages_messages
wp_bp_messages_meta
wp_bp_messages_notices
wp_bp_messages_recipients
wp_bp_notifications
wp_bp_notifications_meta
wp_bp_xprofile_data
wp_bp_xprofile_fields
wp_bp_xprofile_groups
wp_bp_xprofile_meta
```

**Member Avatars Migration:**
```bash
# Copy avatar uploads
cp -r /old/wp-content/uploads/avatars/ /new/wp-content/uploads/avatars/

# Fix permissions
chown -R www-data:www-data /new/wp-content/uploads/avatars/
chmod -R 755 /new/wp-content/uploads/avatars/
```

### WooCommerce Migration Specifics

**WooCommerce Data:**
```sql
-- Critical WooCommerce tables
wp_woocommerce_*
wp_wc_*

-- Product images
/wp-content/uploads/woocommerce_uploads/

-- Session data (optional)
wp_woocommerce_sessions
```

**Order Migration Verification:**
```php
// Verify order count
$old_orders = 1500; // From old site
$new_orders = wc_get_orders(array('limit' => -1, 'return' => 'count'));

if ($old_orders !== $new_orders) {
    error_log("Order count mismatch: Old: $old_orders, New: $new_orders");
}
```

## Post-Migration Tasks

### Essential Checks

**1. Update URLs:**
```php
// Search and replace URLs
function update_urls_after_migration() {
    global $wpdb;

    $old_url = 'http://old-site.com';
    $new_url = 'https://new-site.com';

    // Update in common tables
    $tables = array(
        $wpdb->posts => array('guid', 'post_content'),
        $wpdb->postmeta => array('meta_value'),
        $wpdb->options => array('option_value'),
        $wpdb->comments => array('comment_content', 'comment_author_url'),
    );

    foreach ($tables as $table => $columns) {
        foreach ($columns as $column) {
            $wpdb->query($wpdb->prepare(
                "UPDATE $table SET $column = REPLACE($column, %s, %s)",
                $old_url,
                $new_url
            ));
        }
    }
}
```

**2. Regenerate Permalinks:**
```
Settings → Permalinks → Save Changes
```

**3. Clear Caches:**
```php
// Clear all caches
wp_cache_flush();
if (function_exists('w3tc_flush_all')) {
    w3tc_flush_all();
}
if (function_exists('wp_rocket_clean_domain')) {
    wp_rocket_clean_domain();
}
```

**4. Test Critical Functions:**
```
□ User registration
□ User login
□ Password reset
□ Contact forms
□ Payment processing
□ Email sending
□ Search functionality
□ Media uploads
□ Social sharing
```

### Troubleshooting Migration Issues

#### Database Connection Errors
```php
// Test database connection
$connection = new mysqli(DB_HOST, DB_USER, DB_PASSWORD, DB_NAME);
if ($connection->connect_error) {
    die("Connection failed: " . $connection->connect_error);
}
echo "Connected successfully";
```

#### Serialized Data Issues
```php
// Fix serialized data
function fix_serialized_data($data) {
    $data = preg_replace_callback(
        '!s:(\d+):"(.*?)";!',
        function($match) {
            return 's:' . strlen($match[2]) . ':"' . $match[2] . '";';
        },
        $data
    );
    return $data;
}
```

#### Permission Problems
```bash
# Fix file permissions
find /path/to/wordpress -type d -exec chmod 755 {} \;
find /path/to/wordpress -type f -exec chmod 644 {} \;
chmod 600 wp-config.php
```

## Disaster Recovery

### Recovery Plan

**Level 1: Minor Issues**
```
Time to Recovery: < 1 hour
- Restore from daily backup
- Fix specific corrupted files
- Clear caches and regenerate
```

**Level 2: Major Issues**
```
Time to Recovery: 2-4 hours
- Full site restore from backup
- Database restoration
- Reconfigure settings
```

**Level 3: Complete Failure**
```
Time to Recovery: 4-8 hours
- Provision new server
- Install fresh WordPress
- Restore from offsite backup
- DNS propagation wait
```

### Recovery Scripts

```bash
#!/bin/bash
# Emergency recovery script

# Variables
BACKUP_FILE="/backup/latest/full_backup.tar.gz"
RESTORE_PATH="/var/www/html"
DB_BACKUP="/backup/latest/database.sql"

# Stop services
systemctl stop apache2
systemctl stop mysql

# Restore files
tar -xzf $BACKUP_FILE -C $RESTORE_PATH

# Restore database
mysql -u root -p < $DB_BACKUP

# Fix permissions
chown -R www-data:www-data $RESTORE_PATH
find $RESTORE_PATH -type d -exec chmod 755 {} \;
find $RESTORE_PATH -type f -exec chmod 644 {} \;

# Start services
systemctl start mysql
systemctl start apache2

# Clear caches
wp cache flush --path=$RESTORE_PATH

echo "Recovery complete!"
```

## Best Practices

### Backup Best Practices
1. **3-2-1 Rule** - 3 copies, 2 different media, 1 offsite
2. **Test Restores** - Regularly test backup restoration
3. **Automate** - Use scripts and cron jobs
4. **Document** - Keep restoration procedures documented
5. **Monitor** - Set up alerts for backup failures
6. **Encrypt** - Secure sensitive backup data
7. **Version** - Keep multiple backup versions
8. **Rotate** - Implement backup rotation policy

### Migration Best Practices
1. **Test First** - Always test on staging
2. **Schedule Wisely** - Migrate during low traffic
3. **Communicate** - Inform users about downtime
4. **Verify** - Check everything post-migration
5. **Keep Old Site** - Don't delete immediately
6. **Document Changes** - Track all modifications
7. **Monitor** - Watch for issues post-migration
8. **Rollback Plan** - Have a plan to revert if needed

## Tools and Resources

### Backup Tools
- UpdraftPlus
- BackWPup
- VaultPress
- BlogVault
- WP Time Capsule

### Migration Tools
- All-in-One WP Migration
- Duplicator
- WP Migrate DB
- Search Replace DB
- WP CLI

### Server Tools
- rsync
- mysqldump
- tar
- scp
- lftp

### Monitoring Tools
- Uptime Robot
- Pingdom
- New Relic
- StatusCake