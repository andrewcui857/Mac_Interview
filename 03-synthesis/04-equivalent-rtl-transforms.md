# Synthesis: Logically Equivalent RTL Transforms
Status: draft
Priority: high
JD line: optimize with logically equivalent RTL transforms

---

## Core idea
- Change structure, not function. Outputs for every input sequence stay identical.
- Equivalent to the formal tool means it must prove it. See the LEC file.

---

## Transforms that stay equivalent
- Operator restructuring: balanced tree instead of a chain, carry-save for multi-operand
  adds, parallel-prefix adders (Kogge-Stone fast and big, Brent-Kung small and slower).
- Late-arriving signal last: move the late signal to the final mux/AND so it sees
  one gate instead of many.
- Mux restructuring: priority chain to parallel one-hot select when conditions are
  mutually exclusive (only if truly exclusive).
- Logic duplication: copy high-fanout logic to cut load and depth.
- Resource sharing: one adder reused for two mutually exclusive operations (saves area).
- Bit-width trimming and constant propagation.
- Clock gating enable extraction: the register holds when enable is off.
- Operand isolation: AND the inputs of an arithmetic block with the use-enable.
- Retiming (moving flops across logic): same I/O behavior, different register
  positions. LEC needs retiming support or sequential equivalence checking.

---

## Not equivalent (changes cycle behavior)
- Adding a pipeline stage: latency changes. Only with architecture-level agreement.
- Changing reset values or initial state.
- Removing "dont care" assumptions the verification relies on.

---

## Q&A

### Q: A MAC is on the critical path. What changes?
- Use carry-save accumulation, Booth encoding for the multiplier, balance the add
  tree, keep the late accumulator input to the last stage. Cost: area, and complexity.

### Q: Why is pipelining not a logically equivalent transform?
- It shifts outputs by a cycle, so the sequence of outputs differs. Combinational
  equivalence fails, and the surrounding design must be updated.

### Q: What does retiming change and why is it tricky?
- Moves registers across gates to balance stage delay. Reset/initial values must be
  recomputed. LEC needs to know the register correspondence changed.

### Q: Resource sharing hurts timing. When?
- The shared unit needs input muxes on the path. If the path was critical, those muxes
  add delay. Share only off the critical path.

### Q: Priority mux versus parallel mux?
- Priority chain depth grows with number of conditions. Parallel (one-hot) select has
  constant depth but needs a proof or a pragma that conditions are exclusive.

---

## Drill
- Take `y = a + b + c + d` (chain). Rewrite as a balanced tree. Count adder delays
  before and after.
