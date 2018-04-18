Universidad Distrital Francisco José de Caldas. Arenas - Ramirez - Rocha. Patrones 

## integrantes:

* Hernan Arenas
* Andres Ramirez
* Kevin Rocha


## I introducción: 

En este documento, se encontrará información acerca de cuatro patrones de diseño; dos creacionales (Builder y Singleton) y dos estructurales (Decorator y Adapter), se explicará cada patrón detalladamente, su diagrama de clases, como será su implementación y cuál fue la razón para escoger específicamente estos patrones en vez de los otros existentes en GOF. 

## II Patrones de diseño:

Un patrón de diseño es un conjunto de objetos y clases organizados de cierta forma que ayudan a resolver un problema recurrente en el diseño de un software de una forma limpia y reusable.

Según el libro [Design Patterns: Elements of Reusable Object-Oriented Software](https://sophia.javeriana.edu.co/~cbustaca/docencia/DSBP-2018-01/recursos/Erich%20Gamma,%20Richard%20Helm,%20Ralph%20Johnson,%20John%20M.%20Vlissides-Design%20Patterns_%20Elements%20of%20Reusable%20Object-Oriented%20Software%20%20-Addison-Wesley%20Professional%20(1994).pdf), a los patrones se los puede clasificar en tres categorías:

* **Patrones Creacionales**
* **Patrones Estructurales**
* **Patrones de Comportamiento**

(en este documento solo se explicaran los dos primeros)

## III Patrones Creacionales

los patrones creacionales buscan principalmente solucionar los problemas acerca de cómo crear instancias de las clases de nuestra aplicación, basicamente buscan en cierta forma "despreocupar" al sistema de como sus objetos son creados o compuestos. Existen cinco tipos de patrones creacionales y a pesar que se nombrarán todos para que haya claridad, en este documento solo nos centraremos en los dos anteriormente mencionados. 

* **Abstract Factory:** permite trabajar con objetos de diferentes familias de manera que no se mezclen entre sí. De esa manera se consigue la el tipo de familia que se esté utilizando sea transparente.
* **Builder:** abstrae el proceso de creación de los objetos complejos, centralizandolo en pun punto.
* **Factory Method:** centraliza en una clase constructora la creación de objetos de un tipo determinado. Ocultando al invocante la necesidad de indicar un tipo u otro.
* **Prototype:** crea un objeto a partir de la clonación de un objeto ya existente.
* **Singleton:** garantiza que solo exista una instancia de un objeto y que la forma de acceder a dicha instancia sea general.

## III.I Patron Builder

Permite la creación de un objeto complejo, a partir de una variedad de partes que contribuyen individualmente a la creación y ensamblación del objeto mencionado. Hace uso de la frase "divide y conquistarás". Por otro lado, centraliza el proceso de creación en un único punto, de tal forma que el mismo proceso de construcción pueda crear representaciones diferentes.

Los objetos que dependen de un algoritmo tendrán que cambiar cuando el algoritmo cambia. Por lo tanto, los algoritmos que estén expuestos a dicho cambio deberían ser separados, permitiendo de esta manera reutilizar dichos algoritmos para crear diferentes representaciones. 

### ¿cuándo se debe usar este patrón?

se debe usar cuando sea necesario:

* Independizar el algoritmo de creación de un objeto complejo de las partes que constituyen el objeto y cómo se ensamblan entre ellas.
* Que el proceso de construcción permita distintas representaciones para el objeto construido, de manera dinámica.

Esta patrón debe utilizarse cuando el algoritmo para crear un objeto suele ser complejo e implica la interacción de otras partes independientes y una coreografía entre ellas para formar el ensamblaje. Por ejemplo: la construcción de un objeto Computadora, se compondrá de otros muchos objetos, como puede ser un objeto PlacaDeSonido, Procesador, PlacaDeVideo, Gabinete, Monitor, etc.

![uml builder](builder.jpg)

*Fig 1. Diagrama UML Builder*

* **Producto:** representa el objeto complejo a construir.
* **Builder:** especifica una interface abstracta para la creación de las partes del Producto. Declara las operaciones necesarias para crear las partes de un objeto concreto.
* **ConcreteBuilder:** implementa Builder y ensambla las partes que constituyen el objeto complejo.
* **Director:** construye un objeto usando la interfaz Builder. Sólo debería ser necesario especificar su tipo y así poder reutilizar el mismo proceso para distintos tipos.

El Cliente crea el objeto Director y lo configura con el objeto Builder deseado.

El Director notifica al constructor cuándo una parte del Producto se debe construir.

El Builder maneja los requerimientos desde el Director y agrega partes al producto.

El Cliente recupera el Producto desde el constructor.

### ¿Por qué se escogió?

El patrón builder es un patrón usado muy frecuentemente en la programación, por esto se consideró pertinente, enfatizar en su explicación con respecto a los demás patrones. 

a continuación se verá un ejemplo de como utilizar builder:

El objetivo del ejemplo es poder crear un objeto Auto (este sería nuestro producto). El auto se compondrá de varios atributos que lo componen: motor, marca, modelo y cantidad de puertas. En nuestro ejemplo, el auto no se compone de muchos objetos complejos. De hecho, se compone de sólo 4 objetos relativamente sencillos. Esto es para poder hacer entendible la propuesta del Builder y no perderse en los objetos que lo componen. Queda en la imaginación del lector la posibilidad de trabajar con ejemplos más complejos. Yo particularmente usé mucho este patrón cuando trabajé con archvios.

![builder1](codbuil1.jpg)

![builder 2](codbuil2.jpg)

Siguiendo con nuestro ejemplo, definimos nuestro Builder llamado AutoBuilder. El Builder define al menos dos cosas: un método para devolver el Producto (el auto en nuestro caso) y los métodos necesarios para la construcción del mismo.

![builder 3](codbuil3.jpg)

Serán los ConcreteBuilders los encargados de colocarle la lógica de construcción de cada Auto en particular. En nuestro caso, tendremos dos ConcreteBuilder: FiatBuildery FordBuilder. Recordemos que, en nuestro ejemplo, son clases que construyen objetos muy sencillos con datos hardcodeados para facilitar el aprendijaze del patrón en sí.

![builder 4](codbuil4.jpg)

![builder 5](codbuil5.jpg)

Por último, realizaremos el Director. Lo primero que debe hacerse con esta clase es enviarle el tipo de auto que se busca construir (Ford, Fiat, etc). Luego, al llamar al método constructAuto(), la construcción se realizará de manera automática. 

![builder 6](codbuil6.jpg)

la vista desde el cliente sería:

![builder 7](codbuil7.jpg)

## III.II Patron Singleton 

La idea del patrón Singleton es proveer un mecanismo para limitar el número de instancias de una clase. Por lo tanto el mismo objeto es siempre compartido por distintas partes del código. Puede ser visto como una solución más elegante para una variable global porque los datos son abstraídos por detrás de la interfaz que publica la clase singleton.

Dicho de otra manera, esta patrón busca garantizar que una clase sólo tenga una instancia y proporcionar un punto de acceso global a ella.

### ¿cuándo se debe usar este patrón?

* Debe haber exactamente una instancia de una clase y deba ser accesible a los clientes desde un punto de acceso conocido.
* Se requiere de un acceso estandarizado y conocido públicamente.

Sus usos más comunes son clases que representan objetos unívocos. Por ejemplo, si hay un servidor que necesita ser representado mediante un objeto, este debería ser único, es decir, debería existir una sola instancia y el resto de las clases deberían de comunicarse con el mismo servidor. Un Calendario, por ejemplo, también es único para todos.

No debe utilizarse cuando una clase esta representando a un objeto que no es único, por ejemplo, la clase Persona no debería ser Singleton, ya que representa a una persona real y cada persona tiene su propio nombre, edad, domicilio, DNI, etc.
 
![uml singleton](singleton.jpg)

*Firg 2. Estructura Singleton tomado de la app de GoF** 

### **Interpretación:** 

Crear una clase Singleton con una instancia estática y un constructor privado. Proviene un método estático para permitir solamente el acceso a la instancia. 

### **Singletonitis:** 

Debido a que Singleton es probablemente el patrón más sencillo del GoF, muchas veces las personas abusan de su uso y ponen el patrón donde es innecesario, a este uso indebido se le conoce como Singletonitis. 

acontinuación se mostrará un ejemplo de como implementar singleton:

Este patrón es ideal para aquellas clases que representan objetos únicos. Por ejemplo, un instituto educativo es un objeto único. No deberíamos crear muchas instancias de esta clase ya que al hacer esto estaríamos diciendo que hay varios institutos educativos. Caso contrario serían los alumnos que asisten a dicho instituto. Debería haber un objeto por cada uno de los alumnos, ya que todos ellos tienen propiedades distintivas, desde el nombre hasta el documento de identidad. Pero todos los alumnos deberían comunicarse con el mismo instituto.

Entonces, haremos que el instituto aplique el patrón Singleton:

![singleton1](codsing1.jpg)

Para llamar al instituto debemos hacer lo siguiente:

![singleton2](codsing2.jpg)

Bien, veamos ahora este mismo ejemplo, con una pequeña modificación: vamos a agregarle un atributo a la clase InstitutoEducativo y veremos como se comporta a lo largo de las distintas llamadas al método getInstance().

![singleton3](codsing3.jpg)

Y, el main, que representa al cliente que necesita utilizar esta clase:

![singleton4](codsing4.jpg)

### Otros temas a considerar.
  
Como vimos, el Singleton es un patrón sencillo para aplicar. Solo requiere de unos pequeños cambios a una clase. Sin embargo, debemos considerar un tema importante con respecto a este patrón: ¿que pasa si dos hilos del programa llaman (la primera vez) al método getInstance() al mismo tiempo? Bueno aqui podriamos tener un problema, ya que existe la remota posibilidad de que se logre crear dos instancias de la clase, en vez de una como quisieramos. La solución más sencilla es realizar un pequeño cambio:

![singleton5](codsing5.jpg)

### ¿Por qué se escogió?

El patrón singleton es uno de los patrones creacionales más sencillos, pero también es uno a de los que más se puede sacar provecho si se implementa bien, por esta razón, se decidió profundizar en el por encima de los otros.

## IV Patrones Estructurales

Los patrones estructurales se enfocan en como las clases y objetos se componen para formar estructuras mayores, los patrones estructurales describen como las estructuras compuestas por clases crecen para crear nuevas funcionalidades de manera de agregar a la estructura flexibilidad y que la misma pueda cambiar en tiempo de ejecución lo cual es imposible con una composición de clases estáticas a pesar que se nombrarán todos para que haya claridad, en este documento solo nos centraremos en los dos anteriormente mencionados

estos patrones estan conformados por:

* **Adapter**
* **Bridge**
* **Composite**
* **Decorator**
* **Facade**
* **Flyweight**
* **Proxy**

 ## IV.I Decorator
 
 Por definición la funcionalidad de este patrón se expresa como:
 
“responde a la necesidad de añadir dinámicamente funcionalidad a un Objeto. Esto nos permite no tener que crear sucesivas clases que hereden de la primera incorporando la nueva funcionalidad, sino otras que la implementan y se asocian a la primera.”

Un ejemplo de cómo debería expresarse la funcionalidad de este patrón mediante un diagrama en UML es: 

 ![uml decorator](decorator.jpg)
 
 *Fig 3. Design Patterns: Elements of Reusable Object-Oriented Software*

* **Componente**: Se quiere agregar o quitar dinámicamente la funcionalidad de un objeto.
* **ComponenteConcreto:** Se quiere agregar o quitar dinámicamente la funcionalidad de un objeto.
* **Decorator:** Se quiere agregar o quitar dinámicamente la funcionalidad de un objeto.
* **DecoradorConcreto:** Se quiere agregar o quitar dinámicamente la funcionalidad de un objeto.

### ¿cuándo se debe usar este patrón?

•	necesitamos añadir funcionalidades a una clase de forma dinámica, evitando las jerarquías de clases que se tienen construir en tiempo de compilación.
•	Hay una necesidad de extender la funcionalidad de una clase, pero no hay razones para extenderlo a través de la herencia.
•	Se quiere agregar o quitar dinámicamente la funcionalidad de un objeto.

Ejemplo práctico:

Imaginemos que vendemos automóviles y el cliente puede opcionalmente adicionar ciertos componentes (aire acondicionado, mp3 player, etc). Por cada componente que se adiciona, el precio varía.
 
 ![decorator1](coddec1.jpg)
 
 *Fig 3. Diagrama UML Decorator*
 
Bien, hasta aquí clases comunes de negocio: una interface que implementa la clase Auto y dos tipos de Auto (Ford y Fiat). Ahora veremos en que consiste el Decorator y los decoradores:
 
 ![decorator2](coddec2.jpg)

 ![decorator3](coddec3.jpg)

 ![decorator4](coddec4.jpg)

 ![decorator5](coddec5.jpg)

![decorator6](coddec6.jpg)

Veremos cómo funciona desde el punto de vista del cliente:
 
![decorator7](coddec7.jpg)

## IV.II Adapter

Según la definición es patrón adapter se define como:

“Se utiliza para transformar una interfaz en otra, de tal modo que una clase que no pueda utilizar la primera haga uso de ella a través de la segunda.”

Es conocido como Wrapper (al patrón Decorator también se lo llama Wrapper, con lo cual es nombre Wrapper muchas veces se presta a confusión).

Una clase Adapter implementa un interfaz que conoce a sus clientes y proporciona acceso a una instancia de una clase que no conoce a sus clientes, es decir convierte la interfaz de una clase en una interfaz que el cliente espera. Un objeto Adapter proporciona la funcionalidad prometida por un interfaz sin tener que conocer que clase es utilizada para implementar ese interfaz. Permite trabajar juntas a dos clases con interfaces incompatibles.

Un ejemplo de como debe ir representado el patrón Adapter mediante un diagrama UML es:

![uml adapter](adapter.jpg)
 
*Fig 4. Diagrama UML Adapter*

* **Target:** Define la interfaz específica del dominio que Cliente usa.
* **Cliente:** Colabora con la conformación de objetos para la interfaz Target.
* **Adaptado:** Define una interfaz existente que necesita adaptarse.
* **Adapter:** adapta la interfaz de Adapte a la interfaz Target.
•	El Cliente llama a las operaciones sobre una instancia Adapter. De hecho, el adaptador llama a las operaciones de Adapte que llevan a cabo el pedido.

### ¿Cuándo se debe usar este patrón?

•	Se quiere utilizar una clase que llame a un método a través de una interface, pero se busca utilizarlo con una clase que no implementa esa interface.
•	Se busca determinar dinámicamente que métodos de otros objetos llama un objeto.
•	No se quiere que el objeto llamado tenga conocimientos de la otra clase de objetos.

Ejemplo práctico:

Vamos a plantear el siguiente escenario: nuestro código tiene una clase Persona (la llamamos PersonaVieja) que se utiliza a lo largo de todo el código y hemos importado un API que también necesita trabajar con una clase Persona (la llamamos PersonaNueva), que si bien son bastante similares tienen ciertas diferencias:

Nosotros trabajamos con los atributos nombre, apellido y fecha de nacimiento.

Sin embargo, la PersonaNueva tiene un solo atributo nombre (que es el nombre y apellido de la persona en cuestión) y la edad actual, en vez de la fecha de nacimiento.

Para esta situación lo ideal es utilizar el Adapter. Para ello primero crearemos las 2 clases de Persona y sus correspondientes interfaces.
 
![adapter1](codada1.jpg)

![adapter2](codada2.jpg)

![adapter3](codada3.jpg)

![adapter4](codada4.jpg) 
 
Ahora crearemos al Adapter.

![adapter5](codada5.jpg)
 
Y se utiliza de esta manera:

![adapter6](codada6.jpg)

## Referencias

* https://migranitodejava.blogspot.com.co/
* http://blog.koalite.com/2016/12/los-patrones-de-diseno-hoy-patrones-estructurales/
* https://highscalability.wordpress.com/2010/04/12/patrones%C2%A0estructurales/
* Aplicacion Mobil de GoF
* http://www.cristalab.com/tutoriales/patrones-de-diseno
* http://lineadecodigo.com/patrones/patrones-creacionales/
