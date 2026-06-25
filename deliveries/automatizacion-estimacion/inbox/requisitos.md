# Requisitos candidatos — Automatización de estimación

> Fuentes: `ejecutiva-ventas1.md` y `ejecutiva-ventas2.md` (ejecutiva de
> ventas, primera mano cada una), `ejecutiva-ventas3.md` (contenido de
> gerente de ventas; su `rol_entrevistado` literal dice ahora "ejecutiva de
> ventas" pero el contenido sigue describiendo a una gerente — ver nota de
> calidad de evidencia en `personas.md`). No hay requisitos no funcionales
> explícitos en la evidencia disponible (rendimiento, seguridad,
> disponibilidad no se mencionan).

- **[R-01]** Al seleccionar el cliente en el formulario de estimación, el
  sistema debe precargar automáticamente la ejecutiva comercial relacionada a
  ese cliente, junto con su departamento y oficina, y estos campos deben
  quedar deshabilitados para edición manual.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[R-02]** La estimación debe crearse por defecto con estado "propuesta" y
  probabilidad 50%.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas2.md

- **[R-03]** El ingreso de artículos/productos a ofrecer al cliente se
  mantiene como proceso manual, sin cambios.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[R-04]** El formulario de estimación debe incluir una subficha de
  comunicación con el cliente (p. ej. "comunicación") con: checkbox "enviar
  por correo", campo de correo del cliente, campo de mensaje, carga de un
  archivo xlsx de bienes, y carga opcional de un PDF de estrategia de
  venta/productos sugeridos.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md, ejecutiva-ventas2.md

- **[R-05]** El envío al cliente debe consolidar la información en un solo
  PDF unificado, en el orden: (1) PDF opcional de estrategia de venta si fue
  cargado, (2) la plantilla de la estimación ya generada por el sistema, (3)
  el detalle de bienes del Excel convertido a tabla PDF.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md
  - **Nota de evidencia:** `ejecutiva-ventas2.md` describía inicialmente el
    envío de 3 PDF separados, pero incluye una reflexión explícita de la
    misma entrevistada: "esto puede ser malo para el cliente tener 3 archivos
    pdf dispersos y sería mejor unificarlos para optimizar el tiempo del
    cliente". Las 3 fuentes convergen en el formato unificado.

- **[R-06]** El correo enviado al cliente debe incluir un botón/enlace a una
  página interna del sistema, expuesta para el cliente, donde pueda revisar
  su estimación en línea y aceptar o rechazar.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[R-07]** Si el cliente acepta la estimación desde el portal en línea, el
  sistema debe: cambiar el estado de la estimación a "compra" con
  probabilidad 90%, enviar un correo de confirmación al cliente, y enviar un
  correo de notificación a la ejecutiva de ventas.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[R-08]** Si el cliente rechaza la estimación desde el portal en línea, el
  sistema debe: cambiar el estado de la estimación a "perdida" con
  probabilidad 5%, enviar un correo de confirmación al cliente, y enviar un
  correo de notificación a la ejecutiva de ventas.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md, ejecutiva-ventas3.md

- **[R-09]** El sistema debe enviar también al gerente de ventas un correo de
  notificación cuando el cliente acepta o rechaza la estimación.
  - Tipo: funcional
  - Origen: ejecutiva-ventas3.md

- **[R-10]** El sistema debe enviar al gerente de ventas un correo de
  seguimiento cuando una ejecutiva envía una estimación a un cliente, para
  visibilidad de quién está vendiendo a quién.
  - Tipo: funcional
  - Origen: ejecutiva-ventas3.md

- **[R-11]** Los bienes cargados por Excel en una estimación deben quedar
  visibles en el sistema en formato de grid/tabla dentro de la estimación.
  - Tipo: funcional
  - Origen: ejecutiva-ventas1.md
