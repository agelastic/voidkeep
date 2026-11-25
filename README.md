# Voidkeep

A small first-person shooter in the early-90s raycaster style, built to be played in **Safari on iPhone** (it also runs in desktop browsers). It is one self-contained `index.html`. No libraries, no build step and no external assets: every texture, sprite and sound effect is generated in code when the page loads.

**Play:** https://agelastic.github.io/voidkeep/

## On iPhone

1. Open the link in Safari and turn the phone to landscape.
2. For full screen, tap **Share -> Add to Home Screen** and launch Voidkeep from the home screen icon.
3. Sound starts after your first tap. If you hear nothing, check that the ring/silent switch is not set to silent, because iOS mutes web audio in silent mode.

### Touch controls

| Control | Action |
|---|---|
| Left thumb, anywhere on the left side | Virtual joystick: move and strafe |
| Right thumb, drag | Turn |
| **FIRE** (hold) | Shoot. Keep your thumb on it and slide sideways to aim while firing |
| **WPN** | Cycle weapons |
| **MAP** | Toggle the automap |
| **II** | Pause (resume, restart level, sound on/off, quit) |

### Keyboard and mouse

WASD to move, mouse (click to capture the pointer), Q/E or the arrow keys to turn, click or Space to fire, 1-3 or Tab for weapons, M for the map, P or Esc to pause.

## The game

Three levels: **Intake Deck**, **Foundry** and **Warden Core**. Find the keycards, open the coloured doors and reach the green EXIT panel. On the last level the yellow keycard is held by the Warden.

- **Weapons:** Blaster (unlimited ammo), Scattergun (shells), Arc Lance (cells, rapid plasma bolts)
- **Enemies:** Husks (melee), Wisps (floating, ranged), Brutes (armoured, triple shot), the Warden (boss)
- **Pickups:** medkits, stims, armour, shells, cells, keycards. Orange fuel canisters explode when shot.
- Health, armour, weapons and ammo carry over between levels. Dying restarts the current level with what you had when you entered it.

## Technical notes

- Raycasting with DDA grid traversal, textured walls, perspective floor and ceiling casting, distance fog, billboarded sprites with a depth buffer, and sliding doors cast as mid-tile planes.
- Rendering goes into a low-resolution `ImageData` buffer (about 430x200 on a landscape iPhone), upscaled with pixelated filtering. The HUD and touch controls sit on a second canvas at device resolution. If frames run slow, the internal resolution drops automatically.
- Enemies path towards the player using a breadth-first flow field over the tile grid, recomputed several times per second. They open unlocked doors.
- Safe-area insets (notch and home indicator) are read from CSS `env()` so the controls stay clear of them.
- Audio is synthesised with the Web Audio API and unlocked on the first touch, as iOS requires.

## Run locally

```sh
python3 -m http.server 8000
# then open http://localhost:8000 (or your computer's LAN IP from the phone)
```

## Credits and licence

Original code and procedurally generated art and sound. "Doom-like" here describes the genre only; Voidkeep uses no names, assets, levels or designs from any existing game.

MIT licence. See [LICENSE](LICENSE).
