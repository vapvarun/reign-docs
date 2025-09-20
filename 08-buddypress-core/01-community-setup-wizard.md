# BuddyPress Community Setup Wizard - Build Your Social Network

## Welcome to Community Building

Transform your WordPress site into a thriving social community with BuddyPress and Reign. This comprehensive guide walks you through every step of creating an engaging community platform.

## Pre-Setup Checklist

### Before You Begin

**Ensure You Have:**
- [ ] Reign theme activated and licensed
- [ ] Administrator access to WordPress
- [ ] At least 256MB PHP memory limit
- [ ] Backup of your site (if existing)
- [ ] Clear vision of community purpose

**Decide On:**
- [ ] Open vs closed registration
- [ ] Public vs private community
- [ ] Moderation level needed
- [ ] Types of user interactions
- [ ] Content sharing permissions

## Step 1: Installing BuddyPress

### Installation Process

#### Method 1: From WordPress Admin (Recommended)
```
1. Navigate to: Plugins → Add New
2. Search for: "BuddyPress"
3. Look for: By BuddyPress Community
4. Click: Install Now
5. Click: Activate
```

#### Method 2: Manual Installation
```
1. Download from: wordpress.org/plugins/buddypress
2. Upload to: /wp-content/plugins/
3. Extract zip file
4. Navigate to: Plugins → Installed Plugins
5. Find BuddyPress and click: Activate
```

### Post-Installation Welcome

**After activation, you'll see:**
- Welcome screen with setup options
- Quick configuration wizard
- Component selection screen

**Choose:** "Let's Get Started!" to begin configuration

## Step 2: Component Configuration

### Understanding Components

BuddyPress components are modular features you can enable/disable based on your community needs.

### Core Components Setup

**Navigate to:** Settings → BuddyPress → Components

#### Essential Components (Usually Enable All)

**Extended Profiles**
```
What it does: Rich member profiles beyond WordPress defaults
Enable if: You want detailed member information
Features:
- Custom profile fields
- Profile field groups
- Visibility controls
- Required fields
```

**Account Settings**
```
What it does: User account management
Enable if: Members need to control their accounts
Features:
- Email/password changes
- Privacy settings
- Notification preferences
- Account deletion
```

**Activity Streams**
```
What it does: Facebook-like activity feed
Enable if: You want social interactions visible
Features:
- Status updates
- Activity comments
- Mentions (@username)
- Favorites/likes
- Activity filtering
```

**Notifications**
```
What it does: Alert system for user interactions
Enable if: You want engaged members
Features:
- On-site notifications
- Email notifications
- Mention alerts
- Friend request alerts
```

#### Social Components

**Friend Connections**
```
What it does: Allow members to connect
Enable if: Building social network
Features:
- Friend requests
- Friend lists
- Friendship privacy
- Mutual friends display
```

**Private Messaging**
```
What it does: Direct member communication
Enable if: Members should communicate privately
Features:
- Compose messages
- Threaded conversations
- Multiple recipients
- Message notifications
```

**User Groups**
```
What it does: Member-created communities
Enable if: You want sub-communities
Features:
- Public/private/hidden groups
- Group forums
- Group activities
- Member management
- Group media (with plugins)
```

#### Optional Components

**Site Tracking** (WordPress Multisite only)
```
What it does: Track sites in network
Enable if: Running multisite network
```

**Legacy Widgets**
```
What it does: Classic BuddyPress widgets
Enable if: Using older theme/plugins
Note: Reign has modern widgets built-in
```

### Recommended Component Settings

**For Social Community:**
- ✅ All core components
- ✅ Friend Connections
- ✅ Private Messaging
- ✅ User Groups

**For Professional Network:**
- ✅ Extended Profiles
- ✅ Activity Streams
- ✅ Private Messaging
- ❌ Friend Connections (use "Follow" instead)

**For Learning Community:**
- ✅ Extended Profiles
- ✅ User Groups (study groups)
- ✅ Activity Streams
- ✅ Private Messaging (teacher-student)

## Step 3: Pages Setup

### Automatic Page Creation

**BuddyPress creates these pages automatically:**

| Page | Purpose | URL |
|------|---------|-----|
| Members | Member directory | /members/ |
| Groups | Groups directory | /groups/ |
| Activity | Activity stream | /activity/ |
| Register | Registration form | /register/ |
| Activate | Account activation | /activate/ |

### Assigning Pages

**Navigate to:** Settings → BuddyPress → Pages

**Verify each component has a page:**
```
Members Directory: [Members Page]
Groups Directory: [Groups Page]
Activity Stream: [Activity Page]
Register: [Register Page]
Activate: [Activate Page]
```

**If pages are missing:**
1. Click "Create Page" next to component
2. Page auto-generates with correct shortcode
3. Save settings

### Custom Page Titles

**To rename pages:**
```
1. Go to: Pages → All Pages
2. Find BuddyPress page
3. Click: Quick Edit
4. Change title (URL slug remains same)
5. Update

Example:
"Members" → "Community"
"Groups" → "Teams"
"Activity" → "Feed"
```

