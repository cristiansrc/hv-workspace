# Integration Map - HV Ecosystem

## Integraciones entre Servicios

### 1. Frontend Público → ms-resume (Sync REST)

| Propiedad | Valor |
|---|---|
| **Tipo** | Sync HTTP/REST |
| **Protocolo** | HTTPS |
| **Direction** | hv-rt-fr-portal → hv-go-ms-resume |
| **Auth** | Ninguna (endpoints públicos) |
| **Timeout** | 10s |
| **Retry** | No (el frontend maneja error UI) |

**Endpoints consumidos:**
- `GET /v1/ms-resume/public/info-page` → InfoPageResponse (JSON)
- `GET /v1/ms-resume/public/curriculum/{language}` → PDF binary
- `POST /v1/ms-resume/public/contact` → Contact form → Telegram
- `GET /v1/ms-resume/public/challenge` → Altcha challenge

### 2. Admin Panel → ms-resume (Sync REST)

| Propiedad | Valor |
|---|---|
| **Tipo** | Sync HTTP/REST |
| **Protocolo** | HTTPS |
| **Direction** | hv-rt-fr-admin → hv-go-ms-resume |
| **Auth** | JWT Bearer Token |
| **Timeout** | 10s |
| **Retry** | No (el admin maneja error UI) |

**Endpoints consumidos:**
- Todos los endpoints CRUD: `/basic-data/*`, `/experience/*`, `/skill/*`, `/blog/*`, etc.
- `POST /v1/ms-resume/login` → JWT token

### 3. ms-resume → ms-render-cv (Sync HTTP Interno)

| Propiedad | Valor |
|---|---|
| **Tipo** | Sync HTTP |
| **Protocolo** | HTTP (red interna Docker) |
| **Direction** | hv-go-ms-resume → hv-py-ms-render-cv |
| **Auth** | Ninguna (red interna) |
| **Timeout** | 30s (generación PDF puede tardar) |
| **Retry** | 1 reintento |

**Contrato:**
```
POST /render
Request:  { "cv": { ...schema RenderCV... } }
Response: { "pdf_base64": "<base64-encoded-pdf>" }
```

### 4. ms-resume → AWS S3 (Sync SDK)

| Propiedad | Valor |
|---|---|
| **Tipo** | Sync SDK |
| **Protocolo** | HTTPS (AWS SDK v2) |
| **Direction** | hv-go-ms-resume → AWS S3 |
| **Auth** | AWS Access Key + Secret Key |
| **Timeout** | 15s |

**Uso**: Almacenamiento de imágenes y videos del portfolio

### 5. ms-resume → Telegram Bot (Sync HTTP)

| Propiedad | Valor |
|---|---|
| **Tipo** | Sync HTTP |
| **Protocolo** | HTTPS (Telegram Bot API) |
| **Direction** | hv-go-ms-resume → Telegram API |
| **Auth** | Bot Token |
| **Timeout** | 10s |

**Uso**: Notificaciones de mensajes de contacto

## Error Contract

Todos los servicios siguen el mismo formato de error para mantener compatibilidad con los frontends:

```json
{
  "timestamp": "2025-07-16T09:00:00Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Descripción del error",
  "path": "/ruta/que/causo/el/error",
  "validationErrors": [
    {"field": "nombreDelCampo", "message": "Mensaje de validación"}
  ]
}
```

## Data Ownership

| Dato | Fuente de Verdad | Owner | Replicación |
|---|---|---|---|
| Datos personales | hv-go-ms-resume (SQLite) | Resume Context | Ninguna |
| Experiencia laboral | hv-go-ms-resume (SQLite) | Resume Context | Ninguna |
| Habilidades | hv-go-ms-resume (SQLite) | Resume Context | Ninguna |
| Blog | hv-go-ms-resume (SQLite) | Resume Context | Ninguna |
| Imágenes/Videos | AWS S3 | Resume Context | Ninguna |
| PDFs generados | Efímero (no se persisten) | CV Rendering Context | Ninguno |
