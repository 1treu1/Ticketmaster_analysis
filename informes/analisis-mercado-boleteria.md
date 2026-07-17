# Análisis de mercado: plataformas de boletería y costo de construir una propia

**Fecha:** 17 de julio de 2026
**Spec:** [specs/analisis-mercado-boleteria.md](../specs/analisis-mercado-boleteria.md)
**Metodología:** Investigación de escritorio con verificación adversarial — 24 fuentes leídas, 111 afirmaciones extraídas, las 25 más importantes verificadas con 3 votos independientes cada una (22 confirmadas, 3 refutadas), más 3 búsquedas complementarias dirigidas. Los datos financieros provienen de reportes oficiales ante la SEC y páginas de precios oficiales (verificadas el 17-jul-2026). Las estimaciones propias están marcadas explícitamente como tales.

---

## 1. Resumen ejecutivo

- **El mercado tiene tres capas**: (a) gigantes verticalmente integrados (Ticketmaster con $3,081M de ingresos de ticketing y 346M de boletos con fee en 2025; StubHub con $9.2B transaccionados), (b) marketplaces especializados que compiten por nicho (TickPick sin fees al comprador, Gametime en last-minute, DICE en música indie), y (c) decenas de proveedores SaaS/white-label que te montan una boletería completa desde **$20/mes + $1 por boleto**.
- **No necesitas construir nada para tener tu propia taquilla**: con Ticketor puedes operar una plataforma white-label "tipo Ticketmaster" (donde otros organizadores se registran bajo TU marca) por ~$100–150/mes + 2.5% + $0.09–0.19/boleto. Con ThunderTix, TicketSpice o Ticket Tailor montas la boletería de un venue por $1–1.25/boleto. Además, en este negocio los fees casi siempre **se trasladan al comprador**, así que el costo neto para el organizador tiende a cero.
- **Construir una plataforma propia** cuesta desde ~$120k–400k (MVP con equipo LATAM/agencia) hasta $2–5M (plataforma media completa en 18–24 meses) — y "escala Ticketmaster" es un proyecto de $50–150M+ y 4–6 años que solo tiene sentido con contratos de venues asegurados. La razón económica para construir no es ahorrar fees, sino **capturar el fee de servicio (15–25% del valor del boleto) como ingreso propio**.
- **Regla de decisión**: <100k boletos/año → SaaS sin dudarlo. 100k–1M → white-label/reseller o SaaS enterprise (Spektrix ~1–3.3% de ventas). >1M boletos/año con marca y distribución propias → empieza a justificarse el build, por captura de fees, no por ahorro.

---

## 2. Comparativa de plataformas de venta (12 casos)

### 2.1 Tabla comparativa

