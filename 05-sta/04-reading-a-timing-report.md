# STA: Reading a Timing Report
Status: draft
Priority: high

---

## Sample setup report (generic format)

```
Startpoint: u_a/q_reg  (rising edge-triggered flop clocked by clk)
Endpoint:   u_b/d_reg  (rising edge-triggered flop clocked by clk)
Path Type: max

Point                          Incr     Path
clock clk (rise edge)          0.00     0.00
clock network delay (ideal)    0.00     0.00
u_a/q_reg/Q                    0.11     0.11 r
u_a/U12/Y (NAND2)              0.09     0.20 f
u_a/U31/Y (NOR2)               0.12     0.32 r
u_a/U44/Y (XOR2)               0.18     0.50 f
u_a/U51/Y (AOI21)              0.15     0.65 r
u_a/U60/Y (BUF)                0.10     0.75 r
u_a/U72/Y (INV)                0.13     0.88 f
data arrival time                       0.88

clock clk (rise edge)          1.00     1.00
clock uncertainty             -0.05     0.95
library setup time            -0.06     0.89
data required time                      0.89
slack (MET)                             0.01
```

---

## How to read it (in order)
1. Startpoint and endpoint: which two registers, which clocks. Path type: max (setup).
2. Launch: clock edge, clock network delay, then clk2q (the `Q` line).
3. Data path: each cell with increment. Look for the biggest increments first.
4. Capture: next edge at T = 1.0, minus uncertainty, minus library setup.
5. Required minus arrival = slack.

## What to say about this path
- Slack is +0.01, so it is nearly critical. Seven cells deep including an XOR and an
  AOI. If it were negative: shorten the cone, upsize the XOR and AOI, or restructure.
- Check for high fanout, large transition, or long wire on any cell with big Incr.

---

## Q&A

### Q: What is the first thing you look at in a failing path?
- Is the delay from logic depth, high fanout/large cap, a long wire, or clock skew?
  The fix depends on which.

### Q: What changes in a hold report?
- Path type min, uses fast corner, required time includes hold time plus capture
  clock latency, slack = arrival - required.

### Q: Data-path vs clock-path pessimism lines?
- Look for derates, CRPR adjustment, and uncertainty lines. They explain where margin
  went.

---

## Drill
- Make up a failing version of this report (slack -0.10) and list your fixes in order.
