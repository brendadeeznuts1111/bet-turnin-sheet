# Reference Registry

Canonical **Ref IDs** for this project. Cite these in specs, code comments, commits, and PRs.

| Document | Role |
|----------|------|
| **REFS.md** (this file) | Human-readable registry (URLs synced to refs.json) |
| [refs.json](refs.json) | Machine-readable SSOT (validated by audit) |
| [README.md](README.md) | Overview; links here for full registry |
| [OUTLINE.md](OUTLINE.md) | Architecture and phases |
| [spec.html](spec.html) | Interactive v2.6 spec |

## Document map

| Need | Start here | Registry | Deep dive |
|------|------------|----------|-----------|
| Overview | [README.md](README.md) (DOC-01) | [REFS.md](REFS.md#prefixes) | [spec.html](spec.html) |
| Architecture & phases | [OUTLINE.md](OUTLINE.md) (DOC-02) | [Cross-ref matrix](#cross-reference-matrix) | [SPEC-08](REFS.md#ref-spec-08) |
| External APIs | [REFS.md#external-references](#external-references) | [refs.json](refs.json) | [OUTLINE API tables](OUTLINE.md#bun-api-references) |
| Audit & signoff | [Registry domain signoffs](#registry-domain-signoffs) · [Operational approvals](#operational-domain-approvals) | [ref-audit.json](ref-audit.json) | [SPEC-10](REFS.md#ref-spec-10) |

---

> **Canonical data:** [refs.json](refs.json) · **Schema:** [refs.schema.json](refs.schema.json)
> **Run:** `bun run audit:refs --fix` · **Gate:** `bun run audit:refs --strict` · **Offline:** `bun run audit:refs:offline` · **Fresh URLs:** `bun run audit:refs --no-cache`
> **Governance:** local audit + [registry domain signoffs](#registry-domain-signoffs) (no GitHub Actions)
> **Last audit:** 2026-06-28 · **Status:** pass · **Refs:** 37 · [JSON](ref-audit.json) · [Report](ref-audit.md)

| Check | Description |
|-------|-------------|
| Zod schema | refs.json structure validated on every run |
| URL health | Parallel HEAD/GET with retry + 24h cache |
| ID drift | All cited Ref IDs exist; unused refs reported |
| Nav contract | spec.html `data-ref` + `REFS.md#ref-*` in registry nav |
| REFS sync | REFS.md table URLs match refs.json |
| Pairings | All pairing refs resolve |
| Cross-ref matrix | `crossRefMatrix` specs and external refs valid |

## Registry domain signoffs (docs audit)

External **documentation** refs are grouped by URL domain. After `bun run audit:refs --strict` passes, record a signoff per registry group (not per ref). Internal groups (SPEC, DOC) follow doc review only.

> **Not the same as** [operational domain approvals](#operational-domain-approvals) (Risk/Finance/Compliance/Operations in [SPEC-10](REFS.md#ref-spec-10)).

| Group | Domain | Refs | Signed off | Notes |
|-------|--------|------|------------|-------|
| [Bun (B01–B08)](#bun-b01-b08) | `bun.com` | B01–B08 | — | Run `--strict`, then `--fix` |
| [Effect (E01–E05)](#effect-e01-e05) | `effect.website` | E01–E05 | — | |
| [grammY/Telegram (T01–T05)](#grammy-telegram-t01-t05) | `grammy.dev` · `core.telegram.org` | T01–T05 | — | Two domains, one signoff row |
| [Google Sheets (S01–S05)](#google-sheets-s01-s05) | `developers.google.com` | S01–S05 | — | |

**Workflow:** audit → strict gate → update signoff date in this table → commit `refs.json` + `ref-audit.json` with `--fix`.

## Operational domain approvals (v2.7)

High-stakes **runtime** sign-offs for bets, settlements, config, and admin actions. Full spec: [SPEC-10](REFS.md#ref-spec-10) · [spec.html#domain-approvals](spec.html#domain-approvals) · Phase [7](OUTLINE.md#phase-7).

| Domain | What needs sign-off | Trigger | Sheet / flow |
|--------|---------------------|---------|--------------|
| **Risk** | Large bets / high exposure | `Risk > big_ticket_threshold` | `BetLog` `Risk_Signoff_*` · `/logbet` |
| **Finance** | Settlements / payouts | `/settleup` or large `/payment` | `PaymentLog` `Finance_Signoff_*` |
| **Compliance** | Partner onboarding / config | New partner or whitelist change | `Approvals` · `Config` |
| **Operations** | Manual edits / overrides | `/editbet`, `--force` | `Approvals` · `AuditLog` |

**Commands:** `/approvals pending` · `/approve <id>` · `/reject <id>`

**Central trail:** `Approvals` tab (see [SPEC-10](REFS.md#ref-spec-10)). Pairing: [domain-approval-flow](#key-pairings).

---

Machine-readable registry: [refs.json](refs.json). Edit JSON first; keep REFS.md table URLs in sync.

```typescript
// B03 — Bun.serve webhook
// E02 — Effect Schema validation
// SPEC-04 — command behavior matrix
```

In prose: *Per **B04** and **SPEC-03**, the daily summary cron…*

### Usage in spec.html (DOC-03)

Every **SPEC-01–SPEC-09** section in [spec.html](spec.html) includes:

- An **h2 ref-pill** linking back to this registry (`#ref-spec-XX`)
- A **ref-bar** (section + related API Ref IDs → `REFS.md`)
- **Inline ref-tags** on tables, rules, code blocks, and demo tabs where applicable

Navigate the spec via sticky nav / sidebar **SPEC-XX** labels, or jump from any tag to the canonical entry here.

---

## Prefixes

| Prefix | Range | Meaning |
|--------|-------|---------|
| **B** | B01–B08 | Bun runtime & APIs |
| **E** | E01–E05 | Effect |
| **T** | T01–T05 | grammY / Telegram |
| **S** | S01–S05 | Google Sheets API |
| **SPEC** | SPEC-01–SPEC-10 | Internal [spec.html](spec.html) sections |
| **DOC** | DOC-01–DOC-04 | Project documents |

---

## External references

### Bun (B01–B08)

<a id="bun-b01-b08"></a>

| Ref ID | Topic | Documentation | Project use | Related SPEC |
|--------|-------|---------------|-------------|--------------|
| [B01](#ref-b01) | Runtime overview | [bun.com/docs](https://bun.com/docs) | TypeScript runtime and tooling | — |
| [B02](#ref-b02) | TypeScript & types | [Runtime → TypeScript](https://bun.com/docs/runtime/typescript) | `bun-types`, strict typing | — |
| [B03](#ref-b03) | HTTP server (`Bun.serve`) | [API → HTTP](https://bun.com/docs/api/http) | Telegram webhook endpoint | [SPEC-08](REFS.md#ref-spec-08) |
| [B04](#ref-b04) | Cron (`Bun.cron`) | [Runtime → Cron](https://bun.com/docs/runtime/cron) | Daily summary, integrity check | [SPEC-03](REFS.md#ref-spec-03) |
| [B05](#ref-b05) | Environment (`Bun.env`) | [Runtime → Env](https://bun.com/docs/runtime/env) | Bot token, sheet ID, cache TTL | [SPEC-02](REFS.md#ref-spec-02) |
| [B06](#ref-b06) | File I/O (`Bun.file`) | [API → File I/O](https://bun.com/docs/api/file-io) | Config JSON, service-account file | — |
| [B07](#ref-b07) | Package manager | [install](https://bun.com/docs/pm/cli/install) | Dependency setup (future) | — |
| [B08](#ref-b08) | Test runner | [Test runner](https://bun.com/docs/test) | Unit/integration tests (future) | — |

### Effect (E01–E05)

<a id="effect-e01-e05"></a>

| Ref ID | Topic | Documentation | Project use | Related SPEC |
|--------|-------|---------------|-------------|--------------|
| [E01](#ref-e01) | Overview | [effect.website/docs](https://effect.website/docs) | Typed services, error handling | — |
| [E02](#ref-e02) | Schema | [Schema introduction](https://effect.website/docs/schema/introduction/) | Command + config validation | [SPEC-02](REFS.md#ref-spec-02), [SPEC-05](REFS.md#ref-spec-05) |
| [E03](#ref-e03) | Layers & services | [Requirements management](https://effect.website/docs/requirements-management/layers) | `ConfigService`, `SheetApiService` | [SPEC-08](REFS.md#ref-spec-08) |
| [E04](#ref-e04) | Retry | [Retrying](https://effect.website/docs/error-management/retrying) | Cron failure recovery | [SPEC-03](REFS.md#ref-spec-03) |
| [E05](#ref-e05) | `Effect.gen` | [Getting started](https://effect.website/docs/getting-started/introduction) | Cron workflows, handlers | [SPEC-03](REFS.md#ref-spec-03) |

### grammY & Telegram (T01–T05)

<a id="grammy-telegram-t01-t05"></a>

| Ref ID | Topic | Documentation | Project use | Related SPEC |
|--------|-------|---------------|-------------|--------------|
| [T01](#ref-t01) | grammY guide | [grammy.dev/guide](https://grammy.dev/guide/) | Bot setup, command routing | [SPEC-04](REFS.md#ref-spec-04) |
| [T02](#ref-t02) | Webhooks | [Deployment — Webhooks](https://grammy.dev/guide/deployment-types.html) | Webhook via B03 | [SPEC-08](REFS.md#ref-spec-08) |
| [T03](#ref-t03) | Inline keyboards | [Keyboard plugin](https://grammy.dev/plugins/keyboard.html) | Big-ticket Confirm/Cancel | [SPEC-05](REFS.md#ref-spec-05), [SPEC-07](REFS.md#ref-spec-07), [SPEC-09](REFS.md#ref-spec-09), [SPEC-10](REFS.md#ref-spec-10) |
| [T04](#ref-t04) | Forum topics | [Bot API — forum topics](https://core.telegram.org/bots/api#forum-topic-edited) | `message_thread_id` mapping | [SPEC-04](REFS.md#ref-spec-04), [SPEC-07](REFS.md#ref-spec-07) |
| [T05](#ref-t05) | Bot API | [core.telegram.org/bots/api](https://core.telegram.org/bots/api) | Updates, callbacks | [SPEC-04](REFS.md#ref-spec-04) |

### Google Sheets (S01–S05)

<a id="google-sheets-s01-s05"></a>

| Ref ID | Topic | Documentation | Project use | Related SPEC |
|--------|-------|---------------|-------------|--------------|
| [S01](#ref-s01) | Overview | [API concepts](https://developers.google.com/sheets/api/guides/concepts) | Spreadsheet and tab layout | [SPEC-06](REFS.md#ref-spec-06) |
| [S02](#ref-s02) | Append rows | [Values — append](https://developers.google.com/sheets/api/guides/values#append_values) | BetLog, PaymentLog, AuditLog | [SPEC-06](REFS.md#ref-spec-06) |
| [S03](#ref-s03) | Read values | [Values — read](https://developers.google.com/sheets/api/guides/values) | Config tab, cron reads | [SPEC-02](REFS.md#ref-spec-02) |
| [S04](#ref-s04) | Service account | [Authorizing](https://developers.google.com/sheets/api/guides/authorizing#service-account) | Credentials | — |
| [S05](#ref-s05) | REST append | [values.append](https://developers.google.com/sheets/api/reference/rest/v4/spreadsheets.values/append) | HTTP API reference | [SPEC-06](REFS.md#ref-spec-06) |

<!-- external ref anchors -->
<a id="ref-b01"></a><a id="ref-b02"></a><a id="ref-b03"></a><a id="ref-b04"></a><a id="ref-b05"></a><a id="ref-b06"></a><a id="ref-b07"></a><a id="ref-b08"></a>
<a id="ref-e01"></a><a id="ref-e02"></a><a id="ref-e03"></a><a id="ref-e04"></a><a id="ref-e05"></a>
<a id="ref-t01"></a><a id="ref-t02"></a><a id="ref-t03"></a><a id="ref-t04"></a><a id="ref-t05"></a>
<a id="ref-s01"></a><a id="ref-s02"></a><a id="ref-s03"></a><a id="ref-s04"></a><a id="ref-s05"></a>

---

## Internal spec sections (SPEC-01–SPEC-10)

<a id="internal-spec-sections"></a>

Sections in [spec.html](spec.html). Use when citing project requirements (not external APIs).

| Ref ID | Section | spec.html | Related external Ref IDs |
|--------|---------|-----------|--------------------------|
| [SPEC-01](#ref-spec-01) | Changelog | [#changelog](spec.html#changelog) | — |
| [SPEC-02](#ref-spec-02) | Hub & partner config | [#hub-config](spec.html#hub-config) | [E02](REFS.md#ref-e02), [B05](REFS.md#ref-b05), [S03](REFS.md#ref-s03) |
| [SPEC-03](#ref-spec-03) | Scheduled jobs | [#scheduled-jobs](spec.html#scheduled-jobs) | [B04](REFS.md#ref-b04), [E04](REFS.md#ref-e04), [E05](REFS.md#ref-e05) |
| [SPEC-04](#ref-spec-04) | Command matrix | [#command-matrix](spec.html#command-matrix) | [T01](REFS.md#ref-t01), [T04](REFS.md#ref-t04), [T05](REFS.md#ref-t05) |
| [SPEC-05](#ref-spec-05) | Edge cases | [#edge-cases](spec.html#edge-cases) | [E02](REFS.md#ref-e02), [T03](REFS.md#ref-t03) |
| [SPEC-06](#ref-spec-06) | Sheet contracts | [#sheet-contracts](spec.html#sheet-contracts) | [S01](REFS.md#ref-s01), [S02](REFS.md#ref-s02), [S05](REFS.md#ref-s05) |
| [SPEC-07](#ref-spec-07) | Rules summary | [#rules-summary](spec.html#rules-summary) | [T03](REFS.md#ref-t03), [T04](REFS.md#ref-t04), [B04](REFS.md#ref-b04) |
| [SPEC-08](#ref-spec-08) | Architecture | [#architecture](spec.html#architecture) | [B03](REFS.md#ref-b03), [B04](REFS.md#ref-b04), [T02](REFS.md#ref-t02), [E03](REFS.md#ref-e03) |
| [SPEC-09](#ref-spec-09) | Interactive demo | [#mockup](spec.html#mockup) | [T03](REFS.md#ref-t03), [T04](REFS.md#ref-t04) |
| [SPEC-10](#ref-spec-10) | Domain approvals | [#domain-approvals](spec.html#domain-approvals) | [S02](REFS.md#ref-s02), [E02](REFS.md#ref-e02), [T03](REFS.md#ref-t03) |

<a id="ref-spec-01"></a><a id="ref-spec-02"></a><a id="ref-spec-03"></a><a id="ref-spec-04"></a><a id="ref-spec-05"></a>
<a id="ref-spec-06"></a><a id="ref-spec-07"></a><a id="ref-spec-08"></a><a id="ref-spec-09"></a><a id="ref-spec-10"></a>

---

## Project documents (DOC-01–DOC-04)

<a id="project-documents"></a>

| Ref ID | Document | Description |
|--------|----------|-------------|
| [DOC-01](#ref-doc-01) | [README.md](README.md) | Overview and quick reference |
| [DOC-02](#ref-doc-02) | [OUTLINE.md](OUTLINE.md) | Architecture, phases, acceptance criteria |
| [DOC-03](#ref-doc-03) | [spec.html](spec.html) | Full v2.6 spec — every section tagged with SPEC-XX ref-bars |
| [DOC-04](#ref-doc-04) | [REFS.md](REFS.md) | This registry |

<a id="ref-doc-01"></a><a id="ref-doc-02"></a><a id="ref-doc-03"></a><a id="ref-doc-04"></a>

---

## Cross-reference matrix

Quick lookup: spec section → external refs → implementation phase ([OUTLINE](OUTLINE.md#implementation-phases)). Machine-readable copy: [refs.json](refs.json) `crossRefMatrix`.

| SPEC | External Ref IDs | OUTLINE phase |
|------|------------------|---------------|
| [SPEC-02](REFS.md#ref-spec-02) | [E02](REFS.md#ref-e02), [B05](REFS.md#ref-b05), [S03](REFS.md#ref-s03) | [Phase 1](OUTLINE.md#phase-1) |
| [SPEC-03](REFS.md#ref-spec-03) | [B04](REFS.md#ref-b04), [E04](REFS.md#ref-e04), [E05](REFS.md#ref-e05) | [Phase 4](OUTLINE.md#phase-4) · [Phase 5](OUTLINE.md#phase-5) |
| [SPEC-04](REFS.md#ref-spec-04) | [T01](REFS.md#ref-t01), [T04](REFS.md#ref-t04), [T05](REFS.md#ref-t05) | [Phase 2](OUTLINE.md#phase-2) |
| [SPEC-05](REFS.md#ref-spec-05) | [E02](REFS.md#ref-e02), [T03](REFS.md#ref-t03) | [Phase 2](OUTLINE.md#phase-2) · [Phase 3](OUTLINE.md#phase-3) |
| [SPEC-06](REFS.md#ref-spec-06) | [S01](REFS.md#ref-s01), [S02](REFS.md#ref-s02), [S05](REFS.md#ref-s05) | [Phase 2](OUTLINE.md#phase-2) |
| [SPEC-07](REFS.md#ref-spec-07) | [T03](REFS.md#ref-t03), [T04](REFS.md#ref-t04) | [Phase 3](OUTLINE.md#phase-3) |
| [SPEC-08](REFS.md#ref-spec-08) | [B03](REFS.md#ref-b03), [T02](REFS.md#ref-t02), [E03](REFS.md#ref-e03) | [Phase 0](OUTLINE.md#phase-0) · [Phase 2](OUTLINE.md#phase-2) |
| [SPEC-09](REFS.md#ref-spec-09) | [T03](REFS.md#ref-t03), [T04](REFS.md#ref-t04) | [Phase 3](OUTLINE.md#phase-3) · [Phase 6](OUTLINE.md#phase-6) |
| [SPEC-10](REFS.md#ref-spec-10) | [S02](REFS.md#ref-s02), [E02](REFS.md#ref-e02), [T03](REFS.md#ref-t03) | [Phase 7](OUTLINE.md#phase-7) |

---

## Key pairings

| Use case | Ref IDs |
|----------|---------|
| Webhook server | [B03](REFS.md#ref-b03) + [T02](REFS.md#ref-t02) + [SPEC-08](REFS.md#ref-spec-08) |
| Cron daily summary | [B04](REFS.md#ref-b04) + [E04](REFS.md#ref-e04) + [E05](REFS.md#ref-e05) + [SPEC-03](REFS.md#ref-spec-03) |
| Big-ticket confirm | [T03](REFS.md#ref-t03) + [SPEC-05](REFS.md#ref-spec-05) + [SPEC-07](REFS.md#ref-spec-07) + [SPEC-09](REFS.md#ref-spec-09) |
| Topic → partner mapping | [T04](REFS.md#ref-t04) + [SPEC-04](REFS.md#ref-spec-04) + [SPEC-07](REFS.md#ref-spec-07) |
| Log bet to sheet | [E02](REFS.md#ref-e02) + [S02](REFS.md#ref-s02) + [SPEC-04](REFS.md#ref-spec-04) + [SPEC-06](REFS.md#ref-spec-06) |
| Live config reload | [S03](REFS.md#ref-s03) + [E02](REFS.md#ref-e02) + [SPEC-02](REFS.md#ref-spec-02) |
| Parser validation errors | [E02](REFS.md#ref-e02) + [SPEC-05](REFS.md#ref-spec-05) |
| Domain-specific approvals | [SPEC-10](REFS.md#ref-spec-10) + [SPEC-06](REFS.md#ref-spec-06) + [SPEC-04](REFS.md#ref-spec-04) + [S02](REFS.md#ref-s02) + [E02](REFS.md#ref-e02) + [T03](REFS.md#ref-t03) |

---

## Index by prefix

| Prefix | IDs |
|--------|-----|
| Bun | [B01](REFS.md#ref-b01) · [B02](REFS.md#ref-b02) · [B03](REFS.md#ref-b03) · [B04](REFS.md#ref-b04) · [B05](REFS.md#ref-b05) · [B06](REFS.md#ref-b06) · [B07](REFS.md#ref-b07) · [B08](REFS.md#ref-b08) |
| Effect | [E01](REFS.md#ref-e01) · [E02](REFS.md#ref-e02) · [E03](REFS.md#ref-e03) · [E04](REFS.md#ref-e04) · [E05](REFS.md#ref-e05) |
| grammY/Telegram | [T01](REFS.md#ref-t01) · [T02](REFS.md#ref-t02) · [T03](REFS.md#ref-t03) · [T04](REFS.md#ref-t04) · [T05](REFS.md#ref-t05) |
| Google Sheets | [S01](REFS.md#ref-s01) · [S02](REFS.md#ref-s02) · [S03](REFS.md#ref-s03) · [S04](REFS.md#ref-s04) · [S05](REFS.md#ref-s05) |
| Spec sections | [SPEC-01](REFS.md#ref-spec-01) … [SPEC-10](REFS.md#ref-spec-10) |
| Documents | [DOC-01](REFS.md#ref-doc-01) · [DOC-02](REFS.md#ref-doc-02) · [DOC-03](REFS.md#ref-doc-03) · [DOC-04](REFS.md#ref-doc-04) |
