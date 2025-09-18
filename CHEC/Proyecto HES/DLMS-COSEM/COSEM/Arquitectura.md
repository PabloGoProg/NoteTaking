## Modelo de Comunicación

DLMS/COSEM usa los conceptos del modelo de referencia OSI (_Open Systems Interconnection_) para definir su modelo de comunicación.

El intercambio de datos entre los medidores y las aplicaciones recolectoras de datos (HESs) esta basada en el modelo **cliente servidor**, donde los HES toman el papel de los clientes y los medidores el papel de servidor. Adicionalmente. el servidor puede enviar respuestas no solicitadas al cliente para informar sobre eventos o enviar datos de forma pre configurada.

![[Pasted image 20250910150514.png]]

La comunicación de un cliente con un medidor se lleva a cabo en tres fases:

1. **Conexión a Nivel de Aplicación**: Aquí se lleva a cabo una _Application Association (AA)_ entre el cliente y la interfaz de comunicación del medidor.
	- Se debe tener en cuenta que cada _Logical Device (LD)_ puede comunicarse con 1 a N AAs.
2. Se lleva a cabo el intercambio de información.
3. Se da por finalizado el AA.

### Application Association
Son conexiones lógicas entre el cliente y la interfaz de comunicación del servidor. Pueden ser establecidas (_established_) o pre establecidas (_pre-established_), y las mismas pueden ser confirmadas o no confirmadas (_confirmed & unconfirmed_).

- Una AA confirmada es propuesta por el usuario y aceptada por el servidor. Aquí se asegura que:
	- El usuario que se comunica mediante el cliente es conocido por el servidor.
	- El _Application Context (AC)_ propuesto por el cliente es aceptado por el servidor.
	- El mecanismo de autenticación es valido y aceptado.
	- Los elementos solicitados pueden ser intercambiados de forma exitosa.
- Un AA no confirmada también es propuesta con el cliente, asumiendo que el cliente la aceptará - Aquí no se hace intercambio de información, este medio sirve para hacer broadcasting de mensajes de un cliente a los medidores.

---
### Factores y Conceptos a Tener en Cuenta
La autenticación en conexiones DLMS/COSEM toma lugar durante es establecimiento del AA.
- En AA confirmadas la auth puede ser unidireccional o bidireccional.
- En AA no confirmadas, el cliente se puede identificar el mismo.
- En AA pre establecidas no exite auth.


