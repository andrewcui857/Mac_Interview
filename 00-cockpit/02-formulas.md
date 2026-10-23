# Formulas and Numbers Cheat Sheet
Status: draft
Priority: high

---

## Timing
- Setup: `T_launch + t_clk2q + t_logic(max) <= T_clk + T_capture - t_setup - uncertainty`
- Hold: `T_launch + t_clk2q + t_logic(min) >= T_capture + t_hold + hold_uncertainty`
- Slack = required time - arrival time. Negative means violation.
- Skew = capture clock latency - launch clock latency.
- Positive skew (capture later) helps setup, hurts hold.
- Hold does not depend on the clock period. Setup does.
- f_max ~ 1 / (t_clk2q + t_logic + t_setup + skew + uncertainty)

## Power
- Dynamic: `P_dyn = alpha * C * V^2 * f` (alpha = switching activity)
- Short-circuit: small, during input transitions.
- Leakage: subthreshold dominates, grows exponentially as Vt drops.
- Biggest dynamic levers: reduce V (squared), reduce alpha (clock gating), reduce C.

## Logical effort
- Stage delay `d = g*h + p`   (g logical effort, h = Cout/Cin electrical effort, p parasitic)
- Path effort `F = G * B * H`, best stage count `N ~ log4(F)`, stage effort `f = F^(1/N)`
- Path delay `D = N*F^(1/N) + P`
- g: inverter 1, NAND2 4/3, NOR2 5/3. p: inverter 1, NAND2 2, NOR2 2.

## Digital
- FIFO depth (burst B words, write rate fw, read rate fr, fr < fw): `ceil(B * (1 - fr/fw))`
- Gray code: `gray = bin ^ (bin >> 1)`
- Async FIFO pointers: N+1 bits for a 2^N deep FIFO.

## Physical
- Utilization = cell area / core area.
- Wire RC delay grows with length squared (unbuffered). Buffer long wires.
