Aprendizaje sobresaliente sobre los datos de entrenamiento - "memorización" de los patrones de entrenamiento - incapaz de generalizar a los conceptos a nuevos datos.

## Regularización del Sobreajuste
* L1 (_Lasso_): Agrega una penalización basada en la suma de los valores absolutos de los pesos. - Pesos de conexiones irrelevantes son reducidos a 0. 
* L2 (_Ridge_): Agrega una penalización basada en la suma del cuadrado de los pesos. - Elimina valores muy grandes.
- _Dropout_: Desactivación aleatoria de un % de neuronas - eliminación de dependencia de características - aprendizaje distribuido.
- _Data Augmentation_: Enfasis en imágenes - reducción de sobre ajuste mediante modificaciones ligeras (zoom, rotaciones, cambios de escala).

# Gradient Vanishing
Ocurre cuando los gradientes que se propagan en capas iniciales toman valors muy cercanos a cero, reduciendo o impidiendo el aprendizaje. - Provocado por funciones de activación (ej. Sigmoide, tangente hiperbólica - Valores con derivada cercana a 0).

### Métodos de Mitigación
- **RelU**: la función de activación RelU, Leaky RelU o Parametric RelU mantienen derivadas constantes para valores mayores a 0.
- **Inicialización adecuada de valores**: valores iniciales malos pueden resultar en activaciones con valores muy grandes o pequeños - Inicialización de Xavier y Hehan promueven soluciones.
- **Batch Normalization**: Normalización de las salidas de activación para mantener los gradientes en valores óptimos.