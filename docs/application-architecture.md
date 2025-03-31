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