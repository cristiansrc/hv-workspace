# Context Map - HV Ecosystem

## Bounded Contexts

### 1. Resume Management Context (hv-go-ms-resume)
- **Owner**: cristiansrc
- **Responsabilidad**: Gestión completa del CV (CRUD de datos personales, experiencia, habilidades, blog, multimedia)
- **Modelo**: Entidades de dominio propias (BasicData, Experience, Skill, Blog, etc.)
- **Persistencia**: SQLite
- **Upstream**: Ninguno
- **Downstream**: CV Rendering Context (vía HTTP sync)

### 2. CV Rendering Context (hv-py-ms-render-cv)
- **Owner**: cristiansrc
- **Responsabilidad**: Generar PDFs ATS-friendly a partir de datos de CV
- **Modelo**: Schema de RenderCV (YAML → Typst → PDF)
- **Dependencia externa**: RenderCV library + Typst binary
- **Upstream**: Resume Management Context
- **Downstream**: Ninguno

### 3. Public Portal Context (hv-rt-fr-portal)
- **Owner**: cristiansrc
- **Responsabilidad**: Mostrar información pública del CV/Portfolio
- **Upstream**: Resume Management Context (vía API REST)
- **Downstream**: Ninguno

### 4. Admin Panel Context (hv-rt-fr-admin)
- **Owner**: cristiansrc
- **Responsabilidad**: Administrar contenido del CV
- **Upstream**: Resume Management Context (vía API REST)
- **Downstream**: Ninguno

## Context Map Relationships

```
┌─────────────────────┐
│   Public Portal     │ ─── Customer ───▶ ┌─────────────────────┐
│   (hv-rt-fr-portal) │                    │  Resume Management  │
└─────────────────────┘                    │  (hv-go-ms-resume)  │
                                           └────────┬────────────┘
┌─────────────────────┐                             │
│   Admin Panel       │ ─── Customer ───▶           │
│   (hv-rt-fr-admin)  │                             │
└─────────────────────┘                             │
                                                    │ Supplier
                                                    ▼
                                           ┌─────────────────────┐
                                           │   CV Rendering      │
                                           │   (hv-py-ms-render) │
                                           └─────────────────────┘
```

### Relaciones

| Upstream | Downstream | Relación | Contrato |
|---|---|---|---|
| Resume Management | Public Portal | Open Host Service | REST API `/public/*` |
| Resume Management | Admin Panel | Open Host Service | REST API completa + Auth JWT |
| Resume Management | CV Rendering | Customer-Supplier | HTTP POST `/render` (JSON → base64 PDF) |

### Anti-Corruption Layers

- **Frontends**: No requieren ACL porque la API expone DTOs ya adaptados al consumo del frontend
- **CV Rendering**: ms-resume actúa como ACL, transformando sus entidades de dominio al schema YAML de RenderCV
