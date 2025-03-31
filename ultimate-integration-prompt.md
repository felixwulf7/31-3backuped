# Ultimate Prompt for Cursor AI: Integrating PsyGaming Lab Website

I need to integrate the PsyGaming Lab Website (a Next.js application) into my existing website while preserving all functionalities. In previous attempts, the integration compromised the app's functionality. I want a robust, simple solution that makes the app easily accessible from my main site.

## What I Have:

- A Next.js 14 application with TypeScript and Tailwind CSS
- Multilingual support (English/German) using dynamic `[lang]` routing
- HTML5 games embedded via iframes (stored in `public/games/`)
- Complex routing with dynamic paths (`[serviceSlug]` and `[gameSlug]`)
- Currently running on port 3001 (was getting conflicts on port 3000)

## Integration Requirements:

1. Preserve ALL functionalities, including:
   - Language switching
   - Dynamic routing
   - Game embedding and playability
   - Responsive design

2. Make the app easily accessible from my main website

3. Use a straightforward solution that minimizes the risk of breaking things

## Project Structure to Preserve:

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

## Solution Approach:

Please provide step-by-step instructions to:

1. Deploy the Next.js app as a standalone application (either on a subdomain or with a reverse proxy)
2. Configure any necessary settings to ensure all functionalities work
3. Create a simple, robust way to access the app from my main website (considering either direct linking or iframe embedding)

I'm prioritizing functionality and simplicity over complex integration. I don't want to modify the core application structure if it risks breaking features.

Please provide detailed, copy-pastable commands and code snippets where needed. Assume I'm using Cursor AI IDE to implement this solution. 