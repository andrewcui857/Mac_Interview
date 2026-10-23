# DD: Finite State Machines
Status: draft
Priority: high

---

## Core idea
- Moore: outputs depend on state only. Mealy: outputs depend on state and inputs
  (faster response, glitch risk, combinational input to output path).

---

## Template (three-block style)

```systemverilog
typedef enum logic [1:0] {IDLE, RUN, DONE} state_t;
state_t state, next;

always_ff @(posedge clk or negedge rst_n)
  if (!rst_n) state <= IDLE;
  else        state <= next;

always_comb begin
  next = state;                 // default avoids latches
  unique case (state)
    IDLE: if (start) next = RUN;
    RUN:  if (finish) next = DONE;
    DONE: next = IDLE;
    default: next = IDLE;
  endcase
end

assign busy = (state == RUN);   // Moore output
```

---

## Q&A

### Q: One-hot vs binary encoding?
- One-hot: more flops, simpler next-state logic, faster, good for FPGAs/high speed.
  Binary: fewer flops, deeper logic.

### Q: Why register outputs?
- Avoid glitches and shorten timing from state to output.

### Q: Unused states?
- Add default to recover to IDLE, important for safety.

### Q: Mealy vs Moore for timing?
- Mealy has input to output combinational path, which hurts timing at block boundaries.

---

## Drill
- Write a detector for the sequence 1011 (overlapping). Moore, then Mealy.
