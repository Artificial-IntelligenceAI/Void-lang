# Graft — Design decisions

Running log. Each entry gives the date, the decision, who proposed it and who chose it, quoting the owner where they
spoke. Nothing is final until the owner says so. Open questions are at the bottom.

## Decided

### 2026-11-01 — The language is called Graft (owner)

The owner: "Let's make/design Graft (coding language)." The design choices are the owner's. Claude may suggest.

### 2026-11-01 — Licences: Apache-2.0 WITH LLVM-exception for code, CC BY 4.0 for writing (owner)

The owner: "legal: Apache 2.0 with LLVM exception, CC BY 4.0". This follows CyborgPL: [`LICENSE`](LICENSE) covers the
code and everything else, and [`LICENSE-CC-BY-4.0`](LICENSE-CC-BY-4.0) covers this repo's Markdown and future logos.

### 2026-11-01 — The repo is `Artificial-IntelligenceAI/Graft-lang`, with commits in CyborgPL's style (owner)

The owner: "GH repo location: <myacc, not Soclets>/Graft-lang" and "GH commit style: Soclets/CyborgPL (don't over
read, though)". Commits are written `kind.area.topic: what is now true`, with `(owner: "…")` when the owner chose it.
The kinds are `decision`, `design`, `feature`, `fix` and `test`. The author identity is the one CyborgPL uses (a
`.invalid` address), so no personal email lands in the history. Claude created the repo **private**. Whether it
becomes public is open (pitch, decision 9).

## Open

The first decisions are listed at the end of [`design/pitch.md`](design/pitch.md): the core idea, the first program,
typing, memory, how it runs, the implementation language, syntax, the file extension and visibility.
