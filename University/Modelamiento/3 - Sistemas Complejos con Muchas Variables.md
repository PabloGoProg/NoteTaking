### Automatas Celulares
Son un conjunto de automatas dispuestos a lo largo de una _cuadricula espeical regular_, - Sus estados son actualizados de forma simultanea mediante una _funcion de transicion_ 
* _Actualizacion sincronica_ -> Puede ser configurada para ser _asincronica_.

_Automata(s)_ -> Maquina teorica que cambia sus estado interno segun sus entradas y estados anteriores.
* El conjunto de estados es finito y discreto -> Causa no linealidad
#### Matematicamente:
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
### Reglas de Autómatas Celulares

1. _Regla de Mayoría:_ Se actualiza el valor conforme al valor que tengan la mayoría de sus vecinos.
2. _Regla de Paridad:_ 
