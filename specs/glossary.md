# Glossary – TBTB Global (v1.0)

## 1. Objetivo
Este glosario define los términos técnicos, de negocio y de Inteligencia Artificial utilizados dentro de TBTB Global.  
Es una referencia obligatoria para:

- desarrolladores  
- líderes técnicos  
- producto  
- diseño  
- QA  
- herramientas IA (Cursor, Claude, etc.)  

Este archivo estandariza el vocabulario corporativo para evitar ambigüedades y mejorar la precisión en desarrollo IA-first.

---

# 2. Términos de Negocio (Business & Operations)

### **Patient**
Persona para la cual se realiza un proceso diagnóstico.

### **Diagnostic Request**
Solicitud que un médico o paciente realiza para iniciar un proceso diagnóstico dentro de un programa.

### **Diagnostic Test**
Prueba específica realizada dentro de una solicitud diagnóstica (ej: ALP, biomarcadores, genética).

### **Sample (Muestra)**
Unidad biológica (sangre, tejido, orina, etc.) que se recolecta para realizar pruebas.

### **Sample Code**
Identificador único asignado a una muestra.

### **Order (Logistics Order)**
Orden logística asociada a una muestra para su transporte entre países o laboratorios.

### **Program (Programa Diagnóstico)**
Arquitectura operativa y tecnológica que TBTB implementa para clientes farmacéuticos.

### **Courier**
Proveedor de transporte encargado de mover muestras.

### **Request Source**
Origen de una solicitud diagnóstica:
- app  
- WhatsApp  
- email  
- portal  
- integración externa  

### **Status Operacionales**
Estados estandarizados para solicitudes, muestras y pruebas:
- pending  
- collected  
- in_lab  
- processing  
- completed  
- error  
- cancelled  

### **DSP / PSP**
Programas de soporte diagnóstico (Diagnostic Support Program) o soporte a pacientes.

---

# 3. Términos Técnicos (Software & Architecture)

### **Module**
Unidad funcional dentro del backend o frontend, basada en dominio.

### **Controller**
Capa responsable de recibir requests HTTP y delegar a servicios.

### **Service**
Contiene la lógica de negocio del módulo.

### **Repository**
Capa de acceso a datos (base de datos) responsable de operaciones CRUD.

### **Entity**
Representación del modelo de datos dentro del dominio.

### **DTO (Data Transfer Object)**
Objeto usado para validar y transportar datos entre capas.

### **Mapper**
Convierte entidades a DTOs y viceversa.

### **Middleware**
Funciones que interceptan requests para validación, autenticación o manejo de errores.

### **OpenAPI / api-spec.yml**
Documento que define los contratos oficiales de la API.

### **Architecture Overview**
Documento que describe cómo funcionan y se conectan todos los módulos.

### **Design System**
Sistema de diseño corporativo que define componentes, tokens, colores, espaciado, tipografías.

### **Tokens (UI Tokens)**
Variables globales de diseño:
- colores  
- espaciado  
- tamaños  
- radio de bordes  
- sombras  
- tipografía  

### **Dev Mode (Figma)**
Modo de Figma que muestra propiedades técnicas para desarrollo.

---

# 4. Términos de Seguridad

### **PII (Personally Identifiable Information)**
Información que identifica directamente a una persona (ej: documento, dirección, email).

### **PHI (Protected Health Information)**
Información médica protegida (resultados de pruebas, biomarcadores, diagnósticos).

### **Sanitización**
Proceso de limpiar y validar inputs.

### **JWT (JSON Web Token)**
Mecanismo de autenticación basado en tokens.

### **HttpOnly Cookie**
Cookie segura que no es accesible desde JavaScript.

### **AuditLog**
Registro de acciones críticas para trazabilidad.

### **Least Privilege Principle**
Principio donde cada usuario solo tiene el mínimo acceso necesario.

---

# 5. Términos IA-First (Inteligencia Artificial)

### **Plan Técnico**
Documento generado por la IA antes de escribir código donde define:
- impacto técnico  
- pasos detallados  
- archivos a modificar  
- riesgo y mitigación  
- cumplimiento con ai-specs  

Obligatorio antes de cualquier desarrollo.

### **Alucinación (AI Hallucination)**
Cuando la IA inventa:
- entidades  
- endpoints  
- módulos  
- estructuras  
- lógica que no existe  
- dependencias  
- detalles no incluidos en la historia  

Prohibido aceptar código con alucinaciones.

### **Fuzziness**
Inconsistencias, ambigüedad o respuestas parcialmente correctas generadas por IA.

### **Scope Creep IA**
Cuando la IA agrega más de lo solicitado en la historia.

### **AI Drift**
Cuando la IA deja de seguir estándares y empieza a generar código inconsistente.

### **AI Enforcement**
Proceso mediante el cual el desarrollador obliga a la IA a seguir ai-specs.

---

# 6. Términos de Metodología y Procesos

### **HU IA (Historia de Usuario IA-first)**
Historia extendida que incluye:
- contexto  
- alcance  
- diseño  
- criterios  
- exclusiones  
- prompt técnico  
- impacto técnico  

### **SCRUM-XXX**
Convención de numeración de historias.

### **PR (Pull Request)**
Solicitud de merge donde se revisa el código.

### **Branching**
Uso de ramas en Git:
- main  
- develop  
- feature/*  
- hotfix/*  
- release/*  

### **CHANGELOG**
Historial de cambios del proyecto.

### **Refactor Plan**
Plantilla obligatoria antes de cualquier refactor.

### **SSOT (Single Source of Truth)**
Repositorio único y oficial para estándares:
- ai-specs  

---

# 7. Estados y Terminología de Logs / Mensajes

### **success**
Operación completada sin errores.

### **error**
Error en el proceso.

### **failed**
El proceso falló en ejecución.

### **pending**
A la espera de procesamiento.

### **processing**
En estado de ejecución.

---

# 8. Tipos de Tests

### **Unit Test**
Prueba unidades aisladas (funciones, servicios, componentes).

### **Integration Test**
Prueba módulos conectados entre sí.

### **E2E (End to End)**
Prueba el flujo completo desde el frontend al backend.

### **Mock**
Simulación controlada de servicios externos.

---

# 9. Roles Técnicos

### **Tech Lead**
Responsable de revisar y aprobar planes técnicos y PRs.

### **Developer**
Ejecuta desarrollo IA-first y revisa planes.

### **Gerente de Tecnología & Data**
Gobernanza de ai-specs y estándares.

### **CGTO**
Lidera estrategia tecnológica, define lineamientos globales, valida impacto de alto nivel.

---

# 10. Gobernanza

La modificación de este archivo requiere:

1. Pull Request  
2. Justificación técnica  
3. Aprobación del Tech Lead  
4. Aprobación de Gerente Tech & Data  
5. Actualización del CHANGELOG  

---

**Fin del documento — glossary.md (v1.0)**
