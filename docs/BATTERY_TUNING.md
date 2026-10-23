# Battery Profile – Simple Step-by-Step Undervolting Guide

Battery Mode is intended to keep the console inside Nintendo's stock handheld frequency range while reducing voltage headroom that is only needed for higher OC clocks.

Performance Modes assumes that you already have a **known-good, stability-tested OC profile** for your own console. This guide does not build that OC profile. It starts from a known-good setup and shows a simple way to find stable Battery Mode values one setting at a time.

> [!WARNING]
> There is no universal safe minimum voltage or universal UV level. Every CPU and RAM setup is different. A value that works on one Switch can fail on another.
>
> Keep a known-good **OC Mode** and a **Safety Backup** before tuning Battery Mode. If an aggressive setting prevents normal CFW from booting, use your **Hekate `CFW no OC` / safe boot entry** if your setup provides one, correct the value and reboot normally. Performance Modes does not create or modify that Hekate entry.

## Before you start

Prepare Battery Mode for stock-handheld behavior before starting the undervolting process. Use the conservative baseline values below unless you already have known-stable values for your console.

### Horizon OC

**Safety Settings**
- **Uncapped Clocks: OFF**

**RAM Settings**
- **HP Mode: OFF**
- **RAM Max Clock: 1600 MHz**
- **VDD2: 1175 mV** or your known stable lower value
- **VDDQ: 600 mV** or your known stable lower value

**CPU Settings**
- **CPU Low VMIN: 620mv** or your known-stable value
- **CPU Max Clock: set to the lowest selectable value**
- **CPU UV Table: 1683 MHz Tbreak** or your known-working CPU UV table
- **Low UV: 0** or your known-stable value
- **High UV: 0** or your known-stable value

### HOC Toolkit

**CPU Settings**
- **CPU Boost Clock: set to the lowest selectable value**

The stock CPU Boost limit cannot be selected directly in Horizon OC, so it must be set through HOC Toolkit. After setting it in HOC Toolkit and rebooting CFW, Horizon OC will reflect the new CPU Boost limit.

### Reboot CFW

After the reboot, this is your starting point. From here, begin the undervolting process and change only one setting at a time as described below.

The basic method is the same throughout the guide:

**change one step -> reboot -> set Overrides -> short test -> if it PASSes, change one more step -> reboot -> test again -> stop at the first failing setting -> restore the previous passing setting -> long confirmation test**

---

# 1. Find the Best CPU Low UV

Keep the RAM voltages at the baseline values selected in **Before you start**. Do not change VDD2 or VDDQ during CPU tuning.

Keep the CPU UV table selected in **Before you start** unchanged throughout the CPU tuning steps. The recommended baseline is:

- CPU UV Table: **1683 MHz Tbreak**
- Low UV: **0**, or your known-stable Low UV value
- High UV: **0**, or your known-stable High UV value

### Start

1. Open Horizon OC.
2. Increase **Low UV by 1 level**.
   - If you started from **Low UV 0**, change **Low UV 0 -> Low UV 1**.
   - If you entered a known-stable Low UV value in **Before you start**, continue from that value.
3. Reboot.

### Does the Switch boot?

<table width="100%">
  <thead>
    <tr>
      <th width="50%">✅ YES</th>
      <th width="50%">❌ NO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
<ol>
<li>Open Horizon OC.</li>
<li>Set Overrides to <strong>CPU 1020 / GPU 384 / RAM 1331</strong>.</li>
<li>Run <strong>StressNX -> Matrixprod -> 1 minute</strong>.</li>
<li>If it <strong>PASSes</strong>, increase Low UV by <strong>1 level</strong>.</li>
<li>Reboot.</li>
<li>Set <strong>1020 / 384 / 1331</strong> again.</li>
<li>Run <strong>Matrixprod for 1 minute</strong> again.</li>
<li>If it <strong>PASSes</strong>, increase Low UV by another <strong>1 level</strong> and repeat steps 5–7 with the new level.</li>
<li>When a newly tested Low UV level <strong>FAILS</strong>, reduce Low UV by <strong>1 level</strong> and reboot. The previous passing level is your candidate.</li>
</ol>
      </td>
      <td width="50%" valign="top">
<ol>
<li>Boot Hekate.</li>
<li>Start <strong>CFW without Horizon OC / hoc.kip</strong>.</li>
<li>Open Horizon OC.</li>
<li>Reduce Low UV by <strong>1 level</strong>.</li>
<li>Reboot normally.</li>
<li>Use the restored Low UV level as your candidate.</li>
</ol>
      </td>
    </tr>
  </tbody>
