# Domain Docs

How the engineering skills should consume this repo's project and domain documentation when exploring the codebase.

## Before exploring, read these

Read the source-of-truth docs that exist for this repo:

- **Orientation docs** such as `README.md`, `index.md`, `docs/index.md`, `ARCHITECTURE.md`, `DESIGN.md`, or area-specific specs.
- **Project language docs** such as a domain glossary, product glossary, ubiquitous language doc, `docs/project-language.md`, `docs/glossary.md`, `docs/domain.md`, or area-specific language docs.
- **Decision docs** such as `docs/adr/`, area-specific ADRs, or decision sections in architecture docs.

If any of these files don't exist, **proceed silently**. Don't flag their absence and don't suggest creating them upfront. Producer skills such as `/grill-with-docs` create or update docs lazily only when language or decisions actually get resolved.

## Common layouts

Existing docs convention:

```
/
├── index.md
├── ARCHITECTURE.md
├── docs/
│   ├── index.md
│   └── decisions/
└── src/
```

Dedicated project-language glossary:

```
/
├── README.md
├── ARCHITECTURE.md
├── docs/
│   ├── project-language.md
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

Area-specific docs:

```
/
├── docs/
│   └── adr/                           <- repo-wide decisions
└── apps/
    ├── web/
    │   ├── README.md
    │   └── docs/adr/                  <- area-specific decisions
    └── api/
        ├── ARCHITECTURE.md
        └── docs/adr/
```

## Use the project's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the canonical term from the project's language docs. Don't drift to synonyms the docs explicitly avoid.

If the concept you need isn't documented yet, that's a signal: either you're inventing language the project doesn't use, or there's a real docs gap. Note it for `/grill-with-docs` instead of creating a new convention in passing.

## Flag decision conflicts

If your output contradicts an existing ADR or documented decision, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders) - but worth reopening because..._
