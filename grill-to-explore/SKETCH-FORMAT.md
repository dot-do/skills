# Sketch Format

## The file

```md
> **Sketch.** Throwaway thinking that answers one question. Not a decision. Cite as "sketch", never as binding. Graduated parts, if any, are listed at the bottom.

# {Question, as one sentence}

Owner present: yes | no · {YYYY-MM-DD}

## Shape so far

**Settled for this sketch:** …
**Open:** …
**Tried and dropped:** …

## Answer

{Verdict in the owner's words, or "open" plus the evidence that would close it.}
Holds while: {one-line premise}

## Graduation

{none} | ADR-NNNN ← {which part}
```

*Shape so far* is rewritten at the end of every round; it is the only state the interview keeps. Terms coined in the sketch are defined where they first appear, inside the sketch.

## Rules, mirrored from `prototype`

1. **Throwaway from day one, clearly marked.** The banner is the first line. The file lives in the repo's incubation folder, beside the work it explores, never in `docs/adr/`.
2. **Trivial to read.** Question at the top, answer near the bottom. A reader who opens only this file can state both.
3. **No persistence.** `CONTEXT.md` and `docs/adr/` are untouched while sketching. Graduation is the only door.
4. **Skip the polish.** No numbered rulings, no `Status:` line, no R-headings. Those shapes signal "decided", and a sketch is not.
5. **Surface the state.** Every round ends with *Shape so far* rewritten.
6. **Capture it when done.** The sketch stays as a primary source. Graduated ADRs point back to it; it points forward to them.

## Graduation

Only **law** or **ruling** graduates. An ADR born from a sketch adds these lines under its title, in the `domain-modeling` ADR format:

```md
Conviction: ruling ("I'd revisit this if the atlas numbers move" — owner, 2026-09-08)
Holds while: coordinate supply stays decoupled from ICP discovery
Sketch: docs/sketches/2026-09-08-icp-grain.md
Supersedes: ADR-0047 §1 (superseded), ADR-0049 (stands, narrowed to the residual gate)
```

| Level | Meaning | What a later agent does |
|---|---|---|
| **law** | The owner will defend this. Changing it takes a grill and an amendment. | Honor it. Propose no alternative outside a grill. |
| **ruling** | Decided and in force. The owner would revisit it given evidence. | Honor it. A counter-finding is welcome when aimed at the premise. |

A law also gets one line in `docs/adr/LAW.md`, the register agents read first, created with the first law:

```md
- ADR-0003 · An ICP is a junction, evaluated, never minted · holds while junction grain remains N-ary · 2026-09-08
```
