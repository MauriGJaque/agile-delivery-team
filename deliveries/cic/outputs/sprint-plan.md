# Sprint Plan — SIC v2

> Scrum Master · 2026-06-20
> Fuente: `deliveries/cic/outputs/backlog.json` · `deliveries/cic/outputs/stories.md`
> Gate DoR/INVEST: aprobado

---

## Revisión DoR antes del sprint

El Scrum Master verificó las 9 historias del backlog contra la Definition of Ready.
Resultado: **todas cumplen** — formato Como/Quiero/Para completo, ≥ 2 criterios de
aceptación Gherkin, estimación Fibonacci entre 1 y 8 pts, dependencias internas
resueltas y `open_questions` vacío.

La historia de prueba `HU-E3-03` ("quiero ver que pasa" / "azul") fue eliminada en
el paso de refinamiento por violación de cero invención; no está en el backlog.

**Bloqueo de flujo identificado:** HU-E2-02 (firma electrónica, 8 pts) depende de
la resolución de OQ-01 (validez legal ante contraloría) y OQ-02 (capacidad de
contrapartes externas). Se puede desarrollar técnicamente, pero no puede pasar
pruebas de aceptación legales hasta resolver esas preguntas. El Scrum Master
recomienda escalarlas al Product Owner antes del Sprint 2.

---

## Sprint 1

### Sprint Goal

> **Activar el ciclo de alerta y preparar el borrador del cierre:** al terminar
> el sprint, la directora y los docentes reciben avisos automáticos de vencimiento,
> y pueden generar desde el sistema el Acta de Finiquito prellenada y el informe
> técnico de alumnos sin redactar desde cero.

**Capacidad:** 20 pts · **Comprometido:** 20 pts

| Historia | Título | Épica | Pts | Dependencias |
|----------|--------|-------|-----|--------------|
| HU-E1-01 | Notificación automática de vencimiento a la directora | E1 | 3 | — |
| HU-E1-02 | Panel de próximos vencimientos en la dirección | E1 | 2 | HU-E1-01 |
| HU-E1-03 | Notificación automática al docente responsable | E1 | 2 | HU-E1-01 |
| HU-E2-04 | Panel de convenios propios del docente | E2 | 3 | — |
| HU-E2-01 | Generación del Acta de Finiquito prellenada | E2 | 5 | HU-E2-04 |
| HU-E2-03 | Generación automática del informe técnico de alumnos | E2 | 5 | HU-E2-04 |
| **Total** | | | **20** | |

**Orden de construcción sugerido:**
1. HU-E1-01 y HU-E2-04 en paralelo (sin dependencias entre sí).
2. HU-E1-02 y HU-E1-03 una vez que HU-E1-01 esté integrado.
3. HU-E2-01 y HU-E2-03 una vez que HU-E2-04 esté integrado.

**Valor entregado al final del Sprint 1:**
La directora y los docentes ya no dependen de avisos manuales. El proceso de cierre
tiene soporte digital para los dos documentos más costosos de producir (Acta y
informe técnico). La contabilidad del ~20 % de convenios caducados sin cierre puede
iniciarse.

---

## Sprint 2

### Sprint Goal (tentativo)

> **Cerrar el ciclo completo:** al terminar el sprint, un convenio puede cerrarse
> formalmente con firma electrónica de todas las partes, y el estudiante ve el
> estado real en tiempo real.

**Capacidad:** 20 pts · **Comprometido:** 13 pts

| Historia | Título | Épica | Pts | Dependencias | Condición |
|----------|--------|-------|-----|--------------|-----------|
| HU-E2-02 | Firma electrónica del Acta de Finiquito | E2 | 8 | HU-E2-01 (✓ Sprint 1) | Requiere resolver OQ-01/OQ-02 antes de pruebas de aceptación |
| HU-E3-01 | Semáforo visual de estado por convenio | E3 | 3 | HU-E1-01 (✓), HU-E2-02 | Después de HU-E2-02 |
| HU-E3-02 | Bloqueo de postulación a convenios caducados | E3 | 2 | HU-E3-01 | Después de HU-E3-01 |
| **Total** | | | **13** | | |

> Los 7 pts de capacidad restante del Sprint 2 se reservan como buffer para la
> resolución técnica de OQ-01/OQ-02 (integración con el proveedor de firma
> electrónica una vez validado legalmente) o para incorporar historias diferidas
> si el equipo lo decide en la Sprint Planning.

---

## Historias fuera del plan (diferidas al backlog)

| ID | Título | Razón |
|----|--------|-------|
| D1 | Postulación digital con CV en PDF | Fuera del MVP Canvas |
| D2 | Buscador con filtros por carrera | Fuera del MVP Canvas |
| D3 | Registro de adendas sin perder historial | Fuera del MVP Canvas |
| D4 | Rediseño completo de la interfaz de usuario | Fuera del MVP Canvas |

---

## Impedimentos identificados

| ID | Descripción | Responsable de escalar | Sprint afectado |
|----|-------------|------------------------|-----------------|
| IMP-01 | OQ-01: validez legal de firma electrónica ante la contraloría | Product Owner → Área Legal | Sprint 2 (HU-E2-02) |
| IMP-02 | OQ-02: capacidad de contrapartes externas para firmar digitalmente | Product Owner → Directora | Sprint 2 (HU-E2-02) |
| IMP-03 | OQ-03: completitud de datos de alumnos en SIC v1 | Developer → auditoría previa al Sprint 1 | Sprint 1 (HU-E2-03) |
