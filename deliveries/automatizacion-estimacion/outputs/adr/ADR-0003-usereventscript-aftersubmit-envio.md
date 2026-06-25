# ADR-0003 · UserEventScript afterSubmit para disparar el envío de estimación
**Estado:** aceptado
**Fecha:** 2026-06-25

## Contexto y fuerza
US-02 y US-03 requieren que, al confirmar el envío desde la subficha de comunicación,
el sistema genere el PDF y envíe el correo al cliente automáticamente, sin que la
ejecutiva tenga que salir del formulario de estimación. La fuerza es el requisito R-04
y R-05 (`inbox/requisitos.md`).

Necesitamos un mecanismo que se active después de que el registro de estimación se
haya guardado (para tener un ID persistente y acceso a los archivos adjuntos guardados).

## Decisión
Implementar la lógica de envío en el evento **`afterSubmit`** de un
**UserEventScript API 2.1** (`UE_Estimate.js`). El script verifica si
`custbody_send_by_email == true` como señal de intención de envío. Si es así:
ejecuta la generación del PDF, el envío del email y la generación del token del portal.
Al terminar, desmarca `custbody_send_by_email` en el registro para evitar re-envíos
accidentales en ediciones futuras.

Se usa `afterSubmit` (y no `beforeSubmit`) porque los archivos adjuntos
(`custbody_goods_xlsx`, `custbody_strategy_pdf`) ya están guardados y accesibles vía
`N/file` en ese momento.

## Alternativas consideradas
- **beforeSubmit** — los archivos adjuntos pueden no estar comprometidos en la base de
  datos aún; riesgo de condición de carrera. Descartado.
- **Workflow de NetSuite** — puede dispararse al guardar, pero tiene capacidades muy
  limitadas para lógica compleja (generación de PDF, manejo de archivos, construcción
  dinámica del email). Requeriría una acción de workflow que llame a un script de todas
  formas. Descartado como mecanismo principal.
- **Scheduled Script / MapReduce** — introduce latencia (el envío no sería inmediato
  al guardar). Para MVP, la ejecutiva espera ver confirmación inmediata. Registrado como
  fallback en `architecture.md` si `afterSubmit` supera el límite de tiempo de ejecución.
- **Botón personalizado con ClientScript** — el click del botón podría llamar a un
  Suitelet que haga el envío en background. Añade complejidad innecesaria para MVP.

## Consecuencias
- El envío es síncrono: la ejecutiva espera en el formulario hasta que el script
  termina. Si la generación del PDF es lenta (>5s), la experiencia se degrada.
- Límite de tiempo de ejecución de `afterSubmit`: 10 000 ms por defecto en NetSuite.
  Monitorear en QA con estimaciones de muchos artículos.
- Al desmarcar `custbody_send_by_email` en el mismo `afterSubmit`, el script hace una
  segunda escritura al registro (`record.submitFields`). Esto puede desencadenar el
  propio UserEventScript nuevamente; se debe incluir un guard de re-entrada
  (verificar el contexto con `N/runtime` o un flag).
