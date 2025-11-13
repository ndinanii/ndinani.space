# Deployment Instructions for ndinani.space

Your portfolio is now synced to: **https://github.com/ndinanii/ndinani.space**

## Choose Your Deployment Platform

---

## Option 1: Netlify (RECOMMENDED) ⭐

### Why Netlify?
- ✅ Easiest setup (3 minutes)
- ✅ Automatic HTTPS & CDN
- ✅ Instant rollbacks
- ✅ Deploy previews for branches
- ✅ Free tier is generous

### Setup Steps:

1. **Go to Netlify**
   - Visit: https://app.netlify.com/
   - Sign in with GitHub

2. **Import Repository**
   - Click "Add new site" → "Import an existing project"
   - Choose "Deploy with GitHub"
   - Select repository: `ndinanii/ndinani.space`

3. **Configure Build** (Auto-detected from netlify.toml)
   - Build command: `npm run build` ✅
   - Publish directory: `dist` ✅
   - Node version: 20 ✅

4. **Deploy**
   - Click "Deploy site"
   - Wait 2-3 minutes
   - Site live at: `[random-name].netlify.app`

5. **Custom Domain** (Optional)
   - Site settings → Domain management
   - Add custom domain: `ndinani.space`
   - Update DNS records with your registrar:
     ```
     Type: A
     Name: @
     Value: 75.2.60.5
     
     Type: CNAME
     Name: www
     Value: [your-site].netlify.app
     ```

### That's it! 🎉
- Auto-deploys on every push to `main`
- HTTPS automatically configured
- Site live in minutes

---

## Option 2: GitHub Pages

### Why GitHub Pages?
- ✅ Free hosting
- ✅ Integrated with GitHub
- ✅ Good for open-source portfolios

### Setup Steps:

1. **Enable GitHub Pages**
   - Go to: https://github.com/ndinanii/ndinani.space/settings/pages
   - Under "Build and deployment":
     - Source: **GitHub Actions**
   - Save

2. **Deploy Workflow** (Already created)
   - File: `.github/workflows/deploy-github-pages.yml` ✅
   - Will run automatically on next push

3. **Push Workflow to GitHub**
   ```powershell
   git add .github/workflows/deploy-github-pages.yml
   git commit -m "Add GitHub Pages deployment workflow"
   git push
   ```

4. **Wait for Deployment**
   - Go to: https://github.com/ndinanii/ndinani.space/actions
   - Watch workflow run (takes 2-3 minutes)
   - Site will be live at: `https://ndinanii.github.io/ndinani.space/`

5. **Custom Domain** (Optional)
   - Settings → Pages → Custom domain
   - Enter: `ndinani.space`
   - Create CNAME file or use GitHub UI
   - Update DNS at your registrar:
     ```
     Type: A
     Name: @
     Values: 
       185.199.108.153
       185.199.109.153
       185.199.110.153
       185.199.111.153
     
     Type: CNAME
     Name: www
     Value: ndinanii.github.io
     ```

---

## Comparison

| Feature | Netlify | GitHub Pages |
|---------|---------|--------------|
| Setup Time | 3 min | 5 min |
| Custom Domain | Easy | Moderate |
| HTTPS | Automatic | Automatic |
| Deploy Speed | Very Fast | Fast |
| Build Logs | Excellent | Good |
| Forms Support | Yes | No |
| Serverless Functions | Yes | No |
| Deploy Previews | Yes | No |
| Free Tier | 300 build min/month | Unlimited |
| Best For | Professional portfolios | Open source projects |

---

## My Recommendation: Netlify

**Start with Netlify because:**
1. Faster deployment process
2. Better build logs and debugging
3. Deploy previews for testing
4. Can always switch to GitHub Pages later

---

## Post-Deployment Checklist

After deploying to either platform:

- [ ] Visit your live URL
- [ ] Test all navigation links
- [ ] Click "My Resume" → Verify Google Drive opens
- [ ] Test social media links (LinkedIn, GitHub, YouTube, Instagram)
- [ ] Click portfolio project → Verify GitHub repo opens
- [ ] Test email links → Verify mailto works
- [ ] Test on mobile device
- [ ] Run Lighthouse audit (Chrome DevTools)
- [ ] Share your portfolio! 🚀

---

## Updating Your Site

After deployment, updating is automatic:

```powershell
# Make changes to your code
git add .
git commit -m "Update portfolio content"
git push
```

Your site redeploys automatically! ✨

---

## Troubleshooting

### Build Fails
- Check build logs on Netlify/GitHub Actions
- Verify Node version is 18+
- Test locally: `npm run build`

### Images Not Loading
- Ensure images are in `/public` folder
- Check file paths (case-sensitive)

### Links Not Working
- Verify all URLs in `src/sample.ts`
- Check navigation in `Header.astro`

---

## Support Resources

- **Netlify Docs:** https://docs.netlify.com/
- **GitHub Pages Docs:** https://docs.github.com/pages
- **Astro Deployment:** https://docs.astro.build/en/guides/deploy/

---

**Your portfolio is ready! Choose your platform and deploy in minutes.** 🎉
