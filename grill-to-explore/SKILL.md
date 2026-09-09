---
name: grill-to-explore
description: A relentless interview that fleshes out a concept into a sketch, throwaway thinking that answers a question, without deciding anything. Graduating a sketch into an ADR is a separate, explicit step.
disable-model-invocation: true
compatibility: "Requires three skills from mattpocock/skills, invoked by name via the Skill tool (grilling, domain-modeling, grill-with-docs). Install them first; see metadata.install."
metadata:
  requires: "mattpocock/skills@grilling mattpocock/skills@domain-modeling mattpocock/skills@grill-with-docs"
  install: "npx skills add https://skills.sh/p/cU1n03Di8YeEI7ZX"
  pack: "https://skills.sh/p/cU1n03Di8YeEI7ZX"
---

A **sketch** is throwaway thinking that answers a question. It is to a decision what a prototype is to production code: fast, unpolished, clearly marked, and kept only as a primary source. `grilling` supplies the interview; this skill changes what the interview produces. Nothing here writes `CONTEXT.md` or `docs/adr/`.

Formats: [SKETCH-FORMAT.md](./SKETCH-FORMAT.md). Reading rule for later agents: [CONSUMER-RULES.md](./CONSUMER-RULES.md).

## Steps

1. **Name the question.** One sentence the sketch exists to answer. Write it as the first line of the sketch file before the interview starts. If the owner's prompt holds two questions, that is two sketches.

2. **Open the sketch file.** Use the repo's existing incubation folder if one exists (`docs/brainstorms/`, `docs/sketches/`, `docs/plans/`); otherwise create `docs/sketches/`. File name `YYYY-MM-DD-slug.md`, banner from SKETCH-FORMAT.md at the top.

3. Call the Skill tool with `grilling`. Two changes to its default:
   - **Surface the state.** Close every round by rewriting the sketch's *Shape so far* section: what is settled for the purpose of this sketch, what is still open, what was tried and dropped. The file is the state; the chat is scratch.
   - **Terms stay local.** A term coined during the sketch is defined inside the sketch. `CONTEXT.md` is untouched until graduation.
   Run to an empty frontier.

4. **Answer the question.** Write the *Answer* section: the verdict in the owner's words, and the premise it holds while. If the frontier emptied without an answer, the answer is "open" and the sketch says what evidence would close it. Done when a reader who opens only the file can state the question, the answer, and the premise.

5. **Offer graduation, once.** Ask the owner: does any part of this sketch deserve to become a decision now? On a no, stop; the sketch is complete as a sketch. On a yes, for each named part:
   - Ask how strongly they hold it, **law** or **ruling**, and record the answer verbatim. Anything weaker stays in the sketch.
   - Call the Skill tool with `domain-modeling` for that part only. The resulting ADR carries the conviction and premise lines and a pointer back to the sketch (SKETCH-FORMAT.md, *Graduation*).
   - Where the part redefines a term already in `CONTEXT.md` or a prior ADR, the ADR names every prior definition and gives each a disposition. Done when none is left unaddressed.

6. **Consumer rule.** Check the repo's `docs/agents/domain.md`, else `CLAUDE.md` or `AGENTS.md`, for a `## Sketches and conviction` section. If it is missing, show the owner CONSUMER-RULES.md and offer to append it. Write only on a yes.
