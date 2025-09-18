Las siglas _DLMS_ (Device Language Message Specification) hacen referencia a un ==estándar global que define la modulación estructurada y el intercambio de datos generados por medidores==. _DLMS_ provee aplicaciones para la ==lectura de medidores, su control de forma remota y valor añadido para la medición de cualquier tipo de recurso== (agua, gas, electricidad, etc.).

Por su parte, _COSEM_ (Companion Specification for Energy Metering) es un modelo de interfaz especifico para la comunicación equipos de medición de energía eléctrica. Este proporciona:
- Una visión estandarizada de las funcionalidad accesibles.
- Una aproximación para la transferencia de datos basada en objetos.
- ==Un método controlado para identificar, obtener e interpretar información de cualquier tipo de medidor.==

---
## Términos Clave

| Nombre                              | Descripción                                                                                                   |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Client (master)                     | La maquina que corre el software capaz de realizar las peticiones.                                            |
| Server (slave)                      | El medidor                                                                                                    |
| Logical device                      | Es un dispositivo de almacenamiento para los objetos COSEM (Este dispositivo es interno al medidor).          |
| Object                              | Colección de atributos y métodos.                                                                             |
| Attribute                           | Un dato.                                                                                                      |
| OBIS (Object Identification System) | Un OBIS es un identificador único usado para diferenciar cada uno los datos usados en el dispositivo medidor. |
| Method                              | Una operación realizada sobre un atributo - GET, SET                                                          |

Usar la especificación _COSEM_ permite que los medidores de distintos proveedores y los sistemas recolectores de datos puedan intercambiar información de forma controlada gracias al modelado de objetos:

- Un objeto es representado por los atributos y sus valores. - El valor de un atributo _puede_ cambiar el comportamiento de un objeto.
- Los métodos para obtener o editar la información de atributos dependen del objeto.
- Los objetos que comparten características comunes se generalizan en interfaces (y se identifican con un `class_id`) Cada instancia de una clase que implementa una de estas interfaces se conoce como un _COSEM Object_.

