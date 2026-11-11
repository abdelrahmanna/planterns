# Tech Stack

## Packages / Workspaces

| Package | Technology |
|---------|-----------|
| `web/`  | Vite + React + TypeScript |
| `rules/` | Pure TypeScript (no UI imports) |
| `game/` | Godot 4, exported to HTML5 |

## Key Libraries

- **Dexie** — IndexedDB wrapper used in `web/` for all local persistence.
- **Property-based testing** — used in `rules/` to verify the five core rules (framework TBD, e.g. fast-check).
- Node 20+ required. Godot 4.x required only to rebuild the game export.

## Architecture Notes

- `rules/` is a pure TS package with zero UI imports — import it from `web/` and test it in isolation.
- The game communicates with the web app exclusively via `postMessage`. It receives today's state and reports back ghosts cleared, lamps bought, and rooms lit. It knows nothing else about app state.
- The web page is the data owner. The game only ever sees one day at a time.
- The Godot HTML5 export is committed to `web/public/game/` so the web app runs without Godot installed.

## Common Commands

```sh
# Install all dependencies
npm install

# Run web dev server (http://localhost:5173)
npm run dev

# Run unit and property-based tests
npm test
```

> Game: export from `game/` using the Godot HTML5 export preset into `web/public/game/`.

## Data & Privacy Constraints

- **No server, no account, no analytics, no crash reporting.**
- All persistence goes through Dexie / IndexedDB in `web/`.
- Backup = JSON export; restore = JSON import.
- Demo mode data must be fully isolated from real user data.
