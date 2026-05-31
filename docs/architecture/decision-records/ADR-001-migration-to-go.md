# ADR-001: Migración de ms-resume a Go y Separación de Repositorios

**Estado**: accepted
**Fecha**: 2026-05-31
**Owner**: cristiansrc

## Contexto

El ecosistema del portfolio/CV actualmente consiste en:
- `ms-resume`: Spring Boot 3.5 + Java 21 + SQLite (API REST)
- `ms-render-cv`: Python 3.12 + FastAPI + RenderCV (generación PDF), embebido dentro de `portfolio-cv`
- `fr-resume`: Next.js 14 (frontend público en Vercel)
- `fr-resume-admin`: React 19 + Refine (admin panel en Vercel)
- `portfolio-cv`: Repo que contiene infra + ms-render-cv

Se identifican los siguientes problemas:
1. `ms-render-cv` está acoplado al repo de infraestructura (`portfolio-cv`)
2. Spring Boot tiene overhead de memoria innecesario para un portfolio personal
3. No hay separación clara de bounded contexts en los repositorios
4. La convención de nombres de repositorios no es consistente

## Decisión

1. **Migrar ms-resume de Spring Boot a Go 1.22+**
   - Stack: Chi router, SQLite (modernc.org/sqlite), golang-migrate, JWT, AWS SDK v2
   - Mantener arquitectura hexagonal (domain, ports, adapters)
   - Mantener 100% compatibilidad con el contrato API actual para no romper los fronts
   - Mantener mismo formato de ErrorResponse

2. **Separar ms-render-cv en repositorio propio**
   - Nuevo repo: `hv-py-ms-render-cv`
   - Mantener Python + RenderCV + Typst (no hay equivalente Go maduro)
   - RenderCV genera PDFs ATS-friendly con validación Pydantic estricta
   - Comunicación vía HTTP interno desde ms-resume

3. **Renombrar todos los repositorios con convención**
   - `hv-go-ms-resume` (Go microservicio resume)
   - `hv-py-ms-render-cv` (Python microservicio render-cv)
   - `hv-rt-fr-portal` (React frontend portal)
   - `hv-rt-fr-admin` (React frontend admin)
   - `hv-dk-infra-cv` (Docker infraestructura CV)

4. **Mantener los frontends sin cambios funcionales**
   - Solo actualizar URLs de API si cambia el dominio
   - El contrato de respuesta se mantiene idéntico

## Alternativas Consideradas

### A: Reimplementar RenderCV en Go desde cero
- **Rechazada**: Requeriría meses de trabajo para replicar validación Pydantic, 8 temas Typst, locales, y ATS compliance. RenderCV tiene 16.8k stars y mantenimiento activo.

### B: Embeber Python dentro de Go (go-python3)
- **Rechazada**: Deployment frágil, doble runtime, memory overhead, debugging complejo.

### C: Mantener Spring Boot
- **Rechazada**: Overhead de memoria (~512MB mínimo vs ~20MB de Go), startup lento, complejidad innecesaria para el scope actual.

## Consecuencias

### Positivas
- Reducción de memoria del servicio principal de ~512MB a ~20MB
- Startup time de segundos a milisegundos
- Separación clara de bounded contexts
- Convención de nombres consistente
- RenderCV actualizable independientemente

### Negativas
- Trabajo de migración de todos los endpoints CRUD
- Necesidad de mantener compatibilidad de contrato API
- Dos lenguajes en el ecosistema (Go + Python)

### Riesgos Mitigados
- **Riesgo**: Los fronts se rompen con el cambio de API
  **Mitigación**: Contrato idéntico, mismo formato de error, mismos paths

- **Riesgo**: RenderCV deja de ser mantenido
  **Mitigación**: Es open source con comunidad activa; si falla, se puede migrar a Typst directo desde Go como fallback

## Servicios Resultantes

| Servicio | Lenguaje | Responsabilidad | Deploy |
|---|---|---|---|
| hv-go-ms-resume | Go | API REST, Auth JWT, CRUD, S3, Telegram | Docker (servidor) |
| hv-py-ms-render-cv | Python | Generación PDF ATS-friendly vía RenderCV | Docker (red interna) |
| hv-rt-fr-portal | Next.js | Frontend público | Vercel |
| hv-rt-fr-admin | React | Panel de administración | Vercel |
