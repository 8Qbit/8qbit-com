# 8Qbit.com - Paul Nylund CV

A personal CV/portfolio website with a retro pixel art style inspired by LucasArts' classic adventure game "Day of the Tentacle". Features a SCUMM-style interface, CRT TV effects.

The site was "vibe coded" with Cursor and Claude Opus 4.5. The initial project took around 5 hours.

You can see the live site **[Here](https://8qbit.com/)** 

## 🎮 Features

- **Retro SCUMM Interface** - Navigation styled like classic LucasArts adventure games
- **CRT TV Effects** - Scanlines, vignette, and channel-change animations
- **Interactive Profile** - Click the Purple Tentacle to reveal the real photo
- **Gold Shimmer Effect** - Elegant highlight animation on the profile frame
- **Responsive Design** - Works on desktop and mobile devices
- **Pixel Art Aesthetic** - Custom pixel-perfect borders and styling

## 🛠️ Technologies Used

- **[Svelte 5](https://svelte.dev/)** - Modern reactive frontend framework
- **[Vite](https://vitejs.dev/)** - Fast build tool and development server
- **CSS3** - Custom animations, TV effects, and pixel art styling
- **[Firebase Hosting](https://firebase.google.com/docs/hosting)** - Static site hosting

## 📁 Project Structure

```
8qbit-com/
├── public/
│   └── images/
│       ├── purple-tentacle.png   # Profile mascot image
│       └── paul.jpg              # Real profile photo
├── src/
│   ├── lib/
│   │   ├── components/
│   │   │   └── PurpleTentacle.svelte  # Flip card profile component
│   │   ├── data/
│   │   │   └── cv.json                # CV content data
│   │   └── styles/
│   │       └── pixel-art.css          # Global pixel art styles
│   ├── App.svelte                     # Main application component
│   └── main.js                        # Application entry point
├── firebase.json                      # Firebase hosting configuration
├── .firebaserc                        # Firebase project settings
└── package.json
```

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or higher)
- [npm](https://www.npmjs.com/) or [pnpm](https://pnpm.io/)
- [Firebase CLI](https://firebase.google.com/docs/cli) (for deployment)

### Installation

```bash
# Clone the repository
git clone https://github.com/8Qbit/8qbit-com.git
cd 8qbit-com

# Install dependencies
npm install
```

### Development

```bash
# Start development server
npm run dev

# The site will be available at http://localhost:5173
```

### Building for Production

```bash
# Create production build
npm run build

# Preview production build locally
npm run preview
```

## ✏️ Updating Content

### CV Data

Edit `src/lib/data/cv.json` to update your CV information:

```json
{
  "name": "Your Name",
  "title": "Your Title",
  "tagline": "Your tagline",
  "summary": "Your professional summary...",
  "experience": [...],
  "education": [...],
  "skills": {...},
  "contact": {
    "email": "your@email.com",
    "linkedin": "linkedin.com/in/yourprofile",
    "github": "github.com/yourusername"
  }
}
```

### Profile Images

Replace the images in `public/images/`:
- `purple-tentacle.png` - Main profile avatar
- `paul.jpg` - Photo revealed on click

### Contact Links

Edit the contact section in `src/App.svelte` to update social links (search for `contact-grid`).

## 🔥 Deploying to Firebase

### First-Time Setup

1. **Install Firebase CLI** (if not already installed):
   ```bash
   npm install -g firebase-tools
   ```

2. **Login to Firebase**:
   ```bash
   firebase login
   ```

3. **Initialize Firebase** (if not already configured):
   ```bash
   firebase init hosting
   ```
   - Select your Firebase project or create a new one
   - Set public directory to `dist`
   - Configure as single-page app: Yes
   - Don't overwrite `index.html`

### Deployment

```bash
# Build the project
npm run build

# Deploy to Firebase
firebase deploy
```

Or deploy in one command:
```bash
npm run build && firebase deploy
```

### Firebase Configuration

The project includes pre-configured Firebase files:

**firebase.json**:
```json
{
  "hosting": {
    "public": "dist",
    "ignore": ["firebase.json", "**/.*", "**/node_modules/**"],
    "rewrites": [
      {
        "source": "**",
        "destination": "/index.html"
      }
    ]
  }
}
```

**.firebaserc**:
```json
{
  "projects": {
    "default": "your-firebase-project-id"
  }
}
```

### Automatic Deployment (GitHub Actions)

The project includes a GitHub Actions workflow that automatically deploys to Firebase when you push or merge to the `main` branch.

#### Setup GitHub Actions for Firebase

1. **Generate Firebase Service Account Key**:
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Select your project
   - Go to **Project Settings** → **Service accounts**
   - Click **Generate new private key**
   - Download the JSON file

2. **Add GitHub Secrets**:
   
   Go to your GitHub repository → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**
   
   Add these secrets:
   
   | Secret Name | Value |
   |-------------|-------|
   | `FIREBASE_SERVICE_ACCOUNT` | Paste the entire contents of the downloaded JSON key file |
   | `FIREBASE_PROJECT_ID` | Your Firebase project ID (e.g., `my-cv-site-12345`) |

3. **Push to main branch**:
   ```bash
   git add .
   git commit -m "Your changes"
   git push origin main
   ```

The workflow will automatically:
- Build the project
- Deploy to Firebase Hosting

#### Workflow Features

- **On push to main**: Deploys directly to production (live channel)
- **On pull request**: Creates a preview deployment URL for testing

You can monitor deployments in the **Actions** tab of your GitHub repository.

## 🎨 Customization

### Colors

Edit CSS variables in `src/lib/styles/pixel-art.css`:

```css
:root {
  --purple-main: #7B2D8E;
  --scumm-bg: #1a0a2e;
  --text-gold: #FFD700;
  /* ... more variables */
}
```

### TV Effects

Adjust CRT effects in `src/lib/styles/pixel-art.css`:
- Scanline intensity
- Vignette strength
- Flicker animations

## 📄 License

This project is personal portfolio code. Feel free to use it as inspiration for your own CV site.

## 🙏 Credits

- **Day of the Tentacle** - LucasArts (inspiration for the visual style)
- **Purple Tentacle** character design - LucasArts
- Built with ❤️ using Svelte and Vite 
