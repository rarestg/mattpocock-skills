# Interface Design

When the user wants to explore alternative interfaces for a chosen deepening candidate, use this parallel sub-agent design pattern. Independent sub-agents are the point: they make it much more likely that the alternatives are genuinely different. Based on "Design It Twice" (Ousterhout) — your first idea is unlikely to be the best.

Uses the vocabulary in [LANGUAGE.md](LANGUAGE.md) — **module**, **interface**, **seam**, **adapter**, **leverage** — and the project's documented language as described in [PROJECT-DOCS.md](PROJECT-DOCS.md).

## Process

### 1. Frame the problem space

Before spawning sub-agents, write a user-facing explanation of the problem space for the chosen candidate:

- The constraints any new interface would need to satisfy
- The dependencies it would rely on, and which category they fall into (see [DEEPENING.md](DEEPENING.md))
- A rough illustrative code sketch to ground the constraints — not a proposal, just a way to make the constraints concrete

Show this to the user, then immediately proceed to Step 2. The user reads and thinks while the sub-agents work in parallel.

### 2. Spawn sub-agents

Spawn 3+ sub-agents in parallel. Each must produce a **radically different** interface for the deepened module. If sub-agents are unavailable, explicitly say so and then produce the alternatives yourself.

Use blank-slate delegation when the environment supports it, so each sub-agent reasons from an independent brief instead of inheriting the current conversation. In Codex, spawn with `fork_context: false`, `model: "gpt-5.5"`, and `reasoning_effort: "xhigh"` for this substantive design work. In other environments, use the strongest available model and the closest equivalent of a no-prior-context spawn.

Prompt each sub-agent with a standalone technical brief. Do not assume it has read this conversation. Include the repo purpose, relevant docs, file paths, coupling details, dependency category from [DEEPENING.md](DEEPENING.md), what sits behind the seam, scope, and expected output. Give each sub-agent a different design constraint:

- Agent 1: "Minimise the interface — aim for 1–3 entry points max. Maximise leverage per entry point."
- Agent 2: "Maximise flexibility — support many use cases and extension."
- Agent 3: "Optimise for the most common caller — make the default case trivial."
- Agent 4 (if applicable): "Design around ports & adapters for cross-seam dependencies."

Include both [LANGUAGE.md](LANGUAGE.md) vocabulary and relevant project language/orientation docs in each brief so every sub-agent names things consistently with the architecture language and the project's domain language.

Each sub-agent outputs:

1. Interface (types, methods, params — plus invariants, ordering, error modes)
2. Usage example showing how callers use it
3. What the implementation hides behind the seam
4. Dependency strategy and adapters (see [DEEPENING.md](DEEPENING.md))
5. Trade-offs — where leverage is high, where it's thin

### 3. Present and compare

Present designs sequentially so the user can absorb each one, then compare them in prose. Contrast by **depth** (leverage at the interface), **locality** (where change concentrates), and **seam placement**.

After comparing, give your own recommendation: which design you think is strongest and why. If elements from different designs would combine well, propose a hybrid. Be opinionated — the user wants a strong read, not a menu.
