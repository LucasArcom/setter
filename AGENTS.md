# Contexto del Proyecto: Setter

Setter es una aplicación web integral para la gestión de torneos de vóley.
El objetivo es reemplazar el papel en las planillas de juego, gestionar fixtures, tablas de posiciones, triangulares y llaves de eliminación, y ofrecer vistas públicas compartibles en tiempo real.

## Stack Tecnológico

- **Framework:** SvelteKit (App Router) usando sintaxis de Svelte 5 (Runes, `$props()`, `$state()`).
- **Estilos:** CSS puro.
- **Base de Datos/Backend:** Supabase (Fase posterior - NO implementar conexiones reales aún).
- **Arquitectura actual:** Fase 1 - "Data-Driven UI". Desarrollo de componentes visuales aislados alimentados estrictamente por Mock Data estructurada.

## Estructura de Datos (Core)

- **Multitorneo:** La base de datos será relacional. TODAS las entidades (equipos, partidos, zonas) deben incluir obligatoriamente un `torneo_id` para aislar los datos de cada competición.
- **Cambios Dinámicos:** Propiedades como la `zona` de un equipo son atributos directos del objeto (ej. `equipo.zona = "Zona B"`), permitiendo reasignaciones sin romper la estructura.

## Reglas de Desarrollo (Directivas para la IA)

1. **Svelte 5 Idiomático:** Usa las mejores y más modernas prácticas de Svelte 5. Nada de `export let`, usa `let { propName } = $props();`. Mantén los componentes pequeños y enfocados.
2. **UI First con Mock Data:** NO implementes llamadas a Supabase ni lógicas complejas de estado global/stores todavía. Todo componente visual debe recibir sus datos a través de props mediante objetos de mock data fuertemente tipados/estructurados.
3. **No asumas herramientas externas:** No instales ni uses librerías de UI pesadas a menos que el usuario lo indique explícitamente.
4. **Cero Código Espagueti:** Si un archivo supera las 150-200 líneas, sugiere dividirlo en componentes más pequeños inmediatamente.

## Reglas de Negocio del Vóley (Contexto de Dominio)

Cuando generes lógica de cálculos o mock data, respeta estas reglas estrictas:

- **Puntuación en Fase de Grupos:**
  - Ganar 2-0 = 3 puntos.
  - Ganar 2-1 = 2 puntos.
  - Perder 1-2 = 1 punto.
  - Perder 0-2 = 0 puntos.
- **Categorización:** Los equipos se agrupan por Rama (Femenino/Masculino), Categoría (ej: Sub 14, Sub 16, Sub 18) y Zona (ej: Zona A).
- **Cálculos Requeridos:** Partidos Jugados (PJ), Ganados (PG), Perdidos (PP), Sets a Favor/Contra (SF/SC), Puntos a Favor/Contra (PF/PC).
- **Coeficientes:** Coeficiente de Sets (CS = SF/SC) y Puntos (CP = PF/PC). Si el divisor es 0, el valor es infinito (MAX).
- **Orden de Desempate:** Puntos > Partidos Ganados > Coeficiente de Sets > Coeficiente de Puntos > Resultado entre sí (Head-to-Head).

## Convenciones de Código

- Nombres de componentes en PascalCase (ej: `MatchCard.svelte`).
- Nombres de archivos de rutas siempre en minúsculas (ej: `+page.svelte`, `+layout.svelte`).
- Funciones y variables en camelCase.
- Comentarios en español.
- Código, clases, variables, funciones, etc. en inglés.
