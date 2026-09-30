# Enterprise systems knowledge catalog

This folder documents the knowledge embedded in [`../index.html`](../index.html). The graph is self-contained: its records are JavaScript constants in that file and are converted into nodes and relationships in the browser.

Use [`../index.html?view=table`](../index.html?view=table) to browse the complete node and relationship records in tabular form, filter them, or export the current result as CSV.

## Data inventory

| Source constant | Contains | Record shape | Records | Graph result |
|---|---|---|---:|---|
| `DOM` | Business domains | `[id, name]` | 5 | `Domain` nodes |
| `SYS` | Enterprise system categories | `[id, name, domainId, description]` | 42 | `SystemType` nodes and `BELONGS_TO` edges |
| `IND` | Industries | `[id, name]` | 14 | `Industry` nodes |
| `FEAT` | Business capabilities and their providers | `[id, name, systemIds[]]` | 55 | `Feature` nodes and 72 `COVERS` edges |
| `P` | Representative products by system and lifecycle | `{ systemId: { l: [], m: [], x: [] } }` | 209 products | Product nodes and `IMPLEMENTS` edges |
| `MIG` | Named product migration paths | `[legacyProduct, modernProduct]` | 16 | `MIGRATES_TO` edges |
| `UIN` | System-to-industry usage | `[systemId, industryIds[]]` | 38 mappings | `USED_IN` edges |
| `INTEG` | System-to-system integrations | `[sourceSystemId, targetSystemId]` | 25 | `INTEGRATES_WITH` edges |
| Generated rules | Middleware, storage, analytics, governance and security links | Explicit system ID lists | 20 mappings | Five operational edge types |

## Node types

| Node label | Count | Meaning | Important fields |
|---|---:|---|---|
| `Domain` | 5 | Top-level business grouping | `id`, `name`, `dom` |
| `SystemType` | 42 | Category of enterprise application | `id`, `name`, `dom`, `desc` |
| `Feature` | 55 | Business or technical capability | `id`, `name`, `dom` |
| `Industry` | 14 | Industry where systems are used | `id`, `name` |
| `LegacyProduct` | derived from `P.l` | Representative legacy/on-premises product | `name`, `status`, `hosting`, `sys` |
| `ModernProduct` | derived from `P.m` | Representative modern/cloud product | `name`, `status`, `hosting`, `sys` |
| `HybridProduct` | derived from `P.x` | Product whose deployment varies by version | `name`, `status`, `hosting`, `sys` |
| **All product labels** | **209** | Combined product catalog | — |
| **Total** | **325** | All graph nodes | — |

## Relationship types

| Relationship | Count | From → to | Meaning |
|---|---:|---|---|
| `BELONGS_TO` | 42 | System → Domain | Places a system in its primary domain |
| `COVERS` | 72 | System → Feature | A system provides a capability |
| `IMPLEMENTS` | 209 | Product → System | A product implements a system category |
| `MIGRATES_TO` | 16 | Legacy product → Modern product | Representative modernization path |
| `USED_IN` | 38 | System → Industry | Industry relevance |
| `INTEGRATES_WITH` | 25 | System → System | Common application integration |
| `ORCHESTRATES` | 6 | Middleware → System | Middleware coordinates a system |
| `STORES_DATA_IN` | 5 | System → Database | Operational persistence |
| `READS_FROM` | 2 | BI → Source system | Analytics consumption |
| `GOVERNS_DATA_OF` | 3 | MDM → System | Master-data governance |
| `SECURES` | 4 | IAM → System | Identity and access protection |
| **Total** | **422** | — | All graph relationships |

## ID conventions

| Prefix | Example | Entity |
|---|---|---|
| `d:` | `d:core` | Domain |
| `s:` | `s:erp` | System type |
| `f:` | `f:gl` | Feature |
| `i:` | `i:mfg` | Industry |
| `p:` | `p:erp:l0` | Product; system, lifecycle bucket and position are encoded |

## Scope and quality notes

- Products are representative examples, not a complete vendor catalog.
- `Modern`, `Legacy`, and hosting values are orientation labels, not vendor lifecycle guarantees.
- Migration links show common conceptual paths; they do not imply direct technical upgrade compatibility.
- Vendor support dates, licensing, deployment options, and product names should be verified before using the data for a purchasing or migration decision.
