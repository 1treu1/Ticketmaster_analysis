# Costo anual en fees por plataforma — escenario del venue

**Fecha:** 21 de julio de 2026
**Base:** fees documentados en [informes/analisis-mercado-boleteria.md](analisis-mercado-boleteria.md)

## Supuestos del escenario

| Variable | Valor |
|---|---|
| Precio promedio del boleto | **$90 – $100 USD** (uso $95 como punto medio) |
| Aforo del recinto | 2.800 asientos |
| Asistentes promedio por evento | **2.500** (no siempre hay sold out) |
| Eventos al año | **70** |

## Cálculo base (referencia al 15%)

```
Ingreso por evento   = $95 × 2.500 asistentes        = $237.500
Fees por evento (15%)= $237.500 × 15%                 = $35.625
Fees al año          = $35.625 × 70 eventos           = $2.493.750
```

**Volumen anual derivado:**
- Boletos vendidos/año: 2.500 × 70 = **175.000 boletos**
- GMV (venta bruta)/año: $237.500 × 70 = **$16.625.000**

**Rango según precio del boleto (fee al 15%):**

| Precio boleto | Ingreso/evento | GMV/año | Fees/año @ 15% |
|---|---|---|---|
| $90 | $225.000 | $15.750.000 | **$2.362.500** |
| $95 | $237.500 | $16.625.000 | **$2.493.750** |
| $100 | $250.000 | $17.500.000 | **$2.625.000** |

---

## Fees al año en cada plataforma (a 175.000 boletos / $16,6M GMV)

> ⚠️ Distinción clave: no todas cobran igual **ni a la misma persona**.
> - **Grupo A** cobra un *take rate* alto **al comprador** (10–25%) → el fan lo paga, tu costo neto tiende a $0, pero es el ingreso que dejas de capturar.
> - **Grupo B** (SaaS/white-label) cobra una tarifa baja **al organizador**, trasladable al comprador → el "gasto" real es mucho menor que el 15%.

### Grupo A — plataformas que cobran al comprador (modelo Ticketmaster)

| Plataforma | Fee típico | Fee estimado/año | Quién lo paga |
|---|---|---|---|
| **Ticketmaster (TM1)** | 15–25% del valor | **$2,49M – $4,16M** | Comprador |
| **AXS** | All-in al fan (no publica tarifa) | ~similar a TM | Comprador |
| **DICE** | ~7–10% al organizador | **$1,16M – $1,66M** | Organizador (trasladable) |
| **Eventbrite** | 3,7% + $1,79/boleto + 2,9% proc. | **~$1,41M** (≈8,5% efectivo) | Organizador (trasladable) |

*El $2,49M del cálculo base es exactamente el escenario Ticketmaster al 15%.*

### Grupo B — SaaS / white-label (tarifa baja al organizador)

| Plataforma | Tarifa | Fee de plataforma/año | Nota |
|---|---|---|---|
| **TicketSpice** | $0,99/boleto | **~$173k** | + procesamiento (~2,9%) aparte |
| **ThunderTix** (asientos numerados) | $25/mes + $1,25/boleto | **~$219k** | 0% comisión; marca propia (White Glove): ~$344k |
| **Spektrix** | % decreciente (all-in) | **~$250k – $330k** (~1,5–2%) | Incluye procesamiento |
| **Ticketor (Reseller)** | $1,2k/año + 2,5% + $0,14/boleto | **~$441k** | Ya es plataforma white-label multi-organizador con tu marca |

*Procesamiento de tarjeta (~2,9% + $0,30 ≈ $535k/año en Stripe) aplica encima en el Grupo B y también suele trasladarse al comprador.*

---

## Lectura

1. **El "15% = $2,49M/año" es el modelo Ticketmaster** — pero ese dinero lo paga el fan, no el venue. Para el organizador, ese número es el **ingreso que Ticketmaster captura y tú no**.
2. **En un SaaS el gasto real ronda $173k–441k/año** (1–2,7% efectivo), y es trasladable al comprador → costo neto para el venue ≈ $0.
3. **Por eso construir/operar plataforma propia se justifica por CAPTURA de ingreso, no por ahorro**: a este volumen, cobrar tú el 15% = **~$2,49M/año de ingreso** contra un costo operativo mucho menor. Ese es el negocio.
