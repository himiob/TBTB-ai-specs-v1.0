# Architecture Overview – TBTB Global (v1.0)

## 1. Objetivo

Definir la arquitectura base corporativa que debe seguir todo proyecto tecnológico de TBTB Global, asegurando consistencia, escalabilidad, mantenibilidad, seguridad y compatibilidad con desarrollo asistido por Inteligencia Artificial (IA).

Este documento actúa como la **fuente única de verdad arquitectónica** (SSOT) y es consumido por:

- Desarrolladores  
- Líderes técnicos  
- Herramientas de IA (Cursor, Claude, etc.)  
- Revisores de PR  
- Arquitectos de software  
- Documentación técnica  
- QA y seguridad  

---

## 2. Principios Arquitectónicos Fundamentales

1. **Modularidad estricta**  
   Cada módulo debe ser independiente y con responsabilidad clara.

2. **Separación de capas (SoC)**  
   Controllers → Services → Repositories → Database.

3. **IA-Consistent Architecture**  
   La IA debe generar código alineado a esta arquitectura sin improvisar estructuras nuevas.

4. **Evolutiva y escalable**  
   La arquitectura debe soportar crecimiento funcional sin generar deuda técnica.

5. **No acoplamiento**  
   Los módulos deben comunicarse mediante interfaces o servicios, no de forma directa.

6. **Diseño orientado al dominio**  
   El código debe reflejar procesos reales de TBTB (diagnóstico, logística, muestras, workflows, etc.).

7. **Seguridad embebida**  
   La arquitectura debe cumplir siempre con `security-standards.mdc`.

---

## 3. Arquitectura General del Proyecto

Todo proyecto TBTB sigue un enfoque modular basado en **Clean Architecture + Domain-Driven Design (DDD ligera)**.

### 3.1. Estructura mínima obligatoria

src/
modules/
/
controllers/
services/
repositories/
dtos/
entities/
mappers/
tests/
config/
utils/
common/
middlewares/
database/
migrations/

### 3.2. Flujo interno de la arquitectura

Request → Controller → DTO Validation → Service → Repository → Database

Respuesta:

Database → Repository → Service → Mapper → Controller → Response

---

## 4. Módulos (Domain Modules)

Cada módulo representa un dominio funcional dentro de TBTB.

### Ejemplos típicos:

- **patients** (pacientes)  
- **samples** (muestras biológicas)  
- **orders / requests** (solicitudes)  
- **diagnostics** (pruebas)  
- **logistics** (envíos y recolecciones)  
- **users**  
- **auth**  
- **notifications**  
- **reports**  
- **dashboard**  

### Reglas:

- Cada módulo es independiente.  
- No debe existir dependencia circular entre módulos.  
- Los módulos deben comunicarse vía servicios, nunca referencias directas a archivos internos.

---

## 5. Backend Architecture

### 5.1. Capa de Controllers
Responsables de:
- Validar entradas (DTO)
- Enrutar requests
- Delegar la lógica a Services
- Formatear respuestas

### 5.2. Capa de Services
Responsable de la lógica de negocio:
- Validaciones de reglas de negocio  
- Procesamiento de datos  
- Coordinación entre repositorios  
- Flujo “core” del caso de uso  

### 5.3. Capa de Repositories
Responsable de:
- Acceder a la BD  
- Consultas y mutaciones  
- Manejo de ORM (Prisma / Sequelize)  
- Sin lógica de negocio  

### 5.4. Entities
Representan el dominio:
- Estructuras tipadas  
- Invariantes sencillas  
- Definición clara del modelo  

### 5.5. Mappers
Responsables de:
- Convertir entity → DTO
- Convertir DTO → entity
- Evitar exponer datos internos  

---

## 6. Frontend Architecture

### 6.1. Framework principal
- React  
- Next.js (preferido)

### 6.2. Estructura recomendada

src/
components/
ui/
shared/
modules/
/
components/
hooks/
services/
types/
tests/
pages/ (Next.js)
styles/
lib/
utils/
assets/

### 6.3. Reglas
- UI debe provenir del **TBTB UI Kit**.  
- Tokens 100% obligatorios (colores, spacing, radius).  
- Nunca hardcodear estilos fuera del Design System.  
- Toda UI debe corresponder a un diseño en Figma Dev Mode.

