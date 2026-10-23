# PD System Design: Cross-Block Timing Budget
Status: draft
Priority: high

---

## Prompt
- A 1 ns path goes from block A's register, through top-level wires, to block B's
  register. Block teams work in parallel. How do you set constraints?

---

## Reasoning outline
1. Start from the cycle: 1.0 ns total.
2. Estimate pieces: A clk2q + A output logic, top wire (distance and layer), B input
   logic + setup, clock uncertainty.
3. Example budget: A 0.35, top wire 0.20, B 0.30, margin 0.15.
4. Write set_output_delay for A (0.65) and set_input_delay for B (0.35 + wire share).
5. Iterate: if one block misses, rebalance with PD and RTL teams.
6. At top, check with real wires and update budgets.

---

## Follow-up Qs
- What if the top wire is longer than planned? Pipeline, move pins, add repeaters.
- Who owns the fix? Whoever has the cheapest change; communicate early.
