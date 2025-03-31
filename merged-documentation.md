# PsyGaming Lab Website Documentation - Complete Reference

---

# Table of Contents
- [Project Overview](#project-overview)
- [Application Architecture](#application-architecture)
- [Component Directory](#component-directory)
- [Internationalization Implementation](#internationalization-i18n-implementation)
- [Deployment Guide](#deployment-guide)
- [Game Integration Guide](#game-integration-guide)

---

# Project Overview

## Project Description
PsyGaming Lab Website is a multilingual Next.js application designed to provide therapeutic gaming experiences, community forums, and psychology-related gaming content. The website combines psychology with gaming to create therapeutic and educational experiences.

## Technology Stack
- **Framework**: Next.js 14.2.23
- **UI Library**: React 18
- **Styling**: Tailwind CSS 3.4.17
- **Language**: TypeScript 5
- **Package Manager**: npm
- **Deployment**: Standard Next.js production build

## Key Features
1. Multilingual support (English, German)
2. Service listings for therapeutic gaming experiences
3. Game catalog with multiple game categories
4. Responsive design for all devices
5. Internationalized routing with dynamic paths
6. Contact form for user inquiries
7. Interactive game components embedded in pages

## Production Notes
- The application runs on port 3001 for production (configured in package.json)
- Built with static site generation for most pages (SSG)
- Mobile-responsive layout built with Tailwind CSS

---

# Application Architecture

## Project Structure
```
psygaminglabwebsite/
├── app/                      # Main application code (Next.js App Router)
│   ├── [lang]/               # Language-specific routes with dynamic routing
│   │   ├── [serviceSlug]/    # Service-specific pages
│   │   │   └── [gameSlug]/   # Game-specific pages
│   │   ├── contact/          # Contact page
│   │   ├── games/            # Games directory
│   │   ├── privacy-policy/   # Privacy policy page
│   │   └── terms-of-service/ # Terms of service page
│   ├── components/           # Reusable UI components
│   │   └── service-game/     # Service and game specific components
│   ├── config/               # Configuration files
│   ├── fonts/                # Custom font files
│   ├── utils/                # Utility functions and helpers
│   ├── globals.css           # Global CSS
│   ├── layout.tsx            # Root layout component
│   └── page.tsx              # Root page component (redirects to language route)
├── public/                   # Static assets
│   ├── games/                # Embedded game HTML files
│   └── images/               # Image assets
├── docs/                     # Technical documentation
├── next.config.js            # Next.js configuration
├── package.json              # Dependencies and scripts
├── postcss.config.mjs        # PostCSS configuration
├── tailwind.config.ts        # Tailwind CSS configuration
└── tsconfig.json             # TypeScript configuration
```

## Application Layers

### Routing Layer
- Uses Next.js App Router with directory-based routing
- Internationalization through dynamic `[lang]` parameter
- Nested dynamic routes for services and games

### Component Layer
- Reusable UI components in `app/components/`
- Page-specific components co-located with routes
- Specialized service and game components in `app/components/service-game/`

### Data Layer
- Configuration data in `app/config/`
- Static data for games, services, and languages
- No external API or database dependencies

### Utility Layer
- Helper functions in `app/utils/`
- Translations and internationalization helpers
- Metadata generation utilities

## Key Design Patterns

### Internationalization Pattern
- Dynamic `[lang]` segments in the URL
- Language-specific content defined in `translations.ts`
- Language switcher component for changing locales

### Dynamic Routing Pattern
- Nested dynamic routes (`[serviceSlug]` and `[gameSlug]`)
- Content mapping through configuration files
- SEO-friendly URLs with meaningful slugs

### Component Composition Pattern
- Reusable components composed into page layouts
- Specialized components for specific content types
- Consistent styling and theming across components

---

# Component Directory

This document provides an overview of the reusable components in the PsyGaming Lab Website, explaining their purpose and usage.

## Core Components

### `Header.tsx`
- **Purpose**: Main navigation header for the website
- **Features**: 
  - Responsive navigation menu
  - Language switcher integration
  - Mobile menu toggle
  - Service navigation links

### `Footer.tsx`
- **Purpose**: Footer present on all pages
- **Features**:
  - Site navigation links
  - Social media links
  - Copyright information
  - Language options
  - Legal links (Privacy, Terms)

### `Hero.tsx`
- **Purpose**: Hero section for landing pages
- **Features**:
  - Large background image
  - Call-to-action button
  - Headline and subheadline
  - Responsive design

### `ContactForm.tsx`
- **Purpose**: Interactive contact form for user inquiries
- **Features**:
  - Form validation
  - Multiple input fields
  - Submit handling
  - Responsive layout

### `FeatureCard.tsx`
- **Purpose**: Display features or benefits in card format
- **Features**:
  - Icon display
  - Title and description
  - Hover effects
  - Customizable appearance

### `ContentBlock.tsx`
- **Purpose**: Reusable content block with image and text
- **Features**:
  - Left/right image alignment options
  - Heading and description
  - Call-to-action button
  - Responsive layout

### `SectionTitle.tsx`
- **Purpose**: Consistent section titles across the site
- **Features**:
  - Main title and subtitle support
  - Customizable alignment
  - Consistent styling

### `LanguageSwitcher.tsx`
- **Purpose**: Allow users to switch between available languages
- **Features**:
  - Language selection dropdown
  - Maintains current path when switching
  - Visual indication of current language

## Service and Game Components

### `BenefitCard.tsx`
- **Purpose**: Display benefits of specific games or services
- **Features**:
  - Icon or image
  - Benefit title and description
  - Consistent styling with overall design

### `BenefitsSection.tsx`
- **Purpose**: Section showcasing multiple benefits
- **Features**:
  - Grid layout of benefit cards
  - Section title
  - Responsive design

### `CallToAction.tsx`
- **Purpose**: Prominent call-to-action section
- **Features**:
  - Eye-catching design
  - Primary button
  - Headline and supporting text

### `FeatureSection.tsx`
- **Purpose**: Display feature list for services or games
- **Features**:
  - Multiple feature cards
  - Section header
  - Responsive grid layout

### `HeroSection.tsx`
- **Purpose**: Hero section specific for service or game pages
- **Features**:
  - Game/service specific imagery
  - Targeted messaging
  - Call-to-action

### `StepCard.tsx`
- **Purpose**: Display step-by-step instructions or process
- **Features**:
  - Numbered or sequential steps
  - Visual indication of order
  - Description for each step

### `StepsSection.tsx`
- **Purpose**: Section showing a process or procedure
- **Features**:
  - Multiple step cards in sequence
  - Visual connection between steps
  - Section header

---

# Internationalization (i18n) Implementation

## Overview
PsyGaming Lab Website implements internationalization using Next.js's App Router with dynamic route parameters. This allows for language-specific content while maintaining the same URL structure across languages.

## Supported Languages
The application currently supports:
- English (en) - Primary language
- German (de) - Secondary language

Configuration for languages is stored in `app/config/languages.ts`.

## URL Structure
The internationalization approach uses language-specific routes:
- `/en/...` - English content
- `/de/...` - German content

The root URL `/` automatically redirects to the default language (English).

## Implementation Details

### Directory Structure
```
app/
├── [lang]/               # Dynamic language segment
│   ├── layout.tsx        # Language-specific layout
│   ├── page.tsx          # Home page with language-specific content
│   ├── contact/          # Contact page
│   └── ...               # Other language-specific routes
└── page.tsx              # Root redirector to default language
```

### Language Parameter
The `[lang]` parameter in the URL is captured by Next.js and used to:
1. Determine which language to display content in
2. Load the appropriate translations
3. Set the HTML lang attribute correctly

### Translation System
Translations are managed in `app/utils/translations.ts`, which contains:
- Language-specific text strings
- Function to access translations based on current language

Example translation usage:
```typescript
import { getTranslations } from '@/app/utils/translations';

export default function Page({ params }: { params: { lang: string } }) {
  const t = getTranslations(params.lang);
  
  return (
    <h1>{t.welcomeMessage}</h1>
  );
}
```

### Language Switching
The `LanguageSwitcher` component allows users to change languages while maintaining their current page:
- Preserves the current path when switching
- Updates URL to reflect the selected language
- Visual indication of current language

### SEO Considerations
- Each language version has appropriate HTML lang attribute
- Metadata is translated for each language
- Canonical links point to the same page in different languages
- hreflang tags indicate language alternatives

## Adding New Languages
To add a new supported language:
1. Add the language to `app/config/languages.ts`
2. Add translations for all strings in `app/utils/translations.ts`
3. Create language-specific content for pages that need customization
4. Update metadata generation for the new language

---

# Deployment Guide

This guide explains how to deploy the PsyGaming Lab Website to various environments.

## Prerequisites
- Node.js 18.x or later
- npm 9.x or later
- Git

## Local Development

### Setup
1. Clone the repository:
   ```bash
   git clone https://github.com/felixwulf7/28marchwebsite.git
   cd 28marchwebsite
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Start the development server:
   ```bash
   npm run dev
   ```
   
   The development server will start on http://localhost:3000 by default.

### Building for Production
To create a production build:
```bash
npm run build
```

This will generate optimized production files in the `.next` directory.

### Running Production Build Locally
To test the production build locally:
```bash
npm run start
```

The production server will start on http://localhost:3001 (configured in package.json).

## Deployment Options

### Option 1: Vercel Deployment (Recommended)

1. Push your code to GitHub
2. Sign up for a Vercel account: https://vercel.com
3. Import your GitHub repository
4. Select the "Next.js" framework preset
5. Configure environment variables if needed
6. Deploy

Vercel will automatically detect the Next.js project and deploy it with the best settings.

### Option 2: Traditional Web Server Deployment

1. Build the application:
   ```bash
   npm run build
   ```

2. Transfer the following files to your server:
   - `.next/` directory
   - `node_modules/` directory
   - `package.json`
   - `public/` directory
   - `next.config.js` (or `.mjs`)

3. On the server, install production dependencies:
   ```bash
   npm install --production
   ```

4. Start the production server:
   ```bash
   npm run start
   ```

5. Configure a reverse proxy (like Nginx) to forward requests to the Node.js server

### Option 3: Docker Deployment

1. Create a Dockerfile:
   ```
   FROM node:18-alpine AS base

   # Install dependencies only when needed
   FROM base AS deps
   WORKDIR /app
   COPY package.json package-lock.json ./
   RUN npm ci

   # Rebuild the source code only when needed
   FROM base AS builder
   WORKDIR /app
   COPY --from=deps /app/node_modules ./node_modules
   COPY . .
   RUN npm run build

   # Production image, copy all the files and run next
   FROM base AS runner
   WORKDIR /app
   ENV NODE_ENV production

   COPY --from=builder /app/public ./public
   COPY --from=builder /app/.next ./.next
   COPY --from=builder /app/node_modules ./node_modules
   COPY --from=builder /app/package.json ./package.json
   COPY --from=builder /app/next.config.js ./next.config.js

   EXPOSE 3001
   ENV PORT 3001

   CMD ["npm", "start"]
   ```

2. Build the Docker image:
   ```bash
   docker build -t psygaming-website .
   ```

3. Run the Docker container:
   ```bash
   docker run -p 3001:3001 psygaming-website
   ```

## Environment Variables

The following environment variables can be configured:

- `PORT`: The port the application should run on (default: 3001)
- `NODE_ENV`: The environment mode (development/production)

## Production Considerations

### Performance Optimizations
- Enable the Sharp image optimization package:
  ```bash
  npm install sharp
  ```

### Security Recommendations
- Configure Content Security Policy headers
- Set up regular security updates
- Use HTTPS in production

### Monitoring
- Consider setting up monitoring tools like:
  - New Relic
  - Datadog
  - Sentry for error tracking

### CDN Integration
For better performance, consider using a CDN for static assets:
- Cloudflare
- Akamai
- AWS CloudFront

---

# Game Integration Guide

## Overview
The PsyGaming Lab Website includes integrated HTML5 games focused on psychological wellness. This document explains how games are integrated, managed, and displayed within the website.

## Game Files Location
All game files are stored in the `public/games/` directory. These are self-contained HTML files that can be embedded or linked to from the main application.

Current games include:
- 3D shooter games focused on psychological themes
- Mental health matching game
- Mindful snake game
- Mindful starship game
- PsyJump game

## Game Configuration
Games are configured in `app/config/games.ts`, which contains metadata about each game:

```typescript
// Example game configuration
{
  id: 'emotional-presence',
  nameKey: 'emotionalPresenceGame',
  slugEn: 'emotional-presence',
  slugDe: 'emotionale-praesenz',
  categoryId: 'shooter',
  imageUrl: '/images/gaming_controller.jpg',
  filePath: '/games/3d_shooter_emotional_presence.html',
  featureImageUrl: '/images/gamer_on_laptop.jpg',
}
```

Key properties:
- `id`: Unique identifier
- `nameKey`: Translation key
- `slugEn`/`slugDe`: Language-specific URL slugs
- `categoryId`: Game category (shooter, puzzle, etc.)
- `filePath`: Path to the HTML game file
- `imageUrl`: Thumbnail image
- `featureImageUrl`: Larger feature image

## Game Categories
Games are organized into categories (defined in `app/config/games.ts`):

1. **Shooter Games**
   - Emotional presence
   - Performance fear
   - Self-doubt
   - Accepting tiredness

2. **Relaxation Games**
   - Mindful snake
   - Mindful starship

3. **Puzzle Games**
   - Mental health matching

## Integration Methods

### 1. Embedded Games
Games are embedded directly using iframes:

```tsx
<iframe 
  src={game.filePath}
  className="w-full h-[600px] border-0"
  title={gameName}
  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
  allowFullScreen
/>
```

This approach is used in the `/[lang]/games/play` route to display games directly within the website.

### 2. Game Cards
Game cards are used on category pages to display available games:

```tsx
<div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
  {categoryGames.map((game) => (
    <Link 
      key={game.id}
      href={`/${params.lang}/games/play?game=${game.id}`}
      className="block group"
    >
      <div className="bg-white rounded-lg shadow-md overflow-hidden transition-all duration-300 group-hover:shadow-xl">
        <img 
          src={game.imageUrl} 
          alt={getGameName(game, t)} 
          className="w-full h-48 object-cover"
        />
        <div className="p-4">
          <h3 className="text-xl font-semibold mb-2">{getGameName(game, t)}</h3>
          <p className="text-gray-600">{getGameDescription(game, t)}</p>
        </div>
      </div>
    </Link>
  ))}
</div>
```

## Game Routing
Games are accessible through several routes:

1. **Direct Play**: `/[lang]/games/play?game=[gameId]` 
   - Loads a specific game in the game player

2. **Category Pages**: `/[lang]/[serviceSlug]/[gameSlug]`
   - Shows games in a specific category (e.g., shooter games)

3. **Service Pages**: `/[lang]/[serviceSlug]`
   - Shows all game categories for a service

## Adding New Games

To add a new game to the website:

1. Add the HTML game file to `public/games/`

2. Add game metadata to `app/config/games.ts`:
   ```typescript
   {
     id: 'new-game-id',
     nameKey: 'newGameNameKey',
     slugEn: 'new-game-slug',
     slugDe: 'new-game-german-slug',
     categoryId: 'existing-category-id',
     imageUrl: '/images/game-thumbnail.jpg',
     filePath: '/games/new-game.html',
     featureImageUrl: '/images/game-feature.jpg',
   }
   ```

3. Add translations for the game name and description in `app/utils/translations.ts`

4. If creating a new category, add it to the categories array in `app/config/games.ts`

## Technical Requirements for Games

Games embedded in the website should:

1. Be completely self-contained HTML files
2. Work within an iframe context
3. Be responsive to different screen sizes
4. Not require external server connections
5. Function without special permissions
6. Be optimized for performance (initial load < 5MB)

## Performance Considerations

- Load games on demand, not on initial page load
- Consider adding loading states for slower connections
- Optimize game assets for web delivery

---

I want to integrate the application in my website but preserve all of the funtionalities. In the past, it failed, while integrating, the functionality of the app was compromised. The hole goal is to create a functional website that has the app integrated and reachable very easily. I dont care if it is extreamly simple solution. It should be robust and simple. Plan out how to exactly do it and what instructions I would give to cursor AI IDE 