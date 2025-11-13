# TBTB AI-SPECS v1.0  
Estándar corporativo para desarrollo asistido por IA en TBTB Global

---

## 📌 Descripción General

Este repositorio contiene la **versión corporativa oficial** de los estándares técnicos, lineamientos, reglas de seguridad, arquitectura, modelos de datos, prompts y guías que rigen el **desarrollo asistido por Inteligencia Artificial (IA-first)** dentro de TBTB Global.

Su propósito es asegurar que todos los desarrolladores, Tech Leads y herramientas IA (Cursor, Claude, etc.) utilicen una **misma estructura, arquitectura y reglas corporativas**, garantizando calidad, seguridad y consistencia en todos los proyectos.

---

## 🎯 Objetivos del Estándar

El estándar AI-SPECS v1.0 garantiza:

- ✔️ Consistencia técnica en todos los proyectos  
- ✔️ Arquitectura unificada, modular y escalable  
- ✔️ Seguridad, privacidad y cumplimiento normativo  
- ✔️ Integración correcta con herramientas IA  
- ✔️ Desarrollo acelerado con calidad  
- ✔️ Reducción de riesgos y deuda técnica  
- ✔️ Trazabilidad total en decisiones técnicas  

---

## 🔧 ¿Qué incluye este repositorio?

Este repositorio contiene:

### 🧱 **Arquitectura y Modelos**
- Architecture Overview  
- Modelo de Datos Corporativo  
- Especificación API (OpenAPI)

### 🧩 **Estándares Técnicos**
- Backend Standards  
- Frontend Standards  
- Base Standards  
- Documentación  
- Seguridad

### 🤖 **Lineamientos IA-First**
- prompts.md (prompts oficiales)  
- .cursorrules (reglas para Cursor)  
- CLAUDE.md (reglas para Claude)  
- Matriz de Riesgos IA-first  
- Plan de Refactorización  
- Guía de Desarrollo IA-first  

### 📂 **Carpeta de Planes Técnicos**

/ai-specs/changes

Aquí deben guardarse:
- Planes técnicos (SCRUM-XXX-plan.md)
- Planes de refactorización
- Documentos generados por IA durante cada historia

---

## 📁 Estructura del Repositorio

/
specs/
api-spec.yml
architecture-overview.md
backend-standards.mdc
base-standards.mdc
data-model.md
development_guide.md
documentation-standards.mdc
frontend-standards.mdc
glossary.md
prompts.md
refactor-plan.mdc
risks.mdc
security-standards.mdc

ai-specs/
changes/
SCRUM-000-plan.md

.cursorrules
CLAUDE.md
CODEOWNERS
CHANGELOG.md
README.md

---

## 🔄 Cómo usar este repositorio (Metodología IA-first)

### **1. Clonar dentro de cada nuevo proyecto**
Debe colocarse en la raíz del proyecto:

/specs
/ai-specs

### **2. Toda historia SCRUM requiere un Plan Técnico**
Guardar en:

ai-specs/changes/SCRUM-XXX-plan.md

### **3. El desarrollo SIEMPRE debe seguir AI-SPECS**
Ver:
- `/specs/development_guide.md`  
- `/specs/prompts.md`  
- `/specs/security-standards.mdc`  
- `/specs/architecture-overview.md`  

### **4. Todo PR debe validar estándares y seguridad**
Ver:
- `/specs/risks.mdc`  
- `/specs/refactor-plan.mdc`  

### **5. Ningún archivo del estándar puede modificarse sin aprobación**
Ver:
- `CODEOWNERS`  

---

## 🛡️ Gobernanza

Los archivos dentro de `/specs` y el contenido de `.cursorrules`, `CLAUDE.md` y `CHANGELOG.md` **están protegidos**.  
Solo pueden ser modificados mediante PR revisado y aprobado por:

- **Rodrigo Marcano (CGTO)**  
- **Andreina Méndez (Gerente de Tecnología & Data)**  

---

## 📚 Documentación Clave

- **Backend Standards:** [`specs/backend-standards.mdc`](specs/backend-standards.mdc)  
- **Frontend Standards:** [`specs/frontend-standards.mdc`](specs/frontend-standards.mdc)  
- **Seguridad:** [`specs/security-standards.mdc`](specs/security-standards.mdc)  
- **Arquitectura:** [`specs/architecture-overview.md`](specs/architecture-overview.md)  
- **Modelo de Datos:** [`specs/data-model.md`](specs/data-model.md)  
- **Guía de Desarrollo:** [`specs/development_guide.md`](specs/development_guide.md)  
- **Prompts IA:** [`specs/prompts.md`](specs/prompts.md)  
- **Riesgos IA-first:** [`specs/risks.mdc`](specs/risks.mdc)  
- **Plan de Refactorización:** [`specs/refactor-plan.mdc`](specs/refactor-plan.mdc)  

---

## 🧪 Versionado

Este repositorio usa **versionado semántico**.  
La versión actual es:

### **v1.0**

Consultar:

CHANGELOG.md

---

## 👤 Responsables

- **Rodrigo Marcano (CTOO, TBTB Global)**  
- **Andreina Méndez (Gerente de Tecnología & Data)**  

---

## 🟢 Estado Actual

🟩 Estructura completa  
🟩 Estándares listos para producción  
🟩 Compatible con IA (Cursor, Claude)  
🟩 Gobernanza implementada  
🟩 Primer plan técnico cargado  

---

## 🚀 AI-SPECS está listo para adopción en todos los proyectos TBTB.
