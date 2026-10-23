# STA: Skew, Uncertainty, OCV
Status: draft
Priority: high

---

## Core idea
- Real silicon varies. STA adds pessimism margins so that signoff covers it.

---

## Terms
- Clock skew: latency difference between launch and capture flops.
- Clock uncertainty: jitter plus margin; applied to setup (and separately to hold).
- OCV (on-chip variation): launch and capture paths see different delay on the same
  die. Applied as derates: data and launch clock slow, capture clock fast for setup.
- AOCV/POCV: derate depends on path depth or statistical distribution, less pessimistic
  than a flat derate.
- CRPR (common path pessimism removal): the shared part of the launch and capture
  clock paths cannot be both slow and fast, so remove that pessimism.
- Useful skew: intentionally skew clocks to borrow time from a path with slack.

---

## Q&A

### Q: Why derate launch and capture differently?
- To model worst-case variation: for setup, the launch path is slow and the capture
  path is fast, giving the least margin.

### Q: What is CRPR and why does it matter?
- Without it, the common clock buffers are counted as both slow and fast. That is
  physically impossible and wastes margin, so tools remove it.

### Q: Clock uncertainty before and after CTS?
- Before CTS (ideal clocks): larger, includes expected skew. After CTS (propagated):
  smaller, mostly jitter plus margin.

### Q: Cost of useful skew?
- It helps one path and hurts neighbors. Hold must be rechecked. Used carefully.

---

## Drill
- Explain CRPR with a diagram: two flops, shared clock buffer, then branches.
