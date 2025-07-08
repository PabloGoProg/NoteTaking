Un web socket es un **protocolo de comunicación** que permite una conexión persistente y bidireccional entre un cliente y un servidor. A diferencia del protocolo HTTP, donde se sigue un modelo de petición y respuesta para el intercambio de información, los Web Sockets permiten que **ambas partes envíen datos en cualquier momento**, sin necesidad de que una petición lo inicie y con muy baja latencia.

A nivel técnico un Web Socket es un **protocolo de mensajería asincrónica full-duplex (tipo de comunicación en la que dos partes pueden enviar y recibir datos al mismo tiempo)** donde tanto el cliente como el servidor pueden enviar mensajes el uno al otro de forma independiente, enviando y recibiendo información **sobre conexiones TCP**.

## Etapas de Trabajo de un Web Socket

1. Se establece una conexión apropiada para web sockets (Web Sockets Handshake) por parte del cliente hacia el servidor.

	Durante este proceso ocurre lo siguiente:
	
	El cliente _usa el protocolo HTTP para realizar una conexión a algún endpoint web socket_ deseado -> Este tipo de endpoints por lo general vienen marcados con el prefijo `ws://` o `wss://`. La petición es de tipo `GET` y viene con headers específicos que _identifican la intención de realizar un upgrade a una conexión de web Sockets._

##### Ejemplo de Header de Handshake
``` HTTP
GET /chat HTTP/1.1
Host: example.com:80
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw== -> Random base64 unique identifier
Sec-WebSocket-Version: 13 -> Protocol version
Sec-WebSocket-Protocol: chat, superchat -> Specific subprotocol
Origin: http://example.com
```

2. Si el servidor comunicado soporta el protocolo, enviará la confirmación de comunicación a través de lo headers.

	Una vez el servidor recibe la petición para la mejora de la conminación el backend:
	1. Valida que los headers en la petición sean validos para la conexión - específicamente valida la presencia de los headers `Upgrade: websocket` y `Connection: Upgrade`.
	2. Genera una clave de aceptación (**Sec-WebSocket-Accept**) para probar que el servidor Web Socket reconoció la operación Handshake como valida y que confirmo que es un cliente legitimo y no un actor malicioso. -> Para llevar a cabo la generación de la clave, el servidor toma el **Sec-WebSocket-Key** y lo concatena con un **UUID** predefinido para posteriormente pasarlo por un hash criptográfico y obtener la nueva clave. 
	3. El servidor envía un código de estado 101 (**Switching Protocols**) para indicar un cambio exitoso de protocolo.

##### Ejemplo de Headers de Respuesta
```HTTP
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
```

3. Una conexión Web Socket reemplaza el Handshake con la misma conexión TCP y se permite la comunicación.

	**Formato de URIs**
	* `ws`: `ws://host[":"port]path["?"query]` -> Port 80
	* `wss`: `wss://host[":"port]path["?"query]` -> Port 443

## Transmisión de Mensajes en Web Sockets
Cuando enviamos mensajes sobre una comunicación basada en web sockets, los mensajes sen envían en una secuencia de frames organizada de la siguiente manera:

![](https://miro.medium.com/v2/resize:fit:1400/1*rPd0v0HfC-tbAh1N_hhELQ.png)

* **FIN**: Determina si faltan más frames en ese mensaje (0) o si el último mensaje (1)
* **RSV 1,2,3**: Son tres bits reservados para futuros casos de uso o extensiones del protocolo.
* **opcode**: Define el tipo de datos que lleva el frame. -> Utf8, binario, ping (keep alive).
* **Mask**: Indica si el contenido lleva una mascara. -> Siempre esta activa en envíos cliente - servidor.
* **Payload Length**: Define el tamaño del contenido del frame (0 a 125).
* **Maskin key**: Usada para ofuscar los datos enviados por el cliente al servidor. -- No confundir con cifrado.
* **Payload data**: Contenido del frame.

### Masking
El masking hace que el contenido enviado por una comunicación web socket sea distintivo del trafico enviado en una comunicación HTTP, si bien es útil para prevenir ciertos ataques o filtros de seguridad, no fue implementado con ese fin.

Cuando un cliente WebSocket (como un navegador) envía un mensaje, enmascara (mask) el contenido del mensaje aplicando una operación XOR con una clave aleatoria de 4 bytes. Esto evita que el mensaje en texto plano pueda ser confundido con una petición HTTP u otro protocolo por dispositivos intermedios.