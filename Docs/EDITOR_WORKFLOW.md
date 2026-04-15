# Editor Workflow

This workflow is for testing the plugin in an Unreal level.

## Open The Demo Map

The plugin ships with:

```text
/ProceduralDungeonGenerator/Demo/L_DungeonDemo
```

In the Content Browser, enable plugin content visibility if the map is not shown. Open the map and select `PDG_Demo_DungeonPreview` in the Outliner.

For a presentation-style map, open:

```text
/ProceduralDungeonGenerator/Demo/L_DungeonShowcase
```

Select `PDG_Showcase_DungeonPreview` for generation settings, or press Play to run through the dungeon with the showcase third-person character.

## Add A Preview Actor

1. Open a level.
2. Open Place Actors.
3. Search for `Dungeon Preview Actor`.
4. Drag it into the scene.
5. Select it in the Outliner.

The actor contains a `DungeonGenerator` component. Most settings live on that component.

## Generate And Clear

When the actor is selected, the Details panel includes:

- `Generate Dungeon`
- `Clear Dungeon`

Use `Generate Dungeon` after changing settings. Use `Clear Dungeon` to remove generated instanced mesh data.

If the buttons are not visible:

1. Make sure the project has been rebuilt after plugin changes.
2. Close and reopen Unreal Editor.
3. Select `DungeonPreviewActor` directly in the Outliner.
4. Select the `DungeonGenerator` component if you want component-level settings.

## Recommended First Test

Use these settings:

- `Grid Width`: `64`
- `Grid Height`: `64`
- `Room Count`: `12`
- `Min Room Size`: `4`
- `Max Room Size`: `10`
- `Room Placement Attempts`: `100`
- `Tile Size`: `400`
- `Floor Thickness`: `20`
- `Wall Height`: `300`

Press `Generate Dungeon`. You should see a rectangular grid of instanced floors and walls.

## Debug Overlay

On the `DungeonGenerator` component, open `Dungeon | Debug`.

Enable:

- `Show Debug`
- `Show Room Bounds`
- `Show Room Connections`
- `Show Corridor Paths`
- `Show Entrance`

Layer meanings:

- Room bounds show the generated room rectangles.
- Room connections show the high-level connection graph.
- Corridor paths show the L-shaped carving route.
- Entrance shows the corridor carved from the first room to the nearest grid edge.

Useful debug settings:

- `Line Thickness`: visual width of debug strips
- `Height Offset`: lifts debug lines above the dungeon
- `Emissive Intensity`: controls glow strength
- layer colors: customize each debug layer

For a stronger neon look, enable Bloom in the viewport or add a Post Process Volume with Bloom enabled.

## Performance Notes

The plugin renders floors, walls, and debug lines through `UInstancedStaticMeshComponent`.

Large grids can still be expensive because every generated cell becomes an instance. For faster editing:

- disable `Auto Generate`
- edit multiple settings
- press `Generate Dungeon` manually
- increase `Editor Auto Generate Delay` if numeric sliders still rebuild too eagerly
- disable `Enable Tile Collision` for editor-only top-down or flyover recording, then re-enable it before runtime playtesting

The component debounces editor auto-generation so repeated numeric slider changes are collapsed into a single rebuild shortly after editing pauses.

## Troubleshooting

If the plugin does not appear:

- confirm the plugin folder is under `<Project>/Plugins/ProceduralDungeon`
- confirm `ProceduralDungeonGenerator.uplugin` is present
- rebuild the project modules
- restart Unreal Editor

If Unreal says modules are missing:

- close the editor
- rebuild the project from source or let Unreal rebuild on launch
- avoid Live Coding for full module rebuilds

If debug lines look bright but not glowy:

- enable Bloom
- increase `Emissive Intensity`
- assign your own emissive material to `Debug Line Material`
