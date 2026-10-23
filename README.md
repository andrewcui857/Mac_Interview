# Interview Prep Workspace

Current target: Apple, GPU Implementation Intern (front-end synthesis, STA, timing closure, PPA).
Folders are numbered by importance for this role, then by study flow inside each folder.
Other roles (DD, DV, PD) and companies can be added without restructuring.

---

## During an interview
- Open `00-cockpit/00-start-here.md` first. Keep `00-cockpit/02-formulas.md` beside it.
- Search the whole folder (Cmd+Shift+F in VS Code) for a keyword, e.g. "hold" or "retiming".
- Every question is a `### Q:` heading. Answers are short bullets you can say aloud.

---

## Folder map (most important first)
- `00-cockpit`  Pitch, answer framework, JD, formulas. Open these live.
- `01-sta`  Highest JD weight: setup/hold, skew, OCV, exceptions, reports, MMMC.
- `02-synthesis`  Flow, SDC, PPA, equivalent RTL transforms, LEC, low power.
- `03-pd`  Physical design in flow order, plus `system-design/` scenarios.
- `04-resume-deep-dives`  Hiring manager will probe these. One file per project.
- `05-dd`  Digital design: Verilog style, FSM, FIFO, CDC, CoderPad drills.
- `06-fundamentals`  CMOS, logic effort, digital basics. Reference when a gap shows up.
- `07-dv`  Design verification: testbench, assertions, coverage, debug.
- `08-company`  One folder per company. Apple is the active one.
- `09-mocks-and-log`  Mock protocol, question log, weak spots.

## Suggested study flow for Apple
1. `00-cockpit` (10 min), then `01-sta` and `02-synthesis` (about half your time).
2. `03-pd` for basics and scenarios, then `04-resume-deep-dives`.
3. `05-dd` drills for CoderPad, `06-fundamentals` and `07-dv` as gaps appear.
4. `09-mocks-and-log` to test yourself.

---

## Conventions
- Numbers inside a folder follow the real flow (for example, `03-pd` runs floorplan to signoff).
- One topic per file, about 5 to 8 questions. Split a file when it grows past that.
- First lines of every file: `Status:` (draft, reviewed, solid) and `Priority:` (high, med, low).
- `[VERIFY]` marks a claim not yet confirmed. Resolve it before using it in an interview.
- No tables, no m-dashes. Lines wrapped near 90 characters.
- New role: copy a topic folder and edit. New company: copy `08-company/apple/`.
- Template for a new topic file: `00-cockpit/_topic-template.md`.
