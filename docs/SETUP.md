# Setup and Usage Guide

This document is a shorter operational reference. For background and safety details, see the main README.

## Menu layout

```text
Main
  Current Profile

  Change Profile
    Battery Mode
    Performance Mode

  Save Settings
    as Battery Mode
    as Performance Mode

Setup
  Initial Setup
    Reset Battery App Profiles -> STOCK
    Mark Current Boot -> Battery
    Mark Current Boot -> Performance
    Check Files

  Backup Files
    Create Safety Backup
    Restore Safety Backup
```

## Recommended first setup from Performance

1. `Mark Current Boot -> Performance`
2. `Save Settings -> as Performance Mode`
3. `Save Settings -> as Battery Mode` (temporary clone)
4. `Battery Mode` and allow the reboot
5. Configure Battery HOC/Horizon settings
6. `Performance Mode` and allow the reboot — Battery changes are auto-saved
7. Optional: `Reset Battery App Profiles -> STOCK`
8. `Check Files`
9. Optional: `Create Safety Backup`

## Everyday workflow

Change Horizon OC, per-game clocks, KIP settings or ReverseNX-RT settings as desired in the current mode. When you switch modes, the current mode is saved automatically before the target mode is restored.

## If Current Profile is unknown

Do not use a mode switch until you know what was actually booted. Choose the matching `Mark Current Boot` entry first. The switch commands deliberately refuse to overwrite a stored mode unless the state is exactly `BATTERY` or `PERFORMANCE`.
