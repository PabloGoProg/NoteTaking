Mathematical model inspired by the biological neurons.

Inicialmente desarrollado por _**Frank Rosenblatt**_ en 1958 - modelo pionero del aprendizaje supervisado - base de redes neuronales modernas - Capas de resolver **problemas linealmente separables.**

## Conceptos
- **Frank Rosenblatt**: representan las características del conjunto de datos.
- **Pesos**: la importancia de cada una de las variables.
- **Sumas Ponderadas**: $y = w_1x_1 + w_2x_2 + w_3x_3 = b$ combinación lineal de entradas y pesos - se agrega un sesgo o bias (b) que permite el ajuste del modelo y el desplazamiento de la función de activación.
- **Funciones de Activación**: decide la salida final del perceptron.
***
### Proceso de Funcionamiento
1. Se asignan valores _aleatorios pequeños_ a los pesos y el sesgo.
2. Cálculo de suma ponderada y aplicación de la función de activación.
3. Comparar con la salida esperada.
4. Si falla -> Ajustar los valores de los pesos con respecto a la regla de aprendizaje. $w_i = w_i + n(y - \hat{y})x_i$ - dónde n es la taza de aprendizaje.
***

# Multi Layer Perceptron (MLP)
Adaptación del perceptron para la solución de problemas no linealmente separables. - Primera implementación de capas ocultas y _back propagation_ del error para entrenar la red.

## Capas
1. Entrada - Recibe los datos de entrada. - Envío de los datos sin modificaciones.
2. Ocultas - Se reciben las entradas de la salida de la capa anterior - suma ponderada - función de activación no lineal
3. Salida - Predicción del modelo
	- 1 Neurona - Regresión
	- 2 Neuronas - Binaria
	- 2 Neuronas - Multi clase