## Step 4: Registration & Privacy

### Registration Settings

**Navigate to:** Settings → BuddyPress → Options

#### Registration Options

**Allow Registration**
```
Settings → General → Membership
✅ Anyone can register

Then in BuddyPress:
- Enable registration
- Show toolbar for logged-out users (optional)
```

**Registration Fields**
```
Users → Profile Fields → Primary
Add fields:
- Name (required)
- Bio (optional)
- Location (optional)
- Interests (optional)
- Social links (optional)
```

### Privacy Controls

#### Profile Visibility

**Default Visibility Settings:**
```
Extended Profiles → Settings
- Default visibility: Public/Members/Friends/Only Me
- Allow members to override
- Hide profiles from search engines
```

**Per-Field Visibility:**
```
Each profile field can have:
- Public: Everyone sees
- Members: Logged-in users only
- Friends: Connected friends only
- Only Me: Private
```

#### Activity Privacy

**Activity Stream Settings:**
```
- Who can post: All members/Verified only
- Default privacy: Public/Friends/Only Me
- Allow deletion: Yes/No
- Moderation: None/New users/All
```

## Step 5: Member Profiles Setup

### Profile Fields Configuration

**Navigate to:** Users → Profile Fields

#### Creating Field Groups

**Primary Group (Default):**
```
Name (required)
About Me
Location
Website
```

**Professional Info Group:**
```
Job Title
Company
Skills
Experience
LinkedIn Profile
```

**Social Details Group:**
```
Interests
Favorite Movies
Favorite Books
Hobbies
Social Media Links
```

#### Field Types Available

| Type | Use For | Example |
|------|---------|---------|
| Text Box | Short answers | Name, City |
| Text Area | Long answers | Bio, About |
| Date | Dates | Birthday, Join date |
| Radio | Single choice | Gender, Status |
| Checkbox | Multiple choice | Interests, Skills |
| Dropdown | Select one | Country, Language |
| Number | Numeric values | Age, Years experience |
| URL | Web links | Website, Social profiles |
| Phone | Contact numbers | Mobile, Office |

### Profile Completion

**Encouraging Complete Profiles:**

1. **Required Fields:**
   - Mark essential fields as required
   - Users must complete before proceeding

2. **Profile Progress Widget:**
   ```
   Appearance → Widgets
   Add: Reign Profile Completion
   Shows: Progress bar (65% complete)
   ```

3. **Gamification:**
   - Award badges for completion
   - Unlock features at milestones
   - Display completion percentage

## Step 6: Activity Stream Configuration

### Activity Settings

**Navigate to:** Settings → BuddyPress → Activity

#### Stream Options

**Enable/Disable Activity Types:**
```
✅ Updates (status posts)
✅ Comments on updates
✅ Group joins/creates
✅ Friendships created
✅ Profile updates
✅ New members
❌ Blog posts (if not relevant)
❌ Blog comments (if not relevant)
```

**Activity Display:**
```
Customizer → Community Settings → Activity
- Layout: Classic/Masonry/Grid
- Posts per page: 20
- Load more: Button/Infinite scroll
- Show filters: Yes/No
- Default filter: All/Friends/Groups/Mentions
```

### Activity Features

**Mentions (@username):**
- Auto-complete enabled
- Notification sent
- Creates connection

