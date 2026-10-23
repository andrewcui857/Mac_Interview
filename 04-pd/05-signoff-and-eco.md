# PD: Signoff and ECO
Status: draft
Priority: med
JD line: setup/hold closure; ECO implementation

---

## Signoff checks
- STA with extracted parasitics at all MMMC scenarios.
- IR drop and EM, DRC, LVS, antenna, density.
- LEC final netlist vs RTL.

---

## ECO (engineering change order)
- A late, minimal change to a nearly finished design.
- Functional ECO: patch a logic bug, often with spare cells to avoid mask changes.
- Timing ECO: resize, buffer, swap Vt, add delay cells for hold.
- Always: rerun LEC, STA, DRC/LVS afterward.

---

## Q&A

### Q: Why use spare cells?
- A metal-only ECO reuses pre-placed unused gates, avoiding base-layer mask changes.

### Q: Steps of a functional ECO?
- Identify the RTL change, generate a netlist patch, map to existing/spare cells,
  implement and route incrementally, verify with LEC vs new RTL, rerun STA/DRC.

### Q: Why does a timing ECO need care?
- One fix can break another path (hold vs setup), and changes must stay LEC equivalent.

### Q: Signoff STA vs PD tool STA?
- Signoff uses a golden engine with more accurate extraction and derates, and is the
  basis for tapeout approval.

---

## Gaps
- ECO experience: none (be upfront). Concept: patch smallest change, rerun checks.
