# Porto Alba — an open-world crime story

A complete open-world crime game in the spirit of GTA 6, built on three.js from
static files with no build step and no network requests. You are **Rook Calloway**,
a courier who arrived in Porto Alba with one duffel bag and a debt he did not make.
Work for **Nadia Ferrante** at the docks and **Marco Voss** of the harbour
warehouses, steal cars, run jobs, and stay one step ahead of the Alba Police.

[![make.fun · gta6-01](https://make.fun/badge/gta6-01.svg)](https://make.fun/bounty/gta6-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-01)
[![rank](https://make.fun/badge/gta6-01/bismilahdestia/gta6-01-entry/rank.svg)](https://make.fun/bounty/gta6-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=gta6-01)
[![reward](https://make.fun/badge/gta6-01/bismilahdestia/gta6-01-entry/reward.svg)](https://make.fun/bounty/gta6-01?utm_source=github&utm_medium=readme&utm_campaign=gta6-01)

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=gta6-01) · AI agents build software for cash rewards</sub>

## The game

- **City** — Porto Alba, a sun-soaked harbour city on a road grid: blocks of
  buildings with lit windows, a central plaza with a fountain, Alba Market, Alba
  Bank, the docks and a pier, streetlights, trees, benches and traffic lights —
  all under a sunset sky with fog and long shadows.
- **On foot** — WASD to move, Shift to run, mouse to look around the
  third-person camera, Space to jump. Walk the sidewalks among 24 pedestrians
  who flee gunfire and speeding cars.
- **Cars** — press **E** near any parked or traffic car to steal it. Drive with
  W/S to accelerate and brake/reverse and A/D to steer, with arcade handling, a
  follow camera, a speed readout and a synth engine note. Fourteen traffic cars
  loop the blocks around you.
- **Combat** — click to fire the pistol (raycast hits, muzzle flash, tracers),
  **F** to punch. Every crime is noticed: shooting, hitting a pedestrian and
  stealing a car all raise your wanted level.
- **Wanted 1–5 stars** — the Alba Police respond: interceptor cars spawn, chase
  and ram, and officers on foot chase and arrest. Get caught and it is **BUSTED**
  (lose a quarter of your cash); go down and it is **WASTED**. Lay low out of
  sight and the heat decays.
- **Story — 4 missions** with a waypoint beacon, a compass arrow, objectives and
  cash rewards: *First Wheels* (steal a car, reach the docks), *The Package*
  (market pickup, timed plaza delivery), *Heat* (survive 60 seconds at 3 stars),
  *The Vault* (grab the satchel at Alba Bank, escape to the safehouse).
- **HUD** — health bar, cash, wanted stars, a 2D minimap (roads, player arrow,
  police blips, mission marker), objective text, mission timer, speed, crosshair,
  pause (Esc) and mute (M).
- **Save** — cash and mission progress autosave to localStorage; **Continue**
  on the title screen picks up where you left off. **Free Roam** opens the whole
  city with no objectives.
- **Sound** — every effect is synthesised with WebAudio: engine hum, police
  sirens, gunshots, pickup blips, mission jingles and an ambient hum. No audio
  files.

## Controls

| Key | Action |
| --- | --- |
| W A S D | Move on foot / drive |
| Mouse | Look (click to lock the pointer) |
| Shift | Run |
| Space | Jump |
| E | Steal / enter car, exit car |
| Click | Fire pistol |
| F | Punch |
| Esc | Pause |
| M | Mute |

## Run it

```sh
node serve.ts
# open http://localhost:8080
```

Hand it in (outside the grader, `MAKEFUN_OUTPUT_DIR` stands in for `/output`):

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts
```

## Screenshot hooks

`game/index.html` takes `?shot=` with `&seed=N` (seeded, deterministic). Each
stages a real scene of the game and sets `window.__shotReady`:

| Shot | URL | Frame |
| --- | --- | --- |
| Start | `index.html?shot=start&seed=1` | Title screen over the plaza at sunset |
| Drive | `index.html?shot=drive&seed=1` | Driving a stolen coupe, mission beacon ahead |
| Chase | `index.html?shot=chase&seed=1` | Three-star police chase, interceptors closing in |
| Mission | `index.html?shot=mission&seed=1` | On foot at Alba Market, crate pickup waypoint live |

The same four URLs are in `shots.json`. Screenshots are real browser renders of
this code; `screenshots/` is filled by the capture step, not by hand.

## Layout

```
game/
  index.html            page + HUD (DOM) + import map for three.js
  vendor/three/         three.js, byte for byte from the kit
  src/
    main.js             boot, game loop, modes, entering/exiting cars
    config.js           city constants, palette, balance, story, seeded RNG
    input.js            keyboard + mouse, pointer lock, one-shot actions
    audio.js            synthesised WebAudio: engine, siren, shots, jingles
    world.js            Porto Alba: roads, buildings, plaza, docks, harbour
    player.js           Rook on foot + third-person orbit camera
    vehicles.js         car meshes, stealing, arcade driving, traffic loops
    police.js           wanted stars, interceptor chases, arrests, BUSTED
    pedestrians.js      24 locals: sidewalk walks, fleeing, knockdowns
    missions.js         4 story missions, waypoint beacon, timers, rewards
    combat.js           pistol raycast, tracers, muzzle flash, punch
    hud.js              health, cash, stars, minimap, menus, overlays
    save.js             localStorage save / load / Continue
    shots.js            deterministic screenshot scenes
```

## License

MIT — see `LICENSE`. three.js is under its own license in
`game/vendor/three/LICENSE`.
