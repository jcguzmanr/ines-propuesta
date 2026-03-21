# Pasarelas de Pago en Perú — Evaluación para INES

**Contexto:** Eventualmente el sitio de INES necesitará una pasarela de pago para venta directa. Este documento evalúa las opciones disponibles en Perú.

**Nota:** Todas las comisiones están sujetas a IGV (18%), lo que eleva la tasa efectiva. Ej: 3.49% + IGV ≈ 4.12% efectivo. Verificar precios actuales en cada proveedor.

---

## Comparativo rápido

| | Mercado Pago | Culqi | Izipay | Niubiz | PayU |
|---|---|---|---|---|---|
| **Comisión** | ~3.99% + IGV | 3.49% + S/0.30 + IGV | ~3.29-3.69% + IGV | ~3.29-3.99% + IGV | ~3.49-3.99% + IGV |
| **Costo mensual** | Gratis | Gratis | S/ 0-49.90 | S/ 0-50 | Gratis |
| **Setup** | Gratis | Gratis | Gratis-variable | S/ 0-200 | Gratis |
| **Yape** | Si | Si | Si | Si | No |
| **Plin** | No | No | Si | Expandiendo | No |
| **Liquidación** | 7-14 días | 3 días | 48 horas | 48 horas | 7-14 días |
| **Facilidad integración** | Fácil | Fácil (mejor API) | Media | Media-Difícil | Media |
| **RUC mínimo** | RUC 10 | RUC 10 | RUC 10/20 | RUC 10/20 | RUC 20 preferido |

---

## Detalle por proveedor

### 1. Mercado Pago
- **Web:** mercadopago.com.pe
- **Comisión:** ~3.99% + IGV (~4.71% efectivo)
- **Pro:** Setup inmediato, sin costos fijos, protección al vendedor, acepta Yape
- **Contra:** Comisión alta, liquidación lenta (7-14 días para cuentas nuevas)
- **Ideal para:** Arrancar rápido con mínima inversión
- **Plugins:** WooCommerce, Shopify, PrestaShop. Sin plugin nativo para Webflow
- **Requisitos:** RUC (acepta persona natural), DNI, cuenta bancaria peruana

### 2. Culqi
- **Web:** culqi.com
- **Comisión:** 3.49% + S/0.30 + IGV por transacción
- **Pro:** Mejor API y documentación de Perú, dashboard moderno, Yape integrado, comisión más baja en Yape (~1.99% + IGV)
- **Contra:** El fee fijo de S/0.30 pesa en transacciones pequeñas, soporte puede ser lento
- **Ideal para:** Negocios con desarrollador o tech-savvy
- **Plugins:** WooCommerce, Shopify (app disponible). API REST con SDKs en PHP, Node.js, Python, Ruby, Java, Go
- **Requisitos:** RUC, DNI, cuenta bancaria. Onboarding 2-5 días hábiles
- **Nota:** Pertenece al grupo Credicorp/BCP

### 3. Izipay
- **Web:** izipay.pe
- **Comisión:** ~3.29-3.69% + IGV
- **Pro:** Yape Y Plin (único con ambos), liquidación rápida (48h), respaldo de BCP + Scotiabank
- **Contra:** Menos developer-friendly, documentación mejorable
- **Ideal para:** Negocio que quiere cubrir el mayor % de billeteras digitales peruanas
- **Plugins:** WooCommerce, PrestaShop. API REST disponible
- **Requisitos:** RUC, documentación estándar. Onboarding 5-10 días hábiles

### 4. Niubiz (ex VisaNet)
- **Web:** niubiz.com.pe
- **Comisión:** ~3.29-3.99% + IGV (negociable por volumen)
- **Pro:** Marca más confiable en Perú, liquidación 48h, Yape integrado, PCI DSS Level 1
- **Contra:** Barrera de entrada alta, burocrático, integración compleja, precios no transparentes
- **Ideal para:** Negocio establecido con volumen consistente
- **Plugins:** WooCommerce, PrestaShop. API REST mejorada pero históricamente difícil
- **Requisitos:** RUC, documentos de empresa, cuenta bancaria. Onboarding 5-15 días hábiles

### 5. PayU Latam
- **Web:** payu.com.pe
- **Comisión:** ~3.49-3.99% + IGV
- **Pro:** Cobertura multi-país (LatAm), buenas herramientas anti-fraude
- **Contra:** Sin Yape ni Plin, liquidación lenta, menos enfocado en Perú
- **Ideal para:** Solo si se planea vender a otros países
- **Requisitos:** Prefiere RUC 20

### 6. Stripe
- **Estado:** No disponible directamente en Perú (no acepta cuentas con banco peruano)
- **Workaround:** Incorporar empresa en USA vía Stripe Atlas ($500 USD) y operar desde allá
- **Nota:** Monitorear — puede expandirse a Perú eventualmente
- **No recomendado** para negocio puramente local

---

## Yape y Plin — Lo que importa

### Yape (BCP)
- +15 millones de usuarios en Perú
- Billetera digital dominante
- Soportado por: Mercado Pago, Culqi, Izipay, Niubiz
- Comisiones generalmente más bajas que tarjetas

### Plin (BBVA, Interbank, Scotiabank)
- Base de usuarios significativa y creciendo
- **Solo Izipay** lo integra de forma madura
- Niubiz expandiendo soporte
- Mercado Pago y Culqi NO lo soportan aún

---

## Consideración Webflow / Framer / Vercel

**Ninguna pasarela peruana tiene plugin nativo para Webflow.** Las opciones son:

1. **Webflow + Checkout personalizado vía API** — usar Culqi o Mercado Pago API con serverless functions
2. **Snipcart o Foxy.io** — carrito de terceros que se conecta a pasarela peruana
3. **WordPress + WooCommerce** — todas las pasarelas tienen plugin, pero cambia la plataforma
4. **Custom (Next.js/Vercel)** — máxima flexibilidad, integración directa con cualquier API

---

## Recomendación para INES

### Fase 1 — Ahora (sin e-commerce)
- No se necesita pasarela. CTA a Instagram/WhatsApp.

### Fase 2 — Primer e-commerce
- **Culqi** como primera opción: mejor API, fácil de integrar, Yape incluido, sin costos fijos
- **Mercado Pago** como alternativa si no hay desarrollador disponible (más fácil pero más caro)

### Fase 3 — Escala
- Migrar a **Izipay** o **Niubiz** por mejores tasas negociadas y liquidación rápida
- Agregar Plin vía Izipay

### Presupuesto estimado de integración
| Concepto | Estimado |
|---|---|
| Integración de pasarela (desarrollo) | S/ 1,500 - 3,000 |
| Certificado SSL | Incluido (Vercel/Webflow) |
| Dominio (anual) | ~$15 USD |
| Comisión por venta | 3.5-4.5% + IGV |
| Costo mensual pasarela | S/ 0 (Culqi/MercadoPago) |

---

## Contactos y links directos

| Proveedor | Web | Registro |
|---|---|---|
| Mercado Pago | mercadopago.com.pe | Autoservicio online |
| Culqi | culqi.com | Autoservicio online |
| Izipay | izipay.pe | Formulario de contacto |
| Niubiz | niubiz.com.pe | Contactar equipo comercial |
| PayU | payu.com.pe | Formulario de contacto |

---

*Documento interno de Itera. Verificar precios actualizados antes de presentar al cliente.*
