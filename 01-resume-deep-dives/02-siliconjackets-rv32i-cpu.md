# Project: SiliconJackets RV32I CPU (Digital Design Onboarding F26)
Status: draft
Priority: high

---

## Facts
- Single-core RV32I-style CPU in SystemVerilog around a provided scaffold
  (cpu_top.sv, fetch.sv, reg_file.sv, and others).
- Required instructions implemented: addi, add, sub, lw, sw, beq, sll, srl, ebreak.
- x0 stays zero.
- `make regress` passes all provided tests on Cadence Xcelium.

---

## What I did vs what the scaffold gave
- Scaffold gave: [VERIFY: list the files provided]
- I wrote: [VERIFY: decode, ALU, branch logic, load/store, etc.]

---

## Expected questions
### Q: Walk me through the pipeline/datapath.
- [VERIFY] Single-cycle or multi-cycle? Describe fetch, decode, execute, memory, writeback.

### Q: How did you implement beq?
- Compare rs1 and rs2, compute PC + imm if equal. Mention sign extension of the B-type
  immediate.

### Q: How do you guarantee x0 is zero?
- Writes to x0 are ignored in the register file; reads of x0 return 0.

### Q: What would limit your clock frequency?
- Critical path: instruction fetch to decode to regfile read to ALU to data memory.
  [VERIFY] with actual structure.

### Q: Design decision you made and why?
- [VERIFY] Prepare one real decision.

---

## Gaps
- Not run through synthesis yet? [VERIFY]. If true, say so, and say how you would
  expect the critical path to behave.
