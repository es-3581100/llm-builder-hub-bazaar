# LLM Builder Hub Bazaar

> **Status: UNSTARTED / PRE-IMPLEMENTATION**
>
> This repository currently defines intent, boundaries, and candidate architecture only. It does **not** yet contain a working plugin runtime, SDK, registry, compatibility contract, or production implementation.

## What this repository is

**LLM Builder Hub Bazaar** is the future extension, plugin, and reusable component space for [LLM Builder Hub](https://github.com/es-3581100/llm-builder-hub).

The working idea is to let the Hub eventually support portable, inspectable extensions whose presentation may be HTML5-based while authority remains outside the plugin itself.

The Bazaar is intended to explore and eventually host things such as:

- HTML5-formatted Hub plugins
- plugin manifests and capability declarations
- shared UI/component vocabulary
- semantic document surfaces
- schema-driven configuration and validation
- reusable tool-spine actions and views
- static/read-only plugin projections
- plugin authoring and preview tooling
- reference implementations and integration patterns
- compatibility and admission rules

This repository is **not** intended to become a second copy of the Hub.

## Relationship to LLM Builder Hub

The parent project is:

- [es-3581100/llm-builder-hub](https://github.com/es-3581100/llm-builder-hub)

The Hub currently defines the canonical human + agent workflow and preserves the invariant:

```text
GPT designs
    ↓
Git records
    ↓
OpenCode executes
    ↓
Git records
    ↓
GPT audits
```

Its responsibility boundary is also explicit:

> The Hub transports intent without owning project-specific intent. Project architecture remains payload.

The Bazaar should preserve that boundary.

A useful division of responsibility is:

```text
LLM BUILDER HUB
    │
    ├── workflow / lifecycle
    ├── project transport
    ├── execution handoff
    ├── evidence / audit flow
    └── local authority model
            │
            ▼
LLM BUILDER HUB BAZAAR
    │
    ├── optional extensions
    ├── reusable UI vocabulary
    ├── plugin manifests
    ├── capability declarations
    ├── plugin-side document surfaces
    ├── static projections
    └── reference integrations
```

The Bazaar should extend the Hub without becoming authoritative over Hub project state.

## Current project state

As of **2026-09-26**, implementation has not started.

Current state:

```text
repository created
    ↓
project relationship defined
    ↓
design direction recorded
    ↓
implementation NOT started
```

There is currently no claim of:

- a stable plugin format
- a plugin ABI
- a plugin SDK
- a sandbox implementation
- a plugin registry
- a package extension such as `.llmhub`
- a final component library
- a final capability model
- a final host/plugin bridge
- backward compatibility
- production readiness

Anything described below is **design intent or a candidate pattern** until implemented and verified.

## Seed corpus and planned plugin index

A first Bazaar seed corpus has now been inspected and normalized for planning. The imported bundle contains **42 top-level artifacts**, which normalize to **40 conceptual entries** after linking compiled companions and related variants.

The canonical planning record is:

- [PLANNED_PLUGIN_INDEX.md](./PLANNED_PLUGIN_INDEX.md)

This does **not** change the repository's implementation status. The Bazaar remains unstarted as a runtime/SDK/registry; the index records candidate material, reference builds, support artifacts, readiness evidence, authority boundaries, and explicit release/audit caveats so future implementation does not flatten every artifact into a false `ready` state.

### Readiness-driven first implementation queue

The following is an **opinionated implementation order based on current conversion readiness plus fit with the Hub's local-first authority model**. It is not a quality ranking.

| Rank | Candidate | Why implement it early |
|---:|---|---|
| 1 | **Derived State HTML5 Systems** | Only three standalone HTML files. Ideal smallest fixture for proving manifest load, semantic HTML admission, static projection, and a zero-privilege capability set before touching larger runtimes. |
| 2 | **OpenCode CLI Agent Linter** | Single-file, directly relevant to the Hub's OpenCode execution workflow, and naturally read-only. High practical value with a very small authority surface. |
| 3 | **LLM Tokenizer Lab** | Self-contained local analysis UI with no required privileged execution. Good second read-only plugin for validating repeatable packaging and host chrome. |
| 4 | **StackGraph Forge** | Already has a standalone HTML workbench plus an optional Go/Templ shell and baseline audit material. It stress-tests richer stateful UI without requiring arbitrary shell authority. |
| 5 | **Agent Theme Manager** | Web app plus a standalone Go companion. Theme/configuration semantics are low-risk and useful for proving shared component vocabulary and persisted plugin settings. |
| 6 | **go-AHTML** | Small pure-Go library/CLI with tests, schemas, and an embedded viewer. It is unusually well aligned with the Bazaar goal of semantic, agent-readable HTML contracts. |
| 7 | **Worksheet Deck** | Go already owns durable storage/server behavior while Kotlin/JS progressively enhances the browser. That is close to the host-authority / plugin-presentation split the Bazaar wants. |
| 8 | **Donpad Browser Relay** | Explicit localhost staging boundary between browser content and durable authority. A strong first test of real capability requests and a narrow host bridge. |
| 9 | **Logical State Clock** | Audited Go state/history implementation with a browser projection, legal-transition graph, hash-chain history and restart/tamper tests. Strong evidence/provenance plugin candidate. |
| 10 | **HTML Matrix Memory** | Go-booted memory system with stable pointers, persistence, graph/matrix/wiki projections and tests. More complex than the earlier entries, but mature enough to close the first wave. |

More ambitious runtimes such as **GRAPHCORE**, **HTMLChain**, **VEKTOR**, **TruthFrame**, **Nano State / CHEOPS**, and the cross-language **Tree Agent Runtime** are intentionally later. Their source is valuable, but they either carry explicit release/integration caveats or need host contracts that should be proven on smaller plugins first.

## Working design direction

The current direction is:

> **Go owns semantics; schemas define contracts; HTML owns presentation; plugins request capabilities; the Hub grants authority; static HTML remains a portable fallback.**

Conceptually:

```text
PLUGIN
    │
    ├── manifest
    ├── semantic HTML
    ├── local assets
    ├── schemas
    ├── requested capabilities
    └── optional richer live behavior
            │
            ▼
LLM-HUB HOST
    │
    ├── validates manifest
    ├── validates configuration
    ├── grants / denies capabilities
    ├── exposes narrow host APIs
    ├── owns privileged operations
    └── records resulting evidence
```

The core authority rule is:

```text
HTML
→ presentation authority

manifest / schema
→ declared intent and requested capability

Hub
→ capability decision

local service
→ privileged action
```

Never assume:

```text
plugin JavaScript
→ runs locally
→ therefore trusted
```

## Candidate plugin package shape

This is only a working sketch:

```text
my-plugin/
├── plugin.yaml
├── plugin.html
├── plugin.css
├── plugin.js
├── assets/
├── schemas/
└── README.md
```

A later packaging format may exist, but the current preference is to keep the underlying representation boring and inspectable:

```text
HTML5
YAML
JSON
CSS
JavaScript
plain assets
```

rather than inventing an opaque binary container.

## Live and static modes

A future plugin should ideally degrade cleanly:

```text
LIVE PLUGIN
HTML + granted capabilities + Hub APIs
        ↓
STATIC PROJECTION
HTML + semantic content + no mutation
```

This would allow a plugin or project view to remain useful for:

- human inspection
- audit
- archival
- sharing
- attachment to an LLM
- offline review

even when executable capabilities are unavailable.

## Semantic HTML direction

The live UI and static projections should expose useful structure directly.

Example direction:

```html
<article
  data-hub-document="true"
  data-document-id="build-ledger"
  data-document-kind="yaml"
  data-state="saved"
  data-authority="local"
  data-editable="true">
  ...
</article>
```

A host or inspecting agent should be able to recover meaningful state without computer vision alone.

Candidate semantics include:

- document identity
- document kind
- ordering
- authority
- saved / dirty state
- editability
- active tool
- available actions
- plugin identity
- requested capabilities

## Candidate inspiration set

The current design study has identified several useful external references.

### Invopop ecosystem

Particularly relevant repositories include:

- [invopop/console-ui-sdk](https://github.com/invopop/console-ui-sdk) — embedded app ↔ host communication and history synchronization
- [invopop/action-schemas](https://github.com/invopop/action-schemas) — declarative action configuration using YAML + JSON Schema
- [invopop/popui](https://github.com/invopop/popui) — shared component vocabulary for Svelte
- [invopop/popui.go](https://github.com/invopop/popui.go) — Go-side component vocabulary
- [invopop/codemirror-json-schema](https://github.com/invopop/codemirror-json-schema) — schema-aware JSON/JSON5/YAML editing
- [invopop/jsonschema](https://github.com/invopop/jsonschema) — generating JSON Schema from Go types
- [invopop/gobl.builder](https://github.com/invopop/gobl.builder) — self-contained editor/workbench interaction patterns
- [invopop/icons](https://github.com/invopop/icons) — shared icon vocabulary across Go and Svelte
- [invopop/gobl.html](https://github.com/invopop/gobl.html) — deterministic Go → HTML generation patterns
- [invopop/popapp](https://github.com/invopop/popapp) — Go application structure with web, CLI, embedded assets, and gateway separation
- [invopop/phorm](https://github.com/invopop/phorm) — distinction between execution failure and validation findings
- [invopop/ctxi18n](https://github.com/invopop/ctxi18n) — embedded/localizable application assets
- [invopop/expert](https://github.com/invopop/expert) and [invopop/popbot-experiments](https://github.com/invopop/popbot-experiments) — MCP/RAG and agent-evaluation references for much later agent-oriented plugin work

These are **reference sources, not automatic dependencies**.

The Bazaar should mine mature patterns without allowing an external component kit to define Hub architecture.

## Current workstation/UI context

The related Hub design work is moving toward a local-first workstation with:

- explicit local authority
- draft / saved / authoritative state separation
- manual `SAVE CHANGES`, `CLEAR EDITS`, and protected `REFRESH`
- semantic Markdown-fence-style document panes
- deterministic left-side navigation depth
- five-slot contextual tool spines
- right-side non-pushing management overlays
- semantic HTML
- static single-file HTML5 projection

Bazaar plugins should eventually fit into that grammar rather than inventing an unrelated application shell.

## Non-goals for the unstarted state

Do not begin by assuming the project needs:

- a marketplace
- remote package installation
- arbitrary third-party JavaScript trust
- automatic remote publishing
- GitHub as runtime authority
- a browser-owned source of truth
- plugin-controlled filesystem access
- plugin-controlled shell execution
- a giant event/reducer framework
- a mandatory Svelte runtime
- a mandatory PopUI dependency

Those choices require evidence and explicit design decisions.

## Project record

The current architecture, plans, candidate patterns, open questions, and future phase boundaries are tracked in:

- [DESIGN_LEDGER.md](./DESIGN_LEDGER.md)

That file is intentionally a **living design ledger**, not a frozen specification.

## First implementation milestone

When implementation begins, the first milestone should be intentionally small.

The likely first proof should establish:

```text
one local plugin fixture
    ↓
manifest load
    ↓
schema validation
    ↓
semantic HTML render
    ↓
narrow host bridge
    ↓
capability denied/granted explicitly
    ↓
static read-only export
```

No marketplace, remote installation, or arbitrary privileged execution is required for the first proof.

## Status label

Until working code and tests exist, this repository should continue to identify itself as:

> **UNSTARTED / PRE-IMPLEMENTATION / DESIGN RECORD**

Do not interpret detailed design notes as evidence that the described system has already been built.
