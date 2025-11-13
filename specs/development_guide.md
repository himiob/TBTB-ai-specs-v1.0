# Development Guide – TBTB Global (v1.0)

## 1. Objetivo

Este documento define el **flujo oficial de desarrollo IA-first** que deben seguir todos los equipos tecnológicos de TBTB Global. Es la guía que unifica:

- prácticas de desarrollo
- uso de herramientas IA (Cursor, Claude)
- uso de ai-specs
- criterios de calidad
- branching
- PR rules
- documentación
- seguridad
- gobernanza

Este archivo es vinculante y se aplica a todos los proyectos.

---

## 2. Principios del Desarrollo IA-first

1. **La IA es un desarrollador asistente, no un arquitecto.**  
   El desarrollador humano controla, valida y aprueba.

2. **El código debe respetar siempre ai-specs.**  
   (backend, frontend, seguridad, arquitectura, data model)

3. **Ningún código se genera sin un plan técnico aprobado.**

4. **Toda historia requiere:**
   - HU IA  
   - Prompt técnico  
   - Plan técnico IA  
   - Revisión del desarrollador  
   - Aprobación del Tech Lead  

5. **Los PRs deben revisarse con criterios técnicos (no solo funcionales).**

6. **Si la IA no cumple el estándar, se corrige — nunca se acepta.**

---

## 3. Flujo de Desarrollo Completo (End-to-End)

### **1️⃣ Revisión de Historia (HU IA)**  
El desarrollador recibe una historia en formato HU IA:

- Contexto  
- Alcance  
- Exclusiones  
- Diseño Figma  
- Dependencias  
- Criterios de aceptación  
- Prompt técnico IA  
- Impacto técnico esperado  

El desarrollador debe leerla completa antes de trabajar.

---

### **2️⃣ Generación del Plan Técnico con IA**

Solo se usa **Cursor / Claude** para generar el plan.

El plan técnico debe incluir:

- análisis de la historia  
- arquitectura afectada  
- cambios en API  
- cambios en DB  
- cambios en frontend/backend  
- tests necesarios  
- riesgos  
- pasos específicos del desarrollo  

El plan se almacena en:

/ai-specs/changes/SCRUM-XXX-plan.md

**Nadie codifica hasta que el plan esté aprobado.**

---

### **3️⃣ Revisión del Plan Técnico**

El desarrollador debe revisar:

- coherencia con ai-specs  
- coherencia con architecture-overview  
- impacto en seguridad  
- impacto en API  
- impacto en frontend/backend  
- alcance y exclusiones  
- consistencia con diseño (si aplica)  

Si algo está incorrecto → se corrige el plan y se regenera.

---

### **4️⃣ Aprobación del Plan Técnico por Tech Lead**

Sin aprobación NO se inicia el desarrollo.

---

### **5️⃣ Branching del Desarrollo**

Regla corporativa:

