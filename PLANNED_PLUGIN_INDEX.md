# LLM Builder Hub Bazaar — Official Planned Plugin Index

> **Status: PLANNING REGISTRY / NO RUNTIME IMPLIED**
>
> This document is the canonical planning index for the imported Bazaar seed corpus. An entry here does **not** mean the plugin has been admitted, implemented, installed, security-reviewed, API-compatible, or declared production-ready.

## Provenance

- Source corpus: `llm-hub-bazaar-plugins.zip`
- Corpus inspection date: **2026-09-26**
- Original top-level artifacts: **42**
- Normalized conceptual entries: **40**
- This planning pass inspected package structure plus available README/manifest/audit material; it did **not** execute the imported software.
- Audit labels below preserve what the source artifacts themselves claim. They are not a fresh Bazaar certification.

## Catalog vocabulary

| Field | Meaning |
|---|---|
| `artifact_kind` | What the imported thing actually is: runtime source, standalone app, reference build, ledger, flattened data, etc. |
| `implementation_status` | Current conversion posture for Bazaar: `ready-to-wrap`, `adapter-needed`, `integration-heavy`, `release-gated`, `scaffolded`, `reference-only`, `support-only`, or `claims-review-needed`. |
| `runtime_languages` | Languages materially represented by the artifact or its declared runtime boundary. |
| `ui_surface` | Browser/workbench/CLI surface and whether the artifact is already self-contained. |
| `offline_capable` | Whether the artifact appears usable without remote runtime authority. `conditional`/`local-capable` means extra local services or binaries may still be required. |
| `authority_boundary` | Where state, execution, filesystem, network, or privileged authority is intended to live. |
| `audit_status` | Source-declared audit/test/release evidence and caveats retained without flattening them to a generic `ready`. |
| `related_artifacts` | Multiple files belonging to one conceptual entry, variants, compiled companions, or retained legacy filenames. |

## Planning lanes

- **P1-01 … P1-10** — opinionated first implementation wave, ordered by current conversion readiness and Hub relevance.
- **P2** — viable candidates after the first host/plugin contract is proven.
- **DEFERRED** — substantial runtimes, release-gated packages, or cross-language systems that should wait for stronger host contracts.
- **REFERENCE** — architecture/UI quarry; not presumed to be a production runtime.
- **SUPPORT** — provenance, build ledger, prompt, workflow, or data artifact; useful to the Bazaar but not itself a plugin target.

## Normalization decisions

1. **`python mcp html.tar` is canonically indexed as `py-mpc-bench`.** The original filename is retained only as source provenance; the package is a Model-Predictive Control lab, not an MCP package.
2. **TruthFrame is one conceptual entry.** `truthframe-kotlin-0.1.0-SNAPSHOT.zip` is the source package and `truthframe-runtime-0.1.0-SNAPSHOT.jar` is its compiled companion.
3. **Vibe Coding · 144 Hex Master is one conceptual entry with two variants.** The offline packaged release and the larger Over-Engineered standalone edition remain separately traceable under `related_artifacts`.
4. **`A-tree-agent-sitter`, `AI-Driven-Note-Taking-Ecosystem`, `ai-browser`, and `Kotlin HTML AsyncMachine` are classified as interactive architecture/reference builds.** They are not promoted to production-runtime status by appearance alone.
5. **Audit and release caveats are preserved verbatim in spirit.** An audited source package with a remaining release gate stays `release-gated`; a bootstrap PASS does not become production readiness.
6. **The planning registry adopts explicit metadata instead of one generic `plugin` label.** The minimum catalog vocabulary is the field set above.

## Official planned catalog

