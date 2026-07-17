# Fase 2 — UX, colores, tecnología y analítica de las plataformas de boletería

**Fecha:** 17 de julio de 2026
**Spec:** [specs/analisis-mercado-boleteria.md](../specs/analisis-mercado-boleteria.md) (sección 6)
**Complementa a:** [informes/analisis-mercado-boleteria.md](analisis-mercado-boleteria.md)

> Nota sobre "pantallazos": este análisis es de escritorio, sin navegador para capturar pantallas reales. En su lugar: (a) cada flujo está descrito paso a paso con detalles visuales documentados y enlaces a las páginas oficiales para verlos en vivo, y (b) se construyeron **mockups HTML propios** de la vista del cliente y la del promotor como referencia visual de diseño.

---

## 1. Identidad visual: qué colores maneja cada plataforma

| Plataforma | Primario | Secundario / acentos | Fondo | Modo por defecto |
|---|---|---|---|---|
| **Ticketmaster** | `#026CDF` azul "Azure" | `#004075` azul profundo, `#4191E7` claro | Blanco | Claro |
| **StubHub** | `#3F1D75` púrpura profundo | `#8647FD` violeta, `#B3AEF8` lavanda, CTA magenta | Blanco | Claro |
| **SeatGeek** | `#FF5B49` "Sunset Orange" | `#BA2626` rojo oscuro | `#F8F7F5` crema | Claro |
| **TickPick** | `#3399FF` "TP Blue" | `#185BDB` lapis, `#0C177B` navy; acentos verde `#00D66C`, púrpura `#6C31F5`, rojo `#FF0066` | Blanco / oscuro `#0F161E` | Claro |
| **Gametime** | `#19CE85` "Gametime green" | `#0066FF` azul, `#6E49EB` púrpura | `#0C0C0D` casi negro | **Oscuro** |
| **DICE** | Negro + blanco (monocromo) | Acentos "Vibrations": `#0000FE`, `#4BFA94`, `#F2EF1D`, `#A783FF` | Negro (app) | **Oscuro (app)** |
| **Eventbrite** | `#F05537` naranja | `#39364F` gris "Martinique" | Blanco | Claro |
| **AXS** | `#0069D6` azul | `#003268` navy | Blanco / `#F6F6F6` | Claro |

**Lectura estratégica:** las plataformas transaccionales masivas (Ticketmaster, AXS, TickPick, StubHub) usan azules/púrpuras sobre blanco — confianza y neutralidad. Las mobile-first orientadas a jóvenes (Gametime, DICE) usan **modo oscuro** con un acento vibrante — estética "nightlife". El color funcional del mapa de asientos es independiente de la marca: Ticketmaster pinta disponibilidad en azul (más oscuro = más inventario) y reventa en rosa; SeatGeek pinta cada punto según **Deal Score** (verde = buen precio, amarillo = justo, rojo = caro).

