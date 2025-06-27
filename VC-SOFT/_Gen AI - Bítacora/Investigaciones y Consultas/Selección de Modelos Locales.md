Uno de los pasos esenciales previo al desarrollo de flujos automatizados asistidos por agentes de IA Generativa es la selección de un modelo ([[LLMs]]) que pueda ser ejecutado por los recursos existentes del equipo de computo utilizado.

En este caso, para esta implementación se cuenta con los siguientes equipos:

| Referencia       | CPU                          | GPU            | VRAM    |
| ---------------- | ---------------------------- | -------------- | ------- |
| MacBook Pro 2020 | Apple Silicon M1 - 8 núcleos | 8 núcleos      | ~8 Gbs  |
| HP 14cf3032la    | Core i5 1035G1 - 4 núcleos   | Intel Graphics | ~14 Gbs |

El primer equipo (Mac M1), cuenta con la ventaja de tener una GPU dedicada con 8 núcleos de procesamiento y 8 GBs de [memoria unificada](https://www.hoxtonmacs.co.uk/blogs/news/what-is-unified-memory?srsltid=AfmBOopB33VNIKd_omUapt1S9mev7KSeKeGh3prPNMvM0qLXbdZAVYQe), la cual provee un rendimiento considerablemente mayor que el equipo de HP, el cual, si bien utiliza una GPU integrada (SoC), la cual hace uso de la memoria RAM del equipo para obtener mejores resultados de eficiencia, el procesamiento de operaciones matriciales en paralelo, relevantes para la ejecución de modelos de inteligencia artificial basados en **redes neuronales** como lo son los LLMs, es inferior comparado con el de una unidad de procesamiento gráfico dedicado.

```cardlink
url: https://www.techspot.com/review/2796-amd-ryzen-8700g/#google_vignette
title: "AMD Ryzen 7 8700G Review: Most Powerful Integrated Graphics"
description: "The Ryzen 7 8700G is a Zen 4, Ryzen 7000-class processor that also includes a Radeon 700M GPU on the same chip. AMD says the iGPU will..."
host: www.techspot.com
favicon: https://www.techspot.com/images/ts3mobile-badge-196.png
image: https://www.techspot.com/articles-info/2796/images/amd-8700g-7.jpg
```
---
## Ventajas del Uso de Memoria Unificada
Comúnmente, la forma en la que se organiza y se accede a la memoria en las computadoras depende de la unidad de procesamiento, existiendo el concepto de Random Access Memory (RAM), la cual es la memoria utilizada por el procesador (CPU), y el concepto de Video Random Access Memory (VRAM) la cual es utilizada por las unidades de procesamiento gráfico (GPU). 

En caso de utilizar una gráfica integrada, la memoria RAM sería compartida entre el procesador central y el procesador gráfico integrado.

Apple, cuando trajo al mercado sus procesadores de arquitectura ARM, también trajo consigo un cambio de arquitectura que modificaba la forma en la que se manejaba y accedía a la memoria, llamada _Unified Memory_ o memoria unificada. De forma resumida, en este tipo de acceso a la memoria, la RAM es compartida entre la CPU, la GPU y las demás unidades de procesamiento del sistema, como lo pueden ser los aceleradores (Neural Engine o ML Cores).

Este tipo de manejo de la memoria es posible gracias a como se encuentran pensados los procesadores de la línea M de Apple, pues todos los componentes (CPU, GPU, RAM y Aceleradores) se encuentran soldados sobre el mismo chip, mientras que en los procesadores tradicionales, los mismos se encuentran distribuidos sobre la placa madre. Esto logra que todos los componentes tengan acceso a la misma memoria, contando con latencias muy bajas y un ancho de banda brutal (hasta 400 Gb/s en los M3 Max), mejorando el rendimiento en tareas que requieren la manipulación de grandes volúmenes de datos como desarrollo de tareas de IA, Machine Learning o la edición de video.

**Por qué es importante esto?**
Cuando hablamos de una computadora tradicional, especialmente si evaluamos su desempeño en las tareas mencionadas, el equipo estará limitado por la memoria de video con la que cuente la GPU, la cual, hoy en día para tarjetas comerciales de gama media es de 12 y 16 GBs, mientras que en la gama alta, la misma puede llegar hasta los 24 GBs, pero con un costo de compra muy elevado. Esto hace que los equipos de Apple Silicon de Apple sean una opción formidable para el desarrollo y experimentación con LLMs, pues con un costo menor, se puede acceder a una memoria unificada y capacidades de computo similares.

---
## Análisis de LLMs Locales
Más allá de entender las fortalezas y debilidades que tienen los recursos tecnológicos a los cuales se tiene alcance, es importante determinar que podemos hacer con ellos, más específicamente, que LLMs podemos ejecutar de forma local con este hardware y cual es su utilidad, pues cada modelo, a menos de que tenga una cantidad abismal de parámetros, seguramente tenga mejores "_habilidades_" en cierta área o dominio de conocimiento.

```cardlink
url: https://www.reddit.com/r/LocalLLaMA/comments/1iujafd/best_llms_focus_best_7b32b_02212025/
title: "Reddit - The heart of the internet"
host: www.reddit.com
```

Suponiendo entonces, que contamos con una capacidad de computo de una GPU de 8 núcleos y una memoria unificada de 8 GBs de RAM, lo recomendable sería optar por un modelo que se acomodará entre los 2 y 4 billones de parámetros. Esto pues, modelos superiores entre 7 y 9 billones requieren de entre 12 y 16 GBs de memoria, lo cual se sale de los limites establecidos por el hardware.

### Cuantización de Grandes Modelos de Lenguaje
Ahora, si bien contamos con un scenario de entrada que permite la exploración y delimitación de las capacidades de LLMs, en futuros escenarios, donde se cuente con mayores especificaciones de memoria VRAM o memoria unificada, se puede plantear la utilización de modelos cuantificados

La **Cuantización** es una técnica de compresión de modelos que convierte los pesos y los valores de activación de un LLM de valores de alta precisión a otros de menor precisión, lo cual es especialmente útil para permitir que modelos que cuentan con un gran número de parámetros, que comúnmente serían utilizados en negocio de tipo Modelo como Servicio (MaaS), pueda ser utilizados localmente a costo de un porcentaje de la precisión del modelo. Esto implica cambiar tipos de datos que pueden almacenar más información a aquellos que menos, sin alterar la naturaleza del tipo. Ejemplo de esto, sería la transformación de un flotante de 32 bits a uno de únicamente 8, en el cual el flotante de 32 bits podría asegurar 7 dígitos de precision decimal, mientras que el de 8 bits solo alcanzaría 1 o 2 decimales de precisión.

Reducir el número de bits necesarios para cada uno de los pesos o activaciones del modelo **conlleva una disminución significativa de su tamaño total**. En consecuencia, la cuantización reduce los LLM a versiones de si mismos que **consumen menos memoria, requieren menos espacio de almacenamiento y los hace más eficientes energéticamente**.
## Selección del Modelo
Por motivos de experimentación y desarrollo de los primeros flujos automatizados con integración de agentes de IA Generativa, se hará uso de `llama-3.2-3b-instruct`, el cual usa una arquitectura tradicional de transformadores, con una ventana de contexto de 128 mil tokens, siendo capas de obtener buenos resultados en tareas como el resumen de textos, traducción e incluso redacción. Este modelo, tiene un consumo aproximado de unas 6 GBs de memoria de video, siendo uno de los modelos de mejor costo beneficio en cuanto a recursos informáticos se habla.