main         → rama estable del proyecto
develop      → rama para integración continua (opcional)
feature/*    → trabajo de desarrollo por historia
hotfix/*     → corrección urgente
release/*    → preparación de versiones

Para una historia:

git checkout -b feature/SCRUM-XXX

---

### **6️⃣ Desarrollo IA-first (Código)**

El desarrollador pide a la IA:

- solo lo que está en el plan técnico  
- SIN permitir que invente módulos, servicios, endpoints o estructuras no autorizadas

Reglas:

- IA debe citar qué archivo modificará  
- IA debe justificar cambios  
- IA debe respetar arquitectura  
- IA debe incluir tests  
- IA debe cumplir seguridad  

---

### **7️⃣ Desarrollo Manual (si aplica)**

El desarrollador puede corregir y complementar el código generado.

El desarrollador es responsable final del código.

---

### **8️⃣ Pruebas Locales**

Obligatorio antes de crear el PR:

- correr el backend
- correr el frontend
- ejecutar tests
- validar experiencia usuario
- verificar mensajes de error
- validar reglas de negocio
- validar logs
- validar permisos

---

### **9️⃣ Documentación Actualizada**

Durante el PR, el desarrollador debe actualizar:

- `/docs/api` (si cambia API)  
- `/docs/models` (si cambia BD)  
- `/docs/architecture` (si cambia arquitectura)  
- `/CHANGELOG.md` (si se agrega funcionalidad)  

Nunca se aprueba un PR sin documentación actualizada.

---

### **1️⃣0️⃣ Pull Request (PR)**

Todo PR debe:

- vincular historia SCRUM  
- incluir descripción clara  
- incluir plan técnico aprobado  
- incluir screenshots (si aplica)  
- explicar cambios relevantes  
- listar archivos tocados  
- justificar cambios inesperados  

Regla: **un PR por historia.**

---

### **1️⃣1️⃣ Revisión del PR**

El revisor valida:

- cumplimiento de ai-specs  
- cumplimiento de estándares backend/frontend  
- seguridad  
- calidad de código  
- tests  
- documentación  
- consistencia con el plan  

Si algo no cumple → el PR se rechaza con comentarios.

---

### **1️⃣2️⃣ Merge a Develop o Main**

Dependiendo del proyecto:

- `develop` si existe flujo Gitflow  
- `main` si el proyecto es simple  

Antes del merge:
- resolver conflictos  
- aprobar mínimo 1 reviewer técnico  

---

### **1️⃣3️⃣ Deploy / CI/CD**

El código pasa por:

- CI  
- Build  
- Tests  
- QA  
- Deploy staging  
- Aprobación  
- Deploy a producción  

---

## 4. Reglas de Branching y Versionamiento

### **Ramas obligatorias**
- `main`
- `feature/*`

### **Ramas opcionales según complejidad**
- `develop`
- `release/*`
- `hotfix/*`

### **Versionamiento semántico**
- MAJOR: cambios arquitectónicos o incompatibles  
- MINOR: funcionalidades nuevas  
- PATCH: correcciones  

---

## 5. Convenciones de Código (Resumidas)

### **Backend**
- controllers → services → repositories  
- dto para todas las entradas  
- mapper obligatorio  
- validación con Zod o Class-Validator  
- manejo de errores estándar TBTB  
- logs sin PII  

### **Frontend**
- design system obligatorio  
- tokens obligatorios  
- dev mode figma  
- componentes modulares  
- tests para UI  
- manejo seguro de cookies  

---

## 6. Testing

### **Cobertura mínima**
85%

### **Obligatorio**
- unit tests  
- integration tests  
- tests de error/happy path  
- mocks para servicios externos  

### **Rechazo automático del PR si:**
- no hay tests  
- tests están rotos  
- no cubren los cambios  

---

## 7. Uso de IA – Reglas Corporativas

### La IA **NO PUEDE**:
- crear endpoints nuevos no aprobados  
- modificar arquitectura  
- cambiar modelos de datos  
- ignorar ai-specs  
- exponer información sensible  
- omitir validaciones  
- inventar librerías  
- modificar seguridad  

### La IA **DEBE**:
- usar la arquitectura existente  
- seguir ai-specs  
- generar tests  
- justificar cambios  
- solicitar aclaraciones si algo falta  
- documentar decisiones  

---

## 8. Validaciones de Calidad

Antes de aprobar un PR, deben revisarse:

- estructura coherente  
- nombres consistentes  
- estilo uniforme  
- seguridad cumplida  
- documentación actualizada  
- diseño respetado (si aplica)  
- refactor necesario identificado  

---

## 9. PR Checklist (Extracto)

1. Código generado según plan  
2. IA no inventó estructuras nuevas  
3. Arquitectura respetada  
4. API sincronizada  
5. Seguridad cumplida  
6. Tests completos  
7. Diseño respetado  
8. Documentación lista  
9. Changelog actualizado  
10. Revisión aprobada  

---

## 10. Gobernanza del Desarrollo

Cambios en este documento requieren:

1. Pull Request en ai-specs  
2. Justificación técnica  
3. Aprobación del Tech Lead  
4. Aprobación de la Gerente de Tecnología & Data  
5. Actualización de CHANGELOG  

Este documento se revisa trimestralmente.

---

## 11. Cumplimiento Obligatorio

Este documento es vinculante para:

- desarrolladores  
- tech leads  
- gerencia  
- IA  
- proyectos internos  
- proyectos para clientes  
- refactorizaciones  
- hotfix críticos  

Cualquier excepción debe ser autorizada formalmente.

---

**Fin del documento — development_guide.md (v1.0)**
