<div align="center">
<picture>
    <source srcset="https://imgur.com/5bYAzsb.png" media="(prefers-color-scheme: dark)">
    <source srcset="https://imgur.com/Os03JoE.png" media="(prefers-color-scheme: light)">
    <img src="https://imgur.com/Os03JoE.png" alt="Escudo UNAL" width="350px">
</picture>

<h3>Curso de Robótica 2025-I</h3>

<h1>Funcionamiento de ROS 2 Graph</h1>

<h2>Guía 03 - Funcionamiento de ROS 2 Graph</h2>


<h4>Pedro Fabián Cárdenas Herrera<br>
    Manuel Felipe Carranza Montenegro</h4>

</div>

<div align="justify"> 

### 1. ¿Qué es la ROS 2 Graph?

La **ROS 2 Graph** es una representación abstracta de cómo los elementos dentro de un sistema ROS 2 se conectan entre sí. Es una red dinámica de **nodos**, **tópicos**, **servicios**, **parámetros** y **acciones** que interactúan para procesar y compartir datos de forma simultánea.

Si visualizáramos la ROS 2 Graph gráficamente, veríamos todos los nodos (ejecutables) interconectados a través de tópicos, servicios y acciones, mostrando cómo se intercambian datos entre los diferentes componentes del sistema en tiempo real.


### 2. Nodos en ROS 2

En ROS 2, un nodo es la unidad básica de ejecución. Cada nodo tiene una tarea específica y se comunica con otros nodos para realizar funciones dentro del sistema. Por ejemplo, un nodo puede encargarse de controlar los motores de un robot, mientras que otro puede encargarse de procesar datos de un sensor.

> **Importante:** Un único ejecutable puede contener varios nodos, lo que permite modularizar las tareas y distribuirlas de manera más eficiente.

**Ejemplo práctico:** Imagina que tienes un robot móvil. El sistema robótico podría tener nodos para controlar los motores de las ruedas, otros para leer los sensores, y otros para realizar decisiones de navegación. Todos estos nodos trabajan de manera independiente pero se comunican a través de la ROS 2 Graph.

<div align="center">
  <img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExZ2p1N3lrMmJieW5hMXdtMTEwcXBmbTZuajZqYTlmdDJ6dWZ4MGQ0eCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/qquDouwBrGsBnWaAmY/giphy.gif" alt="Prueba de funcionamiento">
</div>

**Ejemplo:** Un sistema robótico completo está compuesto por muchos nodos trabajando en conjunto, en ROS 2, un solo ejecutable (programa en C++, Python, etc.) puede contener uno o más nodos.

### 2. Tópicos en ROS 2

En ROS 2, los tópicos son canales de comunicación que permiten a los nodos intercambiar mensajes. Los nodos pueden publicar mensajes en un tópico y otros nodos pueden suscribirse a ese tópico para recibir actualizaciones. Es como una transmisión de datos donde los nodos que se suscriben reciben los mensajes publicados por otros nodos.

<div align="center">
  <img src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExd3F3dGUwMnJlbjZqd3ZhdTJidW9sNWs1NW9uZjI4ZzAzeTI4cmxvMiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/p42BrUzXTiFzu26CSz/giphy.gif">
</div>

> Un nodo puede publicar datos en cualquier número de tópico y, al mismo tiempo, tener suscripciones a cualquier número de tópicos.

<div align="center">
  <img src="https://media2.giphy.com/media/v1.Y2lkPTc5MGI3NjExa2lrODN1dnA1Z3I4OXF4MHN2M3JpNWlqaWVmeTh0dm5mOXY4bThraCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/B6iyBxGhsGe8UY4CCG/giphy.gif">
</div>

Los tópicos son especialmente útiles cuando se necesita enviar información de manera continua entre los nodos, como por ejemplo, en la transmisión de datos de sensores o la actualización de la posición de un robot.

### 3. Servicios en ROS 2

Los servicios en ROS 2 son otro método de comunicación entre nodos. A diferencia de los tópicos, que funcionan en un modelo de publicación-suscripción continuo, los servicios operan en un modelo de llamada y respuesta.

<div align="center">
  <img src="https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExYWVmeTRvMmltOWlsdTFxOXc1YjNvNWk1em16dnlobW80OHUyYW0zNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/ZwtP7OMlnkGiovXZMP/giphy.gif">
</div>

Cuando un nodo solicita un servicio, este envía una "petición" al nodo servidor, y este le responde con los datos solicitados. Es un tipo de comunicación más puntual y no continua.

