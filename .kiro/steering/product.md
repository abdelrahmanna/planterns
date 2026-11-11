# Product: P-Lantern

A companion app for people doing **behavioural activation therapy for depression**. It pairs a daily activity checklist with a simple game: completed tasks earn lantern time in a dark house where you clear sad ghosts and buy lamps that permanently light rooms.

Built for [Kiroween 2026](https://kiroween.devpost.com) — Costume Contest category. Free, open source, no account, no backend. Complements therapy; does not replace it.

## Core Rules (must never be violated)

These are product invariants enforced as property-based tests in `rules/`:

1. **Any one task protects the house.** A single completed task is enough to hold ground.
2. **Nothing bought is ever lost.** Lamps and furniture are permanent.
3. **Ghost HP never rises.** Targets only increase when the user explicitly confirms.
4. **A room dims only after three silent days**, always with a check-in prompt, never a silent penalty.
5. **No backend, no analytics, no accounts.** All data stays on the device (IndexedDB).

## Key Concepts

- **Checklist** — daily activities with a category (pleasure, mastery, social, physical) and rough duration. Daily target starts at 2, only increases on user confirmation.
- **Lantern time** — earned proportionally from completed tasks; used as currency in the house game.
- **House** — dark rooms with sad ghosts. Lantern is the only weapon; ghosts never fight back. Clearing ghosts earns points.
- **Lamps** — permanent upgrades bought with points; keep a room lit on missed days.
- **Check-in** — after 3 silent days, the app surfaces a trusted contact (set during setup) and local crisis lines.
- **Demo mode** — seeds 30-day history with time-advance controls for judges/reviewers; clearly labelled as simulation, isolated from real data.

## Tone

Gentle, non-punitive. No streaks. No broken chains. Silence is weather, not failure.

## Safety Note

Not a medical device; not clinically evaluated. The reach-out screen lists crisis lines by country. Always remind users to add a trusted contact during setup.
