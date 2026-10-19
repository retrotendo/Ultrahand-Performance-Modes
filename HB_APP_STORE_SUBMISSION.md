# Homebrew App Store submission — ready-to-paste fields

Use the official submission form: https://submit.fortheusers.org/

## Fields

**Console**  
Switch

**App title**  
Performance Modes

**Author**  
retrotendo

**Category**  
Tools / Utilities (choose the closest available category)

**Contact info**  
Enter your own e-mail address or Discord handle. This is the only intentionally personal field not filled in here.

**Version**  
1.0

**License**  
MIT

**App URL**  
https://github.com/retrotendo/Ultrahand-Performance-Modes

**Short description**  
Create and switch separate Battery and Performance profiles for Horizon OC directly from Ultrahand.

**Detailed description**  
Performance Modes is an Ultrahand package for Horizon OC. It is useful if you want one profile tuned for maximum overclocking performance and a second profile tuned for battery life.

A normal overclock profile is often configured around the highest stable CPU/RAM clocks. That can require higher VDD2/VDDQ and more CPU voltage headroom than a game running at stock clocks actually needs. With Performance Modes you can keep those high-performance settings in **Performance Mode**, while creating a separate **Battery Mode** for lower or stock frequencies.

For a Battery profile, the main idea is simple: use stock or otherwise conservative clocks, then lower **VDD2** and **VDDQ** and increase **CPU High UV** only as far as your own console remains fully stable. This is where the largest efficiency gains can come from. Do not copy somebody else's voltage limits blindly; every CPU and RAM setup is different and must be stability-tested.

The package stores the complete Horizon OC `config.ini` and `hoc.kip` for both modes. That means Horizon's global settings and **all per-game app profiles** are switched together with the mode. New title-ID profiles are included automatically because the full config file is saved. A menu function can reset the stored Battery app profiles back to stock/default clocks by removing their per-title CPU/GPU/RAM overrides.

If ReverseNX-RT is installed, its per-title `.dat` settings are silently saved and restored with each mode as well.

When changing mode, the current mode is automatically saved first, the target profile is restored, and the Switch performs a **CFW reboot**. The reboot is intentional and required so the selected `hoc.kip` / Horizon OC profile is actually loaded for the new boot.

### Example from the development console

Red Dead Redemption was tested with the **same stock game clocks/settings** using two different Horizon OC voltage profiles:

- Performance profile: **VDD2 1087.5 mV, VDDQ 600 mV**
- Battery profile: **VDD2 about 912.5 mV, VDDQ 400 mV**
- CPU High UV in Battery Mode was tuned separately for the stock-frequency operating point; users should find their own lowest stable setting instead of copying a fixed number.

Measured runtime:

- Performance profile: **5 h 32 min**
- Battery profile: **6 h 05 min**

That is **33 minutes longer**, about **+9.9% runtime**, which corresponds to roughly **9.0% lower average whole-device power draw** for the same usable battery energy in that test.

This result is only an example from one console and one workload. Actual savings depend on silicon quality, RAM, battery condition, brightness, game workload and the settings used.

### Main functions in simple terms

- **Battery Mode** — saves the current Performance setup, loads the Battery setup and reboots CFW.
- **Performance Mode** — saves the current Battery setup, loads the Performance setup and reboots CFW.
- **Save Settings -> as Battery Mode / as Performance Mode** — manually stores the current Horizon OC config, `hoc.kip` and optional ReverseNX-RT app settings into that slot.
- **Reset Battery App Profiles -> STOCK** — removes stored per-game CPU/GPU/RAM clock overrides from Battery Mode while keeping Battery's global Horizon OC settings.
- **Mark Current Boot** — tells the package which profile was actually loaded for the current boot. If the state is unknown, automatic switching will not overwrite either saved profile.
- **Create / Restore Safety Backup** — keeps one manual recovery snapshot of the active setup plus both saved modes.

Performance Modes does not provide or validate overclock/undervolt values. Users must stability-test their own settings.

**Changelog**  
Version 1.0 initial release:\n- Battery / Performance mode switching\n- Full Horizon OC config + hoc.kip profiles\n- Automatic outgoing-profile save\n- Per-title Horizon app profiles included automatically\n- Optional ReverseNX-RT per-title settings integration\n- Battery app-profile reset to stock/default clocks\n- Manual Safety Backup / Restore\n- Unknown/UNSET state protection

**Banner image**  
`assets/hbas-banner.png`

**Icon**  
`assets/icon.png`

## Submission checklist

- Repository is public.
- Source/config package is included under `package/`.
- Installable SD-root ZIP is included under `dist/`.
- MIT license is included.
- README contains requirements, setup, normal usage, safety behavior and tuning background.
- Banner and icon are included under `assets/`.
