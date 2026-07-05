# Day 3 — RC Time Constants: Lab Record & Reference

**Topic:** Capacitors + RC Time Constants (Day 3 of summer self-study)
**Date:** ______________
**Kit:** Rigol DHO924S oscilloscope (+ built-in AFG), Siglent SPD3303X PSU, Extech EX530A DMM, breadboard, BOJACK 1 % metal-film resistors, electrolytic capacitors.
**Feeds:** ELEC2310 (Signal Processing), ELEC2320 (Control), ELEC2322 (Electronic & Computer Systems).

---

## Part 1 — Illumination (the experiment)

### Aim
- Predict the time constant **τ = RC** for two RC circuits, measure it on the bench, and confirm **τ = RC**.
- Method throughout: **predict first, then measure.**

### Circuit 1 — Slow RC (watched by eye)
- **Components:** R = 10 kΩ (metal-film 1 %), C = 100 µF (electrolytic — polarised, **+** to the resistor/supply side).
- **Source:** PSU at **5.00 V DC**, current limit 50 mA, switched on once.
- **Measured with:** DMM across the capacitor + stopwatch.
- **Predicted:** τ = RC = 10 kΩ × 100 µF = **1 s**.

### Circuit 2 — Fast RC (on the scope)
- **Components:** R = 1 kΩ (metal-film 1 %), C = 1 µF.
- **Source:** AFG **square wave, 0–5 V, 100 Hz** (half-period = 5 ms = 5τ, so the cap fully charges and discharges each half-cycle).
- **Measured with:** scope CH1 on the capacitor node, cursors at the 63 % point.
- **Predicted:** τ = RC = 1 kΩ × 1 µF = **1 ms**.

### Results — predicted vs measured

| Circuit | R | C | Calculated τ = RC | Measured τ | Diff | Verdict |
|---|---|---|---|---|---|---|
| **Slow** | 10 kΩ | 100 µF | 1 s | ~1.15 s | +15 % | **Pass** |
| **Fast** | 1 kΩ | 1 µF | 1 ms | ~1 ms | ~0 % | **Pass** |

- **Slow circuit raw readings:** V = 2.91 V at t = 1 s (predicted 3.16 V); V = 4.91 V at t = 5 s (predicted 4.97 V). Back-calculating from the 1 s point gives **τ ≈ 1.15 s**.

### Conclusions
- Both circuits **confirm τ = RC.**
- The slow circuit's **+15 %** is fully explained by the **electrolytic's ±20 % tolerance** (a real value of ~115 µF gives τ = 1.15 s exactly) plus stopwatch reaction time (~±0.3 s on a 1 s τ) — **not a physics error**.
- Resistors are ±1 %, so the **capacitor dominates the uncertainty**.

---

## Part 2 — Reference (keep permanently)

### Core equations
- **Time constant:** τ = RC (seconds, for R in Ω, C in F). Shortcuts: MΩ × µF → s; kΩ × µF → ms.
- **Charging** (toward final value V_f): **V(t) = V_f (1 − e^(−t/τ))**.
- **Discharging** (from start V₀): **V(t) = V₀ e^(−t/τ)**.
- **Static / dynamic capacitor laws:** Q = CV; I = C·dV/dt; energy U = ½CV².
- **Time to reach a voltage (charging):** t = RC · ln( V_f / (V_f − V) ).
- **Half-way point:** t = RC · ln 2 ≈ **0.69 RC**.
- **Rise time (10 % → 90 %):** t_r = RC · ln 9 ≈ **2.2 RC**.

### The two numbers to memorise (+ full table)

| Elapsed time | 0 | 1τ | 2τ | 3τ | 4τ | 5τ |
|---|---|---|---|---|---|---|
| Charging — % of V_f reached | 0 % | **63 %** | 86 % | 95 % | 98 % | **99 %** |
| Discharging — % of V₀ remaining | 100 % | **37 %** | 14 % | 5 % | 2 % | **1 %** |

- **63 % of the way in 1τ; essentially full (~99 %) by 5τ.**
- Charging % reached + discharging % remaining = 100 at every instant (they are mirror images).

### Measuring τ on a scope — two valid methods
- **Method 1 (fix time, read voltage):** set ΔX = 1τ, read ΔY, check it is 63 % of the swing.
- **Method 2 (fix voltage, read time):** set ΔY = 63 % of the swing, read **ΔX = τ directly**.
- **Measure at the 63 % / 1τ point** (steep, sensitive) — **not at 5τ** (nearly flat, tiny errors swing the result).
- Reference the **actual top and bottom of the trace**, not assumed 0 V / 5 V: 63 % level = **bottom + 0.63 × (top − bottom)**.

### Bench gotchas (learned the hard way)
- **AFG load = High-Z.** The AFG output has 50 Ω source impedance; on the "50 Ω" setting driving a high-impedance RC, the actual output is **doubled** (0–5 V becomes 0–10 V). Set load to **High-Z** (or halve the amplitude).
- **Probe ×10 / ×1 must match.** The CH1 "Probe" setting must equal the physical probe's attenuation, or every reading is off by 10×. A ×10 probe used to **drive** the AFG signal adds a **9 MΩ** series resistor and kills it — use **×1** (or a plain lead) for the drive line.
- **Common ground.** AFG shield, scope probe ground clip, and the circuit ground must all sit on **one rail** — a floating ground gives a flat/garbage trace.
- **Square-wave frequency.** Use **~100 Hz** for the 1 ms circuit (half-period 5 ms = 5τ → full curve). Avoid 500 Hz (chops off at exactly 1τ) and 1 Hz (far too slow).
- **Trigger status.** **"AUTO"** = free-running, usually no signal; **"T'D"** = properly triggered. If a working trace suddenly goes flat, suspect a **loose wire**, not a setting.
- **Reseat breadboard wires.** A half-seated jumper reads as an open circuit.

### Where RC shows up next
- **Simplest low-pass filter / averager** → Signal Processing (ELEC2310).
- **First-order lag, the time constant τ** → Control (ELEC2320).
- **RC timing, switch debouncing, logic delays** → Electronic & Computer Systems (ELEC2322).
