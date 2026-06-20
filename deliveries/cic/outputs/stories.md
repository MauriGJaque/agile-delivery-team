# Historias refinadas — SIC v2

> Developer · 2026-06-20
> Fuente: `deliveries/cic/outputs/backlog.json`
> Inbox: `deliveries/cic/inbox/`
> Gate DoR/INVEST: aprobado

**Resumen:** 9 historias listas · 33 puntos totales · 3 épicas

| Épica | Historias | Puntos |
|-------|-----------|--------|
| E1 — Alertas automáticas | 3 | 7 pts |
| E2 — Cierre formal digital | 4 | 21 pts |
| E3 — Estado confiable | 2 | 5 pts |
| **Total** | **9** | **33 pts** |

---

## Épica E1 — Alertas automáticas de vencimiento

> **Valor:** La Directora y los docentes reciben aviso 30 días antes, eliminando la expiración silenciosa.
> **Origen:** R-01, R-03 · US-01 · `Fundador.md`

---

### HU-E1-01 · Notificación automática de vencimiento a la directora · E1 · 3 pts

**Como** fundadora / directora de alianzas, **quiero** recibir una notificación automática 30 días antes del vencimiento de cada convenio, **para** activar el proceso de cierre antes de que el convenio caduque de facto y genere riesgo legal.

**Criterios de aceptación:**
- Dado un convenio cuya fecha de vencimiento es en 30 días o menos, cuando el sistema ejecuta la revisión diaria de fechas, entonces envía un correo a la directora de alianzas con el nombre del convenio, la contraparte y la fecha exacta de vencimiento.
- Dado que la directora accede al panel de dirección, cuando lo abre, entonces ve una sección "Próximos vencimientos" con todos los convenios con vencimiento en ≤ 30 días, ordenados de más urgente a menos urgente.
- Dado un convenio que ya generó alerta ese día, cuando el sistema ejecuta la revisión al día siguiente, entonces no envía una segunda alerta duplicada por el mismo convenio en el mismo ciclo de 24 horas.

**Estimación:** 3 pts · **Dependencias:** ninguna
**Origen:** US-01, R-01 · `Fundador.md`

---

### HU-E1-02 · Panel de próximos vencimientos en la dirección · E1 · 2 pts

**Como** fundadora / directora de alianzas, **quiero** ver en mi panel una sección "Próximos vencimientos" ordenada por urgencia, **para** conocer de un vistazo cuáles convenios requieren atención inmediata sin revisar registro por registro.

**Criterios de aceptación:**
- Dado que la directora accede al panel, cuando lo carga, entonces ve la sección "Próximos vencimientos" con todos los convenios con vencimiento en ≤ 30 días ordenados por fecha de vencimiento ascendente.
- Dado que no hay convenios próximos a vencer, cuando la directora abre el panel, entonces la sección muestra el mensaje "Sin vencimientos próximos en los próximos 30 días".

**Estimación:** 2 pts · **Dependencias:** HU-E1-01
**Origen:** US-01, R-03 · `Fundador.md`

---

### HU-E1-03 · Notificación automática de vencimiento al docente responsable · E1 · 2 pts

**Como** profesor gestor de convenios, **quiero** recibir una alerta de vencimiento con 30 días de anticipación para los convenios bajo mi responsabilidad, **para** preparar el informe técnico de cierre con tiempo suficiente sin depender de que alguien me avise manualmente.

**Criterios de aceptación:**
- Dado un convenio cuya fecha de vencimiento es en 30 días o menos, cuando el sistema ejecuta la revisión diaria, entonces envía un correo al docente responsable del convenio con el nombre del convenio y la fecha exacta de vencimiento.
- Dado que el docente responsable recibe la alerta y accede a su panel, cuando ve el convenio en la lista, entonces aparece marcado con indicador de urgencia (rojo si vence en ≤ 7 días, ámbar si vence en ≤ 30 días).

**Estimación:** 2 pts · **Dependencias:** HU-E1-01 (reutiliza el motor de alertas)
**Origen:** US-01, R-01 · `Fundador.md`

---

## Épica E2 — Cierre formal digital del convenio

> **Valor:** El cierre de un convenio pasa de Word + firmas físicas a un flujo íntegramente digital con evidencia para la contraloría.
> **Origen:** R-02, R-04, R-05 · US-02, US-03, US-04 · `Fundador.md`, `Profesor.md`

---

### HU-E2-04 · Panel de convenios propios del docente · E2 · 3 pts

