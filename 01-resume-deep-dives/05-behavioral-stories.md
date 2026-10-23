# Behavioral Stories (STAR)
Status: draft
Priority: high

---

## Format
- Situation (1 sentence), Task (1), Action (3 to 4, specific), Result (1 to 2, real).
- Aim for 60 to 90 seconds.

---

## Story 1: Testbench debugging (hard bug / ambiguity / learning)
- Situation: DV onboarding, scoreboard reported a mismatch on a load/store test.
- Task: decide whether the DUT, reference model, or testbench was wrong.
- Action: reproduced the failure against my own known-good CPU; same result, so it was
  not an injected bug. Traced it to the monitor reporting the same store more than
  once when write enable stayed high. Fixed by comparing address/data to the previous
  cycle. [VERIFY who found vs who confirmed]
- Result: scoreboard became trustworthy, so bug-hunt evidence was valid.
- Lesson: check the checker before blaming the design.

## Story 2: Feedback handling
- [VERIFY] pick a real example (lead review, resume feedback, team code review).

## Story 3: Learning quickly
- CPU, then DV, then PD in one semester, plus CUDA. [VERIFY] pick one concrete
  example of learning a tool and what you did when stuck.

## Story 4: Ambiguity
- [VERIFY] e.g., reference model bug causing expected mismatches, deciding how to
  proceed.

## Story 5: Teamwork
- Cave Explorer, 3 person team. [VERIFY] specific moment.

---

## Why Apple / why this role
- Work at the RTL to PD boundary: timing, power, area tradeoffs on a GPU team.
- Want to learn synthesis and timing closure in a real flow.
