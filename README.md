# 🛡️ Endstone SpawnProtect (Beta)

A lightweight **spawn protection plugin** for **Endstone API** (Minecraft Bedrock Edition).  
Prevents players and mobs from modifying or damaging the area around the spawn point.

---

## ⚙️ Features
- Protects the spawn area within a configurable radius (default: 20 blocks)  
- Blocks:
  - Block breaking  
  - Block placing  
  - Player interaction  
  - Player and mob damage near spawn  
- `/setspawn` command to define a new spawn protection point  
- Automatically creates and manages configuration files  

---

## 📦 Installation
1. Download the `.whl` file of **endstone_spawn_protect**  
2. Move it to your server’s `plugins` folder  
3. Restart the server  
4. In-game, use:
   ```
   /setspawn
   ```

---

## ⚙️ Configuration
After the first run, a config file will be created at:
```
plugins/spawnprotect/config.toml
```

### Example:
```toml
radius = 20
message = "You cannot do this near spawn!"

[spawn_location]
x = 0
y = 64
z = 0
world = "world"
```

**Options:**
- `radius` — radius of protected area  
- `message` — message shown to players when an action is blocked  
- `spawn_location` — updated automatically after `/setspawn`  

---

## 🧩 Commands
| Command | Description | Permission |
|----------|--------------|-------------|
| `/setspawn` | Sets a new spawn protection point | `spawnprotect.setspawn` *(OP only)* |

---

## 🧱 Events Blocked
- `BlockBreakEvent` — block breaking  
- `BlockPlaceEvent` — block placing  
- `PlayerInteractEvent` — interaction with blocks  
- `ActorDamageEvent` — player or mob damage in protected zone  

---

---

## 👤 Author
**foityeD**  
Version: `1.0.0`  

---

> Simple. Fast. Secure. Keep your spawn safe.