<div align="center">
  <img src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExc3RwdWs4ZW9jOGtzeWRqcDJqMHo1emw5aHVkcmNqYXFrYzZkY2NsMCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/VF8KR8o034lavFobSD/giphy.gif">
</div>

Los servicios son útiles cuando necesitas obtener una respuesta específica y no un flujo constante de datos. Por ejemplo, si un nodo necesita obtener la temperatura de un sensor en un momento específico, puede hacer una llamada a un servicio para recibir esa información.

### 4. Parámetros en ROS 2

Un parámetro es una configuración que un nodo puede almacenar para modificar su comportamiento. Por ejemplo, puedes tener un parámetro que controle la velocidad de un motor o el rango de un sensor.

> En ROS 2, cada nodo maneja sus propios parámetros, que pueden ser de diferentes tipos: enteros, flotantes, booleanos, cadenas de texto, o incluso listas.

Los parámetros pueden cambiar en tiempo de ejecución, lo que permite modificar el comportamiento del nodo sin necesidad de reiniciarlo. Sin embargo, al intentar cambiar el tipo de un parámetro en tiempo de ejecución, esto fallará por defecto para evitar errores comunes.
Si se necesita permitir varios tipos de datos en un parámetro (por ejemplo, un parámetro que puede ser tanto un número entero como un valor flotante), se puede activar el tipado dinámico al declarar el parámetro con un `ParameterDescriptor` y configurando la propiedad `dynamic_typing` como `true`.

### 5. Acciones en ROS 2

Las acciones son ideales para tareas que requieren un procesamiento de largo plazo, como mover un robot a través de una ruta compleja o realizar un análisis detallado de datos. Las acciones se componen de tres partes principales:

- **Objetivo:** Lo que se desea lograr.
- **Retroalimentación:** Información periódica sobre el progreso de la tarea.
- **Resultado:** El resultado final cuando la tarea se completa.
Las acciones se basan en temas y servicios, pero su principal diferencia es que pueden ser canceladas y proporcionan retroalimentación continua durante su ejecución.

En lugar de funcionar en un modelo de llamada y respuesta como los servicios, las acciones operan bajo un modelo cliente-servidor. Un nodo cliente de acción envía un objetivo a un nodo servidor de acción, que ejecuta la tarea, proporcionando retroalimentación mientras la tarea progresa y, finalmente, devuelve un resultado cuando se completa.

<div align="center">
  <img src="https://media4.giphy.com/media/v1.Y2lkPTc5MGI3NjExenp4Nm9vYnRneXowZm95cTJ4eDY3dGl0cmRobjlpaW56aDFwdjQ2ayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/pvXuyzRoWrUwDlaQUw/giphy.gif">
</div>

### 6. Diferencias

| **Elemento**   | **Descripción**                                                                                          | **Modelo de Comunicación**         | **Propósito**                                                                                       | **Ejemplo**                                                                                         |
|----------------|----------------------------------------------------------------------------------------------------------|------------------------------------|----------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Nodos**      | Son los ejecutables que realizan tareas específicas en ROS 2, como controlar motores o procesar datos.    | Cada nodo es autónomo               | Ejecutan funciones específicas y pueden compartir datos con otros nodos.                           | Un nodo controla un sensor de distancia, otro nodo controla el motor.                               |
| **Tópicos**    | Canales de comunicación entre nodos para intercambiar mensajes.                                           | Publicador-Suscriptor               | Permiten la transmisión continua de datos entre nodos.                                              | Un nodo publica lecturas de un sensor de distancia en un tópico; otro nodo se suscribe para recibir los datos. |
| **Servicios**  | Métodos de comunicación basados en una solicitud y respuesta, a diferencia del modelo de publicación-suscripción de los tópicos. | Cliente-Servidor                   | Proveen datos solo cuando son solicitados por un cliente.                                           | Un nodo solicita el cambio de velocidad a otro nodo que controla el motor.                           |
| **Parámetros** | Valores de configuración que un nodo puede almacenar y que afectan su comportamiento.                    | No aplicable                        | Configuran comportamientos específicos de los nodos.                                                | Un nodo puede tener un parámetro que defina la velocidad máxima del robot.                          |
| **Acciones**   | Comunicación para tareas de larga duración, que permite feedback y cancelación.                          | Cliente-Servidor (con retroalimentación) | Permiten realizar tareas prolongadas, donde se necesita retroalimentación y posibilidad de cancelación. | Un nodo envía un objetivo a otro nodo para mover el robot, y recibe feedback sobre el progreso.     |

</div>

