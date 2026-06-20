# ADR-0003 · Generación de PDF del Acta de Finiquito en el servidor

**Estado:** aceptado
**Fecha:** 2026-06-20

---

## Contexto y fuerza

HU-E2-01 requiere que el sistema genere el Acta de Finiquito como un PDF prellenado
con los datos del convenio. El acta es un documento legal que se archivará en el
sistema y que debe ser idéntica independientemente del dispositivo o navegador del
usuario. La dirección la presentará ante la contraloría como evidencia de cierre
formal (`Fundador.md`, R-02). La integridad y la reproducibilidad del documento son
no negociables.

---

## Decisión

El PDF se genera **en el servidor** a partir de una plantilla HTML/CSS renderizada
con una librería de generación de PDF server-side (p. ej. WeasyPrint, Puppeteer
headless, wkhtmltopdf). El cliente recibe el PDF ya generado y listo para descargar
o enviar al flujo de firma.

---

## Alternativas consideradas

- **Generación en el cliente (JavaScript + jsPDF / html2canvas)** — Descartado: el
  resultado varía según el navegador y la resolución del dispositivo, lo que produce
  documentos inconsistentes. Un acta legal no puede depender del cliente del usuario.
- **Plantilla Word/DOCX servida para que el usuario la rellene** — Descartado:
  requiere que el usuario tenga Word instalado, introduce edición manual no controlada
  y hace imposible el flujo de firma electrónica integrado. Reproduce el flujo manual
  que el discovery documenta como dolor (`Profesor.md`: "redactar informes en Word
  desde cero").
- **Servicio externo de generación de documentos (p. ej. DocRaptor, Carbone.io)** —
  Diferido: puede evaluarse si la generación server-side añade fricción al despliegue.
  Por ahora, una librería local evita dependencia de terceros para un artefacto legal.

---

## Consecuencias

**Ganamos:**
- Documentos reproducibles: el mismo convenio siempre produce el mismo PDF.
- El archivo almacenado en la base de datos es el documento exacto que firmaron las
  partes.
- Sin dependencias del entorno del cliente.

**Aceptamos:**
- La generación de PDF consume CPU en el servidor. Para el volumen esperado
  (convenios universitarios, no miles por segundo) esto no es un problema.
- El mantenimiento de la plantilla HTML/CSS es responsabilidad del equipo de
  desarrollo; cambios de formato requieren un despliegue.
