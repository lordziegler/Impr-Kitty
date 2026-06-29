# kitty — Imperator configuration

> *"I must not fear. Fear is the mind-killer."*
> — Paul Atreides

Kitty terminal configuration for the **Imperator** ricing — amber CRT palette, frosted glass effect via Wayland compositor blur, powerline slanted tab bar with golden hierarchy.

---

### Showcase

[Kitty & NVim](kitty/assets/img1.png)

[kitty & bat](kitty/assets/img2)

[kitty, cava & btop](kitty/assets/img3.png)

---

## What this configures

| File | Purpose |
|------|---------|
| `kitty.conf` | Main config — fonts, cursor, tabs, keybindings, frosted glass |
| `Imperator.conf` | Canonical theme palette (source of truth for all 16 ANSI colors) |
| `current-theme.conf` | Active theme include — loaded by `kitty.conf` via `BEGIN_KITTY_THEME` block |

---

## Dependencies

| Tool | Purpose | Install |
|------|---------|---------|
| `kitty` | Terminal emulator ≥ 0.35 | `pacman -S kitty` |
| `JetBrainsMonoNL Nerd Font Mono` | Primary font with ligatures and Nerd Font glyphs | `pacman -S ttf-jetbrains-mono-nerd` |
| A Wayland compositor with blur support | Frosted glass effect (niri, KDE, etc.) | — |

---

## Paths

| Context | Path |
|---------|------|
| Active config | `~/.config/kitty/` |
| This repo | `kitty/` |

---

## Installation

```sh
# 1. Back up existing config (optional)
mv ~/.config/kitty ~/.config/kitty.bak

# 2. Copy or symlink the config directory
ln -s "$PWD/kitty" ~/.config/kitty
# or: cp -r kitty ~/.config/kitty

# 3. Place the theme in the themes subdirectory
mkdir -p ~/.config/kitty/themes
cp kitty/Imperator.conf ~/.config/kitty/themes/Imperator.conf

# 4. Reload kitty
# Press ctrl+shift+F5 inside a running kitty window, or restart kitty
```

If you prefer kitty's built-in theme manager instead of symlinking:

```sh
kitty +kitten themes --reload-in=all Imperator
```

This regenerates `current-theme.conf` automatically from `themes/Imperator.conf`.

---

## Frosted glass

The frosted glass effect requires:

1. A transparent wallpaper visible behind the terminal (`background_opacity 0.55`).
2. Compositor-side blur. On **niri**, configure blur in `~/.config/niri/config.kdl`. On **KDE**, enable blur in window decoration settings.

`background_blur 64` is a hint sent to the compositor. The actual blur radius is compositor-controlled — kitty does not apply blur itself on Linux/Wayland.

---

## Keybindings

| Key | Action |
|-----|--------|
| `ctrl+shift+t` | New tab |
| `ctrl+shift+w` | Close tab |
| `ctrl+shift+←/→` | Previous / next tab |
| `ctrl+shift+enter` | New window |
| `ctrl+shift+h` | Horizontal split |
| `ctrl+shift+b` | Vertical split |
| `ctrl+shift+c/v` | Copy / paste |
| `ctrl+= / ctrl+-` | Font size +2 / -2 |
| `ctrl+0` | Reset font size |
| `f11` | Toggle fullscreen |

---

## Compatibility

- Tested on **kitty 0.47.1** (Arch Linux / CachyOS, Wayland/niri).
- Requires a Nerd Font for tab bar glyphs (`◆`, powerline arrows).
- `text_composition_strategy legacy` is set for correct glyph rendering on some Wayland compositors.
- `shell_integration no-cursor` disables kitty's cursor override so the shell prompt controls the cursor shape.
