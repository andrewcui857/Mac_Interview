# Synthesis: PPA Tradeoffs
Status: draft
Priority: high
JD line: aggressive power, area, timing goals

---

## Core idea
- Power, performance, area pull against each other. Speed costs area and power.
  Lower power usually costs speed or area. Know what each knob buys and costs.

---

## Knob list (benefit, cost)
- Upsize a cell: faster, more area, more power, more input cap on the previous stage.
- Low-Vt swap: faster, much more leakage.
- High-Vt swap: lower leakage, slower. Use on paths with positive slack.
- Buffer insertion: fixes high fanout or long wire, adds area and some delay.
- Logic duplication: lowers fanout and depth, adds area and power.
- Pipelining (architectural): higher frequency, more flops, more latency. Not an
  equivalent transform.
- Clock gating: saves dynamic power, adds an enable timing check and a gate cell.
- Resource sharing: saves area, adds muxes, may lengthen the critical path.

---

## Q&A

### Q: Timing is failing and area is fine. What do you try first?
- Look at the critical path: logic depth, fanout, or wire? Then upsize or Vt-swap on
  that path, restructure, buffer. Larger changes (retime, duplicate) next.

### Q: Timing is met with lots of slack and power is over budget. Now what?
- Area and power recovery: downsize, High-Vt swap, clock gating, operand isolation,
  multibit flops.

### Q: Why is the critical path hard to improve at the end?
- Fixing one path moves the wall to the next. Wall of slack: many paths near zero.

### Q: How do you compare two synthesis runs?
- WNS, TNS, number of violating endpoints, total area, leakage, dynamic power at the
  same activity, and runtime. Same constraints and library for both.

---

## Drill
- Pick a MAC datapath. List 3 timing fixes and the area/power cost of each.
