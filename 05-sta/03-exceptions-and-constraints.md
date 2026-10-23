# STA: Exceptions and Constraint Pitfalls
Status: draft
Priority: high
JD line: multi-mode timing constraints

---

## Core idea
- Exceptions tell STA which paths are not single-cycle or not real. Wrong exceptions
  hide real bugs.

---

## Q&A

### Q: False path vs multicycle path?
- False: never timed (never functionally active, or async). Multicycle: timed, but
  with more than one cycle for the data to arrive.

### Q: Multicycle with a 2-cycle path. Exact constraints?
- `set_multicycle_path 2 -setup -from A -to B`
- `set_multicycle_path 1 -hold  -from A -to B`
- Without the hold line, the hold check moves with setup and becomes very strict.

### Q: Generated clocks?
- Clocks produced by dividers or muxes. Declared with `create_generated_clock` so STA
  knows the relationship (master, divide factor).

### Q: Clock groups?
- `set_clock_groups -asynchronous` says two clocks have no timing relation. Cleaner
  than a list of false paths, still needs CDC handled in design.

### Q: Case analysis?
- Fixes a mode pin to 0/1 so STA only times the active logic for that mode.

### Q: Common constraint mistakes?
- Missing clock on a port, input delay on a clock port, unconstrained endpoints,
  over-broad false paths, wrong multicycle hold, wrong generated clock source.

---

## Drill
- Given two async clocks and a config register read by both, state exactly what you
  would constrain and what must be done in RTL.
