# Fundamentals: Logical Effort
Status: draft
Priority: med

---

## Core idea
- Method to size gates in a chain for minimum delay.
- Stage delay `d = g*h + p`. g depends on gate type, h = Cout/Cin, p is parasitic.
- Path effort `F = G*B*H`. Best number of stages `N ~ log4(F)`. Stage effort `f = F^(1/N)`.
- Values: inverter g=1, p=1. NAND2 g=4/3, p=2. NOR2 g=5/3, p=2.

---

## Worked example
- Inverter chain drives a load 64x the input cap. F = 64.
- N=3: f = 4, D = 3*4 + 3*1 = 15 tau.
- N=2: f = 8, D = 2*8 + 2 = 18 tau.
- N=4: f = 2.83, D = 4*2.83 + 4 = 15.3 tau.
- Best is 3 stages (stage effort near 4).

---

## Q&A

### Q: Why is the optimum stage effort around 4?
- Fewer stages: each stage has big effort. More stages: parasitic delay adds up.
  Around 4 balances them.

### Q: What does g tell you?
- How much worse the gate is at driving load than an inverter with the same input cap.

### Q: Use in real flows?
- Intuition for buffer chains and sizing. Tools do the sizing; you reason about it.

---

## Drill
- Size a 2-stage vs 3-stage buffer chain to drive 100x load. Which is faster?
