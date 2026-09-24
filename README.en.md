# AULA F75 + Kanata

![AULA F75 + Kanata](assets/cover.png)

[🇧🇷 Português](README.md) · 🇺🇸 English

A custom layout for the **AULA F75** keyboard using [Kanata](https://github.com/jtroo/kanata), a software key remapper. The keyboard firmware is not modified (no QMK/VIA).

```
AULA F75  →  operating system  →  Kanata  →  custom layout
```

| System | Status | Config | Guide |
|---|---|---|---|
| Windows | ✅ working | [`config/windows/f75.kbd`](config/windows/f75.kbd) | [docs/en/windows.md](docs/en/windows.md) |
| Linux (Ubuntu 24.04) | ✅ working | [`config/linux/f75.kbd`](config/linux/f75.kbd) | [docs/en/linux.md](docs/en/linux.md) |
| macOS | 🚧 in progress | – | [docs/en/macos.md](docs/en/macos.md) |

Project milestones: [docs/en/milestones.md](docs/en/milestones.md)

## The keyboard

- 75% layout, hot-swap, RGB, rotary knob
- Connectivity: USB-C, 2.4 GHz and Bluetooth. Kanata works with any of them.
- USB VID `258A` / PID `010C`, SinoWealth chipset
- US (ANSI) keycap legends with Brazilian ABNT2 sub-legends

## Assumptions

1. **OS keyboard layout: Portuguese (Brazil) ABNT2.** Kanata sends key positions, and the OS layout decides which character appears. With a different layout (e.g. US), several keys will produce other characters.
2. **Fn swapped with Right Ctrl in the AULA software.** The stock Fn key is handled by the firmware and never reaches the OS, so Kanata cannot see it. In the official AULA software (Key assignment → Default), the Fn position is set to send **RCtrl** and the Right Ctrl position becomes **FN**. The swap is stored on the keyboard and works on any computer.

In this repository, the key right of Space (which sends RCtrl) is called **UTIL**. It works as a custom "AltGr".

## Layers

### BASE

Only keys that differ from the keycap legends are listed.

| Physical key | Alone | Shift |
|---|---|---|
| Left of 1 | `~` (dead key) | `` ` `` (dead key) |
| 6 | `6` | `^` (dead key) |
| Right of P | `{` | `[` |
| 2nd right of P | `}` | `]` |
| 3rd right of P | `\` | `\|` |
| Right of L | `;` | `:` |
| 2nd right of L | `"` | `'` |
| `/` | `/` | `?` |

Dual-function keys (tap-hold):

| Key | Tap | Hold |
|---|---|---|
| Tab | Tab | **NAV** layer |
| J | j | ← |
| UTIL (right of Space) | Ctrl | **UTIL** layer |

### UTIL (hold the key right of Space)

| Key | Alone | Shift |
|---|---|---|
| Q | `/` | – |
| W | `?` | – |
| Right of P | `´` (dead key) | `` ` `` (dead key) |
| 2nd right of P | `ª` | – |
| 3rd right of P | `º` | – |
| Right of L | `ç` | `Ç` |
| 2nd right of L | `~` (dead key) | `^` (dead key) |
| Z / X / C | previous track / play-pause / next track | – |

### NAV (hold Tab)

| Key | Function |
|---|---|
| I / J / K / L | ↑ / ← / ↓ / → |
| U / O | Home / End |
| Y / H | PgUp / PgDn |
| Backspace | Delete |

Dead keys: press the accent, then the letter (`~` + `a` = `ã`). For the bare symbol, press the accent, then Space.

## Emergency exit

**Left Ctrl + Space + Esc** quits Kanata immediately on any OS.

## Repository layout

```
config/
  windows/f75.kbd     Windows config
  linux/f75.kbd       Linux config
  macos/              in progress
docs/
  *.md                guides in Portuguese
  en/*.md             guides in English
  image-prompt.md     prompt to generate the layer diagram
linux/
  kanata.service      systemd user service
assets/
  cover.png           cover image
```

## Windows vs Linux

Both configs do the same thing. Only the way some characters are produced differs:

| Character | Windows | Linux |
|---|---|---|
| `/ ?` (UTIL + Q/W and `/` key) | direct Unicode | ABNT2 extra key (`ro`) |
| `ª º` | direct Unicode | AltGr + ABNT2 key |
| everything else | ABNT2 key | ABNT2 key |

On Linux, Kanata's Unicode output relies on the Ctrl+Shift+U shortcut, which many apps don't support, so native ABNT2 keys are used there instead.
