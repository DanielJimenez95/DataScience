# Plan de Trabajo: Modelo de Predicción de Fuga de Clientes

## 1. Objetivo del Negocio
El objetivo es construir un modelo de machine learning que prediga la probabilidad de que un cliente cancele su contrato con la empresa de telecomunicaciones Interconnect. Esto permitirá a la empresa tomar acciones proactivas de retención, como ofrecer descuentos y planes especiales a clientes con alta probabilidad de fuga.

## 2. Comprensión y Análisis Exploratorio de Datos (EDA)
- **Carga y Fusión de Datos:** Cargar los cuatro archivos CSV (`contract.csv`, `personal.csv`, `internet.csv`, `phone.csv`) y unirlos en un único DataFrame utilizando la columna `customerID`.
- **Análisis Descriptivo:**
    - Revisar la estructura general del DataFrame (`.info()`, `.shape`).
    - Analizar estadísticas descriptivas de las variables numéricas (`.describe()`).
    - Verificar la existencia de valores nulos y duplicados.
- **Visualización de Datos:**
    - Crear gráficos de distribución para las variables numéricas (histogramas, boxplots) para entender su comportamiento.
    - Generar gráficos de barras para las variables categóricas para visualizar la frecuencia de cada categoría.
    - Analizar la relación entre cada característica y la variable objetivo (`Churn`) mediante gráficos agrupados.
    - Crear un mapa de calor de correlaciones para las variables numéricas.

## 3. Preparación de Datos e Ingeniería de Características
- **Limpieza de Datos:**
    - Corregir el tipo de dato de la columna `TotalCharges` (convertir a numérico) y manejar los valores nulos que puedan surgir.
    - Imputar o eliminar otros valores nulos si los hubiera.
- **Creación de la Variable Objetivo:**
    - Transformar la columna `EndDate` en una variable binaria `Churn` (1 si el cliente canceló, 0 si no).
- **Codificación de Variables Categóricas:**
    - Aplicar One-Hot Encoding a las características categóricas para convertirlas en un formato numérico que los modelos puedan procesar.
- **Escalado de Características:**
    - Estandarizar las variables numéricas (como `MonthlyCharges`, `TotalCharges` y `tenure`) utilizando `StandardScaler` para que tengan una media de 0 y una desviación estándar de 1.

## 4. Construcción y Entrenamiento de Modelos
- **División de Datos:** Separar el conjunto de datos en tres subconjuntos: entrenamiento (70%), validación (15%) y prueba (15%).
- **Modelos Base:** Entrenar varios modelos de clasificación con sus hiperparámetros por defecto para establecer un rendimiento de referencia. Los modelos a considerar son:
    - Regresión Logística
    - Random Forest
    - LightGBM
- **Métricas de Evaluación:** La métrica principal será el **AUC-ROC**, ya que es robusta ante el desbalance de clases. Como métrica secundaria se usará la **Exactitud (Accuracy)**.
- **Optimización de Hiperparámetros:**
    - Seleccionar el modelo con el mejor rendimiento base (probablemente LightGBM o Random Forest).
    - Utilizar una técnica como `GridSearchCV` o `RandomizedSearchCV` sobre el conjunto de validación para encontrar la combinación óptima de hiperparámetros que maximice el AUC-ROC.

## 5. Evaluación Final del Modelo
- **Evaluación en el Conjunto de Prueba:** Una vez optimizado, evaluar el modelo final en el conjunto de prueba (datos que el modelo no ha visto nunca) para obtener una estimación imparcial de su rendimiento.
- **Análisis de Importancia de Características:** Extraer y visualizar las características más influyentes para el modelo final. Esto proporcionará información valiosa sobre los factores que más contribuyen a la fuga de clientes.
- **Matriz de Confusión:** Analizar la matriz de confusión para entender los tipos de errores que comete el modelo (falsos positivos y falsos negativos).

## 6. Elaboración del Informe
Redactar un informe final que resuma el proceso, los hallazgos clave, el rendimiento del modelo, sus limitaciones y las recomendaciones de negocio basadas en los resultados.
