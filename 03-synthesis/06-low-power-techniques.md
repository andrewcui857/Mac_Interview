# Synthesis: Low Power Techniques
Status: draft
Priority: high
JD line: aggressive low power

---

## Core idea
- Dynamic power: `alpha * C * V^2 * f`. Leakage: depends on Vt, temperature, V.
- Attack switching activity first (cheap), then leakage, then voltage.

---

## Dynamic power
- Clock gating: stop the clock to idle registers. Biggest win, since the clock toggles
  every cycle. Use an ICG cell (latch plus AND) to avoid glitches.
- Operand isolation: block input toggling into idle datapaths.
- Multibit flops: share clock buffering, lower clock cap.
- Reduce glitches: balance path delays, fewer deep XOR chains.
- Data encoding: Gray code for counters/addresses reduces bit flips.
- Memory banking or enable gating: only the used bank toggles.

## Leakage
- Multi-Vt: High-Vt on non-critical paths, low-Vt only on critical ones.
- Power gating: header/footer switches cut supply to idle blocks.
  Needs isolation cells, retention flops, always-on logic, and a power-up sequence.
- Longer-channel cell variants where available.

## Voltage
- DVFS: lower V and f in light modes. Level shifters between voltage domains.

---

## Q&A

### Q: Why is clock gating the first lever?
- Clock nets have activity 1 (toggle every cycle), so gating idle blocks removes the
  largest switching component.

### Q: What goes wrong with clock gating?
- Enable arrives late or glitches (use ICG), gated clock adds skew, LEC and STA need
  clock gating checks, and CTS must balance through the gate.

### Q: Power gating needs what extra cells?
- Isolation cells (hold outputs at a known value), retention flops (save state),
  header/footer switch cells, always-on supply for control, and UPF to describe it.

### Q: What is UPF?
- Unified Power Format: a text spec of power domains, supply nets, isolation, level
  shifters, retention and power states. Tools use it in synthesis, PD and LEC.

### Q: Two ways to cut dynamic power with no function change?
- Clock gating and operand isolation.

---

## Drill
- A block is idle 80 percent of the time. List two ways to save power and the
  verification cost of each.
