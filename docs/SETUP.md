# Setup and Usage Guide

This document covers the initial Performance Modes setup and normal use. Detailed undervolting is intentionally kept in the [Battery Profile – Simple Step-by-Step Undervolting Guide](BATTERY_TUNING.md).

## Before you start

Performance Modes assumes that you already have a **known-good, stability-tested OC profile** for your console. It is a profile switcher, not an automatic OC tuner.

Start from the OC configuration you already know is stable.

## Menu layout

```text
Main
  Current Profile

  Change Profile
    Battery Mode
    OC Mode

  Save Settings
    as Battery Mode
    as OC Mode

Setup
  Initial Setup
    Reset Battery App Profiles -> STOCK
    Mark Current Boot -> Battery Mode
    Mark Current Boot -> OC Mode
    Check Files

  Backup Files
    Create Safety Backup
    Restore Safety Backup
```

## First-time setup

1. Boot your known-good OC configuration.
2. Open **Setup** and choose `Mark Current Boot -> OC Mode`.
3. On **Main**, choose `Save Settings -> as OC Mode`.
4. Open **Setup -> Backup Files** and choose `Create Safety Backup`.
5. On **Main**, choose `Save Settings -> as Battery Mode`. This creates a temporary Battery Mode copy from the known-good OC profile.
6. Choose `Battery Mode`. Performance Modes saves OC Mode, loads Battery Mode and **automatically reboots CFW**.
7. Tune Battery Mode by following the [Battery Profile – Simple Step-by-Step Undervolting Guide](BATTERY_TUNING.md).
8. When Battery Mode is stable, choose `Save Settings -> as Battery Mode`.
9. Choose `OC Mode`. Performance Modes restores OC Mode and **automatically reboots CFW**.
10. If you want Battery Mode to use stock/default per-game clocks, run `Setup -> Reset Battery App Profiles -> STOCK` while **OC Mode is active**.
11. Run `Setup -> Check Files`. When all four required files are present, it reports `All 4 files: OK`.
12. Once both modes are final and known-good, optionally run `Create Safety Backup` again to replace the initial backup with a complete backup of both finished modes.

## Everyday workflow

Normal use is simple:

- Choose **Battery Mode** to save the current OC Mode files, restore Battery Mode, and automatically reboot CFW.
- Choose **OC Mode** to save the current Battery Mode files, restore OC Mode, and automatically reboot CFW.

You normally do not need to manually save before switching. The mode you are leaving is saved automatically.

The manual **Save Settings** entries are mainly useful during initial setup or when you intentionally want to overwrite one stored profile without switching.

## If Current Profile is unknown

Do not switch modes until you know which profile was actually booted.

Choose the matching `Mark Current Boot` entry first. The switch commands deliberately refuse to overwrite a stored mode unless the internal state is exactly:

- `Battery Mode`
- `OC Mode`

Battery Mode files are stored under `Battery/`; OC Mode files are stored under `OCMode/`.

## Recovery

If an undervolt prevents normal CFW from booting and your Hekate setup provides a **`CFW no OC`** / safe boot entry:

1. Boot that no-OC/safe CFW entry.
2. Correct the unstable Horizon OC / HOC Toolkit value.
3. Save the KIP.
4. Reboot normally.

Performance Modes does not create or modify the Hekate no-OC entry.
