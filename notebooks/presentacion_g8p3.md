
# 🤖 Proyecto de Aprendizaje Supervisado para Clasificación

## 🎓 Maestría en Ciencia de Datos e Inteligencia Artificial  
**Módulo:** Machine Learning and Deep Learning  
**Docente:** M.Sc. Renzo Claure Aracena  
**Grupo 5:**
- Patricia Aguilar Cabrera  
- David Aliaga Nina  
- Harold Aponte Zuñiga  
- Rubén Baltazar Balderrama  
- Jhonny García Zelaya  
---

## 1. 🧩 Definición del Problema

El presente proyecto tiene como finalidad construir un modelo de clasificación binaria utilizando técnicas de aprendizaje supervisado.  
La variable objetivo es `OBJ`, con valores `'SI'` y `'NO'`. El dataset incluye 30 variables independientes, disponibles en formato absoluto (`V1` a `V31`) y relativo (`V1_P` a `V31_P`).

> ⚠️ Se decide trabajar solo con las **variables absolutas**, debido a la **baja varianza** observada en las variables relativas.

---

## 2. 🧾 Descripción del Dataset

📂 **Fuente de datos:** Archivo `.csv` delimitado por `|`  
🔢 **Total de registros:** 3,152 observaciones  
📌 **Características:**

| Tipo de variable        | Descripción                                 |
|-------------------------|---------------------------------------------|
| `OBJ`                   | Variable objetivo binaria (`SI` / `NO`)     |
| `V1` a `V31`            | Variables absolutas                         |
| `V1_P` a `V31_P`        | Variables relativas (descartadas)           |

---

## 3. 🔧 Preprocesamiento de Datos

✔️ Renombrado de columna duplicada `V31_P` → `V31`  
✔️ Selección de columnas: `V1` a `V31` + `OBJ`  
✔️ Conversión de `OBJ`:  
- `SI` → 1  
- `NO` → 0  
✔️ Validación de datos nulos (no se encontraron)  
✔️ Estandarización de variables mediante `StandardScaler`

---

## 4. 🧪 Selección de Variables Relevantes

Se aplicó la prueba estadística **Chi-cuadrado** para determinar la relación entre cada variable independiente (`V1` a `V31`) y la variable objetivo (`OBJ`). Este test evalúa la independencia entre las variables categóricas y permite filtrar aquellas que presentan una relación estadísticamente significativa.

### 🔹 Procedimiento:

1. Para cada variable `Vi`, se generó una tabla de contingencia con la variable `OBJ`.
2. Se aplicó `chi2_contingency` de `scipy.stats` para obtener el valor p.
3. Se seleccionaron aquellas variables con **valor p < 0.05**, lo que indica dependencia estadística con la variable objetivo.

📌 **Variables seleccionadas:**  
`V3, V4, V5, V7, V9, V10, V12, V14, V15, V17, V19, V20, V21, V22, V24, V26, V27, V29, V30, V31`

---

## 5. ⚙️ Entrenamiento de Modelos de Clasificación

Utilizando las variables seleccionadas por Chi-cuadrado, se entrenaron múltiples algoritmos de clasificación supervisada.  
Los datos fueron divididos en conjuntos de entrenamiento y prueba (80/20), y las variables fueron previamente estandarizadas con `StandardScaler`.

### 🔸 Modelos aplicados:

- Regresión Logística
- K-Nearest Neighbors (KNN)
- Árbol de Decisión
- Random Forest
- XGBoost
- Support Vector Machine (SVM)

---

## 6. 🔁 Validación Cruzada y Ajuste de Hiperparámetros

Se utilizó `GridSearchCV` con validación cruzada de 5 pliegues para optimizar los hiperparámetros de los modelos con mejor rendimiento.

### 🔹 Random Forest
- `n_estimators`: [100, 200, 300]
- `max_depth`: [None, 10, 20]

### 🔹 SVM
- `C`: [0.1, 1, 10]
- `kernel`: ['linear', 'rbf']

---

## 7. 📈 Evaluación de Modelos

### 🔸 Métricas utilizadas:
- Accuracy
- Precision
- Recall
- F1-Score
- ROC-AUC

📊 **Resultado destacado:**  
El modelo **Random Forest** presentó el mejor rendimiento global, alcanzando un **F1-Score de 0.89**, además de valores superiores de precisión y recall frente a los demás modelos.

---

## 8. 🥇 Modelo Seleccionado

### ✔️ Modelo Final: `RandomForestClassifier`

🔧 **Parámetros óptimos encontrados:**
- `n_estimators = 200`
- `max_depth = 20`

📌 **Justificación técnica:**
- Mejor equilibrio entre precisión y recall (F1-score).
- Alta capacidad de generalización.
- Robustez ante variables irrelevantes y colinealidad.
- Bajo riesgo de sobreajuste.

---

## 9. 📌 Conclusiones

- La prueba de **Chi-cuadrado** fue efectiva para seleccionar un subconjunto relevante de variables.
- La combinación de **preprocesamiento adecuado + selección de variables + validación cruzada** condujo a resultados óptimos.
- **Random Forest** fue el modelo que mejor se adaptó al problema de clasificación binaria, combinando interpretabilidad, precisión y estabilidad.

---
