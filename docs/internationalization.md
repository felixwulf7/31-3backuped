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