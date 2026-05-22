<!-- ============================================================
     bLite - README.md
     ============================================================ -->

<div align="center">

```
██████╗ ██╗     ██╗████████╗███████╗
██╔══██╗██║     ██║╚══██╔══╝██╔════╝
██████╔╝██║     ██║   ██║   █████╗  
██╔══██╗██║     ██║   ██║   ██╔══╝  
██████╔╝███████╗██║   ██║   ███████╗
╚═════╝ ╚══════╝╚═╝   ╚═╝   ╚══════╝
```

**The lightweight Minecraft utility client. 1.8 → 1.21.1**

[![Version](https://img.shields.io/badge/version-1.0.0-00ff88?style=for-the-badge&logo=github&logoColor=white)](https://github.com)
[![MC Versions](https://img.shields.io/badge/MC-1.8%20→%201.21.1-0099ff?style=for-the-badge)](https://minecraft.net)
[![License](https://img.shields.io/badge/license-MIT-ff4444?style=for-the-badge)](LICENSE)
[![Stars](https://img.shields.io/github/stars/yourusername/bLite?style=for-the-badge&color=ffcc00)](https://github.com)

> *"Know your enemy. Know yourself."*

</div>

---

## ▸ What is bLite?

**bLite** is a from-scratch remake of a private Minecraft utility client - rebuilt clean, documented, and open for anyone who wants to learn how anticheat bypass actually works under the hood.

It's not just a cheat client. It's a **dissection of modern anticheat systems** - how they detect, what they flag, and how movement/packet manipulation can be tuned to stay under the radar. Whether you're a developer studying game security or a modder building something new, bLite is the annotated lab report.

```
Supported versions ──────────────────────────────────────────────────────────
  Legacy    │  1.8.x  │  The PvP era. Optimized CPS, reach, velocity.
  Modern    │  1.9 – 1.21.1  │  Post-combat update. Full feature parity.
─────────────────────────────────────────────────────────────────────────────
```

---

## ▸ Feature Matrix

<details>
<summary><b>⚔️ Combat</b></summary>

| Module | Description |
|---|---|
| `KillAura` | Auto-targets and attacks nearby entities |
| `Reach` | Extends melee attack range |
| `Velocity` | Reduces knockback taken |
| `AutoClicker` | CPS automation with humanization |
| `AimAssist` | Smooth aim correction |

</details>

<details>
<summary><b>🏃 Movement</b></summary>

| Module | Description |
|---|---|
| `Speed` | Move faster than base walkspeed |
| `Sprint` | Auto-sprint in all directions |
| `NoFall` | Cancel fall damage |
| `Flight` | Freefly / glide modes |
| `Step` | Step up blocks > 0.6 height |

</details>

<details>
<summary><b>📦 World / Misc</b></summary>

| Module | Description |
|---|---|
| `ESP` | Entity/player boxes through walls |
| `Fullbright` | Max brightness, no gamma dependency |
| `NoRotate` | Ignore server-sent look packets |
| `Scaffold` | Tower/bridge block placement |
| `Freecam` | Detached spectator camera |

</details>

---

## ▸ Anticheat Coverage

bLite has been tested and tuned against the following systems:

```
┌──────────────────┬────────────────────────────────────────────┐
│ Anticheat        │ Status                                     │
├──────────────────┼────────────────────────────────────────────┤
│ NCP              │ ✅ Most checks bypassed                   │
│ AAC              │ ✅ Movement + combat modules functional   │
│ Grim             │ ⚠️  Partial - strict prediction is hard   │
│ Spartan          │ ✅ Stable across combat modules           │
│ Intave           │ ⚠️  Limited functionality                 │
│ Vulcan           │ ✅ Rotation + velocity bypassed           │
│ Matrix           │ ⚠️ Limited functionality - combat works   │
└──────────────────┴────────────────────────────────────────────┘

  ✅ = Tested, working    ⚠️  = Partial / WIP    ❌ = Detected
```

> **Note:** Anticheat software updates constantly. Bypass status may drift. PRs with updated configs are welcome.

---

## ▸ Getting Started

### Prerequisites

- Java 17+
- Gradle 8+
- Minecraft with Fabric (recommended) or Forge loader

### Build

```bash
git clone https://github.com/yourusername/bLite.git
cd bLite
./gradlew build
```

Output jar lands in `build/libs/`. Drop it into your mods folder.

### Usage

| Keybind | Action |
|---|---|
| `Right Shift` | Open ClickGUI |
| `Insert` | Toggle HUD |
| Module panel | Click to enable · Right-click to configure |

---

## ▸ Learning Resources

bLite is annotated as a **learning tool**. Every bypass technique links back to why it works.

---

## ▸ Contributing

PRs are open. If you've found a new bypass, refined an existing one, or added support for a newer version, feel free to fork the repo.

Bug reports with reproduction steps and AC version info are gold.

---

## ▸ Disclaimer

bLite is published for **educational and research purposes**. Understanding how game security works - from both sides - is a legitimate field of study. Using this client on servers without permission may violate their rules or terms of service. You're responsible for how you use it.

Don't be stupid about it.

---

<div align="center">

**bLite** · built with love and packet inspection

*Star the repo if it taught you something.*

</div>
