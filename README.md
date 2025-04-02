# Predicción de Demanda Semanal de Órdenes

Este proyecto aborda el pronóstico de la demanda semanal de órdenes para una compañía manufacturera global, utilizando datos reales anonimizados. El objetivo es construir un modelo que anticipe la demanda con al menos una semana de anticipación, ayudando en la planificación logística y de inventario.

---

## 📊 Contexto del Dataset

- **Origen:** Compañía manufacturera con presencia global
- **Contenido:**
  - `Product_Code`: identificador del producto (codificado)
  - `Warehouse`: centro de distribución (codificado)
  - `Product_Category`: categoría del producto (codificada)
  - `Order_Demand`: demanda (objetivo a predecir)
  - **Rango temporal:** varios años de historia, a nivel transacción

---

## 🔄 Transformación y Preprocesamiento

1. **Conversión de fechas:** se asegura que el índice sea `datetime`.
2. **Resampleo:** los datos son agregados semanalmente (‘W-MON’) utilizando el promedio.
3. **Transformación logarítmica:** se aplica `np.log1p` para estabilizar la varianza.
4. **Limpieza:**
   - Se eliminan outliers extremos por percentil.
   - Se interpolan valores nulos linealmente.
5. **Variable objetivo final:** `Order_Demand_log` semanal, transformada con logaritmo.

---

## 🔹 Análisis Exploratorio

- Se identificaron patrones estacionales claros de 52 semanas (anuales).
- Se detectaron semanas con disminuciones sistemáticas de demanda.

---


## 📊 Evaluación del Modelo

- El modelo fue evaluado sobre un conjunto de prueba (15-20% final de la serie).
- Se transformaron las predicciones de vuelta a la escala original usando `np.expm1`.
- Métricas:
  - **RMSE:** 28.70 unidades
  - **Media real:** 242.24 unidades
  - **Error relativo (RMSE/Media):** 11.8%

> El error promedio de predicción es de ±28.7 órdenes por semana, lo que representa un 11.8% del promedio real, indicando buen ajuste.

---

## 🔍 Visualizaciones

- Comparación visual entre predicciones y valores reales semanales.
- Gráficos de residuos: QQ plot, ACF, y residuos en el tiempo.

---

## 🎓 Conclusiones

- Se logró capturar el comportamiento estacional y las caídas sistemáticas.
- El modelo se comporta con residuos similares a ruido blanco.
- Es una solución viable y explicable para pronóstico de series temporales en producción.

---

## 🚀 Posibles Extensiones

- Incorporar más variables exógenas como `Warehouse`, `Category`, feriados o eventos.
- Validación cruzada con backtesting en ventanas.
- Probar modelos alternativos: Prophet, XGBoost, modelos recurrentes (RNN/LSTM).

---

## 📚 Librerías usadas

- `pandas`, `numpy`, `matplotlib`, `statsmodels`, `sklearn`

---

## 😎 Autor

Kevin G. — [LinkedIn / GitHub / Portafolio]

> Proyecto parte de mi portafolio personal de ciencia de datos.