</table>

### Confirm the candidate

Set Overrides:

**1020 / 384 / 1331**

Run:

**Matrixprod -> 1 hour**

If the 1-hour test fails, reduce Low UV by another **1 level**, reboot and repeat the 1-hour test.

Keep the **highest Low UV level that passes the full hour**.

---

# 2. Find Your Low VMIN Test Clocks

Keep the final **Low UV** value from Step 1.

Before tuning Low VMIN, first find out how the CPU voltage changes across the lower CPU clocks on your console.

### Find the clocks to test

1. Reboot with your current settings.
2. Open Horizon OC.
3. Use **CPU Override** and step through the available CPU clocks from low to high.
4. Watch the reported CPU voltage in your overlay.
5. Whenever several CPU clocks use the same voltage, note only the **highest clock that still uses that voltage**.

These highest clocks for each different voltage level will be your **Low VMIN test clocks** in the next step.

### Example

With:

- Low VMIN: **570 mV**
- Low UV: **1**

one console may show approximately:

- 510–816 MHz -> **570 mV**
- 918 MHz -> **570–585 mV**
- 1020 MHz -> **600 mV**

In this example, the useful test clocks are:

- **816 MHz** -> highest clock at 570 mV
- **918 MHz** -> highest clock in the 570–585 mV transition range
- **1020 MHz** -> highest clock at 600 mV in this example

There is no need to separately stress-test 510, 612 or 714 MHz if they all run at the same **570 mV**. The highest frequency using that voltage is the more demanding test point.

Your exact clocks and voltage steps may be different, so always determine them from the values shown on your own console.

---

# 3. Find the Lowest Stable Low VMIN

Use the **Low VMIN test clocks identified in Step 2**.

Keep your final **Low UV** value from Step 1 and keep VDD2/VDDQ unchanged.

### Find the lowest value that still boots

1. Open Horizon OC.
2. Lower **Low VMIN** to the next available value.
3. Reboot.

### Does the Switch boot?

<table width="100%">
  <thead>
    <tr>
      <th width="50%">✅ YES</th>
      <th width="50%">❌ NO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
<ol>
<li>Lower Low VMIN to the <strong>next available value</strong>.</li>
<li>Reboot again.</li>
<li>If the Switch still boots, lower Low VMIN by another step.</li>
<li>Continue until you reach the first Low VMIN value that no longer boots.</li>
</ol>

The last value that still booted is your first candidate.

      </td>
      <td width="50%" valign="top">
<ol>
<li>Boot Hekate.</li>
<li>Start <strong>CFW without Horizon OC / hoc.kip</strong>.</li>
<li>Open Horizon OC.</li>
<li>Restore the <strong>previous Low VMIN value</strong>.</li>
<li>Reboot normally.</li>
</ol>

The restored value is your first candidate.

      </td>
    </tr>
  </tbody>
</table>

### Test the candidate

Use the **Low VMIN test clocks from Step 2**.

Keep:

- GPU: **384 MHz**
- RAM: **1331 MHz**

Run:

**Matrixprod -> 1 minute**

at **each Low VMIN test clock**.

If all test clocks **PASS**, keep this Low VMIN value as your candidate for the long confirmation test.

If any test clock **FAILS or crashes**:

1. Increase Low VMIN by **one step**
2. Reboot
3. Test **all Low VMIN test clocks again**

Repeat until every test clock passes.

### Confirm the final candidate

Run **Matrixprod -> 1 hour** at each Low VMIN test clock.

If any test fails, increase Low VMIN by one more step, reboot and repeat the tests.

Keep the **lowest Low VMIN value that passes all test clocks**.

---

# 4. Find the Lowest Stable VDDQ

Keep your final CPU Low UV and Low VMIN. Keep the CPU UV table and High UV at the baseline values selected in **Before you start** so CPU settings remain unchanged while tuning RAM.

Start from the RAM-voltage baseline selected in **Before you start**:

- Keep **VDD2 unchanged**
- Start VDDQ from **600 mV**, or your known-stable lower baseline value

Only change VDDQ in this step.

### Start

Lower VDDQ by **10 mV**.

Example from the conservative baseline:

**600 -> 590 mV**

Reboot.

### Does the Switch boot?

