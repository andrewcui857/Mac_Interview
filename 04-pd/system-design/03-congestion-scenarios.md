# PD System Design: Congestion Scenarios
Status: draft
Priority: med

---

## Scenarios

### Routing fails though utilization is 65 percent
- Local hotspot. Read congestion map, macro halos, high fanout nets. Lower local
  density, add padding, move macros.

### Hotspot at a wide crossbar
- RTL: reduce width, split into stages, localize. PD: spread cells, add blockages.

### Congestion near macros
- Widen channels, adjust halos, reorient macros, move pins.

### High fanout reset or enable net
- Buffer tree, duplicate drivers, pipeline the enable.

---

## Always end with
- Check timing impact of each fix and rerun placement.
