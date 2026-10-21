# Performance Modes v1.0

Initial public release.

## Install
Extract `Performance-Modes-v1.0.zip` to the root of the SD card.

## Highlights
- Battery Mode / OC Mode switching for Horizon OC
- Full Horizon OC `config.ini` and `hoc.kip` profiles
- Automatic outgoing-profile save before switching
- Full ReverseNX-RT folder saved/restored with each mode when present
- Manual Save Settings checkpoints for Battery Mode and OC Mode
- Battery app-profile reset to stock/default clocks
- Safety Backup / Restore including active, Battery Mode and OC Mode ReverseNX-RT snapshots
- Unknown-state overwrite protection
- Structured Ultrahand menu with Change Profile, Save Settings, Initial Setup and Backup Files sections
- `Check Files` gives a clear `All 4 core profile files: OK` confirmation when both Battery Mode and OC Mode config/KIP files are present

## Why two profiles?
OC Mode can retain the voltage and memory headroom required for high clocks, while Battery Mode can be tuned only for the lower/stock clocks actually used there. On the development OLED, Red Dead Redemption at identical stock game clocks improved from 5 h 32 min to 6 h 05 min (+33 min / ~9.9% runtime) with the tuned Battery profile. Both runs used 50% display brightness and 0% volume. Results vary by hardware and settings.

The visible profile name is **OC Mode**. For compatibility, its internal state remains `PERFORMANCE` and its internal storage folder remains `Performance/`.

SHA256: `a654d0c1b97c4959a37c71f1ffb994408546b3472cd231062b8648812b1dc3b6`
