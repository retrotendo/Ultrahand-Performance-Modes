<p align="center">
  <img src="assets/hbas-banner.png" alt="Performance Modes banner" width="100%">
</p>

# Performance Modes

**Performance Modes** is an Ultrahand package for Nintendo Switch that switches between complete **Battery** and **Performance** configurations for [Horizon OC](https://github.com/Horizon-OC/Horizon-OC).

Instead of changing a few clocks, it stores the whole Horizon OC configuration together with the active `hoc.kip`. Per-title Horizon clock profiles are included automatically. If ReverseNX-RT is installed, its per-title `.dat` settings are stored and restored with the mode as well.

## Features

- One-action **Battery Mode ↔ Performance Mode** switching with CFW reboot.
- Automatically saves the mode you are leaving before loading the other one.
- Stores the complete `/config/horizon-oc/config.ini` per mode.
- Stores `/atmosphere/kips/hoc.kip` per mode.
- Automatically includes all current and future Horizon OC title-ID app profiles because the full config file is saved.
- Optional **ReverseNX-RT** per-title state/resolution settings are silently saved with each mode.
- **Reset Battery App Profiles -> STOCK** removes standard per-title CPU/GPU/RAM overrides from the stored Battery config while preserving Horizon OC's global `[values]` settings.
- Manual **Safety Backup / Restore**.
- Safety state: if the package cannot confirm whether Battery or Performance is active, it does **not** overwrite either stored profile.

## Requirements

- Nintendo Switch running Atmosphère/CFW.
- [Ultrahand Overlay](https://github.com/ppkantorski/Ultrahand-Overlay) — current release recommended.
- [Horizon OC](https://github.com/Horizon-OC/Horizon-OC).
- Optional: [ReverseNX-RT](https://github.com/masagrator/ReverseNX-RT) with SaltyNX.

> [!WARNING]
> Performance Modes does not validate overclock, undervolt or memory-timing values. Horizon OC settings can cause instability and, if misused, may risk data corruption. Use settings that are stable on your own console and keep appropriate backups.

## Installation

1. Download `Performance-Modes-v1.0.zip` from the `dist` folder (or a GitHub release when available).
2. Extract it to the **root of the SD card**.
3. Confirm this path exists:
   ```text
   /switch/.packages/Performance Modes/package.ini
   ```
4. Reboot/open Ultrahand and go to **Packages -> Performance Modes**.

The package does not ship personal Horizon OC settings, `hoc.kip` profiles or backups. Those are created on your console.

## First-time setup

The safest setup is to create both profile slots first, switch into the temporary Battery slot, tune Battery while it is the confirmed current mode, then return to Performance.

### If Performance is currently booted

1. Open **Setup** and choose **Mark Current Boot -> Performance**.
2. On **Main**, choose **Save Settings -> as Performance Mode**.
3. Still without changing anything, choose **Save Settings -> as Battery Mode**. This creates a temporary Battery clone so the first switch is safe.
4. Choose **Battery Mode**. The console saves Performance, loads the temporary Battery clone and reboots.
5. Now configure your desired Battery Horizon OC/HOC settings while Battery is the confirmed current mode.
6. Choose **Performance Mode**. Your Battery settings are automatically saved, Performance is restored, and the console reboots.
7. If you want Battery games to use stock/default app clocks, open **Setup -> Reset Battery App Profiles -> STOCK** while Performance is active.
8. Open **Setup -> Check Files**. All four core profile files should report `OK`.
9. Optionally choose **Create Safety Backup** once both modes are known-good.

### If Battery is currently booted

Use the same procedure in reverse: mark Battery, save Battery, create a temporary Performance clone, switch to Performance, configure it, then switch back so the outgoing Performance settings are saved.

## Normal use

After setup, normal operation is intentionally simple:

- **Battery Mode**: saves the current Performance files, restores Battery files, restores optional ReverseNX-RT per-title settings, sets the state to Battery and reboots.
- **Performance Mode**: does the reverse.

You normally do **not** need to manually save after changing Horizon OC settings. The outgoing mode is automatically saved when you switch modes.

The manual **Save Settings** entries are useful when you intentionally want to overwrite one stored mode without switching.

## What is saved per mode?

```text
Battery/
├── config.ini          # full Horizon OC config, including title-ID app profiles
├── hoc.kip             # Horizon OC KIP configuration
└── ReverseNX-RT/       # optional per-title *.dat settings

Performance/
├── config.ini
├── hoc.kip
└── ReverseNX-RT/
```

The active source files are:

```text
/config/horizon-oc/config.ini
/atmosphere/kips/hoc.kip
/SaltySD/plugins/ReverseNX-RT/*.dat   # optional
```

ReverseNX-RT stores its per-title saves as `%TITLEID%.dat` files under `/SaltySD/plugins/ReverseNX-RT/`; Performance Modes only touches those `.dat` files and does not replace ReverseNX-RT itself.

## Battery app-profile reset

`Reset Battery App Profiles -> STOCK` is only allowed while **Performance Mode** is the confirmed active state. This prevents the package from editing the Battery profile while it is being used as the live source.

The reset removes the standard Horizon/sys-clk per-title keys (`handheld_*`, `docked_*`, charging variants) from all sections of the stored Battery config. Empty title-ID sections may remain; without clock keys they do not provide a custom clock override. Stored Battery ReverseNX-RT per-title settings are cleared as well.

## Safety behavior

The package state is stored locally as either `BATTERY`, `PERFORMANCE` or `UNSET`.

- An automatic profile save only occurs when the current state is an exact confirmed match.
- `UNSET`, a missing value, or an unexpected value never overwrites Battery or Performance during a mode switch.
- `Mark Current Boot` only changes this local state marker. Use it only when you know which profile was actually loaded for the current boot.
- A separate Hekate safe/no-OC boot entry is not modified by this project.

## Safety Backup

**Create Safety Backup** stores the current active Horizon config/KIP, both stored modes, optional ReverseNX-RT snapshots, and the package state under the package's `Backup/` directory.

**Restore Safety Backup** writes that snapshot back and reboots CFW.

The backup is replaced only when you explicitly run **Create Safety Backup**.

## Updating

Future updates should be extracted over the existing package folder unless release notes say otherwise. User-generated `Battery/`, `Performance/`, `Backup/` and `config.ini` files are not included in release ZIPs and therefore are not intentionally replaced by the project package.

## Credits

- [Ultrahand Overlay](https://github.com/ppkantorski/Ultrahand-Overlay) by ppkantorski and contributors.
- [Horizon OC](https://github.com/Horizon-OC/Horizon-OC) and its contributors.
- [ReverseNX-RT](https://github.com/masagrator/ReverseNX-RT) / SaltyNX by MasaGratoR and contributors.

Performance Modes is an independent community package and is not affiliated with Nintendo, the Ultrahand project, Horizon OC, or ReverseNX-RT.

## License

MIT. See [LICENSE](LICENSE).
