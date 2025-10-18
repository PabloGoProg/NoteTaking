El modelo de servidor COSEM esta estructurado en tres niveles organizados de forma jerárquica:

1. **Physical Device**: Equipos físico real y todo el hardware que lo compone - medidor, concentrador, gateway, microcontrolador, interfaces de comunicación, etc. (Cada dispositivo físico puede tener más de un _Logical Device_).
2. **Logical Device**: Instancia lógica dentro de un physical device. - Es definido para que un mismo medidor (dispositivo) pueda ofrecer. distintos grupos de servicios.
3. **Accessible COSEM Objects**: Dentro de cada _Logical Device_ exiten los _Objetos COSEM_: Instancias de clases de interfaz.

---
### Logical Devices a Profundidad
Los _COSEM Logical Devices_ son conjuntos de _COSEM Objects_. Cada _Physical Device_ debe contener un **Management logical device**.
