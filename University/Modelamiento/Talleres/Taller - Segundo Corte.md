# Preguntas Teóricas

## Modelamiento en Tiempo Discreto y Continuo

2. ¿Cómo puede usarse un modelo en tiempo discreto para predecir el comportamiento a largo plazo de una población?

Un modelo en tiempo discreto puede predecir el comportamiento a largo plazo de una población mediante **ecuaciones en diferencias**, que describen cómo evoluciona la población entre instantes sucesivos.

Un ejemplo básico es el **modelo de crecimiento exponencial**, donde la población crece proporcionalmente a su tamaño anterior:

$$
P_t = \alpha P_{t-1}
$$

Sin embargo, para reflejar un crecimiento más realista, limitado por recursos, se puede usar el **modelo logístico**, que incorpora la **capacidad de carga** del ambiente (K) y permite que la población tienda a un valor máximo estable. Su ecuación es:

$$
x_t = \left(-\frac{\alpha - 1}{K}x_{t-1} + \alpha\right)x_{t-1}
$$
---
7. ¿Cómo puede afectar un parámetro la evolución de un sistema?

	Cuando modelamos un sistema dinámico, sea discreto o continuo, los parámetros son valores constantes que caracterizan cómo se comporta dicho sistema con el paso del tiempo. Si bien estos no cambian sus valores durante la simulación, tienen un impacto directo sobre diversos aspectos del sistema, entre los que se incluyen:
	
	1. **Estabilidad del Sistema:** El valor que tengan los parámetros de nuestro sistema pueden afectar la estabilidad del mismo, implicando. que puede ser más sensible al desorden frente a cambios o perturbaciones ligeras del sistema. Ejemplo de esto, es la tasa de crecimiento dentro de un sistema de crecimiento exponencial ($\alpha$). pues dependiendo de su valor se pueden presentar los siguientes casos: 
		$$P = \alpha P_{t-1}$$
		
		1. $\alpha < 0$, se considera **estable**, pues cualquier valor de $x_0$ va a llegar a 0 con el tiempo.
		2. $\alpha > 1$, se considera **inestable**, pues el valor crecerá sin limites.
		3. $\alpha = 1$, el sistema se mantiene en su mismo valor, lo que lo hace **marginalmente estable**.
		
	2. **Velocidad de Convergencia:** El valor de los parámetros puede determinar a que velocidad converge una variable. Siguiendo el ejemplo pasado, supongamos el siguiente cambio:
		$$P = (1 - b)P_{t-1}$$
		
		Si el valor de b es cercano a 0, la variable converge de una forma muy lenta, mientras que si si su valor es cercano a uno, este converge de forma más acelerada.

	3. **Bifurcaciones:** Cuando se cambia el valor de un parámetro, también cambia el comportamiento general del sistema, llevando a oscilaciones, ciclos que son cada vez más complejos o la aparición de comportamientos caóticos. Estos cambios severos de comportamiento por pequeños cambios en los parámetros son también llamados _bifurcaciones_.
---
8. ¿Qué suposiciones se hacen al utilizar ecuaciones diferenciales ordinarias para representar sistemas dinámicos?

	1. Las trayectorias del sistema son siempre continuas y suaves, por lo que no existen saltos o discontinuidades.
	2. La dinámica del sistema es determinista, por lo que si se conoce el estado inicial y las ecuaciones describen el comportamiento del sistema, se puede predecir su evolución.
	3. El tiempo es una variable continua y no una serie de tiempo de pasos equitativamente distantes el uno de el otro.
	4. Se usan condiciones iniciales para trazar la trayectoria correspondiente a su solución.
---
11. Una solución analítica produce una solución exacta en forma de función, esta es hallada tras resolver la ecuación diferencial ordinaria que representan el sistema, la misma es capas de definir el comportamiento del sistema para cualquier instante de tiempo dado (variable independiente de la función). El problema con este tipo de soluciones, es que muchos de los sistemas estudiados en el mundo real se describen mediante ecuaciones diferenciales no lineales o sistemas de soluciones acopladas, las cuales no tienen soluciones analíticas o son extremadamente complejas de encontrar

	Por su parte, las soluciones numéricas generan soluciones aproximadas del comportamiento del sistema, las cuales discretizan el tiempo para permitirle a la computadora realizar cálculos de forma secuencial. Esta discretización del tiempo, simula el efecto que producen las tasas de cambio definidas por las ecuaciones diferenciales, por lo que usar tasas de cambio cada vez más pequeñas, hace que el resultado sea más aproximado a la solución continua del sistema. 
	
	Este tipo de soluciones permiten observar el comportamiento del sistema bajo condiciones especificas, como lo son las condiciones iniciales del sistema o el valor de sus parámetros.
