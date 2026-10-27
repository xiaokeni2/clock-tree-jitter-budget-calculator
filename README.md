# Clock Tree Jitter Budget Calculator

A free, single-file web tool for timing and RF engineers that computes the **total RMS phase jitter of a cascaded clock tree** — a source oscillator plus up to 8 stages of clock distribution (fanout buffers, PLL buffers, retimers, muxes) — together with a per-stage contribution chart and the remaining **jitter budget margin**.

## Online use

Open the tool directly in your browser (no install, no dependencies, all math runs client-side):

**https://xiaokeni2.github.io/clock-tree-jitter-budget-calculator/**

## What it does

- Enter the source RMS jitter (ps) and the additive (residual) RMS jitter of up to 8 cascaded stages.
- Device-class presets fill typical additive-jitter values (fanout buffer, retimer/jitter cleaner, PLL buffer, clock mux, oscillator output, FPGA PLL) — clearly marked as approximate; always verify with the datasheet.
- Live results: total RMS jitter, each stage's share of the jitter variance (bar chart), dominant contributor, and margin against your jitter budget with a 20–30 % reserve warning.
- Pure HTML/CSS/JS, dark engineering UI, mobile friendly.

## Formulas

```
J_total (RMS)   = √( J_src² + Σ J_add,i² )        (quadrature sum)
Contribution p_i = J_add,i² / J_total² × 100 %
Budget margin   = ( J_budget − J_total ) / J_budget × 100 %
```

Uncorrelated random jitter adds in quadrature (variances add). Deterministic jitter (spurs, periodic) is out of scope and must be handled separately. All inputs must share the same integration bandwidth (e.g. 12 kHz–20 MHz).

## Usage

1. Type the source oscillator RMS jitter (e.g. 0.5 ps for a high-grade OCXO output).
2. Add stages and pick a device class per stage, then fine-tune the residual jitter.
3. Optionally enter the system jitter budget (e.g. 1.0 ps) to see the remaining margin.

Example: J_src = 1.0 ps, two stages of 0.5 ps and 0.25 ps → J_total = √(1 + 0.25 + 0.0625) = 1.146 ps.

## Related

- [BRIDZA RF — oscillator & RF component selection](https://rf.bridza.com/)
- [Clock distribution & buffering selection guide](https://rf.bridza.com/resources/selection-guides/clock-distribution-buffering-guide.html)
- [Phase noise to jitter calculator](https://rf.bridza.com/resources/calculators/phase-noise-jitter-calculator.html)

---

More free RF/timing tools: [VSWR Calculator](https://xiaokeni2.github.io/vswr-return-loss-calculator/) · [Phase Noise–Jitter Converter](https://xiaokeni2.github.io/phase-noise-jitter-converter/) · [Holdover Time Calculator](https://xiaokeni2.github.io/holdover-time-calculator/) · [LEO Doppler Calculator](https://xiaokeni2.github.io/leo-doppler-calculator/)

© BRIDZA · MIT-style open code, free to use.
