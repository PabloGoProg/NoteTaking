Un API Gateway es un componente clave en arquitecturas distribuidas de microservicios que actúa como un **punto de entrada único** para todas las peticiones externas dirigidas a los servicios internos de una aplicación. Se encarga de **recibir, enrutar, transformar y gestionar** las solicitudes antes de que lleguen a los microservicios correspondientes.

## Funcionalidades Ofrecidas por un API Gateway
- Autenticación y Aseguramiento de las políticas de seguridad.
- Balanceo de Carga y Circuit Breaking.
- Uso de rate limits.
- Traducción de protocolos de comunicación o formato de los datos.
- Monitoreo, logging y analíticas.
- Cache para respuestas comunes.
- Enrutamiento de solicitudes.

## Ventajas de uso de un API Gateway
- **Punto de entrada único:** Centraliza todas las solicitudes externas hacia los servicios internos, simplificando el acceso para los clientes del sistema.
- **Seguridad centralizada:** Hace el manejo de la autorización y la autenticación y aplica validaciones políticas de seguridad.
- **Rate limiting y control de tráfico:** Evita abusos con limitación de peticiones por segundo e implementa sistemas de **throttling**, **circuit breaking** o **timeout** de forma central.
- **Observabilidad:** Provee un registro centralizado de los logs métricas y trazas, facilitando el monitoreo, alertas y auditorías.
- **Desacoplamiento del cliente:** Permite cambiar o refactorizar servicios internos sin afectar a los consumidores.

## Flujo de la Petición de un Cliente
1. El cliente envía una petición al API Gateway (Comúnmente basada en HTTP).
2. El API Gateway valida la petición HTTP.
3. El API Gateway valida la dirección IP de la solicitud y headers relacionados con su origen para determinar si hace parte de un allow-list o un deny=list.
4. El API Gateway pasa la petición un **proveedor de identidad** para validar la autenticación y autorización de quien realiza la petición.
5. Con ayuda de un componente de **Service Discovery**, el API Gateway localiza la aplicación backend apropiada para manejar la petición usando **Path Matching**.
6. El API Gateway transforma el protocolo de comunicación de la petición en caso de ser necesario. -> Ej. REST -> gRPC. Una vez retornada la respuesta, la misma se traduce al protocolo original.

![](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fcb0c8192-4b1b-4834-b068-20d8cfb65050_1856x1412.png)