| Plan | Canonical entry | artifact_kind | implementation_status | runtime_languages | UI / offline | authority_boundary | audit_status | related_artifacts |
|---|---|---|---|---|---|---|---|---|
| REFERENCE | `arbor-mesh` | Interactive architecture/reference build | reference-only | React/TypeScript; describes Rust + Go + Kotlin target | Vite dossier / unknown | No production runtime authority claimed; architecture study only | No Bazaar audit established | `A-tree-agent-sitter.tar` |
| P2 | `ai-stack-flowchart` | Standalone HTML app / reference | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Presentation and diagram generation only | No formal audit recorded | `AI Stack Flowchart for Agents and Actors.html` |
| REFERENCE | `mnemo-os` | Interactive architecture/reference build | reference-only | React/TypeScript | Vite dossier / unknown | Reference architecture only; no runtime authority claimed | No Bazaar audit established | `AI-Driven-Note-Taking-Ecosystem.tar` |
| SUPPORT | `branding-flattened` | Flattened data / provenance artifact | support-only | YAML | document / yes | No executable authority | Hashes and flattened metadata preserved | `Branding.zip.flattened.yaml` |
| P1-08 | `donpad-browser-relay` | Runtime source + local app | adapter-needed | Go + Chrome/Chromium extension JavaScript | extension + loopback web UI / loopback-local | Web content stages through an explicit localhost relay; database/filesystem authority stays outside the page | Phase-0 self-audit present | `Donpad-Browser-Relay-v0.2.0.zip` |
| DEFERRED | `vektor` | Runtime / state-memory engine | release-gated | Go + browser/TypeScript + optional native kernels | HTTP/WASM lab / local-capable | Go core owns vector/index semantics; browser is a client/projection | Audited source with remaining release gates explicitly recorded | `Golang%20Vector%20Database-audited-v0.5.0.tar` |
| DEFERRED | `graphcore` | Browser-native graph runtime | release-gated | Go + C++/WASM + HTML5 | browser workbench / local-capable | Go owns orchestration contracts; C++/WASM owns compute; browser is the workbench | Audited source; fresh production frontend build still required by package caveat | `HTML5-Native-LangGraph-audited-source.tar.gz` |
| REFERENCE | `asyncmachine-kotlin-html` | Interactive architecture/reference build | reference-only | React/TypeScript; documents Kotlin runtime concepts | Vite docs/playground / unknown | Reference/playground only; do not treat as a proven Kotlin production runtime | No Bazaar audit established | `Kotlin HTML AsyncMachine.tar` |
| SUPPORT | `necronomitron-dbl` | Build ledger / bootstrap | support-only | Markdown/YAML/ledger assets | documents / yes | No plugin execution authority; records plan, state and verification receipts | Bootstrap validation reports PASS while real checkout/Git grounding remains deferred | `NecronomiTron-DBL-bootstrap.zip` |
| P2 | `q-table-parity-lab` | Cross-language parity lab | adapter-needed | Go + C++17 + Rust + TypeScript | browser lab / yes | Pure-Go implementation is the canonical semantic baseline; other languages mirror for parity | Deterministic parity target present; not re-audited by Bazaar | `Q-Table-Parity-Lab-upgraded.tar` |
| P1-04 | `stackgraph-forge` | Standalone workbench + optional Go shell | ready-to-wrap | HTML/CSS/JavaScript + Go/Templ | standalone HTML + optional Go/PopUI shell / yes | Local graph/workbench state; optional Go shell can become host-side authority | Baseline audit present in package | `StackGraph-Forge-ultimate.zip` |
| P2 | `vibe-coding-144-hex-master` | Standalone/offline app family | ready-to-wrap | HTML/CSS/JavaScript | single-file/offline editions / yes | Presentation, palette state and export only | Offline verification, hashes and lineage included in packaged release | `Vibe_Coding_144_Hex_Master_v1.0_OFFLINE (1).zip`<br>`vibe-coding-144-hex-master-over-engineered-edition.html` |
| REFERENCE | `browseros-reference` | Interactive architecture/reference build | reference-only | React/TypeScript | Vite presentation/prototype / unknown | Product/architecture reference; no complete browser-engine authority assumed | No Bazaar audit established | `ai-browser.tar` |
| REFERENCE | `ai-text-detector-humanizer` | Standalone text-processing UI specimen | claims-review-needed | HTML/CSS/JavaScript | single-file / yes | Local presentation/text transformation only | Detector-quality claims are not validated; keep reference-only until separately evaluated | `ai-text-detector-humanizer.html` |
| P2 | `browser-tool-mcp-kotlin-html` | Runtime + browser MCP cockpit | integration-heavy | Kotlin/JS + HTML + local proxy | browser cockpit / local proxy required | Kotlin/JS owns MCP envelopes and risk classification; privileged admission is gated through the local proxy | No formal Bazaar audit recorded | `browser-tool-mcp-kotlin-html.tar.gz` |
| SUPPORT | `neon-html-agent-syntax-engine` | Prompt / builder source | support-only | Text | prompt source / yes | No runtime authority | Not an executable plugin artifact | `chat-Neon HTML Agent Syntax Engine.txt` |
| P1-01 | `derived-state-html5-systems` | Minimal plugin fixture set | ready-to-wrap | HTML/CSS/JavaScript | three standalone HTML files / yes | Derived UI state only; no privileged authority | No formal audit; deliberately tiny and directly inspectable | `derived-state-html5-systems.zip` |
| P2 | `dynamic-agent-master-ledger` | Standalone provenance/ledger app | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Local document/provenance/export surface only | No formal Bazaar audit recorded | `dynamic_agent_master_ledger.html` |
| P2 | `emergent-html-sheets` | Standalone simulation sheet collection | ready-to-wrap | HTML/CSS/JavaScript | multiple standalone sheets / yes | Presentation/simulation only | No formal Bazaar audit recorded | `emergent-html-sheets.zip` |
| P2 | `flat-zip-dons` | Flattened project viewer / DONS projection | ready-to-wrap | HTML5 | single-file / yes | Read/browse/export projection; no implied project mutation authority | Source corpus carries build/test/hash evidence, but Bazaar has not re-run it | `flat-zip.html5` |
| P1-06 | `go-ahtml` | Go runtime/library + CLI + viewer | ready-to-wrap | Go + embedded HTML | CLI + embedded tree viewer / yes | Go owns AHTML snapshot construction/validation/serialization; viewer is projection | Tests and schema/examples included | `go-AHTML-v0.1.0.tar.gz` |
| P2 | `go-html-anything` | Local agentic HTML editor/runtime | integration-heavy | Go + embedded browser UI | CLI + local web workspace / conditional | Go host discovers and invokes installed coding-agent CLIs; privileged execution must remain outside plugin HTML | Source is tightly scoped, but agent-CLI integration requires explicit Hub capability design | `go-html-anything-source.tar.gz` |
| P2 | `html-kotlin-runtime-starter` | Kotlin-owned runtime starter | adapter-needed | Kotlin + HTML/JavaScript | HTML bridge + Android/WebView guidance / local-capable | Kotlin owns state, execution, token routing, validation, lineage and policy; HTML owns presentation | Starter includes explicit trusted-origin warning for Android WebView bridge exposure | `html-kotlin-runtime-starter.zip` |
| P1-10 | `html-matrix-memory` | State/memory runtime + app | adapter-needed | Go + HTML5 + optional Kotlin enrichment | matrix/graph/wiki workspace / yes | Go boot/runtime owns ingest, stable pointers, retrieval and persisted workspace; browser is projection/controller | Tests, source manifest and build scripts included | `html-matrix-memory-v0.1.0.zip` |
| P1-07 | `worksheet-deck` | Local worksheet catalog/runtime | adapter-needed | Go + HTML + Kotlin/JS enhancement | browser deck / yes | Go owns durable storage/server authority; browser enhancement is progressive | Build report and Go tests included | `html-worksheet-library-v0.2.0.zip` |
| P2 | `htmlchain` | Browser-native composable chain runtime | integration-heavy | Go + C++/WASM + HTML5 | browser runtime/workbench / local-capable | Go/C++ runtime semantics stay outside browser presentation; JS is bootstrap/ABI glue | Runtime tests and build scripts included; no Bazaar revalidation | `html5-langchain-runtime.zip` |
| P1-05 | `agent-theme-manager` | Theme authoring app + Go companion | ready-to-wrap | HTML/CSS/JavaScript + Go | web app + standalone Go module / yes | Theme documents/configuration only; low privilege if host writes are capability-gated | README and Go module present; no formal Bazaar audit recorded | `interactive-agent-theme-manager (2).zip` |
| P2 | `llm-memory-wiki` | Exploratory memory/wiki UI | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Presentation and local workspace semantics only unless paired with an external runtime | Exploratory/reference status; no formal audit recorded | `llm-memory-wiki-system.html` |
| P1-03 | `llm-tokenizer-lab` | Standalone tokenizer analysis UI | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Read-only/local text analysis surface | No formal Bazaar audit recorded | `llm-tokenizer-lab.html` |
| P2 | `local-tools-studio` | Standalone multi-tool utility suite | ready-to-wrap | HTML/CSS/JavaScript | single-file tabbed tool suite / yes | Local browser utility operations only; any future filesystem/shell access must be host-granted | No formal Bazaar audit recorded | `local-tools-studio-2.html` |
| P1-09 | `logical-state-clock` | Audited logical-state runtime | adapter-needed | Go + browser/TypeScript | browser projection + Go runtime / local-capable | Go state graph/history owns legal transitions and monotonic logical position; browser is projection | Dedicated audit plus Go test suite present | `logical-state-clock-upgraded-source.tar.gz` |
| P2 | `micro-state-system` | Minimal finite-state UI | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Small local FSM visualization/control surface only | No formal Bazaar audit recorded | `micro-state-system.html` |
| P2 | `nano-sec-state-clock` | Derived-state/time visualization | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Observer-facing derived-state presentation; no privileged authority | No formal Bazaar audit recorded | `nano-sec-state-clock-v2.html` |
| DEFERRED | `nano-state-cheops` | Multi-language state/runtime starter | integration-heavy | Rust + Go + C++ + Kotlin + HTML5 | observer/controller web surface / local-capable | Rust is semantic owner; Go admission/batching, C++ scoring and Kotlin supervision remain separate authority layers | Starter architecture; integration proof still required | `nano-state-cheops-v0.1.zip` |
| P1-02 | `opencode-cli-agent-linter` | Standalone compatibility/lint UI | ready-to-wrap | HTML/CSS/JavaScript | single-file / yes | Read-only contract/parser/lint surface unless a future host action is explicitly granted | No formal Bazaar audit recorded | `opencode-cli-agent-linter.html` |
| SUPPORT | `opencode-cli-flow` | Workflow/process source | support-only | Text | workflow note / yes | No runtime authority | Process source, not a packaged plugin | `opencode_cli_flow` |
| SUPPORT | `polymath-matrix-build-ledger` | Build-ledger + skill scaffold | support-only | Markdown/HTML/project skill assets | ledger/workbench docs / yes | No plugin runtime authority; records checkpoint/skill context | Explicitly states plugin runtime is not implemented | `polymath-matrix-build-ledger.zip` |
| REFERENCE | `py-mpc-bench` | Standalone control-system lab | reference-only | HTML/JavaScript + Python via Pyodide | browser lab / local-capable | Browser simulation/control lab only; unrelated to MCP despite original filename | Canonical rename fixes the original `python mcp html.tar` filename/content mismatch | `python mcp html.tar` |
| DEFERRED | `tree-agent-runtime` | Cross-language runtime scaffold | scaffolded | Go + C/C++ + Rust + Kotlin + Protobuf | runtime scaffold / conditional | Control plane and language adapters are separated; no finished Tree-sitter fork/runtime should be inferred | Generation report verifies selected pieces while other integration work remains scaffolded/future | `tree-agent-runtime-one-shot.tar.gz` |
| P2 | `truthframe` | Kotlin/JVM truth/provenance runtime | adapter-needed | Kotlin/JVM | runtime/library; no primary browser UI claimed / local-capable | Truth ledger, capabilities, events and probes live in the Kotlin runtime; consumers receive coherent truth frames | Tests/docs/manifest hashes present; source and compiled JAR are one conceptual entry | `truthframe-kotlin-0.1.0-SNAPSHOT.zip`<br>`truthframe-runtime-0.1.0-SNAPSHOT.jar` |