**Hashtags (#topic):**
- Auto-link to search
- Trending tags widget
- Topic discovery

**Media in Activities:**
```
Install: RTMedia or MediaPress
Features:
- Photo uploads
- Video sharing
- Audio posts
- Albums/galleries
```

## Step 7: Groups Configuration

### Group Settings

**Navigate to:** Settings → BuddyPress → Groups

#### Group Creation

**Who Can Create Groups:**
```
○ All members (open community)
○ Verified members only
○ Moderators and above
○ Admins only
```

**Group Types:**

**Public Groups**
```
- Listed in directory
- Open to all members
- Content visible to all
- Anyone can join
```

**Private Groups**
```
- Listed in directory
- Request membership
- Content member-only
- Admin approves members
```

**Hidden Groups**
```
- Not in directory
- Invite only
- Content hidden
- Complete privacy
```

### Group Features

**Enable for Groups:**
- ✅ Activity streams
- ✅ Member list
- ✅ Admin/mod roles
- ✅ Group forums (with bbPress)
- ✅ Group media (with plugin)
- ✅ Group messages

**Group Customization:**
- Cover images
- Group avatars
- Custom slugs
- Group types/categories
- Group metadata

## Step 8: Notifications Setup

### Notification Settings

**Navigate to:** Settings → BuddyPress → Emails

#### Email Notifications

**Customize Email Templates:**
```
Emails → All Emails
Each template has:
- Subject line
- Email body
- Tokens (dynamic content)
- HTML/Plain text versions
```

**Common Notifications:**
- New message received
- Friend request received
- Mentioned in activity
- Group invitation
- Group membership approved

#### On-Site Notifications

**Notification Display:**
```
Appears in:
- Admin bar bubble
- Profile notification page
- Toast/popup (with plugin)
- Mobile push (with app)
```

**Notification Management:**
```
Users can:
- Mark as read
- Delete notifications
- Set preferences
- Bulk actions
```

## Step 9: Reign Integration

### BuddyPress + Reign Settings

**Navigate to:** Appearance → Reign Settings → BuddyPress

#### Layout Options

**Member Directory:**
```
Display: Grid/List
Columns: 3/4/5
Card style: Modern/Classic
Show: Avatar, Name, Last active, Buttons
Per page: 20/40/60
```

**Group Directory:**
```
Display: Grid/List
Columns: 2/3/4
Show: Cover, Avatar, Description, Members
Per page: 20/40/60
```

**Activity Stream:**
```
Style: Timeline/Cards
Width: Full/Contained
Comments: Nested/Flat
Media: Lightbox/Inline
```

#### Reign-Specific Features

**Profile Headers:**
```
Style: Cover image/Pattern/Gradient
Layout: Centered/Left aligned
Elements: Avatar, Name, Badges, Stats
Navigation: Horizontal/Vertical
```

**Member Widgets:**
- Reign Member Carousel
- Reign Who's Online
- Reign Popular Members
- Reign Recent Activities

## Step 10: Moderation & Safety

### Content Moderation

#### Moderation Tools

**Akismet Integration:**
```
Settings → BuddyPress → Options
✅ Enable Akismet for BuddyPress
Checks: Activities, Comments, Messages
```

**Activity Moderation:**
```
- Report button on activities
- Admin review queue
- Auto-flag keywords
- Member blocking
```

### User Safety

**Privacy Features:**
- Block users
- Report content
- Private profiles
- Restricted messaging
- Visibility controls

**Moderation Roles:**
```
Administrator: Full control
Moderator: Content management
Member: Standard access
Restricted: Limited access
```

## Step 11: Performance Optimization

### BuddyPress Performance

#### Database Optimization

**Regular Cleanup:**
```
- Clear old notifications
- Remove spam accounts
- Clean activity meta
- Optimize tables
```

**Caching Setup:**
```
Recommended plugins:
- W3 Total Cache
- WP Rocket
- Redis Object Cache
```

#### Query Optimization

**Limit Queries:**
```
Settings → BuddyPress → Options
- Members per page: 20 (not 100)
- Activities per page: 20
- Groups per page: 20
- Avatar uploads: Limit size
```

## Step 12: Testing Your Community

### Pre-Launch Testing

#### Create Test Accounts

**Test Different Roles:**
1. Admin account (you)
2. Moderator account
3. Regular member
4. New member
5. Restricted member

#### Test User Flows

**Registration Flow:**
1. Register new account
2. Receive activation email
3. Activate account
4. Complete profile
5. Explore community

**Interaction Flow:**
1. Post activity update
2. Comment on activities
3. Send friend request
4. Join group
5. Send private message

### Launch Preparation

#### Content Seeding

**Before Opening:**
- Create 5-10 groups
- Post 20+ activities
- Add welcome content
- Create FAQs
- Set community guidelines

#### Invite Beta Users

**Soft Launch Strategy:**
1. Invite 10-20 friends
2. Gather feedback
3. Fix issues
4. Invite 50 more
5. Full launch

## Troubleshooting Common Issues

### Registration Not Working

**Check:**
1. Settings → General → Anyone can register ✓
2. BuddyPress → Options → Enable registration ✓
3. Register page exists and assigned
4. Email sending works
5. Spam protection not blocking

### Activities Not Showing

**Check:**
1. Activity component enabled
2. Activity page assigned
3. At least one activity exists
4. Permalink settings saved
5. Cache cleared

### Profile Pages 404

**Fix:**
1. Settings → Permalinks
2. Change to Plain
3. Save
4. Change back to Post name
5. Save again

### Emails Not Sending

**Solutions:**
1. Install SMTP plugin
2. Configure with service (SendGrid/Mailgun)
3. Test email delivery
4. Check spam folders

## Best Practices

### Community Guidelines

**Create Clear Rules:**
- Acceptable behavior
- Content guidelines
- Consequence for violations
- Reporting process
- Appeal process

### Engagement Strategies

**Keep Members Active:**
- Welcome new members
- Regular activities
- Challenges/contests
- Feature members
- Recognize contributions

### Growth Tactics

**Attract Members:**
- SEO optimization
- Social media integration
- Referral rewards
- Quality content
- Active moderation

## Next Steps

### Immediate Actions
1. ✅ Test all features work
2. ✅ Create welcome content
3. ✅ Set up moderation
4. ✅ Configure emails
5. ✅ Invite first members

### Week 1 Goals
- 50+ registered members
- 10+ daily activities
- 5+ active groups
- Engagement baseline set
- Feedback collected

### Month 1 Targets
- 500+ members
- 50+ daily activities
- 20+ active groups
- Community culture established
- Growth strategy refined

---

**Community Ready?** Congratulations! Your BuddyPress community is configured. Start inviting members and watch your community grow!