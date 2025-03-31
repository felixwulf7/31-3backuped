# PsyGaming Lab Website - Technical Reference

## Project Overview
PsyGaming Lab Website is a Next.js 14 application providing therapeutic gaming experiences with psychology-focused content. Built with React 18, TypeScript, and Tailwind CSS, it features multilingual support (English/German), responsive design, and embedded HTML5 games.

## Architecture
```
app/
├── [lang]/                  # Language routes (en, de)
│   ├── [serviceSlug]/       # Service pages
│   │   └── [gameSlug]/      # Game category pages
│   ├── games/play/          # Game player
│   └── contact/             # Contact page
├── components/              # UI components
├── config/                  # Configuration files
└── utils/                   # Helpers and translations
public/
└── games/                   # HTML game files
```

### Key Design Patterns
- **Routing**: Next.js App Router with dynamic routes
- **Internationalization**: URL-based language segments `/[lang]/`  
- **Component Composition**: Reusable UI elements
- **Static Data**: Configuration-driven content

## Core Components
- **Header/Footer**: Site navigation and branding
- **Hero/HeroSection**: Landing page and section headers
- **FeatureCard/ContentBlock**: Content display components
- **LanguageSwitcher**: Language toggle maintaining current path
- **Game-specific**: BenefitCard, StepCard, CallToAction

## Game Integration
Games are HTML files stored in `public/games/` and configured in `app/config/games.ts`:

```typescript
{
  id: 'game-id',
  nameKey: 'translationKey', 
  categoryId: 'category',
  filePath: '/games/game-file.html',
  // Other metadata
}
```

Games are embedded using iframes and accessible via:
- `/[lang]/games/play?game=[gameId]` - Direct play
- `/[lang]/[serviceSlug]/[gameSlug]` - Category pages

## Deployment Options

### Local Development
```bash
# Install dependencies
npm install

# Start development server (port 3000)
npm run dev

# Build for production
npm run build

# Run production server (port 3001)
npm run start
```

### Production Deployment
**Option 1: Vercel** (Recommended)
- Push to GitHub repository
- Connect to Vercel
- Deploy with Next.js preset

**Option 2: Traditional Server**
- Build application with `npm run build`
- Transfer `.next/`, `public/`, and configuration files
- Run with `npm start` on port 3001
- Set up reverse proxy if needed

**Option 3: Docker**
```bash
# Build image
docker build -t psygaming-website .

# Run container
docker run -p 3001:3001 psygaming-website
```

## Troubleshooting
- Port conflicts: Use `-p` flag to specify alternate port
- Missing packages: Install `sharp` for image optimization
- Game issues: Ensure HTML files are self-contained and iframe-compatible

## Integration Guidelines
When integrating the application:
1. Preserve the directory structure
2. Maintain the relationship between games config and HTML files
3. Keep the routing patterns intact
4. Ensure proper port configuration (3001 by default)
5. Test game functionality in iframes

I want to integrate the application in my website but preserve all of the funtionalities. In the past, it failed, while integrating, the functionality of the app was compromised. The hole goal is to create a functional website that has the app integrated and reachable very easily. I dont care if it is extreamly simple solution. It should be robust and simple. Plan out how to exactly do it and what instructions I would give to cursor AI IDE 