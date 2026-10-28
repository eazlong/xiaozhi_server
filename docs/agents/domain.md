# Domain Docs

How the engineering skills should consume this repo's domain documentation when exploring the codebase.

**Layout: multi-context.** This repo's primary code lives under `main/` as five separately-deployable subprojects (`xiaozhi-server`, `manager-api`, `manager-web`, `manager-mobile`, `digital-human`), so each context gets its own `CONTEXT.md` and the repo root carries a `CONTEXT-MAP.md` that points at them.

> At initialization these files do **not** exist yet: no `CONTEXT-MAP.md`, no per-context `CONTEXT.md`. They are created lazily the first time real glossary terms are written down. Do not create them speculatively.

## Before exploring, read these

- **`CONTEXT-MAP.md`** at the repo root, if it exists: it points at one `CONTEXT.md` per context. Read each one relevant to the topic.
- **`CONTEXT.md`** for the context you're working in, once it exists, e.g. `main/xiaozhi-server/CONTEXT.md`.
- **`docs/adr/`**: read ADRs that touch the area you're about to work in. In multi-context repos, also check `<context>/docs/adr/` for context-scoped decisions.

If any of these files don't exist, **proceed silently**. Don't flag their absence; don't suggest creating them upfront. The `/domain-modeling` skill (reached via `/grill-with-docs` and `/improve-codebase-architecture`) creates them lazily when terms or decisions actually get resolved.

## File structure

Multi-context repo (presence of `CONTEXT-MAP.md` at the root):

```
/
├── CONTEXT-MAP.md                     ← created with the first glossary entry
├── docs/
│   ├── adr/                           ← system-wide decisions
│   └── agents/                        ← this setup
└── main/
    ├── xiaozhi-server/
    │   ├── CONTEXT.md                 ← the voice pipeline & protocol context
    │   └── docs/adr/
    ├── manager-api/
    │   ├── CONTEXT.md                 ← the management/console backend context
    │   └── docs/adr/
    ├── manager-web/
    │   ├── CONTEXT.md
    │   └── docs/adr/
    ├── manager-mobile/
    │   ├── CONTEXT.md
    │   └── docs/adr/
    └── digital-human/
        ├── CONTEXT.md
        └── docs/adr/
```

## Use the glossary's vocabulary

When your output names a domain concept (in an issue title, a refactor proposal, a hypothesis, a test name), use the term as defined in `CONTEXT.md`. Don't drift to synonyms the glossary explicitly avoids.

If the concept you need isn't in the glossary yet, that's a signal: either you're inventing language the project doesn't use (reconsider) or there's a real gap (note it for `/domain-modeling`).

## Flag ADR conflicts

If your output contradicts an existing ADR, surface it explicitly rather than silently overriding:

> _Contradicts ADR-0007 (event-sourced orders), but worth reopening because…_
