# Official AI Prompts – TBTB Global (v1.0)

## 1. Objetivo

Este documento define los **prompts oficiales** que deben utilizar los desarrolladores y herramientas IA (Cursor, Claude, etc.) dentro de TBTB Global.

Los prompts están diseñados para:

- evitar alucinaciones IA  
- asegurar cumplimiento de ai-specs  
- garantizar consistencia arquitectónica  
- mejorar calidad de código  
- evitar riesgos de seguridad  
- estandarizar flujo de trabajo  
- producir planes técnicos sólidos  
- desarrollar código correcto y mantenible  

Ningún desarrollador debe improvisar prompts — se deben usar siempre los oficiales.

---

# 2. Estructura de Prompts (IA-first)

Todos los prompts deben incluir 3 elementos:

### **(A) Contexto**  
Explicar al modelo qué archivo está tocando, qué historia se desarrolla y qué reglas seguir.

### **(B) Instrucción precisa**  
Qué debe hacer la IA exactamente.

### **(C) Restricciones**  
Lo que la IA NO puede hacer.

---

# 3. Prompt Oficial – Generación de Plan Técnico (OBLIGATORIO)

Usar este prompt SIEMPRE antes de generar código:

Quiero que generes un PLAN TÉCNICO para esta historia. No generes código.

Usa los estándares corporativos de TBTB (backend-standards.mdc, frontend-standards.mdc,
security-standards.mdc, architecture-overview.md, data-model.md y api-spec.yml).

Reglas:
	•	No inventes estructuras nuevas.
	•	No inventes endpoints.
	•	No cambies modelos o arquitectura.
	•	No supongas datos no incluidos en la HU.
	•	Verifica el alcance y las exclusiones.
	•	Cita explícitamente cualquier archivo que debas modificar.

El plan técnico debe incluir:
	1.	Análisis de la historia (scope y out-of-scope)
	2.	Impacto técnico (backend, frontend, API, BD, seguridad)
	3.	Cambios en arquitectura (si aplica)
	4.	Archivos a modificar (con rutas)
	5.	Pasos detallados del desarrollo
	6.	Validaciones necesarias
	7.	Tests obligatorios
	8.	Riesgos IA-first y cómo mitigarlos
	9.	Confirmación de cumplimiento con ai-specs

Al final responde:
“Plan técnico listo para revisión humana”.

---

# 4. Prompt Oficial – Desarrollo de Código Backend

Genera SOLO el código para el backend siguiendo exactamente el plan técnico aprobado.

Reglas:
	•	Respeta backend-standards.mdc.
	•	Usa la arquitectura: controller → service → repository.
	•	Usa DTOs para validar entradas.
	•	Usa mappers para los datos.
	•	No cambies nombres de funciones existentes.
	•	No inventes endpoints ni rutas fuera de api-spec.yml.
	•	No modifiques arquitectura.
	•	No modifiques modelos de datos sin autorización.
	•	No expongas PII o PHI.
	•	Agrega tests unitarios y de integración.
	•	Documenta cada paso con comentarios claros.

Indica qué archivos modificarás y qué agregarás en cada uno.

---

# 5. Prompt Oficial – Desarrollo de Código Frontend

Genera SOLO el código frontend en React/Next.js siguiendo el plan técnico aprobado.

Reglas:
	•	Respeta frontend-standards.mdc.
	•	Usa el Design System TBTB UI Kit.
	•	Usa los tokens oficiales (colores, spacing, radius).
	•	No agregues estilos hardcoded.
	•	Usa Dev Mode Figma para componentes.
	•	No inventes componentes nuevos no definidos en el diseño.
	•	No modifiques UI Kit.
	•	No cambies arquitectura.
	•	Implementa estados (loading, error, empty, success).
	•	Agrega tests con React Testing Library.

Antes de generar código, lista los archivos a modificar.

---

# 6. Prompt Oficial – Revisión de Código (Code Review por IA)

