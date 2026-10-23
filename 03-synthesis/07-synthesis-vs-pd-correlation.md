# Synthesis: Correlation with Physical Design
Status: draft
Priority: med
JD line: handoff to physical design; congestion awareness

---

## Core idea
- Synthesis sees estimated wires. PD sees real placement and routing. The gap is the
  main source of late surprises.

---

## Q&A

### Q: Why do timing results change after placement and routing?
- Real wire RC (long wires, vias, coupling), clock tree skew replacing ideal clocks,
  OCV derates, crosstalk, and congestion detours.

### Q: What RTL structures cause congestion?
- Wide muxes, big crossbars, high fanout nets, many-to-one buses, and logic that
  pulls far-apart registers together.

### Q: How do you make synthesis more predictable?
- Use physical-aware synthesis, realistic uncertainty and derates, correct IO budgets,
  and feedback loops: send PD timing/congestion results back as updated constraints.

### Q: What do you hand PD that reduces rework?
- Clean SDC, scan chain info, floorplan hints (macro grouping, hierarchy), reports of
  nearly-critical paths, and LEC-clean netlist.

---

## Drill
- Explain to a PD engineer in 60 seconds why a path that passed in synthesis fails
  after route and what you would change in RTL.
