# Battery profile tuning — simple guide

The point of Battery Mode is **not** to create a second maximum-overclock profile. It is most useful when the Battery profile is intentionally limited to stock or otherwise conservative clocks.

## Basic idea

A high-performance OC profile is usually tuned so that the console can remain stable at high CPU/RAM clocks. That can require voltage and memory settings that are unnecessary when you are only running stock clocks.

For Battery Mode:

1. Use stock or conservative CPU/GPU/RAM clocks.
2. Keep `uncapped_clocks` disabled if you do not need OC clock steps in Battery Mode.
3. Set RAM maximums conservatively (for example stock RAM operation if that is your goal).
4. Reduce **VDD2** and **VDDQ** gradually until you find the lowest values that remain fully stable at those clocks.
5. Increase **CPU High UV** only as far as the intended Battery CPU clocks remain fully stable.
6. Stress-test CPU and RAM after every meaningful change.
7. When stable, switch back to Performance Mode; Performance Modes automatically saves the outgoing Battery configuration.

There is no universal safe minimum. Silicon quality and RAM behavior vary from console to console.

## Development-console example

The project was developed on a Mariko/OLED system with these RAM-voltage profile values:

| Setting | Performance profile | Battery profile |
| --- | ---: | ---: |
| VDD2 | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 400 mV |

CPU High UV was also treated as a **per-profile stability setting**: the Battery profile can use a more aggressive UV level when it only needs to remain stable at stock/lower CPU frequencies. Do not copy a fixed High UV number from another console; find the highest UV level that passes your own stress testing.

With Red Dead Redemption using the same stock game clocks/settings, the development console measured:

- Performance voltage profile: **5 h 32 min**
- Battery voltage profile: **6 h 05 min**

That is **+33 minutes / +9.9% runtime**, equivalent to roughly **9.0% lower average whole-device power draw** for that specific test.

## App profiles

Horizon OC stores per-title CPU/GPU/RAM profiles inside the same `config.ini` that Performance Modes saves. Therefore game profiles are automatically switched with Battery/Performance Mode.

If Battery Mode should use stock/default per-game clocks, run:

`Setup -> Reset Battery App Profiles -> STOCK`

This removes the stored per-title clock override keys from Battery Mode while keeping its global Horizon OC settings (including the Battery voltage configuration).

## Reboot behavior

Every Battery/Performance mode change ends with a CFW reboot **on purpose**. The active `hoc.kip` is replaced during the switch, and the reboot is necessary for that KIP profile to be loaded for the next boot.
