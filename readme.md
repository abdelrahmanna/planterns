# P-Lantern

A companion app for people doing activity scheduling in therapy for depression. Your day's small tasks earn time in a dark house, where you clear sad little ghosts with a lantern and buy lamps that keep rooms lit for good. The house mirrors how the routine is going: rooms light up as it holds, and slowly dim after days of silence, which is the early warning to reach out.

Built for [Kiroween 2026](https://kiroween.devpost.com) in the **Costume Contest** category. Free, open source, no account, no backend. It complements therapy; it does not replace it.

> **Status:** in development. Submission period 30 Oct – 4 Dec 2026.

## Why

Behavioural activation is a standard part of treating depression: plan small daily activities, do them, notice that mood follows action. It works, and it is hardest exactly when it matters most. Low mood drains motivation, paper schedules feel like chores, and a missed day feels like failure. Most habit apps make that worse by punishing missed days with broken streaks. P-Lantern is built around the opposite rules.

## The rules

These hold everywhere in the app and the game. They are also the property-based tests.

1. **Any one task protects the house.** Waking up on time counts. Brushing your teeth counts. You never have to hit the daily target to hold your ground.
2. **Nothing bought is ever lost.** Lamps and furniture are permanent.
3. **Ghost HP never rises.** Targets rise only when you agree to it.
4. **A room dims only after three silent days**, and always with a check-in, never a consequence.
5. **No backend, no analytics, no accounts.** Everything stays on your device.

## How it works

**The checklist.** Plan a few small activities with a category (pleasure, mastery, social, physical) and a rough length. Tick them off during the day. The daily target starts at 2 and only goes up when you confirm.

**The house.** At the end of the day you get lantern time proportional to what you did. The house is dark; sad ghosts are in it. Your lantern is the only weapon: ghosts dissolve in the beam, and they never fight back. Clearing ghosts and finishing tasks earns points.

**Lamps.** Points buy lamps. A lamp in a room keeps that room lit on the days you can't. The goal is a house where every room has a lamp.

**After that.** Furnish the house. Ghosts still turn up at the door sometimes; that's weather, not failure.

**If the house goes quiet.** Nothing changes for a day or two of silence. After three, an un-lamped room dims and the app asks how you're doing, with a trusted contact you chose during setup and a short list of crisis lines by country. If you open the app after a gap it asks whether you managed anything yesterday; one tap holds the day.

## Architecture

```
web/      Vite + React + TypeScript. The checklist, progress, settings, demo mode.
          Data in IndexedDB via Dexie. JSON export/import for backup.
rules/    Pure TypeScript package. All game and scheduling rules. No UI imports.
          Property-based tests for the five rules above.
game/     Godot 4 project. The house, exported to HTML5 and embedded in an iframe.
          Receives today's state by postMessage; reports back ghosts cleared,
          lamps bought, rooms lit. Knows nothing else.
.kiro/    Specs, hooks and steering used to build this. See "Built with Kiro".
```

The page owns the data. The game only ever sees one day.

## Running locally

Requires Node 20+ and Godot 4.x (for the game only).

```sh
npm install
npm run dev          # web app at http://localhost:5173
npm test             # unit and property-based tests
```

The game is exported from `game/` with the Godot HTML5 export preset into `web/public/game/`. A prebuilt export is committed so the web app runs without Godot installed.

## Demo mode

Judges and curious people have five minutes; the house needs weeks. Settings → Demo mode seeds a 30-day history and adds "advance a day" and "advance a week" controls. Everything in demo mode is labelled as a simulation and is kept separate from your own data.

## Data and privacy

All data lives in your browser's IndexedDB. There is no server, no account, no analytics and no crash reporting. Backup is a JSON file you export and keep wherever you like. Deleting the site data deletes everything.

## Built with Kiro

_To be written during the build. Will cover: the steering docs and what they changed, the specs (rules engine, checklist, progress, game contract), the hooks, what property-based testing caught, the MCP server tried, and where spec-driven development helped or didn't._

## Credits

- Tiles, UI, particles and sounds: [Kenney](https://kenney.nl) (CC0)
- Icons: [game-icons.net](https://game-icons.net) (CC BY 3.0)
- Fonts: Google Fonts (OFL)

## A note on safety

This is a self-help tool made by one person, not a medical device, and it has not been clinically evaluated. If you are in crisis, contact local emergency services or a crisis line in your country. The app's reach-out screen lists several; please add your own trusted contact during setup.

## Licence

MIT. See [LICENSE](LICENSE).