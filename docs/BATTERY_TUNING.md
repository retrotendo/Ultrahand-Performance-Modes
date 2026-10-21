# Battery profile tuning — practical quick guide

The point of Battery Mode is **not** to create a second maximum-overclock profile. The biggest opportunity is usually the opposite: keep Battery Mode inside the stock frequency range, then tune only the voltage headroom required for those lower clocks.

A normal maximum-performance OC profile is often built around the highest CPU/RAM clocks the console can stably reach. That can require substantially more VDD2/VDDQ and CPU voltage headroom than stock-frequency gaming needs. Performance Modes lets you keep that high-performance setup untouched in **OC Mode** while building a second, efficiency-focused Battery profile.

> [!WARNING]
> There is no universal safe minimum voltage or universal UV level. Every CPU, GPU and RAM setup is different. A setting that works on one Switch can crash or corrupt data on another. Change one area at a time, test it, and keep a known-good profile / Safety Backup.

## Recommended Battery target

For a true efficiency profile, keep the Battery operating range at Nintendo stock handheld clocks.

For validation, use **Temporary Overrides** only for the component currently being tested:

| Component | Battery validation target |
| --- | ---: |
| CPU | **1785 MHz** stock boost step |
| GPU | **384 MHz** stock handheld maximum |
| RAM | **1600 MHz** stock boost-memory step |

CPU and RAM boost behavior can still reach **1785 MHz CPU** and **1600 MHz RAM**, so an efficiency profile that should remain reliable during normal boost/load behavior must be stable there.

### Important: setting the CPU maximum to stock boost

In Horizon OC itself, `CPU Max Clock` and `CPU Boost Clock` cannot currently be lowered all the way to **1785 MHz** through the normal Horizon settings screen.

Set both values to **1785 MHz in HOC Toolkit instead**. Apply/save the HOC configuration there (HOC Toolkit writes the active `hoc.kip`), then reboot CFW. After the reboot, Horizon OC uses the values from that KIP and the 1785 MHz limits are reflected in the active configuration.

For the finished Battery profile, also consider:

- `uncapped_clocks = 0` if you do not need OC-only clock steps.
- Stock/default per-title app clocks using `Setup -> Reset Battery App Profiles -> STOCK`.
- Keep RAM at stock speed if Battery Mode is intended purely for efficiency.
- Tune only the GPU voltage points used by stock handheld clocks.

## Suggested tuning order

The procedure below is a reproducible way to tune one area at a time: isolate one voltage domain, find its stability edge, add margin, then move to the next area.

### 1. Start from a known-good baseline

Before reducing anything:

1. Create/confirm a working **OC Mode**.
2. Create the Battery profile slot.
3. If Battery should have no per-game OC profiles, use `Reset Battery App Profiles -> STOCK` while **OC Mode** is the confirmed current mode.
4. Switch to Battery Mode.
5. Start with voltages / UV values that are already known stable.
6. Use Temporary Overrides only for the part being tested: CPU **1785**, RAM **1600**, or GPU **384 MHz**.

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

The **OC Mode profile** used **1087.5 mV**. These are example results from one OLED/Mariko console, not recommended universal values.

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

The **OC Mode profile** used **600 mV**.

After both RAM voltages have been tuned separately, run **Memtester for at least another 30–60 minutes with both final values active together**. The combined setting matters more than either value in isolation.

---

## 4. Tune CPU High UV at stock boost

CPU High UV should be treated as a **profile-specific stability setting**. An **OC Mode** profile that must support very high CPU clocks can need more voltage than a Battery profile that only needs stock boost.

For Battery Mode:

1. Make sure CPU Max Clock / CPU Boost Clock have been set to **1785 MHz through HOC Toolkit** and rebooted once so the KIP is active.
2. Set the CPU Temporary Override to **1785 MHz**.
3. Keep RAM at the already validated stock Battery setting.
4. Start from a known-stable CPU High UV level.
5. Increase **CPU High UV** one step at a time (a higher UV setting means a more aggressive undervolt).
6. Reboot when required so the KIP setting is actually active.
7. Run **Benchmark Toolbox -> CPU Stress -> Matrixprod**.
8. Use short passes while approaching the limit, then run a candidate for about **30 minutes**.
9. Any mismatch, freeze, application crash or CFW reboot means the undervolt is too aggressive. Step back.

