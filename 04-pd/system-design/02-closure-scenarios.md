# PD System Design: Timing Closure Scenarios
Status: draft
Priority: high

---

## Scenarios (say answers aloud)

### Block closes, top fails
- Check top constraints, clock definitions, interface budgets, extraction differences,
  CDC. Rebudget or fix the interface.

### Hold violations appear after CTS
- Real skew now present. Insert delay cells on short paths, then recheck setup.

### Setup -50 ps after route on one path
- Find cause: wire, cell, or skew. Upsize/Vt swap, buffer, useful skew. Rerun STA and LEC.

### Closure oscillates (fix setup, hold breaks)
- Fix hold first with minimal delay, fix setup with sizing/restructure, run both
  corners together in the optimizer.

### Many paths near zero slack (wall)
- Look for a systemic cause: bad constraint, clock uncertainty too high, a common
  structure (e.g., all adders). Fix at the source.

---

## Always end with
- Rerun STA at all corners, rerun LEC, check area and power cost.
