# Fundamentals: CMOS Basics
Status: draft
Priority: med

---

## Core idea
- CMOS gate = PMOS pull-up network + NMOS pull-down network, complementary. Only one
  network conducts in steady state, so static power is near zero (leakage only).

---

## Q&A

### Q: Why are NAND gates preferred over NOR?
- NAND stacks NMOS in series (NMOS is faster, higher mobility). NOR stacks PMOS in
  series (slower, needs wider PMOS). So NAND is faster and smaller for equal drive.

### Q: Sources of power?
- Dynamic (charging C), short-circuit (both networks briefly on), leakage (subthreshold,
  gate, junction).

### Q: Why does lowering Vt speed a gate and raise leakage?
- Lower Vt means more drive current, but subthreshold current rises exponentially.

### Q: What sets inverter delay?
- Drive resistance times load capacitance (RC). Bigger driver or smaller load is faster.

### Q: Noise margin?
- How much noise a gate input tolerates before the output is wrong: NM_H = V_OH - V_IH,
  NM_L = V_IL - V_OL.

### Q: Why scale voltage down?
- Dynamic power goes with V squared. Cost: slower gates and less noise margin.

---

## Drill
- Draw a CMOS NAND2 and NOR2 and name which transistors are in series.
