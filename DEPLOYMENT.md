# 🚀 Deployment Guide

Complete instructions for publishing Workout Tracker online.

## Option 1: GitHub Pages (Recommended - FREE)

### Setup Repository
1. Create GitHub account at github.com
2. Create new repository named `workout-tracker`
3. Don't initialize with README (you already have one)

### Push Your Code
```bash
cd workout-tracker
git init
git add .
git commit -m "Initial commit: Workout Tracker v1.0.0"
git remote add origin https://github.com/YOUR_USERNAME/workout-tracker.git
git branch -M main
git push -u origin main
```

### Enable GitHub Pages
1. Go to repo → **Settings** → **Pages**
2. Under "Source", select **main** branch
3. Click **Save**
4. Wait 1-2 minutes
5. Your app is live at: `https://YOUR_USERNAME.github.io/workout-tracker/`

### Custom Domain (Optional)
1. Buy domain (Namecheap, Google Domains, etc.)
2. Go to repo Settings → Pages
3. Enter domain under "Custom domain"
4. Follow DNS instructions provided

---

## Option 2: Netlify (FREE Alternative)

Faster deploys with more features.

### Deploy with Git
1. Go to netlify.com
2. Sign up with GitHub
3. Click "New site from Git"
4. Select your `workout-tracker` repository
5. Click **Deploy site**
6. Live at: `https://random-name-xyz.netlify.app`

### Or Deploy Manually
```bash
# Install Netlify CLI
npm i -g netlify-cli

# Deploy current directory
netlify deploy --prod --dir .
```

### Custom Domain
1. After deployment, go to **Domain settings**
2. Click "Add custom domain"
3. Enter your domain
4. Update DNS records

---

## Option 3: Vercel (FREE)

Optimized for web apps.

### Deploy
```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

Live instantly at a Vercel subdomain.

---

## Option 4: Self-Hosted Server

For your own VPS or hosting account.

### Via FTP/SFTP
1. Connect with FileZilla or WinSCP
2. Upload all files to `public_html/` or `www/`
3. Access at your domain

### Via Git
```bash
# On your server
cd /var/www/html
git clone https://github.com/YOUR_USERNAME/workout-tracker.git
```

### Nginx Configuration
```nginx
server {
    listen 80;
    server_name workout-tracker.com;
    
    location / {
        root /var/www/html/workout-tracker;
        try_files $uri /index.html;
    }
}
```

### Apache Configuration
Create `.htaccess`:
```apache
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

---

## Important: SSL/HTTPS

PWAs **require HTTPS** to work.

✅ **Included by default:**
- GitHub Pages: HTTPS ✅
- Netlify: HTTPS ✅
- Vercel: HTTPS ✅

⚠️ **Self-hosted:**
Use Let's Encrypt (free):
```bash
sudo certbot certonly --standalone -d workout-tracker.com
```

---

## Post-Deployment Checklist

After going live, verify:

- [ ] App loads at your domain
- [ ] Install button shows in browser
- [ ] Can install to home screen on mobile
- [ ] Works offline (disable WiFi, test)
- [ ] localStorage persists data
- [ ] Workout logging works
- [ ] Progress charts display
- [ ] Theme switching works

### Test PWA Features
1. Open DevTools (F12)
2. Go to **Application** tab
3. Check **Service Workers**: Should show "registered"
4. Check **Storage**: Should see localStorage keys
5. Go **Offline** and refresh - should still work

---

## Performance Tips

### Measure Performance
Open DevTools → **Lighthouse** → Run audit
- Look for Performance, Accessibility scores
- Fix any warnings

### Optimize
- App is already minified (single HTML file)
- No images or large assets to load
- Fast on 4G networks

### Monitor
- Use Google Analytics (optional) to track usage
- Use Uptime Robot (free) to monitor 24/7

---

## Git Workflow for Updates

### Make Changes Locally
```bash
cd workout-tracker
# Edit index.html or other files
git add .
git commit -m "Add new feature"
git push origin main
```

**GitHub Pages & Netlify** automatically redeploy on push.

### Rollback if Needed
```bash
git log --oneline           # See history
git revert COMMIT_ID        # Undo a change
git push origin main        # Deploy rollback
```

---

## SEO & Discovery

### Submit to Google
1. Go to google.com/search-console
2. Add your domain
3. Google indexes your app

### Meta Tags (Already Included)
- Description: ✅
- Theme color: ✅
- Viewport: ✅

### Optional Enhancements
- Create `sitemap.xml` for search engines
- Create `robots.txt` to control crawling
- Submit to fitness app directories

---

## Analytics (Optional)

### Add Google Analytics
Insert before `</head>`:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script>
```

Replace `GA_MEASUREMENT_ID` with your ID from Google Analytics.

---

## Continuous Deployment (GitHub Actions)

Auto-deploy when you push to main:

Create `.github/workflows/deploy.yml`:
```yaml
name: Deploy PWA

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./
```

---

## Troubleshooting

### Site not loading
- [ ] Check DNS propagation: whatsmydns.net
- [ ] Wait 24-48 hours for DNS to fully propagate
- [ ] Verify A record points to correct IP

### Install button not showing
- [ ] Verify HTTPS is enabled
- [ ] Check Service Worker in DevTools
- [ ] Try different browser

### Data not persisting
- [ ] Check localStorage in DevTools
- [ ] Ensure localStorage is enabled
- [ ] Try incognito mode
- [ ] Clear site data: Settings → Clear browsing data

### Slow performance
- [ ] Check internet speed
- [ ] Use browser DevTools Network tab
- [ ] Enable gzip compression on server
- [ ] Use CDN for static files

---

## Support & Help

- GitHub Issues: yourusername/workout-tracker/issues
- Email: your.email@example.com
- Twitter: @yourhandle

---

**You're ready to deploy! 🚀**
