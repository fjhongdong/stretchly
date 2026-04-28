# Stretchly Project Guidelines

## Design System
Always read DESIGN.md before making any visual or UI decisions.
All font choices, colors, spacing, and aesthetic direction are defined there.
Do not deviate without explicit user approval.
In QA mode, flag any code that doesn't match DESIGN.md.

## Architecture Notes
- Electron v41 app with ESM modules
- Main entry: `app/main.js` (1718 lines — needs refactoring)
- Break scheduling: `app/breaksPlanner.js`
- 54 language translations in `app/locales/`
- CSS architecture: `app/css/color-scheme.css` → `commons.css` → component CSS

## Code Style
- StandardJS linting (no semicolons)
- Immutable data patterns (create new objects, never mutate)
- JSDoc for public APIs where types improve clarity
- No console.log in production code

## Testing
- Vitest framework with 315 tests
- Run: `npm test`
- Coverage: `npm run coverage`
- CI: GitHub Actions (3 platforms)

## Key Files
| File | Purpose |
|------|---------|
| `app/main.js` | Main Electron process, window management |
| `app/breaksPlanner.js` | Break scheduling logic |
| `app/css/color-scheme.css` | Light/dark theme CSS variables |
| `app/utils/sanitizeIdea.js` | HTML sanitization (security) |
| `test/sanitizeIdea.js` | Security tests |
