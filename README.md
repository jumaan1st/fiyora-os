# Fiyora OS

> **Fiyora OS is a lightweight, open-source, installable Linux-based operating system whose sole purpose is to run one configurable web application.**

---

## Architecture Overview

```text
                               FIYORA OS
┌────────────────────────────────────────────────────────────────────────┐
│                              FIYORA SHELL                              │
│   ┌────────────────────────────────────────────────────────────────┐   │
│   │                      ONE WEB APPLICATION                       │   │
│   │                                                                │   │
│   │                  Chromium (Kiosk / Wayland)                    │   │
│   └────────────────────────────────────────────────────────────────┘   │
│   │ Minimal Status Bar / Nav Overlay / Protected Admin Panel (PIN) │   │
├────────────────────────────────────────────────────────────────────────┤
│                              FIYORA CORE                               │
│                                                                        │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────────┐  │
│  │  Config Manager  │  │   App Manager    │  │   Browser Manager    │  │
│  └──────────────────┘  └──────────────────┘  └──────────────────────┘  │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────────┐  │
│  │ Navigation Policy│  │ Security Manager │  │    Health Monitor    │  │
│  └──────────────────┘  └──────────────────┘  └──────────────────────┘  │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────────┐  │
│  │  Update Manager  │  │ Hardware Manager │  │   IPC/Event Broker   │  │
│  └──────────────────┘  └──────────────────┘  └──────────────────────┘  │
├────────────────────────────────────────────────────────────────────────┤
│                           LINUX USER SPACE                             │
│                                                                        │
│  systemd  │  NetworkManager  │  CUPS  │  BlueZ  │  PipeWire  │  udev  │  │
│  Cage (Wayland Kiosk Compositor)  │  Mesa / DRM / KMS  │  seatd        │
├────────────────────────────────────────────────────────────────────────┤
│                             LINUX KERNEL                               │
├────────────────────────────────────────────────────────────────────────┤
│                          HARDWARE (x86_64)                             │
└────────────────────────────────────────────────────────────────────────┘
```

---

## Directory Layout

```text
fiyora-os/
├── core/         # Core orchestrator, configuration, health & navigation engine
├── shell/        # Minimal UI, overlay bar, admin diagnostic screen
├── browser/      # Chromium launcher & CDP supervisor
├── hardware/     # Hardware abstraction layer (NetworkManager, CUPS, BlueZ, udev)
├── security/     # Admin authentication, PIN hashing & system lockdown
├── updater/      # A/B atomic image update engine
├── config/       # Schema and default configuration profiles
├── system/       # systemd units, Wayland compositor configs, udev rules
├── build/        # Reproducible Debian Live ISO build system
│   ├── live/     # live-build configuration files
│   ├── scripts/  # Automated build scripts
│   └── output/   # Generated bootable ISO images
├── installer/    # Bare-metal installation wizard
├── tests/        # Unit & integration test suites
└── docs/         # System architecture & documentation
```

---

## Foundation Targets

* **Base OS**: Debian 13 (Trixie)
* **Compositor**: Cage (Wayland Kiosk)
* **Browser Runtime**: Chromium (Kiosk mode)
* **Target Memory**: 2 GB RAM minimum (with zram enabled)
* **Build System**: Debian `live-build` (`Fiyora-OS-x86_64.iso`)

---

## License

Apache 2.0 / MIT
