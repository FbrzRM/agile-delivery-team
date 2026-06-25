# Historias refinadas — Automatización de estimación
> Delivery: `automatizacion-estimacion` · Generado: 2026-06-25
> Fuente: `outputs/backlog.json` · Gate: `dor-invest-gate`

---

## E-01 · Envío de estimación desde el formulario

### US-01 · Precarga automática de datos de ejecutiva   ·   épica E-01   ·   2 pts
**Como** Ejecutiva de ventas, **quiero** que el sistema precargue automáticamente mi información de ejecutiva comercial, departamento y oficina al seleccionar el cliente, **para** no tener que llenar esos campos manualmente en cada estimación.

Criterios de aceptación (Gherkin):
- Dado que selecciono un cliente que tiene una ejecutiva comercial relacionada, cuando creo una nueva estimación, entonces los campos ejecutiva comercial, departamento y oficina se cargan automáticamente y quedan deshabilitados para edición manual.

Origen: us:US-01, req:R-01, personas:dolor-llenado-manual-datos-ejecutiva

---

### US-02 · Subficha de comunicación con mensaje y adjuntos   ·   épica E-01   ·   5 pts
**Como** Ejecutiva de ventas, **quiero** una subficha de comunicación en el formulario de estimación donde pueda escribir un mensaje y adjuntar un Excel de bienes y un PDF opcional de estrategia de venta, **para** poder enviar la estimación sin salir del sistema.

Criterios de aceptación (Gherkin):
- Dado que tengo una estimación con artículos definidos, cuando abro la subficha de comunicación, marco "enviar por correo", escribo un mensaje y adjunto los archivos, entonces puedo confirmar el envío desde el mismo formulario.

Origen: us:US-02, req:R-04, personas:dolor-envio-manual-estimacion-cliente

---

### US-03 · PDF unificado para el cliente   ·   épica E-01   ·   5 pts
**Como** Cliente, **quiero** recibir la estimación en un solo documento unificado (estrategia de venta, plantilla de estimación y detalle de bienes), **para** poder revisar la propuesta completa de un vistazo sin manejar varios archivos dispersos.

Criterios de aceptación (Gherkin):
- Dado que la ejecutiva confirmó el envío de una estimación, cuando reviso mi correo, entonces encuentro un único PDF que incluye, en orden, la estrategia de venta (si fue cargada), la plantilla de la estimación y el detalle de bienes.

Origen: us:US-03, req:R-05, personas:stakeholder-cliente

---

## E-02 · Ciclo de respuesta del cliente en línea

### US-04 · Portal de aceptación/rechazo en línea   ·   épica E-02   ·   8 pts
**Como** Cliente, **quiero** un enlace en el correo que me lleve a una página donde pueda revisar la estimación en línea y aceptarla o rechazarla, **para** poder responder sin tener que llamar o escribir a la ejecutiva.

Criterios de aceptación (Gherkin):
- Dado que recibí el correo con la estimación, cuando hago clic en el botón del correo, entonces accedo a una página del sistema donde veo el detalle de mi estimación y puedo elegir aceptar o rechazar.

Origen: us:US-04, req:R-06, personas:dolor-perdida-contacto-post-envio

---

### US-05 · Actualización automática de estado y notificación al aceptar   ·   épica E-02   ·   3 pts
**Como** Ejecutiva de ventas, **quiero** que el sistema actualice automáticamente el estado de la estimación y me notifique cuando el cliente acepta, **para** no tener que perseguirlo por teléfono para saber si sigue interesado.

Criterios de aceptación (Gherkin):
- Dado que el cliente aceptó la estimación desde el portal en línea, cuando se registra esa aceptación, entonces el sistema cambia el estado a "compra" con probabilidad 90%, envía un correo de confirmación al cliente y me notifica por correo.

Origen: us:US-05, req:R-07, personas:dolor-perdida-contacto-post-envio

---

### US-06 · Actualización automática de estado y notificación al rechazar   ·   épica E-02   ·   3 pts
**Como** Ejecutiva de ventas, **quiero** que el sistema actualice el estado de la estimación y me notifique cuando el cliente rechaza, **para** poder replantear mi estrategia con ese cliente a tiempo.

Criterios de aceptación (Gherkin):
- Dado que el cliente rechazó la estimación desde el portal en línea, cuando se registra ese rechazo, entonces el sistema cambia el estado a "perdida" con probabilidad 5%, envía un correo de confirmación al cliente y me notifica por correo.

Origen: us:US-06, req:R-08, personas:dolor-perdida-contacto-post-envio

---

## E-03 · Visibilidad de resultados para el Gerente de ventas

### US-07 · Notificación al Gerente de ventas   ·   épica E-03   ·   2 pts
**Como** Gerente de ventas, **quiero** recibir un correo cuando el cliente acepta o rechaza una estimación, **para** tener visibilidad del resultado de las ventas de mi equipo sin tener que preguntarles.

Criterios de aceptación (Gherkin):
- Dado que el cliente respondió (aceptó o rechazó) una estimación desde el portal en línea, cuando se registra esa respuesta, entonces recibo un correo de notificación indicando el resultado y la ejecutiva involucrada.

Origen: us:US-07, req:R-09, personas:dolor-falta-seguimiento-gerencial, evidence-map:pain-falta-seguimiento-gerencial

---

## Resumen
| Historia | Épica | Pts | Estado DoR |
|----------|-------|-----|------------|
| US-01    | E-01  | 2   | ✓ Lista    |
| US-02    | E-01  | 5   | ✓ Lista    |
| US-03    | E-01  | 5   | ✓ Lista    |
| US-04    | E-02  | 8   | ✓ Lista    |
| US-05    | E-02  | 3   | ✓ Lista    |
| US-06    | E-02  | 3   | ✓ Lista    |
| US-07    | E-03  | 2   | ✓ Lista    |

**Total: 7 historias · 28 puntos**
