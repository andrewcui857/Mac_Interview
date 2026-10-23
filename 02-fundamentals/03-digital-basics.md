# Fundamentals: Digital Basics
Status: draft
Priority: med

---

## Q&A

### Q: Latch vs flip-flop?
- Latch is level sensitive. Flop is edge triggered (two latches back to back).

### Q: Metastability?
- If data changes within the setup/hold window the output can hover between levels.
  Resolve with synchronizers (2 flops) to give time to settle.

### Q: Glitches and hazards?
- Unequal path delays cause brief wrong outputs. Harmless if only the final value is
  sampled, harmful for clocks, async resets, gated enables. Use registered/ICG outputs.

### Q: Why are flops preferred over latches in design?
- Easier timing analysis and DFT. Latches can borrow time but complicate STA.

### Q: Gray code use?
- Only one bit changes per step, safe to sample across clock domains.

### Q: Synchronous vs asynchronous reset?
- Async: immediate, needs synchronized deassertion. Sync: only on clock edge, more logic.

---

## Drill
- Convert 4-bit binary 0 to 7 to Gray. Why is the sequence safe for CDC?
