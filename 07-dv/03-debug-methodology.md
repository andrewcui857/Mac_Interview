# DV: Debug Methodology
Status: draft
Priority: med

---

## Steps
1. Reproduce deterministically (same seed).
2. Find the first mismatch in time, not the loudest error.
3. Decide who is wrong: DUT, reference model, or testbench.
4. Minimize: shrink to a small directed test.
5. Check the waveform: inputs, internal state, outputs around that time.
6. Fix, re-run the full regression, add a directed test or assertion.

---

## Q&A

### Q: How do you tell a testbench bug from a DUT bug?
- Run against a known-good DUT. If the same failure appears, it is testbench or model.

### Q: What if results differ between runs?
- Check seeds, uninitialized state, race conditions, X propagation.

### Q: Story to tell
- See `04-resume-deep-dives/05-behavioral-stories.md` (testbench debugging story).
