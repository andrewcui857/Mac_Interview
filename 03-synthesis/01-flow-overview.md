# Synthesis: Flow Overview
Status: draft
Priority: high
JD line: front-end design synthesis; timing clean, logically equivalent netlist

---

## Core idea
- Synthesis turns RTL plus constraints plus a cell library into a gate-level netlist
  that meets timing, area and power goals.
- Inputs: RTL, SDC constraints, standard cell library (.lib), sometimes physical
  info (floorplan, DEF) for physical-aware synthesis.
- Outputs: netlist, updated SDC, reports (timing, area, power, QoR), then LEC vs RTL.

---

## Flow steps
1. Read and elaborate RTL (parameters resolved, hierarchy built).
2. Read constraints (clocks, IO delays, exceptions, operating conditions).
3. Generic mapping: RTL to technology-independent logic.
4. Technology mapping: pick library cells.
5. Optimization: restructure logic, size cells, buffer, swap Vt, recover area.
6. DFT insertion (scan) often here, then incremental compile.
7. Write netlist, SDC, reports. Run LEC. Hand off to PD.

---

## Q&A

### Q: What does a synthesis tool optimize?
- A cost function over timing (WNS, TNS), area, and power, subject to design rules
  (max transition, max capacitance, max fanout).
- Timing usually has priority, then area and power recovery on paths with slack.

### Q: Why can the same RTL give different results?
- Different constraints (clock period, uncertainty, IO budgets), different libraries
  or Vt mixes, different effort settings, and different hierarchy handling
  (flatten vs keep) all change the result.

### Q: What is the difference between logic synthesis and physical synthesis?
- Logic synthesis uses a wire load model or estimates. Physical (physical-aware)
  synthesis uses placement, so wire delay is closer to post-route reality.
- Fewer surprises at PD: better correlation of timing and congestion.

### Q: What is in the handoff to physical design?
- Netlist, SDC (all modes), scan chain info (DEF/ SCANDEF), reports, LEC result
  showing the netlist is equivalent to the RTL.

### Q: Which tools do you know?
- Commercial: Synopsys Design Compiler, Cadence Genus. Open source: Yosys.
- [VERIFY] Say exactly which you have run. If none, say you understand the flow and
  have used Xcelium for simulation.

---

## Drill
- Draw the flow on paper with inputs and outputs at every step, in under 2 minutes.
