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
Tools

**Contact info**  
Enter your preferred e-mail address or Discord handle.

**Version**  
1.0

**License**  
MIT

**App URL**  
https://github.com/retrotendo/Ultrahand-Performance-Modes

**Short description**  
Ultrahand profile switcher for Horizon OC with separate OC and battery-focused undervolting modes.

**Detailed description**  
Performance Modes is an Ultrahand package for Horizon OC that switches between two complete setups: OC Mode for your normal overclock/performance profile and Battery Mode for a stock-clock undervolting profile focused on battery life.

It saves and restores the complete Horizon OC config.ini and hoc.kip for each mode, including per-game Horizon clock profiles. Optional ReverseNX-RT settings are switched with the selected mode as well. The outgoing profile is saved automatically before the other profile is loaded, then CFW reboots automatically so the selected hoc.kip becomes active.

Battery Mode is intended for users who already have a stable OC profile and want a separate efficiency profile using stock handheld clocks. The package does not ship fixed OC/UV values; each console must be stability-tested individually.

Requires Ultrahand Overlay and Horizon OC. ReverseNX-RT is optional.

**Changelog**  
Initial release:
- Battery Mode ↔ OC Mode profile switching
- Full Horizon OC config.ini + hoc.kip stored per mode
- Automatic saving of the outgoing profile
- Automatic CFW reboot after changing modes
- Per-game Horizon clock profiles switch with each mode
- Optional ReverseNX-RT folder save/restore
- Reset Battery app profiles to stock/default clocks
- Safety Backup / Restore
- Protection against overwriting profiles when current state is unknown

**Banner image**  
`assets/performance-modes-banner.jpg`

**Icon**  
`assets/performance-modes-icon.png`

**Screenshot**  
`assets/performance-modes-screenshot.jpg`

## Release

**GitHub release**  
https://github.com/retrotendo/Ultrahand-Performance-Modes/releases/tag/v1.0

**Install ZIP**  
https://github.com/retrotendo/Ultrahand-Performance-Modes/releases/download/v1.0/Performance-Modes-v1.0.zip

**SHA256**  
`c850e8f444845df8d1f68d898dbb58800e61357f6a733869cc371e420528adb5`

## Notes for the reviewer

Performance Modes is an **Ultrahand package**, not a standalone `.nro` application. The SD-root install ZIP places the package under:

```text
/switch/.packages/Performance Modes/
```

Required existing software:
- Ultrahand Overlay
- Horizon OC

ReverseNX-RT support is optional.

The project does not ship fixed overclock/undervolt values. Users create and stability-test their own OC Mode and Battery Mode settings.

The package uses the visible state values directly:
- `Battery Mode`
- `OC Mode`

Profile storage folders are `Battery/` and `OCMode/`.

## Final checklist

- Public GitHub repository: ready
- MIT license: ready
- README: ready
- Setup guide: ready
- Battery tuning guide: ready
- GitHub v1.0 release: ready
- Installable SD-root ZIP: ready
- Release SHA256 verified: ready
- Banner: ready
- Icon: ready
- Screenshot: ready
- Changelog: ready
- Contact field: enter preferred e-mail or Discord handle before submitting