| Plataforma | Modelo | Fees típicos | Segmento | Escala (dato público más reciente) | En qué destaca |
|---|---|---|---|---|---|
| **Ticketmaster** (Live Nation) | Primario + secundario, integrado con promotor (Live Nation) y venues exclusivos | Service fee + facility fee, varía por evento; reporte del Senado de EE.UU. documenta fees altos y precios dinámicos (Platinum/Pricemaster) | Arenas, estadios, giras top | **$3,081M ingresos ticketing FY2025 (+3%); 346M boletos fee-bearing; GTV conciertos $26B** (SEC) ✔️ | Escala y exclusividades; SafeTix (barcode rotativo ~15s + NFC); Smart Queue anti-bots; mapas interactivos en tiempo real |
| **StubHub** (NYSE: STUB) | Marketplace secundario (reventa) global | Take rate efectivo **~19% del GMS** (revenue $1.7B / GMS $9.2B, FY2025, SEC) ✔️ | Reventa de deportes/conciertos | **GMS $9.2B FY2025 (+6%)** ✔️ | El marketplace de reventa más grande; liquidez global |
| **SeatGeek** | Híbrido: marketplace secundario + **primario enterprise (SRO)** — socio de 6 equipos NFL (Cowboys, Ravens, Cardinals, Saints, Commanders, Titans) | Fees variables al comprador (no publica tarifa fija) | Deportes, venues enterprise | Privada; sin cifras públicas auditadas | Mejores mapas (vistas 3D desde el asiento), **Deal Score** de valor; construyó su propia waiting room serverless en AWS ✔️ |
| **Vivid Seats** (ex-NASDAQ: SEAT) | Marketplace secundario + white-label ("Private Label") | Service + delivery fees al comprador | Reventa deportes/conciertos | **GOV $2,704M FY2025 (-31%); ingresos $570.8M** (10-K SEC) ✔️ — en contracción fuerte | Programa de lealtad; línea Private Label ($57M de ingresos) — hasta un marketplace grande vende marca blanca |
| **TickPick** | Marketplace secundario **sin fees al comprador** | Comprador: **0%**; vendedor: **~15%** de comisión | Reventa, comprador sensible al precio | **~$1B GMV/año (2024); inversión de $250M** de Brighton Park (la mayor del sector a esa fecha); 14M descargas | "No buyer fees" — el precio listado es el final; BestPrice Guarantee |
| **Gametime** | Marketplace mobile-first de **último minuto** | Fee al comprador incrustado en "All-In Pricing" (~10–15% est. de terceros) | Deportes/conciertos last-minute | **+$1B en boletos acumulado (2022); >$500M ventas 2022**; funding ~$75M | Compra en ~2 taps hasta 90 min después de iniciado el evento; >10% de sus ventas ocurren con el evento ya empezado |
| **AXS** (AEG) | Primario enterprise + secundario propio (como Ticketmaster, pero del ecosistema AEG) | No publica tarifas estándar (all-in antes de pagar); reventa: fee vendedor tope 10% | Arenas/festivales AEG: The O2, Red Rocks, Coachella, LA28 | **~50M boletos/año** (dato 2019, el último público); compró mayoría de SISTIC (2025) | **AXS Mobile ID** (boleto = identidad digital, sin PDF): control total de transferencia y reventa |
| **Eventbrite** (NYSE: EB) | Self-service SaaS + fees por transacción | **3.7% + $1.79/boleto + 2.9% procesamiento** (EE.UU.); gratis para eventos gratuitos | Eventos pequeños/medianos, autoservicio | **Ingresos FY2025 ~$290–293M; 19.1M boletos pagados en Q3-2025 (-3%)** (SEC) | Descubrimiento/distribución de audiencia + autoservicio total; 162k creadores de pago |
| **DICE** (adquirida por Fever, jun-2025) | Mobile-only para música en vivo | All-in para el fan; **~7–10% al organizador** (est. de terceros sobre su help center) | Conciertos, clubes, festivales indie | ~60k eventos (2025); levantó $122M (SoftBank) + $65M; vendida a Fever tras casi entrar en administración | Anti-reventa estructural: QR dinámico activado ~2h antes, transferencia solo in-app, **waiting lists** con reventa a precio de cara |
| **Fever** | Descubrimiento de experiencias + ticketing + contenido propio ("Fever Originals", ej. Candlelight) | Comisión negociada por partner (no pública) | Experiencias/ocio urbano; con DICE, también música | **Valuación ~$1.8–2B; ~$527M levantados; 40+ países; ~200M personas alcanzadas/mes** | Motor de demanda basado en datos + producción de contenido original — no es solo boletería |
| **Tixr** | "Commerce" enterprise para eventos: boletos + F&B + merch + upsells en una transacción | Revenue share custom, sin costo inicial | Festivales, deportes, venues grandes; 700+ clientes en 60 países | **~$1B ventas/año procesadas; ~20M boletos/año**; rentable, solo ~$16M de capital externo | Comercio unificado más allá del boleto; Fan-Driven Marketing |
| **Ritz Theatre** (Elizabeth, NJ — caso venue individual) | **Sin boletería propia**: sitio Wix con listado de eventos; cada botón "comprar" enlaza al proveedor del promotor | N/A (los fija cada plataforma externa) | Teatro histórico ~2,800 butacas, fuerte programación latina | 10 eventos del cartel actual: 4 en Tickeri, 3 en Boletos Express, 1 Ticketmaster, 2 otros | El modelo de costo mínimo absoluto: cero infraestructura, el ticketing lo resuelve el promotor de cada show |

