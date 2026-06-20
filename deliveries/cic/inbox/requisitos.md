# Requisitos candidatos — Discovery CIC (SIC v2)

> Generado por `/discovery:analyze discoveries/cic`
> Fuentes: `Fundador.md`, `Profesor.md`, `alumno.md`

---

## Requisitos funcionales

- **[R-01]** El sistema debe detectar convenios cuya fecha de vencimiento se encuentre dentro de los próximos 30 días y enviar una alerta automática al docente responsable y a la contraparte externa.
  - Tipo: funcional
  - Origen: `Fundador.md` · Fundadora

- **[R-02]** El sistema debe generar digitalmente el Acta de Finiquito del convenio, prellenada con los datos del registro, y admitir firma electrónica de todas las partes para cerrar el convenio formalmente.
  - Tipo: funcional
  - Origen: `Fundador.md` · Fundadora

- **[R-03]** El panel de la fundadora / dirección debe mostrar un reporte consolidado de convenios próximos a vencer y convenios ya vencidos sin cierre formal.
  - Tipo: funcional
  - Origen: `Fundador.md` · Fundadora

- **[R-04]** El sistema debe extraer automáticamente los datos de alumnos participantes registrados en un convenio y generar el borrador del informe técnico de cierre, editable antes de adjuntarlo al Acta de Finiquito.
  - Tipo: funcional
  - Origen: `Profesor.md` · Profesor

- **[R-05]** El sistema debe ofrecer a cada docente un panel propio que liste únicamente los convenios bajo su responsabilidad, con su estado actualizado.
  - Tipo: funcional
  - Origen: `Profesor.md` · Profesor

- **[R-06]** El sistema debe permitir registrar adendas y modificaciones a un convenio existente sin eliminar el historial de versiones originales.
  - Tipo: funcional
  - Origen: `Profesor.md` · Profesor

- **[R-07]** El sistema debe sincronizar y mostrar el estado real del convenio (activo, en renovación, caducado) en tiempo real, impidiendo que un convenio vencido aparezca como activo.
  - Tipo: funcional
  - Origen: `alumno.md` · Estudiante

- **[R-08]** El sistema debe incluir indicadores visuales tipo semáforo (verde = activo con cupos; amarillo = en renovación; rojo = caducado) visibles en el listado de convenios.
  - Tipo: funcional
  - Origen: `alumno.md` · Estudiante

- **[R-09]** El sistema debe ofrecer un buscador de convenios con filtros por carrera académica.
  - Tipo: funcional
  - Origen: `alumno.md` · Estudiante

- **[R-10]** El sistema debe permitir a los estudiantes postularse a un convenio activo con cupos disponibles, adjuntando el currículum en formato PDF, desde la propia plataforma.
  - Tipo: funcional
  - Origen: `alumno.md` · Estudiante

---

## Requisitos no funcionales

- **[R-11]** La arquitectura del SIC v2 debe permitir modificaciones y extensiones de funcionalidad de forma iterativa, sin que un cambio en un módulo requiera reescribir el sistema completo (principio opuesto al desarrollo en cascada que generó la rigidez del v1).
  - Tipo: no funcional
  - Origen: `Fundador.md`, `Profesor.md` · Fundadora, Profesor

- **[R-12]** El estado de los convenios mostrado a los estudiantes debe reflejar la realidad en todo momento; la inconsistencia entre el estado del sistema y la realidad del convenio es el daño principal al usuario final.
  - Tipo: no funcional (integridad de datos / confiabilidad)
  - Origen: `alumno.md` · Estudiante
