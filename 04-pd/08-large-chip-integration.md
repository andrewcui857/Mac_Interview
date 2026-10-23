# PD: Large Chip Integration
Status: draft
Priority: high
JD line: large chip integration

---

## Core idea
- Big chips are built hierarchically: blocks are implemented in parallel, then
  integrated at top with budgets and interface models.

---

## Key ideas
- Partitions with defined pins and timing budgets.
- Top-level constraints are split into block constraints (budgets).
- Block timing models (ILM, ETM, abstracts) let the top level time without full blocks.
- Top-level clock distribution, power domains, CDC and reset integration.
- Feedthroughs and repeaters for long top-level wires.

---

## Q&A

### Q: What is a timing budget?
- Allocation of the cycle for a cross-block path: block A output delay, top wire delay,
  block B input delay.

### Q: Block closes but top fails. Why?
- Different constraints, clock definitions, interface budgets, extraction differences,
  or real top wire delay larger than assumed.

### Q: Why hierarchical?
- Runtime, parallel teams, reuse (many identical shader cores), and ECO isolation.

### Q: What integration checks matter?
- Connectivity, lint, CDC/RDC, power intent (UPF), constraints consistency, LEC at top.

### Q: Why identical-block reuse?
- Implement one hard core and instantiate many, saving effort and giving regular timing.

---

## Drill
- Split a 1 ns cross-block path between block A, top wire and block B.
