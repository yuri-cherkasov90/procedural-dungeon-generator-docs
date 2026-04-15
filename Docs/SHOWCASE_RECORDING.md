# Showcase Recording

Use this guide to record a short demo of the plugin.

## Map

Open:

```text
/ProceduralDungeonGenerator/Demo/L_DungeonShowcase
```

Enable plugin content visibility in the Content Browser if the map is not shown.

## Blueprint Screenshot

Open:

```text
/ProceduralDungeonGenerator/Demo/BP_DungeonPreview_Showcase
```

Use this asset for Blueprint-first screenshots. It inherits from `DungeonPreviewActor` and exposes the `DungeonGenerator` component defaults in the Blueprint editor.

## Recording Beats

Suggested sequence:

1. Show the plugin compiling or the successful `RunUAT BuildPlugin` result.
2. Open the showcase map.
3. Select `PDG_Showcase_DungeonPreview`.
4. Change `Seed` or `Room Count`, then press `Generate Dungeon`.
5. Show the neon debug overlay from the overview angle.
6. Switch to `PDG_Showcase_FlyoverCamera` for a cinematic pass.
7. Press Play and run through the dungeon with the showcase character.
8. Toggle `Show Debug` off for a clean gameplay-style view.

## Play Controls

- `WASD` / arrow keys: move
- mouse: look around
- `Space`: jump

The showcase character reads keys directly, so it does not require project input mappings.

## Useful Actors

- `PDG_Showcase_DungeonPreview`: generated dungeon and settings
- `PDG_Showcase_PlayerStart`: playable spawn point
- `PDG_Showcase_OverviewCamera`: top-down overview
- `PDG_Showcase_FlyoverCamera`: angled cinematic view
- `PDG_Showcase_RunPreviewCamera`: third-person run preview angle
- `PDG_Showcase_PostProcess`: mild bloom without manual exposure override

## Regenerate The Showcase Map

The showcase map is included in the plugin package. If you maintain the optional helper scripts locally, regenerate the map with Unreal Editor commandlet workflow for your project path.
