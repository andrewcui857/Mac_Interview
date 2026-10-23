# PD: Placement and Congestion
Status: draft
Priority: high
JD line: placement, congestion

---

## Core idea
- Placement positions every standard cell. Goal: short wires on critical nets, no
  overlaps, legal rows, routable density.
- Steps: global placement, legalization, detailed placement, timing-driven
  optimization (sizing, buffering, cloning) with scan reordering.

---

## Congestion
- Congestion = more routing demand than supply in a region (GCell overflow).
- Causes: high pin density cells, wide muxes, crossbars, high fanout, macro channels
  too narrow, high local utilization.
- Fixes: lower density locally, cell padding, move or reorient macros, widen channels,
  placement blockages, RTL restructure (smaller muxes, pipeline wide buses), partition.

---

## Q&A

### Q: Global vs detailed placement?
- Global: approximate positions minimizing wire length with overlap allowed. Detailed
  and legalization: snap to rows and sites, remove overlaps.

### Q: What is timing-driven placement?
- Weights critical nets so their cells are closer, using current timing estimates.

### Q: How do you diagnose congestion?
- Congestion map, overflow report, find hotspots, trace nets and cells in the hotspot
  (often one wide mux or a high fanout net).

### Q: Why can routing fail with only 60 percent utilization?
- Local hotspots. Average utilization hides pin-dense regions and narrow macro channels.

### Q: What does an RTL designer change to reduce congestion?
- Reduce mux width, avoid huge shared buses, pipeline long routes, split high fanout.

---

## Drill
- A hotspot shows a 32:1 mux fed by many far-apart registers. List four fixes.
