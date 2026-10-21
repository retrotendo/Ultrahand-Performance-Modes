# Homebrew App Store submission — ready to paste

Official form: https://submit.fortheusers.org/

## Form fields

**Console**  
Switch

**App title**  
Performance Modes

**Author**  
retrotendo

**Category**  
Utilities / Tools if available. Otherwise use Misc.

**Contact info**  
Enter your own e-mail address or Discord handle.

**Version**  
1.0

**License**  
MIT

**App URL**  
https://github.com/retrotendo/Ultrahand-Performance-Modes

**Short description**  
Switch between an OC Mode profile and a stock-clock undervolting Battery Mode profile from Ultrahand.

**Detailed description**  
Performance Modes is an Ultrahand package for Horizon OC that lets you keep two complete setups: **OC Mode** for your normal overclock/performance configuration and **Battery Mode** for a separate stock-clock undervolting profile focused on battery life.

OC Mode keeps the voltage, memory and clock headroom needed for higher overclocks. Battery Mode is designed around Nintendo stock handheld clocks, so VDD2, VDDQ, CPU High UV and the required GPU voltage points can be tuned specifically for those lower operating points.

On the development OLED, Red Dead Redemption at identical stock game clocks/settings, 50% display brightness and 0% volume ran **4:56 with a stock no-OC/no-UV profile**, **5:32 with the OC Mode voltage profile**, and **6:05 with the tuned Battery Mode profile**. Battery Mode was +23.3% runtime versus stock and +9.9% versus OC Mode. Results vary by console and settings.

The package switches the complete Horizon OC config and hoc.kip. All per-game Horizon clock profiles therefore switch with the mode as well. Battery app profiles can be reset to stock/default clocks from the menu, and the complete optional ReverseNX-RT settings folder is saved and restored with each mode when present.

When changing mode, the current profile is saved, the other profile is loaded and CFW reboots. This reboot is intentional and required to load the selected hoc.kip.

Requires Ultrahand and Horizon OC. Undervolting limits are console-specific and must be stability-tested by the user.

**Changelog**  
Initial release:
- Battery Mode / OC Mode profile switching
- Full Horizon OC config + hoc.kip saved per mode
- Automatic save of the profile being left
- Per-game Horizon clock profiles switch with each mode
- Reset Battery app profiles to stock/default clocks
- Optional ReverseNX-RT folder save/restore
- Manual Safety Backup / Restore
- Protection against overwriting profiles when current state is unknown

**Banner image**  
`assets/performance-modes-banner.jpg`

**Icon**  
`assets/performance-modes-icon.png`

**Screenshot**  
`assets/performance-modes-screenshot.jpg`

## Notes for the reviewer

Performance Modes is an **Ultrahand package**, not a standalone `.nro` application. The install ZIP places the package under:

```text
/switch/.packages/Performance Modes/
```

Required existing software:
- Ultrahand Overlay
- Horizon OC

ReverseNX-RT support is optional.

The project does not ship fixed overclock/undervolt values. Users create and stability-test their own OC Mode and Battery Mode settings.

OC Mode is stored under `OCMode/`, and its package state marker is `OC Mode`. Older `PERFORMANCE` state values are migrated automatically when the package boots.

## Final checklist before submitting

- Public GitHub repository: ready
- MIT license: ready
- README and setup guide: ready
- Battery tuning guide: ready
- Installable SD-root ZIP: ready
- Banner: ready
- Icon: ready
- Screenshot: ready
- Changelog: ready
- Contact field: user must enter e-mail or Discord handle
- GitHub release: recommended before submission so future releases can be detected automatically by HBAS
