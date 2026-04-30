# Project Language Docs

Use this guidance when a grilling session resolves domain terms and the repo has no stronger convention. Prefer updating the repo's existing source-of-truth docs over creating a dedicated glossary.

## Choose the target

Read `docs/agents/domain.md` first when it exists; it should describe the repo's doc layout. Then prefer the clearest existing home:

- Orientation docs that already define project concepts: `README.md`, `index.md`, `docs/index.md`, `ARCHITECTURE.md`, `DESIGN.md`, product specs, or area-specific specs.
- Dedicated language docs: a domain glossary, product glossary, ubiquitous language doc, `docs/project-language.md`, `docs/glossary.md`, or `docs/domain.md`.
- Area docs: a package/app `README.md`, area glossary, area architecture doc, or area design doc.

Create a new dedicated project-language glossary only when no suitable source-of-truth doc exists and the user wants terms captured. A neutral default is `docs/project-language.md`, but follow the repo's naming and placement style when it clearly has one.

## Dedicated glossary structure

Use this shape only for a dedicated project-language glossary. If writing into an existing architecture, product, or index doc, preserve that document's structure instead.

```md
# Project Language

{One or two sentence description of what this language covers and why it exists.}

## Terms

**Order**:
{A concise description of the term}
_Avoid_: Purchase, transaction

**Invoice**:
A request for payment sent to a customer after delivery.
_Avoid_: Bill, payment request

**Customer**:
A person or organization that places orders.
_Avoid_: Client, buyer, account

## Relationships

- An **Order** produces one or more **Invoices**
- An **Invoice** belongs to exactly one **Customer**

## Example dialogue

> **Dev:** "When a **Customer** places an **Order**, do we create the **Invoice** immediately?"
> **Domain expert:** "No - an **Invoice** is only generated once a **Fulfillment** is confirmed."

## Flagged ambiguities

- "account" was used to mean both **Customer** and **User** - resolved: these are distinct concepts.
```

## Rules

- **Be opinionated.** When multiple words exist for the same concept, pick the best one and list the others as aliases to avoid.
- **Flag conflicts explicitly.** If a term is used ambiguously, call it out in "Flagged ambiguities" with a clear resolution.
- **Keep definitions tight.** One sentence max. Define what it IS, not what it does.
- **Show relationships.** Use bold term names and express cardinality where obvious.
- **Only include terms specific to this project's domain.** General programming concepts don't belong even if the project uses them extensively.
- **Group terms under subheadings** when natural clusters emerge. If all terms belong to a single cohesive area, a flat list is fine.
- **Write an example dialogue** when it clarifies boundaries between related concepts.
- **Keep implementation details out.** The language should be meaningful to domain experts, not just maintainers reading code.

## Multi-area repos

When a repo has multiple product or domain areas, infer which area the current topic relates to. Put terms where future readers would naturally look:

- Repo-wide language belongs in the repo-level project-language or orientation doc.
- Area-specific language belongs in that area's source-of-truth docs.
- Cross-area relationships belong in the smallest shared doc that both areas already use.

If ownership is unclear, ask before writing.
