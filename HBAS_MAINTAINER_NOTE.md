# Optional note to the Homebrew App Store maintainers

**Subject:** Performance Modes — new Switch homebrew submission

Hi 4TU / Homebrew App Store team,

I'd like to submit **Performance Modes**, an open-source Ultrahand package for Nintendo Switch and Horizon OC.

It switches between two complete Horizon OC setups: **OC Mode**, which keeps the voltage and memory headroom needed for higher clocks, and a separate **stock-clock undervolting / efficiency profile** called Battery Mode.

The package switches the full Horizon OC configuration and `hoc.kip`, including per-game Horizon clock profiles, and automatically saves the profile being left before loading the other one. Battery per-game clock overrides can also be reset to stock/default from the package menu.

On the development OLED, Red Dead Redemption at the same stock game clocks/settings, 50% display brightness and 0% volume ran **4:56 on a stock no-OC/no-UV profile**, **5:32 on the OC Mode voltage profile**, and **6:05 on the tuned Battery Mode profile**. This is only an example; the project does not ship fixed OC/UV values and users must stability-test their own settings.

This is **not a standalone `.nro`**. It is an Ultrahand package installed under:

`/switch/.packages/Performance Modes/`

Requirements are Ultrahand Overlay and Horizon OC. ReverseNX-RT integration is optional.

OC Mode files are stored under `OCMode/`, and the active state marker is `OC Mode`. Older `PERFORMANCE` state values are migrated automatically when the package boots.

Repository, source, installation ZIP, documentation, license and artwork are available here:

https://github.com/retrotendo/Ultrahand-Performance-Modes

Thanks for reviewing the submission.

Best regards,  
retrotendo
