# Deployment Guide for ndinani.space

## Pre-Deployment Status: ✅ READY

---

## Deployment Options

### Option 1: Netlify (Recommended)
**Pros:** Free tier, automatic builds, easy setup, custom domain support

#### Steps:
1. Push code to GitHub repository
   ```powershell
   git init
   git add .
   git commit -m "Initial commit: Salesforce portfolio"
   git remote add origin https://github.com/ndinanii/ndinani.space.git
   git push -u origin main
   ```

2. Connect to Netlify
   - Go to https://app.netlify.com/
   - Click "Add new site" > "Import an existing project"
   - Connect to GitHub and select your repository

3. Configure build settings:
   - **Build command:** `npm run build`
   - **Publish directory:** `dist`
   - **Node version:** 18 or higher

4. Deploy
   - Click "Deploy site"
   - Wait for build to complete
   - Your site will be live at `[random-name].netlify.app`

5. Custom domain (optional)
   - Go to "Domain settings"
   - Add custom domain: `ndinani.space`
   - Follow DNS configuration instructions

---

### Option 2: Vercel
**Pros:** Excellent performance, automatic previews, free tier

#### Steps:
1. Push code to GitHub (see Option 1 Step 1)

2. Connect to Vercel
   - Go to https://vercel.com/
   - Click "Add New Project"
   - Import your GitHub repository

3. Configure:
   - **Framework Preset:** Astro
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist`
   - **Install Command:** `npm install`

4. Deploy
   - Click "Deploy"
   - Site will be live at `[project-name].vercel.app`

---

### Option 3: GitHub Pages
**Pros:** Free, integrated with GitHub, simple setup

#### Steps:
1. Update `astro.config.mjs`:
   ```javascript
   export default defineConfig({
     site: 'https://ndinanii.github.io',
     base: '/ndinani.space',
   });
   ```

2. Create deployment workflow:
   ```powershell
   New-Item -ItemType Directory -Path .github/workflows -Force
   ```

3. Create `.github/workflows/deploy.yml`:
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches: [ main ]

   permissions:
     contents: read
     pages: write
     id-token: write

   jobs:
     build:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@v3
         
         - name: Setup Node
           uses: actions/setup-node@v3
           with:
             node-version: 18
         
         - name: Install dependencies
           run: npm ci
         
         - name: Build
           run: npm run build
         
         - name: Upload artifact
           uses: actions/upload-pages-artifact@v1
           with:
             path: ./dist

     deploy:
       needs: build
       runs-on: ubuntu-latest
       environment:
         name: github-pages
         url: ${{ steps.deployment.outputs.page_url }}
       steps:
         - name: Deploy to GitHub Pages
           id: deployment
           uses: actions/deploy-pages@v1
   ```

4. Enable GitHub Pages:
   - Go to repository Settings > Pages
   - Source: "GitHub Actions"
   - Save

5. Push code:
   ```powershell
   git add .
   git commit -m "Add GitHub Pages deployment"
   git push
   ```

---

## Pre-Deployment Checklist

### ✅ Code Quality
- [x] Build completes without errors
- [x] No security vulnerabilities (npm audit: 0)
- [x] All broken imports fixed
- [x] Unused assets removed

### ✅ Content Verification
- [x] Personal information correct (NDINANI, email, social links)
- [x] All navigation links working
- [x] Case study content complete
- [x] Portfolio projects configured

### ✅ Security & Privacy
- [x] Personal files excluded (.gitignore configured)
- [x] No sensitive data in codebase
- [x] External links use HTTPS
- [x] Email uses secure mailto: protocol

### ✅ SEO & Meta
- [x] Page title set ("ndinani")
- [x] Favicon configured (cloud-icon.svg)
- [ ] Consider adding meta description (optional)
- [ ] Consider adding Open Graph tags (optional)

---

## Post-Deployment Testing

### After site goes live, test:

1. **Homepage Load**
   - Site loads without errors
   - All sections visible
   - Images display correctly

2. **Navigation**
   - All menu links work
   - Resume opens Google Drive
   - Email link opens mail client

3. **External Links**
   - GitHub repository accessible
   - Social media links work
   - Resume document opens

4. **Mobile Responsive**
   - Test on mobile device
   - Menu toggle works
   - Content readable

5. **Performance**
   - Run Lighthouse audit
   - Check load times
   - Verify image optimization

---

## Environment Variables (If Needed)

For this project, no environment variables are required. However, if you add analytics or third-party services later:

### Netlify:
- Go to Site settings > Environment variables
- Add key-value pairs

### Vercel:
- Go to Project settings > Environment Variables
- Add variables for Production

### GitHub Pages:
- Use repository Secrets for sensitive data
- Access via workflow: `${{ secrets.SECRET_NAME }}`

---

## Domain Configuration

### If using custom domain (ndinani.space):

1. **Purchase domain** from registrar (Namecheap, GoDaddy, etc.)

2. **Configure DNS records:**
   
   For Netlify:
   ```
   Type: A
   Name: @
   Value: 75.2.60.5
   
   Type: CNAME
   Name: www
   Value: [your-site].netlify.app
   ```

   For Vercel:
   ```
   Type: A
   Name: @
   Value: 76.76.21.21
   
   Type: CNAME
   Name: www
   Value: cname.vercel-dns.com
   ```

3. **SSL Certificate:**
   - Netlify & Vercel provide free auto-renewing SSL
   - Will be active within minutes after DNS propagation

---

## Continuous Deployment

Once connected to GitHub:

1. **Automatic deploys** on every push to main branch
2. **Preview deployments** for pull requests
3. **Rollback capability** to previous versions
4. **Build logs** for debugging

---

## Monitoring & Analytics (Optional)

### Add Google Analytics:
1. Create GA4 property
2. Add tracking script to `Layout.astro` in `<head>`
3. Deploy update

### Add Simple Analytics (Privacy-friendly):
1. Sign up at simpleanalytics.com
2. Add script tag to Layout.astro
3. No cookies, GDPR compliant

---

## Troubleshooting Common Issues

### Build fails on deployment:
- Check Node version (needs 18+)
- Verify `package.json` scripts
- Review build logs for errors

### Images not loading:
- Ensure images in `/public` folder
- Check image paths (case-sensitive)
- Verify Sharp is installed

### 404 errors:
- Check routing configuration
- Verify base path in `astro.config.mjs`
- Ensure all files in `dist/` folder

### Slow load times:
- Run `npm run build` to optimize
- Check image sizes (compress if needed)
- Enable CDN on hosting platform

---

## Recommended: Netlify Deployment

**Why Netlify?**
- Easiest setup for Astro projects
- Excellent free tier
- Automatic HTTPS
- Built-in form handling (for contact forms)
- Great performance

**Expected deployment time:** 2-5 minutes  
**Cost:** Free (with generous limits)

---

## Next Steps After Deployment

1. ✅ Deploy to chosen platform
2. ✅ Test all functionality on live site
3. ✅ Run Lighthouse audit
4. ✅ Share portfolio URL on LinkedIn
5. ✅ Update GitHub profile with portfolio link
6. ✅ Monitor analytics for visitors

---

**Deployment Status:** Ready for production  
**Recommended Platform:** Netlify or Vercel  
**Estimated Setup Time:** 10-15 minutes
