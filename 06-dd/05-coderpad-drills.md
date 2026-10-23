# DD: CoderPad Drills (write from memory, run in a simulator)
Status: draft
Priority: high

---

## Checklist per drill
- Ports and widths. Reset style. Registered or combinational output.
- Edge cases: reset, back-to-back inputs, wraparound.
- Say what you would test.

---

## Warm-ups
- Edge detector (rising, falling).
- Gray counter.
- Shift register with load.
- Parity generator / checker.
- Round-robin arbiter (4 requesters).
- Clock divide by 3 (50 percent duty is tricky).
- Debounce / synchronizer.
- Sync FIFO (template in `03-fifo.md`).

---

## Examples

Edge detector:
```systemverilog
logic d;
always_ff @(posedge clk or negedge rst_n)
  if (!rst_n) d <= 1'b0; else d <= sig;
assign rise = sig & ~d;
assign fall = ~sig & d;
```

Gray counter (registered output is better for CDC):
```systemverilog
logic [W-1:0] bin, gray;
always_ff @(posedge clk or negedge rst_n)
  if (!rst_n) begin bin <= '0; gray <= '0; end
  else if (en) begin
    bin  <= bin + 1'b1;
    gray <= (bin + 1'b1) ^ ((bin + 1'b1) >> 1);
  end
```

---

## Log (add your timings)
- Drill, date, time taken, mistakes.
