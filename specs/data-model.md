# Data Model – TBTB Global (v1.0)

## 1. Objetivo

Definir los lineamientos y estructuras fundamentales del modelo de datos corporativo de TBTB Global.  
Este documento actúa como la referencia oficial para:

- diseñar bases de datos  
- modelar entidades  
- relacionar dominios  
- generar código con IA  
- validar esquemas  
- documentar información sensible  
- garantizar consistencia entre proyectos  

Todas las entidades, relaciones y reglas aquí definidas deben respetarse en nuevos desarrollos, refactorizaciones y funcionalidades IA-first.

---

## 2. Principios de Modelado de Datos

1. **Consistencia corporativa**  
   Todos los proyectos deben seguir las mismas reglas de nombrado, tipos y relaciones.

2. **Normalización controlada**  
   Modelo basado en 3NF, con desnormalización solo cuando existan motivos de performance comprobados.

3. **Dominio primero**  
   Las entidades deben representar procesos reales de TBTB (diagnóstico, pacientes, muestras, logística, etc.).

4. **IA-consistent schema**  
   La IA debe generar entidades alineadas a este documento y nunca crear modelos no aprobados.

5. **Minimización de datos sensibles**  
   Ninguna entidad debe almacenar información sensible innecesaria.

6. **Trazabilidad**  
   Todo registro debe incluir timestamps y referencias claras.

7. **Relaciones explícitas**  
   Todas las relaciones deben estar definidas con cardinalidad.

---

## 3. Convenciones de Nombres

### 3.1. Entidades
- nombres en **singular**  
- camelCase o PascalCase según convención del proyecto

Ejemplos:
- `Patient`
- `Sample`
- `OrderRequest`
- `DiagnosticTest`

### 3.2. Campos
- snake_case en base de datos  
- camelCase en backend/frontend

### 3.3. Llaves
- PK: `id` (UUID v4 recomendado)  
- FK: `<entity>Id`  

Ejemplos:
- `patientId`
- `orderRequestId`

---

## 4. Entidades Corporativas Base

A continuación se describen las entidades comunes a la mayoría de los proyectos TBTB.

---

## 4.1. **User**

User
	•	id: uuid
	•	firstName: string
	•	lastName: string
	•	email: string (unique)
	•	phone: string | null
	•	role: enum(admin, agent, doctor, coordinator, patient, system)
	•	country: string
	•	status: enum(active, inactive, suspended)
	•	createdAt: datetime
	•	updatedAt: datetime

### Relación:
- Un usuario puede estar asociado a varios dominios (pacientes, médicos, etc.) según rol.

### Notas:
- Nunca almacenar contraseñas directamente.
- Campos sensibles deben respetar `security-standards.mdc`.

---

## 4.2. **Patient**

Patient
	•	id: uuid
	•	firstName: string
	•	lastName: string
	•	documentType: string | null
	•	documentNumber: string | null
	•	birthDate: date | null
	•	gender: enum(male, female, other, undisclosed)
	•	phone: string | null
	•	email: string | null
	•	country: string
	•	city: string | null
	•	address: string | null
	•	createdAt: datetime
	•	updatedAt: datetime

### Relación:
- 1 Patient → N Samples  
- 1 Patient → N DiagnosticRequests  

### Notas:
- Datos altamente sensibles (PII).  
- No se deben loggear jamás.

---

## 4.3. **Sample (Muestra)**

Sample
	•	id: uuid
	•	patientId: uuid (FK)
	•	sampleCode: string (unique)
	•	sampleType: enum(blood, tissue, urine, dna, other)
	•	collectionDate: datetime | null
	•	status: enum(collected, in_transit, delivered, processing, completed, error)
	•	createdAt: datetime
	•	updatedAt: datetime

### Relación:
- Many samples belong to one patient.
- One sample may have many test results.

---

## 4.4. **DiagnosticRequest (Solicitud de Diagnóstico)**

DiagnosticRequest
	•	id: uuid
	•	patientId: uuid (FK)
	•	doctorId: uuid | null (FK)
	•	requestSource: enum(app, whatsapp, email, portal, integration)
	•	status: enum(pending, scheduled, collected, in_lab, completed, cancelled)
	•	createdAt: datetime
	•	updatedAt: datetime

### Relación:
- 1 DiagnosticRequest → N DiagnosticTests  
- FK hacia paciente y médico (si aplica)

---

## 4.5. **DiagnosticTest (Prueba Diagnóstica)**

