# Project: SiliconJackets DV Onboarding F26
Status: draft
Priority: high

---

## Facts
- Built a testbench around the same CPU: driver, monitor, scoreboard.
- Directed tests 1.1 to 1.18 (addi, add, sub, shifts, lw/sw roundtrip, beq taken/not
  taken, x0 write ignored, RAW hazard chain, ebreak halt timing, timeout, branch loop,
  long NOP sled of 511 instructions, and others).
- Coverage: DUT instance at 98.47 percent against a 98 percent requirement. The
  bottleneck was toggle coverage on pc_o/next_pc in fetch. Fixed by extending the
  NOP sled to 511 instructions.
- Bug hunt: find 3 bugs injected into an encrypted CPU.
  - Bug 1: a store wrote to dmem[0x178] instead of dmem[0x1b8] (one address bit, 0x40,
    differs). An address computation bug. Isolated as a directed test.
  - Bug 3 lead (as of Oct 3): beq seemed to ignore rs2 when rs1 == 0.
  - [VERIFY] final count and details of bugs 2 and 3 before saying "I found three".
- Testbench bug found during review: the monitor reported the same store multiple times
  when write enable stayed high across cycles. Fixed by comparing address and data with
  the previous cycle. [VERIFY] who found it (you vs the lead who reviewed).
- Known issue: a software reference model bug caused about 47 expected scoreboard
  mismatches, so random programs ran with a no-stop-on-error flag.

---

## Expected questions
### Q: Tell me about a hard bug you debugged.
- Use the monitor duplicate-store story. See `05-behavioral-stories.md`.

### Q: How did you decide a mismatch was a testbench bug and not a DUT bug?
- Reproduced against my own known-good CPU. Same failure, so not an injected bug.

### Q: How did you reach coverage goals?
- Looked at which toggle bins were missing, found the high PC bits, wrote a long
  NOP sled.

### Q: What assertions did you write?
- Halt is a single-cycle pulse; transport idle while running. [VERIFY] which ones
  you wrote vs were provided.

---

## Gaps
- Exact bug counts and which assertions are yours. Do not overstate.
