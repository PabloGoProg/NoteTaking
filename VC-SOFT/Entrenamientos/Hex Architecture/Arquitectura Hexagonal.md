BASE FUNDAMENTAL - Separation of Concerns (SoC)

Separation of Concerns es la práctica de organizar el código de manera que cada módulo, clase, o componente tenga una **única responsabilidad claramente definida**, sin mezclarse con otras.

Qué ventajas tiene?

- **Mejora la mantenibilidad**: Los cambios en una parte del sistema no afectan otras.
- **Facilita el testeo**: Al tener componentes con responsabilidades bien delimitadas, es más fácil probarlos de forma aislada.
- **Reduce el acoplamiento**: Componentes con responsabilidades separadas interactúan de forma más limpia.
- **Favorece la reutilización**: Una parte del sistema con una sola responsabilidad puede reutilizarse en otros contextos.

La **arquitectura hexagonal** busca aislar el núcleo de la aplicación (la lógica de negocio) de sus mecanismos de entrada/salida, pues organiza el sistema en torno a un núcleo independiente (**dominio**) que se comunica con el exterior a través de puertos (**interfaces**) y adaptadores (**implementaciones**), lo que permite intercambiar tecnologías sin afectar la lógica de negocio.

![](https://franiglesias.github.io/assets/images/ha/hexagonal_architecture.png)

## Componentes de la Arquitectura Hexagonal

* **Dominio:** El dominio es el conjunto de conocimientos, reglas, procesos y lógica de negocio que resuelve un problema específico del mundo real. En software, representa el "qué hace" el sistema, no el "cómo lo hace".
* **Puertos:** Un puerto es una abstracción (**interface**) que **expone** o **requiere** una funcionalidad específica del sistema, permitiendo al dominio **mantenerse independiente** de las tecnologías externas como bases de datos, APIs, UI o servicios externos.
	* **Driving Ports:** También llamado como puerto de entrada, define cómo se puede invocar la lógica de negocio (ej. ``CrearCuenta``, ``TransferirDinero``) 
	* **Driver Ports:** 	También conocidos como puertos de salida, define cómo el dominio usa servicios externos (ej. ``RepositorioDeCuentas``, ``ServicioDeNotificación``)
* **Adaptadores:** Un adaptador es una implementación concreta de un puerto (de entrada o de salida), que conecta el dominio con una tecnología externa como una API REST, una base de datos, un sistema de mensajería o una interfaz de usuario.
	* **Adaptadores de Entrada:** Reciben solicitudes del mundo externo y las traducen a llamadas al dominio.
	* **Adaptadores de Salida:** Implementan servicios requeridos por el dominio (puertos de salida), conectándose con tecnologías externas.