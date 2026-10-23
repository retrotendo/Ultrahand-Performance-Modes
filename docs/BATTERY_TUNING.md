# Battery Profile – Simple Step-by-Step Undervolting Guide

Battery Mode is intended to keep the console inside Nintendo's stock handheld frequency range while reducing voltage headroom that is only needed for higher OC clocks.

Performance Modes assumes that you already have a **known-good, stability-tested OC profile** for your own console. This guide does not build that OC profile. It starts from a known-good setup and shows a simple way to find stable Battery Mode values one setting at a time.

> [!WARNING]
> There is no universal safe minimum voltage or universal UV level. Every CPU and RAM setup is different. A value that works on one Switch can fail on another.
>
> Keep a known-good **OC Mode** and a **Safety Backup** before tuning Battery Mode. If an aggressive setting prevents normal CFW from booting, use your **Hekate `CFW no OC` / safe boot entry** if your setup provides one, correct the value, save the KIP, and reboot normally. Performance Modes does not create or modify that Hekate entry.

## Before you start

Prepare Battery Mode with a conservative stock-handheld baseline before starting the undervolting process.

### Horizon OC

**Safety Settings**
- **Uncapped Clocks: OFF**

**RAM Settings**
- **HP Mode: OFF**
- **RAM Max Clock: 1600 MHz**
- **VDD2: 1175 mV** or your known stable lower value
- **VDDQ: 600 mV** or your known stable lower value

**CPU Settings**
- **CPU Max Clock: set to the lowest selectable value**
- **CPU UV Table: 1683Mhz Tbreak** or your already known working values
- **Low UV: 0** or your known working highest values
- **High UV: 0** or your known working highest values

### HOC Toolkit

**CPU Settings**
- **CPU Boost Clock: set to the lowest selectable value**

The stock CPU Boost limit cannot be selected directly in Horizon OC, so it must be set through HOC Toolkit. After applying the setting and rebooting CFW, Horizon OC will reflect the new CPU Boost limit.

### Reboot CFW

After the reboot, this is your conservative starting point. From here, begin the undervolting process and lower one setting at a time as described below.

The basic method is the same throughout the guide:

**change one step -> Save KIP -> reboot -> set Overrides -> short test -> repeat until first FAIL -> step back once -> long confirmation test**

---

# 1. Find the Best CPU Low UV

Keep RAM voltages at stock:

- VDD2: **1175 mV**
- VDDQ: **600 mV**

Start from:

- CPU UV Table: **Normal**
- Low UV: **0**
- High UV: **0**

### Start

1. Open Horizon OC.
2. Change **Low UV 0 -> Low UV 1**.
3. Save KIP.
4. Reboot.

### Does the Switch boot?

| ✅ YES | ❌ NO |
| --- | --- |
| Open Horizon OC and set Overrides: **CPU 1020 / GPU 384 / RAM 1331**.<br><br>Run **StressNX -> Matrixprod -> 1 minute**.<br><br>If it **PASSes**, increase Low UV by **1 level**.<br><br>Example: **Low UV1 -> Low UV2**.<br><br>Save KIP -> reboot -> set **1020 / 384 / 1331** again -> Matrixprod for 1 minute.<br><br>Repeat until the first FAIL.<br><br>If the 1-minute test FAILS, reduce Low UV by **1 level**, Save KIP and reboot. That previous level is your candidate. | 1. Boot Hekate.<br>2. Start **CFW without Horizon OC / hoc.kip**.<br>3. Open Horizon OC.<br>4. Reduce Low UV by **1 level**.<br>5. Save KIP.<br>6. Reboot normally.<br><br>The previous UV level is now your candidate. |

### Confirm the candidate

Set Overrides:

**1020 / 384 / 1331**

Run:

**Matrixprod -> 1 hour**

If the 1-hour test fails, reduce Low UV by another **1 level**, Save KIP, reboot and repeat the 1-hour test.

Keep the **highest Low UV level that passes the full hour**.

---

# 2. Find the Lowest Stable Low VMIN

Keep the final Low UV value from Step 1.

RAM voltages remain stock:

- VDD2: **1175 mV**
- VDDQ: **600 mV**

### Start

1. Open Horizon OC.
2. Lower Low VMIN to the **next available mV value**.
3. Save KIP.
4. Reboot.

### Does the Switch boot?

