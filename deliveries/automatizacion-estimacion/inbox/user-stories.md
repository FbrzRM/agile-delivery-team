# User stories — Automatización de estimación

> Historias del núcleo de valor del MVP: automatizar el envío de la
> estimación al cliente y el ciclo de respuesta (aceptar/rechazar), que es el
> dolor más repetido y más explícito entre las fuentes (`ejecutiva-ventas1.md`
> y `ejecutiva-ventas2.md` — ejecutiva de ventas, dos entrevistas de primera
> mano; `ejecutiva-ventas3.md` — contenido de gerente de ventas, ver nota de
> calidad de evidencia en `personas.md`). No se incluyen historias para
> R-02/R-03 (defaults de estado/probabilidad, ingreso manual de artículos)
> porque la evidencia los describe como comportamiento ya esperado, sin
> cambios pedidos.

- **[US-01]** Como Ejecutiva de ventas, quiero que el sistema precargue
  automáticamente mi información de ejecutiva comercial, departamento y
  oficina al seleccionar el cliente, para no llenar esos campos manualmente
  en cada estimación.
  - Criterios de aceptación:
    - Dado que selecciono un cliente que tiene una ejecutiva comercial
      relacionada, cuando creo una nueva estimación, entonces los campos
      ejecutiva comercial, departamento y oficina se cargan automáticamente y
      quedan deshabilitados para edición manual.
  - Fuente: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[US-02]** Como Ejecutiva de ventas, quiero una subficha de comunicación en
  el formulario de estimación donde pueda escribir un mensaje y adjuntar un
  Excel de bienes y un PDF opcional de estrategia de venta, para enviar la
  estimación sin salir del sistema.
  - Criterios de aceptación:
    - Dado que tengo una estimación con artículos definidos, cuando abro la
      subficha de comunicación, marco "enviar por correo", escribo un mensaje
      y adjunto los archivos, entonces puedo confirmar el envío desde el
      mismo formulario.
  - Fuente: ejecutiva-ventas1.md, ejecutiva-ventas3.md, ejecutiva-ventas2.md

- **[US-03]** Como cliente, quiero recibir la estimación en un solo documento
  unificado (estrategia de venta, plantilla de estimación y detalle de
  bienes), para revisar la propuesta completa de un vistazo sin manejar
  varios archivos dispersos.
  - Criterios de aceptación:
    - Dado que la ejecutiva confirmó el envío de una estimación, cuando reviso
      mi correo, entonces encuentro un único PDF que incluye, en orden, la
      estrategia de venta (si fue cargada), la plantilla de la estimación y
      el detalle de bienes.
  - Fuente: ejecutiva-ventas1.md, ejecutiva-ventas3.md, ejecutiva-ventas2.md

- **[US-04]** Como cliente, quiero un enlace en el correo que me lleve a una
  página donde pueda revisar la estimación en línea y aceptarla o
  rechazarla, para responder sin tener que llamar o escribir a la ejecutiva.
  - Criterios de aceptación:
    - Dado que recibí el correo con la estimación, cuando hago clic en el
      botón del correo, entonces accedo a una página del sistema donde veo el
      detalle de mi estimación y puedo elegir aceptar o rechazar.
  - Fuente: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[US-05]** Como Ejecutiva de ventas, quiero que el sistema actualice
  automáticamente el estado de la estimación y me notifique cuando el
  cliente acepta, para no tener que perseguirlo por teléfono para saber si
  sigue interesado.
  - Criterios de aceptación:
    - Dado que el cliente aceptó la estimación desde el portal en línea,
      cuando se registra esa aceptación, entonces el sistema cambia el estado
      a "compra" con probabilidad 90%, envía un correo de confirmación al
      cliente y me notifica por correo.
  - Fuente: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[US-06]** Como Ejecutiva de ventas, quiero que el sistema actualice el
  estado de la estimación y me notifique cuando el cliente rechaza, para
  poder replantear mi estrategia con ese cliente a tiempo.
  - Criterios de aceptación:
    - Dado que el cliente rechazó la estimación desde el portal en línea,
      cuando se registra ese rechazo, entonces el sistema cambia el estado a
      "perdida" con probabilidad 5%, envía un correo de confirmación al
      cliente y me notifica por correo.
  - Fuente: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[US-07]** Como Gerente de ventas, quiero recibir un correo cuando el
  cliente acepta o rechaza una estimación, para tener visibilidad del
  resultado de las ventas de mi equipo sin tener que preguntarles.
  - Criterios de aceptación:
    - Dado que el cliente respondió (aceptó o rechazó) una estimación desde
      el portal en línea, cuando se registra esa respuesta, entonces recibo
      un correo de notificación indicando el resultado y la ejecutiva
      involucrada.
  - Fuente: ejecutiva-ventas3.md