Fuentes: [design.ticketmaster.com/brand/color](https://design.ticketmaster.com/brand/color/), [brand.seatgeek.com/color](https://brand.seatgeek.com/color), [lp.tickpick.com/branding/colors](https://lp.tickpick.com/branding/colors) (verificada en vivo), CSS en vivo de gametime.co / dice.fm / axs.com, [rebrand DICE (It's Nice That)](https://www.itsnicethat.com/news/dice-rebrand-graphic-design-250220), agregadores para StubHub/Eventbrite. Confiabilidad: TickPick/Gametime/DICE/AXS de primera mano; Ticketmaster/SeatGeek de portales oficiales vía snippets; StubHub/Eventbrite de segunda mano.

---

## 2. Cómo se ve la compra (vista del cliente), paso a paso

### Ticketmaster — el flujo de referencia con asientos numerados
1. Página del evento → "Find Tickets" abre el **mapa de asientos interactivo (ISM)**: secciones disponibles en azul (más oscuro = más inventario dentro del filtro); al filtrar por precio, lo que queda fuera se pinta gris.
2. Zoom a nivel de asiento: puntos individuales — azul = disponible, **rosa = reventa verificada**, gris = ocupado; hover muestra el precio.
3. Al seleccionar arranca un **temporizador (~5 min, ajustable por demanda)** visible arriba en todo el checkout; si expira, los asientos vuelven al pool.
4. **All-in pricing** desde 2025 (total con fees visible desde el mapa, por la regla FTC contra junk fees).
5. Checkout: login / cuenta nueva / **guest checkout**; entrega por defecto "Mobile Entry" con **SafeTix** (barcode rotativo + NFC, sin screenshot ni impresión).
Fuentes: [blog ISM](https://blog.ticketmaster.com/interactive-seating-chart/), [help: time limit](https://help.ticketmaster.com/hc/en-us/articles/9642204793617-Why-is-there-a-time-limit-for-checking-out), [Ticketing 101](https://www.ticketmaster.com/ticketing101).

### SeatGeek — el mapa con inteligencia de precio
1. Mapa interactivo de **puntos de colores por Deal Score (1–10)**: verde = buen negocio, amarillo = justo, rojo = sobrevalorado; vista panorámica real desde el asiento.
2. **All-in pricing por defecto desde mayo 2025**.
3. Checkout con email de entrega + contacto + pago; estados de orden Pending → Confirmed → Fulfilled (la mayoría en 24 h, por ser marketplace).
4. Entrega: e-ticket en su app o **transferencia móvil** vía Ticketmaster/AXS/app del equipo (24–48 h antes del evento).
Fuentes: [Deal Score](https://seatgeek.com/deal-score), [all-in pricing press](https://seatgeek.com/press/SeatGeek-Now-Shows-Total-Prices-Upfront-for-Fans), [how to buy](https://support.seatgeek.com/hc/en-us/articles/360037250494-How-do-I-buy-tickets-on-SeatGeek).

### DICE — el flujo mínimo sin mapa
1. Feed curatorial en app (UI negra, tarjetas fotográficas); casi todo es admisión general — se elige tipo y cantidad de una lista, sin mapa.
2. Precio "lo que ves es lo que pagas" (fee incluido desde el inicio).
3. **Checkout de 2 pasos** con Apple Pay/tarjeta guardada; **cuenta obligatoria** (el boleto vive en el perfil, sin PDF ni email).
4. El **QR se activa ~2 horas antes** del evento con advertencia de no screenshot; para shows agotados, **Waiting List** con reasignación automática a precio de cara.
Fuentes: [DICE fees](https://dicefm.zendesk.com/hc/en-gb/articles/19919684020113-How-DICE-fees-work), [activación de tickets](https://dicefm.zendesk.com/hc/en-gb/articles/19413725197713-How-to-activate-your-tickets-on-the-day-of-the-event), [Wikipedia](https://en.wikipedia.org/wiki/Dice_(ticketing_company)).

### Eventbrite — el flujo self-service
1. Página del evento (blanco + CTA naranja) → lista de tipos de entrada; con asientos reservados hay mapa "shoppable" y el mismo pedido sienta al grupo junto.
2. Al iniciar la orden corre un **countdown (~8 min por defecto**, extensible por el organizador; dato de fuente terciaria — Eventbrite no lo publica).
3. Checkout en un solo formulario: contacto + preguntas custom del organizador + pago; fees NO all-in por defecto (se suman salvo que el organizador los absorba); la cuenta se crea sola con el email.
4. Entrega inmediata: email con PDF/QR + app.
Fuentes: [reserved seating](https://www.eventbrite.com/organizer/features/reserved-seating/), [help center](https://www.eventbrite.com/help/en-us/).

**Patrones que un build propio debe copiar:** temporizador de reserva visible (5–8 min), all-in pricing (ya es exigencia regulatoria FTC en EE.UU.), mapa con codificación semántica de color (disponibilidad o valor), guest checkout con creación silenciosa de cuenta, y entrega mobile-first con QR dinámico.

---

## 3. Cómo se ve el lado del promotor (crear evento + analítica)

### Creación de evento

| Plataforma | Flujo | Aprobación | Campos clave |
|---|---|---|---|
| **Eventbrite** | Self-service total, minutos ("create with AI" disponible) | **Ninguna** — autopublicable | Título, resumen, categoría, fecha/hora, ubicación, imágenes/video, tipos de boleto (Free/Paid/Donation) con aforo y precio por tipo, order form con preguntas custom, política de reembolso, payout |
| **Ticketmaster TM1** | Solo clientes; **plantillas reutilizables** (floor plans, price grids, ticket types) — de días a **5–10 min** por evento | Workflow interno: el promotor solicita cambios de precio y el box office aprueba (vista "Changes/Current/Difference") | Mapa drag-and-drop con impacto de revenue en tiempo real, price levels por zona, holds con colores, 40+ plantillas de ofertas/presales |
| **Tixr** | Clientes; un evento GA con tiers y add-ons "en una sesión" | No mencionada | Título, fechas, flyer 550×770 + mobile 640×359, tiers con **triggers por inventario y/o fecha**, payment plans, waitlist con preautorización, red de promoters/afiliados con landing propia |
| **DICE (MIO)** | Self sign-up (UK/IE) | **Sí — DICE revisa cada listing** y puede rechazarlo | Custom ticket types, extras (VIP, meet & greet) |
| **AXS** | 100% gestionado por AXS (enterprise) | Contractual | No público |

### Qué métricas muestra el dashboard al promotor

| Métrica | Eventbrite | TM1 | Tixr | DICE | AXS |
|---|---|---|---|---|---|
| Ventas por día/hora (tiempo real) | ✅ | ✅ | ✅ "zero-lag" | ✅ | ✅ Instant AXS |
| Ingresos brutos/netos | ✅ | ✅ | ✅ | ✅ | ✅ |
| Vendido vs. disponible por tier | ✅ (por ticket type) | ✅ (+ holds) | ✅ | ✅ | ✅ |
| Embudo de conversión | ✅ Visitas → Órdenes → Boletos | Tráfico de página + ventas | Velocidad de venta + correlación con campañas | — | Fuentes de tráfico |
| Atribución por canal | ✅ last-touch (creator tools/paid/direct/marketplace) | Pixels de campaña propios | GA, Meta **CAPI server-side**, TikTok | — | Atribución por promotor |
| Geografía de compradores | ✅ ciudad/estado/país | No público | ✅ **mapas de cluster y penetración** | ✅ geo-concentración (Fan Insights) | ✅ demográfico/mercado |
| Demografía | — | ✅ (TM1 Marketing) | ✅ **90+ data points por fan** | Afinidad de artistas, propensión | ✅ AXS IQ |
| Día del evento (escaneo) | App Organizer básica | ✅ entradas, **rechazos**, salidas, % attended, scan log export | ✅ | Escaneo in-app | ✅ tiempo real |
| Comparación entre eventos | ✅ | ✅ Sales Comparison (guardable + email programado) | ✅ | — | — |
| Señal de demanda insatisfecha | — | — | Waitlist | ✅ **Waiting List cuenta fans exactos de un show agotado** | — |
| Dynamic pricing nativo | — | Platinum/Pricemaster | ✅ automático (por inventario/fecha/velocidad) | No (postura anti) | ✅ |
| Export/API | Excel + API | Scan log, email programado | API + webhooks + CSV | CSV + **GraphQL Ticket Holders API** | Data Feeds diarios |

**Lectura:** el estándar mínimo de un dashboard de promotor es: ventas en tiempo real + desglose por tier + embudo + geografía por ciudad + export. Los diferenciadores de élite: correlación campaña→pico de ventas (Tixr), waiting list como sensor de demanda (DICE), y comparación multi-evento programada (TM1).

Fuentes: [Eventbrite Analytics](https://www.eventbrite.co.uk/help/en-gb/articles/237711/how-to-use-the-analytics-tool/) · [Traffic & Conversion](https://www.eventbrite.co.uk/help/en-gb/articles/840658/view-your-traffic-and-conversion-report/) · [TM1 Event Creation](https://business.ticketmaster.com/solutions/event-creation-management/) · [TM1 insights](https://business.ticketmaster.com/new-insights-with-tm1-events/) · [TM1 Sales Comparison](https://business.ticketmaster.com/business-solutions/track-compare-and-analyze-your-events/) · [Tixr Studio](https://creators.tixr.com/products/studio) · [Tixr tiers](https://support.tixr.com/building-your-event-tickets-tiers) · [DICE partners](https://dice.fm/partners) · [DICE GraphQL API](https://partners-endpoint.dice.fm/graphql/docs/index.html) · [AXS Data & Analytics](https://solutions.axs.com/us/data-analytics/).

---

## 4. Qué tecnologías manejan

| Plataforma | Backend | Datos | Nube | Eventos/colas | Detalle distintivo | Confiabilidad |
|---|---|---|---|---|---|---|
| **Ticketmaster** | Microservicios (Node.js, Python, Java) descomponiendo un legado de 40+ años | RDS, ElastiCache | **AWS** (Lambda, ECS, API Gateway) | **Kafka/Confluent** como columna vertebral + MSK, Kinesis, SNS/SQS | Hasta **~1M requests/segundo**; "inventory stream" unificado; ML antifraude sobre el stream | Alta (casos oficiales AWS + Confluent) |
| **SeatGeek** | Python + FastAPI, **Go**, C#/.NET Core | Postgres, Redis, Memcached, Elasticsearch; CDC con **Debezium** | **AWS** + Fastly | Kafka | Waiting room propia serverless (DynamoDB+Lambda); simulan on-sales masivos con **AWS Batch**; frontend Next.js/TypeScript | Alta (blogs AWS + ChairNerd) |
| **StubHub** | Java, Go, Python | **Oracle** (núcleo transaccional) + BigQuery | **Google Cloud** (GKE, Bare Metal Solution para Oracle, ~1,500 máquinas) | — | Migró Oracle a GCP Bare Metal sin reescribir (+64% rendimiento) | Alta (caso oficial GCP) |
| **Eventbrite** | **Python + Django** (microservicios), Java, Node | MySQL, Redis, Elasticsearch, Cassandra | — | No confirmado | Frontend React | Media |
| **DICE** | **Elixir** (migró desde Go) | — | Kubernetes + Helm, operator propio | — | Eligió Elixir específicamente por las **ráfagas de on-sale**; API GraphQL + REST; monorepo umbrella | Media-alta (ingeniero de DICE en HN) |
| **Gametime** | **Go** (microservicios) | PostgreSQL, MySQL, MongoDB, DynamoDB | AWS | Kafka + RabbitMQ | ~1M requests/minuto; ingesta de inventario en tiempo real de 60k+ eventos | Media (job posting oficial) |
| **TickPick** | **C#/.NET** | No público | AWS (señales mixtas con Azure) | No público | Frontend React/React Native/Next.js | Media-baja (solo job postings) |
| **AXS** | .NET/C# + Node.js | SQL Server, PostgreSQL, MySQL, DynamoDB, Elasticsearch | AWS | Kafka | React+TypeScript, Terraform, SOA para on-sales masivos | Media (job postings oficiales) |

**Patrones para el build propio:** (1) **Kafka aparece en 4 de 8** — el inventario como stream de eventos es el patrón dominante; (2) AWS domina (6 de 8; StubHub es la excepción en GCP); (3) los lenguajes de la capa caliente de on-sale son Go y Elixir (concurrencia barata); (4) Postgres/MySQL para lo transaccional + Redis para locks/caché + Elasticsearch para búsqueda es el trío estándar; (5) probar la carga ANTES del on-sale (AWS Batch en SeatGeek) es práctica de élite, no opcional.

---

## 5. Datos del comprador: qué pedir y qué capturar

### 5.1 Qué piden las plataformas reales en el checkout

| Plataforma | ¿Cuenta obligatoria? | Obligatorios | Verificación |
|---|---|---|---|
| Ticketmaster | No (guest checkout; recibir transferencia sí exige cuenta) | Email, entrega, facturación + tarjeta | Cuenta: email + **teléfono OTP** (rechazan VoIP — antibots) |
| Eventbrite | No — la cuenta se crea sola con el email | **Nombre + email** + pago (mínimo del mercado) | Ninguna |
| DICE | **Sí** | Nombre (como en el ID), email, **teléfono verificado SMS**, fecha de nacimiento | SMS 4 dígitos |
| StubHub | No (guest con código de 6 dígitos) | Email + teléfono | Código de acceso a la orden |
| TickPick | Orientado a cuenta | Email, nombre, pago, ZIP | No documentada |

### 5.2 La matriz para nuestro checkout

| Categoría | Datos | Justificación |
|---|---|---|
| **Obligatorios (mínimo viable)** | Email, nombre, método de pago + **ZIP/código postal de facturación** | Entrega del boleto, antifraude AVS. Es el estándar del mercado — más fricción = menos conversión |
| **Comunes (recomendados)** | Teléfono móvil (idealmente verificado por SMS en compras de alta demanda) | Anti-bots (patrón Ticketmaster/DICE), recuperación de orden, canal SMS (ROI 22x documentado) |
| **Para analítica potente (opcionales, pedir con incentivo)** | Fecha de nacimiento o rango de edad, género (opcional), ciudad de residencia, artista/género favorito (onboarding tipo DICE), consentimiento de marketing | Segmentación demográfica, afinidad para recomendaciones, LTV. Pedirlos POST-compra o en el onboarding de la app, nunca bloqueando el checkout |
| **Por asistente (eventos B2B/festivales)** | Nombre de cada asistente (patrón Eventbrite order form) | Personalización de la entrada, control de reventa, datos 1:1 en compras de grupo |

### 5.3 Qué se captura automáticamente (sin pedirlo) y su base legal

| Dato | Cómo | Precisión | Base legal |
|---|---|---|---|
| **País/ciudad por IP** | MaxMind/IPinfo; Cloudflare regala `CF-IPCountry` y ciudad con Managed Transforms | País ~99.8%; ciudad ~66% (radio 50 km) — suficiente para heatmap, jamás domicilio | IP = dato personal (GDPR, caso Breyer). Geo agregada server-side sin ligar a perfil: **interés legítimo**. Ligada al perfil del usuario: requiere base sólida y minimización |
| Idioma y dispositivo | Headers HTTP (Accept-Language, User-Agent) | Exacta | Interés legítimo para logs/segmentación agregada; si deviene **fingerprinting** → consentimiento (EDPB Guidelines 2/2023) |
| **UTM + referrer** | Query string / header, first-party | Exacta | Sin consentimiento si no se persiste en cookie de tracking |
| Cookies esenciales (sesión, carrito, antifraude) | First-party | — | Exentas ("estrictamente necesarias", ePrivacy Art. 5(3)) |
| Cookies analíticas/ads, píxeles, fingerprinting | — | — | **UE: consentimiento previo obligatorio** (el interés legítimo NO sustituye; +1,100 sanciones 2021-2025). Brasil (ANPD): consentimiento para no esenciales. **California: opt-out** "Do Not Sell or Share" + respetar señal GPC. **Colombia (Ley 1581): autorización previa e informada**, conservable como prueba, supervisa la SIC |
| **ZIP de facturación** | Viene del pago | Exacta a nivel código postal | Dato dado voluntariamente para procesar el pago; usarlo para analítica interna agregada es defendible; para marketing → consentimiento |

**Regla práctica:** sin banner de consentimiento puedes tener: geo país/ciudad por IP server-side, idioma, dispositivo, UTM/referrer, cookies esenciales y ZIP de facturación agregado. Todo identificador persistente para tracking (GA4 client-side, Meta Pixel, fingerprint) requiere el banner en UE/Brasil y opt-out en California.

### 5.4 El mapa de calor geográfico — cómo se construye

Tres capas de ubicación, de menos a más precisa, que se cruzan:
1. **IP del visitante** (todas las visitas, incluso sin compra): país exacto, ciudad ~66% — alimenta el heatmap de DEMANDA (quién mira sin comprar).
2. **ZIP/código postal de facturación** (solo compradores): precisión de barrio — alimenta el heatmap de CONVERSIÓN. Los promotores lo usan para descubrir de qué códigos postales viajan los fans y reasignar presupuesto de ads a los ZIP que convierten.
3. **Ciudad del evento** como referencia: la distancia comprador→venue es la métrica clave, porque **el 85% de los asistentes viaja <30 millas** — la demanda es hiperlocal.

Implementación: en cada `purchase` guardar `{geo_ip_city, billing_zip, venue_city, distancia_km}`; el heatmap es un agregado por ZIP/ciudad sobre el warehouse. Con visitas sin compra (IP only) se construye el mapa de demanda insatisfecha: ciudades con muchas vistas y pocas compras = candidatas a fecha nueva o precio distinto.

---

## 6. Analítica estratégica: cómo responder las preguntas difíciles

### 6.1 El esquema de eventos (modelo GA4 ecommerce, estándar de industria)

```
page_view → view_item_list → view_item (evento; item_category=ciudad/venue, item_variant=tier)
  → add_to_cart → begin_checkout → add_payment_info → purchase (+ refund)
```

Reglas de implementación que separan una analítica confiable de una decorativa:
- **`purchase` SIEMPRE server-side** (desde el webhook del pago): los adblockers + iOS matan 15–50% del tracking client-side; el tagging server-side recupera ~20–30% de conversiones perdidas. El resto del embudo: client-side + réplica server-side.
- **Todo evento lleva**: `event_id, tier, precio, cantidad, utm_*, referrer, geo_ip, device, timestamp` — y en `purchase` además `billing_zip, transaction_id, valor, moneda`.
- **Warehouse como fuente única** (BigQuery/Snowflake): compras + ads + email/SMS + escaneos de puerta unidos por email/user_id. Un CDP composable (Segment/Hightouch) encima. En ticketing ya existe Hive (CRM de fans integrado con Ticketmaster).

### 6.2 Las preguntas difíciles y cómo responderlas

| Pregunta estratégica | Datos que la responden | Señal/umbral documentado |
|---|---|---|
| **¿En qué ciudad hago la próxima parada de la gira?** | Heatmap de demanda (vistas por IP-ciudad sin compra) + geografía de streaming (Spotify for Artists por metro, tendencia 90 días) + box office de artistas comparables | Se corta la fecha si el ingreso proyectado no supera **2.5x el costo de routing**; ciudad con concentración inesperada de oyentes = parada candidata |
| **¿Cuándo lanzo la 2ª fecha?** | Velocidad de venta (boletos/hora tras on-sale) + waiting list (patrón DICE: fans exactos en espera) | El % vendido en presale/primeras 48h es el trigger; forecasting con streaming predice sellouts ~30 días antes |
| **¿Subo el precio? ¿A qué tier?** | Sell-through por tier + elasticidad observada entre fases (early bird → GA) | La sensibilidad al precio crece al alejarse del escenario: los tiers premium aguantan subidas, los baratos no. Práctica: 3–5 tiers con ≥20–25% de diferencia; subir precio si el sell-through proyectado ≥85%. Asignar 20–40% del aforo a fases early para MEDIR la demanda real antes de fijar el resto |
| **¿Qué canal de marketing convierte?** | UTM en todo el embudo + atribución en warehouse (no last-touch simple) | Métrica reina: **costo por boleto vendido por canal**. Los canales cooperan: descubren en social, convierten en email/SMS. Caso real: SMS con ROI 22x ($950k en boletos con $42k de inversión) |
| **¿Cuánto vale un fan? (LTV)** | Historial de compras + escaneos + merch unidos por user_id | Un comprador de este año asiste a 2–3 shows más; "Audience Quality Score" por canal: los fans de social orgánico repiten y refieren, los de ads amplios suelen ser one-time |
| **¿De dónde viene mi demanda insatisfecha?** | Vistas sin compra por geo + drop-off del embudo por ciudad + waiting list | Ciudad con alto `view_item` y bajo `purchase` = problema de precio, fecha o distancia — cada hipótesis se testea distinto |

### 6.3 Mejoras estratégicas por nivel de madurez

1. **Nivel 1 (día 1, casi gratis):** GA4 + eventos estándar, UTM disciplinado en toda campaña, geo por IP server-side, export a warehouse. Responde: qué canal vende, de dónde son los compradores.
2. **Nivel 2 (plataforma media):** `purchase` server-side, dashboard de promotor con embudo + heatmap + velocidad de venta (estándar Tixr/TM1), waiting list como producto (señal de demanda), preguntas opcionales post-compra. Responde: cuándo abrir fecha, qué tier ajustar.
3. **Nivel 3 (élite):** identidad de fan unificada (compras + streaming + escaneos), scoring de propensión (a quién avisarle del próximo show — patrón TM1 "high propensity audiences"), pricing dinámico con guardarraíles (+20–40% de revenue documentado, pero con riesgo de confianza — DICE construyó su marca militando en contra), predicción de sellout. Responde: LTV, elasticidad, routing completo de gira.

---

## 7. Fuentes de la Fase 2

**Checkout y datos:** [Ticketmaster Ticketing 101](https://www.ticketmaster.com/ticketing101) · [TM verificación de cuenta](https://help.ticketmaster.com/hc/en-us/articles/9782182310545) · [Eventbrite order form](https://www.eventbrite.com/help/en-us/articles/246376/) · [DICE create account](https://dicefm.zendesk.com/hc/en-gb/articles/4409604062481-Create-an-account) · [StubHub guest](https://support.stubhub.com/articles/61000276840)

**Legal:** [EDPB Guidelines 2/2023 (ePrivacy Art. 5(3))](https://www.edpb.europa.eu/system/files/2024-10/edpb_guidelines_202302_technical_scope_art_53_eprivacydirective_v2_en_0.pdf) · [IP como dato personal (CookieYes)](https://www.cookieyes.com/blog/ip-address-personal-data-gdpr/) · [CCPA (OAG California)](https://oag.ca.gov/privacy/ccpa) · [ANPD Brasil cookies (Mayer Brown)](https://www.mayerbrown.com/en/insights/publications/2022/11/brazilian-data-protection-authority-issues-guidance-on-cookies) · [Ley 1581 Colombia](http://www.secretariasenado.gov.co/senado/basedoc/ley_1581_2012.html)

**Geo y tracking:** [MaxMind accuracy](https://support.maxmind.com/knowledge-base/articles/maxmind-geolocation-accuracy) · [Cloudflare IP geolocation](https://developers.cloudflare.com/network/ip-geolocation/) · [GA4 ecommerce](https://developers.google.com/analytics/devguides/collection/ga4/ecommerce) · [server-side tracking (Stape)](https://stape.io/blog/server-side-tagging)

**Analítica estratégica:** [insights.live demand forecasting](https://insights.live/blog/event-demand-forecasting/) · [insights.live box office](https://insights.live/blog/promoters-analyze-concert-box-office-data-before-booking-tours/) · [Audience Republic attribution](https://www.audiencerepublic.com/blog/attribution-for-live-events-the-questions-every-venue-and-promoter-should-be-asking) · [streaming y routing (AMG)](https://amgmusic.org/did-you-know-streaming-data-impacts-tour-routing/) · [elasticidad (ACEI)](https://culturaleconomics.org/trends-in-concert-ticket-pricing-and-consumer-preferences-whats-driving-the-changes/) · [Ticketmaster + Hive](https://business.ticketmaster.com/ticketmaster-and-hive-partner-to-power-smarter-event-marketing/)

**Stacks:** [Confluent–Ticketmaster](https://www.confluent.io/customers/ticketmaster/) · [AWS–Ticketmaster serverless](https://aws.amazon.com/blogs/media/ticketmaster-optimizes-add-on-offers-for-fans-with-a-unified-serverless-data-stream-powered-by-aws/) · [AWS–SeatGeek waiting room](https://aws.amazon.com/blogs/architecture/build-a-virtual-waiting-room-with-amazon-dynamodb-and-aws-lambda-at-seatgeek/) · [AWS–SeatGeek load testing](https://aws.amazon.com/blogs/hpc/how-seatgeek-simulates-massive-load-with-aws-batch-to-prepare-for-big-events/) · [GCP–StubHub](https://cloud.google.com/customers/stubhub/) · [DICE Elixir (HN)](https://news.ycombinator.com/item?id=32722391) · [Eventbrite engineering](https://www.eventbrite.com/engineering/)

**Límites:** los hexes de StubHub/Eventbrite son de agregadores (segunda mano); el timer de Eventbrite (~8 min) es un dato de 2014; los help centers de StubHub/TickPick/DICE bloquean fetch directo (403) — sus filas se basan en snippets de páginas oficiales; el detalle interno de AXS (Flash Seats) y el stack de TickPick no son públicos.
