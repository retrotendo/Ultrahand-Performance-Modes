# Optional note to the Homebrew App Store maintainers

**Subject:** Performance Modes — new Switch homebrew submission

Hi 4TU / Homebrew App Store team,

I'd like to submit **Performance Modes**, an open-source Ultrahand package for Nintendo Switch.

It is designed for Horizon OC users who want to keep two separate complete setups: a normal Performance profile and a Battery profile. The package switches the full Horizon OC configuration and `hoc.kip`, including per-game Horizon clock profiles, and automatically saves the profile being left before loading the other one.

The Battery profile is intended to make it practical to run stock handheld clocks with separately tuned VDD2, VDDQ and CPU High UV settings for better efficiency. The project does not ship fixed OC/UV values; users must create and stability-test their own settings.

This is **not a standalone `.nro`**. It is an Ultrahand package installed under:

`/switch/.packages/Performance Modes/`

Requirements are Ultrahand Overlay and Horizon OC. ReverseNX-RT integration is optional.

Repository, source, installation ZIP, documentation, license and artwork are available here:

https://github.com/retrotendo/Ultrahand-Performance-Modes

Thanks for reviewing the submission.

Best regards,  
retrotendo
