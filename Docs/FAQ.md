# FAQ

## Where is the documentation?

Public documentation is available in this repository:

```text
https://github.com/yuri-cherkasov90/procedural-dungeon-generator-docs
```

The plugin package also includes `README.md` and the `Docs/` folder.

## Does this plugin work from Blueprint?

Yes. Use `Dungeon Preview Actor` for editor preview, or add `DungeonGeneratorComponent` to your own actor or Blueprint.

The public Blueprint API is:

- `GenerateDungeon()`
- `ClearDungeon()`
- `RegenerateWithSeed(int32 Seed)`

## Is generation deterministic?

Yes. The generator uses a seed-based random stream. The same seed, settings, plugin version, and algorithm implementation produce the same layout.

## Does it spawn one actor per tile?

No. Floor, wall, and debug visualization tiles are rendered with `UInstancedStaticMeshComponent`.

## Can I use my own meshes?

Yes. Assign your own static meshes to the floor and wall mesh settings on `DungeonGeneratorComponent`.

## Does it include doors, enemies, loot, or AI navigation?

No. Version `0.1.0` focuses on dungeon layout generation, editor/runtime generation, Blueprint access, instanced mesh rendering, demo maps, and debug visualization.

## Is multiplayer replication included?

No. Network replication is not included in this MVP.

## Which platforms are supported?

The plugin is validated for Unreal Engine 5.7 on Windows with Win64 target builds.
