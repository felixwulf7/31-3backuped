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