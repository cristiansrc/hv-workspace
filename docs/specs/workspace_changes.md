# Workspace Changes - HV Workspace

**Última actualización**: 2026-06-01

## Cambios Recientes

### 2026-06-01: Implementación completa de hv-go-ms-resume y hv-py-ms-render-cv

**Tipo**: Implementación de incrementos

**Proyectos afectados**:
- `hv-go-ms-resume`: Incremento `migration-to-go` → `implemented`
- `hv-py-ms-render-cv`: Incrementos `001-foundation-and-hardening` y `002-production-readiness` → `implemented`

**Cambios en el System Landscape**:
- `hv-go-ms-resume`: Estado cambiado de `🔄 En desarrollo` → `✅ Implementado`
- `hv-py-ms-render-cv`: Estado cambiado de `🔄 Migrando` → `✅ Implementado`

**Resumen de implementación**:

#### hv-go-ms-resume
- 18 entidades de dominio (13 existentes + 5 nuevas)
- CRUD completo para todas las entidades
- Autenticación JWT + Altcha
- Rate limiting (público, login, autenticado)
- PDF generation con caché inteligente por hash SHA-256
- Integración con AWS S3 y Telegram Bot
- Migración de datos desde Spring Boot
- OpenAPI 3.1.0 contract (3859 líneas)
- Docker multi-stage con distroless (~10MB)
- Tests de dominio y handlers

#### hv-py-ms-render-cv
- Schema Pydantic estricto para validación de entrada
- Error responses alineados al estándar del workspace (ApiErrorResponse)
- Health check con verificación de Typst
- Trace ID middleware
- Métricas Prometheus (render_requests_total, render_duration_seconds, render_errors_total)
- Graceful shutdown configurado
- Docker hardening (non-root user, sin dev dependencies)
- Tests con cobertura ≥ 85%
- README completo

**Deuda técnica identificada**:
- `hv-dk-infra-cv`: Pendiente crear infraestructura como código
- Legacy repos aún activos (deprecar tras verificación en producción)

**Próximos pasos recomendados**:
1. Crear repo hv-dk-infra-cv con Docker Compose + Nginx
2. Configurar CI/CD con GitHub Actions
3. Verificar funcionamiento en producción antes de deprecar legacy repos