### Important telemetry warning

Do not assume two High UV levels are equivalent just because the overlay displays the same rounded CPU voltage. During development, **High UV 12 at stock CPU Boost 1785 MHz displayed about 745 mV but failed the Matrixprod/CPU stress test**. High UV 11 showed the same displayed voltage, which demonstrates why the overlay number alone is not a stability test.

The correct goal is therefore not "reach a particular mV number". The goal is **the most aggressive High UV level that remains stable at 1785 MHz**.

---

## 5. GPU: find the minimum stable voltage for stock handheld clocks

For the Battery profile, only the stock handheld GPU range needs to be tuned.

The development console used:

- **Mariko GPU VMIN: 500 mV**

Validate the required GPU clock points with **Benchmark Toolbox -> GPU Stress**. The stress tool reports **Mismatches**; anything above zero indicates instability.

A practical procedure is:

1. Select one stock handheld GPU clock with Temporary Overrides.
2. Run GPU Stress / FurMark at that clock.
3. Lower that clock point's voltage one available step at a time.
4. If Mismatches appear, graphics crash, or CFW becomes unstable, go back to the previous stable voltage.
5. Validate the final candidate for about **30 minutes**.
6. Repeat for the other stock handheld GPU clock points you use.

### Development-console GPU reference

The following values are only a **reference from the development OLED/Mariko console**. They are not universal safe values.

| GPU clock | Development-console voltage |
| ---: | ---: |
| 76.8 MHz | 500 mV |
| 153.6 MHz | 500 mV |
| 230.4 MHz | 500 mV |
| 307.2 MHz | 500 mV |
| 384.0 MHz | 500 mV |

---

## 6. Final combined validation

Passing the individual tests is only the first stage. Once VDD2, VDDQ, CPU High UV and the stock handheld GPU points are individually stable, validate the finished Battery profile.

Use the relevant stock limits:

- CPU **1785 MHz**
- RAM **1600 MHz**
- GPU **384 MHz**

Then run, separately:

1. **CPU Matrixprod — about 30 min**
2. **RAM Memtester — at least 30 min; 60 min is better for the final RAM combination**
3. **GPU Stress / FurMark — about 30 min at 384 MHz**
4. Several real games for longer sessions, especially titles that heavily load CPU/RAM/GPU in different ways.

A 30-minute synthetic test is a useful screening test, not absolute proof of long-term stability. If a setting sits right on the edge, real games, shader compilation, loading transitions, sleep/wake or different temperatures can still expose it later. Keep one step of margin if you want a profile that is dependable rather than just benchmark-stable.

---

## Development-console result

The project was developed on a Mariko/OLED system with these RAM-voltage profile values:

| Setting | OC Mode profile | Battery Mode profile |
| --- | ---: | ---: |
| VDD2 | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 400 mV |

With **Red Dead Redemption using the same stock game clocks/settings**, measured runtime was:

- OC Mode voltage profile: **5 h 32 min**
- Battery Mode voltage profile: **6 h 05 min**

Both runs used **50% display brightness** and **0% volume**.

That is **+33 minutes / +9.9% runtime**, equivalent to roughly **9.0% lower average whole-device power draw** for that specific test.

This result is an example, not a guarantee. Battery condition, screen brightness, silicon quality, RAM, game load, temperatures and your own voltage margins all matter.

## App profiles

Horizon OC stores per-title CPU/GPU/RAM profiles inside the same `config.ini` that Performance Modes saves. Therefore game profiles are automatically switched together with **Battery Mode / OC Mode**.

If Battery Mode should use stock/default per-game clocks, run:

`Setup -> Reset Battery App Profiles -> STOCK`

This action only runs while **OC Mode is active**. If Battery Mode is active, nothing is changed and the package tells you to switch to OC Mode first.

## Reboot behavior

Every **Battery Mode / OC Mode** change ends with a CFW reboot **on purpose**. The active `hoc.kip` is replaced during the switch, and the reboot is necessary for that KIP profile to be loaded for the next boot.

## Internal compatibility names

The visible profile is called **OC Mode**, while the internal state remains `PERFORMANCE` and its storage folder remains `Performance/`. These internal names are intentionally retained so existing profiles remain compatible.
