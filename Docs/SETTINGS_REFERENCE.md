# Settings Reference

All user-facing settings live on `UDungeonGeneratorComponent`.

## Generation

| Setting | Default | Description |
| --- | ---: | --- |
| `Grid Width` | `64` | Number of cells on the X axis. |
| `Grid Height` | `64` | Number of cells on the Y axis. |
| `Seed` | `1337` | Deterministic seed used by the generator. Same settings and same seed produce the same layout. |
| `Room Count` | `12` | Target number of rooms to place. Fewer rooms may be placed if attempts run out. |
| `Min Room Size` | `4` | Minimum room width and height in cells. |
| `Max Room Size` | `10` | Maximum room width and height in cells. |
| `Room Placement Attempts` | `100` | Maximum random placement attempts before stopping room placement. |
| `Auto Generate` | `true` | Rebuilds the dungeon after committed editor setting changes. |
| `Editor Auto Generate Delay` | `0.25` | Editor-only debounce in seconds before auto rebuilding after Details panel changes. Helps keep numeric sliders responsive. |

## Rendering

| Setting | Default | Description |
| --- | ---: | --- |
| `Tile Size` | `400` | World-space distance between grid cell centers. |
| `Floor Thickness` | `20` | Height of floor instances. |
| `Wall Height` | `300` | Height of wall instances. |
| `Enable Tile Collision` | `true` | Enables floor and wall collision. Leave enabled for playtesting; disable for faster editor-only visual recording. |
| `Floor Mesh` | Engine cube | Static mesh used for floor cells. |
| `Wall Mesh` | Engine cube | Static mesh used for wall cells. |

The renderer uses `UInstancedStaticMeshComponent` and batches instance creation for floors and walls. Rebuilds use lightweight state hashes to skip unchanged instance sets and avoid per-instance transform reads during editor iteration.

## Debug

| Setting | Default | Description |
| --- | ---: | --- |
| `Show Debug` | `false` | Enables or disables all debug overlay rendering. |
| `Show Room Bounds` | `true` | Draws room rectangle outlines. |
| `Show Room Connections` | `true` | Draws direct room center connection lines. |
| `Show Corridor Paths` | `true` | Draws the L-shaped corridor route used by carving. |
| `Show Entrance` | `true` | Draws the entrance path from the first room to the nearest grid edge. |
| `Line Thickness` | `16` | Thickness of debug mesh strips. |
| `Height Offset` | `80` | Extra vertical offset above the dungeon. |
| `Emissive Intensity` | `10` | Multiplier applied to debug colors. |
| `Room Bounds Color` | Cyan | Color for room outlines. |
| `Room Connection Color` | Magenta | Color for room graph links. |
| `Corridor Path Color` | Yellow | Color for corridor carving paths. |
| `Entrance Color` | Green | Color for entrance path. |
| `Debug Line Mesh` | Engine cube | Mesh used for debug strips. |
| `Debug Line Material` | Engine emissive material | Material used for debug strips. |

## Blueprint Methods

| Method | Description |
| --- | --- |
| `GenerateDungeon()` | Builds a dungeon from current settings and renders it. Callable in editor and Blueprint. |
| `ClearDungeon()` | Clears generated mesh and debug instances. Callable in editor and Blueprint. |
| `RegenerateWithSeed(int32 Seed)` | Updates `Seed`, then generates a dungeon. |

## Determinism

Generation uses a single `FRandomStream` initialized from `Seed`.

The layout should remain deterministic when these inputs are identical:

- generation settings
- seed
- plugin version
- algorithm implementation

Changing generation algorithm code can intentionally change results for the same seed.

## Current MVP Limits

- Rectangular rooms only.
- Corridors are L-shaped Manhattan paths.
- One floor mesh and one wall mesh are used for the full dungeon.
- Debug overlay is visual only and does not affect generation.
- No door placement yet.
- No gameplay object spawning yet.
- No nav mesh, AI, replication, streaming, or save/load integration yet.
