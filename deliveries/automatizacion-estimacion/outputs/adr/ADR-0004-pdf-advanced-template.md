# ADR-0004 · Estrategia de generación del PDF unificado (US-03 / R-05)
**Estado:** aceptado con restricción temporal
**Fecha:** 2026-06-25

## Contexto y fuerza
US-03 y R-05 requieren que el cliente reciba **un único PDF** que contenga, en orden:
(1) PDF de estrategia de venta (si fue cargado), (2) plantilla de estimación generada
por el sistema, (3) detalle de bienes del Excel convertido a tabla PDF.
La fuerza viene de la reflexión de `ejecutiva-ventas2.md`: "tener 3 archivos PDF
dispersos es malo para el cliente; sería mejor unificarlos".

SuiteScript 2.1 no expone una API nativa de merge de PDFs arbitrarios.

## Decisión
**Fase 1 — MVP:** Generar el PDF de estimación con el módulo `N/render` usando un
**Advanced PDF/HTML Template** (BFO) personalizado en NetSuite. El template incluirá
los datos de la estimación y los artículos directamente desde el record. El PDF de
estrategia de venta (archivo externo subido por la ejecutiva) se **adjunta como
segundo archivo** en el mismo email, hasta que se resuelva el merge nativo.

El Excel de bienes (`custbody_goods_xlsx`) se convierte a tabla dentro del Advanced PDF
Template mediante la lectura de los artículos del record del estimate (que ya los
contiene), eliminando la necesidad de parsear el Excel para el PDF.

**Fase 2 — post-MVP (open question):** Evaluar si algún bundle de NetSuite o la API
`N/pdf` (disponibilidad variable por versión de cuenta) permite concatenar PDFs. Si es
viable, el PDF de estrategia se fusionaría con el PDF de estimación para cumplir R-05
completamente.

## Alternativas consideradas
- **Merge de PDFs en un Suitelet con librería externa** — SuiteScript no permite
  importar librerías de Node.js arbitrarias (no hay acceso a `pdf-lib`, `pdfkit`, etc.).
  Requeriría un servicio externo (Lambda, Cloud Function) con llamada HTTP desde
  NetSuite, añadiendo latencia, costo y un punto de fallo externo. Descartado para MVP.
- **Enviar siempre 3 archivos separados** — Posible, pero explícitamente rechazado por
  la evidencia del Discovery (`ejecutiva-ventas2.md`). Descartado como solución
  permanente.
- **SuiteCommerce / REST API con servicio de merge externo** — over-engineering para
  MVP. Registrado como alternativa para Fase 2.

## Consecuencias
- **Divergencia temporal con R-05:** En el MVP, el cliente recibe 2 adjuntos (PDF de
  estimación + PDF de estrategia por separado) cuando la ejecutiva carga una estrategia.
  Cuando no carga estrategia, recibe 1 PDF. Esta divergencia es conocida y aceptada
  explícitamente para no bloquear el delivery del MVP.
- El Advanced PDF Template requiere diseño y configuración en el entorno de NetSuite
  (no es solo código). Es parte del scope de implementación de US-03.
- El Excel de bienes no se parsea en el script: se usan los artículos del record de
  estimate directamente. Esto asume que el Excel que carga la ejecutiva es consistente
  con los artículos ya ingresados en la estimación (supuesto de flujo operacional).
