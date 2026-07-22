# Propuesta comercial — Plataforma de ticketing propia

**Fecha:** julio de 2026
**Validez de la propuesta:** 30 días calendario
**Documentos de referencia:** Análisis de mercado (adjunto) · Arquitectura técnica — Plataforma de ticketing (adjunto) · Flujo · wireframe de pantallas (solo como referencia)

---

## 1. Resumen de la propuesta

Se propone el diseño, desarrollo, puesta en producción y **administración integral** de una plataforma propia de venta de boletas para el venue, con capacidad para operar eventos de alta demanda (~2,800 asientos, ~70 eventos al año).

| Elemento | Condición |
|---|---|
| Modalidad | **Precio fijo** por el alcance definido en la sección 2 |
| Plazo de desarrollo | **2 meses (8 semanas)** desde la firma y el cumplimiento de los prerrequisitos (sección 8) |
| Inversión del desarrollo | **\$67,000 USD** |
| Operación y soporte posterior | Servicio administrado + **bolsa de horas a \$66 USD/hora** (paquetes con descuento, sección 5) |
| Cortesía de lanzamiento | **15 horas de soporte sin costo**, válidas durante los primeros 2 meses posteriores a la entrega |

El contexto económico está en el análisis de mercado adjunto: a ~175,000 boletas/año con boleta promedio de \$95, el fee de servicio que hoy capturan plataformas externas equivale a **~\$2.5M USD anuales**. Esta propuesta convierte ese costo perpetuo en un activo propio del venue.

---

## 2. Alcance

La entrega corresponde al núcleo transaccional completo descrito en el documento de arquitectura, operable en producción con eventos reales:

**Venta (lado del comprador)**
- Sitio de venta web responsive (PWA), con catálogo de eventos y página por función.
- **Mapa de asientos interactivo** del recinto (~2,800 asientos), con selección por asiento y por zona, y soporte de admisión general.
- Checkout con **temporizador de reserva**, precios all-in (total con fees visible desde el inicio, conforme a la regla FTC), compra como invitado y creación silenciosa de cuenta.
- Pagos con **Stripe** (tarjetas, Apple Pay / Google Pay) y confirmación inmediata.
- Boleta digital con **código QR firmado criptográficamente**, entregada por correo y accesible desde el navegador.
- **Fila virtual (waiting room)** para on-sales de alta demanda y protección anti-bots.

**Operación (lado del venue)**
- **Panel del operador** con ventas en tiempo real, vendido vs. disponible por tier, embudo de conversión, geografía de compradores, velocidad de venta y exportación de datos (sección 11 del documento de arquitectura).
- Creación y gestión de eventos, funciones, tiers de precio, holds y cortesías.
- **Escáner de puerta** (aplicación web progresiva, sin hardware dedicado): validación de firma, redención atómica (una boleta entra una sola vez), operación tolerante a fallas de red y registro de auditoría de cada lectura.

**Puesta en marcha**
- Configuración del mapa maestro del recinto y de los datos del primer evento.
- **Capacitación** al personal de taquilla, marketing y puerta (2 sesiones).
- **Acompañamiento durante el primer evento** en producción.

### Exclusiones de esta entrega

Los siguientes módulos no forman parte del precio fijo y se cotizan como fases posteriores: aplicaciones nativas iOS/Android, marketplace de reventa entre usuarios, precios dinámicos, operación multi-venue / white-label para terceros, e integraciones con sistemas externos no listadas en el alcance. Cualquier funcionalidad no descrita en esta sección se gestiona como cambio de alcance (sección 6).

---

## 3. Cronograma e hitos

| Semana | Hito | Verificable |
|---|---|---|
| 1–2 | Diseño aprobado | UX del flujo de compra y del panel, mapa del recinto validado por el venue |
| 3–5 | Demo funcional | Compra de extremo a extremo en ambiente de pruebas (mapa → checkout → boleta QR) |
| 6–7 | Plataforma completa en staging | Panel del operador, escáner de puerta, fila virtual; **prueba de carga** simulando on-sale |
| 8 | **Producción y evento piloto** | Venta real de un evento sin sobreventa ni caída — criterio de aceptación |

**Criterio de aceptación:** la plataforma vende un evento real en producción cumpliendo la invariante central (cada asiento se vende exactamente una vez), con el panel reportando en tiempo real y la validación en puerta operativa.

---

## 4. Servicio administrado (posterior a la entrega)

La plataforma se entrega **administrada por completo**; el venue no requiere equipo técnico propio:

