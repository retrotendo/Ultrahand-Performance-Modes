# Performance Modes v1.0

Initial public release.

## Install
Extract `Performance-Modes-v1.0.zip` to the root of the SD card.

## Highlights
- Battery / Performance mode switching for Horizon OC
- Full Horizon OC `config.ini` and `hoc.kip` profiles
- Automatic outgoing-profile save before switching
- Full ReverseNX-RT folder saved/restored with each mode when present
- Manual Save Settings checkpoints for Battery and Performance
- Battery app-profile reset to stock/default clocks
- Safety Backup / Restore including active, Battery and Performance ReverseNX-RT snapshots
- Unknown-state overwrite protection
- Structured Ultrahand menu with Change Profile, Save Settings, Initial Setup and Backup Files sections
- `Check Files` gives a clear `All 4 core profile files: OK` confirmation when both Battery and Performance config/KIP files are present

## Why two profiles?
A Performance profile can retain the voltage and memory headroom required for high clocks, while a Battery profile can be tuned only for the lower/stock clocks actually used there. On the development OLED, Red Dead Redemption at identical stock game clocks improved from 5 h 32 min to 6 h 05 min (+33 min / ~9.9% runtime) with the tuned Battery profile. Both runs used 50% display brightness and 0% volume. Results vary by hardware and settings.

SHA256: `6dc4df2a35f1f6f52a2a8a0b5fa7181721a8622ea26447c0c046a3cdb8286e6e`
