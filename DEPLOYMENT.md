# Deployment Guide for mlxshiv.com

This guide will help you deploy your Jekyll Chirpy blog to **mlxshiv.com** using GitHub Pages.

## Prerequisites

- ✅ Your repository is forked on GitHub
- ✅ You have push access to your repository
- ✅ You own the domain `mlxshiv.com` and have access to DNS settings

## Step 1: Update Site Configuration

The `_config.yml` file has been updated with your domain URL:
- `url: "https://mlxshiv.com"`

**Optional:** Update other settings in `_config.yml`:
- `title`: Your blog title
- `tagline`: Your blog subtitle
- `description`: SEO description
- `timezone`: Your timezone (currently set to `Asia/Shanghai`)
- `social.name`: Your full name
- `social.email`: Your email address
- `social.links`: Your social media profiles
- `github.username`: Your GitHub username

## Step 2: Enable GitHub Pages with GitHub Actions

1. Go to your GitHub repository
2. Click on **Settings** tab
3. In the left sidebar, click **Pages**
4. Under **Source**, select **GitHub Actions** from the dropdown (NOT "Deploy from a branch")
5. Save the settings

## Step 3: Configure Custom Domain

1. Still in the **Pages** settings, scroll down to **Custom domain**
2. Enter: `mlxshiv.com`
3. Check **Enforce HTTPS** (this will be available after DNS is configured)
4. Click **Save**

## Step 4: Configure DNS Settings

You need to configure DNS records with your domain registrar. Choose **ONE** of the following methods:

### Option A: Apex Domain (Recommended for mlxshiv.com)

Add the following DNS records:

**Type: A**
- Name: `@` (or root domain)
- Value: `185.199.108.153`
- TTL: 3600 (or default)

**Type: A**
- Name: `@` (or root domain)
- Value: `185.199.109.153`
- TTL: 3600 (or default)

**Type: A**
- Name: `@` (or root domain)
- Value: `185.199.110.153`
- TTL: 3600 (or default)

**Type: A**
- Name: `@` (or root domain)
- Value: `185.199.111.153`
- TTL: 3600 (or default)

### Option B: CNAME (Alternative - requires www subdomain)

If you prefer to use `www.mlxshiv.com`:

**Type: CNAME**
- Name: `www`
- Value: `your-username.github.io` (replace with your GitHub username)
- TTL: 3600 (or default)

Then update `_config.yml`:
```yaml
url: "https://www.mlxshiv.com"
```

## Step 5: Push Changes and Deploy

1. Commit and push your changes to GitHub:
   ```bash
   git add .
   git commit -m "Configure site for mlxshiv.com deployment"
   git push origin main
   ```
   (Replace `main` with `master` if that's your default branch)

2. Go to the **Actions** tab in your GitHub repository
3. You should see the "Build and Deploy" workflow running
4. Wait for it to complete (usually takes 2-5 minutes)

## Step 6: Verify Deployment

1. After the workflow completes successfully, wait 10-20 minutes for DNS propagation
2. Visit `https://mlxshiv.com` in your browser
3. If you see your site, you're done! 🎉

## Troubleshooting

### DNS Not Working
- DNS changes can take up to 48 hours to propagate, but usually happen within a few hours
- Use tools like [whatsmydns.net](https://www.whatsmydns.net) to check DNS propagation
- Verify your DNS records are correct with your domain registrar

### HTTPS Not Available
- Wait for DNS to fully propagate
- GitHub Pages needs to verify domain ownership before enabling HTTPS
- This can take a few hours after DNS is configured

### Build Failures
- Check the **Actions** tab for error messages
- Ensure `Gemfile.lock` is committed (if you're on a non-Linux machine, run: `bundle lock --add-platform x86_64-linux`)
- Verify all required dependencies are in `Gemfile`

### Site Not Updating
- Clear your browser cache
- Check if the GitHub Actions workflow completed successfully
- Verify you pushed to the correct branch (`main` or `master`)

## Alternative Deployment Options

If you prefer not to use GitHub Pages, you can deploy to:

- **Netlify**: Connect your GitHub repo, set build command: `bundle exec jekyll build`, publish directory: `_site`
- **Vercel**: Similar setup to Netlify
- **Cloudflare Pages**: Connect repo, build command: `bundle exec jekyll build`, output directory: `_site`
- **Self-hosted**: Build locally with `JEKYLL_ENV=production bundle exec jekyll build` and upload `_site` folder

## Next Steps

After deployment:
1. ✅ Test all pages and links
2. ✅ Set up analytics (Google Analytics, etc.) in `_config.yml`
3. ✅ Configure comments (Disqus, Giscus, or Utterances) if desired
4. ✅ Add your avatar image to `/assets/img/commons/avatar.jpg`
5. ✅ Customize the theme colors and styles if needed
6. ✅ Write your first blog post!

## Resources

- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Chirpy Theme Wiki](https://github.com/cotes2020/jekyll-theme-chirpy/wiki)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Custom Domain on GitHub Pages](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

