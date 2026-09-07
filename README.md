# 📊 E-Commerce Executive Performance Dashboard (Olist Brazil)

Un panel ejecutivo interactivo diseñado en Power BI para analizar el rendimiento comercial, la logística de envíos y la satisfacción del cliente en el conjunto de datos de e-commerce de **Olist Brasil**.

![Dashboard Overview](assets/dashboard_overview.png)

---

## 🎯 Objetivo del Proyecto

Transformar datos transaccionales crudos en **insights accionables a nivel directivo**, garantizando una alta integridad de datos, un modelo estelar optimizado y un diseño visual con estándares profesionales de UX/UI.

---

## 📈 Principales KPIs y Métricas Negociales

* **Ingresos Totales:** ~$13.59M
* **Total Pedidos:** ~99K órdenes procesadas
* **Ticket Promedio:** $137.75
* **Puntuación de Satisfacción (CSAT):** 4.09 / 5.00 estrellas

---

## 💡 Hallazgos Clave de Negocio (Executive Insights)

1. **Impacto Logístico en la Satisfacción:**
   Existe una clara correlación inversa entre los costos de envío y las puntuaciones de los clientes. Los pedidos con calificación de **1 estrella** registraron un flete promedio significativamente más alto (~$27) en comparación con las órdenes de **5 estrellas** (~$21).
2. **Distribución Geográfica:**
   La densidad de ventas está altamente concentrada en el Sudeste de Brasil, liderada por estados como **São Paulo (SP), Río de Janeiro (RJ) y Minas Gerais (MG)**.
3. **Categorías Lideres:**
   Categorías como *Cool Stuff*, *Pet Shop* y *Consoles/Games* dominan la generación de ingresos con un ticket promedio elevado.

---

## 🛠️ Desafíos Técnicos y Soluciones de Modelado

* **Normalización de Datos Moneda:** Se aplicó una normalización por factor 100 en `price` y `freight_value` para corregir la escala original del dataset.
* **Modelo Dimensional (Estrella):** Se implementó una dirección de **filtro cruzado bidireccional (`Ambos`)** entre `Fact_orders` y `Fact_order_reviews` para permitir la correcta propagación del contexto de filtro por `review_score`.
* **Manejo de Incompletitud Temporal:** Se configuraron reglas de filtrado en la dimensión temporal (`Dim_Calendar`) cortando la serie en **Agosto de 2018** para mitigar sesgos por datos residuales de septiembre.
* **Geolocalización Directa:** Se implementó lógica DAX para mapear estados (` customer_state & ", Brasil"`) evitando inconsistencias de Bing Maps a nivel global.

---

## 📐 Medidas DAX Clave

```dax
// Ingresos Totales
Ingresos Totales = SUM(Fact_order_items[price])

// Flete Promedio por Pedido
Flete Promedio = DIVIDE(SUM(Fact_order_items[freight_value]), [Total Pedidos], 0)

// Puntuación Promedio de Reseñas
Puntuación Promedio = AVERAGE(Fact_order_reviews[review_score])
```
---
git clone [https://github.com/tu-usuario/olist-ecommerce-powerbi.git](https://github.com/tu-usuario/olist-ecommerce-powerbi.git)
