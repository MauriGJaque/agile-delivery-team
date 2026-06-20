# ADR-0001 · Monolito modular en lugar de microservicios

**Estado:** aceptado
**Fecha:** 2026-06-20

---

## Contexto y fuerza

El SIC v1 fue construido en cascada como un bloque rígido: cualquier ajuste exige
una nueva versión completa del sistema, lo que congela la mejora continua
(`Fundador.md`, R-11). La dirección y el equipo coinciden en que el v2 debe ser
modificable y extensible de forma iterativa.

Al mismo tiempo, el equipo es pequeño (contexto universitario), el presupuesto es
ajustado y el MVP cubre tres épicas acotadas con nueve historias. No hay evidencia
en el discovery de cargas de tráfico que justifiquen distribución.

---

## Decisión

Se adopta una **arquitectura de monolito modular**: un único proceso desplegable,
dividido internamente en módulos cohesivos con responsabilidades claras (Módulo de
Convenios, Motor de Alertas, Módulo de Cierre, Motor de Estado). Los módulos se
comunican por llamadas internas, no por red.

---

## Alternativas consideradas

- **Microservicios** — Cada módulo como servicio independiente. Descartado: añade
  complejidad operativa (service discovery, trazabilidad distribuida, deploys
  coordinados) que el equipo no necesita ni puede sostener en esta fase. Viola el
  principio de maximizar trabajo no hecho.
- **Monolito sin módulos (igual que v1)** — Descartado: reproduce exactamente el
  problema que el discovery documenta (rigidez, imposibilidad de cambiar una parte
  sin tocar todo).

---

## Consecuencias

**Ganamos:**
- Despliegue simple; un solo artefacto.
- Trazas de ejecución en un mismo proceso; depuración directa.
- Iteración más rápida: agregar o modificar un módulo no exige coordinación entre
  servicios.
- Los límites entre módulos se respetan por convención y revisión de código; si el
  equipo crece, la extracción a servicios es posible sin reescribir el dominio.

**Aceptamos:**
- Si el tráfico crece significativamente (escenario no evidenciado), escalar
  implicará escalar el monolito completo en lugar de módulos individuales.
- La disciplina de no crear dependencias circulares entre módulos es responsabilidad
  del equipo, no del runtime.
