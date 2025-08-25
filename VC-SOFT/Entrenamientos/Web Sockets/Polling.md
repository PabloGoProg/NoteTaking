Previo a la implementación de los web sockets como un estándar en las comunicaciones en tiempo real, las actualizaciones del contenido compartido entre dos aplicaciones debía realizarse mediante **conexiones HTTP**. Para alcanzar un efecto similar a una **comunicación en tiempo real**, se empleo una técnica basada en este protocolo de comunicación: ==Polling==.

El Polling  es una técnica en la que un proceso o hilo verifica repetidamente (de forma activa y periódica) si ha ocurrido un evento o si hay datos disponibles para ser procesados.

---
### Short Polling
En el short polling el cliente o aplicación que requiere de las actualizaciones de los datos, hace peticiones constantes con una frecuencia muy alta y una distancia temporal corta entre ellas.

- Si el servidor tiene actualizaciones o nuevos datos, los devuelve dentro de la respuesta.
- De lo contrario, entrega una respuesta vacía.

#### Desventajas
- Uso inadecuados de recursos de computo.
- Incremento innecesario del trafico de red.
- Latencia impredecible entre la actualización de los datos en el servidor y la próxima iteración de polling.
- Mal escalado con grandes números de usuarios.
- Mala eficiencia energética en dispositivos móviles.

![](https://miro.medium.com/v2/resize:fit:911/1*b3T7Z5GonDo__72j2OUDmQ.png)

---
### Long Polling
En Long polling, a diferencia del short polling, el servidor no responde de inmediato. En su lugar, mantiene la conexión abierta hasta que tenga datos nuevos o hasta que se alcance un timeout (Hanging GET).

- En caso de que sea exitoso el llamada, el servidor enviara los datos en la respuesta y el cliente enviara nuevamente la petición de forma inmediata.
- En caso de presentarse un timeout, el cliente decide si realizar la conexión nuevamente de forma inmediata o esperar antes de realizarla nuevamente. 

#### Desventajas

- Posible saturación de servidores web mal configurados.
- Ineficiencia en el uso de recursos.
- Dificultad en la implementación de timeouts y reconexiones.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1712145017903/2c24bace-451a-42d6-9aea-5f65876dd284.jpeg)