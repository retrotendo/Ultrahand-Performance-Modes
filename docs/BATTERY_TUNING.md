# Battery profile tuning — practical quick guide

Battery Mode is **not** a second maximum-overclock profile. It is intended to keep the console inside Nintendo's stock handheld frequency range while reducing the voltage headroom that is no longer needed for the higher clocks used by OC Mode.

Performance Modes assumes that you already have a **known-good, stability-tested OC profile** for your console. That OC Mode should already contain CPU/GPU/RAM limits, voltage curves and other Horizon OC / HOC Toolkit values that you know are stable on your own hardware.

Battery Mode starts from that known-good profile and simplifies it for stock handheld operation. In practice, the main Battery Mode efficiency controls are usually:

- **RAM VDD2**
- **RAM VDDQ**
- **CPU Low UV** for normal stock-frequency handheld CPU operation

Most other values can normally remain at their known-good OC Mode settings unless you have a specific reason to change them. If you retain a higher CPU boost limit such as 1785 MHz, the higher-frequency UV settings still need to remain stable, but they do not need to be the main Battery Mode tuning target.

> [!WARNING]
> There is no universal safe minimum voltage or universal UV level. Every CPU and RAM setup is different. Change one area at a time, test it, and keep a known-good OC Mode / Safety Backup.
>
> If an overly aggressive UV prevents normal CFW from booting, use your **Hekate `CFW no OC` / safe boot entry** if your setup provides one. Correct the value in Horizon OC or HOC Toolkit, save/apply it, then reboot normal CFW. Performance Modes does not create that Hekate entry.

## Recommended Battery starting point

Before lowering voltages, first create a conservative stock-behavior baseline:

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

On the development OLED, the stock comparison baseline used **VDD2 1175 mV / VDDQ 600 mV**. These values are useful as conservative reference points for that console, not universal minimums.

### Optional CPU maximum / boost

If desired, keep **CPU Max Clock = 1785 MHz** and **CPU Boost Clock = 1785 MHz** through HOC Toolkit. Stock game profiles can still remain at stock CPU clocks while the normal boost step remains available.

If the KIP is changed in HOC Toolkit, save/apply it and reboot CFW so the updated `hoc.kip` is actually loaded.

The higher-frequency UV settings used by boost still need to be stable. However, for Battery Mode efficiency at normal stock handheld game clocks, **CPU Low UV is the main CPU tuning control**.

## Suggested tuning order

### 1. Start from a known-good OC profile

1. Boot and save your already tested **OC Mode**.
2. Create the Battery profile slot from that known-good setup.
3. Switch to Battery Mode.
4. In **Horizon OC -> Safety Settings**, set **Uncapped Clocks OFF**.
5. In **RAM Settings**, set **HP Mode OFF** and **RAM Max Clock = 1600 MHz**.
6. Set VDD2/VDDQ to safe stock/default values before beginning the undervolt.
7. Keep stock/default per-title CPU/GPU/RAM clocks if Battery Mode is intended to be a true stock-clock profile.

Do not lower VDD2, VDDQ and CPU Low UV all at the same time. If a test fails, you need to know which change caused it.

### 2. Tune RAM VDD2 first

Keep **VDDQ at a known-safe value** while finding VDD2.

1. Keep RAM at **1600 MHz** with HP Mode OFF.
2. Lower **VDD2** by one available step.
3. Reboot if required for the value to become active.
4. Run **Benchmark Toolbox -> RAM -> Memtester**.
5. Use short passes while approaching the edge, then run a promising candidate for about **30 minutes**.
6. At the first mismatch, freeze or crash, return to the previous stable step.

Development-console Battery value: **~912.5 mV**.  
Development-console stock baseline: **1175 mV**.  
Development-console OC Mode value: **1087.5 mV**.

### 3. Tune VDDQ second

Keep the stable VDD2 value fixed and tune VDDQ independently.

