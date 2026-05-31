# HV Workspace - Solution Workspace

Workspace de solución para el ecosistema del portfolio/CV de cristiansrc.com.

## Repositorios del Ecosistema

| Repositorio | Tipo | Stack | Bounded Context | Estado |
|---|---|---|---|---|
| [hv-go-ms-resume](https://github.com/cristiansrc/hv-go-ms-resume) | Microservicio | Go 1.22+ | Resume Management | 🔄 En desarrollo |
| [hv-py-ms-render-cv](https://github.com/cristiansrc/hv-py-ms-render-cv) | Microservicio | Python 3.12 + RenderCV | CV Rendering | 🔄 Migrando |
| [hv-rt-fr-portal](https://github.com/cristiansrc/hv-rt-fr-portal) | Frontend | Next.js 14 + React | Public Portal | ✅ Activo |
| [hv-rt-fr-admin](https://github.com/cristiansrc/hv-rt-fr-admin) | Frontend | React 19 + Refine | Admin Panel | ✅ Activo |
| [hv-dk-infra-cv](https://github.com/cristiansrc/hv-dk-infra-cv) | Infraestructura | Docker Compose + Nginx | Deployment | 📋 Pendiente |

## Estructura del Workspace

```
hv-workspace/
├── .gitignore              # Ignora projects/* pero mantiene la carpeta
├── projects/               # Clones locales de cada repositorio
│   └── .gitkeep
├── docs/
│   └── architecture/
│       ├── system-landscape.md
│       ├── context-map.md
│       ├── integration-map.md
│       └── decision-records/
│           └── ADR-001-migration-to-go.md
└── README.md
```

## Convención de Nombres

`hv-<lenguaje>-<tipo>-<nombre>`

- **lenguaje**: `go`, `py`, `rt` (React), `dk` (Docker/Infra)
- **tipo**: `ms` (microservicio), `fr` (frontend)
- **nombre**: identificador del proyecto

## Deploy Actual

- **Frontends**: Vercel (hv-rt-fr-portal, hv-rt-fr-admin)
- **Backend**: Servidor propio con Docker (hv-go-ms-resume + hv-py-ms-render-cv)
- **Gateway**: Nginx como reverse proxy

## Comunicación entre Servicios

```
Frontends (Vercel)
       │ HTTPS
       ▼
   Nginx (servidor)
       │
       ├── /api/resume/*     → hv-go-ms-resume (Go, puerto 8080)
       └── /api/render/*     → hv-py-ms-render-cv (Python, puerto 8000, solo red interna)
```

hv-go-ms-resume se comunica con hv-py-ms-render-cv vía red interna Docker para generación de PDFs.
