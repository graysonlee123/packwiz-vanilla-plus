# Vanilla+

Personal and opinionated Minecraft Vanilla+ modpack, distributable via [packwiz](https://github.com/packwiz/packwiz).

Focused on [Prism launcher](https://prismlauncher.org/).

## Development

Use Nix to create a ephemeral shell with the `packwiz` binary. Alternatively, install `packwiz` manually.

```shell
# Development shell
nix develop

# Build Modrinth export file (one-shot)
nix develop --command packwiz modrinth export
```

## Installation/Updates

There are two methods for getting up-and-running: automatic (recommended) and manual.

### Automatic

Use [packwiz-installer-bootstrap](https://github.com/packwiz/packwiz-installer-bootstrap) to enable automatic installation/updates at game launch.

1. Create instance in Prism, matching target Minecraft version and Fabric loader version. Alternatively, follow the manual steps, then proceed to step 2.
2. Get [latest boostrap jar](https://github.com/packwiz/packwiz-installer-bootstrap) and drop it into the instance's root `minecraft/` folder.
3. Add Prism pre-launch command, defined below (instance → Edit → Settings → Custom Commands → Pre-launch Command).
4. Launch, and the install/updates should automatically take place.

Prism pre-launch command:

```shell
# Local repository (useful during testing)
"$INST_JAVA" -jar packwiz-installer-bootstrap.jar file:///home/gray/repos/me/packwiz-vanilla-plus/pack.toml

# Remote repository (useful for sharing)
"$INST_JAVA" -jar packwiz-installer-bootstrap.jar https://raw.githubusercontent.com/graysonlee123/packwiz-vanilla-plus/main/pack.toml
```

`$INST_JAVA` is injected by Prism.

### Manual

1. Run `packwiz modrinth export`, and notate created `.mrpack` file's path.
2. In Prism launcher, "Add Instance" > "Import". Then, select your `.mrpack` file.
3. Click "OK".

## Migrating Between Instances

When moving to a new instance (new Minecraft version, fresh install, or another machine), copy the following from the old instance's `minecraft/` folder to the new one. Mods and shipped configs are handled by packwiz and should not be copied.

- `saves/` — singleplayer worlds (includes stats, advancements, and per-world Distant Horizons LODs).
- `schematics/` — Litematica schematics (see `customSchematicBaseDirectory`).
- `xaero/` — Xaero's World Map data (per world/server).
- `Distant_Horizons_server_data/` — Distant Horizons LOD data for multiplayer servers.
- `resourcepacks/` — resource packs (e.g. VanillaTweaks) referenced by `options.txt`.
- `servers.dat` — multiplayer server list.
- `options.txt` — keybinds and video/personal settings (not shipped by the pack).
- `screenshots/` — optional.
- `config/` — only for mods whose config is not shipped by the pack; shipped configs install automatically.

Do not copy `mods/`, `logs/`, `crash-reports/`, or `.mixin.out/`.

## Configuration

Configuration files included in this modpack are cherry-picked and limited. Configuration files not modified from their defaults are not included. Mod configuration files are only created if they are missing; existing files are never replaced.

### REI

Changes from default (`config/roughlyenoughitems/`):

**config.json5**:

- `focusSearchFieldKeybind`: `unknown` → `enter`
- `appearance.recipeScreenType`: `UNSET` → `ORIGINAL`
- `appearance.layout.searchFieldLocation`: `CENTER` → `BOTTOM_SIDE`
- `appearance.recipeBorder`: `DEFAULT` → `NONE`
- `appearance.horizontalEntriesBoundariesColumns`: `50` → `12`
- `appearance.verticalEntriesBoundariesRows`: `1000` → `24`
- `appearance.leftSideMobEffects`: `false` → `true`
- `advanced.tooltips.appendModNames`: `true` → `false`

**favorites.json5**:

- `favorites`: added utility favorites — gamemode (survival, creative), weather (clear, rain, thunder), time (morn, noon, evening, night)

### Litematica

Changes from default (`config/litematica.json`):

- `customSchematicBaseDirectory`: machine-specific path → `""` (left blank; set per-instance)
- `ignoreExistingFluids`: `false` → `true`
- `ignoreCropAge`: `false` → `true`
- `renderBlocksAsTranslucent`: `false` → `true`
- `schematicOverlayEnableOutlines`: `true` → `false`
- `ghostBlockAlpha`: `0.5` → `0.4`

### Mod Menu

Changes from default (`config/modmenu.json`):

- `compact_list`: `false` → `true`
- `mods_button_style`: `classic` → `replace_realms`

### Scribble

Changes from default (`config/scribble.client.json`):

- `pages_to_show`: `1` → `2`

### MiniHUD

TODO

### Better Clouds

Changes from default (`config/betterclouds-v1.json`):

- `yRange`: `64.0` → `42.0`
- `yOffset`: `0.0` → `24.0`
- `sparsity`: `0.0` → `0.48`
- `spacing`: `5.25` → `3.0`
- `sizeXZ`: `16.0` → `19.0`
- `sizeY`: `8.0` → `12.0`
- `travelSpeed`: `0.03` → `0.04`
- `windSpeedFactor`: `0.8` → `1.0`
- `colorVariationFactor`: `0.8` → `1.0`
- `samplingScale`: `1.0` → `1.09`
- `scaleFalloffMin`: `0.25` → `1.0`
- `presets`: `[]` → added shader presets (BSL, Chocapic13, Complementary, Kappa, etc.)

### Distant Horizons

Changes from default (`config/DistantHorizons.toml`):

- `common.logging.logRendererGLEventToChat`: `ERROR` → `DISABLED`
- `client.advanced.autoUpdater.enableAutoUpdater`: `true` → `false`
- `client.advanced.graphics.overrideVanillaGraphicsSettings`: `true` → `false`
- `client.advanced.graphics.experimental.renderingEngine`: `AUTO` → `OPEN_GL` (required for Better Clouds to render correctly alongside DH)
- `client.advanced.graphics.genericRendering.enableCloudRendering`: `true` → `false` (Better Clouds handles cloud rendering)
- `client.advanced.graphics.texture.enableTexturedLods`: `true` → `false` (works around DH 3.2.0-b beta bug streaking MC 26.1.2 two-layer leaf LODs)

### ItemSwapper

TODO

## Resource Packs

Resource packs are not shipped with the pack. Download and drop them into the instance's `resourcepacks/` folder, then enable in-game.

- [VanillaTweaks](https://vanillatweaks.net/share#OCyRBD) — regenerate the exact selection from this share link.

## Video Settings

Video/graphics settings live in vanilla `options.txt`, not per-mod config, so they are documented here rather than shipped.

Format: default → custom.

- `chunkSectionFadeInTime`: `0.75` → `0.0`
- `enableVsync`: `true` → `false`
- `graphicsPreset`: `fancy` → `custom`
- `cloudRange`: `64` → `128`
- `renderDistance`: `16` → `8`

## Keybinds

Keybinds live in vanilla `options.txt`, not per-mod config, so they are documented here rather than shipped.

Format: default → custom.

### Vanilla

- Chat: `T` → `Enter`
- Toggle Perspective: `F5` → `Mouse 5`

### Xaero's World Map

- Open World Map: `M` → `` ` ``

### Zoomify

- Zoom: `C` → `Z`

### Light Overlay

- Toggle: `F9` → `Mouse 4`

### Presence Footsteps

- Debug Toggle: `Z` → unbound

