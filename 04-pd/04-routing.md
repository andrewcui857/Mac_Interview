# PD: Routing
Status: draft
Priority: med

---

## Core idea
- Global routing assigns nets to regions. Track assignment and detailed routing create
  actual wires and vias, DRC clean.

---

## Q&A

### Q: Why do routes affect timing so much at advanced nodes?
- Wire resistance dominates in thin lower metals. Long nets need buffering and upper
  metals (lower RC).

### Q: Crosstalk (signal integrity)?
- Coupling between neighbors causes delta delay (timing) and glitches (noise). Fix by
  spacing, shielding, buffering, or layer change.

### Q: Antenna violations?
- Charge accumulation on long metal during fabrication can damage gates. Fix with
  diodes, jumper to higher layer.

### Q: Electromigration?
- Current density wear-out in wires and vias. Fix by widening wires, adding vias.

### Q: DRC fixes?
- Detailed route iterates to clear spacing, short, min-area, via rules. Remaining
  violations are fixed in an ECO route.

---

## Drill
- Timing fails by 30 ps after route on a long net. List three fixes.
