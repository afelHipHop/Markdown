Universidad Distrital Francisco José de Caldas. Arenas - Ramirez - Rocha. Patrones 

***Abstract*- text**

Resumen- 

## I introducción: 

En este documento, se encontrará información acerca de cuatro patrones de diseño; dos creacionales (Builder y Singleton) y dos estructurales (Decorator y Adapter), se explicará cada patrón detalladamente, su diagrama de clases, como será su implementación y cuál fue la razón para escoger específicamente estos patrones en vez de los otros existentes en GOF. 

## II Patrones de diseño:

Un patrón de diseño es un conjunto de objetos y clases organizados de cierta forma que ayudan a resolver un problema recurrente en el diseño de un software de una forma limpia y reusable.

Según el libro [Design Patterns: Elements of Reusable Object-Oriented Software](https://sophia.javeriana.edu.co/~cbustaca/docencia/DSBP-2018-01/recursos/Erich%20Gamma,%20Richard%20Helm,%20Ralph%20Johnson,%20John%20M.%20Vlissides-Design%20Patterns_%20Elements%20of%20Reusable%20Object-Oriented%20Software%20%20-Addison-Wesley%20Professional%20(1994).pdf), a los patrones se los puede clasificar en tres categorías:

* Patrones Creacionales
* Patrones Estructurales
* Patrones de Comportamiento

(en este documento solo se explicaran los dos primeros)

## III Patrones Creacionales

los patrones creacionales buscan principalmente solucionar los problemas acerca de cómo crear instancias de las clases de nuestra aplicación, basicamente buscan en cierta forma "despreocupar" al sistema de como sus objetos son creados o compuestos. Existen cinco tipos de patrones creacionales y a pesar que se nombraran todos para que haya claridad, en este documento solo nos centraremos en los dos anteriormente mencionados. 

* Abstract Factory: permite trabajar con objetos de diferentes familias de manera que no se mezclen entre sí. De esa manera se consigue la el tipo de familia que se esté utilizando sea transparente.
* Builder: abstrae el proceso de creación de los objetos complejos, centralizandolo en pun punto.
* Factory Method: centraliza en una clase constructora la creación de objetos de un tipo determinado. Ocultando al invocante la necesidad de indicar un tipo u otro.
* Prototype: crea un objeto a partir de la clonación de un objeto ya existente.
* Singleton: garantiza que solo exista una instancia de un objeto y que la forma de acceder a dicha instancia sea general.

## III.I Patron Builder

Permite la creación de un objeto complejo, a partir de una variedad de partes que contribuyen individualmente a la creación y ensamblación del objeto mencionado. Hace uso de la frase "divide y conquistarás". Por otro lado, centraliza el proceso de creación en un único punto, de tal forma que el mismo proceso de construcción pueda crear representaciones diferentes.

Los objetos que dependen de un algoritmo tendrán que cambiar cuando el algoritmo cambia. Por lo tanto, los algoritmos que estén expuestos a dicho cambio deberían ser separados, permitiendo de esta manera reutilizar dichos algoritmos para crear diferentes representaciones. 

### ¿cuándo se debe usar este patrón?

se debe usar cuando sea necesario:

* Independizar el algoritmo de creación de un objeto complejo de las partes que constituyen el objeto y cómo se ensamblan entre ellas.
* Que el proceso de construcción permita distintas representaciones para el objeto construido, de manera dinámica.

Esta patrón debe utilizarse cuando el algoritmo para crear un objeto suele ser complejo e implica la interacción de otras partes independientes y una coreografía entre ellas para formar el ensamblaje. Por ejemplo: la construcción de un objeto Computadora, se compondrá de otros muchos objetos, como puede ser un objeto PlacaDeSonido, Procesador, PlacaDeVideo, Gabinete, Monitor, etc.

![uml builder](builder.jpg)

Producto: representa el objeto complejo a construir.
Builder: especifica una interface abstracta para la creación de las partes del Producto. Declara las operaciones necesarias para crear las partes de un objeto concreto.
ConcreteBuilder: implementa Builder y ensambla las partes que constituyen el objeto complejo.
Director: construye un objeto usando la interfaz Builder. Sólo debería ser necesario especificar su tipo y así poder reutilizar el mismo proceso para distintos tipos.

El Cliente crea el objeto Director y lo configura con el objeto Builder deseado.
El Director notifica al constructor cuándo una parte del Producto se debe construir.
El Builder maneja los requerimientos desde el Director y agrega partes al producto.
El Cliente recupera el Producto desde el constructor.

# Markdown