- Hosting, infraestructura y actualizaciones de la plataforma.
- Monitoreo continuo con alertado sobre las métricas operativas definidas en la arquitectura (latencia de reserva, fila virtual, tasa de autorización de pagos).
- **Cobertura reforzada durante on-sales y días de evento**, coordinada con el calendario del venue.
- Respaldos y registro de auditoría inmutable.

**Tiempos de respuesta de soporte:**

| Severidad | Ejemplo | Respuesta |
|---|---|---|
| Crítica | Venta caída u on-sale/evento en curso afectado | ≤ 1 hora, 5 días a la semana |
| Alta | Funcionalidad principal degradada sin evento en curso | ≤ 4 horas hábiles |
| Media | Fallo con workaround disponible | ≤ 1 día hábil |
| Baja | Ajustes menores, consultas | ≤ 3 días hábiles |

---

## 5. Inversión

| Concepto | Valor |
|---|---|
| Desarrollo y puesta en producción (alcance de la sección 2) | **\$67,000 USD — precio fijo** |
| Soporte y evolución posterior | **Bolsa de horas a \$66 USD/hora** |
| Cortesía de lanzamiento | **15 horas sin costo, válidas por 2 meses** desde la entrega en producción |

**Paquetes de horas de operación y soporte** (opcionales, con descuento por volumen):

| Bolsa de horas | Precio (USD) | Valor por hora | Ahorro |
|---|---:|---:|---:|
| Bolsa de 5 horas | **\$315** | \$63.00 | 5% |
| Bolsa de 10 horas | **\$590** | \$59.00 | 11% |
| Bolsa de 20 horas | **\$1,120** | \$56.00 | 15% |
| Hora adicional (sin paquete) | **\$66** | \$66.00 | — |

**Reglas de la bolsa de horas:**
- Cubre soporte correctivo fuera de garantía, ajustes, mejoras menores y acompañamiento adicional en eventos.
- Se consume en fracciones mínimas de 1 hora; el consumo se reporta mensualmente.
- Los paquetes se pagan por anticipado y no tienen fecha de vencimiento.
- Las horas adicionales sobre un paquete activo se facturan a la misma tarifa del paquete (ej.: con la bolsa de 20 horas, la hora extra queda en \$56). Sin paquete activo, la hora se factura a \$66 USD.
- Los cambios de alcance mayores se estiman por escrito y se aprueban por el venue antes de ejecutarse.
- Las 15 horas de cortesía se consumen antes que cualquier hora facturable.

**Forma de pago propuesta:** 50% a la firma · 30% en la demo funcional (semana 5) · 20% en la aceptación (evento piloto).

---

## 6. Costos de terceros (a cargo del venue)

Son costos directos del negocio, se contratan a nombre del venue y no forman parte del precio fijo:

| Servicio | Referencia de costo |
|---|---|
| Procesamiento de pagos (Stripe) | ~2.9% + \$0.30 por transacción (trasladable al comprador) |
| Infraestructura cloud (Cloudflare, base de datos) | Estimado \$[100–200]/mes según volumen |
| Dominio y correo transaccional | Menor (~\$100–300/año) |

La cuenta de Stripe y el dominio son del venue desde el día uno: el venue es dueño de su recaudo y de su relación con el comprador.

---

## 7. Garantía y propiedad

- **Garantía de defectos:** 30 días posteriores a la aceptación para corrección de defectos del alcance entregado, sin costo y sin consumir la bolsa de horas.
- **Propiedad de los datos:** todos los datos (compradores, ventas, métricas) son propiedad exclusiva del venue, exportables en formatos estándar en cualquier momento.
- **Software:** el venue recibe una **licencia de uso perpetua, exclusiva para su operación**, sobre la plataforma entregada.

---

## 8. Supuestos y dependencias

El plazo de 2 meses asume que el venue provee oportunamente:

1. Cuenta de Stripe activa (o documentación para crearla) antes de la semana 3.
2. Plano o referencia del recinto para construir el mapa de asientos, en la semana 1.
3. Contenidos del primer evento (imágenes, textos, precios) antes de la semana 6.
4. Un interlocutor con capacidad de decisión y aprobaciones en un máximo de **3 días hábiles** por hito.
5. Un evento real programado dentro de la ventana de la semana 8 (o inmediatamente posterior) para el piloto de aceptación.

Los retrasos en estas dependencias desplazan el cronograma en la misma proporción, sin alterar el precio fijo.

---

## 9. Paso siguiente

Aprobada esta propuesta, se firma la orden de trabajo y el cronograma inicia con la sesión de diseño de la semana 1. El detalle técnico completo de la solución —decisiones de arquitectura, flujo de compra bajo alta demanda, validación en puerta y métricas— está en el documento de arquitectura adjunto.
