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
Switch between complete Horizon OC Battery and Performance profiles directly from Ultrahand.

**Detailed description**  
Performance Modes is an Ultrahand package for Horizon OC that lets you keep two complete setups: Performance and Battery.

Performance Mode can keep your normal high-clock OC settings. Battery Mode is intended for stock handheld clocks, where VDD2, VDDQ and CPU High UV can be tuned for lower power use. On the development OLED, Red Dead Redemption runtime increased from 5:32 to 6:05 at the same stock game clocks (+9.9%).

The package switches the full Horizon OC config, hoc.kip and all per-game Horizon clock profiles. Battery app profiles can be reset to stock/default clocks from the menu. ReverseNX-RT per-title settings are also handled when installed.

When changing mode, the current profile is saved, the other profile is loaded and CFW reboots. This reboot is intentional and required to load the selected hoc.kip.

Requires Ultrahand and Horizon OC. Voltage/UV settings are console-specific and must be stability-tested by the user.

**Changelog**  
Initial release:
- Battery / Performance profile switching
- Full Horizon OC config + hoc.kip saved per mode
- Automatic save of the profile being left
- Per-game Horizon clock profiles switch with each mode
- Reset Battery app profiles to stock/default clocks
- Optional ReverseNX-RT per-title profile handling
- Manual Safety Backup / Restore
- Protection against overwriting profiles when current state is unknown

**Banner image**  
`assets/hbas-banner.jpg`

**Icon**  
`assets/icon.png`

## Notes for the reviewer

Performance Modes is an **Ultrahand package**, not a standalone `.nro` application. The install ZIP places the package under:

```text
/switch/.packages/Performance Modes/
```

Required existing software:

- Ultrahand Overlay
- Horizon OC

ReverseNX-RT support is optional.

The project does not ship personal overclock/undervolt profiles. Users create and stability-test their own Battery and Performance settings.

## Final checklist before submitting

- Public GitHub repository: ready
- MIT license: ready
- README and setup guide: ready
- Battery tuning guide: ready
- Installable SD-root ZIP: ready
- Banner: ready
- Icon: ready
- Changelog: ready
- Contact field: user must enter e-mail or Discord handle
- GitHub release: recommended before submission so future releases can be detected automatically by HBAS
