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

## Recommended first setup from OC Mode

1. `Mark Current Boot -> OC Mode`
2. `Save Settings -> as OC Mode`
3. `Save Settings -> as Battery Mode` (temporary clone)
4. Choose `Battery Mode` and allow the reboot.
5. While Battery is now the confirmed current profile, prepare the Battery baseline before doing any undervolt tuning:
   - In **Horizon OC**, turn **Uncapped Clocks OFF** for a stock-oriented Battery profile.
   - Set **RAM Max Clock to 1600 MHz** if the Battery profile is intended to stay within stock RAM clocks.
   - Do not add per-game CPU/GPU/RAM OC overrides for Battery Mode. These can be cleared later with `Reset Battery App Profiles -> STOCK`.
   - In **HOC Toolkit**, set **CPU Max Clock = 1785 MHz** and **CPU Boost Clock = 1785 MHz**.
6. Horizon OC itself may not offer **1785 MHz** in the Max Clock / Max Boost selectors. Set those two limits in **HOC Toolkit** instead. HOC writes the change to `hoc.kip`; reboot CFW so the new KIP is actually loaded. After that reboot, Horizon OC should reflect the 1785 MHz limits.
7. Keep GPU behavior stock for the Battery profile. For stock handheld validation, the highest relevant GPU point is **384 MHz**; no GPU overclock is needed for this profile.
8. Once the stock-frequency limits are in place, tune **VDD2**, **VDDQ** and **CPU High UV** one area at a time. Use the [Battery tuning guide](BATTERY_TUNING.md) for the stress-test order and stability checks.
9. After the Battery settings are stable, use `Save Settings -> as Battery Mode` as an explicit first-setup checkpoint.
10. Choose `OC Mode` and allow the reboot. The OC profile is restored.
11. If you want Battery games to use stock/default app clocks, run `Setup -> Reset Battery App Profiles -> STOCK` while OC Mode is active.
12. Run `Setup -> Check Files`. All four core profile files should report `OK`.
13. Optional: `Create Safety Backup` once both profiles are known-good.

## Recommended Battery baseline

For the stock-oriented Battery concept used by this project, the intended starting point is:

| Setting | Battery target |
| --- | ---: |
| CPU Max Clock | **1785 MHz** via HOC Toolkit |
| CPU Boost Clock | **1785 MHz** via HOC Toolkit |
| RAM Max Clock | **1600 MHz** |
| GPU | **stock handheld behavior, up to 384 MHz** |
| Uncapped Clocks | **OFF** |
| Per-game Horizon clock overrides | **stock/default** |

These are frequency limits / behavior targets, not universal voltage values. VDD2, VDDQ and CPU High UV must be tuned and stability-tested on the individual console.

## Everyday workflow

Change Horizon OC, per-game clocks, KIP settings or ReverseNX-RT settings as desired in the current mode. When you switch modes, the current mode is saved automatically before the target mode is restored.

You normally do not need to press a manual Save entry before every profile switch. The manual save entries are mainly useful for first setup or when you deliberately want to overwrite one stored profile without switching.

## If Current Profile is unknown

Do not use a mode switch until you know what was actually booted. Choose the matching `Mark Current Boot` entry first. The switch commands deliberately refuse to overwrite a stored mode unless the internal state is exactly `BATTERY` or `PERFORMANCE`.

`PERFORMANCE` is the internal compatibility state used for the visible **OC Mode**. The internal profile folder also remains `Performance/` so existing setups continue to work.
