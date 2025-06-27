La Arquitectura Basada en Eventos (EDA), es una arquitectura basada en el patrón _publisher-subscriber_, orientadas a las aplicaciones basadas en micro servicios.

En esta arquitectura se cuenta con los siguientes elementos:
`Publisher -> [ Message Broker ] -> Micro Servicios Consumidores`
[[TO-DO]]
- **Publisher:** Micro servicio encargado de publicar el evento.
- **Message Broker:** Actúan como una ubicación centralizada para:
	- Ingerir y filtrar los eventos recibidos.
	- Definir control de acceso y políticas sobre quienes publican y quienes consumen.
- **MS Consumer:** Son los micro servicios que consumen los eventos publicados _bajo demanda_ 

### Ventajas
1. Supone menores tiempos de respuesta para el usuario, Esto ya que los eventos tarde o temprano serán procesados por los micro servicios, realizando los cambios pertinentes.
2. En caso de fallar alguno de los micro servicios, este no afectará a ninguno de los demás. Además, dependiendo de la implementación del broker, el evento del proceso fallido volverá a la cola y será ejecutado nuevamente.
3. Reducen costos de escalamiento vertical y horizontal, los cuales se ven aumentados en costes de infraestructura y monitoreo.
4. Reducen la necesidad de funciones personalizadas para la conexión entre el publisher y los consumidores.
### Desventajas
1. Se tienen latencias variables entre los servicios consumidores.
2. Frente a un volumen alto de procesamiento de eventos, se evidencian complicaciones en la detección de duplicados, determinar el estado del sistema o procesar las mismas transacciones.
3. Al ser una arquitectura asincrónica, los publishers no esperan por peticiones adicionales o resultados de sus eventos. 