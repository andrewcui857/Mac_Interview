# PD System Design: Power Scenarios
Status: draft
Priority: med

---

## Scenarios

### Power is 20 percent over budget
- Clock gating first, then multi-Vt swaps, check activity, then consider power gating.

### IR hotspot near a macro
- Strengthen grid locally, add decap, spread active cells, check switching alignment.

### Leakage too high
- High-Vt on slack paths, power gate idle blocks, check temperature corner used.

### Power gating adds timing problems
- Isolation/level shifter delays, wake-up inrush. Budget them and stage the wake-up.

---

## Always end with
- State the tradeoff on timing, area, verification effort.
