# Project Docs

How this skill consumes repo-specific language and decision docs.

## Read order

Before judging architecture, look for docs that explain what the codebase is trying to say:

- Repo agent instructions, plus `docs/agents/domain.md` when present.
- Orientation docs such as `README.md`, `index.md`, `docs/index.md`, `ARCHITECTURE.md`, `DESIGN.md`, or area-specific specs that route readers through the repo.
- Project language docs: a domain glossary, product glossary, ubiquitous language doc, `docs/project-language.md`, `docs/glossary.md`, `docs/domain.md`, or area-specific language docs.
- Architectural decisions: ADRs, decision records, design notes, or decision sections in architecture docs.

If none exist, continue from the code. Missing docs make the output less sharp; they do not block the skill.

## Use language

- Use the project's canonical names for domain concepts.
- When docs conflict, surface the conflict instead of silently picking a synonym.
- When no glossary exists, prefer names already used in orientation docs and code over newly invented nouns.
- Use [LANGUAGE.md](LANGUAGE.md) for architecture vocabulary regardless of the project's domain language.

## Updating docs

Do not create a glossary just to satisfy this skill. Record clarified language or decisions only when the repo already has an obvious source-of-truth doc and the user wants the side effect.

Supported conventions include:

- Existing orientation or architecture docs such as `index.md`, `docs/index.md`, or `ARCHITECTURE.md`.
- Domain, product, glossary, or project-language docs under `docs/`.
- Area-specific language docs near the code or product area they describe.
- ADRs or other decision records for load-bearing architectural choices.

If the repo convention is unclear, keep the resolved wording in the recommendation and suggest where it could be recorded later.

## Recording decisions

Offer a decision record only for load-bearing architectural choices that a future explorer would otherwise re-litigate. Prefer the repo's existing ADR or decision-doc convention.

If no convention exists and the user wants the decision captured, create `docs/adr/` lazily and use a minimal ADR:

```md
# {Short title of the decision}

{1-3 sentences: what's the context, what did we decide, and why.}
```
