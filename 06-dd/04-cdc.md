# DD: Clock Domain Crossing
Status: draft
Priority: med

---

## Techniques
- Single-bit level: 2-flop synchronizer.
- Single-bit pulse: toggle synchronizer or handshake.
- Multi-bit data: Gray code (counters only), req/ack handshake, or async FIFO.
- Reset: assert async, deassert synchronous to each domain (reset synchronizer).

---

## Q&A

### Q: Why not just double-flop a multi-bit bus?
- Bits can arrive on different cycles, so the receiver sees a value that never existed.

### Q: Handshake CDC?
- Sender holds data stable, toggles req. Receiver synchronizes req, captures data,
  toggles ack back. Safe but slow.

### Q: Reconvergence problem?
- Two synchronized signals from the same source recombine downstream and can be out
  of sync by a cycle.

### Q: How is CDC verified?
- CDC lint/static tools (SpyGlass, Questa CDC), plus assertions and simulation with
  randomized clock phase.

---

## Drill
- Draw the toggle pulse synchronizer. State the minimum pulse spacing requirement.
