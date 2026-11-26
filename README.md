``markdown
# 🏥 Proyecto de Predicción de Enfermedades Cardíacas (UCI)

Este repositorio contiene un flujo de trabajo completo para el análisis exploratorio de datos (EDA), la limpieza y el preprocesamiento de un conjunto de datos sobre enfermedades cardíacas proveniente de la **UCI (University of California, Irvine)**.

El objetivo de este proyecto es preparar y estructurar de manera óptima las variables clínicas y demográficas de los pacientes para entrenar modelos predictivos capaces de detectar la presencia o ausencia de afecciones cardíacas.

---

## 📋 Estructura y Flujo del Proyecto

### 1. Conexión e Importación de Datos
* **Entorno:** Google Colab con montaje en Google Drive para la gestión de archivos.
* **Librerías principales:** `pandas`, `numpy`, `matplotlib`, `seaborn` y componentes de `scikit-learn`.
* **Conjunto de datos:** Un dataset de 920 registros clínicos y 16 columnas iniciales.

### 2. Análisis Exploratorio de Datos (EDA)
* **Auditoría de Datos:** Inspección de las dimensiones, tipos de datos (`df.info()`) y distribución estadística de las variables numéricas (`df.describe()`).
* **Visualización de la Variable Objetivo:**
  * **Multiclase (`num`):** Se analizó la distribución original del diagnóstico (valores de `0` a `4`), donde `0` representa ausencia de enfermedad y `1-4` diferentes niveles de gravedad.
  * **Binaria (`enfermo`):** Se transformó la variable a un problema de clasificación binaria (`1` si presenta enfermedad, `0` si no la presenta) para simplificar la detección preventiva.
* **Análisis de Valores Faltantes:** Visualización gráfica mediante un diagrama de barras (`sns.barplot`) para identificar qué variables presentaban mayores vacíos (por ejemplo, `ca`, `thal` y `slope` con mayor cantidad de nulos).

### 3. Preprocesamiento Automatizado (Pipelines)
Se estructuró un flujo de transformación robusto utilizando `ColumnTransformer` de scikit-learn:
* **Variables Numéricas:** Imputación por la media y escalado estándar (`StandardScaler`).
* **Variables Categóricas:** Imputación de nulos por la moda (el valor más frecuente) y codificación con `OneHotEncoder`.
* *Nota de Corrección:* Se solucionó en caliente un error de nombres de columna corrigiendo el descriptor de la variable `'trestbs'` por `'trestbps'` (presión arterial en reposo).

### 4. Normalización Manual y Codificación Alternativa
Como alternativa de ingeniería de características, se generó un flujo personalizado sobre un set `df_model`:
* **Imputación de Nulos:** Los nulos en las columnas numéricas críticas `'trestbps'` y `'chol'` (colesterol) se rellenaron con su mediana respectiva para evitar sesgos por valores extremos.
* **Escalado MinMax:** Se escalaron las variables de `'age'` (edad), `'trestbps'` y `'chol'` para que sus valores queden estrictamente entre `0` y `1`.
* **Codificación de Categóricas:** Aplicación de `pd.get_dummies` de forma manual sobre `'sex'` (género) y `'cp'` (tipo de dolor de pecho).

### 5. Consolidación y Limpieza Final
* Se fusionaron las variables procesadas de características (`x`) con nuestra etiqueta objetivo (`y`).
* Se realizó una limpieza final eliminando cualquier fila residual con valores faltantes mediante un `dropna()` global.
* **Resultado:** Un dataset final de variables independientes `x` y etiquetas `y` verificado con `0%` de valores nulos, listo para algoritmos de clasificación como Regresión Logística, Árboles de Decisión o Random Forest.
```
