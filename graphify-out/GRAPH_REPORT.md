# Graph Report - hv-workspace  (2026-05-31)

## Corpus Check
- 6 files · ~1,772 words
- Verdict: corpus is large enough that graph structure adds value.

## Summary
- 47 nodes · 41 edges · 7 communities (6 shown, 1 thin omitted)
- Extraction: 100% EXTRACTED · 0% INFERRED · 0% AMBIGUOUS
- Token cost: 0 input · 0 output

## Graph Freshness
- Built from commit: `21578a80`
- Run `git rev-parse HEAD` and compare to check if the graph is stale.
- Run `graphify update .` after code changes (no API cost).

## Community Hubs (Navigation)
- [[_COMMUNITY_Community 0|Community 0]]
- [[_COMMUNITY_Community 1|Community 1]]
- [[_COMMUNITY_Community 2|Community 2]]
- [[_COMMUNITY_Community 3|Community 3]]
- [[_COMMUNITY_Community 4|Community 4]]
- [[_COMMUNITY_Community 5|Community 5]]
- [[_COMMUNITY_Community 6|Community 6]]

## God Nodes (most connected - your core abstractions)
1. `HV Workspace - Solution Workspace` - 6 edges
2. `Integraciones entre Servicios` - 6 edges
3. `ADR-001: Migración de ms-resume a Go y Separación de Repositorios` - 6 edges
4. `Bounded Contexts` - 5 edges
5. `Integration Map - HV Ecosystem` - 4 edges
6. `Workspace Mapping - HV Ecosystem` - 4 edges
7. `Alternativas Consideradas` - 4 edges
8. `Consecuencias` - 4 edges
9. `Context Map - HV Ecosystem` - 3 edges
10. `Context Map Relationships` - 3 edges

## Surprising Connections (you probably didn't know these)
- None detected - all connections are within the same source files.

## Import Cycles
- None detected.

## Communities (7 total, 1 thin omitted)

### Community 0 - "Community 0"
Cohesion: 0.20
Nodes (9): 1. Resume Management Context (hv-go-ms-resume), 2. CV Rendering Context (hv-py-ms-render-cv), 3. Public Portal Context (hv-rt-fr-portal), 4. Admin Panel Context (hv-rt-fr-admin), Anti-Corruption Layers, Bounded Contexts, Context Map - HV Ecosystem, Context Map Relationships (+1 more)

### Community 1 - "Community 1"
Cohesion: 0.20
Nodes (9): 1. Frontend Público → ms-resume (Sync REST), 2. Admin Panel → ms-resume (Sync REST), 3. ms-resume → ms-render-cv (Sync HTTP Interno), 4. ms-resume → AWS S3 (Sync SDK), 5. ms-resume → Telegram Bot (Sync HTTP), Data Ownership, Error Contract, Integraciones entre Servicios (+1 more)

### Community 2 - "Community 2"
Cohesion: 0.22
Nodes (8): A: Reimplementar RenderCV en Go desde cero, ADR-001: Migración de ms-resume a Go y Separación de Repositorios, Alternativas Consideradas, B: Embeber Python dentro de Go (go-python3), C: Mantener Spring Boot, Contexto, Decisión, Servicios Resultantes

### Community 3 - "Community 3"
Cohesion: 0.29
Nodes (6): Comunicación entre Servicios, Convención de Nombres, Deploy Actual, Estructura del Workspace, HV Workspace - Solution Workspace, Repositorios del Ecosistema

### Community 4 - "Community 4"
Cohesion: 0.40
Nodes (4): Mapeo de Repositorios, Notas, Repositorios Legacy (a deprecar), Workspace Mapping - HV Ecosystem

### Community 5 - "Community 5"
Cohesion: 0.50
Nodes (4): Consecuencias, Negativas, Positivas, Riesgos Mitigados

## Knowledge Gaps
- **31 isolated node(s):** `hv-workspace`, `Repositorios del Ecosistema`, `Estructura del Workspace`, `Convención de Nombres`, `Deploy Actual` (+26 more)
  These have ≤1 connection - possible missing edges or undocumented components.
- **1 thin communities (<3 nodes) omitted from report** — run `graphify query` to explore isolated nodes.

## Suggested Questions
_Questions this graph is uniquely positioned to answer:_

- **Why does `ADR-001: Migración de ms-resume a Go y Separación de Repositorios` connect `Community 2` to `Community 5`?**
  _High betweenness centrality (0.052) - this node is a cross-community bridge._
- **What connects `hv-workspace`, `Repositorios del Ecosistema`, `Estructura del Workspace` to the rest of the system?**
  _31 weakly-connected nodes found - possible documentation gaps or missing edges._