# DD: FIFOs (Sync and Async)
Status: draft
Priority: med

---

## Sync FIFO template

```systemverilog
module sync_fifo #(parameter int W = 8, D = 16)(
  input  logic clk, rst_n, wr_en, rd_en,
  input  logic [W-1:0] din,
  output logic [W-1:0] dout,
  output logic full, empty);
  localparam int AW = $clog2(D);
  logic [W-1:0] mem [D];
  logic [AW:0] wptr, rptr;               // extra bit distinguishes full/empty

  assign empty = (wptr == rptr);
  assign full  = (wptr[AW-1:0] == rptr[AW-1:0]) && (wptr[AW] != rptr[AW]);

  always_ff @(posedge clk or negedge rst_n)
    if (!rst_n) begin wptr <= '0; rptr <= '0; end
    else begin
      if (wr_en && !full)  wptr <= wptr + 1'b1;
      if (rd_en && !empty) rptr <= rptr + 1'b1;
    end

  always_ff @(posedge clk)
    if (wr_en && !full) mem[wptr[AW-1:0]] <= din;

  assign dout = mem[rptr[AW-1:0]];
endmodule
```
(D must be a power of two.)

---

## Async FIFO idea
- Write and read pointers in different clock domains.
- Convert pointers to Gray code, pass through 2-flop synchronizers to the other domain.
- Empty is computed in the read domain (rptr_gray == synced wptr_gray).
- Full is computed in the write domain (wptr_gray equals synced rptr_gray with top two
  bits inverted).

---

## Q&A

### Q: Why the extra pointer bit?
- To tell full from empty when low bits are equal.

### Q: Why Gray pointers across domains?
- Only one bit changes per increment, so a sampled value is either old or new, never
  a wrong mix.

### Q: Why are full/empty conservative in async FIFO?
- Synchronized pointers lag, so flags may assert late/early safely. Throughput can dip.

### Q: FIFO depth for a burst?
- `ceil(B * (1 - fr/fw))`, see `00-cockpit/02-formulas.md`.

---

## Drill
- Write the sync FIFO from memory, then explain how to extend to async.
