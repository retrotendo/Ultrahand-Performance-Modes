# Homebrew App Store submission — ready to paste

Official form: https://submit.fortheusers.org/

The current form asks for console, app title, author, category, contact info, version, license, app URL, short description, detailed description, changelog, banner and icon.

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

This can reduce power consumption without reducing game performance below stock clocks. On the development OLED, Red Dead Redemption runtime increased from 5:32 to 6:05 using the same stock game clocks (+9.9%). Both runs used 50% display brightness and 0% volume.

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

For compatibility with existing test builds, the visible **OC Mode** still uses the internal state value `PERFORMANCE` and the internal folder `Performance/`.

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
