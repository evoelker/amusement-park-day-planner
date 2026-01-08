# Amusement Park Day Planner

A single-page web application that helps theme park guests plan their day with drag-and-drop scheduling, live wait times, and a fun spinner wheel for decision-making.


## 🎢 Features

- **Live Wait Times**: Real-time ride wait times from Queue-Times.com API
- **Drag & Drop Scheduling**: Plan your day by dragging rides into Morning, Midday, Afternoon, and Evening blocks
- **Spinner Wheel**: Can't decide? Spin the wheel to randomly select from your favorite rides
- **Favorites System**: Mark rides as favorites with a simple star toggle
- **Ride Filtering**: Filter rides by Open/Closed status
- **LocalStorage Persistence**: Save and load your plans
- **Responsive Design**: Works on desktop and mobile devices

## 🚀 Live Demo

Currently configured for **Disneyland Park (California)** with live wait times.

## 🛠️ Technology Stack

- **Frontend**: Pure HTML, CSS, and JavaScript (no frameworks)
- **API**: Queue-Times.com API with CORS proxy fallback
- **Deployment**: Azure Static Web Apps
- **Storage**: Browser LocalStorage for plan persistence

## 📦 Project Structure

```
amusement_park_day_planner/
├── index.html                    # Main application file
├── staticwebapp.config.json      # Azure Static Web Apps configuration
├── .github/
│   └── workflows/
│       └── azure-static-web-apps-deploy.yml  # CI/CD workflow
└── README.md                     # This file
```

## 🌐 Deployment to Azure Static Web Apps

### Prerequisites

- Azure account
- GitHub account
- Azure CLI (optional, for command-line deployment)

### Option 1: Deploy via Azure Portal

1. **Create a Static Web App**:
   - Go to [Azure Portal](https://portal.azure.com)
   - Click "Create a resource" → Search for "Static Web App"
   - Click "Create"

2. **Configure the deployment**:
   - **Subscription**: Select your Azure subscription
   - **Resource Group**: Create new or use existing
   - **Name**: `amusement-park-planner` (or your preferred name)
   - **Plan type**: Free
   - **Region**: Choose closest to your users
   - **Source**: GitHub
   - **GitHub account**: Authorize and select your account
   - **Organization**: Your GitHub username/org
   - **Repository**: `amusement_park_day_planner`
   - **Branch**: `main` or `master`
   
3. **Build Details**:
   - **Build Presets**: Custom
   - **App location**: `/`
   - **Api location**: (leave empty)
   - **Output location**: (leave empty)

4. Click "Review + Create" then "Create"

5. Azure will automatically:
   - Create a GitHub Actions workflow in your repository
   - Build and deploy your app
   - Provide a public URL

### Option 2: Deploy via Azure CLI

```bash
# Login to Azure
az login

# Create a resource group (if needed)
az group create --name rg-park-planner --location eastus

# Create and deploy the static web app
az staticwebapp create \
  --name amusement-park-planner \
  --resource-group rg-park-planner \
  --source https://github.com/YOUR_USERNAME/amusement_park_day_planner \
  --location eastus \
  --branch main \
  --app-location "/" \
  --login-with-github
```

### Option 3: Deploy via GitHub Actions (Manual Setup)

1. Create a GitHub repository and push your code
2. In Azure Portal, get your deployment token:
   - Navigate to your Static Web App
   - Go to "Overview" → "Manage deployment token"
   - Copy the token
3. Add the token to GitHub Secrets:
   - Go to your GitHub repo → Settings → Secrets and variables → Actions
   - Create new secret: `AZURE_STATIC_WEB_APPS_API_TOKEN`
   - Paste the deployment token
4. The GitHub Actions workflow will automatically deploy on push to main

## 🔧 Configuration

### API Configuration

The app uses the Queue-Times.com API with a CORS proxy fallback:
- **Primary**: Direct API calls to `https://queue-times.com`
- **Fallback**: CORS proxy at `https://api.allorigins.win`

To change the park, update the `DISNEYLAND_API_URL` in `index.html`:
```javascript
const DISNEYLAND_API_URL = 'https://queue-times.com/parks/16/queue_times.json';
// Change 16 to any park ID from https://queue-times.com/parks.json
```

### Azure Static Web Apps Configuration

The `staticwebapp.config.json` file configures:
- **Content Security Policy**: Allows API calls to Queue-Times.com and CORS proxy
- **Caching**: Sets cache headers for optimal performance
- **404 Handling**: Redirects to index.html for SPA behavior

## 🧪 Local Development

Simply open `index.html` in a web browser. For a better development experience with live reload:

```bash
# Using Python
python -m http.server 8000

# Using Node.js (npx)
npx http-server -p 8000

# Using PHP
php -S localhost:8000
```

Then visit `http://localhost:8000`

## 📝 API Attribution

This application uses the [Queue-Times.com API](https://queue-times.com/en-US/pages/api) for real-time theme park wait times.

**Powered by Queue-Times.com** - As required by the API terms, this attribution is displayed in the application.

## 🎨 Design

**Color Palette**:
- Sunset Coral: `#FF6F61`
- Golden Peach: `#FFB680`
- Sky Glow: `#FFDFAE`
- Twilight Purple: `#6A4FBF`
- Clean Sand: `#FAF7F2`

**Design Philosophy**: Playful, approachable, minimal cognitive load, sunset gradient aesthetic

## 📱 Browser Compatibility

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## 🔒 Privacy

- No user data is collected or sent to any server
- All schedule data is stored locally in the browser's LocalStorage
- API calls are made directly from the client to Queue-Times.com

## 📄 License

This project is open source and available for educational and personal use.

## 🤝 Contributing

This is a demo/educational project. Feel free to fork and customize for your needs!

## 🐛 Troubleshooting

### Rides not loading
- Check browser console (F12) for error messages
- Verify internet connection
- The app uses a CORS proxy as fallback if direct API access is blocked

### Plans not saving
- Ensure LocalStorage is enabled in your browser
- Check browser privacy settings
- Clear cache if issues persist

## 📞 Support

For issues with the Queue-Times API, visit [queue-times.com](https://queue-times.com/en-US/pages/api)

---

Built with ❤️ for theme park enthusiasts
