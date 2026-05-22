<!-- ============================================================
     bLite — README.md
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

**bLite** is a from-scratch remake of a private Minecraft utility client — rebuilt clean, documented, and open for anyone who wants to learn how anticheat bypass actually works under the hood.

It's not just a cheat client. It's a **dissection of modern anticheat systems** — how they detect, what they flag, and how movement/packet manipulation can be tuned to stay under the radar. Whether you're a developer studying game security or a modder building something new, bLite is the annotated lab report.

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

| Module | Description | Bypass Notes |
|---|---|---|
| `KillAura` | Auto-targets and attacks nearby entities | Rotations randomized per-tick; swing timing jittered |
| `Reach` | Extends melee attack range | Delta capped to avoid server-side trace rejection |
| `Velocity` | Reduces knockback taken | Packet-level horizontal/vertical multipliers |
| `AutoClicker` | CPS automation with humanization | Gaussian distribution on delays; no fixed intervals |
| `AimAssist` | Smooth aim correction | FOV-gated, speed-limited, no snap |

</details>

<details>
<summary><b>🏃 Movement</b></summary>

| Module | Description | Bypass Notes |
|---|---|---|
| `Speed` | Move faster than base walkspeed | Ground-strafe, bunny-hop, and timer modes |
| `Sprint` | Auto-sprint in all directions | Removes vanilla sprint restrictions |
| `NoFall` | Cancel fall damage | Packet-based; sends ground flag before impact |
| `Flight` | Freefly / glide modes | NCP creative simulation, vanilla glide blending |
| `Step` | Step up blocks > 0.6 height | Incremental Y-spoofing to avoid clip detection |

</details>

<details>
<summary><b>📦 World / Misc</b></summary>

| Module | Description | Bypass Notes |
|---|---|---|
| `ESP` | Entity/player boxes through walls | Render-only; zero packet changes |
| `Fullbright` | Max brightness, no gamma dependency | Client-side gamma override |
| `NoRotate` | Ignore server-sent look packets | Strips `PlayerLookPacket` before dispatch |
| `Scaffold` | Tower/bridge block placement | Legit mode uses real rotations + delay variance |
| `Freecam` | Detached spectator camera | Suppresses position packets during session |

</details>

---

## ▸ Anticheat Coverage

bLite has been tested and tuned against the following systems:

```
┌──────────────────┬────────────────────────────────────────────┐
│ Anticheat        │ Status                                     │
├──────────────────┼────────────────────────────────────────────┤
│ NCP              │ ✅ Most checks bypassed (configurable)      │
│ AAC              │ ✅ Movement + combat modules functional      │
│ Grim             │ ⚠️  Partial — strict prediction is hard    │
│ Spartan          │ ✅ Stable across combat modules             │
│ Intave           │ ⚠️  Limited — under active research        │
│ Vulcan           │ ✅ Rotation + velocity bypassed             │
│ Matrix           │ ✅ Full bypass on most modules              │
└──────────────────┴────────────────────────────────────────────┘

  ✅ = Tested, working    ⚠️  = Partial / WIP    ❌ = Detected
```

> **Note:** Anticheat software updates constantly. Bypass status may drift. PRs with updated configs are welcome.

---

## ▸ Architecture

```
bLite/
├── src/
│   ├── client/
│   │   ├── BLite.java              ← Entry point, mod init
│   │   ├── ModuleManager.java      ← Module registry + tick dispatch
│   │   └── EventBus.java           ← Lightweight event system
│   ├── modules/
│   │   ├── combat/                 ← KillAura, Reach, Velocity, etc.
│   │   ├── movement/               ← Speed, Flight, NoFall, etc.
│   │   └── misc/                   ← ESP, Freecam, etc.
│   ├── mixins/                     ← Mixin patches into MC internals
│   ├── utils/
│   │   ├── RotationUtils.java      ← Silent/legit rotation helpers
│   │   ├── PacketUtils.java        ← Packet send/cancel/spoof helpers
│   │   └── TimerUtils.java         ← Tick rate manipulation
│   └── gui/
│       ├── ClickGUI.java           ← In-game module panel
│       └── HUD.java                ← On-screen overlays
├── gradle/
└── build.gradle
```

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

bLite is annotated as a **learning tool**. Every bypass technique links back to why it works:

- **[`RotationUtils.java`](src/utils/RotationUtils.java)** — explains the difference between silent rotations (server-side only) and legit rotations (client + server synced), and why each matters for different anticheat checks.
- **[`PacketUtils.java`](src/utils/PacketUtils.java)** — documents which packet fields anticheats read and how spoofing them triggers (or avoids) flags.
- **[`modules/movement/`](src/modules/movement/)** — each file has a header explaining the AC detection vector it's designed around.

If you're here to learn, start with the `utils/` folder — that's where the real meat is.

---

## ▸ Contributing

PRs are open. If you've found a new bypass, refined an existing one, or added support for a newer version:

1. Fork the repo
2. Branch off `main` (`git checkout -b feat/your-module`)
3. Keep commits atomic and descriptive
4. Submit a PR with bypass context — _what does it evade and why?_

Bug reports with reproduction steps and AC version info are gold.

---

## ▸ Disclaimer

bLite is published for **educational and research purposes**. Understanding how game security works — from both sides — is a legitimate field of study. Using this client on servers without permission may violate their rules or terms of service. You're responsible for how you use it.

Don't be stupid about it.

---

<div align="center">

**bLite** · built with ☕ and packet inspection

*Star the repo if it taught you something.*

</div>
