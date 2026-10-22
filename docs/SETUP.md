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
    Mark Current Boot -> Battery Mode
    Mark Current Boot -> OC Mode
    Check Files

  Backup Files
    Create Safety Backup
    Restore Safety Backup
```

## Before you start

Performance Modes assumes that you already have a **known-good, stability-tested OC profile** for your console. The package is a profile switcher, not an automatic OC tuner.

Your existing OC setup should already contain the CPU/GPU/RAM limits, voltage curves and other Horizon OC / HOC Toolkit values that you know are stable on your hardware. Save that setup as **OC Mode** first. Battery Mode is then derived from this known-good profile and simplified for stock handheld operation.

For Battery Mode, the main efficiency controls are usually:

- **RAM VDD2**
- **RAM VDDQ**
- **CPU Low UV** for normal stock-frequency handheld CPU operation

Other values can normally stay at the known-good settings inherited from OC Mode unless you have a specific reason to change them. If you keep a higher CPU boost limit such as 1785 MHz, the corresponding higher-frequency CPU UV settings still need to remain stable, but they do not need to be the main Battery Mode tuning target.

## Recommended first setup

Start by booting the normal OC configuration that you already know is stable and want to keep as **OC Mode**.

1. Boot your known-good OC configuration.
2. Open **Setup** and choose `Mark Current Boot -> OC Mode`.
3. On **Main**, choose `Save Settings -> as OC Mode`.
4. Open **Setup -> Backup Files** and choose `Create Safety Backup`. Do this **before creating or tuning Battery Mode** so you have a recovery snapshot of the known-good OC configuration, saved OC Mode files and package state.
5. Without changing anything yet, choose `Save Settings -> as Battery Mode`. This creates a safe temporary Battery clone from the known-good OC profile.
6. Choose `Battery Mode`. Performance Modes saves OC Mode, loads the temporary Battery clone and **automatically reboots CFW**.
7. Prepare a conservative Battery baseline before undervolting:
   - In **Horizon OC -> Safety Settings**, turn **Uncapped Clocks OFF**.
   - In **RAM Settings**, set **HP Mode OFF**.
   - Set **RAM Max Clock = 1600 MHz**.
   - Start **VDD2** and **VDDQ** from safe stock/default values for your setup before lowering them. On the development OLED, the stock baseline used for comparison was **VDD2 1175 mV / VDDQ 600 mV**.
   - Keep GPU behavior at stock handheld clocks. There is normally no need to retune the full GPU curve just to create Battery Mode if your existing curve is already known-good at those clocks.
   - Use stock/default per-game CPU/GPU/RAM clocks if the goal is a true stock-clock efficiency profile.
   - Keep the rest of the Horizon OC / HOC Toolkit configuration at known-good values inherited from OC Mode unless there is a specific reason to change it.
8. If desired, keep **CPU Max Clock = 1785 MHz** and **CPU Boost Clock = 1785 MHz** through HOC Toolkit. Those limits allow the normal boost step while stock game profiles remain at stock clocks. Save/apply the HOC configuration and reboot CFW if the KIP changes.
9. Tune the Battery-specific efficiency controls one at a time:
   - lower **VDD2** and stability-test it;
   - then lower **VDDQ** and stability-test the final VDD2/VDDQ pair;
   - then tune **CPU Low UV** for the stock-frequency CPU range.
10. After the Battery settings are stable, use `Save Settings -> as Battery Mode` as an explicit checkpoint.
11. Choose `OC Mode`. Performance Modes restores the OC profile and **automatically reboots CFW**.
12. If you want Battery games to use stock/default app clocks, run `Setup -> Reset Battery App Profiles -> STOCK` while **OC Mode is active**.
13. Run `Setup -> Check Files`. When all four core files are present, it reports `All 4 files: OK`.
14. Once both modes are fully tested and known-good, you can optionally run `Create Safety Backup` again to replace the initial OC-only safety snapshot with a complete backup of both finished modes.

## Recommended Battery baseline

| Setting | Starting target |
| --- | ---: |
| Uncapped Clocks | **OFF** |
| RAM HP Mode | **OFF** |
| RAM Max Clock | **1600 MHz** |
| VDD2 | **safe stock/default starting value** |
| VDDQ | **safe stock/default starting value** |
| CPU tuning focus | **Low UV at stock-frequency operation** |
| GPU | **stock handheld behavior** |
| Per-game Horizon clock overrides | **stock/default** |

Development-OLED stock comparison baseline: **VDD2 1175 mV / VDDQ 600 mV**. These are not universal minimums; they are conservative starting/reference values from the development console. Final stable values vary by hardware.

## If an undervolt prevents normal CFW from booting

If your Hekate setup provides a **`CFW no OC`** or equivalent safe boot entry:

1. Boot that no-OC/safe CFW entry from Hekate.
2. Correct the too-low voltage / too-aggressive UV value in Horizon OC or HOC Toolkit.
3. Save/apply the corrected configuration.
4. Reboot into normal CFW and test again.

Performance Modes does not create or modify the Hekate no-OC entry.

## Everyday workflow

Change Horizon OC, per-game clocks, KIP settings or ReverseNX-RT settings as desired in the current mode. When you switch modes, the current mode is saved automatically before the target mode is restored, and Performance Modes then automatically reboots CFW so the selected `hoc.kip` becomes active.

You normally do not need to press a manual Save entry before every profile switch. The manual save entries are mainly useful for first setup or when you deliberately want to overwrite one stored profile without switching.

## If Current Profile is unknown

Do not use a mode switch until you know what was actually booted. Choose the matching `Mark Current Boot` entry first. The switch commands deliberately refuse to overwrite a stored mode unless the internal state is exactly `Battery Mode` or `OC Mode`.

Battery Mode files are stored under `Battery/`; OC Mode files are stored under `OCMode/`.
