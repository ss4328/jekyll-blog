# DNS Setup Guide for mlxshiv.com

## Current Issue
GitHub Pages shows: "Domain does not resolve to the GitHub Pages server" - this means DNS records need to be configured.

## Step-by-Step DNS Configuration

### Option 1: Apex Domain (mlxshiv.com) - Recommended

Go to your domain registrar (where you bought mlxshiv.com) and add these **4 A records**:

| Type | Name/Host | Value | TTL |
|------|-----------|-------|-----|
| A | @ (or blank/root) | 185.199.108.153 | 3600 |
| A | @ (or blank/root) | 185.199.109.153 | 3600 |
| A | @ (or blank/root) | 185.199.110.153 | 3600 |
| A | @ (or blank/root) | 185.199.111.153 | 3600 |

**Important Notes:**
- Some registrars use `@` for the root domain, others use blank/empty
- You need ALL 4 A records (not just one)
- TTL can be 3600 (1 hour) or your registrar's default

### Option 2: CNAME (www.mlxshiv.com) - Alternative

If you prefer using `www.mlxshiv.com`:

1. Add CNAME record:
   - Type: `CNAME`
   - Name/Host: `www`
   - Value: `YOUR-USERNAME.github.io` (replace with your GitHub username)
   - TTL: 3600

2. Update `_config.yml`:
   ```yaml
   url: "https://www.mlxshiv.com"
   ```

## Common Domain Registrars - Quick Links

- **Namecheap**: DNS → Advanced DNS → Add A records
- **GoDaddy**: DNS Management → Add A records
- **Google Domains**: DNS → Custom records → Add A records
- **Cloudflare**: DNS → Add A records (disable proxy initially)
- **Name.com**: DNS Records → Add A records

## Verify DNS Configuration

After adding DNS records, verify they're working:

1. **Check DNS propagation:**
   - Visit: https://www.whatsmydns.net/#A/mlxshiv.com
   - You should see all 4 IP addresses: 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153

2. **Test from command line:**
   ```bash
   dig mlxshiv.com +short
   # Should return all 4 IP addresses
   ```

3. **Wait for propagation:**
   - DNS changes can take 5 minutes to 48 hours
   - Usually works within 1-2 hours
   - GitHub Pages may take additional time to verify

## After DNS is Configured

1. **Wait 10-30 minutes** for DNS to propagate
2. Go back to GitHub → Settings → Pages
3. Click **"Check again"** button next to the DNS error
4. Once verified, **"Enforce HTTPS"** checkbox will become available
5. Check the box to enable HTTPS

## Troubleshooting

### Still showing DNS error after 2+ hours?

1. **Double-check DNS records:**
   - Ensure all 4 A records are added (not just 1-2)
   - Verify IP addresses are exactly: 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153
   - Check for typos in the domain name

2. **Check for conflicting records:**
   - Remove any old A records pointing to different IPs
   - Remove any CNAME records for the root domain (apex domains can't use CNAME)

3. **Verify with dig:**
   ```bash
   dig mlxshiv.com A +short
   ```
   Should return exactly 4 IP addresses matching GitHub's IPs

4. **Clear DNS cache:**
   - Your computer: `sudo dscacheutil -flushcache` (Mac) or `ipconfig /flushdns` (Windows)
   - Or wait - DNS propagates globally over time

### If using Cloudflare

- **Important**: Turn OFF the proxy (orange cloud) initially
- Set DNS records to "DNS only" (gray cloud)
- After GitHub Pages verifies, you can enable Cloudflare proxy if desired

### Still not working?

1. Remove the custom domain from GitHub Pages
2. Wait 5 minutes
3. Re-add the custom domain
4. Click "Check again" after DNS propagates

## Expected Timeline

- **DNS propagation**: 5 minutes - 2 hours (usually ~30 minutes)
- **GitHub verification**: 10-30 minutes after DNS propagates
- **HTTPS certificate**: 10-30 minutes after verification
- **Total**: Usually 1-3 hours, can take up to 24 hours

## Need Help?

If DNS is correctly configured but still not working after 24 hours:
- Check GitHub Pages documentation: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
- Verify your domain registrar supports A records for apex domains
- Contact your domain registrar's support

