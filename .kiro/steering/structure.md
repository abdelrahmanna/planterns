# Project Structure

```
planterns/
├── web/                  # Vite + React + TypeScript — UI, checklist, settings, demo mode
│   ├── public/
│   │   └── game/         # Prebuilt Godot HTML5 export (committed; no Godot needed to run)
│   └── src/
│       ├── checklist/    # Activity planning, tick-off UI, daily target logic
│       ├── progress/     # Visualisation of routine over time
│       ├── settings/     # Trusted contact, crisis lines, demo mode toggle
│       └── store/        # Dexie (IndexedDB) — all persistence lives here
│
├── rules/                # Pure TypeScript package — game + scheduling rules, NO UI imports
│   └── tests/            # Property-based tests for the five core rules
│
├── game/                 # Godot 4 project — the house, ghosts, lantern, lamps
│
├── .kiro/                # Kiro specs, hooks, and steering
│   └── steering/
│
└── readme.md
```

## Organisation Rules

- **`rules/` is the source of truth** for all game and scheduling logic. `web/` imports from it; never inline rule logic in UI components.
- **`rules/` has zero UI imports.** Keep it pure TS so it can be tested headlessly.
- **Persistence is isolated in `web/src/store/`.** Nothing outside `store/` reads or writes IndexedDB directly.
- **The game is a black box.** The only contract between `web/` and `game/` is `postMessage`: web sends today's state in, game sends back { ghostsCleared, lampsBought, roomsLit }. No shared modules.
- **Demo mode data is fully isolated** from real user data at the store layer.
- **Crisis-line data** is a static local file, never fetched at runtime.

## Package Boundary Summary

| From → To | Allowed? |
|-----------|----------|
| `web/` → `rules/` | ✅ import freely |
| `game/` → `rules/` | ❌ use postMessage contract only |
| `rules/` → `web/` | ❌ no UI imports |
| anything → network (user data) | ❌ never |
