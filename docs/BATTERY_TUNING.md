# Battery profile tuning — practical quick guide

Battery Mode is **not** a second maximum-overclock profile. The idea is to keep Battery Mode inside Nintendo's stock handheld frequency range and tune only the voltage headroom required for those lower clocks.

OC Mode can keep the voltage and memory headroom needed for your normal higher-clock setup while Battery Mode is tuned separately for efficiency.

> [!WARNING]
> There is no universal safe minimum voltage or universal UV level. Every CPU, GPU and RAM setup is different. Change one area at a time, test it, and keep a known-good OC Mode / Safety Backup.
>
> If an overly aggressive UV prevents normal CFW from booting, use your **Hekate `CFW no OC` / safe boot entry** if your setup provides one. Correct the value in Horizon OC or HOC Toolkit, save/apply it, then reboot normal CFW. Performance Modes does not create that Hekate entry.

## Recommended Battery target

| Component | Battery validation target |
| --- | ---: |
| CPU | **1785 MHz** stock boost step |
| GPU | **384 MHz** stock handheld maximum |
| RAM | **1600 MHz** stock boost-memory step |

For the finished Battery profile:

- `uncapped_clocks = 0` if you do not need OC-only clock steps.
- Use stock/default per-title app clocks if Battery Mode is intended to be a true stock-clock profile.
- Keep RAM at stock speed.
- Tune only the GPU voltage points used by stock handheld clocks.

### CPU maximum / boost

Horizon OC itself may not offer **1785 MHz** in the normal CPU Max Clock / CPU Boost Clock selectors. Set both values to **1785 MHz in HOC Toolkit**, save/apply the HOC configuration, then reboot CFW so the updated `hoc.kip` is actually loaded.

## Suggested tuning order

### 1. Start from a known-good baseline

1. Boot and save a working **OC Mode** first.
2. Create the Battery profile slot from that known-good setup.
3. Switch to Battery Mode.
4. Set the stock Battery frequency limits above.
5. Start from voltages / UV values already known to boot and run reliably.

Do not lower VDD2, VDDQ, CPU High UV and GPU voltage all at the same time. If a test fails, you need to know which change caused it.

### 2. Tune RAM VDD2 first

Keep **VDDQ at a known-safe value** while finding VDD2.

1. Set RAM to **1600 MHz** with Temporary Overrides.
2. Lower **VDD2** by one available step.
3. Reboot if required for the value to become active.
4. Run **Benchmark Toolbox -> RAM -> Memtester**.
5. Use short passes while approaching the edge, then run a promising candidate for about **30 minutes**.
6. At the first mismatch, freeze or crash, return to the previous stable step.

Development-console Battery value: **912.5 mV**.  
Development-console OC Mode value: **1087.5 mV**.

### 3. Tune VDDQ second

Keep the stable VDD2 value fixed and tune VDDQ independently.

1. Keep RAM at **1600 MHz**.
2. Lower VDDQ one available step at a time.
3. Run Memtester again.
4. At the first error / mismatch / crash, return to the previous stable step.
5. After both RAM voltages are chosen, run **30–60 minutes** of Memtester with the final pair active together.

Development-console Battery value: **400 mV**.  
Development-console OC Mode value: **600 mV**.

### 4. Tune CPU High UV at stock boost

1. Set CPU Max Clock / CPU Boost Clock to **1785 MHz through HOC Toolkit**.
2. Use a **1785 MHz** CPU Temporary Override.
3. Start from a known-stable High UV level.
4. Increase High UV one step at a time; a higher UV setting is a more aggressive undervolt.
5. Reboot when required.
6. Run **Benchmark Toolbox -> CPU Stress -> Matrixprod**.
7. Use short passes while approaching the limit, then about **30 minutes** on a final candidate.
8. Any mismatch, freeze, app crash or CFW reboot means the undervolt is too aggressive. Step back.

Do not rely only on the rounded voltage shown by an overlay. During development, a more aggressive High UV level could display the same approximate voltage while still failing Matrixprod.

### 5. Tune GPU only for stock handheld clocks

For Battery Mode, validate only the stock handheld GPU range you actually use. The highest relevant stock handheld point is **384 MHz**.

The development OLED/Mariko console used **500 mV** from 76.8 through 384 MHz. Those values are examples, not universal safe values.

Use **Benchmark Toolbox -> GPU Stress / FurMark** and treat any mismatch, graphics crash or CFW instability as a failed setting.

### 6. Final combined validation

Once the individual domains are stable, validate the completed Battery profile with the relevant stock limits:

- CPU **1785 MHz**
- RAM **1600 MHz**
- GPU **384 MHz**

Then run separately:

1. **CPU Matrixprod — about 30 min**
2. **RAM Memtester — at least 30 min; 60 min is better for the final RAM combination**
3. **GPU Stress / FurMark — about 30 min at 384 MHz**
4. Several real games for longer sessions

A synthetic pass is useful screening, not absolute proof of long-term stability. Keep some margin if you want dependable daily settings.

## Development-console battery-life result

Red Dead Redemption was tested at the **same stock game clocks/settings**, with **50% display brightness** and **0% volume**:

| Setting | Stock — no OC/UV profile | OC Mode profile | Battery Mode profile |
| --- | ---: | ---: | ---: |
| VDD2 | 1175 mV | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 600 mV | 400 mV |
| Runtime | 4 h 56 min | 5 h 32 min | 6 h 05 min |

Battery Mode vs OC Mode: **+33 minutes / +9.9% runtime**, equivalent to roughly **9.0% lower average whole-device power draw** in that test.

Battery Mode vs true stock: **+69 minutes / +23.3% runtime**, equivalent to roughly **18.9% lower average whole-device power draw**.

OC Mode vs true stock: **+36 minutes / +12.2% runtime**, equivalent to roughly **10.8% lower average whole-device power draw**.

This result is an example, not a guarantee. Battery condition, silicon quality, RAM, game load, temperatures and your own voltage margins all matter.

## App profiles

Horizon OC stores per-title CPU/GPU/RAM profiles inside the same `config.ini` that Performance Modes saves, so game profiles automatically switch together with Battery Mode / OC Mode.

If Battery Mode should use stock/default per-game clocks, run:

`Setup -> Reset Battery App Profiles -> STOCK`

This action only runs while **OC Mode is active**. If Battery Mode is active, nothing is changed and the package tells you to switch to OC Mode first.

## Storage names

Battery Mode is stored under `Battery/`.  
OC Mode is stored under `OCMode/`.

The internal state values are `BATTERY` and `OC Mode`. Older `PERFORMANCE` state values are migrated automatically to `OC Mode` when the package boots.
