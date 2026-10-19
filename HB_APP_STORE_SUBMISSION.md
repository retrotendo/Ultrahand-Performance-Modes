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
Switch complete Battery and Performance profiles for Horizon OC from Ultrahand.

**Detailed description**  
Performance Modes is an Ultrahand package for Horizon OC that lets users keep a high-performance overclock profile and a separate efficiency-focused Battery profile. A normal maximum-performance OC may require higher VDD2/VDDQ and CPU voltage headroom to remain stable at high CPU/RAM clocks; a Battery profile can instead be tuned only for the lower or stock frequencies actually used there. The package switches the full Horizon OC config.ini and hoc.kip, automatically saves the mode being left, and therefore preserves global Horizon settings plus all current and future per-title clock profiles. Optional ReverseNX-RT per-title settings are saved and restored silently when installed. It also includes a Battery app-profile reset, manual profile saves, unknown-state overwrite protection, and Safety Backup/Restore. In one development test using Red Dead Redemption at the same stock game clocks/settings, runtime increased from 5 h 32 min to 6 h 05 min (+33 min / about +9.9% runtime, equivalent to roughly 9.0% lower average whole-device draw). Results vary by console and settings. The package does not provide or validate overclock/undervolt values; users must stability-test their own settings.

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