| ✅ YES | ❌ NO |
| --- | --- |
| Open Horizon OC and set Overrides: **CPU 1020 / GPU 384 / RAM 1331**.<br><br>Run **Matrixprod -> 1 minute**.<br><br>If it **PASSes**, lower Low VMIN to the next lower available value.<br><br>Save KIP -> reboot -> set Overrides again -> test 1 minute.<br><br>Repeat until the first FAIL.<br><br>If the 1-minute test FAILS, restore the **previous Low VMIN value**, Save KIP and reboot. That previous value is your candidate. | 1. Boot Hekate.<br>2. Start **CFW without Horizon OC / hoc.kip**.<br>3. Open Horizon OC.<br>4. Restore the **previous Low VMIN value**.<br>5. Save KIP.<br>6. Reboot normally.<br><br>The restored value is your candidate. |

### Confirm the candidate at low CPU clocks

With the candidate Low VMIN, test:

- **510 MHz**
- **612 MHz**
- **816 MHz**
- **1020 MHz**

Keep:

- GPU: **384 MHz**
- RAM: **1331 MHz**

Run Matrixprod briefly at each CPU clock.

If all pass, run Matrixprod for **1 hour** at the low CPU clock that appeared most sensitive during the sweep. If none stands out, use the lowest tested clock as the long confirmation point.

Also check normal system behavior:

- Home Menu
- Sleep
- Wake
- Launch a game
- Close a game

If anything fails, raise Low VMIN to the **previous mV value** and repeat the checks.

---

# 3. Find the Lowest Stable VDDQ

Keep your final CPU Low UV and Low VMIN.

Start RAM tuning from stock:

- VDD2: **1175 mV**
- VDDQ: **600 mV**

Only change VDDQ.

### Start

Lower:

**VDDQ 600 -> 590 mV**

Save KIP and reboot.

### Does the Switch boot?

| ✅ YES | ❌ NO |
| --- | --- |
| Open Horizon OC and set Overrides: **CPU 1785 / GPU 76.8 / RAM 1600**.<br><br>Run **Benchmark Toolbox -> MemTester -> 1 minute**.<br><br>If it **PASSes**, lower VDDQ by another **10 mV**.<br><br>Example: **590 -> 580 -> 570 -> 560 mV**.<br><br>After every change: Save KIP -> reboot -> set **1785 / 76.8 / 1600** -> MemTester for 1 minute.<br><br>Repeat until the first FAIL.<br><br>If the 1-minute test FAILS, increase VDDQ by **10 mV**, Save KIP and reboot. That previous value is your candidate. | 1. Boot Hekate.<br>2. Start **CFW without Horizon OC / hoc.kip**.<br>3. Open Horizon OC.<br>4. Increase VDDQ by **10 mV**.<br>5. Save KIP.<br>6. Reboot normally.<br><br>Example: **410 mV does not boot -> restore 420 mV**.<br><br>The restored value is your candidate. |

### Confirm the candidate

Set Overrides:

**1785 / 76.8 / 1600**

Run:

**MemTester -> 1 hour**

If the 1-hour test fails, increase VDDQ by another **10 mV**, Save KIP, reboot and repeat the 1-hour test.

Keep the **lowest VDDQ that passes the full hour**.

---

# 4. Find the Lowest Stable VDD2

Keep your final VDDQ from Step 3.

Start VDD2 from:

**1175 mV**

Only change VDD2.

### Start

Lower VDD2 by:

**12.5 mV**

Save KIP and reboot.

### Does the Switch boot?

| ✅ YES | ❌ NO |
| --- | --- |
| Open Horizon OC and set Overrides: **CPU 1785 / GPU 76.8 / RAM 1600**.<br><br>Run **Benchmark Toolbox -> MemTester -> 1 minute**.<br><br>If it **PASSes**, lower VDD2 by another **12.5 mV**.<br><br>Save KIP -> reboot -> set **1785 / 76.8 / 1600** -> MemTester for 1 minute.<br><br>Repeat until the first FAIL.<br><br>If the 1-minute test FAILS, increase VDD2 by **12.5 mV**, Save KIP and reboot. That previous value is your candidate.<br><br>Horizon OC may display half-step values rounded, e.g. **937.5 -> 937 mV** and **912.5 -> 912 mV**. | 1. Boot Hekate.<br>2. Start **CFW without Horizon OC / hoc.kip**.<br>3. Open Horizon OC.<br>4. Increase VDD2 by **12.5 mV**.<br>5. Save KIP.<br>6. Reboot normally.<br><br>Example: **900 mV does not boot -> restore 912.5 mV**.<br><br>The restored value is your candidate. |

### Confirm the candidate

Set Overrides:

**1785 / 76.8 / 1600**

Run:

**MemTester -> 1 hour**

If the 1-hour test fails, increase VDD2 by another **12.5 mV**, Save KIP, reboot and repeat the 1-hour test.

Keep the **lowest VDD2 that passes the full hour**.

