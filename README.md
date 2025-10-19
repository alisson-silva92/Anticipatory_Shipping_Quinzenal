# 🧠 Anticipatory Shipping Quinzenal

> “¿Cómo pueden las tiendas —como Amazon— saber lo que vas a comprar incluso antes de que entres en la web a buscarlo?”

Empresas como **Amazon**, **El Corte Inglés** y **PcComponentes** ya lo hacen cada día.  
Son capaces de **enviar productos a los centros de distribución adecuados antes de que la compra ocurra**, reduciendo el tiempo de entrega de días a horas.

A este proceso se le llama **Anticipatory Shipping** — o **envío anticipado inteligente**.  
La lógica es simple:  
si puedes prever la demanda con precisión, puedes mover el stock antes de la compra y tener el producto lo más cerca posible del cliente.

---

## 📦 Proyecto: Anticipatory Shipping Quinzenal

Este proyecto simula el comportamiento del **Anticipatory Shipping** utilizando **Python + Prophet (Meta)**.  
El modelo predice, cada 15 días, qué productos deberían ser enviados anticipadamente a cada región de España 🇪🇸.

---

## ⚙️ ¿Cómo funciona?

### 1️⃣ Datos de entrada
Un dataset sintético con las columnas:
- `fecha_pedido`: fecha del pedido  
- `comunidad_autonoma`: región española  
- `id_producto`: identificador del producto  
- `cantidad`: unidades vendidas  
- `precio`: precio medio  

### 2️⃣ Agregación temporal
Las ventas se agrupan de forma **quincenal (cada 15 días)** por producto y región.

### 3️⃣ Modelado con Prophet
Para cada combinación de producto y región:
- Se densifica la serie temporal (rellenando quinzenas sin ventas).  
- Se entrena un modelo **Prophet** con 90% de intervalo de confianza.  
- Se generan previsiones para los siguientes **2 periodos quinzenales (~1 mes)**.

### 4️⃣ Decisión de envío
El modelo evalúa la cantidad sugerida (`qtd_sugerida`) y aplica reglas de negocio:

| Condición | Acción |
|------------|---------|
| Demanda prevista alta (≥ percentil p70) y confianza OK | `ENVIAR_ANTES` |
| Caso contrario | `AGUARDAR` |

También se pueden activar criterios opcionales de **ROI** (beneficio estimado vs. coste logístico).

---

## 📊 Resultados

El resultado es un archivo CSV (`recomendaciones_pre_envio.csv`) con las siguientes columnas:

| Columna | Descripción |
|----------|--------------|
| `comunidad_autonoma` | Región de destino |
| `id_producto` | SKU / producto |
| `ds` | Fecha del periodo (quinzena) |
| `yhat` | Predicción mediana |
| `yhat_lower`, `yhat_upper` | Intervalo de confianza |
| `qtd_sugerida` | Cantidad sugerida para envío |
| `conf_ok` | Si la previsión es fiable |
| `decisao_pre_envio` | `ENVIAR_ANTES` o `AGUARDAR` |

---

## 🧩 Ejemplo visual

Gráfico de las 12 combinaciones región × producto con mayor recomendación de envío anticipado:

![Top 12 envíos anticipados](plot_3d_top20_pre_envios.png)

Distribución general de decisiones:

![Distribución de decisiones](plot_share_decisoes.png)

---

## 💡 Insights

- **p70** (percentil 70) logra un equilibrio entre agilidad logística y riesgo de sobrestock.  
- El modelo permite identificar **qué regiones muestran señales de demanda temprana**.  
- Con pequeñas modificaciones, podría escalarse a granularidad **semanal o diaria**.  

---

## 🧠 Stack tecnológico

- **Python 3.11+**
- **Prophet (Meta)**
- **Pandas / NumPy**
- **Matplotlib / tqdm**

---

## ▶️ Ejecución

1. Clona el repositorio  
   ```bash
   git clone https://github.com/alisson-silva92/Anticipatory_Shipping_Quinzenal.git
   cd Anticipatory_Shipping_Quinzenal
