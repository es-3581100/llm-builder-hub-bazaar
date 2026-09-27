# Design Ledger
## LLM Builder Hub Bazaar — Pre-Implementation Record

**Repository:** [es-3581100/llm-builder-hub-bazaar](https://github.com/es-3581100/llm-builder-hub-bazaar)  
**Related project:** [es-3581100/llm-builder-hub](https://github.com/es-3581100/llm-builder-hub)  
**Initial ledger date:** 2026-09-26  
**Current status:** **UNSTARTED / PRE-IMPLEMENTATION**

---

## Purpose of this ledger

This file records the current design direction of LLM Builder Hub Bazaar before implementation begins.

It is intended to preserve:

- architectural intent
- project boundaries
- candidate interaction patterns
- reference projects worth mining
- working plugin-format ideas
- safety/authority invariants
- open questions
- deferred decisions
- expected implementation sequence

It is **not** a claim that the described architecture exists.

It is also not yet a frozen specification.

Use the following vocabulary:

```text
RECORDED INTENT
    design direction we currently want to preserve

CANDIDATE
    promising pattern that still needs implementation evidence

OPEN
    unresolved design question

DEFERRED
    intentionally not part of the first implementation phase

PROVEN
    implemented and verified in this repository
```

At project creation there are no `PROVEN` architecture entries yet.

---

# 1. Project relationship

## RECORDED INTENT

LLM Builder Hub Bazaar is an **adjacent extension ecosystem** for LLM Builder Hub.

It is not:

- a fork of the Hub
- a replacement for the Hub
- a second workflow authority
- the canonical project-state store

The parent Hub currently defines the workflow:

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

and preserves the boundary:

> The Hub transports intent without owning project-specific intent. Project architecture remains payload.

Bazaar should preserve that model.

Working relationship:

```text
LLM BUILDER HUB
    │
    │ owns / coordinates
    │
    ├── workflow lifecycle
    ├── build handoff
    ├── evidence flow
    ├── audit handoff
    └── project authority boundaries
            │
            │ may load or present
            ▼
LLM BUILDER HUB BAZAAR
    │
    │ provides optional
    │
    ├── plugins
    ├── reusable UI elements
    ├── schemas
    ├── extension manifests
    ├── plugin-side views
    ├── static projections
    └── reference integrations
```

The Bazaar should remain optional.

A project should not need Bazaar-specific behavior merely to remain a valid Hub project unless a future compatibility contract explicitly says otherwise.

---

# 2. Working thesis

## RECORDED INTENT

The current architectural thesis is:

> **Go owns semantics; schemas define contracts; HTML owns presentation; plugins request capabilities; the Hub grants authority; static HTML remains the portable fallback.**

Expanded:

```text
GO / LOCAL SERVICE
    ↓
canonical types
state
validation
privileged operations

SCHEMA
    ↓
declared structure
configuration contracts
action contracts
validation surface

HTML5
    ↓
presentation
semantic documents
user interaction
static projection

PLUGIN MANIFEST
    ↓
identity
capability requests
actions
views
document kinds
assets

HUB
    ↓
admission
capability grant
host bridge
state/evidence recording
```

---

# 3. Authority model

## RECORDED INTENT

An HTML5 plugin must not become authoritative merely because it executes locally.

The desired authority relationship is:

```text
HTML
→ presentation authority

plugin manifest
→ declared intent

schema
→ declared data/action contract

Hub
→ capability decision

local service
→ privileged action

evidence layer
→ durable result record
```

Explicit anti-pattern:

```text
plugin JavaScript
    ↓
local browser
    ↓
"therefore trusted"
```

That shortcut is rejected.

## CANDIDATE

Future capability declarations may resemble:

```yaml
plugin:
  id: audit-go
  version: 0.1.0

capabilities:
  requested:
    - project.read
    - report.write

actions:
  audit:
    title: Run Audit
```

The final vocabulary is not frozen.

---

# 4. Plugin package shape

## CANDIDATE

Initial boring, inspectable layout:

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

Potential later package:

```text
my-plugin.llmhub
```

but only if packaging provides real value.

The underlying contents should remain inspectable and based on ordinary formats where practical.

Preferred building blocks:

```text
HTML5
YAML
JSON
CSS
JavaScript
plain-text documentation
ordinary assets
```

## OPEN

Questions not yet resolved:

- directory package vs archive package
- package signing
- package hashes
- compatibility/version negotiation
- installation manifest location
- dependency declarations
- local-only vs remotely discoverable packages
- plugin update policy
- whether JavaScript is optional or required
- whether some plugins can be HTML/schema-only

---

# 5. Live plugin vs static projection

## RECORDED INTENT

Plugins should have a useful non-executable representation.

Desired capability reduction:

```text
LIVE PLUGIN
HTML
+ granted host APIs
+ interactive state
+ allowed actions
        ↓
freeze / project
        ↓
STATIC HTML5
semantic content
+ metadata
+ evidence
- mutation
- privileged host calls
```

Static output should clearly identify itself as read-only.

## Candidate uses

- audit artifact
- project handoff
- ChatGPT attachment
- offline viewing
- release artifact
- documentation
- evidence archive
- human review

---

# 6. Host / plugin bridge

## CANDIDATE

A narrow embedded-app bridge is currently preferred over direct arbitrary DOM trust.

Conceptual layout:

```text
LLM-HUB HOST
      │
      │ controlled bridge
      ▼
┌────────────────────┐
│ plugin HTML5 app   │
│ sandboxed/isolated │
└────────────────────┘
```

Possible host SDK vocabulary:

```text
navigate()
readDocument()
writeDraft()
requestCapability()
requestAction()
emitFinding()
getProjectMetadata()
```

These are placeholders, not an API contract.

## RECORDED INTENT

The plugin should ask the host for privileged behavior.

It should not reach directly into:

- filesystem
- shell
- Git mutation
- OpenCode execution
- credential stores
- host-local secrets

unless a later capability design explicitly grants a narrow operation.

---

# 7. Declarative actions and schemas

## RECORDED INTENT

Prefer declarative contracts over bespoke per-plugin UI validation.

Candidate relationship:

```text
Go type
   ↓
JSON Schema
   ↓
plugin/action contract
   ↓
generated or schema-aware form
   ↓
validation
   ↓
same authoritative Go type
```

The objective is to reduce drift between:

```text
backend type
schema
form
validation
documentation
```

## CANDIDATE

An action may eventually resemble:

```yaml
actions:
  audit:
    title: Run Audit

    config_schema:
      type: object

      properties:
        depth:
          type: string
          enum:
            - normal
            - deep

        include_tests:
          type: boolean

      required:
        - depth

      additionalProperties: false
```

---

# 8. Document model

## RECORDED INTENT

Bazaar should align with the Hub's developing **LLM-native document workbench** rather than inventing a separate dashboard language.

Primary visual/document primitive:

```text
Markdown-fence-style document pane
```

Example:

```text
┌─ yaml ─ PLUGIN MANIFEST ─────────── VIEW | EDIT ┐
│ ```yaml                                       │
│ plugin:                                         │
│   id: audit-go                                  │
│ ...                                             │
│ ```                                           │
└─────────────────────────────────────────────────┘
```

Candidate document kinds:

- text
- markdown
- yaml
- json
- source
- manifest
- prompt
- report
- finding
- diff
- ledger
- audit

## RECORDED INTENT

Documents should expose identity and semantics directly in HTML where practical.

Example:

```html
<article
  data-hub-document="true"
  data-document-id="plugin-manifest"
  data-document-kind="yaml"
  data-plugin="audit-go"
  data-state="saved"
  data-authority="local">
  ...
</article>
```

This supports both humans and inspecting agents.

---

# 9. Hub workstation grammar that plugins should fit

## RECORDED INTENT

Current Hub UI direction includes:

```text
far-left quick rail
    ↓
0–3 hierarchical left sliders
    ↓
document field
    ↓
right-side overlay
```

Desktop document geometry:

```text
0 open sliders → 4 document columns
1 open slider  → 3 document columns
2 open sliders → 2 document columns
3 open sliders → 1 document column
```

Each hierarchical slider is expected to own a five-slot contextual tool spine.

The two axes remain separate:

```text
slider depth
→ hierarchy / workspace geometry

tool-spine selection
→ function inside that hierarchy level
```

Plugins should eventually integrate with this grammar rather than building unrelated full-screen navigation systems by default.

---

# 10. Shared component vocabulary

## CANDIDATE

A common vocabulary may include:

- buttons
- fields
- select controls
- tabs
- accordions
- dialogs
- notices
- progress indicators
- tables
- code/document surfaces
- toolbars
- diagnostics
- status markers

The architecture should distinguish:

```text
PLUGIN
→ meaning + content + requested capability

HUB
→ shell + authority + interaction grammar

THEME / COMPONENT VOCABULARY
→ presentation
```

No external component library should be allowed to define the Hub's authority model.

---

# 11. Icon vocabulary

## CANDIDATE

Five-slot tool spines should eventually reference semantic icon identities, not treat a Unicode glyph as the actual meaning.

Prefer:

```yaml
slot: 3
action: run
icon: play
```

over:

```yaml
slot: 3
icon: "▶"
```

Possible canonical identities:

```text
hub.icon.nodes
hub.icon.files
hub.icon.run
hub.icon.report
hub.icon.search
```

Glyph/theme selection then becomes presentation.

---

# 12. Validation result semantics

## RECORDED INTENT

Do not confuse:

```text
the validator successfully ran
and found problems
```

with:

```text
the validation operation failed to run
```

Candidate result model:

```text
plugin/action result
├── execution_status
│   ├── completed
│   └── failed
│
└── findings
    ├── info
    ├── warning
    └── error
```

Example:

```text
AUDIT FOUND 12 ERRORS
```

must not imply:

```text
AUDITOR CRASHED
```

This distinction should survive UI, static export, and agent-readable evidence.

---

# 13. Static-generation testing

## CANDIDATE

Static projections should eventually be tested as deterministic outputs.

Possible test pattern:

```text
fixture project/plugin
        ↓
render/export
        ↓
normalize
        ↓
compare with golden HTML
```

This is preferable to only asserting that an export command returned success.

Semantic regressions matter.

---

# 14. Configuration and localization

## DEFERRED

Potential later concerns:

- embedded localization dictionaries
- locale negotiation
- plugin-local translations
- configuration overlays
- environment-specific settings
- generated docs from schemas

These should not block the first plugin proof.

---

# 15. Agent-oriented plugins

## DEFERRED

The Bazaar may eventually support plugins whose purpose includes:

- research
- verification
- auditing
- evaluation
- retrieval
- actor execution
- MCP integration

But the first plugin format should not be designed around agent autonomy.

The base format should first prove:

```text
identity
manifest
schema
HTML presentation
capability request
host admission
static projection
```

Agent-oriented behavior can then build on that foundation.

---

# 16. External reference set

These are pattern sources, not automatic dependencies.

## Primary references

### Invopop Console UI SDK

Repository:

- https://github.com/invopop/console-ui-sdk

Interesting for:

- host ↔ embedded app communication
- iframe application model
- child navigation mirrored into host/deep-link state

### Invopop Action Schemas

Repository:

- https://github.com/invopop/action-schemas

Interesting for:

- declarative action definitions
- YAML
- JSON Schema
- explicit argument/config contracts

### PopUI / PopUI Go

Repositories:

- https://github.com/invopop/popui
- https://github.com/invopop/popui.go

Interesting for:

- shared component vocabulary
- browser + Go-rendered UI concepts
- reusable control patterns

### GOBL Builder

Repository:

- https://github.com/invopop/gobl.builder

Interesting for:

- self-contained editor component
- menu/toolbar/editor/diagnostics composition
- configurable backend endpoint

## Secondary "mine when needed" references

- https://github.com/invopop/jsonschema
- https://github.com/invopop/codemirror-json-schema
- https://github.com/invopop/icons
- https://github.com/invopop/gobl.html
- https://github.com/invopop/gobl.generator
- https://github.com/invopop/popapp
- https://github.com/invopop/phorm
- https://github.com/invopop/ctxi18n
- https://github.com/invopop/expert
- https://github.com/invopop/popbot-experiments

## Reference rule

Do not adopt a dependency merely because its design informed this project.

For each candidate dependency:

```text
identify pattern
    ↓
verify actual need
    ↓
check license / maintenance / fit
    ↓
compare against simpler local implementation
    ↓
adopt only if justified
```

---

# 17. First implementation proof

## PLANNED

The first implementation phase should remain bounded.

Target vertical slice:

```text
local plugin fixture
    ↓
plugin manifest discovered
    ↓
manifest/schema validated
    ↓
semantic HTML loaded
    ↓
plugin identity exposed
    ↓
one narrow host API
    ↓
one capability request
    ↓
explicit allow/deny
    ↓
one structured result/finding
    ↓
static read-only HTML export
```

The first proof should prefer a disposable fixture plugin.

It should not begin with a marketplace or arbitrary third-party execution.

---

# 18. Candidate first-phase acceptance conditions

## PLANNED

A future first implementation phase should likely prove:

```text
[ ] plugin fixture can be discovered locally
[ ] manifest has a defined schema
[ ] invalid manifest fails clearly
[ ] valid manifest normalizes deterministically
[ ] plugin HTML is identifiable semantically
[ ] host/plugin boundary is narrow
[ ] plugin cannot silently acquire capability
[ ] capability decision is explicit
[ ] structured result distinguishes findings from runtime failure
[ ] live view can become a static read-only projection
[ ] static output contains no privileged mutation path
[ ] tests demonstrate the full vertical slice
```

This list remains draft until implementation starts.

---

# 19. Explicitly deferred features

## DEFERRED

Do not front-load these into the first build:

- public marketplace
- automatic online package discovery
- arbitrary remote plugin installation
- automatic updates
- plugin ratings/reviews
- payment infrastructure
- multi-user tenancy
- direct ChatGPT OAuth
- GitHub-as-runtime-authority
- arbitrary shell access
- arbitrary filesystem access
- plugin-to-plugin unrestricted calls
- distributed workflow execution
- autonomous background agents
- final package signing infrastructure
- final compatibility guarantees

---

# 20. Open design questions

## OPEN

### Plugin isolation

Options to investigate:

- iframe sandbox
- same-origin isolated route
- no-JavaScript static plugin mode
- Web Worker for selected logic
- WASM for selected bounded logic

### Capability vocabulary

Need a small, comprehensible initial set.

Possible future examples:

```text
project.read
document.read
draft.write
report.write
action.request
export.create
```

Do not freeze these yet.

### Host API transport

Possible candidates:

- `postMessage`
- host-injected SDK
- local HTTP endpoints with scoped tokens
- generated adapter
- combination of the above

### Plugin state

Need to decide boundaries among:

```text
plugin draft state
plugin saved configuration
Hub project state
runtime result/evidence
static projection state
```

### Packaging

Need evidence before choosing:

- folder
- zip
- custom extension
- signed archive
- Git checkout
- single HTML file for simple plugins

### Dependency policy

Need explicit rules for:

- CDN use
- vendored JS/CSS
- offline operation
- third-party license capture
- integrity hashes
- reproducibility

---

# 21. Design invariants to preserve

## RECORDED INTENT

Until superseded by a documented decision, preserve:

```text
local authority over browser convenience

explicit capability over implied trust

schema over undocumented contract

semantic HTML over opaque UI

static fallback over live-only dependency

structured finding over ambiguous error

boring files over unnecessary custom formats

host-owned privilege over plugin-owned privilege

inspection over hidden state

evidence over confidence
```

---

# 22. Change-log convention

Future entries should be added with:

```text
DATE
STATUS
AREA
CHANGE
RATIONALE
EVIDENCE / REFERENCE
SUPERSEDES (if any)
```

Example:

```text
2026-10-xx

STATUS:
CANDIDATE → PROVEN

AREA:
Plugin manifest validation

CHANGE:
Implemented JSON Schema Draft 2020-12 validation for plugin.yaml.

RATIONALE:
Manifest contracts need deterministic admission behavior.

EVIDENCE:
tests/...
fixture/...
commit ...

SUPERSEDES:
Initial candidate manifest sketch.
```

Do not silently rewrite history when a major architectural assumption changes.

Record the new decision and identify what it supersedes.

---

# 23. Initial ledger entry

## 2026-09-26

**STATUS:** RECORDED INTENT  
**AREA:** Repository creation / project boundary

### Change

Created the LLM Builder Hub Bazaar repository as a separate pre-implementation project for future Hub extensions, HTML5-formatted plugins, shared component vocabulary, schema contracts, and portable/static plugin projections.

### Current architecture direction

```text
Hub
→ workflow + authority

Bazaar
→ optional plugin/extension ecosystem

Go
→ semantics / privileged operations

Schema
→ contract

HTML5
→ presentation / portable projection

Plugin
→ requests capability

Hub
→ grants or denies
```

### Current reference discoveries

Invopop's ecosystem exposed several candidate patterns:

```text
console-ui-sdk
→ narrow host/embedded-app bridge

action-schemas
→ declarative schema-driven actions

PopUI / popui.go
→ shared component vocabulary

jsonschema
→ Go type → JSON Schema

codemirror-json-schema
→ schema-aware editor surface

gobl.builder
→ self-contained editor/workbench component

icons
→ shared semantic icon vocabulary

gobl.html
→ deterministic Go → HTML projection

phorm
→ runtime failure != validation finding
```

### Implementation status

```text
NOT STARTED
```

No listed component is yet adopted as a dependency.

No plugin format is yet frozen.

No runtime capability is yet implemented.

---

# 24. Next decision boundary

The next meaningful transition for this repository should be:

```text
DESIGN RECORD
    ↓
bounded Phase-0 / first-plugin proof
```

Before that transition, define:

- exact first fixture plugin
- first manifest schema
- first host API
- first capability
- first static export requirement
- first test matrix

Then build only that vertical slice.

Do not promote the Bazaar to a "plugin platform" by documentation alone.
