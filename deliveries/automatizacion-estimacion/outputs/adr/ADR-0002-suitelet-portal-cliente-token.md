# ADR-0002 · Suitelet externo con token UUID para el portal del cliente
**Estado:** aceptado
**Fecha:** 2026-06-25

## Contexto y fuerza
US-04 requiere que el cliente reciba un enlace en su correo que lo lleve a una página
donde pueda aceptar o rechazar la estimación **sin tener que llamar a la ejecutiva ni
crear una cuenta en NetSuite**. La fuerza es eliminar el dolor
`perdida-contacto-post-envio` (fuente: `ejecutiva-ventas1.md`, `ejecutiva-ventas3.md`).

El cliente es externo al sistema de Carseg: no tiene credenciales de NetSuite. La
solución debe funcionar con un simple clic en el correo.

## Decisión
Implementar un **Suitelet API 2.1** (`SL_EstimatePortal.js`) con `isExternal: true`.
La URL del portal incluye un token UUID generado por `N/crypto/random` y almacenado en
el campo custom `custbody_portal_token` del estimate. El flujo es:

1. `UE_Estimate.js` genera el UUID al momento del envío y lo guarda en el estimate.
2. La URL del portal: `https://<account>.suitecommerce.com/app/site/hosting/scriptlet.nl?script=<id>&deploy=<id>&token=<UUID>`
3. El Suitelet valida el token con `N/search`, renderiza el detalle con
   `N/ui/serverWidget`, y procesa la respuesta POST (aceptar/rechazar).

## Alternativas consideradas
- **NetSuite Customer Center / SuiteCommerce** — requiere que el cliente tenga un portal
  de clientes configurado y credenciales de acceso. Agrega fricción de onboarding que
  el MVP no puede asumir. Descartado.
- **URL con ID interno del estimate** — expone el ID interno de NetSuite, permite
  adivinar otros estimates por incremento. Inseguro. Descartado.
- **Servicio externo (formulario en otra plataforma)** — introduce un componente fuera
  de NetSuite que requiere integración, hosting y mantenimiento adicional. Maximiza el
  trabajo innecesario para el MVP. Descartado.
- **Suitelet sin token (solo ID en URL)** — mismo problema de seguridad que la URL con
  ID interno. Descartado.

## Consecuencias
- El cliente puede responder con un clic, sin credenciales. Cumple el criterio de
  aceptación de US-04.
- El token UUID no se invalida automáticamente después de la primera respuesta en esta
  implementación MVP (open question en `architecture.md`). Un cliente técnico podría
  volver a entrar al portal y cambiar su respuesta. Riesgo bajo para MVP; se puede
  mitigar en una siguiente iteración checando `custbody_portal_status != pending`.
- La URL del Suitelet externo en NetSuite tiene formato fijo por cuenta; no es una URL
  "bonita". Para MVP es aceptable; una URL de vanidad (`portal.carseg.cl/responder/...`)
  requeriría un proxy externo.
