### Autómatas Celulares
Son un conjunto de autómatas dispuestos a lo largo de una _cuadricula especial regular_, - Sus estados son actualizados de forma simultanea mediante una _función de transición_ 
* _Actualización sincrónica_ -> Puede ser configurada para ser _asincronica_.

_Automata(s)_ -> Maquina teorica que cambia sus estado interno segun sus entradas y estados anteriores.
* El conjunto de estados es finito y discreto -> Causa no linealidad
#### Matemáticamente:
* Son definidas como sistemas dinamicos donde el tiempo/espacio son discretos.
* Su modelo consiste en automatas identicos (celulas) dispuestos sobre una reticulo de alguna dimension (1, 2, 3).
* Cada automata es una variable dinamica, y su cambio temporal se da por la siguiente funcion _Funcion de transicion de estado_:![[Pasted image 20250312190528.png]]
	* El valor de la `x` o _celula focal_, tiene un valor definido por su _vecindario_, el cual esta compuesto del conjunto de las celulas adyacentes a ella -> ek vecindario puede tener un radio que define que tan grande es su alcance.
* La misma _funcion de transicion de estado_ debe de ser aplicada uniformemente a cada una de las celulas del automata. 

#### Definiciones:
* _Configuracion:_ una "imagen" del automata al completo.
* _Situacion:_ El contecto de una celula y su vecindario en un momento determinado.
	* _Neuman_: el nuevo estado de una celula se define por sus celulas adyacentes (arriba, abajo, izquierda, derecha).
	* _Morre_: Anade las 4 celulas diagonales.
	* En ambos persiste el radio.
* _Funcion de transicion:_ 
	* Se aplic uniforme y simultaneamente a todas las celulas del espacio.
	* Puede ser definida de muchas formas.
	* Si una funcion de transicion da un mismo valor en situaciones iguales cuando son rotadas, se tiene _Simetria Rotacional_.
	* _Simetria Rotacional_: 
		* Fuerte: El vecindario tiende a rotar cuando las variables son actualizadas.
		* Debil: No se conserva una orientacion identica en todos los vecinos.
	* Si la funcion depende unicamnete de la suma del estado de las celulas de un vecindario, se le llama _funcion totalista_.
* _Estados de las celulas:_
	* _Quiescentes_ Una celula mantiene su estado si sus vecinos tambien lo hacen.
		* Se encuentra inactiva
	* _No Quiescentes:_ 
* _Limite - Borde:_ 
	* Sin limites -> Espacio infinito.
	* Limites de corte -> Espacio limitado -> no hay vecinos de ciertas dimensiones.
	* Limites fijos -> Se asume que las células encontradas en los bordes _nunca_ cambiaran.
#### Reglas de Autómatas Celulares

1. _Regla de Mayoría:_ Se actualiza el valor conforme al valor que tengan la mayoría de sus vecinos.
2. _Regla de Paridad:_ 
## Redes
Son un conjunto de vertices y aristas que se interconectan entre si.
- Un node es llamado de otro sis y solo se esta conectado a este.

**Representación de los nodos del vecindario:** Se pueden utilizar dos recursos:
1. Matriz de Adyacencia![](https://calculo.cc/temas/temas_algebra/matriz/imagenes/teoria/grafo/grafo-y-matriz.gif)
2. Lista de Adyacencia ![](https://www.researchgate.net/publication/309278789/figure/fig14/AS:750920426086401@1556044789767/Grafo-dirigido-con-su-representacion-como-lista-de-adyacencia.ppm)

**Clasificación de las redes:**
- _Grado:_ el número de lazos conectados a un nodo -Si un nodo esta conectado a dos vecinos tiene grado _dos_.
- _Caminata - recorrido:_ Lista de nodos secuenciales usados para hacer un recorrido en la red.
	- _Sendero_: No pasa por ningún lazo más de una vez.
	- _Camino:_ No pasa por ningún nodo más de una vez.
	- _Ciclo:_ Empieza y termina en el mismo nodo, pero no repite ni nodos ni enlaces en su recorrido.
- _Sub-red:_ 
- _Conectada:_ Siempre que exista un camino para cada par de nodos.
- _Componente conectado:_