# Procedural Dungeon Generator

Procedural Dungeon Generator is an Unreal Engine plugin for grid-based dungeon generation.

Current MVP features:
- deterministic seed-based generation
- rectangular room placement
- nearest-room connection pass
- L-shaped corridor carving
- editor preview through a placed actor or component
- runtime and Blueprint-callable generation API
- instanced mesh rendering for floors and walls
- optional neon debug overlay for room bounds, connections, corridor paths, and entrance path

## Requirements

- Unreal Engine 5.7
- Windows / Win64 target
- Visual Studio 2022 build tools
- .NET SDK compatible with the installed Unreal Engine toolchain

The plugin has been validated with `RunUAT BuildPlugin -TargetPlatforms=Win64`.

## Installation

1. Copy this plugin folder into your Unreal project:

```text
<YourProject>/Plugins/ProceduralDungeon
```

2. Open the `.uproject`.
3. If Unreal asks to rebuild missing modules, choose rebuild.
4. Enable `Procedural Dungeon Generator` in the Plugins window if needed.
5. Restart the editor after enabling or rebuilding.

## Quick Start

1. Open your level.
2. Open the Place Actors panel and search for `Dungeon Preview Actor`.
3. Drag `Dungeon Preview Actor` into the level.
4. Select the actor in the viewport or Outliner.
5. In Details, use the `Dungeon` buttons:
   - `Generate Dungeon`
   - `Clear Dungeon`
6. Select the `DungeonGenerator` component to edit generation, rendering, and debug settings.

The preview actor is a convenience wrapper around `UDungeonGeneratorComponent`. You can also add `DungeonGeneratorComponent` directly to your own actor or Blueprint.

## Demo Map

The plugin includes a basic demo level:

```text
/ProceduralDungeonGenerator/Demo/L_DungeonDemo
```

Open it from the Content Browser with plugin content visible. The level contains:

- `DungeonPreviewActor`
- configured `DungeonGenerator` component
- generated dungeon preview
- neon debug overlay enabled
- key light, sky light, camera, and bloom post process volume

The demo map is included in the plugin package. If you maintain the optional helper scripts locally, regenerate the map with Unreal Editor commandlet workflow for your project path.

## Showcase Map

The plugin also includes a presentation-focused showcase level:

```text
/ProceduralDungeonGenerator/Demo/L_DungeonShowcase
```

Use it for recording or gameplay-style validation. The map contains:

- a larger generated dungeon
- neon debug overlay enabled
- playable third-person showcase character
- `PlayerStart` placed on a generated floor tile
- overview, flyover, and run-preview cameras
- visible lighting and mild bloom

Press Play to run through the dungeon.

Controls:

- `WASD` / arrow keys: move
- mouse: look around
- `Space`: jump

Useful cameras in the Outliner:

- `PDG_Showcase_OverviewCamera`
- `PDG_Showcase_FlyoverCamera`
- `PDG_Showcase_RunPreviewCamera`

The showcase map is included in the plugin package. If you maintain the optional helper scripts locally, regenerate the map with Unreal Editor commandlet workflow for your project path.

## Blueprint API

`UDungeonGeneratorComponent` exposes:

- `GenerateDungeon()`
- `ClearDungeon()`
- `RegenerateWithSeed(int32 Seed)`

Use `GenerateDungeon()` at runtime to build the dungeon from the component settings. Use `RegenerateWithSeed()` when you want deterministic regeneration from a specific seed.

## Editor Preview

`Auto Generate` controls whether the component rebuilds automatically when settings change.

For fast iteration:
- leave `Auto Generate` enabled for small grids
- disable it for large grids and use `Generate Dungeon` manually
- use `Clear Dungeon` before removing or replacing the actor if you want to clear preview instances immediately

The component avoids rebuilding during interactive slider or numeric drag changes, then rebuilds after the final edit.

## Neon Debug Overlay

Enable `Show Debug` under `Dungeon | Debug` on the `DungeonGenerator` component.

Debug layers:
- `Show Room Bounds`: cyan room outlines
- `Show Room Connections`: magenta center-to-center room links
- `Show Corridor Paths`: yellow L-shaped corridor paths
- `Show Entrance`: green entrance path from the first room to the grid edge

For stronger glow, enable Bloom in your viewport or Post Process settings. Without Bloom, the lines still render as bright emissive mesh strips.

## Build Validation

From PowerShell:

```powershell
& "<UE_5.7>\Engine\Build\BatchFiles\RunUAT.bat" BuildPlugin `
  -Plugin="<YourProject>\Plugins\ProceduralDungeon\ProceduralDungeonGenerator.uplugin" `
  -Package="<OutputFolder>\ProceduralDungeonGenerator" `
  -TargetPlatforms=Win64 `
  -Rocket
```

If the editor is open and Live Coding is active, close the editor before rebuilding the project module.

## Current Limitations

- The generator creates simple rectangular rooms and Manhattan corridors.
- It uses one floor mesh and one wall mesh for the whole dungeon.
- It does not place doors, enemies, loot, nav data, gameplay volumes, or modular socket-based room pieces.
- It does not include multiplayer, save/load, streaming, or AI integration.
- Demo content is intended as a starting point; showcase content is for presentation and visual validation.

## More Docs

- [Editor Workflow](Docs/EDITOR_WORKFLOW.md)
- [Showcase Recording](Docs/SHOWCASE_RECORDING.md)
- [Settings Reference](Docs/SETTINGS_REFERENCE.md)
- [FAQ](Docs/FAQ.md)
- [Release Notes 0.1.0](Docs/RELEASE_NOTES_0.1.0.md)
