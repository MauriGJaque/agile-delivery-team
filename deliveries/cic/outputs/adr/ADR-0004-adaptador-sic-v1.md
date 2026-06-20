# ADR-0004 · Adaptador de lectura al SIC v1 en lugar de migración de datos

**Estado:** aceptado
**Fecha:** 2026-06-20

---

## Contexto y fuerza

HU-E2-03 requiere extraer automáticamente los datos de alumnos participantes de un
convenio para generar el borrador del informe técnico de cierre. Esos datos residen
en el SIC v1. El MVP Canvas registra como supuesto crítico (OQ-03) que "los datos
de alumnos en el SIC v1 son suficientemente completos para precargar el informe
técnico"; este supuesto no está validado. El criterio de aceptación de HU-E2-03
contempla explícitamente el caso de datos incompletos (campos "[PENDIENTE]").

La dirección no ha solicitado ni presupuestado una migración completa del SIC v1.
(`Fundador.md`: el problema es el ciclo de cierre, no la base de datos histórica.)

---

## Decisión

El SIC v2 accede a los datos de alumnos del SIC v1 mediante un **adaptador de
lectura**: una capa de abstracción que expone la interfaz que necesita el Módulo de
Cierre, ocultando los detalles del esquema del sistema legado. El adaptador puede
implementarse como una consulta directa a la base de datos del SIC v1 (si está
accesible) o como una llamada a una API existente. El SIC v1 permanece en modo
**solo lectura** para el SIC v2.

---

## Alternativas consideradas

- **Migración completa de datos del SIC v1 al SIC v2** — Diferida: OQ-03 no está
  resuelta. Migrar datos incompletos o mal estructurados antes de auditar la calidad
  introduce deuda de datos en el nuevo sistema. Es trabajo que se haría dos veces si
  la migración requiere limpieza posterior.
- **Reintroducción manual de datos de alumnos** — Descartado: es exactamente el
  dolor que documenta el discovery (`Profesor.md`: "redactar informes desde cero").
- **Sin acceso al SIC v1 (borrador completamente en blanco)** — Descartado: la
  historia HU-E2-03 pierde su valor principal si no hay prellenado. La historia
  se convertiría en un editor de formularios, no en un generador de borradores.

---

## Consecuencias

**Ganamos:**
- El MVP no bloquea la entrega de valor por una migración de datos compleja.
- El adaptador aísla el SIC v2 del esquema del SIC v1: si el legado cambia, solo
  cambia el adaptador.
- La calidad del prellenado es proporcional a la calidad de los datos del SIC v1;
  los campos "[PENDIENTE]" hacen visible dónde está el problema de datos sin bloquear
  el flujo.

**Aceptamos:**
- El SIC v2 tiene una dependencia en tiempo de ejecución del SIC v1. Si el SIC v1
  no está disponible, el borrador del informe técnico no puede generarse.
- La migración completa de datos seguirá siendo necesaria a largo plazo; este ADR
  la aplaza, no la cancela. Se recomienda auditar los datos del SIC v1 antes del
  sprint de E2.
