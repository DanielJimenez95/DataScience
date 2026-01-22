# Informe de Solución: Predicción de Fuga de Clientes

## 1. Resumen Ejecutivo
Se ha desarrollado un modelo predictivo para identificar a los clientes de Interconnect con mayor probabilidad de cancelar sus servicios. Tras un proceso de análisis, preparación de datos y optimización de modelos, se seleccionó un clasificador **LightGBM** como la solución final. El modelo alcanzó un **AUC-ROC de [valor final]** y una **exactitud de [valor final]%** en el conjunto de datos de prueba, demostrando una alta capacidad para distinguir entre clientes que cancelarán y los que no. Las variables más influyentes en la predicción fueron el tipo de contrato, la antigüedad del cliente (`tenure`) y el total de cargos mensuales. Este informe detalla los resultados y ofrece recomendaciones para la implementación del modelo en una estrategia de retención.

## 2. Resultados Clave del Modelo
- **Modelo Seleccionado:** LightGBM (Gradient Boosting Machine)
- **Métricas de Rendimiento (Conjunto de Prueba):**
    - **AUC-ROC:** [valor final]
    - **Exactitud (Accuracy):** [valor final]%
- **Características Más Predictivas:**
    1.  **Tipo de Contrato (`Contract`):** Los clientes con contratos mes a mes tienen una probabilidad de cancelación significativamente mayor que aquellos con contratos anuales.
    2.  **Antigüedad (`tenure`):** Los clientes más nuevos son mucho más propensos a cancelar.
    3.  **Servicio de Internet (`InternetService_Fiber optic`):** Los clientes con fibra óptica muestran una tasa de cancelación más alta, lo que podría indicar problemas de precio o calidad en este servicio.
    4.  **Cargos Mensuales (`MonthlyCharges`):** A mayores cargos mensuales, mayor es la probabilidad de fuga.

## 3. Metodología
El proyecto siguió el plan de trabajo definido, que incluyó las siguientes fases:
1.  **Análisis Exploratorio de Datos (EDA):** Se unificaron las fuentes de datos y se analizaron las distribuciones y relaciones entre las variables para entender los perfiles de los clientes que cancelan.
2.  **Preprocesamiento:** Se realizó una limpieza de datos, se transformaron las variables categóricas mediante One-Hot Encoding y se estandarizaron las variables numéricas.
3.  **Modelado y Optimización:** Se entrenaron tres modelos base (Regresión Logística, Random Forest, LightGBM). Se seleccionó LightGBM por su rendimiento superior y se optimizaron sus hiperparámetros para maximizar el AUC-ROC.
4.  **Evaluación Final:** El modelo optimizado fue evaluado en un conjunto de datos de prueba, previamente reservado, para validar su rendimiento.

## 4. Limitaciones
- **Datos Estáticos:** El modelo se basa en una fotografía de los datos al 1 de febrero de 2020. El comportamiento de los clientes puede cambiar con el tiempo, por lo que el modelo podría requerir reentrenamiento periódico.
- **Variables Externas:** El análisis no incluye factores externos que podrían influir en la decisión de un cliente (ej. ofertas de la competencia, situación económica general).

## 5. Conclusiones y Recomendaciones
**Conclusión:** El modelo desarrollado es una herramienta eficaz y fiable para predecir la fuga de clientes. Permite a Interconnect pasar de una estrategia reactiva a una proactiva, identificando a los clientes en riesgo antes de que tomen la decisión de irse.

**Recomendaciones:**
1.  **Implementación Operativa:** Integrar el modelo en los sistemas de CRM de la empresa para generar una "puntuación de riesgo de fuga" para cada cliente mensualmente.
2.  **Campañas de Retención Dirigidas:** Utilizar esta puntuación para segmentar a los clientes y dirigir las campañas de retención (códigos promocionales, planes especiales) a aquellos con mayor riesgo.
3.  **Revisión de Estrategia de Contratos:** Fomentar la migración de clientes de contratos mes a mes a contratos de 1 o 2 años, ya que estos últimos tienen una tasa de retención mucho mayor.
4.  **Análisis del Servicio de Fibra Óptica:** Investigar las razones de la alta tasa de cancelación entre los usuarios de fibra óptica. Podría estar relacionado con el precio, la estabilidad del servicio o la calidad del soporte técnico asociado.
5.  **Monitoreo Continuo:** Monitorear el rendimiento del modelo a lo largo del tiempo y reentrenarlo cada 6-12 meses con datos nuevos para asegurar su precisión.