1. Keep RAM at **1600 MHz** with HP Mode OFF.
2. Lower VDDQ one available step at a time.
3. Run Memtester again.
4. At the first error / mismatch / crash, return to the previous stable step.
5. After both RAM voltages are chosen, run **30–60 minutes** of Memtester with the final pair active together.

Development-console Battery value: **400 mV**.  
Development-console stock baseline: **600 mV**.

### 4. Tune CPU Low UV for stock-frequency operation

For Battery Mode, the goal is to optimize the CPU range actually used during normal stock handheld gaming rather than retune the full high-clock CPU curve.

1. Keep stock/default game CPU clocks.
2. Start from a known-stable **CPU Low UV** level.
3. Increase the Low UV setting one step at a time; a higher UV setting is a more aggressive undervolt.
4. Reboot when required.
5. Run CPU stress tests and real games that exercise the normal stock-frequency CPU range.
6. Any mismatch, freeze, application crash or CFW reboot means the undervolt is too aggressive. Step back.
7. Once a candidate is found, perform a longer combined validation with the final RAM voltages active as well.

If you retain a 1785 MHz CPU boost limit, leave the higher-frequency UV side at a **known-stable value** from your existing OC profile unless you specifically want to tune it separately. It is not necessary to chase the lowest possible high-frequency voltage just to build an effective Battery Mode.

### 5. GPU and other OC settings

If your existing OC profile already has stable GPU voltage points and other Horizon OC settings, there is normally no need to retune all of them for Battery Mode.

Battery Mode uses stock handheld GPU clocks, so the full high-clock GPU curve is not a primary Battery Mode tuning lever. The same applies to other OC-only parameters that are not used at stock handheld frequencies.

Keep these values at known-good settings unless you have a specific reason and a separate stability-testing plan for changing them.

### 6. Final combined validation

Once VDD2, VDDQ and CPU Low UV are individually stable, validate the completed Battery profile with the intended stock handheld limits.

Recommended final checks:

1. **RAM Memtester — at least 30 min; 60 min is better for the final RAM combination**
2. **CPU stress testing at the stock-frequency range**
3. Several real games for longer sessions
4. Repeated mode changes between Battery Mode and OC Mode to verify both stored profiles still load correctly

A synthetic pass is useful screening, not absolute proof of long-term stability. Keep some margin if you want dependable daily settings.

## Development-console battery-life result

Red Dead Redemption was tested at the **same stock game clocks/settings**, with **50% display brightness** and **0% volume**:

| Setting | Stock — no OC/UV profile | OC Mode profile | Battery Mode profile |
| --- | ---: | ---: | ---: |
| VDD2 | 1175 mV | 1087.5 mV | ~912.5 mV |
| VDDQ | 600 mV | 600 mV | 400 mV |
| Runtime | 4 h 56 min | 5 h 32 min | 6 h 05 min |

Compared with the **true stock baseline**, OC Mode ran **36 minutes longer**, or about **+12.2% runtime**, equivalent to roughly **10.8% lower average whole-device power draw** at the same game clocks/settings.

Compared with the **true stock baseline**, Battery Mode ran **69 minutes longer**, or about **+23.3% runtime**, equivalent to roughly **18.9% lower average whole-device power draw** at the same game clocks/settings.

This result is an example, not a guarantee. Battery condition, silicon quality, RAM, game load, temperatures and your own voltage margins all matter.

## App profiles

Horizon OC stores per-title CPU/GPU/RAM profiles inside the same `config.ini` that Performance Modes saves, so game profiles automatically switch together with Battery Mode / OC Mode.

If Battery Mode should use stock/default per-game clocks, run:

`Setup -> Reset Battery App Profiles -> STOCK`

This action only runs while **OC Mode is active**. If Battery Mode is active, nothing is changed and the package tells you to switch to OC Mode first.

## Storage names and state

Battery Mode is stored under `Battery/`.  
OC Mode is stored under `OCMode/`.

The package uses the visible state values directly:

- `Battery Mode`
- `OC Mode`
