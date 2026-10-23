# PD: Flow Overview (RTL to GDS)
Status: draft
Priority: high
JD line: basic physical design concepts

---

## Core idea
- PD turns a netlist into a manufacturable layout that still meets timing, power, and
  design rules. Each stage refines the previous one and feeds timing back.

---

## Flow in order (inputs, outputs)
1. Synthesis: RTL to netlist. See `02-synthesis/`.
2. Floorplan: die/core size, macros, IO pins, power grid. Output: floorplan DEF.
3. Placement: standard cells placed and legalized. Output: placed design.
4. CTS: build clock tree. Output: clocked design, then hold fixing.
5. Routing: global then detailed. Output: routed design, DRC clean.
6. Signoff: STA with extraction, IR/EM, DRC/LVS, antenna. Output: GDS.
7. ECO: late fixes, then rerun LEC and signoff.

---

## Q&A

### Q: What does each stage fix?
- Floorplan decides what can be close to what. Placement sets wire length. CTS makes
  clocks real. Routing makes wires real. Signoff proves it is correct.

### Q: Where is timing checked?
- At every stage with increasing accuracy: ideal clocks and estimated wires after
  placement, propagated clocks after CTS, extracted wires after route, full signoff.

### Q: Tools?
- Commercial: Cadence Innovus, Synopsys IC Compiler II / Fusion Compiler. Open source:
  OpenROAD (OpenROAD-flow-scripts).

### Q: What have I actually run? [VERIFY]
- List exactly which stages your SiliconJackets PD onboarding has covered so far
  (floorplan, place, CTS, route, reports) and which tool was used.

---

## Drill
- Draw the flow with one sentence per stage on what it fixes and what can go wrong.
