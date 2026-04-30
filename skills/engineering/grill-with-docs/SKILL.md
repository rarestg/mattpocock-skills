---
name: grill-with-docs
description: Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates project language docs and ADRs inline as decisions crystallise. Use when user wants to stress-test a plan against their project's language and documented decisions.
---

<what-to-do>

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

Ask the questions one at a time, waiting for feedback on each question before continuing.

If a question can be answered by exploring the codebase, explore the codebase instead.

</what-to-do>

<supporting-info>

## Domain and docs awareness

During codebase exploration, also look for existing documentation. Prefer the repo's current convention over creating a new one:

- `docs/agents/domain.md` if this setup skill has already recorded the repo's doc layout.
- Orientation docs such as `README.md`, `index.md`, `docs/index.md`, `ARCHITECTURE.md`, `DESIGN.md`, and area-specific specs.
- Project language docs such as a domain glossary, product glossary, ubiquitous language doc, `docs/project-language.md`, `docs/glossary.md`, or `docs/domain.md`.
- Decision docs such as `docs/adr/`, area-specific ADRs, or decision sections in architecture docs.

If the repo already has source-of-truth docs for language, update those. Use [PROJECT-LANGUAGE-DOCS.md](./PROJECT-LANGUAGE-DOCS.md) when choosing where and how to capture terms.

Create files lazily - only when you have something to write and the target convention is clear. Do not create a parallel glossary in a repo that already uses different source-of-truth docs for project language. If no language-doc convention exists, ask before creating a dedicated glossary; a neutral default is `docs/project-language.md` when the user wants one.

### Supported doc layouts

Existing docs convention:

```
/
├── docs/
│   ├── index.md
│   └── adr/
├── ARCHITECTURE.md
├── index.md
└── src/
```

Dedicated project-language glossary:

```
/
├── docs/
│   ├── project-language.md
│   └── adr/
└── src/
```

Area-specific docs:

```
/
├── docs/
│   └── adr/                          <- repo-wide decisions
├── apps/
│   ├── web/
│   │   ├── README.md
│   │   └── docs/adr/                 <- area-specific decisions
│   └── api/
│       ├── ARCHITECTURE.md
│       └── docs/adr/
```

If no `docs/adr/` exists, create it only when the first ADR is needed.

## During the session

### Challenge against project language

When the user uses a term that conflicts with existing project language, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y - which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account' — do you mean the Customer or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible — which is right?"

### Update project docs inline

When a term is resolved, update the relevant project language doc right there. Don't batch these up - capture them as they happen. Preserve the repo's existing doc convention; use [PROJECT-LANGUAGE-DOCS.md](./PROJECT-LANGUAGE-DOCS.md) only when a dedicated glossary is appropriate.

Don't couple project language docs to implementation details. Only include terms that are meaningful to domain experts.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR. Use the format in [ADR-FORMAT.md](./ADR-FORMAT.md).

</supporting-info>
