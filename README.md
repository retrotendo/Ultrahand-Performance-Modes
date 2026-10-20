<p align="center">
  <img src="https://raw.githubusercontent.com/retrotendo/Ultrahand-Performance-Modes/main/assets/hbas-banner.jpg" alt="Performance Modes banner" width="100%">
</p>

# Performance Modes

**Performance Modes** is an Ultrahand package for Nintendo Switch that switches between a complete **Performance** setup and a separate **Battery** setup for [Horizon OC](https://github.com/Horizon-OC/Horizon-OC).

The intended concept is simple: keep your normal high-clock OC setup in **Performance Mode**, and use **Battery Mode as a stock-clock undervolting / efficiency profile**. The package stores the whole Horizon OC configuration together with the active `hoc.kip`. Per-title Horizon clock profiles are included automatically. If ReverseNX-RT is installed, its complete `ReverseNX-RT` settings folder is stored and restored with the mode as well.

<p align="center">
  <img src="https://raw.githubusercontent.com/retrotendo/Ultrahand-Performance-Modes/main/assets/screenshot-main.jpg" alt="Performance Modes running in Ultrahand" width="100%">
</p>

## Why Performance + Battery profiles?

A normal performance-oriented OC setup is often tuned around the **highest CPU/RAM clocks the console can stably reach**. Reaching those clocks can require more VDD2/VDDQ and CPU voltage headroom than Nintendo stock-frequency gaming actually needs.

Battery Mode is therefore not intended as a second maximum-OC profile. It is a **stock-clock undervolting profile**: keep Nintendo stock handheld operating points, then tune the voltage headroom only as low as your own console remains stable.

- **Performance Mode** keeps the voltage, memory and clock headroom needed for higher CPU/GPU/RAM clocks.
- **Battery Mode** uses stock handheld clocks and can be tuned specifically for efficiency and battery life.

On Mariko/OLED systems, the most useful Battery-profile tuning controls can include **VDD2**, **VDDQ**, **CPU High UV** and the GPU voltage points required by stock handheld clocks. Every chip and RAM setup is different, so stability testing is essential.

See the [Battery tuning guide](docs/BATTERY_TUNING.md) for a practical walkthrough.

### Example battery-life result

In the development OLED, Red Dead Redemption was tested at the **same stock game clocks/settings** with the two different Horizon OC voltage profiles:

| Setting | Performance profile | Battery profile |
| --- | ---: | ---: |
| VDD2 | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 400 mV |
| Runtime | 5 h 32 min | 6 h 05 min |

That is **33 minutes longer**, or about **+9.9% runtime**. For the same usable battery energy, that corresponds to roughly **9.0% lower average whole-device power draw** during that test.

CPU High UV can also be tuned more aggressively in Battery Mode when it only needs to remain stable at the stock CPU operating point. No fixed High UV number is published here because that limit is silicon-specific and must be stability-tested on each console.

This is only one console and one workload, not a guaranteed result. The actual benefit depends on silicon quality, RAM, voltages, game workload, display brightness, battery condition and the settings used in both profiles.

## Features

- One-action **Battery Mode ↔ Performance Mode** switching with an intentional CFW reboot.
- Automatically saves the mode you are leaving before loading the other one.
- Stores the complete `/config/horizon-oc/config.ini` per mode.
- Stores `/atmosphere/kips/hoc.kip` per mode.
- Automatically includes all current and future Horizon OC title-ID app profiles because the full config file is saved.
- Optional **ReverseNX-RT** settings are silently saved/restored by copying the complete `/SaltySD/plugins/ReverseNX-RT` folder with each mode.
- **Reset Battery App Profiles -> STOCK** removes standard per-title CPU/GPU/RAM overrides from the stored Battery config while preserving Horizon OC's global `[values]` settings.
- Manual **Safety Backup / Restore**.
- Safety state: if the package cannot confirm whether Battery or Performance is active, it does **not** overwrite either stored profile.

The reboot after changing mode is intentional and required: the active `hoc.kip` is replaced during the switch, and CFW must restart so that the selected KIP/profile is actually loaded.

## Requirements

- Nintendo Switch running Atmosphère/CFW.
- [Ultrahand Overlay](https://github.com/ppkantorski/Ultrahand-Overlay) — current release recommended.
- [Horizon OC](https://github.com/Horizon-OC/Horizon-OC).
- Optional: [ReverseNX-RT](https://github.com/masagrator/ReverseNX-RT) with SaltyNX.

> [!WARNING]
> Performance Modes does not validate overclock or undervolt values. Horizon OC settings can cause instability and, if misused, may risk data corruption. Use settings that are stable on your own console and keep appropriate backups.

## Installation

1. Download `Performance-Modes-v1.0.zip` from the `dist` folder or from the GitHub `v1.0` release.
2. Extract it to the **root of the SD card**.
3. Confirm this path exists:
   ```text
   /switch/.packages/Performance Modes/package.ini
   ```
4. Reboot/open Ultrahand and go to **Packages -> Performance Modes**.

The package does not ship personal Horizon OC settings, `hoc.kip` profiles or backups. Those are created on your console.

## First-time setup

The safest setup is to create both profile slots first, switch into the temporary Battery slot, prepare the stock-clock Battery baseline, tune it, then return to Performance.

### If Performance is currently booted

1. Open **Setup** and choose **Mark Current Boot -> Performance**.
2. On **Main**, choose **Save Settings -> as Performance Mode**.
3. Still without changing anything, choose **Save Settings -> as Battery Mode**. This creates a temporary Battery clone so the first switch is safe.
4. Choose **Battery Mode**. The console saves Performance, loads the temporary Battery clone and reboots.
5. Prepare the Battery baseline:
   - In **Horizon OC**, turn **Uncapped Clocks OFF**.
   - Set **RAM Max Clock = 1600 MHz**.
   - Keep GPU behavior at stock handheld clocks; **384 MHz** is the highest relevant stock handheld GPU point.
   - Do not keep per-game CPU/GPU/RAM OC overrides in Battery Mode if the goal is a true stock-clock efficiency profile.
   - In **HOC Toolkit**, set **CPU Max Clock = 1785 MHz** and **CPU Boost Clock = 1785 MHz**.
6. Horizon OC itself may not offer 1785 MHz in those two maximum-clock selectors. Set both values in **HOC Toolkit**, save/apply the HOC configuration, and reboot CFW so the updated `hoc.kip` is loaded. After reboot, Horizon OC should reflect those 1785 MHz limits.
7. Tune **VDD2**, **VDDQ**, **CPU High UV** and the required stock GPU voltage points one area at a time. See the [Battery tuning guide](docs/BATTERY_TUNING.md).
8. After the Battery settings are stable, use **Save Settings -> as Battery Mode** as a checkpoint.
9. Choose **Performance Mode**. Performance is restored and CFW reboots.
10. If you want Battery games to use stock/default app clocks, open **Setup -> Reset Battery App Profiles -> STOCK** while Performance is active.
11. Open **Setup -> Check Files**. All four core profile files should report `OK`.
12. Optionally choose **Create Safety Backup** once both modes are known-good.

### If Battery is currently booted

Use the same procedure in reverse: mark Battery, save Battery, create a temporary Performance clone, switch to Performance, configure/save it, then return to Battery as needed.

For a shorter operational version, see [Setup and Usage Guide](docs/SETUP.md).

## Normal use

After setup, normal operation is intentionally simple:

- **Battery Mode**: saves the current Performance files and ReverseNX-RT folder, restores Battery files and ReverseNX-RT folder, sets the state to Battery and reboots.
- **Performance Mode**: does the reverse.

You normally do **not** need to manually save after changing Horizon OC settings. The outgoing mode is automatically saved when you switch modes.

The manual **Save Settings** entries are useful during initial setup or when you intentionally want to overwrite one stored mode without switching.

## Horizon app profiles

Horizon OC stores its per-game CPU/GPU/RAM profiles inside the same `config.ini` that Performance Modes saves. This means those app profiles automatically change together with Battery/Performance Mode.

If you want the Battery profile to use stock/default game clocks, choose:

`Setup -> Reset Battery App Profiles -> STOCK`

That removes the standard per-title clock override keys from the stored Battery profile while keeping Battery's global Horizon OC `[values]` settings, including its voltage configuration.

## What is saved per mode?

```text
Battery/
├── config.ini          # full Horizon OC config, including title-ID app profiles
├── hoc.kip             # Horizon OC KIP configuration
└── ReverseNX-RT/       # optional complete ReverseNX-RT settings folder

Performance/
├── config.ini
├── hoc.kip
└── ReverseNX-RT/
```

The active source files are:

```text
/config/horizon-oc/config.ini
/atmosphere/kips/hoc.kip
/SaltySD/plugins/ReverseNX-RT/        # optional
```

Performance Modes copies the complete ReverseNX-RT settings folder; it does not replace the ReverseNX-RT application itself.

## Safety behavior

The package state is stored locally as either `BATTERY`, `PERFORMANCE` or `UNSET`.

- An automatic profile save only occurs when the current state is an exact confirmed match.
- `UNSET`, a missing value, or an unexpected value never overwrites Battery or Performance during a mode switch.
- `Mark Current Boot` only changes this local state marker. Use it only when you know which profile was actually loaded for the current boot.
- A separate Hekate safe/no-OC boot entry is not modified by this project.

## Safety Backup

**Create Safety Backup** stores the current active Horizon config/KIP, both stored modes, the complete optional ReverseNX-RT snapshots, and the package state under the package's `Backup/` directory.

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
