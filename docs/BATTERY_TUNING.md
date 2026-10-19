# Battery profile tuning — practical quick guide

The point of Battery Mode is **not** to create a second maximum-overclock profile. The biggest opportunity is usually the opposite: keep Battery Mode inside the stock frequency range, then tune only the voltage headroom required for those lower clocks.

A normal maximum-performance OC profile is often built around the highest CPU/RAM clocks the console can stably reach. That can require substantially more VDD2/VDDQ and CPU voltage headroom than stock-frequency gaming needs. Performance Modes lets you keep that high-performance setup untouched while building a second, efficiency-focused profile.

> [!WARNING]
> There is no universal safe minimum voltage or universal UV level. Every CPU, GPU and RAM setup is different. A setting that works on one Switch can crash or corrupt data on another. Change one area at a time, test it, and keep a known-good profile / Safety Backup.

## Recommended Battery target

For a true efficiency profile, start by keeping the intended Battery operating range close to Nintendo stock handheld clocks.

For validation, use **Temporary Overrides** only for the component currently being tested:

| Component | Battery validation target |
| --- | ---: |
| CPU | **1785 MHz** stock boost step |
| GPU | **384 MHz** for strict Nintendo stock handheld; optionally **460.8 MHz** if you deliberately want to validate the classic handheld maximum clock step |
| RAM | **1600 MHz** stock boost-memory step |

**768 MHz is the official docked GPU clock, not the normal stock handheld Battery target.** Horizon OC / uncapped profiles can request 768 MHz or more in handheld on supported Mariko setups, but that is no longer the stock-frequency Battery profile described by this guide.

CPU and RAM are different: Nintendo's boost behavior can use the **1785 MHz CPU** and **1600 MHz RAM** steps, so an efficiency profile that should remain reliable during stock boost/load behavior still needs to be stable there.

If Horizon OC only allows `CPU Max Clock` / `CPU Boost Clock` down to about **1963 MHz** on Mariko, that is not a problem by itself. Those values are ceilings in the HOC configuration; the actual requested CPU clock can still be lower.

For the finished Battery profile, also consider:

- `uncapped_clocks = 0` if you do not need OC-only clock steps.
- Stock/default per-title app clocks using `Setup -> Reset Battery App Profiles -> STOCK`.
- A conservative RAM maximum if Battery Mode is not intended to use RAM OC.
- Only tune GPU voltage points up to the highest handheld GPU clock you actually intend Battery Mode to use.

## Suggested tuning order

The exact historical order in which the development console's VDD2 and VDDQ were first discovered is not preserved well enough to document confidently. The procedure below is therefore the **recommended reproducible order** for new users: isolate one area, find its edge, add stability margin, then move to the next area.

### 1. Start from a known-good baseline

Before reducing anything:

1. Create/confirm a working **Performance Mode**.
2. Create the Battery profile slot.
3. If Battery should have no per-game OC profiles, use `Reset Battery App Profiles -> STOCK` while Performance is the confirmed current mode.
4. Switch to Battery Mode.
5. Start with voltages / UV values that are already known stable.
6. Use Temporary Overrides only for the part being tested: CPU **1785**, RAM **1600**, and GPU **384 MHz** for strict stock handheld (or **460.8 MHz** if you intentionally want that additional handheld clock step validated).

Do not lower VDD2, VDDQ, CPU High UV and GPU voltage all at the same time. If a test fails you need to know which change caused it.

---

## 2. Tune RAM VDD2 first

Keep **VDDQ at a known-safe value** while finding VDD2.

1. Set RAM to **1600 MHz** with Temporary Overrides.
2. Leave CPU/GPU at known-stable settings.
3. Lower **VDD2** by one available step.
4. Reboot if Horizon OC requires it for that setting to become active.
5. Run **Benchmark Toolbox -> RAM -> Memtester**.
6. A quick pass can be used while walking toward the edge, but once a candidate looks good, let Memtester run for about **30 minutes**.
7. If Memtester reports an error/mismatch, the console freezes, or CFW crashes/reboots, the setting is too low.
8. Return to the previous stable VDD2 step.

Do not treat "it booted" as proof of RAM stability. Memtester is the important part here.

### Development-console reference

The final Battery profile stored:

- **VDD2: 912.5 mV** (`common_emc_mem_volt=912500`)

The Performance profile used **1087.5 mV**. These are example results from one OLED/Mariko console, not recommended universal values.

---

## 3. Tune VDDQ second

Once VDD2 has a stable value, leave it fixed and tune **VDDQ** independently.

1. Keep RAM at **1600 MHz**.
2. Keep the stable VDD2 value from the previous step.
3. Lower VDDQ by one available step.
4. Run Memtester again.
5. Use the same method: short screening while approaching the edge, then about **30 minutes** on a promising candidate.
6. At the first error / mismatch / crash, return to the previous stable step.

### Development-console reference

The final Battery profile stored:

- **VDDQ: 400 mV** (`mariko_emc_vddq_volt=400000`)

The Performance profile used **600 mV**.

After both RAM voltages have been tuned separately, run **Memtester for at least another 30–60 minutes with both final values active together**. The combined setting matters more than either value in isolation.

---

## 4. Tune CPU High UV at the Battery CPU ceiling

CPU High UV should be treated as a **profile-specific stability setting**. A Performance profile that must support very high CPU clocks can need more voltage than a Battery profile that only needs stock boost.

For Battery Mode:

