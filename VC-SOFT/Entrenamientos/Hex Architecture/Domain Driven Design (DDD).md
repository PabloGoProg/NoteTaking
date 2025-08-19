Domain-Driven Design (**DDD**) es un enfoque de diseño de software centrado en el dominio del negocio y en la colaboración entre expertos técnicos y expertos del dominio (**usuarios, analistas, stakeholders**) para construir sistemas que **reflejen fielmente la lógica y necesidades del negocio**.

Su enfoque se centra en los siguientes principios: 
1. Capturar el dominio del modelo en los terminus del mismo dominio.
2. Embeber este dominio dentro del código.
3. Protegerlo del paso del tiempo.

![](https://media2.dev.to/dynamic/image/width=800%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fk04kx78m2nfct6qtdfwa.png)

### Lenguaje Ubicuo
Es una colección de términos y definiciones las cuales son utilizados por todo el equipo, incluyendo a aquellos técnicos y no técnicos. -> Incluye terminología referente al dominio del negocio y no aquella que el desarrollador de software suele utilizar.

---
#### Diseño Estratégico
El **diseño estratégico** es la parte de Domain-Driven Design que se enfoca en la **organización y estructuración del sistema a gran escala**, atendiendo las **relaciones entre diferentes áreas del dominio**, sus límites y la forma en que se comunican.

Su objetivo principal es **dividir un sistema complejo en múltiples _Bounded Contexts_**, cada uno con su propio modelo de dominio, lenguaje y responsabilidades bien definidos, permitiendo que el sistema sea **modular, escalable y alineado con la estructura del negocio**.
	
---
##### Conceptos Clave
* **Dominio:** Se refiere al área temática en la cual estamos construyendo la aplicación. Involucra todos los conceptos, actores y procesos que tengan un nombre y estén involucrados con el funcionamiento del área temática.
* **Subdominio:** Los subdominios son secciones bien delimitadas dentro del área temática en cuestión. Entre los tipos de subdominios se encuentran:
	* **Core:** Es el núcleo del negocio: el área que define la ventaja competitiva de la empresa y donde se encuentra la mayor complejidad intelectual.
	* **Soporte:** Son subdominios necesarios para que el negocio funcione, pero que no representan su diferenciador principal. -> Autenticación, pagos, soporte al cliente.
	* **Genérico:** Son funcionalidades comunes a muchos negocios, sin necesidad de personalización. Generalmente se resuelven con soluciones estándar del mercado (productos de terceros, librerías, frameworks). -> Mailing, Logging y Monitoreo, Pasarelas de Pago, etc.
- **Bounded Contexts:** Un contexto delimitado es un entorno explicito en el que un modelo de dominio tiene un significado bien definido, coherente y sin ambigüedades. Dentro de este límite, el lenguaje del negocio (lenguaje ubicuo) se usa de forma consistente, y las reglas del dominio se aplican con precisión.
- **Context Maps:** Diagrama que muestra cómo se relacionan los diferentes Bounded Contexts entre sí dentro de un sistema.
- **Integraciones entre subsistemas** 

### Diseño Táctico
El diseño táctico es el conjunto de patrones, herramientas y prácticas que se utilizan para modelar y estructurar el dominio del negocio dentro de un contexto delimitado. Su propósito principal es **reflejar con precisión las reglas, procesos y entidades del dominio en el código fuente**, de forma coherente, expresiva y mantenible.

-> El diseño táctico traduce el conocimiento del dominio en estructuras de software bien organizadas, promoviendo una alineación directa entre el código y el lenguaje del negocio.

---
##### Conceptos Clave
- **Entidades:** En DDD una entidad es un objeto de dominio que tiene una _entidad_ propria y persistente en el tiempo, independientemente de sus atributos. 
	- Las entidades tienen un identificador único que no cambia incluso si sus atributos lo hacen.
	- Dos instancias de un mismo tipo serán iguales si y solo si su identificador es igual entre ellos.
- **Objetos de Valor:** A diferencia de las entidades, los objetos de valor no tienen una identidad propia y están definidos únicamente por sus atributos.
	- No tienen un identificador único.
	- No importa _quién_ es, sino _qué_ representa.
	- Dos instancias son iguales si sus atributos lo son.
	- Son inmutables, si se require un cambio, se crea uno nuevo.
	- No requieren de una infraestructura para existir.
	- Modelan conceptos como cantidades, fechas, direcciones, rangos, coordenadas, etc.
- **Agregados:** Un agregado es **un conjunto de objetos de dominio** que forma una unidad de **consistencia y transacción**, gobernada por una Entidad raíz llamada _Aggregate Root_, que controla el acceso y las modificaciones al interior del agregado.
- **Raíz de Agregado:** Es un componente que encapsula una operación o regla del negocio que no pertenece naturalmente a una sola entidad u objeto de valor, pero que es parte importante del dominio.
	- Es considerado como una acción y refleja una operación de dominio.
	- No tiene un estado interno, opera sobre entidades y objetos de valor.
	- Implementa reglas del negocio, más no lógica técnica.
- **Repositorios:** Encapsula la lógica de acceso a datos para recuperar, almacenar y eliminar agregados (no entidades sueltas) de forma transparente para el dominio. - El objetivo es que **el dominio no tenga que preocuparse por cómo se guardan o cargan los datos**.
- **Fábricas:** Encapsula la creación compleja de objetos del dominio, especialmente de agregados o entidades que requieren múltiples pasos, validaciones o dependencias para construirse de forma consistente y válida.
- **Eventos de Dominio:** Es una notificación inmutable que indica que algo relevante ha sucedido dentro de un Bounded Context y que puede tener consecuencias para otras partes del sistema o del dominio mismo.
	- Siempre describen algo que ya ocurrió.
	- Tienen una estructura inmutable.
	- Representan un evento significativo para el negocio.

![](https://alok-mishra.com/wp-content/uploads/2021/06/screen-shot-2021-06-30-at-2.04.57-pm.png)