**Como** profesor gestor de convenios, **quiero** acceder a un panel que liste únicamente los convenios bajo mi responsabilidad con su estado actual y acceso directo al flujo de cierre, **para** no depender de búsquedas manuales en toda la base y poder actuar rápido cuando un convenio requiere atención.

**Criterios de aceptación:**
- Dado que el docente inicia sesión, cuando accede a su panel, entonces ve únicamente los convenios asignados a su usuario — no los de otros docentes — con estado, fecha de vencimiento y botón de acceso al flujo de cierre.
- Dado un convenio próximo a vencer en el panel del docente, cuando aparece en la lista, entonces muestra un indicador visual de urgencia (ámbar si vence en ≤ 30 días, rojo si vence en ≤ 7 días).
- Dado que el docente filtra la lista por estado "En cierre", cuando aplica el filtro, entonces ve únicamente los convenios con proceso de cierre formal activo.

**Estimación:** 3 pts · **Dependencias:** ninguna
**Origen:** US-04, R-05 · `Profesor.md`

---

### HU-E2-01 · Generación del Acta de Finiquito prellenada · E2 · 5 pts

**Como** fundadora / directora de alianzas, **quiero** que el sistema genere automáticamente el Acta de Finiquito prellenada con los datos del convenio, **para** eliminar la redacción manual y dejar evidencia digital del cierre disponible para la contraloría.

**Criterios de aceptación:**
- Dado un convenio en estado "vencido" o "en cierre", cuando la directora inicia el proceso de cierre desde el panel, entonces el sistema genera un Acta de Finiquito en PDF prellenada con los datos del convenio (nombre de las partes, fechas de inicio y fin, objeto del convenio).
- Dado el Acta de Finiquito generada, cuando la directora la descarga, entonces el PDF contiene todos los campos del registro del convenio correctamente mapeados y está lista para revisión antes de la firma.
- Dado un convenio con campos nulos o incompletos en el registro, cuando el sistema intenta generar el Acta, entonces muestra un aviso enumerando los campos faltantes antes de generar el documento.

**Estimación:** 5 pts · **Dependencias:** HU-E2-04 (acceso desde el panel del docente)
**Origen:** US-02, R-02 · `Fundador.md`

---

### HU-E2-02 · Firma electrónica del Acta de Finiquito · E2 · 8 pts

**Como** fundadora / directora de alianzas, **quiero** que todas las partes puedan firmar el Acta de Finiquito electrónicamente dentro del sistema, **para** que el convenio quede cerrado formalmente sin requerir documentos físicos ni perseguir firmas presenciales.

**Criterios de aceptación:**
- Dado un Acta de Finiquito generada y revisada, cuando la directora inicia el flujo de firma, entonces el sistema envía un enlace de firma electrónica a cada parte requerida (directora + contraparte) con vigencia de 15 días calendario.
- Dado que todas las partes han firmado el Acta, cuando se registra la última firma, entonces el sistema cambia el estado del convenio a "Cerrado formalmente" y archiva el Acta firmada en el registro del convenio.
- Dado que un enlace de firma ha expirado sin que la parte firme, cuando el sistema detecta la expiración, entonces notifica a la directora para que reenvíe el enlace o escale el caso.

**Estimación:** 8 pts · **Dependencias:** HU-E2-01 (no puedes firmar lo que no existe)
**Origen:** US-02, R-02 · `Fundador.md`

> **Nota del Developer:** OQ-01 (validez jurídica de la firma electrónica ante la contraloría) es un supuesto crítico del MVP Canvas. Esta historia implementa el flujo técnico; la validación legal queda como prueba de aceptación pre-lanzamiento, no como bloqueante de desarrollo. Si la contraloría no acepta firma digital, el equipo deberá diseñar un flujo híbrido en una historia separada.

---

### HU-E2-03 · Generación automática del informe técnico de alumnos · E2 · 5 pts

**Como** profesor gestor de convenios, **quiero** que el sistema extraiga automáticamente los datos de los alumnos participantes y genere el borrador del informe técnico de cierre editable, **para** no tener que redactarlo desde cero en Word y poder adjuntarlo directamente al flujo del Acta de Finiquito.