1. Set the CPU Temporary Override to **1785 MHz**.
2. Keep RAM at the already validated stock Battery setting.
3. Start from a known-stable CPU High UV level.
4. Increase **CPU High UV** one step at a time (a higher UV setting means a more aggressive undervolt).
5. Reboot when required so the KIP setting is actually active.
6. Run **Benchmark Toolbox -> CPU Stress -> Matrixprod**.
7. Use short passes while approaching the limit, then run a candidate for about **30 minutes**.
8. Any mismatch, freeze, application crash or CFW reboot means the undervolt is too aggressive. Step back.

### Important telemetry warning

Do not assume two High UV levels are equivalent just because the overlay displays the same rounded CPU voltage. During development, **High UV 12 at stock CPU Boost 1785 MHz displayed about 745 mV but failed the Matrixprod/CPU stress test**. High UV 11 showed the same displayed voltage, which demonstrates why the overlay number alone is not a stability test.

The correct goal is therefore not "reach a particular mV number". The goal is **the most aggressive High UV level that remains stable at the Battery profile's maximum intended CPU clock**.

---

## 5. GPU: find the minimum stable voltage for the handheld clock steps you use

For an efficiency profile there is little reason to tune GPU voltage points above the maximum GPU frequency Battery Mode will actually request.

For a strict stock handheld profile, focus on **307.2 and 384 MHz**. If you intentionally allow the classic **460.8 MHz handheld maximum step**, validate that as well. **768 MHz belongs to docked / charging use and is not required for a stock handheld Battery profile.**

The development console used:

- **Mariko GPU VMIN: 500 mV**

Then each required GPU clock point was validated with **Benchmark Toolbox -> GPU Stress**. The stress tool explicitly reports **Mismatches**; anything above zero indicates instability.

A practical procedure is:

1. Select one GPU clock with Temporary Overrides.
2. Run GPU Stress / FurMark at that clock.
3. Lower that clock point's voltage one available step at a time.
4. If Mismatches appear, graphics crash, or CFW becomes unstable, go back to the previous stable voltage.
5. Validate the final candidate for about **30 minutes**.
6. Repeat only for the GPU clock points Battery Mode actually needs.

### Development-console GPU table

The following table is included only as a **reference from the development OLED/Mariko console**. It is not a universal safe table.

| GPU clock | Development-console voltage |
| ---: | ---: |
| 76.8 MHz | 500 mV |
| 153.6 MHz | 500 mV |
| 230.4 MHz | 500 mV |
| 307.2 MHz | 500 mV |
| 384.0 MHz | 500 mV |
| 460.8 MHz | 500 mV |
| 537.6 MHz | 500 mV |
| 614.4 MHz | 525 mV |
| 691.2 MHz | 540 mV |
| 768.0 MHz | 570 mV |

Only the lower portion is relevant to a strict stock handheld Battery profile. The higher entries are shown because they were present in the development configuration and may be useful to people who intentionally build a less restrictive Battery profile.

---

## 6. Final combined validation

Passing the individual tests is only the first stage. Once VDD2, VDDQ, CPU High UV and the required GPU clock points are individually stable, test them together.

For a stock-oriented handheld Battery profile, validate the relevant worst cases separately rather than forcing an artificial CPU+GPU+RAM combination that stock handheld mode would never normally use:

- CPU **1785 MHz** + RAM **1600 MHz** for stock boost-path stability.
- GPU **384 MHz** for strict stock handheld graphics, or **460.8 MHz** if you intentionally allow that handheld clock step.

Then run, separately:

1. **CPU Matrixprod — about 30 min**
2. **RAM Memtester — at least 30 min; 60 min is better for the final RAM combination**
3. **GPU Stress / FurMark — about 30 min at the highest Battery GPU point you actually use**
4. Several real games for longer sessions, especially titles that heavily load CPU/RAM/GPU in different ways.

A 30-minute synthetic test is a useful screening test, not absolute proof of long-term stability. If a setting sits right on the edge, real games, shader compilation, loading transitions, sleep/wake or different temperatures can still expose it later. Keep one step of margin if you want a profile that is dependable rather than just benchmark-stable.

---

## Development-console result

The project was developed on a Mariko/OLED system with these RAM-voltage profile values:

| Setting | Performance profile | Battery profile |
| --- | ---: | ---: |
| VDD2 | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 400 mV |

With **Red Dead Redemption using the same stock game clocks/settings**, measured runtime was:

- Performance voltage profile: **5 h 32 min**
- Battery voltage profile: **6 h 05 min**

That is **+33 minutes / +9.9% runtime**, equivalent to roughly **9.0% lower average whole-device power draw** for that specific test.

This result is an example, not a guarantee. Battery condition, screen brightness, silicon quality, RAM, game load, temperatures and your own voltage margins all matter.

## App profiles

Horizon OC stores per-title CPU/GPU/RAM profiles inside the same `config.ini` that Performance Modes saves. Therefore game profiles are automatically switched together with Battery/Performance Mode.

If Battery Mode should use stock/default per-game clocks, run:

`Setup -> Reset Battery App Profiles -> STOCK`

This removes the stored per-title clock override keys from Battery Mode while keeping its global Horizon OC settings, including the Battery voltage configuration.

## Reboot behavior

Every Battery/Performance mode change ends with a CFW reboot **on purpose**. The active `hoc.kip` is replaced during the switch, and the reboot is necessary for that KIP profile to be loaded for the next boot.