## First-wave rationale

The first ten are deliberately biased toward **small, inspectable, local-first surfaces** before high-authority or cross-language runtimes. The objective is to prove the Bazaar contract in increasing difficulty:

```text
static HTML fixture
    ↓
read-only utility
    ↓
richer local workbench
    ↓
Go-backed semantic/runtime surface
    ↓
durable storage / local relay
    ↓
state, provenance and memory systems
```

This is an implementation sequence, **not a quality leaderboard**. GRAPHCORE, HTMLChain, VEKTOR, TruthFrame, Nano State/CHEOPS and other ambitious systems may ultimately be more powerful; they are intentionally held until the host manifest, capability, sandbox/bridge, static-projection and evidence contracts have been proven on smaller candidates.

## Admission rule

No entry moves from this planning index into an implemented/admitted registry merely because source exists. Admission should require, at minimum:

1. normalized package identity and version;
2. manifest/schema validation;
3. explicit capability request set;
4. host-side grant/deny behavior;
5. declared authority boundary;
6. reproducible local build or self-contained artifact verification;
7. static/read-only fallback where applicable;
8. test or audit evidence appropriate to the capability level;
9. provenance linking back to the imported source artifact;
10. an implementation-state update in this index or its future machine-readable successor.

Until then, this remains a **planned plugin corpus**, not a plugin registry.
