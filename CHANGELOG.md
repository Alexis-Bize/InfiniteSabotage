# Changelog

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
