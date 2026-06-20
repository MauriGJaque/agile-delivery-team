# ADR-0002 · Scheduler tipo cron diario para el motor de alertas

**Estado:** aceptado
**Fecha:** 2026-06-20

---

## Contexto y fuerza

HU-E1-01 y HU-E1-03 requieren que el sistema detecte convenios con vencimiento en
≤ 30 días y envíe notificaciones automáticas. El criterio de aceptación establece
que la revisión ocurre una vez al día ("revisión diaria de fechas"). El pain
documentado es la expiración silenciosa (`Fundador.md`: "el sistema no emite alertas
previas al vencimiento; los convenios expiran de forma silenciosa"). La solución no
necesita ser en tiempo real — la granularidad del dominio es de días, no de segundos.

---

## Decisión

El Motor de Alertas se implementa como un **job programado (cron) que se ejecuta
una vez por día**, en horario no pico (p. ej. 06:00 hora local). Consulta la base
de datos por convenios con fecha de vencimiento entre hoy y hoy + 30 días, filtra
los que ya recibieron alerta hoy (deduplicación), y dispara las notificaciones.

---

## Alternativas consideradas

- **Event-driven (publicar evento cuando se crea/actualiza un convenio)** —
  Descartado: el trigger de la alerta no es una acción del usuario sino el paso del
  tiempo. Modelarlo como evento añade complejidad sin beneficio: se necesitaría
  igualmente un job para evaluar fechas periódicamente.
- **Polling cada hora** — Descartado: la granularidad del negocio es días (30 días
  antes del vencimiento). Un cron horario solo añade carga sin cambiar el resultado
  observable para el usuario.
- **Notificación en el momento exacto de cruzar los 30 días** — Requeriría un
  sistema de timers persistentes (p. ej. Sidekiq, Celery scheduled tasks) más
  complejo. El valor incremental sobre un cron diario es nulo para este dominio.

---

## Consecuencias

**Ganamos:**
- Implementación mínima: una tarea programada con una consulta SQL y un bucle de
  envío.
- Deduplicación simple: un campo `ultima_alerta_enviada` por convenio evita
  reenvíos.
- Observabilidad directa: el log del cron registra cuántos convenios fueron
  notificados cada ejecución.

**Aceptamos:**
- La alerta puede llegar hasta 23h 59m tarde con respecto al momento exacto de
  cruzar los 30 días. Dado que el margen de aviso es de 30 días, esta imprecisión
  es irrelevante para el dominio.
- Si en el futuro se necesita notificación en tiempo real (p. ej. alerta inmediata
  al registrar un convenio con vencimiento inminente), el Motor de Alertas puede
  extenderse sin cambiar los demás módulos.
