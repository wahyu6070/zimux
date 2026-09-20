# zimux

**A Linux terminal for Android — full Ubuntu via proot, no root required.**

zimux is a modern terminal emulator for Android, built with Kotlin, Jetpack Compose
and Material 3. It runs a real PTY, so ordinary Linux programs — `vim`, `htop`, `top`,
`apt`, shell job control — behave the way they do on a desktop. Around the terminal
sits a small suite of tools (file manager, code editor, browser, viewers) reachable
from the in-app switcher.

[![Latest release](https://img.shields.io/github/v/release/wahyu6070/zimux?label=download)](https://github.com/wahyu6070/zimux/releases/latest)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

---

## Download

There are two channels.

**Stable** — the [latest release](https://github.com/wahyu6070/zimux/releases/latest).
This is the one to use.

**Development** — the rolling [`dev` prerelease](https://github.com/wahyu6070/zimux/releases/tag/dev),
rebuilt from the current source. Useful for trying a fix before it ships, at the
price of being untested. The URL never changes, so you can bookmark it:

```
https://github.com/wahyu6070/zimux/releases/download/dev/zimux-dev.apk
```

A single APK covers `arm64-v8a`, `armeabi-v7a`, `x86` and `x86_64`. Android 8.0
(API 26) or newer.

> **The two channels are signed with different keys**, so Android will not install
> one over the other — switching between them means uninstalling first, which
> deletes the app's data including any installed Ubuntu rootfs. Pick a channel and
> stay on it. Within a channel, updates install over the previous build normally.

---

## Features

### Terminal

- **Real PTY terminal emulator** with full escape-sequence support, so full-screen
  programs (`vim`, `htop`, `less`, `tmux`) render and respond correctly
- **Job control** — `Ctrl-Z`, `fg`, `bg` work as expected
- **Multiple tabs**, each running its own independent session
- **Extra keys row**: `Esc`, `Ctrl`, `Alt`, `Tab`, arrows, `Home`, `End`, `PgUp`, `PgDn`
  — the keys a soft keyboard doesn't give you
- **Pinch to zoom** the font, copy & paste, and scrollback history
- Run a `.sh` file from another app directly in the terminal

### Three environments

| Environment | Root needed | What it is |
| --- | :---: | --- |
| **Zix Terminal** | no | The device's own shell, plus a bundled BusyBox toolbox on `PATH`. Instant, no download. Type `su` to elevate if your device is rooted. |
| **Ubuntu (proot)** | no | A complete Ubuntu 26.04 userland running under proot fake-root. `apt` works, and you are `root` inside the guest — without touching the device. Downloads ~80 MB on first use. |
| **Ubuntu (chroot)** | yes | A real `chroot` as actual root via `su`. Everything proot gives you, plus genuine access to `/data` and the rest of the system. |

Shared storage appears at `/sdcard` inside both Ubuntu environments, so your files are
reachable from the guest.

### Bundled command-line tools

zimux ships real native binaries, not just shell built-ins: **BusyBox**, **proot**,
**7-Zip** (`7zz`), **GNU tar**, **GNU cpio**, **xz**, **zstd** and **brotli** — all
available on `PATH` in the Zix Terminal.

### Tool suite

Reachable from the app switcher in the top bar:

- **File manager** — internal and removable storage, tabs, list/grid/gallery views,
  sorting, filtering and search. Copy, move, delete and rename run in the background
  with progress and notifications
- **Archives** — create ZIP / TAR / TAR.GZ, extract many formats, and browse archive
  contents without extracting first
- **Code editor** — syntax highlighting for many languages
- **Web browser**, **image viewer** (zoom & pan), **PDF viewer**, **HTML viewer**
- **APK installer** and a **task manager** for background operations
- Optional **root access** to browse the whole filesystem

### Appearance

Material 3 with dynamic color (Material You) on Android 12+, light and dark themes
that follow the system, and English + Indonesian locales.

---

## Getting started

### 1. Pick an environment

On first launch zimux asks which environment you want. You can change it later in
**Settings → Terminal**, and switch from the terminal's ⋮ menu.

If you are not sure: choose **Ubuntu (proot)**. It needs no root and gives you a real
Ubuntu with working `apt`.

### 2. Install Ubuntu (proot or chroot only)

The first launch downloads the Ubuntu base image from Canonical and extracts it.
Expect ~80 MB of download and a few minutes of extraction. It happens once.

### 3. Use it

```bash
apt update && apt install -y git python3 nano
```

You are `root` inside the guest, so no `sudo` is needed.

Your device's shared storage is mounted at `/sdcard`:

```bash
cd /sdcard/Download
```

### Everyday keys

| Action | How |
| --- | --- |
| New tab | **+** in the tab bar |
| Close tab | **×** on the tab |
| Interrupt / EOF | `Ctrl` then `C` / `D` from the extra keys row |
| Suspend and resume | `Ctrl`+`Z`, then `fg` |
| Resize font | pinch on the terminal |
| Copy / paste | long-press the terminal |

---

## Requirements and notes

- **Android 8.0 (API 26) or newer.**
- **Storage permission.** The file manager asks for *All files access*
  (`MANAGE_EXTERNAL_STORAGE`) on Android 11+, which Android requires for a file
  manager to see the whole shared storage. The terminal itself works without it.
- **Root** is optional. Only the **Ubuntu (chroot)** environment requires it, and it
  works with Magisk, KernelSU, KernelSU Next and APatch. Everything else — including
  the full Ubuntu under proot — runs without root.
- **32-bit x86 devices** have no Ubuntu base image upstream, so the Ubuntu
  environments are unavailable there. The Zix Terminal still works.
- The Ubuntu rootfs lives in the app's private storage, so **uninstalling zimux
  deletes it.** Back up anything you care about to `/sdcard` first.

---

## Privacy

zimux has no analytics, no tracking and no account. The only network traffic it makes
on its own is downloading the Ubuntu base image from Canonical when you ask it to.
See [privacy.txt](privacy.txt) for the full policy.

## License

Released under the [MIT License](LICENSE).

zimux builds on excellent open-source work, in particular the
[Termux](https://github.com/termux/termux-app) terminal emulator and PTY (Apache-2.0),
[proot](https://github.com/termux/proot), [BusyBox](https://busybox.net/), and
[sora-editor](https://github.com/Rosemoe/sora-editor). Attribution for every bundled
native binary ships inside the app, under **Settings → About**.

---

## About this repository

This repository is the public home for zimux: **releases**, the license and the
privacy policy. The application source is developed in a separate private repository.

Found a bug or have a request? Open an [issue](https://github.com/wahyu6070/zimux/issues).
