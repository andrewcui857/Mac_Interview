# DD: Synthesizable Verilog / SystemVerilog Style
Status: draft
Priority: high
JD line: Verilog/VHDL familiarity

---

## Rules
- Sequential logic: `always_ff` with non-blocking (`<=`).
- Combinational logic: `always_comb` with blocking (`=`) and full default assignments.
- No `initial`, `#delay`, or file IO in synthesizable code.
- Use explicit widths, `unique case` or `case` with default.

---

## Q&A

### Q: Blocking vs non-blocking?
- Non-blocking for clocked logic so all flops sample old values (no races). Blocking for
  combinational so statements evaluate in order. Mixing gives sim/synth mismatch.

### Q: How does a latch get inferred?
- Combinational block that doesn't assign an output on every path. Fix with defaults.

### Q: always_comb vs always @(*)?
- always_comb has automatic sensitivity, runs at time 0, and tools warn on latches and
  multiple drivers.

### Q: Async reset coding?
- `always_ff @(posedge clk or negedge rst_n) if (!rst_n) ... else ...`
  Deassert should be synchronized.

### Q: Width pitfalls?
- Context-determined widths, silent truncation, sign extension. Size constants and use
  casts.

### Q: What is not synthesizable?
- Delays, initial blocks (except FPGA init), real numbers, force/release, fork-join.

---

## Drill
- Write a 4-bit loadable counter with async active-low reset, from memory.
