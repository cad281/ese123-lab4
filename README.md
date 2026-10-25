# ESE 123 Lab 4: Function Generator & Oscilloscope

**Interactive page:** https://cad281.github.io/ese123-lab4/

All labs: [Lab 1: DC Power & Ohm's Law](https://cad281.github.io/ese123-lab1/) · [Lab 2: Digital Multimeter](https://cad281.github.io/ese123-lab2/) · [Lab 3: SPICE & Soldering](https://cad281.github.io/ese123-lab3/) · [Lab 4: Function Generator & Scope](https://cad281.github.io/ese123-lab4/) · [Lab 5: Capacitors & Scope](https://cad281.github.io/ese123-lab5/) · [Lab 6: Operational Amplifiers](https://cad281.github.io/ese123-lab6/)

A TA-written guide for ESE 123 students: **what** you do in Lab 4, **why** it matters and **how** to do it. The interactive page simulates the generator's 50 Ω output, builds RMS step by step, explains the 10:1 probe and lets you play with scope triggering.

---

## What this lab is about

| You will… | Using… |
|---|---|
| Set frequency, amplitude, wave shape, duty cycle and symmetry | Keysight 33210A / 33220A function generator |
| Discover the generator's **50 Ω output resistance** | DMM (AC volts) and a 51 Ω load |
| Measure **RMS** of sine and square waves | DMM, pre-lab formulas |
| Check probe attenuation, read the screen, count boxes | Agilent DSO-X 3012A oscilloscope + 10:1 probes |
| Learn **triggering**: source, level, slope, Auto vs Normal | Probe-comp square wave + generator sine |
| Save scope screenshots | The lab's *Take Screenshot* tool |
| (Pre-lab) Simulate a sine and resistor power with **.tran** | LTspice |

## Why it matters

- The generator and scope are used in **every remaining lab**. Lab 5 builds directly on this one.
- The generator's voltage display is an **estimate that assumes a 50 Ω load**. Our circuits are usually high-impedance, so the real voltage is about **2× the display**. Always measure; trust only the frequency display.
- **RMS** is how AC voltages are compared with DC (it's what wall outlets and DMMs quote).
- Without **triggering**, a fast repeating signal is an unreadable blur. Setting the trigger is the most important scope skill.

## How to do it, step by step

### Part 1: function generator + DMM (steps 1–10)
1. Connect the generator **OUTPUT** (not SYNC) BNC to the DMM's voltage inputs. Twist the BNC sleeve ¼ turn to lock it.
2. DMM to **AC volts**.
3. Generator: **Sine**, **Freq** = 60 Hz (keypad → Hz soft key), **Ampl** = 1 → **Vrms** soft key, then press **Output**.
4. Record display and DMM. **Expect DMM ≈ 2.0 Vrms**: the DMM is 10 MΩ, not 50 Ω.
5. Measure the 51 Ω resistor (green-brown-black) with the DMM's Ω function to full precision.
6. Put it across the output and measure AC volts again. **Expect ≈ 1.0 Vrms** (nearly matched).
7. **Graph** key: look at sine, square (**Dty Cyc** 20%) and ramp (**Symtry** 50% = triangle). **Graph** again to exit.

### Part 2: RMS of different shapes
1. Set **1 Vpp** (51 Ω still connected).
2. Sine: **expect ≈ 0.354 Vrms**. 50% square (V_L = −0.5, V_H = +0.5 V): **expect ≈ 0.500 Vrms**.
3. Output off; disconnect.

### Part 3: probe check
Power the scope on, wait for the self-test, press **Default Setup**. The Channels panel should show **10.0:1** for both channels. If not, tell your TA.

### Part 4: periodic waves (steps 1–9)
1. Generator: **1 Vpp sine at 990 Hz** into the **channel 2** probe. Press **Auto-Scale**.
2. Read V/div at the top left; count boxes for **Vpp** (**expect ≈ 2 Vpp**, see Part 1).
3. Turn the small channel-2 knob (position): the trace and its ground marker move. Turn the big one (scale): V/div changes.
4. Read time/div at the top right; count boxes for the **period** (≈ 1.01 ms).
5. Horizontal big knob = time/div; small knob moves the trigger point (solid orange triangle) relative to the time reference (hollow triangle).

### Part 5: dual trace and triggering
1. Channel 1 probe on **Demo 2 / probe comp**, ground clip on the ground terminal. **Auto-Scale.**
2. Sweep the generator between **990 and 1110 Hz**. One trace is still, the other drifts; tune until it drifts slowly.
3. **Trigger** → **Source** → turn the multi-purpose knob to channel 2. Now the other wave stands still.
4. Turn the **Level** knob and watch the "T" marker. Push it above the wave: in **Auto** the scope draws anyway (*Auto?* blinking, picture jumps). Switch **Mode/Coupling → Normal**: the screen freezes (*Trig'd?*). Bring the level back.
5. **Slope**: switch rising/falling and watch the picture flip around the trigger point.

### Part 6: screenshots
Desktop **Take Screenshot** icon → **Take Screenshot** → choose a name → Save. Use this for every scope image from now on (no phone photos).

## What you should observe, and why

| Observation | Why it happens |
|---|---|
| DMM shows 2.0 V for a 1.0 V setting (open output) | Generator assumes a 50 Ω load and doubles its internal source; with 10 MΩ nothing is lost inside. |
| ≈ 1.0 V with 51 Ω | Nearly matched, so the 2 V splits in half. |
| Sine 0.354 Vrms, square 0.500 Vrms for the same 1 Vpp | RMS depends on shape: a square spends all its time at the peak. |
| Scope shows 2 Vpp for "1 Vpp" | The probe is 10 MΩ, again far from 50 Ω. |
| One wave still, the other drifting | The scope aligns every sweep to the trigger channel. The other wave's frequency differs slightly, so it starts at a new phase on each sweep: it drifts at the difference frequency. |
| Level above the wave: jumping picture (Auto) or frozen picture (Normal) | No trigger events. Auto gives up and free-runs; Normal waits. |
| Power wave (pre-lab) is all positive at twice the frequency | p = v·i and v, i have the same sign in a resistor; squaring a sine doubles its frequency. |

## Formula sheet (what, when, example)

### Generator output (50 Ω source)

```
Vout = Vs · RL / (50 + RL)
```

**Use it when:** Predicting the real voltage the generator delivers into any load (Question 3).

- `Vs`: hidden internal source = 2 × the displayed setting
- `RL`: your load resistance

**Example:** Vs = 2 Vrms, RL = 50.9 Ω → 2 × 50.9/100.9 = 1.009 Vrms.

### Matched vs open load

```
RL = 50 Ω → Vout = Vs/2 (display correct)
RL → ∞ → Vout ≈ Vs (2 × display)
```

**Use it when:** Explaining why a DMM or scope (10 MΩ) shows double the setting (Questions 1 and 5).

**Example:** Set 1 Vpp, scope probe → 2 Vpp on screen.

### Peak and peak-to-peak

```
Vpp = 2 Vp  (zero-offset waves)
```

**Use it when:** Converting between the generator’s amplitude units and what you read on the screen.

**Example:** 1 Vpp → Vp = 0.5 V.

### RMS definition

```
Vrms = √⟨V²(t)⟩
```

**Use it when:** Understanding what the DMM’s AC reading means: the DC voltage with the same heating effect.

**Example:** Square the wave, average it, take the root.

### RMS of a sine

```
Vrms = Vp / √2 = Vpp / (2√2)
```

**Use it when:** Any sine wave with zero offset.

**Example:** 1 Vpp sine → 0.5/1.414 = 0.354 Vrms.

### Duty cycle

```
D = tH / T
```

**Use it when:** Describing a rectangular wave: fraction of each period spent high.

**Example:** High 0.2 ms of a 1 ms period → D = 20%.

### RMS of a rectangular wave

```
Vrms = √(VH² D + VL² (1 − D))
```

**Use it when:** Square/pulse waves with any two levels (pre-lab).

**Example:** 50% square, ±0.5 V → √(0.25·0.5 + 0.25·0.5) = 0.500 Vrms.

### RMS of a rectangular wave with VL = 0

```
Vrms = VH √D
```

**Use it when:** Pulses that sit at 0 V when low.

**Example:** 5 V pulses at 20% → 5 × √0.2 = 2.236 Vrms.

### RMS of a triangle / ramp

```
Vrms = Vp / √3
```

**Use it when:** Triangle or ramp waves with zero offset, any symmetry.

**Example:** 1 Vpp triangle → 0.5/1.732 = 0.289 Vrms.

### Frequency and period

```
f = 1 / T
```

**Use it when:** Turning a period measured on the scope into frequency.

**Example:** Period 1.01 ms → 990 Hz.

### Reading the scope grid

```
V = divisions × V/div,   t = divisions × s/div
```

**Use it when:** Counting boxes for Vpp and period (8 divisions tall, 10 wide).

**Example:** 4 div × 500 mV/div = 2 Vpp.

### 10:1 probe

```
Vscope input = Vtip × 1M/(9M + 1M) = Vtip/10
```

**Use it when:** Understanding why the probe gives 10 MΩ input resistance and why the scope multiplies by 10.

**Example:** 2 Vpp at the tip → 0.2 Vpp at the BNC → displayed as 2 Vpp.

### Drift (beat) rate when not triggered on it

```
fdrift = |f2 − ftrigger|
```

**Use it when:** Question 6: how fast the un-triggered wave slides across the screen.

**Example:** Trigger on 1000 Hz, CH2 at 1001 Hz → drifts 1 cycle per second.

### Instantaneous power

```
p(t) = v(t) · i(t),   Pavg = Vrms² / R
```

**Use it when:** Pre-lab .tran plot of power in a resistor: always ≥ 0, at twice the signal frequency.

**Example:** 0.5 V peak across 1 kΩ: Ppeak = 250 µW, Pavg = 125 µW.

### Percent error

```
(measured − expected) / expected × 100%
```

**Use it when:** Questions 1, 2 and 4.

**Example:** DMM 2.003 V vs display 1.000 V → +100.3%.


## Report guide

1. % error, generator display vs DMM (step 4) and explanation (50 Ω assumption).
2. % error with the 51 Ω load (step 6).
3. V_out = 2 V × R_L/(50 + R_L) with your measured R_L.
4. % error between pre-lab RMS predictions and your sine/square measurements.
5. Is the step-4 scope Vpp equal to 1 Vpp? Why?
6. Why does one wave move while the other is still?
7. Paste the oscilloscope screenshot from the capture tool.

---
*Made for ESE 123 students by a TA. Simulated values are ideal; your readings will differ slightly.*
