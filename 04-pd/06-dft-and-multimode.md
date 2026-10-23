# PD: DFT and Multi-Mode
Status: draft
Priority: med
JD line: DFT insertion; multi-mode timing constraints

---

## Core idea
- DFT adds structures that make the chip testable after manufacturing: scan chains,
  BIST, JTAG.

---

## Scan basics
- Scan flop = flop with a mux on D (functional vs scan input), selected by scan enable.
- Scan chains link flops into shift registers. Shift in a pattern, capture, shift out.
- ATPG generates patterns for fault models (stuck-at, transition delay).
- MBIST tests memories. JTAG gives board-level access.

---

## Timing effects
- Mux on D adds delay to functional setup paths.
- Scan-shift paths are short and hold-critical (flop to next flop, no logic).
- Scan clock may differ from functional; lockup latches on clock-domain boundaries.
- Separate modes and constraints: shift, capture, functional.

---

## Q&A

### Q: What does scan insertion do to timing?
- Adds the mux delay to D paths and creates many short hold-critical shift paths.

### Q: Why do scan chains get reordered in PD?
- Place-aware reordering shortens scan wiring and reduces congestion.

### Q: Does scan affect LEC?
- Yes, scan enable must be constrained so LEC compares functional behavior.

### Q: Stuck-at vs transition fault?
- Stuck-at: node fixed at 0/1. Transition: node too slow to switch (tests timing).

---

## Drill
- Draw a scan flop and a 3-flop scan chain. Mark where hold risk is highest.
