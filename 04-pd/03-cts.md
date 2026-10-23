# PD: Clock Tree Synthesis
Status: draft
Priority: high

---

## Core idea
- CTS builds buffered clock trees so all sinks receive the clock with low skew and
  acceptable latency, power, and slew.

---

## Terms
- Latency (insertion delay): root to sink delay.
- Skew: latency spread across sinks.
- Useful skew, clock gating cells in the tree, NDR (wider spacing/width) for clock
  nets, shielding, H-tree vs clock mesh (mesh for very high-performance blocks).

---

## Q&A

### Q: Why does hold break after CTS?
- Ideal clocks hid skew. Real skew shortens hold margin on some paths. Fix with delay
  cells, then recheck setup.

### Q: What does CTS balance?
- Skew among sinks, including through clock gates and across hierarchy and macros.

### Q: Why use NDR and shielding on clocks?
- Lower resistance and less coupling noise so clock edges are cleaner and jitter is lower.

### Q: Clock power?
- Clock tree is a big part of dynamic power (activity 1). Gating, multibit flops, and
  fewer buffers reduce it.

### Q: Ideal vs propagated after CTS?
- Switch to propagated clocks so STA uses real latencies.

---

## Drill
- Explain how skew affects setup and hold with a two-flop picture.
