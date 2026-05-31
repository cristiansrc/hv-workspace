# Workspace Mapping - HV Ecosystem

## Mapeo de Repositorios

| Ruta Local | Repositorio Remoto | Bounded Context | Owner | Estado |
|---|---|---|---|---|
| `projects/hv-go-ms-resume` | `github.com/cristiansrc/hv-go-ms-resume` | Resume Management | cristiansrc | 🔄 En desarrollo |
| `projects/hv-py-ms-render-cv` | `github.com/cristiansrc/hv-py-ms-render-cv` | CV Rendering | cristiansrc | 🔄 Migrando |
| `projects/hv-rt-fr-portal` | `github.com/cristiansrc/hv-rt-fr-portal` | Public Portal | cristiansrc | ✅ Activo |
| `projects/hv-rt-fr-admin` | `github.com/cristiansrc/hv-rt-fr-admin` | Admin Panel | cristiansrc | ✅ Activo |
| `projects/hv-dk-infra-cv` | `github.com/cristiansrc/hv-dk-infra-cv` | Deployment Infra | cristiansrc | 📋 Pendiente |

## Repositorios Legacy (a deprecar)

| Repositorio | Reemplazado Por | Estado |
|---|---|---|
| `cristiansrc/ms-resume` | `hv-go-ms-resume` | ⏳ Activo hasta migración completa |
| `cristiansrc/fr-resume` | `hv-rt-fr-portal` | ⏳ Activo hasta migración |
| `cristiansrc/fr-resume-admin` | `hv-rt-fr-admin` | ⏳ Activo hasta migración |
| `cristiansrc/portfolio-cv` | `hv-dk-infra-cv` + `hv-py-ms-render-cv` | ⏳ Activo hasta migración |

## Notas

- La carpeta `projects/` existe en el repo pero su contenido está ignorado por `.gitignore`
- Cada proyecto se clona de forma independiente en su propio repositorio
- Los agentes pueden leer arquitectura macro en la raíz y código en `projects/<repo-name>`
- Los cambios operativos se limitan al repositorio activo salvo instrucción explícita