Actúa como revisor técnico senior. Analiza el código proporcionado y verifica:
	1.	Cumplimiento de ai-specs
	2.	Arquitectura (controller → service → repository)
	3.	Seguridad (según security-standards.mdc)
	4.	Consistencia de modelos (data-model.md)
	5.	Contratos API (api-spec.yml)
	6.	Estándares frontend/backend
	7.	Naming conventions
	8.	Test coverage
	9.	Riesgos IA-first
	10.	Código duplicado o innecesario
	11.	Posibles bugs

Indica:
	•	Errores críticos
	•	Advertencias
	•	Mejoras recomendadas
	•	Código sugerido para corregir

---

# 7. Prompt Oficial – Refactor Seguro (usando refactor-plan.mdc)

Realiza un refactor siguiendo estrictamente el REFRACTOR PLAN proporcionado.

Reglas:
	•	No modifiques nada fuera del IN SCOPE.
	•	No alteres arquitectura.
	•	No cambies API contracts.
	•	No cambies modelos de datos.
	•	No elimines lógica existente sin explicación.
	•	No cambies firmas de funciones sin autorización.
	•	Explica cada cambio antes de aplicarlo.
	•	Asegura que los tests pasen.

---

# 8. Prompt Oficial – Tests (Backend y Frontend)

Genera los tests completos para este módulo siguiendo los estándares TBTB.

Incluye:
	•	happy path
	•	error path
	•	edge cases
	•	validación de inputs
	•	validación de permisos
	•	mocks de servicios externos

Usa Jest y Testing Library.
Asegúrate de que los tests cubran la funcionalidad completa.

---

# 9. Prompt Oficial – Seguridad

Evalúa la seguridad del código. Verifica:
	•	exposición de PII/PHI
	•	manejo correcto de JWT
	•	sanitización de inputs
	•	validación de datos
	•	SQL injection
	•	XSS
	•	CSRF
	•	manejo de errores
	•	logs sin datos sensibles

Indica vulnerabilidades y propone soluciones.

---

# 10. Prompt Oficial – Documentación

Genera la documentación completa según documentation-standards.mdc.

Incluye:
	•	actualización del README
	•	actualización del API (si aplica)
	•	documentación de modelo
	•	documentación de arquitectura (si aplica)
	•	explicaciones claras para otros devs
	•	ejemplos

No inventes endpoints, modelos ni arquitectura.

---

# 11. Prompt Oficial – Alineación con Figma (Frontend)

Revisa el diseño en Figma y analiza:
	•	variantes
	•	tokens
	•	autolayout
	•	comportamientos
	•	estados
	•	componentes base

Luego genera el componente React 100% alineado al diseño Dev Mode.

No uses estilos hardcoded.
No cambies tokens.
No inventes variantes.

---

# 12. Prompt Oficial – Evaluación de Riesgos IA

Usa el archivo risks.mdc para evaluar los riesgos IA-first del desarrollo propuesto.

Indica:
	•	riesgos potenciales
	•	alucinaciones posibles
	•	fuzziness
	•	inconsistencias con ai-specs
	•	desviaciones de arquitectura
	•	fallos de seguridad
	•	inventos de API o modelos

Propón mitigaciones específicas.

---

# 13. Prompt Oficial – Auditoría Final de Historia (QA Técnico)

Actúa como auditor técnico. Evalúa si la historia está realmente terminada.

Valida:
	•	cumplimiento de criterios de aceptación
	•	plan técnico ejecutado
	•	código alineado a ai-specs
	•	seguridad
	•	UI fiel a Figma
	•	tests completos
	•	documentación actualizada
	•	PR checklist completo

Indica SÍ/NO si puede ser cerrada, y por qué.

---

# 14. Gobernanza

Cambios a este documento requieren:

1. Pull Request  
2. Justificación técnica  
3. Aprobación del Tech Lead  
4. Aprobación Gerente Tech & Data  
5. Actualización del CHANGELOG  

---

**Fin del documento — prompts.md (v1.0)**
