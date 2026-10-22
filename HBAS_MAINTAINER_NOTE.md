# Optional note to the Homebrew App Store maintainers

**Subject:** Performance Modes — new Switch Homebrew App Store submission

Hi 4TU / Homebrew App Store team,

I'd like to submit **Performance Modes**, an open-source Ultrahand package for Nintendo Switch and Horizon OC.

Performance Modes switches between two complete Horizon OC setups:

- **OC Mode** for the user's normal overclock/performance configuration.
- **Battery Mode** for a separate stock-clock undervolting / efficiency configuration.

The package saves and restores the complete Horizon OC `config.ini` and `hoc.kip`, so per-game Horizon clock profiles switch together with the selected mode. Optional ReverseNX-RT settings are saved/restored as well. The outgoing profile is saved automatically, the target profile is loaded, and CFW is then rebooted automatically so the selected `hoc.kip` becomes active.

This is **not a standalone `.nro`**. It is an Ultrahand package installed from an SD-root ZIP to:

`/switch/.packages/Performance Modes/`

Required existing software:
- Ultrahand Overlay
- Horizon OC

ReverseNX-RT integration is optional.

The project does **not** ship fixed overclock or undervolt values. Users must create and stability-test values appropriate for their own console. The included documentation provides a separate Battery Mode tuning guide.

The package uses the visible state values `Battery Mode` and `OC Mode`. Profile files are stored under `Battery/` and `OCMode/`.

Repository:
https://github.com/retrotendo/Ultrahand-Performance-Modes

Release:
https://github.com/retrotendo/Ultrahand-Performance-Modes/releases/tag/v1.0

Install ZIP:
https://github.com/retrotendo/Ultrahand-Performance-Modes/releases/download/v1.0/Performance-Modes-v1.0.zip

SHA256:
`c850e8f444845df8d1f68d898dbb58800e61357f6a733869cc371e420528adb5`

Thanks for reviewing the submission.

Best regards,  
retrotendo
