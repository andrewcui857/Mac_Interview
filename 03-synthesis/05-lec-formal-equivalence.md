# Synthesis: Formal Equivalence (LEC)
Status: draft
Priority: high
JD line: formal verification; logically equivalent netlists

---

## Core idea
- LEC proves two designs (golden RTL vs revised netlist, or netlist vs netlist) have
  the same function without simulating vectors.
- Method: map compare points (flops, ports, black boxes), then prove each logic cone
  between them is equal (SAT/BDD based).
- Tools: Cadence Conformal LEC, Synopsys Formality.

---

## When to rerun
- After synthesis, after DFT insertion, after each ECO, after PD netlist changes
  (buffering, sizing, CTS), and for the final signoff netlist.

---

## Q&A

### Q: What is a compare point?
- Matched state elements, primary outputs, and black box pins. The tool proves the
  logic cone feeding each point is equivalent.

### Q: Why does LEC fail?
- Unmapped points (names/hierarchy changed), retiming without mapping info, clock
  gating differences, scan logic not constrained off, constant/tie differences,
  black boxes or memories modeled differently, X handling differences, real bugs.

### Q: Scan insertion adds muxes. Why isn't LEC broken?
- Set scan enable to its functional constant (0) in LEC so the scan path is off.

### Q: LEC vs simulation?
- LEC is exhaustive for the compared logic but does not tell you the RTL itself is
  correct. Simulation checks intent. They are complementary.

### Q: What does a non-equivalent point tell you?
- A real function change or a modeling mismatch. Debug by looking at the failing
  cone, a counterexample input, and which cell or transform changed it.

---

## Drill
- State three transforms that LEC will prove equivalent and one it will not.
