# Handover — End of Day 2 → Start of Day 3  *(updated)*

> This supersedes the earlier Day 2 → Day 3 handover. Change since then: **all Day 2 deliverables are now committed and pushed** (commit `da1c3e2`), and a **Day 2 lab record** was produced to stand in for scope screenshots the student chose not to keep.

**Student:** Optimus — Year 1 → Year 2 MEng Electronic & Electrical Engineering, University of Southampton (programme H602).
**Project:** 71-day summer self-study (schedule_v7.tex, in project files). GitHub: `JivPrime`, repo `JivPrime/summer-2026`.
**Handover updated:** 17 Jun 2026.
**Position:** **Day 2 is COMPLETE.** Next session is **Day 3** = schedule box *"Mon 15 Jun [CATCH-UP] — Capacitors + RC Time Constants"*.

> **Day-numbering note:** `schedule_v7.tex` labels days by calendar date, not "Day N". The student counts study days sequentially by content. Day 2 = the Sun 14 Jun box; Day 3 = the Mon 15 Jun box. Use **section numbers as authoritative** and verify any reading length against the ToC `.md` files — schedule page numbers were written from memory.

---

## 0. Day 2 status — COMPLETE & committed (nothing blocking Day 3)

- ✅ **All Day 2 deliverables committed and pushed** to `JivPrime/summer-2026`, commit **`da1c3e2`** (`4d6aba2..da1c3e2`, master): 4 files —
  - `EOD_Thevenin_Loading.pdf` / `.tex` (the EOD write-up)
  - `Day2_Lab_Record.pdf` / `.tex` (expected instrument views + key notes)
- **Scope screenshots:** the student took none and chose not to keep any. `Day2_Lab_Record.pdf` captures the **expected** scope/DMM views per lab instead, so that gap is covered.
- **Physical logbook entries** (*Illumination* / *Reference*) are optional and the student's call — not blocking.
- **Net:** Day 2 is fully wrapped; Day 3 can start clean.

---

## 1. What Day 2 covered — all completed

**Theory (LAoE worked examples + loading):**
- Worked **LAoE §1W.4–1W.6**: three Thévenin reductions; finding **R_in / R_out** by "assuming the other side" (short the source for R_out, open the load for R_in); loading and the **10× rule**.
- **Corrected the student's 1W.6 self-test:** their method (meter in parallel with the bottom resistor) was right; the only error was the VOM input resistance — correct is **10,000 Ω/V × 10 V range = 100 kΩ → 6.7 V** (they had used 200 kΩ). Their scope part (1 MΩ → 9.5 V) was already right.

**Four bench labs (all built and measured):**
1. **Make:E Expt 3 Part A (KVL):** 9 V + 470 Ω + red LED. V_LED ≈ 2 V, V_s ≈ 8.99 V, V_R ≈ 6.8 V; KVL confirmed.
2. **Make:E Expt 3 Part B (Ohm's law via current sweep):** LED removed, resistor only; DMM in mA **in series**; 1k/1.5k/2.2k/3k → ≈ 9/6/4.1/3 mA; V = I·R ≈ 9 V. (3.3 kΩ substituted by the student's 3 kΩ.)
3. **Divider loading lab:** 10 k / 10 k from 5 V → **V_Th = 2.5 V, R_Th = 5 kΩ**. Loaded mid-point: 10 k → 1.67 V, 1 k → 0.42 V, 100 Ω → 49 mV.
4. **Pot-controlled LED:** 10 k pot ends to 5 V / GND, wiper → 470 Ω → LED → GND. Off below ~2 V at the wiper, full at ~5 V (I ≈ 6.4 mA).

**Deliverables produced (both committed — see §0):**
- `EOD_Thevenin_Loading.{pdf,tex}` — Thévenin recipe box, worked divider→Thévenin example with a circuitikz diagram, condensed lab takeaways.
- `Day2_Lab_Record.{pdf,tex}` — per-lab **expected scope traces** (Labs 1 & 4, which used the scope) and the **DMM graphs** the readings produce (Labs 2 & 3), plus a key-notes box. Built with pdflatex (3 passes), all plots rasterised and visually checked.

