``markdown
# Proyecto de Machine Learning: Predicción de Enfermedades Cardíacas

Este repositorio contiene el desarrollo de un modelo de aprendizaje automático para la detección temprana y clasificación de riesgos asociados a enfermedades cardiovasculares utilizando el reconocido dataset de la **UCI (University of California, Irvine)**.

---

## 📋 Estructura y Descripción del Proyecto

El objetivo principal es predecir la presencia o ausencia de afecciones cardíacas a partir de características clínicas y demográficas de los pacientes.

### Fases del Proyecto:
1. **Análisis Exploratorio de Datos (EDA):** Visualización de distribuciones de variables clínicas y análisis de la variable objetivo (`num` y su transformación binaria `enfermo`).
2. **Limpieza y Preparación de Datos:** Identificación de valores duplicados e imputación de valores faltantes (nulos).
3. **Ingeniería de Características:** Creación de Pipelines robustos para automatizar el preprocesamiento de variables numéricas y categóricas.
4. **Modelado Predictivo:** *(Fase Siguiente)* Entrenamiento y evaluación de algoritmos de clasificación.

---

## 🛠️ Tecnologías y Librerías Utilizadas

El proyecto se ha desarrollado enteramente en **Python** utilizando las siguientes librerías esenciales:

*   **Manipulación de Datos:**
    *   `pandas`: Carga de datos, análisis estructural (`info`, `describe`) y manipulación de DataFrames.
    *   `numpy`: Operaciones matriciales y manejo de arreglos numéricos.
*   **Visualización de Datos:**
    *   `matplotlib.pyplot`: Creación de figuras y gráficos personalizados.
    *   `seaborn`: Visualización estadística avanzada (gráficos de barras, recuentos e histogramas estéticos).
*   **Machine Learning (Scikit-Learn):**
    *   `Pipeline`: Para encadenar de forma ordenada los pasos de transformación de datos.
    *   `ColumnTransformer`: Para aplicar preprocesamientos específicos de forma independiente a variables categóricas y numéricas.
    *   `SimpleImputer`: Gestión e imputación de valores faltantes utilizando estrategias de media y moda (valor más frecuente).
    *   `StandardScaler`: Normalización y escalado de las variables numéricas.
    *   `OneHotEncoder`: Codificación de variables cualitativas a variables binarias (Dummies).

---

## 🔄 Últimas Actualizaciones del Notebook

*   **Análisis de Nulos:** Se identificaron y cuantificaron los valores faltantes por columna, destacando una alta ausencia de datos en variables críticas como `ca`, `thal` y `slope`.
*   **Pipeline de Preprocesamiento Automatizado:** Se implementó un flujo de preparación de datos que:
    *   Imputa las variables numéricas con la **media** y las escala (`StandardScaler`).
    *   Imputa las variables categóricas con la **moda (most frequent)** y las codifica (`OneHotEncoder`).
*   **Corrección de Variables:** Se subsanó la discrepancia del nombre de la columna de presión arterial en reposo (`trestbs` corregida a `trestbps`).
*   **One-Hot Encoding Manual:** Se realizó una demostración práctica de codificación dummy sobre la variable de dolor de pecho (`cp`) usando `pd.get_dummies()`.

---

## 📌 Conclusiones Iniciales

1.  **Desequilibrio de Clases:** La variable objetivo original `num` posee múltiples grados de severidad, pero al transformarla en una variable binaria (`enfermo`), encontramos una distribución más equilibrada y apta para un clasificador binario.
2.  **Calidad de los Datos:** El dataset no contiene filas duplicadas, lo que garantiza la unicidad de las observaciones. Sin embargo, el alto volumen de nulos en variables clave (como `ca` y `thal`) exige el uso indispensable de técnicas de imputación robustas para evitar el sesgo en el modelo.
3.  **Modularidad:** La creación del `ColumnTransformer` permite garantizar que los datos de prueba futuros o nuevos registros clínicos pasen exactamente por el mismo flujo de transformación, evitando la fuga de datos (*data leakage*).
```
