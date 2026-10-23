# STA: Timing Fix Cheat Sheet
Status: draft
Priority: high

---

## Setup violations (data too slow)
- Upsize or low-Vt swap cells on the path.
- Buffer high fanout/long wires. Split loads.
- Reduce logic depth: restructure, retime, move late signal last.
- Duplicate registers or logic.
- Useful skew.
- Check constraints: uncertainty too big? exception missing?
- Last resort: relax clock or pipeline (architecture change).

## Hold violations (data too fast)
- Insert delay cells/buffers on short paths.
- Downsize or high-Vt swap short-path cells.
- Fix after CTS using real skew.
- Always recheck setup at slow corner afterward.

## Other
- Max transition / cap violations: buffer or upsize driver.
- Clock gating check fails: move enable earlier or add margin.
- Recovery/removal: retime reset deassertion, synchronize reset.

---

## One-liner to say aloud
- "I first locate the cause, logic depth, fanout, wire or skew. Then I choose the
  cheapest fix in area and power, rerun STA at all corners, and rerun LEC."
