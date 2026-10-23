# Synthesis: Rapid Fire
Status: draft
Priority: med

---

### Q: What is a latch inference and why avoid it?
- Incomplete assignment in combinational logic. Creates unintended storage and
  timing issues. Avoid with default assignments.

### Q: Flatten or keep hierarchy?
- Flatten: better optimization across boundaries, bigger runtime. Keep: parallel
  work, reuse, easier ECO. Large chips keep hierarchy.

### Q: What are max_transition, max_capacitance, max_fanout?
- Design rule constraints. Violations hurt delay accuracy and signal integrity.
  Fixed by buffering and sizing.

### Q: Why is area recovery done last?
- After timing is met, downsize non-critical cells to save area and leakage.

### Q: What is a wire load model?
- A statistical wire cap/RC estimate by fanout. Old and inaccurate at advanced nodes,
  replaced by physical-aware estimates.

### Q: Setup fix, hold fix: who does which?
- Synthesis mostly sets up setup. Hold fixing is normally done in PD after CTS, when
  real skew is known.