DiagnosticTest
	•	id: uuid
	•	diagnosticRequestId: uuid (FK)
	•	testCode: string
	•	testName: string
	•	result: string | null
	•	resultValue: string | null
	•	resultUnit: string | null
	•	resultFlag: enum(normal, high, low, critical) | null
	•	performedAt: datetime | null
	•	createdAt: datetime
	•	updatedAt: datetime

### Notas:
- Campos de resultados médicos son extremadamente sensibles.
- Ver `security-standards.mdc`.

---

## 4.6. **Order (Pedido / Orden de Logística)**

Order
	•	id: uuid
	•	sampleId: uuid (FK)
	•	sourceCountry: string
	•	destinationCountry: string
	•	courier: string | null
	•	trackingNumber: string | null
	•	priority: enum(normal, urgent, critical)
	•	status: enum(created, in_transit, customs, delivered, error)
	•	createdAt: datetime
	•	updatedAt: datetime

---

## 4.7. **Notification**

Notification
	•	id: uuid
	•	userId: uuid (FK)
	•	type: enum(email, sms, whatsapp, push)
	•	content: string
	•	status: enum(pending, sent, failed)
	•	createdAt: datetime

---

## 4.8. **AuditLog**

AuditLog
	•	id: uuid
	•	entity: string
	•	entityId: uuid
	•	action: string
	•	performedBy: uuid | ‘system’
	•	timestamp: datetime
	•	metadata: jsonb | null

### Uso:
- Trazabilidad
- Auditorías internas
- Control de accesos

---

## 5. Relaciones Entre Entidades

### 5.1. Diagrama Lógico (Texto)

User 1—N DiagnosticRequest
User 1—N Notification
Patient 1—N DiagnosticRequest
Patient 1—N Sample
Sample 1—N DiagnosticTest
Sample 1—1 Order (opcional)
DiagnosticRequest 1—N DiagnosticTest

### 5.2. Reglas de relación

1. Un **paciente** puede tener **múltiples solicitudes**.  
2. Cada **solicitud** puede generar **varias pruebas**.  
3. Una **muestra** pertenece a un paciente y puede tener múltiples test asociados.  
4. Opcionalmente una muestra puede generar una **orden logística**.  

---

## 6. Campos Sensibles (PII & PHI)

Los siguientes campos requieren **protección reforzada**:

- Nombre completo del paciente  
- Documento de identidad  
- Resultados médicos  
- Datos de contacto  
- Información clínica  
- Signos de alerta  
- Datos de solicitudes diagnósticas  

### Reglas:
- No loggear  
- No almacenar sin cifrado  
- No enviar en respuestas innecesarias  

Ver: `security-standards.mdc`.

---

## 7. Convenciones de Timestamps

Cada entidad debe incluir:

createdAt: datetime
updatedAt: datetime

### Opcional:

deletedAt: datetime | null

(soft deletes permitidos si el proyecto lo define)

---

## 8. Ejemplo de Objeto Unificado

Ejemplo de un flujo completo (simplificado):

```json
{
  "patient": {
    "id": "uuid",
    "firstName": "Ana",
    "lastName": "Gómez"
  },
  "diagnosticRequest": {
    "id": "uuid",
    "status": "in_lab"
  },
  "sample": {
    "id": "uuid",
    "sampleType": "blood"
  },
  "tests": [
    {
      "testName": "ALP",
      "resultValue": "320",
      "resultUnit": "U/L",
      "resultFlag": "high"
    }
  ]
}


⸻

9. Reglas para IA (Data Modeling)

9.1. IA NUNCA debe:
	•	Crear entidades no autorizadas
	•	Crear relaciones no definidas aquí
	•	Modificar el modelo sin actualizar este archivo
	•	Cambiar nombres arbitrariamente
	•	Combinar entidades sin análisis de negocio

9.2. IA DEBE:
	•	Revisar este archivo antes de modelar datos
	•	Mantener consistencia de tipos
	•	Seguir naming conventions
	•	Sugerir impactos en:
	•	API
	•	DB
	•	seguridad

⸻

10. Gobernanza

Modificaciones a este archivo requieren:
	1.	PR en ai-specs
	2.	Justificación técnica y funcional
	3.	Revisión del Tech Lead
	4.	Revisión de Gerente de Tecnología & Data
	5.	Actualizar CHANGELOG.md
	6.	Comunicar impacto al equipo

⸻

11. Cumplimiento Obligatorio

Este archivo es vinculante para:
	•	Backend
	•	Frontend
	•	Móviles
	•	Modelado de BD
	•	IA
	•	Integraciones
	•	Refactorizaciones

Cualquier excepción debe ser aprobada y documentada.

⸻

Fin del documento — data-model.md (v1.0)