<table width="100%">
  <thead>
    <tr>
      <th width="50%">✅ YES</th>
      <th width="50%">❌ NO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
<ol>
<li>Open Horizon OC.</li>
<li>Set Overrides to <strong>CPU 1785 / GPU 76.8 / RAM 1600</strong>.</li>
<li>Run <strong>Benchmark Toolbox -> MemTester -> 1 minute</strong>.</li>
<li>If it <strong>PASSes</strong>, lower VDDQ by another <strong>10 mV</strong>.</li>
<li>Reboot.</li>
<li>Set <strong>1785 / 76.8 / 1600</strong> again.</li>
<li>Run <strong>MemTester for 1 minute</strong> again.</li>
<li>If it <strong>PASSes</strong>, lower VDDQ by another <strong>10 mV</strong> and repeat steps 5–7 with the new value.</li>
<li>When a newly tested VDDQ value <strong>FAILS</strong>, increase VDDQ by <strong>10 mV</strong> and reboot. The previous passing value is your candidate.</li>
</ol>
      </td>
      <td width="50%" valign="top">
<ol>
<li>Boot Hekate.</li>
<li>Start <strong>CFW without Horizon OC / hoc.kip</strong>.</li>
<li>Open Horizon OC.</li>
<li>Increase VDDQ by <strong>10 mV</strong>.</li>
<li>Reboot normally.</li>
<li>Use the restored VDDQ value as your candidate.</li>
</ol>
<p>Example: <strong>410 mV does not boot -> restore 420 mV</strong>.</p>
      </td>
    </tr>
  </tbody>
</table>

### Confirm the candidate

Set Overrides:

**1785 / 76.8 / 1600**

Run:

**MemTester -> 1 hour**

If the 1-hour test fails, increase VDDQ by another **10 mV**, reboot and repeat the 1-hour test.

Keep the **lowest VDDQ that passes the full hour**.

---

# 5. Find the Lowest Stable VDD2

Keep your final VDDQ from Step 4. Keep all CPU settings unchanged while tuning VDD2.

Start VDD2 from the baseline selected in **Before you start**:

**1175 mV**, or your known-stable lower baseline value

Only change VDD2 in this step.

### Start

Lower VDD2 by:

**12.5 mV**

Reboot.

### Does the Switch boot?

<table width="100%">
  <thead>
    <tr>
      <th width="50%">✅ YES</th>
      <th width="50%">❌ NO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
<ol>
<li>Open Horizon OC.</li>
<li>Set Overrides to <strong>CPU 1785 / GPU 76.8 / RAM 1600</strong>.</li>
<li>Run <strong>Benchmark Toolbox -> MemTester -> 1 minute</strong>.</li>
<li>If it <strong>PASSes</strong>, lower VDD2 by another <strong>12.5 mV</strong>.</li>
<li>Reboot.</li>
<li>Set <strong>1785 / 76.8 / 1600</strong> again.</li>
<li>Run <strong>MemTester for 1 minute</strong> again.</li>
<li>If it <strong>PASSes</strong>, lower VDD2 by another <strong>12.5 mV</strong> and repeat steps 5–7 with the new value.</li>
<li>When a newly tested VDD2 value <strong>FAILS</strong>, increase VDD2 by <strong>12.5 mV</strong> and reboot. The previous passing value is your candidate.</li>
</ol>
<p>Horizon OC may display half-step values rounded, e.g. <strong>937.5 -> 937 mV</strong> and <strong>912.5 -> 912 mV</strong>.</p>
      </td>
      <td width="50%" valign="top">
<ol>
<li>Boot Hekate.</li>
<li>Start <strong>CFW without Horizon OC / hoc.kip</strong>.</li>
<li>Open Horizon OC.</li>
<li>Increase VDD2 by <strong>12.5 mV</strong>.</li>
<li>Reboot normally.</li>
<li>Use the restored VDD2 value as your candidate.</li>
</ol>
<p>Example: <strong>900 mV does not boot -> restore 912.5 mV</strong>.</p>
      </td>
    </tr>
  </tbody>
</table>

### Confirm the candidate

Set Overrides:

**1785 / 76.8 / 1600**

Run:

**MemTester -> 1 hour**

If the 1-hour test fails, increase VDD2 by another **12.5 mV**, reboot and repeat the 1-hour test.

Keep the **lowest VDD2 that passes the full hour**.

---

# 6. Confirm Final VDDQ + VDD2 Together

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

