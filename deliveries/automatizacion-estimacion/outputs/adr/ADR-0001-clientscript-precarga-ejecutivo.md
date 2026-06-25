# ADR-0001 · ClientScript para precarga automática de datos del ejecutivo
**Estado:** aceptado
**Fecha:** 2026-06-25

## Contexto y fuerza
US-01 requiere que, al seleccionar un cliente en el formulario de estimación, los campos
ejecutiva comercial, departamento y oficina se carguen automáticamente y queden
deshabilitados para edición manual. La fuerza es eliminar el dolor
`llenado-manual-datos-ejecutiva` documentado en `ejecutiva-ventas1.md` y
`ejecutiva-ventas3.md`.

En NetSuite SuiteScript 2.1, los scripts que reaccionan a cambios de campo en tiempo real
dentro del formulario son los ClientScripts. Los UserEventScripts corren del lado del
servidor y no perciben cambios de campo hasta que el usuario guarda el registro.

## Decisión
Implementar un **ClientScript API 2.1** (`CS_Estimate.js`) con los eventos `pageInit`
(para cargar campos si el registro ya tiene cliente al abrirse) y `fieldChanged` (para
reaccionar en tiempo real cuando el usuario selecciona o cambia el cliente). El script
usa `N/search` para buscar la ejecutiva comercial relacionada al cliente y llama a
`currentRecord.setValue` + `setFieldDisabled` para cada campo.

## Alternativas consideradas
- **UserEventScript `beforeLoad` con `setFieldValue`** — corre server-side al cargar el
  formulario, pero no reacciona si el usuario cambia el cliente después de abrir el
  formulario. Requiere guardar para refrescar, lo que degrada la experiencia.
- **Workflow de NetSuite** — no tiene acceso a eventos de campo en tiempo real en el
  formulario; solo actúa al guardar el registro. Descartado por la misma razón.
- **Inline Editing / Formula field** — no permite poblar múltiples campos con lógica
  condicional de búsqueda. Descartado.

## Consecuencias
- La precarga ocurre en el browser del usuario sin necesidad de guardar el registro:
  experiencia fluida.
- Requiere que el modelo de datos de Carseg tenga una relación accesible entre cliente
  y ejecutiva comercial (p. ej. campo custom en el registro de cliente). Si no existe,
  esta historia no es implementable sin una migración de datos previa (open question
  registrada en `architecture.md`).
- El script debe incluir un guard para el caso en que el cliente no tenga ejecutiva
  relacionada (no romper el formulario silenciosamente).
