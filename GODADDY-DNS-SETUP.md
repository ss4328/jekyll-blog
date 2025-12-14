# GoDaddy DNS Setup for mlxshiv.com → GitHub Pages

## Current Situation
You have an A record for `@` pointing to "WebsiteBuilder Site" - this needs to be changed to GitHub Pages IP addresses.

## Step-by-Step Instructions for GoDaddy

### Step 1: Remove/Edit the Existing A Record

1. In your GoDaddy DNS management page, find the A record:
   - **Type**: A
   - **Name**: @
   - **Data**: WebsiteBuilder Site

2. Click the **Edit** button (pencil icon) for this record

3. You have two options:

   **Option A: Edit the existing record** (if GoDaddy allows)
   - Change the Data/Value from "WebsiteBuilder Site" to: `185.199.108.153`
   - Save

   **Option B: Delete and recreate** (recommended)
   - Click **Delete** to remove the old record
   - Then proceed to Step 2

### Step 2: Add 4 GitHub Pages A Records

You need to add **4 separate A records** for the root domain (`@`):

1. Click **Add** or **Add Record** button

2. **First A Record:**
   - **Type**: A
   - **Name**: @
   - **Data/Value**: `185.199.108.153`
   - **TTL**: 1 Hour (or default)
   - Click **Save**

3. **Second A Record:**
   - Click **Add** again
   - **Type**: A
   - **Name**: @
   - **Data/Value**: `185.199.109.153`
   - **TTL**: 1 Hour
   - Click **Save**

4. **Third A Record:**
   - Click **Add** again
   - **Type**: A
   - **Name**: @
   - **Data/Value**: `185.199.110.153`
   - **TTL**: 1 Hour
   - Click **Save**

5. **Fourth A Record:**
   - Click **Add** again
   - **Type**: A
   - **Name**: @
   - **Data/Value**: `185.199.111.153`
   - **TTL**: 1 Hour
   - Click **Save**

### Step 3: Update www CNAME (Optional but Recommended)

Your current `www` CNAME points to `mlxshiv.com.` which is fine, but you can also point it directly to GitHub Pages:

1. Find the CNAME record:
   - **Type**: CNAME
   - **Name**: www
   - **Data**: mlxshiv.com.

2. Click **Edit**

3. Change the **Data/Value** to: `YOUR-USERNAME.github.io` (replace with your actual GitHub username, e.g., `ss4328.github.io`)

4. Click **Save**

**Note**: The `www` CNAME pointing to `mlxshiv.com.` will also work, but pointing directly to GitHub is cleaner.

### Step 4: Keep the GitHub Verification Record

**DO NOT DELETE** the TXT record:
- **Type**: TXT
- **Name**: `_github-pages-challenge-ss4328`
- **Data**: `cf984d952c249b08c72f8c3c8868ed`

This is GitHub's verification record - it should stay there.

### Step 5: Final DNS Records Should Look Like:

After setup, you should have:

| Type | Name | Data | TTL |
|------|------|------|-----|
| A | @ | 185.199.108.153 | 1 Hour |
| A | @ | 185.199.109.153 | 1 Hour |
| A | @ | 185.199.110.153 | 1 Hour |
| A | @ | 185.199.111.153 | 1 Hour |
| CNAME | www | mlxshiv.com. (or YOUR-USERNAME.github.io) | 1 Hour |
| TXT | _github-pages-challenge-ss4328 | cf984d952c249b08c72f8c3c8868ed | 1 Hour |
| NS | @ | ns59.domaincontrol.com. | (system) |
| NS | @ | ns60.domaincontrol.com. | (system) |
| SOA | @ | (system record) | (system) |

## After Making Changes

1. **Wait 10-30 minutes** for DNS to propagate
2. Verify DNS is working:
   - Visit: https://www.whatsmydns.net/#A/mlxshiv.com
   - You should see all 4 GitHub IP addresses
3. Go to GitHub → Settings → Pages
4. Click **"Check again"** button
5. Once verified, the **"Enforce HTTPS"** checkbox will become available
6. Check the box to enable HTTPS

## Troubleshooting

### GoDaddy won't let me add multiple A records with the same name?

Some GoDaddy interfaces require you to add them one at a time. Make sure you:
- Click "Add" or "Add Record" for each new A record
- Don't try to edit the same record multiple times

### Still showing "WebsiteBuilder Site" after changes?

- DNS changes can take time to propagate
- Clear your browser cache
- Try checking DNS from a different network/device
- Use https://www.whatsmydns.net/#A/mlxshiv.com to check global propagation

### Can't find the Edit/Delete buttons?

- Make sure you're in the DNS Management section
- Some GoDaddy interfaces show a dropdown menu (three dots) instead of buttons
- Try refreshing the page

## Expected Timeline

- **GoDaddy DNS update**: Immediate (but may take a few minutes to show in interface)
- **DNS propagation**: 10-30 minutes (can take up to 2 hours)
- **GitHub verification**: 10-30 minutes after DNS propagates
- **HTTPS certificate**: 10-30 minutes after verification

## Quick Reference: GitHub Pages IP Addresses

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Copy-paste these exactly as shown (no spaces, no extra characters).

