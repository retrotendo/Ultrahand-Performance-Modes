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
- `Check Files` gives a clear `All 4 files: OK` confirmation when both Battery Mode and OC Mode config/KIP files are present
- OC Mode profile files are stored under `OCMode/` for clearer on-disk naming
- OC Mode uses `OC Mode` as the package state marker; older `PERFORMANCE` values are migrated automatically at package boot
- Recovery guidance for overly aggressive UV settings using a Hekate `CFW no OC` / safe entry when available

## Battery-life example
On the development OLED, Red Dead Redemption used the same stock game clocks/settings, **50% display brightness** and **0% volume**:

| Setting | Stock — no OC/UV profile | OC Mode profile | Battery Mode profile |
| --- | ---: | ---: | ---: |
| VDD2 | 1175 mV | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 600 mV | 400 mV |
| Runtime | 4 h 56 min | 5 h 32 min | 6 h 05 min |

Battery Mode vs OC Mode: **+33 min / +9.9% runtime**, about **9.0% lower average whole-device power draw**.

Battery Mode vs stock: **+69 min / +23.3% runtime**, about **18.9% lower average whole-device power draw**.

Results vary by hardware and settings.

The active state values are `BATTERY` and `OC Mode`, and OC Mode files are stored under `OCMode/`.

SHA256: `da0cbdb2af2a1ceedba3572a9f132162b25753aa56b50cdc4e1ca18cae09f956`
