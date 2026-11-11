# Hook a Beast

Roblox game. Players cast a hook into foggy abyss chasms, reel in beasts, and battle them in co-op pet battles. Caught beasts go to a plot that generates money.

## Game Cache

### Core loop
- Player throws the hook into the abyss wherever they choose.
- Catch: a moving line on a bar must hit green 3 of 5 times.
- The green zone shrinks on every hit. More hits give a better beast chance and tier.
- Fail (timeout or fewer than 3 hits) ends the hook and reels it back.
- Hooks are bought in a shop. Better hooks give better catch luck and a larger green bar.

### Reel formulas
- GreenZoneWidth = BaseWidth * (HookQuality / BeastTier)
- NeedleSpeed = BaseSpeed * (BeastTier / HookQuality) * (FocusPass ? 0.67 : 1)
- Zone shrink per consecutive hit: 100%, 70%, 45%, 25%
- 3 misses: the cable snaps

### Combat and camera
- Player can move freely while the hook is thrown.
- Camera sits out and to the right, follows the character, and both face the hook/beast.
- Green-bar hit: slight zoom in plus camera shake, scaling with combo. A failed hit returns the camera to normal.

### UI
- Glassmorphism style: glass Color3.fromRGB(18,20,26) at 0.15 to 0.25 transparency.
- Per-world accents: emerald, solar orange, cyan, gold, royal purple.
- Button spring: hover 1.05, press 0.95.

### Architecture (server-authoritative Luau)
- ServerScriptService.Services
  - DataService (ProfileService)
  - ReceiptService
  - ReelValidationService
  - CombatService
  - PlotService
- StarterPlayerScripts.Controllers
  - ReelController
  - CombatController
  - UIController

### Plot and progression
- Plot: 10 slots, expandable with money. Placed beasts generate money continuously.
- Later: unlock a new world after buying all hooks. Each player gets a personal abyss with better beasts (not yet planned).

### Open items
- Datastore saving player data (required).
- Larger abyss.
- Player-aimable hook throw.
