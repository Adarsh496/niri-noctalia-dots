<div align="center">

# ✨ CachyOS · niri · Noctalia

**A blurry, translucent, wallpaper-themed Wayland rice**

![CachyOS](https://img.shields.io/badge/CachyOS-Arch-1793D1?style=for-the-badge&logo=archlinux&logoColor=white)
![niri](https://img.shields.io/badge/WM-niri_26.04-F5A97F?style=for-the-badge)
![Noctalia](https://img.shields.io/badge/Shell-Noctalia-C6A0F6?style=for-the-badge)
![kitty](https://img.shields.io/badge/Terminal-kitty-8AADF4?style=for-the-badge)
![Stars](https://img.shields.io/github/stars/Adarsh496/niri-noctalia-dots?style=for-the-badge&color=F5BDE6)

<!-- Put your best screenshot here -->
<img src="screenshots/main.png" alt="Desktop preview" width="90%">

</div>

---

## 📸 Gallery

| Terminal + fastfetch | Firefox + Nautilus | Lock screen |
|---|---|---|
| ![](screenshots/terminal.png) | ![](screenshots/apps.png) | ![](screenshots/lock.png) |

<!-- Rename or replace the images above with your own files in /screenshots -->

---

## 🧩 What's inside

| Component | Choice |
|---|---|
| **Distro** | CachyOS |
| **Compositor** | [niri](https://github.com/niri-wm/niri) 26.04 (scrollable-tiling, Wayland) |
| **Shell / bar** | [Noctalia](https://github.com/noctalia-dev/noctalia-shell) (Quickshell-based) |
| **Terminal** | kitty |
| **Shell** | fish |
| **Browser** | Firefox |
| **File manager** | Nautilus |
| **System info** | fastfetch |

Tested on a modest laptop (i3-6006U, 8 GB RAM), so it runs fine on low-end hardware.

---

## 🌫️ Blur and translucency

niri 26.04 has **native background blur**, so no forks or patches are needed.
The magic lives in [`niri/.config/niri/rules.kdl`](niri/.config/niri/rules.kdl):

```kdl
blur {
    passes 6
    offset 4.0
    noise 0.03
    saturation 1.2
}

window-rule {
    geometry-corner-radius 20
    clip-to-geometry true
    draw-border-with-background false   // fixes the "solid focused window" problem
}

window-rule {
    opacity 0.9
    background-effect {
        blur true
        xray true
    }
}
```

### Tips if it doesn't look right

- **Focused window looks solid and dull?** Add `draw-border-with-background false`. The focus ring was being drawn behind the translucent window.
- **Firefox looks opaque?** Set `widget.wayland.opaque-region.enabled` to `false` in `about:config`, then restart Firefox.
- **Rule not matching?** Check the real app-id with `niri msg windows`.
- **Blur invisible?** Blur only shows on translucent windows, so set `opacity` below 1.0 and use a colorful wallpaper.
- Rules lower in the file override earlier ones, so keep exceptions (like `mpv`) at the bottom.

---

## 📦 Installation

> ⚠️ These are my personal configs. **Back up your own first** and read the files before copying.

### 1. Install the essentials

```bash
sudo pacman -S niri kitty fish firefox nautilus fastfetch git
# Noctalia: follow the official install guide
# https://github.com/noctalia-dev/noctalia-shell
```

### 2. Clone the repo

```bash
git clone https://github.com/Adarsh496/niri-noctalia-dots.git ~/niri-noctalia-dots
cd ~/niri-noctalia-dots
```

### 3. Back up your current configs

```bash
mkdir -p ~/config-backup
cp -r ~/.config/niri ~/.config/kitty ~/config-backup/ 2>/dev/null
```

### 4. Copy the configs

```bash
cp -r niri/.config/niri ~/.config/
cp -r kitty/.config/kitty ~/.config/
cp -r fish/.config/fish ~/.config/
cp -r fastfetch/.config/fastfetch ~/.config/
cp -r noctalia/.config/noctalia ~/.config/
```

### 5. Validate and reload

```bash
niri validate
```

Log out and back in, or let niri hot-reload the config.

---

## 🗂️ Repo structure

```
niri-noctalia-dots/
├── niri/          # config.kdl + rules.kdl (blur, opacity, window rules)
├── kitty/         # terminal config
├── fish/          # shell config
├── fastfetch/     # system info layout
├── noctalia/      # shell settings
├── wallpapers/    # backgrounds I use
└── screenshots/   # previews for this README
```

---

## ⌨️ Keybinds (highlights)


| Keys | Action |
|---|---|
| `Mod + Enter` | Open terminal |
| `Mod + Q` | Close window |
| `Mod + O` | Overview |
| `Mod + Ctrl + Q` | Lock screen |

---

## 🖼️ Wallpapers

Wallpapers are in [`wallpapers/`](wallpapers/). Noctalia generates its color scheme from the wallpaper, so changing it re-themes the whole desktop.

---

## 🙏 Credits

- [niri](https://github.com/niri-wm/niri) by YaLTeR and contributors
- [Noctalia](https://github.com/noctalia-dev/noctalia-shell)
- The r/unixporn and r/niri communities for endless inspiration

---

<div align="center">

If you like this setup, drop a ⭐ and feel free to open an issue or PR.

</div>
