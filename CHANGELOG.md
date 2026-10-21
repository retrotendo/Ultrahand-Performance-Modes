# Changelog

## 1.0

- Initial public release.
- Complete Battery Mode and OC Mode profile switching for Horizon OC.
- Full Horizon OC `config.ini` and `hoc.kip` save/restore.
- Automatic outgoing-mode save before switching.
- Full ReverseNX-RT folder saved/restored with each mode when installed.
- Manual `Save Settings -> as Battery Mode / as OC Mode` checkpoints also save ReverseNX-RT.
- Per-title Horizon clock profiles included automatically.
- Battery app-profile reset to stock/default clocks.
- Manual Safety Backup and Restore, including ReverseNX-RT snapshots for active/Battery/OC Mode states.
- Exact-state protection prevents automatic profile overwrite when state is unknown or unset.
- `Check Files` reports `All 4 core profile files: OK` when both profile configs and KIPs are present.
- OC Mode profile storage renamed to `OCMode/` for consistency with the visible menu name.
- Documentation includes a true stock no-OC/no-UV battery baseline plus OC Mode and Battery Mode results.
- Added Hekate `CFW no OC` / safe-boot recovery guidance for overly aggressive UV settings.
