# Changelog

All notable changes to SpawnProtect plugin will be documented in this file.

---

## [1.0.1] - 2024-11-09

### Requirements
- **Minimum Endstone Version:** 0.5.0


### Added
- **Actionbar Notification System:**
  - Automatic notifications when entering/leaving safe zone
  - Green bold message on zone entry: "§a§lSafe zone"
  - Red bold message on zone exit: "§c§lNot in Safe zone"
  - Messages shown once per zone transition
  - Customizable messages via config.toml

- **Player Session Tracking:**
  - Individual tracking for each player's safe zone status
  - Automatic cleanup on player disconnect
  - Prevents memory leaks from disconnected players

- **Automatic Zone Detection:**
  - Server checks player positions every second (20 ticks)
  - Smooth zone transition detection
  - Efficient position checking algorithm

### Changed
- **Configuration File Structure:**
  - Simplified config path: `plugins/spawn_protect/config.toml` (removed duplicate folder)
  - Removed `safe_message` option (always uses actionbar now)
  - Added detailed comments explaining each configuration option
  - Config now uses inline comments for better readability

- **Protection Logic:**
  - Simplified event handlers for better performance
  - Moved OP check before event cancellation
  - Optimized spawn area distance calculation
  - All protection checks use consistent logic pattern

### Fixed
- **Critical Fixes:**
  - Fixed duplicate folder creation in plugin directory (`spawnprotect/spawnprotect` → `spawn_protect`)

- **Message Delivery Fixes:**
  - Fixed broadcast messages showing to all players (now individual only)

- **Deprecated Code:**
  - Removed `event.cancelled` property usage
  - Removed unused imports and methods


### Technical Details
- **Event Handlers:**
  - `BlockBreakEvent` - Prevents block breaking by non-OPs
  - `BlockPlaceEvent` - Prevents block placing by non-OPs
  - `PlayerInteractEvent` - Blocks interactions with chests, doors, etc.
  - `ActorDamageEvent` - Prevents all damage in safe zone (PvP, PvE, environmental)
  - `ActorExplodeEvent` - Blocks all explosion damage to blocks
  - `PlayerJoinEvent` - Initializes player safe zone tracking
  - `PlayerQuitEvent` - Cleans up player data on disconnect

- **Performance Optimizations:**
  - Zone check runs every 20 ticks (1 second) via scheduler
  - Distance calculation uses 2D distance (X and Z only) for efficiency
  - Early return for OP players to skip unnecessary checks
  - Event cancellation happens before message sending

- **Code Structure:**
  - Uses `send_tip()` for actionbar notifications
  - Uses `send_message()` with `ColorFormat.RED` for error messages
  - Consistent error handling across all event handlers
  - Clear separation of concerns between events

### Known Limitations
- Protection is circular (based on X-Z distance, not 3D sphere)
- Y-coordinate (height) is not considered in protection radius
- OPs can bypass all protection (by design)
- Messages use actionbar which can be overridden by other plugins

### Configuration Example
```toml
# SpawnProtect Configuration File
# Protection radius in blocks from spawn point
radius = 20

# Error message shown when player tries to break/place blocks
message = "You cannot do this near spawn!"

# Message when entering safe zone (actionbar)
in_safe_zone_message = "Safe zone"

# Message when leaving safe zone (actionbar)
not_in_safe_zone_message = "Not in Safe zone"

# Spawn location (set using /setspawn command)
[spawn_location]
x = 0
y = 64
z = 0
world = "world"
```

---

## [1.0.0] - 2024-11-06

### Added
- Initial release
- Basic spawn protection system
- `/setspawn` command for setting protection point
- Block break/place protection in configurable radius
- Player interaction blocking (chests, doors, buttons, etc.)
- Configurable protection radius (default: 20 blocks)
- Basic config.toml file generation
- OP bypass for all protections

### Known Issues (Fixed in 1.0.1)
- Messages not showing in survival mode
- Explosions could destroy blocks
- Scoreboard display had compatibility issues
- Duplicate folder creation in config path
