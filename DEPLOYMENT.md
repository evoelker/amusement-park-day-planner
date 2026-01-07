# Deployment Checklist for Azure Static Web Apps

## Pre-Deployment

- [x] Application code complete
- [x] `index.html` created as entry point
- [x] `staticwebapp.config.json` configured
- [x] `.gitignore` file added
- [x] GitHub Actions workflow created
- [x] README.md with deployment instructions
- [ ] Update `package.json` with your GitHub username
- [ ] Test locally (run `npm start` or open index.html)

## Azure Setup

### Option 1: Via Azure Portal (Recommended for first-time)

1. Go to [portal.azure.com](https://portal.azure.com)
2. Click "Create a resource"
3. Search for "Static Web App" and click "Create"
4. Fill in:
   - **Subscription**: Your Azure subscription
   - **Resource Group**: Create new (e.g., "rg-park-planner")
   - **Name**: "amusement-park-planner"
   - **Plan**: Free
   - **Region**: East US 2 (or closest to your users)
   - **Deployment source**: GitHub
   - **Organization**: Your GitHub username
   - **Repository**: amusement_park_day_planner
   - **Branch**: main
   - **Build presets**: Custom
   - **App location**: /
   - **Output location**: (leave empty)
5. Click "Review + Create"
6. Click "Create"

### Option 2: Via Azure CLI

```bash
# Login
az login

# Create resource group
az group create --name rg-park-planner --location eastus2

# Create static web app
az staticwebapp create \
  --name amusement-park-planner \
  --resource-group rg-park-planner \
  --source https://github.com/YOUR_USERNAME/amusement_park_day_planner \
  --location eastus2 \
  --branch main \
  --app-location "/" \
  --login-with-github
```

## GitHub Setup

1. Create a new repository on GitHub:
   ```bash
   cd c:\Users\erykvoelker\repos\amusement_park_day_planner
   git init
   git add .
   git commit -m "Initial commit - Amusement Park Day Planner"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/amusement_park_day_planner.git
   git push -u origin main
   ```

2. If using Manual GitHub Actions setup:
   - Get deployment token from Azure Portal (Static Web App → Manage deployment token)
   - Add to GitHub Secrets: Settings → Secrets → Actions → New repository secret
   - Name: `AZURE_STATIC_WEB_APPS_API_TOKEN`
   - Value: (paste the token)

## Post-Deployment

- [ ] Verify the site is live at the Azure-provided URL
- [ ] Test all features:
  - [ ] Rides load from API
  - [ ] Drag and drop works
  - [ ] Favorites toggle works
  - [ ] Spinner works
  - [ ] Save/Load plans work
  - [ ] Mobile responsive
- [ ] Configure custom domain (optional)
- [ ] Set up Application Insights for monitoring (optional)

## Custom Domain (Optional)

1. In Azure Portal, go to your Static Web App
2. Click "Custom domains"
3. Click "Add"
4. Enter your domain name
5. Follow instructions to add DNS records

## Monitoring

- View deployment logs in GitHub Actions tab
- Check Application logs in Azure Portal → Static Web App → Log stream
- Monitor usage in Azure Portal → Static Web App → Metrics

## Troubleshooting

### Deployment fails
- Check GitHub Actions logs
- Verify `staticwebapp.config.json` syntax
- Ensure `AZURE_STATIC_WEB_APPS_API_TOKEN` secret is set

### Site shows 404
- Verify `index.html` is in root directory
- Check `staticwebapp.config.json` routes configuration

### API calls fail
- Check browser console for CORS errors
- Verify CSP headers in `staticwebapp.config.json`
- CORS proxy fallback should handle most issues

## Updating the Site

After deployment, updates are automatic:
```bash
git add .
git commit -m "Update feature"
git push
```

GitHub Actions will automatically rebuild and deploy within 2-5 minutes.

## Cost

- **Free tier includes**:
  - 100 GB bandwidth per month
  - 0.5 GB storage
  - 2 custom domains
  - Automatic SSL certificates
  - Global CDN
  - GitHub Actions build minutes

Perfect for this project! No costs expected for normal usage.

## Support

- [Azure Static Web Apps Documentation](https://docs.microsoft.com/en-us/azure/static-web-apps/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Queue-Times API Docs](https://queue-times.com/en-US/pages/api)