---
## Bifurcaciones

3. ¿Por qué las bifurcaciones pueden ser importantes en la predicción de cambios críticos en sistemas reales?

Las bifurcaciones son importantes para la predicción de cambios críticos en sistemas reales, pues estas marcan __Cambios Cualitativos__ en el comportamiento del sistema a medida que se modifican sus parámetros, logrando identificar puntos de transición entre distintas regiones de comportamiento. Esto ayuda a entender la sensibilidad de un sistema a sus parámetros, el seguimiento de comportamientos no lineales de muchos sistemas complejos, y la prevención de cambios críticos en distintas áreas.

---
4. Consulte: ¿Qué diferencia hay entre una bifurcación de transcritical y una de saddle-node?

* _Bifurcación Saddle Node:_ En este tipo de bifurcación se crean o destruyen dos puntos de equilibrio, uno estable y uno inestable al pasar por un punto crítico o punto semi estable.

	![](https://hmco.enpc.fr/UNIT_ComplexSystems/~gen/3_DynamicalSystems/DynamicalSystems_web.publi/web/res/SaddleNode.png)

	En el gráfico se observa que a medida que incremente el parámetro r, ocurre lo siguiente:
	
	- Cuando $r < 0$, no existe ningún punto de equilibrio.
	- Cuando $r = 0$, se encuentra un equilibrio semi estable.
	- Una vez $r > 0$, se crean dos puntos de equilibrio, el estable marcado con la línea azul y el inestable marcado con la línea roja.
	
- _Transcritical Bifurcation:_ En este tipo de bifurcaciones los puntos de equilibrio colisionan el uno con el otro, intercambiando sus estabilidades, por lo que un nodo que tiene un equilibrio estable, pasa a ser inestable una vez colisiona con el otro nodo y vise versa.

	La diferencia con respecto a las bifurcaciones nodos de silla (saddle-nodes) es que en este tipo de bifurcaciones no se crean ni se destruyen puntos de equilibrio, pues estos, tanto el estable como el inestable, ya existen desde el primer momento.
	![](https://math.libretexts.org/@api/deki/files/9661/Fig._8.3.PNG?revision=1)
---
## Caos

2. ¿Cómo puede una pequeña diferencia en las condiciones iniciales llevar a comportamientos caóticamente divergentes?

Esto es debido a que una de las características clave del caos es que un sistema puede comportarse de formas muy diferentes al largo plazo debido a mínimas diferencias en sus condiciones iniciales, lo cual se define como **sensibilidad a las condiciones iniciales**, esto se debe principalmente a que las pequeñas diferencias entre trayectorias se amplifican exponencialmente a medida que pasa el tiempo. Ejemplo de esto es el mapa logístico, el cual a medida que crece la tasa de natalidad, tiene comportamientos cada vez más caóticos.

---
## Redes

2. ¿Cuál es la diferencia entre un grafo dirigido y uno no dirigido? ¿Puedes dar un ejemplo de cada uno en la vida real?

La diferencia entre un grafo dirigido y uno no dirigido es que el grado dirigido tiene lazos unidireccionales con sus vecinos, mientras que en los no dirigidos tienen relaciones bi direccionales con sus vecinos. Por ejemplo, una representación de un grafo dirigido es la red social X (Twitter), ya que seguir a alguien no implica que esa persona te siga a ti también, por lo tanto, si tenemos dos usuarios, A y B, y el usuario A sigue al usuario B, no implica que el usuario B siga al usuario A. Por otro lado, un ejemplo de un grafo no dirigido sería el sistema de amigos de Facebook, pues la relación de amistad en la plataforma es bi direccional, lo que implica que si el usuario A es amigo del usuario B, por lo tanto el Usuario B también es amigo del usuario A.

4. ¿Qué es una caminata (walk), un camino (path) y un ciclo en un grafo?

- **Caminata:** Lista de nodos secuenciales usados para hacer un recorrido en la red.
- **Caminata:** Es un recorrido que no pasa por el mismo nodo más de una vez.
- **Ciclo:** Recorrido que empieza y termina en el mismo nodo, pero no repite nodos ni enlaces en trayecto.