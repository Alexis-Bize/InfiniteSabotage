# InfiniteSabotage

![Third Person Mod](/assets/third-person-2.jpg)

The first Halo Infinite Campaign mod that requires nothing more than a simple text editor.

## Installation

* Download the latest release, or download the files in the [`build`](/build) directory.
* Navigate to your Halo Infinite installation directory (Steam).
* Open `/subgames/CampaignS1/__cms__/managed/OlympusCampaign`.
* Make a backup of the existing files.
* Copy `Easy.bin` and `sabotage.cfg` into this folder.
* Launch the Halo Infinite Campaign in Easy mode (more difficulties to come).

## Usage

Open `sabotage.cfg` with any text editor (Notepad or your preferred editor) and edit the values to enable or disable the available options. Changes are applied in real time, so there's no need to restart the game.

## Available Options

All options live in `sabotage.cfg` as a single Lua table. Below is every field, grouped by category, along with its type, default, and any behavior worth knowing about.

### Global

| Option | Type | Default | Description |
|---|---|---|---|
| `sabotage_isEnabled` | boolean | `false` | Master switch. Must be `true` for any other setting in the file to take effect. If this is `false` (or the file fails to load/parse), everything falls back to safe defaults. |

### Cheats

![No Clip Mod](/assets/no-clip-1.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `cheat_deathless` | boolean | `false` | Makes players immune to death and damage. |
| `cheat_noClip` | boolean | `false` | Disables player physics/collision, letting you fly through geometry. |
| `cheat_activeCamo` | boolean | `false` | Toggles active camouflage on players. |
| `cheat_infiniteAmmo` | boolean | `false` | Grants infinite ammo reserves. |
| `cheat_bottomlessClip` | boolean | `false` | Removes the need to reload. |

**Edge case:** `cheat_noClip` and several other systems (hologram color, creature attachment) touch physics state directly. If NoClip is on, those systems respect it rather than fighting it — you shouldn't get your physics silently re-enabled by an unrelated setting.

**Edge case — active camo + creature transformation:** while `skirmish_creatureGameplay` has attached a creature to you, active camo is controlled by the creature system (to hide your body under the creature model). Toggling `cheat_activeCamo` while a creature is attached has no effect until the creature is removed.

### Narrative

![Legendary Ending](/assets/narrative-play.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `narrative_playScene` | string | `""` | Jumps to a specific narrative scene. Valid values: `"SilentAuditorium_LegendaryEnding"`, `"SilentAuditorium_MidCredits"`. Leave empty for normal gameplay. |
| `narrative_stopCinematics` | boolean | `false` | Skips/stops any currently running cinematic and releases player control. |

**Requirement:** both of the available `narrative_playScene` values are tied to the **Silent Auditorium** mission — you need to be playing that level for either scene to load correctly. Setting this outside of Silent Auditorium won't work as expected.

**Edge case:** while any cinematic is running (including ones you didn't trigger yourself, like story beats), several settings are deliberately deferred rather than applied instantly — see **Cinematics & timing** below.

### Customization

![Laurette Agryna](/assets/spartan-laurette-agryna.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `customization_armorVariant` | string | `""` | Applies an armor variant. See the list of valid keys below. Leave empty for default armor. |
| `customization_hologramColor` | string | `""` | Applies a hologram preview color. Valid values: `"Red"`, `"Blue"`, `"Gold"`. Leave empty to disable. |

Valid `customization_armorVariant` keys: `LauretteAgryna`, `Spartan01`, `Spartan02`, `Spartan03`, `Spartan04`, `Spartan05`, `Spartan06`.

### Scale

![Laurette Agryna](/assets/spartan-tiny.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `scale_player` | number | `1` | Player model scale. Values below `0.01` are clamped up to `0.01`. |

### Camera

![Third Person Mod](/assets/third-person-1.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `camera_thirdPerson` | boolean | `false` | Switches to a third-person camera. |
| `camera_firstPersonFOV` | number | `120` | First-person field of view. Clamped between `1` and `170`. Only applied while in first person. |

**Edge case — zoom & vehicles:** third person is automatically and temporarily suppressed (switched back to the normal gameplay camera) whenever a player zooms in, drives, rides, or gunners in a vehicle. It's restored automatically the moment that condition ends — this is intentional, not a bug, and prevents third person from fighting the game's own zoom/vehicle camera.

**Edge case — cinematics:** toggling third person on/off during a cinematic doesn't fight the cinematic's camera. The setting is remembered and applied the moment the cinematic ends.

### AI

![Friendly Elite](/assets/ai-elite-friend.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `ai_killAll` | boolean | `false` | Continuously kills all AI in the zone while set to `true` — this runs on every tick, not just once, so leaving it enabled will also kill any AI that spawns or enters afterward. Set back to `false` once you're done. |
| `ai_eraseAll` | boolean | `false` | Continuously erases (removes without a kill event) all AI in the zone while set to `true`. Same continuous behavior as `ai_killAll`. |
| `ai_pauseAll` | boolean | `false` | Freezes all AI currently detected in the zone in place. Newly spawned AI may take a few seconds to be caught by the pause. |
| `ai_friendlyEnemies` | boolean | `false` | Makes enemy factions (Brutes, Forerunners, Covenant) friendly toward the player. |

### Teleport

![Machinima Mode](/assets/machima-teleport-coordinate.jpg)

| Option | Type | Default | Description |
|---|---|---|---|
| `teleport_toLocation` | boolean | `false` | Teleports the player(s) to `teleport_locationVector` when set to `true`. One-shot — set back to `false` if you don't want it re-triggering. |
| `teleport_locationVector` | table `{x, y, z}` | `{0, 0, 0}` | The destination coordinates for the teleport above. |

**Finding coordinates:** use Flycam (see the FAQ below) to fly to the spot you want, then hold **X** and press **D-Pad Right** to display the camera's current coordinate vector on screen. Copy those values into `teleport_locationVector`.

### Checkpoint

| Option | Type | Default | Description |
|---|---|---|---|
| `checkpoint_saveTrigger` | number | `0` | Forces a checkpoint save. Change this number to any new value to trigger a save — the number itself doesn't matter, only that it's different from before. |
| `checkpoint_loadTrigger` | number | `0` | Reverts to the last checkpoint. Same trigger behavior as above: change the number to fire it. |

### Skirmish

| ![Judgment Ray Gun](/assets/skirmish-judgment-ray-gun.jpg) | ![Creature Mod](/assets/creature-warthog.jpg) | 
|---|---|

| Option | Type | Default | Description |
|---|---|---|---|
| `skirmish_replaceSentinelBeamWithJudgmentRayGun` | boolean | `false` | The next time you pick up a Sentinel Beam, it's swapped for the Judgment Ray Gun instead. |
| `skirmish_creatureGameplay` | boolean | `false` | Transforms the player into a random creature currently detected in the active zone, with a matching third-person camera. |
| `skirmish_creatureScale` | number | `1` | Scale applied to the transformed creature. Clamped to a minimum floor internally to avoid degenerate sizes. |

**Edge case — no creature available:** if no creature is present in the zone (or one can't be spawned) when `skirmish_creatureGameplay` is set to `true`, the mod keeps retrying automatically every tick until a creature becomes available, rather than failing silently or permanently. You don't need to toggle it off and on again — just wait for a valid creature to be nearby.

## Cinematics & timing

A few settings are intentionally deferred rather than applied the instant you edit the file, to avoid fighting the game's own cinematic camera and transitions:

* **Camera changes** (`camera_thirdPerson`, third-person framing) made while a cinematic is playing are held and applied automatically once the cinematic ends.
* **Armor variant and hologram color** are re-applied as soon as a cinematic starts, since the game itself can reset these when a cinematic takes over — you may still briefly see them revert or flicker if the game reasserts its own state after the mod re-applies yours.
* Once a cinematic ends, the mod does a full re-sync of your settings, so nothing gets left stale — but this happens shortly after the cinematic finishes rather than instantaneously, to give the game time to fully hand control back to the player.
* All of the above is scoped to `sabotage_isEnabled` — the game's own cinematics (including its opening/intro) are left completely alone while the mod is disabled.

## FAQ

### How does InfiniteSabotage work?

InfiniteSabotage leverages Halo Infinite's shared game variants to dynamically read the `sabotage.cfg` file and apply your selected settings at runtime.

The mod is limited to the functionality exposed by the game's configuration system. For your own safety, avoid modifying the configuration beyond the documented options unless you know exactly what you're doing.

You are solely responsible for how you use this mod.

### Can I get banned for using InfiniteSabotage?

While there's never a zero-risk guarantee, Halo Infinite's Campaign does not require an internet connection or Easy Anti-Cheat. As a result, the risk of being banned is considered extremely low.

That said, you are solely responsible for your use of this mod.

### Does InfiniteSabotage support a flycam?

Yes! Machinima controls are enabled in all game variants.

Using a controller, hold **X** and press **D-Pad Up** to enable Flycam. Hold **X** and press **D-Pad Right** to toggle the camera's coordinate vector display.

### Does InfiniteSabotage support a third-person mode?

Yes! Set `camera_thirdPerson` to `true` in `sabotage.cfg`. See the **Camera** section above for details and edge cases (zoom/vehicle suppression, cinematic handling).

### Where can I share feedback or suggestions?

Feel free to open an issue on this GitHub repository or reach out on X: https://x.com/gruntdotapi.
