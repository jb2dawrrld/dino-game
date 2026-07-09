# dino-game [WIP]
Replicating the well-known Google dinosaur game that pops up when your internet is down. Mainly for Node.js practice.

## Phase 1: Game Client (replica of main game ui/frontend)

### 1.1 Imported upstream game assets and engine
Game logic would easily be 2000+ lines of code if implemented from scratch. Google ships the game in Chromium as open source (BSD-3-Clause). The community fork [wayou/t-rex-runner](https://github.com/wayou/t-rex-runner) is a near-direct standalone port with the same sprites, audio, physics, and HiDPI scaling. Since the main focus of this project is Node.js practice, the main foundation of the game was imported from the public repo above.

Copy from `wayou/t-rex-runner` (or Chromium `offline.js`):
- Sprite sheets: `100-offline-sprite.png`, `200-offline-sprite.png`
- Audio: jump, score, hit (`.ogg`)
- Core classes: `Runner`, `Trex`, `Obstacle`, `Horizon`, `HorizonLine`, `Cloud`, `NightMode`, `DistanceMeter`, collision helpers


### 1.2 Preserved original constants 
Likewise, instead of tuning all the parameters casually until I am satisfied, I found it more convenient to source the original constants and their values from: ([Chromium ~ Runner.config](https://chromium.googlesource.com/chromium/src.git/+/master/components/neterror/resources/offline.js)):
| Constant | Value | Effect |
|----------|-------|--------|
| `SPEED` | 6 | Starting scroll speed |
| `MAX_SPEED` | 13 | Difficulty cap |
| `ACCELERATION` | 0.001 | Per-frame speed increase |
| `GRAVITY` | 0.6 | Jump arc |
| `INITIAL_JUMP_VELOCITY` | 12 | Jump height |
| `GAP_COEFFICIENT` | 0.6 | Obstacle spacing |
| `INVERT_DISTANCE` | 700 | Night mode toggle interval |
| Canvas | 600×150 CSS px | HiDPI backing store handled by `updateCanvasScaling` |

This gave it more of an authentic feel.

### 1.3 Verify frontend checklist
Before touching the backend, I confirmed:
- Idle T-Rex blink animation before first jump/space
- Jump (Space / Up) and duck (Down) with speed-dependent duck collision box
- Cactus variants (small/large, 1–3 width) and pterodactyl at higher speeds
- Cloud parallax, scrolling ground, distance meter with sprite digits
- Day/night invert at score milestones
- Speed caps at 13; gap between obstacles caps accordingly
- Game over + restart sprite; local high score in `localStorage` (built into `DistanceMeter`)
Controls 
- Desktop: Space / Up = jump, Down = duck, Enter on game over = restart

Satisfied, ready for Phase 2.

## Phase 2 — Node.js backend (anonymous leaderboard)

Nothing here yet ! [WIP]
