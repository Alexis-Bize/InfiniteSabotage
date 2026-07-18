# Changelog

## 0.3.0

### Added
- New armor variant: **Samurai**.
- New vehicles you can teleport directly into: **Pelican** and **Phantom**.
- New Death FX option, letting you trigger a custom death effect on elimination.

### Fixed
- Fixed player movement speed not scaling correctly when the player's size was increased — bigger players now move faster in proportion to their actual scale, instead of using a flat/incorrect value.
- Various other bugfixes and stability improvements across cheats, camera handling, and cleanup on game end.

### Improved
- Optimized the mod's overall bundle size.

### Compatibility
- Originally designed and tested against the Steam version of Halo Infinite, but confirmed to also work on the Xbox PC app version.

## 0.2.0

### Fixed
- Fixed a bug where the first-person camera could misbehave right after launching the game, even with the mod disabled.
- Fixed cleanup not running properly when a game session ended, which could leave stale state carrying over into the next session.
- Fixed several settings not correctly re-syncing after a cinematic ended.
- Fixed the third-person camera occasionally using the wrong framing after switching out of creature mode.
- Fixed active camo conflicting with creature transformation in certain cases.

### Added
- New cheats: infinite ammo and bottomless clip.
- New AI options: continuously erase all AI, and pause/freeze all AI in the zone.
- New checkpoint options: trigger a save or revert to the last checkpoint directly from the config file.
- New skirmish option to swap the Sentinel Beam for the Judgment Ray Gun on pickup.
- Renamed the god mode cheat to "deathless" for clarity.

### Improved
- Reduced the number of times the game is scanned per settings update by batching related changes together, improving performance when several

## 0.2.0

### Fixed
- Fixed a bug where the first-person camera could misbehave right after launching the game, even with the mod disabled.
- Fixed cleanup not running properly when a game session ended, which could leave stale state carrying over into the next session.
- Fixed several settings not correctly re-syncing after a cinematic ended.
- Fixed the third-person camera occasionally using the wrong framing after switching out of creature mode.
- Fixed active camo conflicting with creature transformation in certain cases.

### Added
- New cheats: infinite ammo and bottomless clip.
- New AI options: continuously erase all AI, and pause/freeze all AI in the zone.
- New checkpoint options: trigger a save or revert to the last checkpoint directly from the config file.
- New skirmish option to swap the Sentinel Beam for the Judgment Ray Gun on pickup.
- Renamed the god mode cheat to "deathless" for clarity.

### Improved
- Reduced the number of times the game is scanned per settings update by batching related changes together, improving performance when several options change at once.
- General internal cleanup and consistency pass across the mod's settings-handling code.

## 0.1.0

- Initial public release.
