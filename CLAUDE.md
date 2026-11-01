# Working on Graft

- Design choices belong to the owner. Claude suggests (mark a suggestion ★) and never decides. A decision exists only
  once it is logged in `DECISIONS.md` with the owner's words quoted.
- Don't use popup questions. Ask the owner one question at a time, in chat, with lettered options (`a`, `b`, …).
- Commits use CyborgPL's style: `kind.area.topic: what is now true`, where kind is decision, design, feature, fix or
  test. Add `(owner: "…")` when the owner chose it. Add a body only when the change needs one.
- Author identity: `Tankun Sriket <tankunsriket63741ecff056.invalid>` (set in this repo's local git config). Never
  use a personal email.
- Licences: code is Apache-2.0 WITH LLVM-exception (`LICENSE`). Markdown and logos are CC BY 4.0 (`LICENSE-CC-BY-4.0`).
- Remote: `Artificial-IntelligenceAI/Graft-lang`.