✔️ = dato verificado adversarialmente (3 votos independientes, fuente primaria SEC/oficial).

### 2.2 Lecturas clave de la comparativa

1. **Cada plataforma gana por UNA cosa, no por hacerlo todo**: Ticketmaster por exclusividades con venues; StubHub por liquidez; TickPick por precio transparente; Gametime por velocidad/último minuto; DICE por confianza anti-reventa; SeatGeek por UX de mapas; AXS por control de identidad del boleto; Eventbrite por autoservicio; Fever por generación de demanda; Tixr por comercio integral. **Una plataforma nueva necesita elegir su "una cosa".**
2. **El poder de Ticketmaster no es (solo) tecnología, es distribución**: sus contratos exclusivos con venues y su integración con Live Nation (promotor) le garantizan inventario. Replicar el software es lo más barato del problema; replicar el inventario es lo más caro.
3. **El fee es el modelo de negocio**: StubHub captura ~19% de cada transacción; los marketplaces de reventa cobran 20–30% combinado entre comprador y vendedor. Quien construye su propia boletería no "ahorra" fees — pasa a **cobrarlos**.
4. **El mercado castiga a los débiles**: Vivid Seats cayó -31% en GOV en un año y fue deslistada; DICE quemó $187M y terminó vendida de urgencia. Escala sin diferenciación no protege.
5. **Anti-fraude es un estándar de facto**: SafeTix (barcode rotativo ~15s + NFC) marca la referencia, aunque un análisis de ingeniería inversa ([conduition.io](https://conduition.io/coding/ticketmaster/)) demostró que el barcode se genera con TOTP estándar (SHA-1, paso 15s) reproducible offline — la seguridad real es menor que la del marketing, y la afirmación de que "vincula el boleto al teléfono impidiendo redistribución" fue refutada en nuestra verificación (0-3). AXS Mobile ID y el QR dinámico de DICE son variantes del mismo concepto.

---

## 3. Proveedores para montar tu propia taquilla (white-label / SaaS)

### 3.1 Self-service con precios públicos (verificados el 17-jul-2026)

| Proveedor | Modelo de precios | A quién sirve | Nota |
|---|---|---|---|
| **ThunderTix** ✔️ | GA: **$20/mes + $1/boleto**; asientos numerados: **$25/mes + $1.25/boleto** (0% comisión; mapa custom: $0.55/asiento, mín. $250); White Glove: **$195/mes + $1.95/boleto** con subdominio de marca propia | Teatros y venues pequeños/medianos | El fee es del organizador, trasladable al comprador; procesamiento de tarjeta aparte |
| **Ticketor (plan Reseller)** ✔️ | **$99.95/mes (anual/3 años) o $149.50/mes + $149.50 setup (mensual)** + **2.5% + $0.09–0.19/boleto** | Quien quiera operar una **plataforma white-label donde otros organizadores se registran bajo tu marca y tus precios** — literalmente "tu propio Ticketmaster" | La vía más barata verificada para ser plataforma (no solo venue); add-ons por cliente: dominio $5, anti-fraude $9.95 |
| **TicketSpice** | **$0.99/boleto** (+ procesamiento ~2.9% + $0.30); sin suscripción | Eventos y venues en EE.UU. | Citado consistentemente como el low-cost líder |
| **Ticket Tailor** | **$0.75–0.85/boleto** pay-as-you-go ($0.30–0.60 con prepago); white-label **+$39/mes**; eventos gratis: $0 | Eventos pequeños/medianos globales | Suscripción opcional $29–99/mes |
| **Purplepass** | **2.5% + $0.99/boleto** online (non-profit 2.0%); tarjeta 3.0%; box office 2.5% + $0.25 | Conciertos, festivales, artes escénicas (self-service US) | Sin suscripción ni setup; trasladable al comprador |
| **Tix.com** | Online **$1.50/boleto**; box office **$0.25/boleto**; tarjeta 5% con su merchant account ($0 con la tuya) | Teatros comunitarios, box office chico | "Costo $0" para el venue si se traslada todo |
| **Showpass** | Essential: **1% + $0.59 CAD/boleto**; Professional: **2.5% + $1.69 CAD/boleto** | Venues y eventos (Canadá/US) | |
| **Weeztix** (ex-Eventix, hoy de Weezevent) | Primeros 5,000 boletos gratis, luego **~€0.20/boleto** (Capterra reporta desde €0.83 con fees de pago) | Festivales y clubes (Europa) | Fees de pago aparte, criticados por poco claros |

### 3.2 Enterprise (cotización)

| Proveedor | Modelo | Cifras conocidas | A quién sirve |
|---|---|---|---|
| **Spektrix** | **% de ventas brutas, decreciente, todo incluido** | Tiers públicos (G-Cloud UK): **3.3%** hasta £600k/año → 2.8% a £1M → 2.3% a £2M → **1%** a £25M | Teatros y artes escénicas (el único enterprise con precio transparente) |
| **Tessitura** | Licencia + cuota ligada al revenue de la organización; sin fee por boleto | **~$25k–150k+/año** + implementación $20k–100k + migración $10k–30k (reviews de terceros) | Artes escénicas y museos non-profit |
| **AudienceView** | Suscripción, fee por boleto, o mezcla — cotización | Escenario modelado por el propio vendor: venue de 10k boletos/año a $50 → **~$31k/año todo incluido** (vs $37k–47.7k competidores) | Teatros, universidades, venues profesionales |
| **Secutix** | SaaS por cotización; pagos Interchange++ | Sin precio público | Estadios, festivales, museos europeos (suite S-360) |
| **vivenu** | Cotización; se posiciona con flat-fee predecible | Sin precio público | Ticketing API-first para deportes/festivales |
| **SeatGeek Enterprise (SRO)** | Contratos por venue/equipo | No público | Estadios y equipos (NFL) |

### 3.3 Componentes para un build propio (comprar la pieza, no la plataforma)

| Componente | Proveedor de referencia | Precio |
|---|---|---|
| Mapas de asientos interactivos | **Seats.io** — renderiza estadios de 80,000 asientos, procesa 7M+ reservas/mes (auto-reportado) ✔️ | Por cotización/suscripción según uso |
| Pagos | **Stripe** ✔️ | **2.9% + $0.30**/transacción online (EE.UU.); +1.5% tarjetas internacionales; $15 por chargeback |
| Sala de espera virtual (picos de on-sale) | **Queue-it** (30 mil millones de interacciones/año, 1,000+ clientes) o "Virtual Waiting Room on AWS" | Cotización; alternativa: construirla como SeatGeek (DynamoDB + Lambda + API Gateway) ✔️ |
| Anti-bots | Cloudflare Bot Management, DataDome, HUMAN | ~$200–5,000+/mes según tráfico (estimación) |
| Cumplimiento PCI-DSS | Con Stripe (SAQ-A) casi todo delegado; propio: **$1k–10k/año nivel pequeño; $50k–150k/año nivel 1** (>6M transacciones) | + pentesting $5k–50k/año |

---

## 4. ¿Cuánto cuesta CONSTRUIR la plataforma? (Opción B)

> ⚠️ **Estimaciones propias** construidas sobre insumos con fuente: tarifas por hora por región (Norteamérica $100–250, LATAM $35–70 — Appinventiv), salarios LATAM 2025 (junior $18–28k, mid $35–48k, senior $55–70k/año — Howdy/ParallelStaff) vs EE.UU. (~$160k fully loaded promedio; senior $230–260k primer año), PCI ($1k–150k/año según nivel), Stripe 2.9% + $0.30. Los rangos de Appinventiv para "app tipo Ticketmaster": $40k–100k MVP básico, $100k–200k medio, $200k–400k+ enterprise (estimación de agencia, tomarla como piso).

### Nivel 1 — MVP (venue propio o promotor local)

**Alcance**: venta de admisión general + asientos numerados básicos (Seats.io), checkout con Stripe, boletos QR por email, app de escaneo en puerta, panel de administración de eventos, reportes. Sin apps nativas, sin reventa, sin dynamic pricing.

| Concepto | Equipo LATAM | Equipo EE.UU. |
|---|---|---|
| Equipo (5–6 pers.: 1 TL, 2 backend, 1 frontend, 1 QA, ½ diseño, ½ PM) × 4–6 meses | **$120k–250k** | $350k–600k |
| Nube (AWS/GCP: contenedores + RDS + CDN) | $300–1,500/mes | igual |
| Seats.io + herramientas | $500–2,000/mes | igual |
| PCI (delegado a Stripe, SAQ-A) | ~$0–3k/año | igual |
| **Total año 1** | **~$150k–300k** | ~$400k–700k |

### Nivel 2 — Plataforma media (competidor regional, 100k–1M boletos/año)

**Alcance**: todo lo anterior + apps iOS/Android, mapas de asientos avanzados, sala de espera para on-sales (Queue-it o propia), anti-bots, transferencia y reventa de boletos, multi-organizador (white-label básico), precios por tiers, analítica, soporte 24/7 en eventos.

| Concepto | Equipo LATAM | Equipo EE.UU. |
|---|---|---|
| Equipo (12–18 pers.) × 12–18 meses de construcción | **$900k–2.2M** | $2.5M–5M |
| Nube con picos de on-sale (auto-scaling, colas, réplicas) | $3k–15k/mes | igual |
| Queue-it/waiting room + anti-bots + fraude | $2k–10k/mes | igual |
| PCI DSS (nivel 2–3) + pentesting | $10k–50k/año | igual |
| Operación anual post-lanzamiento (equipo reducido 8–12 + infra) | **~$700k–1.5M/año** | ~$1.8M–3M/año |
| **Total hasta lanzamiento completo** | **~$1.2M–2.8M** | ~$3M–6M |

### Nivel 3 — Escala Ticketmaster

**El punto de referencia real** (verificado, SEC FY2025): 346M boletos fee-bearing/año, GTV de conciertos de $26B, on-sales con millones de usuarios simultáneos, SafeTix/NFC, marketplace secundario integrado, contratos con miles de venues.

Estimación propia (órdenes de magnitud, no cotización):
- **Ingeniería**: 150–400+ ingenieros permanentes → $25M–80M/año en nómina (incluso con mezcla LATAM).
- **Infraestructura**: nube + edge + anti-bots a escala de millones de concurrentes → $6M–25M+/año.
- **Seguridad/cumplimiento**: PCI nivel 1 ($50k–150k/año de auditoría es lo de menos: el costo real es el equipo de seguridad, SIEM $10k–100k, pentesting continuo).
- **Total**: **$50M–150M+ acumulados en 4–6 años** solo en tecnología — sin contar lo decisivo: adquisición de inventario (contratos con venues, adelantos a promotores), que en la industria real es la barrera de entrada, no el software.

**Conclusión del nivel 3**: nadie debería "construir un Ticketmaster" de entrada. El camino racional (validado por el caso SeatGeek ✔️: usaron waiting room de terceros y la reemplazaron por una propia solo cuando la escala y la necesidad de métricas lo justificó) es: **comprar componentes → construir el diferenciador → internalizar piezas solo cuando duelan**.

---

## 5. ¿Cuánto cuesta PAGARLE a una plataforma? (Opción A) y comparación

Supuesto: boleto promedio de $50. Los fees de plataforma casi siempre pueden **trasladarse al comprador** (columna "costo neto organizador ≈ $0"). Procesamiento de pago (~2.9% + $0.30) aparte, también usualmente trasladado.

| Escenario | ThunderTix (asientos num.) | TicketSpice | Ticketor Reseller (white-label) | Spektrix (% ventas) | Build propio (LATAM, amortizado) |
|---|---|---|---|---|---|
| **10k boletos/año** ($500k GMV) | $25×12 + $1.25×10k ≈ **$12.8k/año** | ≈ **$9.9k/año** | $1.2k + 2.5%×$500k + $0.14×10k ≈ **$15.1k/año** | ~3.3% ≈ **$16.5k/año** | $150k–300k año 1 + $50k+/año — **no compite** |
| **100k boletos/año** ($5M GMV) | ≈ **$126k/año** | ≈ **$99k/año** | ≈ **$140k/año** | ~2.3–2.8% ≈ **$115k–140k/año** | $1.2M–2.8M construcción + $0.7M–1.5M/año — **no compite por ahorro** |
| **1M boletos/año** ($50M GMV) | ≈ **$1.25M/año** | ≈ **$0.99M/año** | ≈ **$1.4M/año** | ~1–2% ≈ **$0.5M–1M/año** | ~$1M/año de operación (ya construida) — **empieza a competir** |

**La lectura correcta de esta tabla:**

1. **Por ahorro de costos, el build casi nunca gana**: incluso a 1M boletos/año, un enterprise como Spektrix cuesta parecido a operar tu propia plataforma — sin el riesgo ni los 18–24 meses de construcción.
2. **El build gana por CAPTURA DE INGRESO, no por ahorro**: si operas tu propia plataforma puedes cobrar el service fee al comprador (10–20% del valor del boleto). A 1M boletos/año × $50 × 15% = **$7.5M/año de ingreso por fees** — contra ~$1M/año de costo operativo. Ese es el modelo de negocio de Ticketmaster (su take rate implícito: $3,081M de ingresos sobre GTV fee-bearing, con margen operativo alto), de StubHub (~19% del GMS) y de todos los demás.
3. **El híbrido Ticketor-style existe**: por ~$1.2k–1.8k/año + 2.5% ya puedes tener una plataforma white-label multi-organizador con TU marca cobrando TUS fees — margen menor que un build, pero con inversión ~1000x menor. Es el mejor "paso 0" para validar el negocio antes de construir.

---

## 6. Plan de construcción con tiempos (build propio)

> Duraciones estimadas para un equipo competente; el camino asume "comprar componentes primero" (Stripe, Seats.io, Queue-it, Cloudflare) e internalizar después.

### Fase 0 — Descubrimiento y diseño (4–6 semanas)
Equipo: PM + arquitecto + diseñador (3 pers.).
Entregables: alcance del MVP, arquitectura (reserva de asientos con locks/TTL, idempotencia de pagos, modelo multi-tenant), selección de componentes, diseño UX del checkout.
**Riesgo que se mitiga aquí**: el problema técnico distintivo de la boletería es el **on-sale** — miles de personas comprando el mismo inventario finito en el mismo segundo. Si la arquitectura de reservas no se diseña para eso desde el día 1 (colas, locks distribuidos, sobreventa cero), todo lo demás sobra.

### Fase 1 — MVP (4–6 meses) → **mes 5–7 en producción**
Equipo: 5–6 (1 tech lead, 2 backend, 1 frontend, 1 QA, ½ diseño/PM).
Alcance: eventos GA + asientos numerados (Seats.io), checkout Stripe, boletos QR, app/PWA de escaneo, panel de organizador, reportes, emails transaccionales.
Criterio de salida: vender un evento real de 1,000–3,000 boletos sin sobreventa ni caída.

### Fase 2 — Producto completo (6–9 meses adicionales) → **mes 12–16**
Equipo: crece a 12–18 (se suman mobile ×2–4, DevOps/SRE ×2, backend ×2, data ×1, soporte).
Alcance: apps nativas iOS/Android, sala de espera virtual (Queue-it primero), anti-bots (Cloudflare), transferencia de boletos, reventa entre usuarios, multi-organizador/white-label, precios por tiers/promociones, analítica para organizadores.
Criterio de salida: on-sale de 20k–50k boletos con pico de 5–10k usuarios concurrentes, métricas limpias.

### Fase 3 — Escala y diferenciación (12+ meses, continua) → **mes 24–36**
Equipo: 25–50+.
Alcance: internalizar waiting room si el volumen lo justifica (patrón SeatGeek ✔️), boleto seguro estilo SafeTix (barcode rotativo TOTP + NFC — técnicamente replicable, ver conduition.io), dynamic pricing, marketplace secundario propio (capturar el fee de reventa), APIs públicas para distribuidores, multi-región/multi-moneda.

### Presupuesto total del camino (equipo LATAM, estimación propia)
- Hasta MVP en producción: **$150k–300k** (mes 5–7).
- Hasta producto completo: **$1.2M–2.8M acumulados** (mes 12–16).
- Operación estable posterior: **$0.7M–1.5M/año**.
- Escala Ticketmaster: $50M–150M+ y 4–6 años — solo con inventario/contratos asegurados.

### Riesgos principales
1. **Inventario, no software**: sin contratos con venues/promotores no hay nada que vender. Es la verdadera barrera (Ticketmaster añadió 27M de boletos enterprise netos en 2025 comprando/ganando clientes ✔️).
2. **On-sale catastrófico**: una caída en el minuto 1 de una venta grande destruye la reputación (el costo del downtime supera $300k/hora según encuestas de industria). Mitigación: waiting room + pruebas de carga como criterio de salida de cada fase.
3. **Fraude y chargebacks**: boletería es categoría de alto riesgo; $15 por disputa en Stripe + posibles retenciones. Presupuestar herramientas anti-fraude desde Fase 2.
4. **Regulación en movimiento**: EE.UU. avanza contra junk fees y bots (informe del Senado 2026 sobre Ticketmaster); el all-in pricing ya es lo esperado. Diseñar precios transparentes desde el inicio.
5. **Competir contra gratis**: para el organizador, el SaaS cuesta ~$0 neto (fees trasladados). Tu plataforma propia debe ofrecer algo que el SaaS no da (marca, datos, fee propio, experiencia).

---

## 7. Recomendación

| Si tu objetivo es… | Camino recomendado | Costo año 1 |
|---|---|---|
| Vender boletos de TU venue/eventos | SaaS: TicketSpice / ThunderTix / Ticket Tailor (o Purplepass/Tix) | **$0–15k** (fees trasladables al comprador) |
| Operar una boletería con TU marca donde otros organizadores venden | White-label reseller: Ticketor (o negociar vivenu/AudienceView) | **~$1.5k–30k** |
| Ser una plataforma regional que captura el fee de servicio | Build por fases (roadmap §6), componentes comprados | **$150k–300k** (MVP) → $1.2M–2.8M (completa) |
| "Ser Ticketmaster" | Primero lo anterior + contratos de inventario; el software a esa escala es $50M+ y no es la barrera real | $50M–150M+ / 4–6 años |

**Paso siguiente sugerido**: validar con un piloto — montar la taquilla en un SaaS ($1k), correr 2–3 eventos reales, medir fees capturables y fricción, y con esos datos decidir si el build de Fase 1 ($150k–300k) tiene caso de negocio.

---

## 8. Fuentes principales

**Financieras (primarias, verificadas 3-0):**
- [Live Nation FY2025 results](https://newsroom.livenation.com/news/live-nation-entertainment-full-year-and-fourth-quarter-2025-results/) — Ticketmaster $3,081M / 346M boletos / GTV $26B
- [StubHub FY2025 results](https://investors.stubhub.com/news/news-details/2026/StubHub-Announces-Full-Year-and-Fourth-Quarter-2025-Results/default.aspx) + [SEC 8-K](https://www.sec.gov/Archives/edgar/data/1337634/000119312525280227/d35879dex991.htm) — GMS $9.2B, take rate 19%
- [Vivid Seats 10-K FY2025 (SEC)](https://www.sec.gov/Archives/edgar/data/1856031/000119312526103023/seat-20251231.htm) — GOV $2.7B, Private Label $57M
- [Eventbrite Q3-2025 (investor relations)](https://investor.eventbrite.com/press-releases/press-releases-details/2025/Eventbrite-Reports-Third-Quarter-2025-Financial-Results/default.aspx)

**Precios de proveedores (páginas oficiales, verificadas en vivo 17-jul-2026):**
- [ThunderTix pricing](https://www.thundertix.com/online-ticketing-software-pricing/) · [Ticketor Platform Prices](https://www.ticketor.com/Account/PlatformPrices) · [Stripe pricing](https://stripe.com/pricing) · [Purplepass](https://www.purplepass.com/learn/pricing/) · [Tix.com](https://www.tix.com/ticket-sales-software/pricing.aspx) · [Weeztix](https://weeztix.com/pricing) · [Spektrix](https://www.spektrix.com/en-us/pricing) + [tiers G-Cloud UK](https://assets.applytosupply.digitalmarketplace.service.gov.uk/g-cloud-14/documents/92833/310640378015414-pricing-document-2024-05-02-2130.pdf) · [Eventbrite fees](https://www.eventbrite.com/organizer/compare-packages/) · [Seats.io](https://www.seats.io/features)

**Técnicas y de arquitectura:**
- [SafeTix (Ticketmaster oficial)](https://blog.ticketmaster.com/introducing-safetix-ticketmasters-next-gen-encrypted-tickets/) · [Ingeniería inversa de SafeTix (conduition.io)](https://conduition.io/coding/ticketmaster/) · [Waiting room de SeatGeek en AWS](https://aws.amazon.com/blogs/architecture/build-a-virtual-waiting-room-with-amazon-dynamodb-and-aws-lambda-at-seatgeek/) · [Queue-it en AWS](https://aws.amazon.com/blogs/apn/how-to-manage-peak-traffic-on-aws-using-queue-its-virtual-waiting-room/)

**Costos de desarrollo y salarios:**
- [Appinventiv — costo app tipo Ticketmaster](https://appinventiv.com/blog/cost-to-build-an-app-like-ticketmaster/) · [Howdy — salarios LATAM 2025](https://www.howdy.com/blog/2025-latin-america-software-developer-salaries) · [ParallelStaff — salarios LATAM](https://parallelstaff.com/blog/latam-software-engineer-salaries/) · [Centraleyes — costos PCI DSS](https://www.centraleyes.com/pci-dss-compliance-cost/)

**Plataformas (búsquedas complementarias):**
- TickPick: [BusinessWire $250M](https://www.businesswire.com/news/home/20240822457355/en/TickPick-Announces-$250-Million-Growth-Investment-from-Brighton-Park-Capital) · Gametime: [PR Newswire $30M](https://www.prnewswire.com/news-releases/gametime-leading-platform-for-last-minute-tickets-secures-30-million-in-new-funding-expanding-reach-as-record-sales-continues-301555492.html), [Wikipedia](https://en.wikipedia.org/wiki/Gametime) · AXS: [AEG press](https://aegworldwide.com/press-center/press-releases/aeg-purchases-all-outstanding-shares-axs) · DICE: [Wikipedia](https://en.wikipedia.org/wiki/Dice_(ticketing_company)), [Variety](https://variety.com/2025/music/global/dice-ceo-phil-hutcheon-fighting-dynamic-pricing-ticketing-industry-1236269673/) · Fever: [newsroom oficial](https://newsroom.feverup.com/en-US/250714-fever-secures-100m-strengthening-its-position-as-the-leading-independent-live-entertainment-tech-platform/) · Tixr: [about oficial](https://creators.tixr.com/about) · Ritz Theatre: [Wikipedia](https://en.wikipedia.org/wiki/Ritz_Theatre_&_Performing_Arts_Center), [ritztheatre.com](https://www.ritztheatre.com/)

**Afirmaciones refutadas en verificación (NO usar):** que SafeTix impide la redistribución por binding al teléfono (0-3); los porcentajes de fees de Ticket Flipping (StubHub 27.76%/Vivid 31.29%/SeatGeek 37.66%; 1-2); que StubHub/SeatGeek/Vivid son puros marketplaces de reventa (0-3 — SeatGeek tiene negocio primario amplio).

**Límites del análisis:** los fees exactos al comprador de cada marketplace varían por evento y no hay fuente confiable transversal (la única encontrada fue refutada); los precios enterprise (Tessitura, Secutix, vivenu, AudienceView, Seats.io) requieren cotización directa; las cifras de costos de build/nube de §4 son estimaciones propias sobre insumos citados, no cotizaciones.
