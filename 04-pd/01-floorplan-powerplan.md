# PD: Floorplan and Power Plan
Status: draft
Priority: high
JD line: floorplanning

---

## Core idea
- Floorplan sets die/core size, block and macro placement, IO pin placement, and the
  power grid. Mistakes here are hard to repair later.

---

## Key terms
- Die vs core area. Utilization = cell area / core area (target depends on design,
  often leaves headroom for buffers, CTS, congestion).
- Aspect ratio of the core.
- Macros (SRAM, analog, hard IP): placed first, usually at edges, with halos (keepout).
- IO pins: placed to shorten critical interfaces.
- Power grid: straps and rails, tap cells, endcaps.

---

## Q&A

### Q: How do you place macros?
- Near the logic that talks to them, at the periphery to keep a contiguous core, with
  channels for routing, respecting halos, orientation aligned to pins.

### Q: What goes wrong with high utilization?
- Congestion, no room for timing buffers and hold fixes, routing detours, worse timing.

### Q: Why are pin placement and floorplan connected to timing?
- Long wires between blocks and pins add delay. Pin position follows dataflow.

### Q: What is a halo or blockage?
- Keepout around macros or regions so cells and routes do not crowd critical areas.

### Q: What is in a power plan?
- Rings, straps (upper metals), rails (lower metals), vias, tap cells for latch-up
  protection, decap cells. Sized to meet IR drop and EM limits.

---

## Drill
- Sketch a floorplan with 2 SRAMs, a datapath and a control block. Justify placement.
