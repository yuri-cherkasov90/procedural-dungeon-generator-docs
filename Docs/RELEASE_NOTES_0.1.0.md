# Release Notes - 0.1.0 Showcase MVP

`0.1.0` is the first showcase-ready MVP for Procedural Dungeon Generator.

## Highlights

- Deterministic seed-based dungeon generation.
- Grid-based rooms and corridors.
- Editor preview actor and reusable generator component.
- Blueprint-callable generation API.
- Instanced mesh rendering for floors and walls.
- Optional neon debug overlay.
- Demo map for basic validation.
- Showcase map for screenshots, flythrough capture, and third-person runtime playtest.
- Product docs, settings reference, and recording guide.

## Included Maps

```text
/ProceduralDungeonGenerator/Demo/L_DungeonDemo
/ProceduralDungeonGenerator/Demo/L_DungeonShowcase
```

## Included Blueprint Asset

```text
/ProceduralDungeonGenerator/Demo/BP_DungeonPreview_Showcase
```

## Public Blueprint API

- `GenerateDungeon()`
- `ClearDungeon()`
- `RegenerateWithSeed(int32 Seed)`

## Validation Target

Validated target platform:

```text
Win64
```

Recommended validation command:

```powershell
& "<UE_5.7>\Engine\Build\BatchFiles\RunUAT.bat" BuildPlugin `
  -Plugin="<YourProject>\Plugins\ProceduralDungeon\ProceduralDungeonGenerator.uplugin" `
  -Package="<OutputFolder>\ProceduralDungeonGenerator_0.1.0" `
  -TargetPlatforms=Win64 `
  -Rocket
```

## Known Limitations

- The generator uses rectangular rooms and L-shaped corridors.
- It does not place doors or gameplay objects.
- It does not generate AI navigation data.
- It does not include multiplayer replication.
- It does not include save/load or content streaming.
- Showcase gameplay is intentionally minimal and exists for presentation and validation.

## Suggested Next Features

- Door placement between rooms and corridors.
- Entrance and exit markers.
- Mesh/material presets.
- Optional room theming.
- Nav mesh validation helper.
- More compact corridor and room tuning controls.

