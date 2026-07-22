# Spec: Análisis profundo del mercado de plataformas de boletería

**Fecha:** 2026-07-17
**Estado:** Aprobado para ejecución
**Metodología:** Spec-Driven Development — este documento define el alcance y los criterios de aceptación de la investigación antes de ejecutarla.

## 1. Objetivo

Realizar un análisis de mercado de plataformas de venta de boletos (ticketing) para responder, con datos verificables:

1. **¿Cuánto costaría crear una plataforma de este tipo?** — especialmente una del calibre de Ticketmaster (build propio en nube).
2. **¿Cuánto cuesta en cambio pagarle a plataformas/empresas existentes** (SaaS / white-label) para montar nuestra propia boletería?
3. **Plan con tiempos** para construir la plataforma (fases, hitos, equipo, duración).

## 2. Alcance

### 2.1 Plataformas a analizar (mínimo 10)

Semilla dada por el usuario:
1. Ticketmaster (https://www.ticketmaster.com/) — referencia principal
2. Ritz Theatre (https://www.ritztheatre.com/) — ejemplo de venue individual con boletería propia/tercerizada
3. TickPick (https://www.tickpick.com) — reventa sin fees al comprador
4. Gametime (https://gametime.co) — last-minute mobile-first

Candidatas para completar 10+ (elegir las más relevantes):
- StubHub, SeatGeek, Vivid Seats, AXS, Eventbrite, DICE, Ticketleap, Etix, See Tickets, Fever, Tixr

### 2.2 Dimensiones de comparación por plataforma

- Modelo de negocio (primario vs. reventa/secundario vs. híbrido; comisiones y fees típicos)
- En qué destaca / diferenciador clave ("si X compañía tiene estas características…")
- Segmento objetivo (estadios/arenas, teatros, conciertos, deportes, eventos pequeños)
- Escala (GMV, ingresos, usuarios, eventos — cuando haya datos públicos)
- Características técnicas visibles: mapas de asientos interactivos, precios dinámicos, app móvil, transferencia de boletos, anti-bots, entrada digital (QR/NFC/SafeTix)
- Stack tecnológico conocido (si hay información pública)

### 2.3 Proveedores de sistemas de boletería (white-label / SaaS para montar tu propia taquilla)

Identificar empresas que venden la tecnología para que un venue/promotor monte su boletería, con precios:
- Candidatos: AudienceView, Ticketure, ThunderTix, TicketSpice, Purplepass, Showpass, Ticket Tailor, Tix, Eventix, Spektrix, Tessitura, SeatGeek Enterprise (SRO), Secutix, Weezevent, vivenu, Seats.io (componente de mapas de asientos)
- Para cada uno: modelo de precios (fee por boleto, suscripción, % de ventas), a quién sirve, qué incluye

### 2.4 Análisis de costos

**Opción A — Pagar a una plataforma/proveedor:**
- Costo por boleto / suscripción mensual / % de ventas
- Escenarios de volumen (p. ej. 10k, 100k, 1M boletos/año)

**Opción B — Construir en la nube (build propio):**
- Costos de desarrollo: equipo (roles, salarios), duración por fase
- Costos de infraestructura en nube (AWS/GCP/Azure): estimación para tráfico normal y picos de on-sale (el problema técnico característico de la boletería)
- Costos recurrentes: mantenimiento, pasarela de pagos, fraude/anti-bots, soporte, cumplimiento (PCI-DSS)
- Tres niveles de estimación: MVP, plataforma media, escala Ticketmaster

### 2.5 Plan de construcción con tiempos

- Roadmap por fases (MVP → producto completo → escala) con duración estimada de cada fase
- Composición del equipo por fase
- Riesgos principales

## 3. Entregables

1. **Informe de investigación** con citas/fuentes, en español.
2. **Tabla comparativa** de las 10+ plataformas.
3. **Tabla de proveedores** white-label con precios.
4. **Modelo de costos** Opción A vs. Opción B con escenarios.
5. **Roadmap con tiempos** para el build propio.

## 4. Criterios de aceptación

- [x] ≥10 plataformas de venta analizadas y comparadas (12: Ticketmaster, StubHub, SeatGeek, Vivid Seats, TickPick, Gametime, AXS, Eventbrite, DICE, Fever, Tixr + caso Ritz Theatre)
- [x] ≥8 proveedores de tecnología de boletería identificados con modelo de precios (14: ThunderTix, Ticketor, TicketSpice, Ticket Tailor, Purplepass, Tix.com, Showpass, Weeztix/Eventix, Spektrix, Tessitura, AudienceView, Secutix, vivenu, SeatGeek SRO + componentes Seats.io/Stripe/Queue-it)
- [x] Estimación de costo de build en 3 niveles (MVP / media / escala Ticketmaster) con supuestos explícitos
- [x] Comparación de costo "pagar vs. construir" con escenarios de volumen (10k / 100k / 1M boletos/año)
- [x] Plan con fases y tiempos (Fase 0–3, mes 5–7 MVP, mes 12–16 completa)
- [x] Afirmaciones clave respaldadas por fuentes citadas (22 claims verificados 3-0 con fuentes SEC/oficiales; 3 refutados y excluidos)

**Entregable:** [informes/analisis-mercado-boleteria.md](../informes/analisis-mercado-boleteria.md) (2026-07-17)

## 6. Fase 2 — UX, tecnología y analítica (añadido 2026-07-17)

### 6.1 Alcance adicional

1. **Identidad visual**: paleta de colores de cada plataforma principal (brand guidelines/press kits).
2. **Vista del cliente**: cómo se ve el flujo de compra (selección de boleto/asiento → checkout) por plataforma; referencia visual mediante descripción documentada + enlaces oficiales + mockups HTML propios (no hay navegador para capturas reales).
3. **Vista del promotor/organizador**: cómo es la creación de un evento y qué métricas muestra el dashboard de analítica (Eventbrite, Ticketmaster TM1, AXS, Tixr, DICE, etc.).
4. **Stack tecnológico** conocido de cada plataforma (blogs de ingeniería, StackShare, ofertas de empleo).
5. **Datos del comprador**: qué es obligatorio pedir en el checkout, qué es común, qué pedir para analítica potente, y qué se puede capturar automáticamente (IP→geo, cookies, device, UTM) con sus límites legales (GDPR/CCPA/consentimiento).
6. **Analítica estratégica**: cómo construir mapas de calor por país/ciudad, y qué modelo de datos/eventos permite responder las preguntas difíciles del negocio (pricing, demanda, churn, atribución).

### 6.2 Criterios de aceptación (Fase 2)

- [x] Paleta de colores documentada para 8 plataformas (hex primario/secundario/fondo/modo)
- [x] Flujo de compra (cliente) descrito paso a paso para 4 plataformas (Ticketmaster, SeatGeek, DICE, Eventbrite) + extras StubHub/Gametime, con enlaces
- [x] Flujo de creación de evento (promotor) + métricas del dashboard para 5 plataformas (Eventbrite, TM1, Tixr, DICE/MIO, AXS)
- [x] Stack tecnológico documentado para 8 plataformas con nivel de confiabilidad por fuente
- [x] Tabla de datos del checkout: obligatorios / comunes / recomendados / automáticos, con base legal (GDPR, ePrivacy/EDPB, CCPA, LGPD, Ley 1581)
- [x] Diseño de analítica estratégica: esquema GA4, geo heatmap en 2 capas (IP + ZIP), 6 preguntas de negocio con señales/umbrales
- [x] Mockups HTML de vista cliente y vista promotor (publicados como Artifact)

**Entregables Fase 2:** [informes/analisis-ux-tecnologia-analitica.md](../informes/analisis-ux-tecnologia-analitica.md) · Mockups: https://claude.ai/code/artifact/d65b3f3e-1239-49c1-913f-388608e56cb2 (2026-07-17)

## 5. Supuestos

- Moneda: USD. Salarios: mercado LATAM y/o remoto mixto se indicará como alternativa al costo US.
- "Escala Ticketmaster" = capacidad para on-sales masivos (cientos de miles de usuarios concurrentes), mapas de asientos en tiempo real, anti-bots, mercado secundario.
- El análisis es de escritorio (fuentes públicas); las cifras de costos son estimaciones fundamentadas, no cotizaciones.