---

## 7. Comunicación Frontend ↔ Backend

Toda comunicación debe seguir:

### 7.1. API Specification obligatoria
- `api-spec.yml` define todas las rutas.  
- La IA y los devs deben sincronizarse con este archivo.  

### 7.2. Reglas de contratos
- Frontend nunca debe inventar rutas.  
- Backend nunca debe cambiar contratos sin actualizar OpenAPI.  

### 7.3. Manejo de errores
Toda respuesta debe seguir:

{
success: boolean,
data: {},
error: { code, message } | null
}

### 7.4. Autorización
- Frontend solo usa token via cookies HttpOnly.  
- Backend valida cada request según permisos.  

---

## 8. Integración con IA (Architecture for AI-Assist)

### 8.1. La arquitectura es normativa
La IA **no puede** modificar estructura ni crear subarquetipos nuevos.

### 8.2. Archivos obligatorios para IA
La IA debe consultar:
- `backend-standards.mdc`
- `frontend-standards.mdc`
- `security-standards.mdc`
- `data-model.md`
- `api-spec.yml`
- Este archivo (`architecture-overview.md`)

### 8.3. Prohibido para IA
- Alterar arquitectura sin permiso  
- Crear modules fuera de convenciones  
- Cambiar contratos API sin actualizar OpenAPI  
- Introducir dependencias sin aprobación  

---

## 9. Componentes Transversales

### 9.1. Autenticación (Auth)
Incluye:
- JWT  
- Roles y permisos  
- Middleware obligatorio  

### 9.2. Logs
- Prohibido loggear datos personales  
- Logs estructurados (Pino / Winston)

### 9.3. Config
Toda variable de configuración debe provenir de env:
- Nunca hardcodear URLs, claves, tokens  
- `.env.example` obligatorio  

### 9.4. Middlewares globales
- Error handler  
- Rate limiter  
- Sanitización de inputs  

---

## 10. Infraestructura (Infra Overview)

Proyectos TBTB consideran:

- Bases de datos SQL (Postgres recomendado)
- Servicios de email / SMS externos  
- S3 o almacenamiento similar  
- Servidores serverless o contenedores  
- CI/CD (GitHub Actions)  
- Integraciones con proveedores (laboratorios, logística, etc.)

---

## 11. Diagramas Obligatorios

Todo proyecto debe incluir en `/docs/architecture/`:

### 11.1. Diagrama general de la arquitectura  
Contexto → módulos → integraciones

### 11.2. Diagrama de módulos del backend  
Cómo interactúan controllers / services / repos

### 11.3. Diagrama de flujos internos  
Ejemplo: creación de paciente → solicitud → laboratorio

### 11.4. Diagramas de infraestructura  
Infra + servicios externos

---

## 12. Eventos y Mensajería (si aplica)

- Colas deben documentarse  
- Nombrado consistente  
- Payloads tipados  
- Manejo de reintentos  
- DLQ (Dead Letter Queue) obligatorio si hay colas

---

## 13. Seguridad incorporada en la arquitectura

Toda arquitectura debe cumplir:

- Sanitización de inputs  
- Control de accesos  
- Datos sensibles cifrados  
- Tokens seguros  
- No exponer información médica  
- No incluir secretos en código  

Ver: `security-standards.mdc`.

---

## 14. Escalabilidad

Patrones recomendados:

- División modular  
- Caché para consultas repetidas  
- Lazy loading en frontend  
- Assets optimizados  
- Paginación obligatoria  
- Posible transición a microservicios si es necesario  

---

## 15. Gobernanza

Modificaciones a este archivo requieren:

1. PR en repositorio ai-specs  
2. Revisión de Tech Lead  
3. Revisión de Gerente de Tecnología & Data  
4. Actualización del `CHANGELOG.md`  
5. Comunicación interna al equipo  

---

## 16. Cumplimiento obligatorio

Este archivo es **normativo y vinculante** para:

- todo desarrollo nuevo  
- refactorizaciones  
- proyectos internos  
- productos para clientes  
- agentes IA  

Cualquier excepción debe documentarse y ser aprobada.

---

**Fin del archivo – architecture-overview.md (v1.0)**
