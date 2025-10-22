# Deployment Guide - Master of Lessons

## Quick Start - Netlify Deployment

Your application is **production-ready** and configured for Netlify deployment!

### Method 1: Deploy to Netlify (Recommended)

#### Using Netlify CLI

1. **Install Netlify CLI** (if not already installed):
```bash
npm install -g netlify-cli
```

2. **Login to Netlify**:
```bash
netlify login
```

3. **Deploy** (from project root):
```bash
netlify deploy --prod
```

The CLI will ask you to:
- Create a new site or link to existing one
- Confirm the build directory (`dist`)

#### Using Netlify UI (Continuous Deployment)

1. **Push to GitHub**:
```bash
git init
git add .
git commit -m "Initial commit: Master of Lessons app"
git remote add origin <your-github-repo-url>
git push -u origin master
```

2. **Connect to Netlify**:
   - Go to https://app.netlify.com
   - Click "Add new site" > "Import an existing project"
   - Choose GitHub and select your repository
   - Build settings are auto-detected from `netlify.toml`:
     - Build command: `npm run build`
     - Publish directory: `dist`
   - Click "Deploy site"

3. **Your site will be live** at a Netlify URL (e.g., `https://master-of-lessons-xyz.netlify.app`)

#### Using Netlify Drop (Manual)

1. **Build locally**:
```bash
npm run build
```

2. **Deploy**:
   - Go to https://app.netlify.com/drop
   - Drag and drop the `dist` folder
   - Your site will be deployed instantly!

### Method 2: Other Hosting Platforms

#### Vercel

```bash
npm install -g vercel
vercel
```

#### GitHub Pages

1. Install gh-pages:
```bash
npm install --save-dev gh-pages
```

2. Update `package.json`:
```json
{
  "scripts": {
    "deploy": "npm run build && gh-pages -d dist"
  }
}
```

3. Update `vite.config.js` with your repo name:
```js
export default defineConfig({
  base: '/your-repo-name/',
  plugins: [react()],
})
```

4. Deploy:
```bash
npm run deploy
```

## Environment Configuration

No environment variables are needed for basic deployment. The application uses static JSON data from `/data/mod_gateway_reviews_5docs.json`.

## Build Verification

Before deploying, verify the build works:

1. **Build**:
```bash
npm run build
```

2. **Preview locally**:
```bash
npm run preview
```

Visit `http://localhost:4173` to test the production build.

## Custom Domain (Netlify)

1. Go to Site settings > Domain management
2. Add custom domain
3. Follow DNS configuration instructions

## Performance Optimization

The application is already optimized with:
- Vite's build optimization
- Code splitting
- Minification
- Tree shaking

## Troubleshooting

### Build fails
- Check Node.js version (16+ required)
- Clear `node_modules` and reinstall:
  ```bash
  rm -rf node_modules
  npm install
  ```

### 404 on refresh
- Netlify: Already configured in `netlify.toml` with SPA redirect
- Other platforms: Configure SPA redirects for client-side routing

### Blank page
- Check browser console for errors
- Verify `data/mod_gateway_reviews_5docs.json` exists
- Check base URL in `vite.config.js`

## Monitoring

After deployment, monitor:
- Build logs in Netlify dashboard
- Function logs (if using serverless functions)
- Analytics (enable in Netlify)

## Updates

To update the deployed app:

1. **Make changes**
2. **Commit and push** (for continuous deployment)
   OR
3. **Run build and deploy** (for manual deployment)

```bash
npm run build
netlify deploy --prod
```

---

**Your app is ready to deploy!** 🎸🐱🌿

Choose your preferred method above and follow the steps. The easiest way to get started is using Netlify's drag-and-drop deployment.
