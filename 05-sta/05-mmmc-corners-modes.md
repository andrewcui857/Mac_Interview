# STA: Multi-Mode Multi-Corner (MMMC)
Status: draft
Priority: med
JD line: multi-mode timing constraints

---

## Core idea
- A chip must meet timing in every operating mode at every PVT corner it ships in.

---

## Terms
- Mode: functional, scan shift, scan capture, MBIST, low power, test. Each has its own
  clocks and exceptions (own SDC).
- Corner: process (slow, typical, fast), voltage, temperature.
- Setup is critical at slow corner (slow process, low V, and high or low T depending
  on node). Hold is critical at fast corner.
- Scenario = mode plus corner.
- Temperature inversion: at advanced nodes low voltage, cold can be slower.

---

## Q&A

### Q: Why does scan mode need its own constraints?
- Different clock (test clock), shift paths that are not functional, and different
  frequency. Scan shift has many hold-critical short paths.

### Q: Why check hold at the fast corner?
- Min delay is smallest there, so the data race is worst.

### Q: How many scenarios is that?
- modes x corners. Tools prune dominant scenarios to save runtime.

### Q: How does a power mode add scenarios?
- Different supply voltage per domain and shut-off domains add corners and constraints.

---

## Drill
- List the scenarios for a block with functional + scan-shift modes and slow + fast
  corners. Mark which checks matter in each.
