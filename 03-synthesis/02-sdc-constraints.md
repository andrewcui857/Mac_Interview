# Synthesis: SDC Constraints
Status: draft
Priority: high
JD line: multi-mode timing constraints; STA

---

## Core idea
- SDC tells the tool what "correct timing" means. Bad constraints give wrong
  optimization, even if the RTL is perfect.

---

## Must-know commands
- `create_clock -period 1.0 [get_ports clk]`  define the clock.
- `create_generated_clock`  clocks from dividers or muxes.
- `set_clock_uncertainty`  jitter plus margin (setup and hold separately).
- `set_clock_latency` / `set_propagated_clock`  ideal before CTS, propagated after.
- `set_input_delay` / `set_output_delay`  external timing at the boundary.
- `set_driving_cell`, `set_load`  model the boundary electrically.
- `set_false_path`, `set_multicycle_path`  exceptions.
- `set_clock_groups -asynchronous`  clocks with no timing relationship.
- `set_case_analysis`  fix a mode pin to a constant.
- `set_max_delay` / `set_min_delay`  explicit point to point constraints.

---

## Q&A

### Q: Input delay of 0.3 ns on a 1 ns clock. What does it mean?
- Data arrives 0.3 ns after the clock edge at the port, so the internal logic gets
  about 0.7 ns minus setup and uncertainty.

### Q: When is a false path legitimate?
- Only if the path can never be functionally exercised or is timing-irrelevant
  (static config, async clock domain already handled by CDC logic).
- Risk: a wrong false path hides a real violation. Review each one.

### Q: Multicycle path: what do you set?
- Same-clock, N cycles: setup N, hold N-1.
- Setup alone leaves hold checked N-1 edges too early, which gives huge hold fixes.

### Q: Ideal vs propagated clock?
- Ideal: zero skew network, used before CTS. Propagated: real tree delays after CTS.
  Switch to propagated once the tree exists.

### Q: Why multiple modes?
- Functional, scan shift, scan capture, test, low power. Each has different clocks
  and exceptions. Timing must close in every mode. See `01-sta/05-mmmc-corners-modes.md`.

---

## Drill
- Write the SDC for a block: 1 GHz clock, 0.3 ns input delay on `din`, 0.2 ns output
  delay on `dout`, one 2-cycle path from `cfg_reg` to `alu_out`.
