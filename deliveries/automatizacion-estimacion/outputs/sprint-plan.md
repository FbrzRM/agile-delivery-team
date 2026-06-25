# Sprint 1 — La ejecutiva envía la estimación sin salir de NetSuite y el cliente puede responderla en línea

**Capacidad:** 20 pts · **Comprometido:** 20 pts

## Historias comprometidas

| Historia | Descripción | Pts | Épica | Prioridad |
|----------|-------------|-----|-------|-----------|
| US-01 | Precarga automática de datos de ejecutiva | 2 | E-01 | 1 |
| US-02 | Subficha de comunicación con mensaje y adjuntos | 5 | E-01 | 2 |
| US-03 | PDF unificado para el cliente | 5 | E-01 | 3 |
| US-04 | Portal de aceptación/rechazo en línea | 8 | E-02 | 4 |

**Total comprometido: 20 pts** (= capacidad)

## Sprint Goal

> La ejecutiva confirma el envío de una estimación desde la subficha de comunicación
> integrada en NetSuite, el cliente recibe un PDF con la propuesta completa y puede
> aceptarla o rechazarla desde un portal en línea — sin que nadie tenga que llamar a nadie.

## Historias diferidas (Sprint 2 — 8 pts)

| Historia | Descripción | Pts | Bloqueada por |
|----------|-------------|-----|---------------|
| US-05 | Actualización automática de estado y notificación al aceptar | 3 | US-04 |
| US-06 | Actualización automática de estado y notificación al rechazar | 3 | US-04 |
| US-07 | Notificación al Gerente de ventas | 2 | US-05, US-06 |

> **Nota de corte:** US-05, US-06 y US-07 dependen del portal (US-04) que se construye
> en este sprint. La automatización del estado y las notificaciones completan el ciclo
> en Sprint 2 una vez que el portal esté operativo y validado.

## Alcance funcional del Sprint 1

Al cierre del sprint, el equipo puede demostrar el flujo completo de envío:

1. La ejecutiva selecciona un cliente → el sistema precarga sus datos automáticamente (US-01).
2. La ejecutiva abre la subficha "Comunicación", escribe un mensaje y adjunta los archivos (US-02).
3. El sistema envía un email al cliente con un PDF unificado de la propuesta (US-03).
4. El cliente hace clic en el enlace del email y accede al portal donde puede aceptar o rechazar (US-04).

Lo que **no** estará listo al final del Sprint 1: la actualización automática de estado
y las notificaciones a ejecutiva y gerente (quedan para Sprint 2).

## Definition of Ready — verificación

Todas las historias comprometidas cumplen INVEST + DoR:
- Criterios de aceptación en Gherkin ✓
- Estimaciones entre 1–8 pts ✓
- Dependencias a IDs existentes ✓
- Sin preguntas abiertas bloqueantes ✓
