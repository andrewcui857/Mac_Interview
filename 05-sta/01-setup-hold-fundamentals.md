# STA: Setup and Hold Fundamentals
Status: draft
Priority: high
JD line: static timing analysis; setup/hold closure

---

## Core idea
- STA checks every timing path against its constraint without simulation vectors.
- Setup: data must arrive and settle before the capturing edge.
- Hold: data must not change too soon after the capturing edge.

---

## Equations
- Setup: `launch_lat + t_clk2q + t_logic(max) <= T + capture_lat - t_setup - uncertainty`
- Hold: `launch_lat + t_clk2q + t_logic(min) >= capture_lat + t_hold + uncertainty`
- Slack = required - arrival.

## Worked setup example
- T = 1.0 ns, clk2q = 0.10, logic = 0.75, setup = 0.05, uncertainty = 0.05, skew = 0
- Arrival = 0.10 + 0.75 = 0.85
- Required = 1.0 - 0.05 - 0.05 = 0.90
- Slack = +0.05 ns (met)

## Worked hold example
- clk2q(min) = 0.08, logic(min) = 0.02, hold = 0.03, capture clock later by 0.06
- Arrival = 0.10. Required = 0.03 + 0.06 = 0.09. Slack = +0.01 (met, barely)
- Remove the 0.02 logic and slack goes to -0.01: a violation. Fix with a delay cell.

---

## Q&A

### Q: Why doesn't lowering the clock frequency fix hold?
- Hold is a same-edge race. The period does not appear in the equation.

### Q: Which fixes help setup and which help hold?
- Setup: reduce logic depth, upsize/low-Vt, buffer, restructure, retime, useful skew,
  last resort slower clock.
- Hold: insert delay cells/buffers, downsize, fix skew. Costs area and can hurt setup.

### Q: What do positive and negative skew do?
- Positive (capture later): more setup time, less hold margin. Negative: the reverse.

### Q: Path types?
- reg2reg, in2reg, reg2out, in2out. Each is constrained by clock and IO delays.

### Q: WNS vs TNS?
- WNS: worst single slack. TNS: sum of all negative slacks. TNS shows how widespread.

### Q: What is a clock gating check?
- STA checks the enable arrives before the clock edge at the gate and holds long
  enough, so the gated clock does not glitch.

### Q: What is a recovery/removal check?
- Timing for deasserting an async reset relative to the clock, analogous to
  setup/hold on the reset pin.

---

## Drill
- A path has slack -0.2 ns. Name three fixes in the order you would try them.
