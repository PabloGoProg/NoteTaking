El **Modelo de Comunicación** seguido por el protocolo usa concepto del modelo _OSI_ (Open Systems Interconnection) y el modelo _cliente servidor_ para intercambiar información entre medidores y recolectores de datos.

En este sentido, las aplicaciones de recolección de datos toman el papel de un cliente, mientras que los medidores toman en papel de un servidor. El cliente puede:
1. Enviar peticiones y recibir respuestas de servicio.
2. Recibir peticiones "no solicitadas" por parte del cliente para ser informado sobre eventos o recibir información en condiciones pre configuradas.

## Nombres y Direcciones (Names & Addressing)
Las entidades participantes de una comunicación DLMS/COSEM (clientes y servidores) deben, dentro de una comunicación, ser identificados de forma única, para esto existe en _System Title_ El System Title es una herramienta de identificación útil tanto para el cliente como para el servidor y permiten que tanto el cliente como el servidor tengan seguridad de con quien se comunican.

Como estructura, el System Title tiene asignada una cadena de 8 bytes, la cual puede:
1. Ser auto generada para cada comunicación (generalmente del lado del cliente).
2. Ser estática y usarse la misma en cada comunicación (Comúnmente visto en medidores, pues el fabricante es quien se la da).

**SAPs**: Cada cliente y servidor DLMS/COSEM esta ligado a un Service Access Point (SAP). Como esta representado depende del perfil de comunicación utilizado. Los SAPs son utiles para la comunicación pues definen el nivel de asociación que se tendrá con el servidor.

Del lado del servidor, por debajo, existe un objeto (SAP Assignment) que mapea el valor del SAP usado con Application Association Object correspondiente.

**SAP's de Servidores**

| Ramge / SAP | Description                                       |
| ----------- | ------------------------------------------------- |
| 0           | Valor no usado                                    |
| 1           | Management Logical Device                         |
| 2 - 15      | Reservados para uso futuro                        |
| 16 ...      | Disponibles para aplicaciones de lado de servidor |
**SAP's de Clientes**

| Ramge / SAP | Description                                   |
| ----------- | --------------------------------------------- |
| 0           | No usado                                      |
| 1           | Client Management Process                     |
| 16          | Public Client                                 |
| 2 - 15      | Reservados para propositos especiales         |
| 17 - ...    | Reservados para aplicaciones de **cliente**** |

