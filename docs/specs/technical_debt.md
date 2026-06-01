# Technical Debt - HV Workspace (Global)

**Workspace**: hv-workspace
**Última actualización**: 2026-06-01

## Consolidación de Deuda Técnica por Proyecto

### hv-go-ms-resume

None. Documentación y código completos.

### hv-py-ms-render-cv

None. Toda la deuda técnica identificada está registrada y gestionada en la Master Spec del proyecto.

## Deuda Técnica Global del Workspace

| Deuda | Impacto | Plan de Mitigación | Estado |
|---|---|---|---|
| hv-dk-infra-cv pendiente | No hay infraestructura como código formalizada para Docker Compose + Nginx | Crear repo con docker-compose.yml, nginx config, y documentación de deploy | 📋 Pendiente |
| Legacy repos aún activos | `cristiansrc/ms-resume`, `cristiansrc/fr-resume`, `cristiansrc/fr-resume-admin`, `cristiansrc/portfolio-cv` siguen activos | Deprecar tras verificación de que los nuevos servicios funcionan en producción | ⏳ En espera |
| Sin CI/CD pipeline | No hay automatización de build/test/deploy | Configurar GitHub Actions para cada repo | 📋 Pendiente |
| Sin observabilidad distribuida | No hay trazabilidad end-to-end entre servicios | Implementar OpenTelemetry o similar | 📋 Pendiente |
