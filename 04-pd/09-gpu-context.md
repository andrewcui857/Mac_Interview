# PD: GPU Context
Status: draft
Priority: high
JD line: GPU implementation; CPUs/GPUs/DSPs desirable

---

## Core idea
- GPUs are arrays of many identical compute units with wide datapaths and high
  throughput. Power, area and timing pressure show up differently than in CPUs.

---

## Points to say
- Many repeated shader cores: hierarchical implementation, regular floorplans.
- Heavy arithmetic (MAC/FMA), wide register files and crossbars: congestion risk.
- High switching activity: dynamic power and IR drop dominate. Clock gating is key.
- Many clock/power domains and DVFS: multi-mode, multi-corner constraints.
- Large chip: budgeting and integration are routine work.
- Intern expectation: fundamentals and clear reasoning, not tool mastery.

---

## Q&A

### Q: What makes GPU implementation different from CPU?
- More replication, higher parallelism, power density driven, throughput over latency,
  bigger regular arrays so hierarchy and reuse matter.

### Q: Which of your experiences connect?
- CUDA in ECE 3803 (programming side), RV32I CPU and PD onboarding (flow side).
  Say clearly it is coursework and club scale.

---

## Drill
- 60 second answer: "Why this team, why GPU?" Use one concrete project.
