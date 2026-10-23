# DV: Assertions and Coverage
Status: draft
Priority: med

---

## SVA basics
- `|->` same-cycle implication, `|=>` next-cycle implication.
- `##N` delay, `##[1:3]` range. `$rose`, `$fell`, `$stable`, `$past`.
- Example:
```systemverilog
assert property (@(posedge clk) disable iff (!rst_n)
  req |-> ##[1:3] ack);
```

---

## Q&A

### Q: Assertion vs scoreboard check?
- Assertions are local and cycle-accurate (protocols, invariants). Scoreboards check
  end-to-end data against a model.

### Q: Types of coverage?
- Code (line, branch, toggle, FSM) and functional (covergroups). 100 percent code
  coverage doesn't mean the feature is verified.

### Q: Why was toggle coverage low on the PC?
- Upper PC bits rarely toggle with short programs. A long NOP sled exercises them.
  (See your CPU project note.)

### Q: What is a cover property?
- Checks that a scenario actually happened, useful to prove tests reach it.

---

## Drill
- Write an assertion: halt is a single-cycle pulse after ebreak. State what it would
  catch.