**Criterios de aceptación:**
- Dado un convenio con alumnos vinculados en el sistema, cuando el docente solicita el informe de cierre desde su panel, entonces el sistema genera un borrador del informe técnico prellenado con nombre, carrera y período de participación de cada alumno.
- Dado el borrador generado, cuando el docente lo revisa y edita, entonces puede modificar el contenido de los campos antes de adjuntarlo al Acta de Finiquito.
- Dado un convenio cuyos registros de alumnos tienen campos incompletos, cuando el sistema genera el borrador, entonces marca los campos faltantes con "[PENDIENTE]" y muestra un aviso al docente antes de continuar.

**Estimación:** 5 pts · **Dependencias:** HU-E2-04 (acceso desde el panel del docente)
**Origen:** US-03, R-04 · `Profesor.md`

---

## Épica E3 — Estado confiable de convenios para estudiantes

> **Valor:** El estudiante ve el estado real con semáforo y no invierte tiempo en convenios caducados.
> **Origen:** R-07, R-08, R-12 · US-05 · `alumno.md`

---

### HU-E3-01 · Semáforo visual de estado por convenio · E3 · 3 pts

**Como** estudiante, **quiero** ver un indicador tipo semáforo (verde = activo con cupos, ámbar = en renovación, rojo = caducado) en el listado de convenios, **para** identificar de un vistazo cuáles están activos sin necesidad de abrir cada registro individualmente.

**Criterios de aceptación:**
- Dado un convenio cuya fecha de vencimiento ya pasó y no tiene Acta de Finiquito firmada, cuando un estudiante consulta el listado, entonces el convenio muestra el indicador rojo ("Caducado").
- Dado un convenio activo con cupos disponibles, cuando un estudiante consulta el listado, entonces el convenio muestra el indicador verde ("Activo") con el número de cupos disponibles.
- Dado un convenio en proceso de renovación, cuando un estudiante lo consulta en el listado, entonces el convenio muestra el indicador ámbar ("En renovación").

**Estimación:** 3 pts · **Dependencias:** HU-E1-01, HU-E2-02 (el semáforo necesita datos de estado real del ciclo completo)
**Origen:** US-05, R-08 · `alumno.md`

---

### HU-E3-02 · Bloqueo de postulación a convenios caducados · E3 · 2 pts

**Como** estudiante, **quiero** que el sistema bloquee mis postulaciones a convenios marcados como Caducado, **para** no invertir tiempo en gestiones que el propio sistema ya sabe que son inválidas por haber expirado sin cierre formal.

**Criterios de aceptación:**
- Dado un convenio con indicador rojo ("Caducado"), cuando el estudiante intenta iniciar una postulación, entonces el sistema muestra el mensaje "Este convenio está caducado; no se aceptan nuevas postulaciones" y no permite completar el formulario.
- Dado un convenio con indicador verde ("Activo") y cupos disponibles, cuando el estudiante inicia una postulación, entonces el sistema permite continuar el proceso normalmente.
- Dado un convenio que cambia de estado "Activo" a "Caducado" mientras un estudiante tiene el formulario de postulación abierto, cuando el estudiante intenta enviar el formulario, entonces el sistema rechaza la postulación e informa al estudiante del cambio de estado.

**Estimación:** 2 pts · **Dependencias:** HU-E3-01
**Origen:** US-05, R-07 · `alumno.md`

---

## Historias diferidas (fuera del MVP)

| ID | Título | Razón | Origin |
|----|--------|-------|--------|
| D1 | Postulación digital con CV en PDF | No genera riesgo legal; fuera de alcance MVP Canvas. | US-06-DIFERIDA |
| D2 | Buscador con filtros por carrera | Mejora usabilidad pero no elimina el riesgo legal. | US-07-DIFERIDA |
| D3 | Registro de adendas sin perder historial | Dolor real del profesor (R-06), diferido por prioridad de cierre. | US-08-DIFERIDA |
| D4 | Rediseño completo de la interfaz | Diferido en MVP Canvas; mejora UX pero no bloquea el núcleo. | personas.md (Estudiante E.) |

---

## Preguntas abiertas del delivery (nivel equipo, no bloqueantes de historias)

| ID | Pregunta | Impacto si falla |
|----|----------|-----------------|
| OQ-01 | ¿La firma electrónica es aceptada legalmente por la contraloría? | El Acta digital no tiene valor jurídico; requiere flujo híbrido. |
| OQ-02 | ¿Las contrapartes externas tienen herramientas para firmar digitalmente? | HU-E2-02 necesitaría alternativa para partes externas. |
| OQ-03 | ¿Los datos de alumnos del SIC v1 son suficientemente completos? | El borrador de HU-E2-03 tendrá más campos "[PENDIENTE]" de lo esperado. |
