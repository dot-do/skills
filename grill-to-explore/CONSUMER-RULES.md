## Sketches and conviction

Thinking in this repo comes in two shapes. A **sketch** (any file whose first line is the sketch banner, wherever it lives) is throwaway exploration: the current best guess, nothing more. An **ADR** is a decision, and carries the conviction the owner stated when it was made.

- **sketch**, or any ADR with no `Conviction:` line: treat as the current default. Propose alternatives freely. Cite it as "sketch", never as binding.
- **ruling**: honor it. A counter-finding is welcome when it names the ADR's `Holds while` premise and shows the premise has fallen.
- **law**: honor it. Propose no alternative outside a grill session. `docs/adr/LAW.md` lists every law in one place; read it first.

Redefining a term that `CONTEXT.md` or a prior ADR already defines requires naming every prior definition and giving each a disposition. A redefinition that cites no prior definition is a sketch, whatever it calls itself; flag it.
