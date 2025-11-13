# Frontend Standards – TBTB Global (v1.0)

## 1. Objetivo

Establecer los estándares, convenciones y lineamientos que deben aplicarse a todo desarrollo frontend dentro de TBTB Global, incluyendo desarrollos asistidos por IA (Cursor, Claude u otros).

Estos estándares aseguran consistencia visual, técnica y funcional entre proyectos, minimizan errores y permiten que la IA genere código alineado a la arquitectura y al Design System de TBTB.

---

## 2. Frameworks y Tecnologías Permitidas

### 2.1. Frameworks frontend aprobados
- **React (obligatorio)**
- **Next.js (preferido para aplicaciones web nuevas)**
- Vite + React (solo para microfrontends o apps pequeñas)

### 2.2. Estilos permitidos
- **Design System TBTB UI Kit**
- **CSS-in-JS:** Styled Components o Emotion
- **TailwindCSS** (si el proyecto lo define desde el inicio)
- **CSS Modules** (solo si está documentado en el proyecto)

### 2.3. Librerías aprobadas
- Zustand (estado)
- Redux Toolkit (solo si el proyecto lo requiere)
- React Query / TanStack Query (fetch y caché)
- Axios / Fetch API
- Headless UI / Radix (componentes accesibles)

### 2.4. Prohibido
- jQuery o librerías DOM ilegales
- Inline styles (salvo casos excepcionales)
- Librerías UI que no estén aprobadas por el Tech Lead
- Uso arbitrario de librerías no tipadas

---

## 3. Estructura de Carpetas

La estructura base recomendada es:

```txt
src/
  components/
    ui/
    shared/
  modules/
    <feature>/
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

Reglas:
	•	components/ui contiene componentes base del Design System.
	•	modules/ contiene funcionalidades con arquitectura modular.
	•	pages/ solo define rutas y delega lógica a módulos.

⸻

4. Design System y Tokens

4.1. Uso obligatorio del TBTB UI Kit
	•	Todos los proyectos deben consumir:
	•	Componentes base
	•	Variantes
	•	Tipografía
	•	Variables globales
	•	Tokens de colores, espaciado, radius, sombras y estados

4.2. Tokens obligatorios

Los colores, espaciados, radius y tamaños deben provenir de variables:

Ejemplos:

bg="var(--color-primary-600)"
padding="var(--spacing-4)"
borderRadius="var(--radius-md)"

4.3. Prohibido
	•	Colores hardcoded como #0A1A57
	•	Margins o paddings numéricos arbitrarios
	•	Usar px sin variable aprobada

⸻

5. Componentes – Estandarización

5.1. Requerimientos para componentes

Todo componente debe ser:
	•	Reutilizable
	•	Documentado
	•	Tipado
	•	Agnóstico de lógica de negocio
	•	Compatible con el UI Kit
	•	De fácil testeo

5.2. Estados obligatorios
	•	default
	•	hover
	•	active
	•	disabled
	•	loading (si aplica)
	•	error (si aplica)

5.3. Naming conventions

TBTB.Button.Primary
TBTB.Input.Text
TBTB.Modal.Centered

5.4. Props
	•	Deben estar fuertemente tipadas
	•	Props opcionales deben tener valores por defecto
	•	No abusar del spread operator ...props

⸻

6. Integración con Figma MCP (Multi-Context Provider)

6.1. Reglas Figma → Código
	•	Usar Dev Mode SIEMPRE
	•	Asegurarse que los frames usan:
	•	Autolayout
	•	Tokens correctos
	•	Variantes definidas en el UI Kit

6.2. Lo que la IA debe saber

El desarrollador debe incluir contexto explícito:
	•	ID del frame o componente
	•	Nombre exacto del componente en Figma
	•	Relación entre variantes
	•	Tokens globales usados

6.3. Prohibido
	•	Codificar un componente si no existe en Figma
	•	Interpretar manualmente un diseño sin MCP

⸻

7. Estado y Lógica

7.1. Estado local

Usar:
	•	Hook interno (useState, useReducer)
	•	Zustand para módulos más complejos

7.2. Estado global

Solo si el proyecto lo necesita:
	•	Zustand
	•	Redux Toolkit

7.3. Fetch Data
	•	React Query recomendado para:
	•	caching
	•	retries
	•	parallel fetching
	•	invalidations

7.4. Prohibido
	•	Estado global innecesario
	•	Efectos secundarios no controlados
	•	fetch sin manejo de errores

⸻

8. Accesibilidad (A11y)

Obligatorio para todo componente:
	•	Roles correctos
	•	aria-label o aria-labelledby
	•	Teclado navegable (tabindex)
	•	Contrastes aprobados por WCAG AA
	•	Labels conectados con inputs

Prohibido:
	•	divs interactivos sin role button
	•	manejar foco manual sin necesidad

⸻

9. Seguridad en Frontend
	•	No almacenar tokens en localStorage (solo cookies HttpOnly)
	•	Sanitización de inputs antes de envío al backend
	•	No exponer endpoints internos
	•	No exponer claves de API
	•	Evitar renderizar datos sensibles en consola o logs

⸻

10. Performance

Requiere:
	•	Componentes memoizados si es necesario (React.memo)
	•	Uso de useCallback/useMemo en casos concretos
	•	Lazy loading de módulos grandes
	•	Code splitting automático en Next.js

Prohibido:
	•	Re-render loops innecesarios
	•	N+1 renders en listas
	•	Renderizar listas gigantes sin virtualización

⸻

11. Testing (Obligatorio)

11.1. Herramientas permitidas
	•	Jest
	•	React Testing Library
	•	Playwright (E2E opcional)

11.2. Cobertura mínima
	•	85% del código frontend

11.3. Tipos de pruebas
	•	Unit tests para componentes
	•	Integration tests para flujos
	•	Snapshot tests para UI (opcional)

⸻

12. Uso de IA en Frontend

12.1. La IA NO puede:
	•	Modificar archivos del UI Kit sin aprobación
	•	Crear variantes de componentes no presentes en Figma
	•	Introducir estilos hardcoded
	•	Inventar estados o interacciones no definidas en la historia

12.2. La IA debe:
	•	Seguir estrictamente los tokens del Design System
	•	Respetar naming conventions
	•	Alinear el componente al plano Figma MCP aprobado
	•	Generar tests para cada componente que cree

⸻

13. Manejo de Errores en Frontend
	•	Mostrar errores con componentes estandarizados:
	•	<TBTB.Alert type="error" />
	•	No filtrar errores internos
	•	Loguear errores críticos con un logger aprobado (Sentry o equivalente)

⸻

14. Internacionalización

Reglas:
	•	Usar sistema i18n del proyecto
	•	No hardcodear textos en los componentes
	•	Todos los textos en archivos de traducción

⸻

15. Versionamiento
	•	Cambios mayores → nueva versión del UI Kit
	•	Cambios menores → documentar en CHANGELOG del proyecto
	•	Cualquier cambio en el Design System debe ser aprobado por:
	•	Líder de Design
	•	Líder de Frontend
	•	Tech Lead

⸻

16. Gobernanza

Para modificar este archivo:
	•	Crear un PR en el repositorio ai-specs
	•	Aprobación del Tech Lead
	•	Revisión y aprobación por la Gerente de Tecnología & Data
	•	Registrar el cambio en CHANGELOG.md

⸻

17. Consistencia entre Proyectos
	•	Todos los proyectos frontend de TBTB deben cumplir este estándar
	•	Excepciones requieren aprobación formal
	•	La IA debe ser instruida para usar este documento como referencia base

⸻

Fin del archivo — frontend-standards.mdc (v1.0)
