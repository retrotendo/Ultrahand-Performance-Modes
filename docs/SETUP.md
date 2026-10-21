# Setup and Usage Guide

This document is a shorter operational reference. For background and safety details, see the main README.

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
    Mark Current Boot -> Battery
    Mark Current Boot -> OC Mode
    Check Files

  Backup Files
    Create Safety Backup
    Restore Safety Backup
```

## Recommended first setup

Start by booting the normal OC configuration that you want to keep as **OC Mode**. Save OC Mode first, then create Battery Mode from it.

1. `Mark Current Boot -> OC Mode`
2. `Save Settings -> as OC Mode`
3. `Save Settings -> as Battery Mode` to create a temporary Battery clone.
4. Choose `Battery Mode` and allow the reboot.
5. Prepare the Battery baseline:
   - In **Horizon OC**, turn **Uncapped Clocks OFF**.
   - Set **RAM Max Clock = 1600 MHz**.
   - Keep GPU behavior at stock handheld clocks; **384 MHz** is the highest relevant stock handheld GPU point.
   - Do not keep per-game CPU/GPU/RAM OC overrides in Battery Mode if the goal is a true stock-clock efficiency profile.
   - In **HOC Toolkit**, set **CPU Max Clock = 1785 MHz** and **CPU Boost Clock = 1785 MHz**.
6. Horizon OC itself may not offer **1785 MHz** in the Max Clock / Max Boost selectors. Set those two limits in **HOC Toolkit**, save/apply the HOC configuration, then reboot CFW so the new `hoc.kip` is active.
7. Tune **VDD2**, **VDDQ**, **CPU High UV** and the required stock GPU voltage points one area at a time. Use the [Battery tuning guide](BATTERY_TUNING.md) for the stress-test order and stability checks.
8. After the Battery settings are stable, use `Save Settings -> as Battery Mode` as an explicit checkpoint.
9. Choose `OC Mode` and allow the reboot. The OC profile is restored.
10. If you want Battery games to use stock/default app clocks, run `Setup -> Reset Battery App Profiles -> STOCK` while **OC Mode is active**.
11. Run `Setup -> Check Files`. When all four core files are present, it reports `All 4 files: OK`.
12. Optional: `Create Safety Backup` once both profiles are known-good.

## Recommended Battery baseline

| Setting | Battery target |
| --- | ---: |
| CPU Max Clock | **1785 MHz** via HOC Toolkit |
| CPU Boost Clock | **1785 MHz** via HOC Toolkit |
| RAM Max Clock | **1600 MHz** |
| GPU | **stock handheld behavior, up to 384 MHz** |
| Uncapped Clocks | **OFF** |
| Per-game Horizon clock overrides | **stock/default** |

These are frequency limits / behavior targets, not universal voltage values. VDD2, VDDQ and CPU High UV must be tuned and stability-tested on the individual console.

## If an undervolt prevents normal CFW from booting

If your Hekate setup provides a **`CFW no OC`** or equivalent safe boot entry:

1. Boot that no-OC/safe CFW entry from Hekate.
2. Correct the too-low voltage / too-aggressive UV value in Horizon OC or HOC Toolkit.
3. Save/apply the corrected configuration.
4. Reboot into normal CFW and test again.

Performance Modes does not create or modify the Hekate no-OC entry.

## Everyday workflow

Change Horizon OC, per-game clocks, KIP settings or ReverseNX-RT settings as desired in the current mode. When you switch modes, the current mode is saved automatically before the target mode is restored.

You normally do not need to press a manual Save entry before every profile switch. The manual save entries are mainly useful for first setup or when you deliberately want to overwrite one stored profile without switching.

## If Current Profile is unknown

Do not use a mode switch until you know what was actually booted. Choose the matching `Mark Current Boot` entry first. The switch commands deliberately refuse to overwrite a stored mode unless the internal state is exactly `BATTERY` or `OC Mode`.

Older `PERFORMANCE` state values are migrated automatically to `OC Mode` when the package boots. OC Mode files are stored under `OCMode/`.
