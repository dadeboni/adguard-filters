# AdGuard Allowlist

An AdGuard Home allowlist focused on enabling work-related services and essential functionality on mobile devices while maintaining ad blocking elsewhere.

## Overview

This allowlist is designed to:
- Enable critical work services (AWS, Microsoft 365, Slack, etc.)
- Allow streaming services (Apple Music, TikTok)
- Prevent breaking important functionality (Reddit, Facebook Graph API, banking sites)
- Support device-specific rules for different users and VPN connections
- Use client tags for child safety controls

## What's Included

### Work & Productivity Services
- **Amazon/AWS**: Full AWS ecosystem, Amazon corporate domains
- **Microsoft**: Office 365, Teams, OneDrive, SharePoint, Azure, Outlook
- **Communication**: Slack, email tracking links (Anthem, Intuit, etc.)
- **Finance**: Bank of America, TurboTax, Instacart

### Consumer Services
- **Social Media**: Reddit, Facebook Graph API
- **Streaming**: Apple Music, TikTok (device-specific)
- **Shopping**: eBay tracking services
- **Apple Services**: iCloud, push notifications, location services, device management

### Device-Specific Rules
Rules are configured for specific clients:
- **Dom's iPhone**: TikTok services, Apple Music, analytics
- **Tailscale VPN**: TikTok services, Apple Music, Reddit
- **Specific IP (192.168.86.27)**: Reddit analytics, app analytics
- **Child User Tag**: Gaming ads, Firebase services with safety controls

## Installation

### Adding to AdGuard Home

1. Copy the contents of the allowlist file
2. Navigate to **Filters → Custom filtering rules** in your AdGuard Home dashboard
3. Paste the rules into the text box
4. Click **Save**

### Adding as a Filter List

Alternatively, you can add this as a custom filter list:

1. Go to **Filters → DNS allowlists**
2. Click **Add allowlist → Add a custom list**
3. Enter the URL to this repository's raw file
4. Click **Save**

## Customizing for Your Setup

### Changing Client Names

Many rules in this list use `$client='Client Name'` to apply rules to specific devices. You'll need to update these to match your device names in AdGuard Home.

**Find your client names:**
1. Go to **Settings → DNS settings → Client tags and blocked services**
2. Look at your configured client names

**Update the rules:**
Replace client names in the rules:
- `Dom's Iphone` → Your iPhone name
- `Tailscale VPN` → Your VPN client name
- `192.168.86.27` → Your device's IP address

**Example:**
```
# Original rule
@@||tiktokcdn-us.com^$client='Dom's Iphone'

# Change to your device
@@||tiktokcdn-us.com^$client='My iPhone'
```

### Removing Client-Specific Rules

If you don't need device-specific rules, you can either:
1. Delete the `$client='...'` portion to apply the rule globally
2. Remove entire sections you don't need (like TikTok if you don't use it)

### Using Client Tags

Some rules use `$ctag='user_child'` for parental controls. To use these:

1. Set up client tags in **Settings → Client tags**
2. Assign the `user_child` tag to appropriate devices
3. Keep or remove these rules based on your needs

## Rule Syntax

Rules use AdGuard Home syntax:
- `@@||domain.com^$important` - Allowlist rule (unblocks domain)
- `||domain.com^$important` - Blocklist rule (blocks domain)
- `$client='name'` - Apply rule to specific client
- `$ctag='tag'` - Apply rule to clients with specific tag
- `*.domain.com` - Wildcard for all subdomains

## Important Notes

- Rules marked with `$important` take priority over other filters
- Wildcard rules (`*`) allow all subdomains
- Test rules after adding to ensure services work as expected
- Some rules are redundant (both wildcard and specific domains) for reliability

## Contributing

If you find issues or have suggestions for additional services that should be allowed, feel free to open an issue or submit a pull request.

## License

This is free and unencumbered software released into the public domain. Use it however you'd like.

---

**Last Updated:** January 20, 2026