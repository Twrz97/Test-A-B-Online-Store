# 🧪 A/B Test: Sistema de Recomendaciones para Tienda Online

Simulación de una prueba A/B para evaluar el impacto de un nuevo sistema de recomendaciones sobre el embudo de conversión en una tienda online.  
Incluye análisis exploratorio, diseño experimental, pruebas estadísticas y conclusiones accionables.

---

## 🏢 Contexto Empresarial

Evaluar si el nuevo sistema de recomendaciones (grupo B) mejora significativamente el rendimiento del embudo de conversión en comparación con el sistema actual (grupo A).

El embudo consta de tres etapas clave:

1. `product_page` → vista de página de producto  
2. `product_cart` → agregar producto al carrito  
3. `purchase` → compra realizada  

Meta esperada: **+10%** de mejora en cada etapa para el grupo B.

---

## 🧠 Resumen conceptual del experimento

- **Nombre de la prueba**: `recommender_system_test`  
- **Objetivo**: Evaluar si un nuevo sistema de recomendaciones mejora el rendimiento del embudo de conversión en una tienda online.

---

## 🧪 Diseño experimental

| Elemento                | Detalle                                                                         |
|-------------------------|----------------------------------------------------------------------------------|
| Grupos                  | A (control) vs B (nuevo sistema de recomendaciones)                             |
| Inicio de prueba        | 2020-12-07                                                                       |
| Cierre de inscripción   | 2020-12-21 (usuarios nuevos hasta esa fecha)                                    |
| Fin de la prueba        | 2021-01-01                                                                       |
| Audiencia               | 15% de los nuevos usuarios de la región de la Unión Europea                     |
| Duración de seguimiento | 14 días desde la inscripción de cada usuario                                    |
| Eventos clave           | `product_page`, `product_cart`, `purchase`                                      |
| Meta esperada           | +10% de mejora en cada etapa del embudo para el grupo B                         |
| Participantes esperados | ~6,000 usuarios (probablemente ~3,000 por grupo si se asignaron equitativamente)|

---

## 📂 Estructura del proyecto

- `ab_test_notebook.ipynb`: Notebook principal con análisis, visualizaciones y conclusiones.
- `data/`: Archivos Excel con datos simulados para los grupos A y B.
- `images/`: Gráficos generados durante el análisis.
- `results/`: Resultados procesados y exportados.
- `requirements.txt`: Librerías necesarias para ejecutar el notebook.

---

## 🛠️ Herramientas y tecnologías

- Python (`pandas`, `numpy`, `scipy`, `matplotlib`, `seaborn`)
- Jupyter Notebook
- Prueba z para proporciones
- Visualización de embudos y comportamiento temporal
- Limpieza y validación de datos con Excel

---

## 🚀 Cómo ejecutar el proyecto

1. Clona este repositorio  
2. Instala las dependencias:

   ```bash
   pip install -r requirements.txt
   ```

3. Abre el notebook `ab_test_notebook.ipynb` en Jupyter  
4. Ejecuta las celdas en orden  

> Los datos utilizados son ficticios y están incluidos en la carpeta `data/`

---

# 🧾 Conclusiones del estudio A/B

## 🎯 Objetivos del estudio

Evaluar si el nuevo sistema de recomendación mejora la conversión de usuarios en cada etapa del embudo:  
`product_page → product_cart → purchase`  
La hipótesis plantea que el grupo B debería mostrar al menos un **10% de mejora** en cada transición respecto al grupo A.

---

## 🔍 Exploración de los datos

- **¿Es necesario convertir los tipos?**  
  Sí. Se tipificaron correctamente las columnas `first_date` y `event_dt` como `datetime`, y se estandarizaron los valores de texto (`str.lower().str.strip()`).

- **¿Hay valores ausentes o duplicados?**  
  No se detectaron valores nulos ni duplicados en los datasets filtrados. Se confirmó unicidad de `user_id` en `participants`, lo que garantiza que cada usuario pertenece a un solo grupo.  
  En `events`, se eliminaron columnas irrelevantes (`details`) y se filtraron eventos fuera del rango de seguimiento.  
  En `new_users`, también se excluyó la columna `device` por no aportar valor al análisis de conversión.  
  Además, el archivo `ab_project_marketing_events_us.csv` fue descartado por no contener información relevante para el propósito del experimento.

---

## 📊 Análisis exploratorio de datos

- El grupo B mostró una ligera mejora en la conversión de `product_page → product_cart` (49.49% vs 46.41%), pero no en `product_cart → purchase` (102.05% vs 106.52%).  
  Ninguna mejora alcanzó el 10% esperado.

- El grupo A representa el 74.7% de los participantes, mientras que el grupo B solo el 25.3%. Este desbalance limita la potencia estadística del análisis.

- Se validó que no hay duplicados en `user_id`, lo que garantiza que cada usuario pertenece exclusivamente a un grupo.

- El grupo A muestra un pico de actividad alrededor del 20 de diciembre, mientras que el grupo B mantiene una participación más estable.  
  No se detectaron anomalías graves ni días sin actividad.

- El embudo no es estrictamente secuencial: algunos usuarios compran directamente desde la página del producto, sin pasar por el carrito.  
  Esto puede explicar por qué `purchase > product_cart` en algunos casos.

---

## 🧪 Evaluación de los resultados de la prueba A/B

- Las tasas de conversión entre etapas fueron similares entre grupos. Aunque el grupo B mostró una mejora marginal en la primera transición, no se observó ventaja en la segunda.  
  Ninguna mejora alcanzó el 10% esperado.

- Se aplicaron pruebas z en ambas transiciones:  
  - `product_page → product_cart`: p = 0.2277  
  - `product_cart → purchase`: p = 0.4433  

  En ambos casos, **no se rechazó la hipótesis nula**, lo que indica que las diferencias no son estadísticamente significativas.

---

## ✅ Conclusión final

No se encontró evidencia estadística suficiente para afirmar que el nuevo sistema de recomendación mejora la conversión en al menos un 10% en ninguna etapa del embudo.  
Se recomienda documentar las limitaciones del experimento (desbalance de grupos, embudo no lineal y exclusión de variables irrelevantes) y considerar rediseñar la prueba si se desea validar mejoras con mayor sensibilidad.
