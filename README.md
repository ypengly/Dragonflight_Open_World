# Dragonflight: Open World

A browser-based 3D dragon flight game built with Three.js. Single self-contained
HTML file — no build step, no install, no server required.

## Run it

Double-click `index.html`, or open it from your browser with **File → Open**.
It also runs fine served from any static web server if you prefer that.

Requires a browser with WebGL (any recent Chrome, Firefox, Safari, or Edge).

## Controls

| Key | Action |
|---|---|
| W / S | Move forward / back, pitch up / down while flying |
| A / D | Turn left / right |
| Space | Take off, flap wings |
| Shift | Run (on ground), dive (in air) |
| Left Mouse | Breathe fire |
| R | Roar |
| 1–7 | Change dragon colour |
| M | Toggle map (scroll wheel to zoom) |
| V | Toggle first-person / third-person camera |
| Esc | Pause menu |

## What's implemented

- **Dragon model** — procedurally built from primitives: horned head, jaw with
  teeth, membrane wings, segmented tail, four legs. No external model files.
- **Flight physics** — takeoff, flapping, gliding, diving, stalling, banking
  turns, and landing (hard landings cost health).
- **World** — infinite terrain streamed in chunks around the player, generated
  from layered noise. Biomes: ocean, desert, grassland, forest, snowy peaks.
  Instanced trees. Water plane you can land on and swim in.
- **Sky** — dynamic day/night cycle (sun, moon, stars), drifting clouds at
  multiple altitudes, distance fog.
- **Camera** — third-person chase camera that pulls back and widens FOV with
  speed; first-person mode; screen shake on attacks and hard landings.
- **Fire breath** — particle stream with glow, heat-colored fade, a light
  source, and an energy bar with cooldown.
- **Discovery system** — procedurally placed glowing landmarks with generated
  names. Flying into one triggers a "Location Found" banner and grants XP.
- **Progression** — level and title (Young → Experienced → Powerful → Ancient
  → Legendary Dragon) driven by XP from discoveries.
- **Map** — top-down rendered terrain map with your heading and discovered
  landmarks, zoomable.
- **Save/load** — autosaves every few seconds to the browser's local storage;
  main menu offers Continue and New Game.
- **Audio** — synthesized wind (volume tied to airspeed), fire crackle, and a
  roar sound. No external audio files.

## What's not implemented

This is Phase 1–2 of the original spec (dragon, flight, and world), plus the
fire-breath and discovery pieces of Phase 3. The following are **not** built,
and there is no placeholder pretending otherwise:

- Villages, cities, and NPCs with routines or reactions
- Quests
- Enemies, wildlife, and other dragons
- Weather (rain, storms, snowfall)
- Fire igniting vegetation or damaging enemies (visual only right now)
- Dragon nest / customization beyond color
- Treasure system
- Music and recorded sound effects (audio is synthesized in-browser)

## Project structure

```
Dragonflight_Open_World/
├── index.html      # entire game: markup, styles, and all JS in one file
└── README.md        # this file
```

Everything — rendering, terrain generation, dragon model, physics, UI, save
system — lives in `index.html`. It's kept as one file so it's trivially
portable; if the project grows further (villages, NPCs, quests), it should be
split into modules at that point.

## Extending it

Natural next steps, in the order the original spec recommends:

1. Villages/cities: place structures the same way landmarks are placed
   (procedural placement keyed off world coordinates), add simple NPC meshes.
2. Quests: a small state machine triggered by proximity to specific
   landmarks or NPCs.
3. Enemies/wildlife: reuse the instancing pattern used for trees for
   simple animated actors; add basic pursue/flee AI.
4. Weather: a global state (like the day/night cycle) driving fog density,
   a rain particle system, and audio filter changes.

## Known limitations

- Terrain uses value noise (not full Perlin/Simplex), which is fast but
  slightly more grid-aligned at extreme zoom-out — fine at play scale.
- No level-of-detail reduction on distant chunks yet; very old/low-power
  GPUs may see reduced framerate with many chunks loaded.
- Save data is per-browser (localStorage), not synced across devices.
