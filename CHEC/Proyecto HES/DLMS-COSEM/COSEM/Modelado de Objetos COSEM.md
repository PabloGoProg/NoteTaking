[Libro (Blue Book)](https://www.cs.ru.nl/~marko/onderwijs/bss/SmartMeter/Excerpt_BB7.pdf)

### Interface Class Notation
Las clases interfaces dentro del modelado COSEM cuentan con los siguientes elementos:

- _Class Name_: describe la clase.
- _Cardinality_: Especifica la cantidad de instancias con las que contara **ese dispositivo lógico**.
- _class_id_: Código de identificación de la clase - Puede tomar valores entre el rango de [0, 65.535], divididos en los siguientes sub intervalos:
	- De [0, 8.191] son valores reservados para los objetos estándar del protocolo DLMS. (Especificados por DLMS UA).
	- De [8.192, 32.767] son valores reservados para las interfaces propias del fabricante.
	- De [32.768, 65.535] son valores reservados para interfaces de un grupo de usuarios especifico.
- _Version_: Indican la versión del objeto - Todos los objetos instancia de una clase interfaz deben tener la misma versión.
	- Cuando se accede a un objeto a través de Logical Name (LN) o Short Name (DN), se puede acceder al atributo `object_list` que provee la lista de instancias.
- _Atributes_: Atributos de la clase:
	- _dyn._: Son una clase de 
	-  atributo que llevan valores necesarios para procesos internos, estos son actualizados únicamente por el medidor.
	- _static_: Atributos que no son configurables por el medidor en si mismo.
	- _logical_name_: Es el primer atributo de una clase, representa un identificador único para instancia de una clase.
	- _Data type_: Tipo de dato de un atributo.
	- _min_. _max_, _def_: valor mínimo, máximo y default de un atributo.
	- _Specific Methods_: Lista de los métodos especificos que pertenecen al objeto/
	- _m/o_: define si el método es opcional u obligatorio.