---

# 5. Confirm Final VDDQ + VDD2 Together

Use your final:

- VDDQ
- VDD2

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1785 MHz**
- GPU: **76.8 MHz**
- RAM: **1600 MHz**

Run:

**MemTester -> 1 hour**

### Did the combined test pass?

| ✅ YES | ❌ NO |
| --- | --- |
| Keep both final values. The VDDQ/VDD2 pair is confirmed at **1785 / 76.8 / 1600**. | Do **not** raise both voltages together.<br><br>First increase **VDDQ by 10 mV**. Save KIP -> reboot -> set **1785 / 76.8 / 1600** -> MemTester for 1 hour.<br><br>If it still FAILS, restore VDDQ to the previous value. Then increase **VDD2 by 12.5 mV**. Save KIP -> reboot -> set the Overrides again -> repeat MemTester for 1 hour.<br><br>This keeps troubleshooting to one voltage at a time. |

---

# 6. Confirm RAM at Normal Handheld Clocks

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1020 MHz**
- GPU: **384 MHz**
- RAM: **1331 MHz**

Run:

**Benchmark Toolbox -> MemTester -> 1 hour**

If it PASSes, your final VDDQ/VDD2 pair has now been checked at both stock RAM states used in this guide.

---

# 7. Find the Best CPU High UV

Keep all final values found so far:

- Low UV
- Low VMIN
- VDDQ
- VDD2

Start from:

**High UV 0**

### Start

Change:

**High UV0 -> High UV1**

Save KIP and reboot.

### Does the Switch boot?

| ✅ YES | ❌ NO |
| --- | --- |
| Open Horizon OC and set Overrides: **CPU 1785 / GPU 76.8 / RAM 1600**.<br><br>Run **StressNX -> Matrixprod -> 1 minute**.<br><br>If it **PASSes**, increase High UV by **1 level**.<br><br>Save KIP -> reboot -> set **1785 / 76.8 / 1600** -> Matrixprod for 1 minute.<br><br>Repeat until the first FAIL.<br><br>If the 1-minute test FAILS, reduce High UV by **1 level**, Save KIP and reboot. That previous level is your candidate. | 1. Boot Hekate.<br>2. Start **CFW without Horizon OC / hoc.kip**.<br>3. Open Horizon OC.<br>4. Reduce High UV by **1 level**.<br>5. Save KIP.<br>6. Reboot normally.<br><br>The previous High UV level is now your candidate. |

### Confirm the candidate

Set Overrides:

**1785 / 76.8 / 1600**

Run:

**Matrixprod -> 1 hour**

If the 1-hour test fails, reduce High UV by another **1 level**, Save KIP, reboot and repeat the 1-hour test.

Keep the **highest High UV level that passes the full hour**.

---

# 8. Confirm High UV + Final RAM Voltages

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1785 MHz**
- GPU: **76.8 MHz**
- RAM: **1600 MHz**

Run:

**CPU-Memtester -> 1 hour**

Any mismatch = FAIL.

If it fails, first reduce **High UV by 1 level**.

Save KIP -> reboot -> set **1785 / 76.8 / 1600** -> CPU-Memtester for another hour.

Do not immediately raise VDDQ or VDD2. Only investigate RAM voltages if reducing High UV does not fix the failure.

---

# 9. Final Normal Handheld Test

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1020 MHz**
- GPU: **384 MHz**
- RAM: **1331 MHz**

Run:

1. **StressNX -> Matrixprod -> 1 hour**
2. **Benchmark Toolbox -> MemTester -> 1 hour**
3. **GPU Stress Test -> 1 hour**

Everything must PASS.

The GPU test here is a final validation of the inherited stock-clock GPU settings; this guide is not trying to retune the full GPU curve.

---

# 10. Final Nintendo Boost Test

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1785 MHz**
- GPU: **76.8 MHz**
- RAM: **1600 MHz**

Run:

1. **Matrixprod -> 1 hour**
2. **MemTester -> 1 hour**
3. **CPU-Memtester -> 1 hour**

Everything must PASS.

---

# 11. Final Real-World Test

Remove all manual Overrides.

Use the console normally and test:

- Game launch
- Home Menu
- Resume game
- Sleep
- Wake
- Loading screens
- CPU Boost
- Return from CPU Boost

Then play:

**The Legend of Zelda: Tears of the Kingdom**

for at least:

**1 hour of active gameplay**

No crashes, freezes, mismatches or reboots.

Once everything is stable, save the finished setup with:

`Performance Modes -> Save Settings -> as Battery Mode`

You can then switch back to OC Mode and optionally create a new Safety Backup containing both final known-good profiles.