---

## 2. Big conceptual win — RESOLVED (do not re-litigate in Day 3)

The student fully worked through how a potentiometer behaves. Treat all of this as solid:

- **The wiper (middle pin) is a real node, not a component.** A pot is **one track split by the wiper into R_top + R_bot** (always summing to 10 k). The wiper voltage is the divider output.
- **The 470 Ω + LED is a *separate branch*** hanging off the wiper node (not inside the pot).
- **The clincher that finally landed:** *parallel = same voltage, always; the voltage "drop"/droop is a **series** effect across R_top.* With R_top = 0 there is no series resistance to drop voltage, so the wiper sits at the full 5 V; R_bot and the LED branch (parallel below the wiper) both see 5 V at different currents. The lab's loading droop happened because **R_top was 10 k**, not 0.
- **Scope grounding:** all probe ground clips are internally common and earth-tied → **tie every ground clip to one circuit-ground node**, or two clips short two points together (this had shorted the LED earlier).
- **LED behaviour:** clamps voltage at ≈ 2 V but does **not** limit current; **current (heat) destroys it**; the series resistor limits current — I = (V_wiper − 2)/470 (can't use V/(R + R_LED): the LED is nonlinear).
- **Bonus tangent covered:** you *can* make a "pot" from fixed resistors — a **stepped attenuator** (resistor string + switch/jumper picking the tap). Stepped, not smooth; more resistors → finer steps; this is what hi-fi stepped volume controls and digital pots do.

---

## 3. Day 3 plan — Capacitors + RC Time Constants
*(verified against schedule_v7.tex; section numbers authoritative, page numbers approximate)*

**AM — reading:**
- Make:E **Experiment 5** ("Let's Make a Battery").
- AoE Ch 1 **§1.4–1.4.2** (capacitors, RC circuits).
- LAoE **§2N.1–2N.4** (RC and capacitor circuits).
- Also work LAoE **§2W.1–2W.2** (RC filters + the RC step response, worked with numbers) — cements the bench RC charging and gives the step-response maths. *(Frequency-domain filter view comes later: AoE §1.7, Mon 6 Jul.)*
- **Key equations:** τ = RC and v_C(t) = V_s(1 − e^(−t/τ)).

**PM — labs:**
- **Make:E Expt 5** (lemon/potato cell, for fun): expect ~0.8–1.0 V per cell, < 1 mA short-circuit.
- **RC charging, value 1:** 10 kΩ + 100 µF driven by the **DHO924S built-in AWG** (square wave). Scope input on CH1, cap voltage on CH2. Measure time to **63 %** = τ; compare to τ = RC = **1 s**.
- **RC charging, value 2:** 1 kΩ + 1 µF, τ = **1 ms**. Use scope **cursors** for precise measurement.

**EOD (Day 3):** Scope screenshots of both RC charging curves; measured vs calculated τ.

---

## 4. Watch-outs for Day 3

- **⚠ Square-wave frequency vs τ (check at the bench).** The schedule says "10 k + 100 µF, 1 Hz square." With τ = 1 s, a 1 Hz square gives only a **0.5 s half-period = 0.5 τ**, so the cap reaches just v_C = 1 − e^(−0.5) ≈ **39 %** before the source flips — it never reaches 63 % within a half-cycle.
  - **Cleanest fix (keeps the round τ = 1 s):** lower the AWG square to **≈ 0.1 Hz** (half-period 5 s ≈ 5τ) so the curve charges fully and the 63 % point is clearly visible. Confirm the DHO924S source reaches that low (it should go well below 0.1 Hz).
  - **Alternative (keeps 1 Hz):** shorten τ to ≤ 0.1 s — e.g. 1 kΩ + 100 µF (τ = 0.1 s) charges fully inside a 0.5 s half-period — but then compare against τ = 0.1 s, not 1 s.
  - Same logic for value 2: 1 kΩ + 1 µF (τ = 1 ms) at 500 Hz gives a 1 ms half-period = exactly 1 τ (hits 63 % right at the flip). For a fuller curve drop to ~100 Hz.
- **New schematic convention to introduce:** the **capacitor symbol** (two parallel plates; polarised electrolytics have a marked + terminal / curved plate = negative). Use the project's Schematic Conventions card.
- **Cap kit:** electrolytics (10/47/100 µF) from the BOJACK electrolytic kit; for any AC/filter work use **X7R or C0G/NP0** ceramics only (Y5V/Z5U banned).

---

## 5. Carried-forward pending items (cross-session — still open)

- **AoE condensation corrections** — apply when `AoE_1_2_2_to_1_3_Condensation.tex` source is next available:
  1. Q5 self-test answer is wrong (states ≈ 2.4 V; **correct = 20/13 ≈ 1.54 V**).
  2. Zener symbol malformed in the §1.2.6 regulator figure (cathode bar at wrong end). Correct: **cathode bar at the +/output end, triangle pointing up toward it.** A correct circuitikz version of the §1.2.7 alarm circuit exists as `alarm.tex` / `alarm.pdf`.
- **Untaken offers from Day 2** (optional): exact DHO924S Math `A−B` button steps; exact circuitikz oscilloscope-shape syntax.

---

## 6. Standing context (unchanged — full detail in project files + memory)

- **Teaching style:** build from basics, plain-language intuition **before** any formula, **one idea at a time**; if the student is lost, go **simpler not bigger** (remove layers, ask which exact sentence is unclear); park side-topics; lead with inline diagrams.
- **Formatting:** bullets + **bold** key terms, concise, British English, **j** (not i) for the imaginary unit, voltage reduction called **"drop"** (not "sag"). Default new documents to **PDF**; **handovers are markdown.**
- **Bench:** Rigol DHO924S scope (1 MΩ input, built-in AWG), Siglent SPD3303X PSU, DSLogic U2Pro16, Extech EX530A + UNI-T UT58C DMMs, Yihua 862BD+, ELEGOO kit, BOJACK 1 % metal-film resistor kit, NUCLEO-F411RE. Devuan Linux (KDE), repo cloned at `~/summer-2026` on host `280-test2` (user `test`). Bench LAN: scope 10.0.0.2, PSU 10.0.0.3.
- **Note-taking:** *Illumination* (experiment log), *Reference* (constants/equations/procedures), Joplin "Summer Experience" for ahead-of-schedule notes.
- **Git workflow confirmed working:** files committed loose as `.pdf` + `.tex` (not zipped); `gh` authenticated; push to `origin master`.

---

## 7. Ready-to-paste opening prompt for Day 3

> **Day 3 (Mon 15 Jun content) — Capacitors + RC Time Constants.**
>
> **AM block:** Make:E Experiment 5 ("Let's Make a Battery"); AoE Ch 1 §1.4–1.4.2 (capacitors, RC circuits); LAoE §2N.1–2N.4 (RC and capacitor circuits); LAoE §2W.1–2W.2 (RC filters + RC step response, worked with numbers). Key equations: τ = RC, v_C(t) = V_s(1 − e^(−t/τ)).
>
> **PM block:** Make:E Expt 5 (lemon/potato cell). Then RC charging: 10 kΩ + 100 µF, and 1 kΩ + 1 µF, driven by the DHO924S AWG; scope input (CH1) and cap voltage (CH2); measure time to 63 % = τ and compare to RC; use cursors. **Watch the square-wave frequency vs τ — see §4 of the handover.**
>
> **EOD:** scope screenshots of both RC charging curves; measured vs calculated τ.
>
> *(then append your standard teaching-style instruction block)*
