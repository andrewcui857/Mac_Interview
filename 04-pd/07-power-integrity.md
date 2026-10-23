# PD: Power Integrity (IR Drop and EM)
Status: draft
Priority: med

---

## Core idea
- The grid has resistance, so cells far from supply see lower voltage (IR drop) and
  switch slower. High current density wears out wires (EM).

---

## Q&A

### Q: Static vs dynamic IR drop?
- Static: average current times resistance. Dynamic: worst-case simultaneous switching,
  including inductance and decap effects.

### Q: Fixes for an IR hotspot?
- Add straps/vias, widen grid, add decap, spread high-activity cells, reduce cell
  density, stagger clock gating, add supply pins.

### Q: Why does IR drop hurt timing?
- Lower local V slows cells (delay grows steeply at low V), eating setup slack.

### Q: Why GPUs care?
- Arrays of high-activity datapaths create concentrated current demand.

---

## Drill
- IR hotspot appears near a macro. List causes and fixes.
