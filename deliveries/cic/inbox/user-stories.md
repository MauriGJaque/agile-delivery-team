# User Stories — Discovery CIC (SIC v2)

> Generado por `/discovery:generate-mvp discoveries/cic`
> Prerrequisitos: `personas.md`, `requisitos.md`, `evidence-map.json`
> Prioridad: núcleo de valor primero — automatización del ciclo de cierre de convenios.

---

## Épica 1 — Alertas automáticas de vencimiento

### [US-01] Notificación preventiva de vencimiento

Como **fundadora / directora de alianzas**, quiero que el sistema me notifique automáticamente 30 días antes de que venza un convenio para evitar que la alianza siga operando de palabra cuando el documento ya expiró.

- **Criterios de aceptación:**
  - Dado un convenio cuya fecha de vencimiento es en 30 días o menos, cuando el sistema ejecuta la revisión diaria de fechas, entonces envía un correo/notificación al docente responsable y a la contraparte externa indicando el convenio afectado y su fecha exacta de vencimiento.
  - Dado que la fundadora accede al panel de dirección, cuando lo abre, entonces ve una sección "Próximos vencimientos" ordenada por urgencia.
- **Fuente:** `Fundador.md`

---

## Épica 2 — Cierre formal digital del convenio

### [US-02] Generación del Acta de Finiquito digital

Como **fundadora / directora de alianzas**, quiero que el sistema genere el Acta de Finiquito prellenada con los datos del convenio para evitar la redacción manual y dejar evidencia digital del cierre.

- **Criterios de aceptación:**
  - Dado un convenio en estado "vencido" o "en cierre", cuando la fundadora inicia el proceso de cierre desde el panel, entonces el sistema genera un Acta de Finiquito prellenada con los datos del convenio (partes, fechas, objeto) en formato PDF editable.
  - Dado el Acta de Finiquito generada, cuando todas las partes requeridas la firman electrónicamente, entonces el convenio cambia su estado a "Cerrado formalmente" y el acta queda archivada en el registro.
- **Fuente:** `Fundador.md`

### [US-03] Generación automática del informe técnico de cierre

Como **profesor gestor de convenios**, quiero que el sistema extraiga automáticamente los datos de los alumnos participantes del convenio para armar el informe técnico de cierre sin redactar desde cero en Word.

- **Criterios de aceptación:**
  - Dado un convenio con alumnos vinculados en el sistema, cuando el profesor solicita el informe de cierre desde su panel, entonces el sistema genera un borrador de informe técnico prellenado con nombre de alumnos, carrera y período de participación.
  - Dado el borrador generado, cuando el profesor lo revisa, entonces puede editar el contenido antes de adjuntarlo al flujo del Acta de Finiquito.
- **Fuente:** `Profesor.md`

### [US-04] Panel de convenios propios del docente

Como **profesor gestor de convenios**, quiero un panel que liste únicamente los convenios bajo mi responsabilidad y su estado actual para no depender de búsquedas manuales en toda la base.

- **Criterios de aceptación:**
  - Dado que el profesor inicia sesión, cuando accede a su panel, entonces ve únicamente sus convenios a cargo con estado, fecha de vencimiento y acceso directo al flujo de cierre.
  - Dado un convenio próximo a vencer, cuando aparece en el panel del profesor, entonces muestra un indicador visual de urgencia (ámbar o rojo según cercanía).
- **Fuente:** `Profesor.md`

---

## Épica 3 — Estado confiable de convenios para estudiantes

### [US-05] Estado real del convenio con indicadores visuales

Como **estudiante**, quiero que el sistema muestre el estado real y actualizado de cada convenio con indicadores tipo semáforo para no postular a alianzas que ya expiraron.

- **Criterios de aceptación:**
  - Dado un convenio cuya fecha de vencimiento ya pasó y no tiene Acta de Finiquito firmada, cuando un estudiante lo consulta, entonces el sistema muestra el indicador rojo ("Caducado") y bloquea nuevas postulaciones.
  - Dado un convenio activo con cupos disponibles, cuando un estudiante lo consulta, entonces el sistema muestra el indicador verde ("Activo") con el número de cupos disponibles.
  - Dado un convenio en proceso de renovación, cuando un estudiante lo consulta, entonces el sistema muestra el indicador ámbar ("En renovación").
- **Fuente:** `alumno.md`

---

## Fuera del alcance del MVP (historias diferidas)

Las siguientes historias emergen de la evidencia pero **no entran en el MVP** porque no atacan el núcleo de valor identificado (cierre formal y estado confiable). Se registran para el backlog.

- **[US-06-DIFERIDA]** Como estudiante, quiero postular a un convenio desde la plataforma adjuntando mi CV en PDF, para evitar trámites físicos. *(Fuente: `alumno.md`)*
- **[US-07-DIFERIDA]** Como estudiante, quiero un buscador con filtros por carrera para encontrar convenios relevantes sin revisar toda la lista. *(Fuente: `alumno.md`)*
- **[US-08-DIFERIDA]** Como profesor, quiero registrar adendas a un convenio activo sin perder el historial original. *(Fuente: `Profesor.md`)*