<table width="100%">
  <thead>
    <tr>
      <th width="50%">✅ YES</th>
      <th width="50%">❌ NO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
<ol>
<li>Keep both final values.</li>
<li>The VDDQ/VDD2 pair is confirmed at <strong>1785 / 76.8 / 1600</strong>.</li>
</ol>
      </td>
      <td width="50%" valign="top">
<ol>
<li>Do <strong>not</strong> raise both voltages together.</li>
<li>Increase <strong>VDDQ by 10 mV</strong>.</li>
<li>Reboot and set <strong>1785 / 76.8 / 1600</strong> again.</li>
<li>Run <strong>MemTester for 1 hour</strong>.</li>
<li>If it still <strong>FAILS</strong>, restore VDDQ to the previous value.</li>
<li>Increase <strong>VDD2 by 12.5 mV</strong>.</li>
<li>Reboot, set the Overrides again and run <strong>MemTester for 1 hour</strong>.</li>
<li>Keep troubleshooting one voltage at a time.</li>
</ol>
      </td>
    </tr>
  </tbody>
</table>

---

# 7. Confirm RAM at Normal Handheld Clocks

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1020 MHz**
- GPU: **384 MHz**
- RAM: **1331 MHz**

Run:

**Benchmark Toolbox -> MemTester -> 1 hour**

If it PASSes, your final VDDQ/VDD2 pair has now been checked at both stock RAM states used in this guide.

---

# 8. Find the Best CPU High UV

Keep all final values found so far:

- Low UV
- Low VMIN
- VDDQ
- VDD2

Start from the High UV value selected in **Before you start**:

- **High UV 0**, or your known-stable High UV value

Keep **CPU UV Table = 1683 MHz Tbreak** (or your known-working table) unchanged.

### Start

Increase High UV by **1 level**.

Example from the conservative baseline:

**High UV 0 -> High UV 1**

Reboot.

### Does the Switch boot?

<table width="100%">
  <thead>
    <tr>
      <th width="50%">✅ YES</th>
      <th width="50%">❌ NO</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td width="50%" valign="top">
<ol>
<li>Open Horizon OC.</li>
<li>Set Overrides to <strong>CPU 1785 / GPU 76.8 / RAM 1600</strong>.</li>
<li>Run <strong>StressNX -> Matrixprod -> 1 minute</strong>.</li>
<li>If it <strong>PASSes</strong>, increase High UV by <strong>1 level</strong>.</li>
<li>Reboot.</li>
<li>Set <strong>1785 / 76.8 / 1600</strong> again.</li>
<li>Run <strong>Matrixprod for 1 minute</strong> again.</li>
<li>If it <strong>PASSes</strong>, increase High UV by another <strong>1 level</strong> and repeat steps 5–7 with the new level.</li>
<li>When a newly tested High UV level <strong>FAILS</strong>, reduce High UV by <strong>1 level</strong> and reboot. The previous passing level is your candidate.</li>
</ol>
      </td>
      <td width="50%" valign="top">
<ol>
<li>Boot Hekate.</li>
<li>Start <strong>CFW without Horizon OC / hoc.kip</strong>.</li>
<li>Open Horizon OC.</li>
<li>Reduce High UV by <strong>1 level</strong>.</li>
<li>Reboot normally.</li>
<li>Use the restored High UV level as your candidate.</li>
</ol>
      </td>
    </tr>
  </tbody>
</table>

### Confirm the candidate

Set Overrides:

**1785 / 76.8 / 1600**

Run:

**Matrixprod -> 1 hour**

If the 1-hour test fails, reduce High UV by another **1 level**, reboot and repeat the 1-hour test.

Keep the **highest High UV level that passes the full hour**.

---

# 9. Confirm High UV + Final RAM Voltages

Reboot.

Open Horizon OC and set Overrides:

- CPU: **1785 MHz**
- GPU: **76.8 MHz**
- RAM: **1600 MHz**

Run:

**CPU-Memtester -> 1 hour**

Any mismatch = FAIL.

If it fails, first reduce **High UV by 1 level**.

Reboot -> set **1785 / 76.8 / 1600** -> CPU-Memtester for another hour.

Do not immediately raise VDDQ or VDD2. Only investigate RAM voltages if reducing High UV does not fix the failure.

---

# 10. Final Normal Handheld Test

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

# 11. Final Nintendo Boost Test

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

# 12. Final Real-World Test

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
