# DV: Testbench Architecture
Status: draft
Priority: med
JD line: simulation and debugging tools

---

## Core idea
- A self-checking testbench has stimulus, a driver, a monitor, a scoreboard with a
  reference model, coverage, and assertions.

---

## Q&A

### Q: Roles of each component?
- Stimulus/test: what to apply. Driver: turns transactions into pin wiggles. Monitor:
  observes pins and rebuilds transactions. Scoreboard: compares DUT behavior to the
  reference model. Coverage: shows what has been exercised.

### Q: Directed vs constrained-random?
- Directed: targeted corner cases, easy to debug. Random: finds unexpected bugs.
  Use both; random with constraints keeps stimulus legal.

### Q: Why can the testbench itself be wrong?
- Monitor mis-sampling, reference model mismatch, scoreboard bug. Always check which
  of DUT, model, or testbench is wrong before changing the DUT.

### Q: What goes in a testplan?
- Features, tests for each, checks, coverage goals, and pass/fail criteria.

---

## Drill
- Draw the testbench for an RV32I CPU: what does the driver do? what does the monitor
  watch (instruction memory, data memory, halt)?
