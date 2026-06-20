# ADR-0005 · Firma electrónica vía proveedor externo (decisión de proveedor diferida)

**Estado:** aceptado (con decisión de proveedor pendiente)
**Fecha:** 2026-06-20

---

## Contexto y fuerza

HU-E2-02 requiere que todas las partes (directora + contraparte externa) firmen el
Acta de Finiquito electrónicamente dentro del sistema. El MVP Canvas registra dos
supuestos críticos sin validar:

- **OQ-01:** ¿La firma electrónica es legalmente aceptada por la contraloría
  institucional? Si no lo es, el Acta digital no tiene valor jurídico.
- **OQ-02:** ¿Las contrapartes externas (empresas aliadas) cuentan con herramientas
  para firmar electrónicamente? Pueden no tener los medios técnicos.

Implementar una infraestructura de firma digital propia (PKI, certificados,
custodios de claves) es un proyecto de seguridad por sí solo, incompatible con el
alcance y el equipo del MVP.

---

## Decisión

La firma electrónica se delega a un **proveedor de firma electrónica externo**
mediante una integración vía API (p. ej. DocuSign, Signaturit, FirmaEC o equivalente
con reconocimiento institucional en Ecuador). El SIC v2 expone un **Adaptador de
Firma** que abstrae el proveedor concreto detrás de una interfaz interna.

La **decisión del proveedor concreto queda diferida** hasta que OQ-01 y OQ-02 se
resuelvan: el proveedor debe ser aceptado por la contraloría institucional y debe
ofrecer un flujo que las contrapartes externas puedan usar sin instalar software
especializado (p. ej. firma por enlace de correo).

---

## Alternativas consideradas

- **Implementación propia de firma digital (PKI interna)** — Descartado: requiere
  gestión de certificados, custodia de claves privadas, infraestructura de
  revocación. Complejidad fuera del alcance del MVP y del equipo universitario.
- **Firma manuscrita escaneada como imagen incrustada en el PDF** — Descartado:
  no es firma electrónica en sentido legal; no resuelve el requisito de cierre formal
  sin documentos físicos (`Fundador.md`).
- **Comprometerse con un proveedor concreto ahora** — Diferido: hasta que OQ-01
  (validez ante contraloría) esté resuelta, elegir un proveedor puede obligar a
  cambiarlo. El adaptador permite postergar esa decisión sin bloquear el desarrollo
  del flujo de firma.

---

## Consecuencias

**Ganamos:**
- El equipo no gestiona PKI, certificados ni custodia de claves privadas.
- El Adaptador de Firma permite cambiar de proveedor sin modificar el Módulo de
  Cierre.
- El flujo "firma por enlace de correo" que ofrecen los proveedores modernos
  resuelve parcialmente OQ-02 (la contraparte solo necesita un navegador web).

**Aceptamos:**
- Dependencia de un servicio externo de pago. El costo debe evaluarse junto con
  OQ-01 antes de seleccionar el proveedor.
- Si la contraloría no acepta ningún proveedor externo y exige firma con certificado
  institucional propio, este ADR deberá revisarse y posiblemente reemplazarse.

## Acción requerida antes del sprint de E2

Resolver OQ-01 y OQ-02 con la dirección y el área legal/contraloría de la
institución. Sin esa validación, HU-E2-02 puede desarrollarse técnicamente pero no
puede pasar pruebas de aceptación legales.
