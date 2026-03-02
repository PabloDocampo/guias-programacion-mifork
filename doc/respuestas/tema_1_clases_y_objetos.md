<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### 1. Abstracción : Consiste en resaltar lo esencial de un objeto y ocultar los detalles irrelevantes.Permite crear modelos conceptuales simples de entidades complejas.Ejemplo: una clase Coche expone métodos como arrancar() o frenar(), pero oculta cómo funciona internamente el motor.
### 2. Encapsulamiento : Agrupa datos (atributos) y comportamientos (métodos) dentro de una misma unidad: la clase . Protege el estado interno del objeto mediante niveles de acceso (privado, público, protegido). Evita modificaciones indebidas y facilita el mantenimiento.
### 3. Herencia : Permite que una clase (subclase) herede atributos y métodos de otra (superclase) . Favorece la reutilización de código y la creación de jerarquías lógicas . Ejemplo: Vehículo → Coche, Moto, Camión.
### 4. Polimorfismo : Habilidad de usar el mismo método con comportamientos distintos según el objeto que lo implemente . Permite escribir código más flexible y extensible . Ejemplo: el método mover() puede comportarse diferente en un Coche y en un Barco.



## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Java , Phyton , C++ y C#


## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Programación estructurada
### Es un paradigma que surgió para combatir el caos del código lleno de gotos y saltos incontrolados. Su idea central es organizar el programa en bloques lógicos y controlados, usando solo tres estructuras:
### • 	Secuencia: instrucciones que se ejecutan una tras otra.
### • 	Selección: decisiones (if, switch).
### • 	Iteración: repeticiones (for, while).
### En esencia:
### • 	Favorece código más legible, predecible y fácil de depurar.
### • 	Evita saltos arbitrarios.
### • 	Obliga a pensar en el flujo lógico del programa.
### Es como pasar de un laberinto lleno de puertas aleatorias a un pasillo con bifurcaciones claras.

### Programación modular
### La modularidad va un paso más allá de la estructurada. Aquí la idea es dividir el programa en módulos independientes, cada uno responsable de una tarea concreta.
### Sus principios clave:
### • 	Cada módulo tiene una responsabilidad clara.
### • 	Los módulos se comunican mediante interfaces bien definidas.
### • 	Puedes desarrollar, probar y mantener cada módulo por separado.
### • 	Facilita la reutilización: un módulo bien hecho sirve en otros programas.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### 1. Atributos (estado)
### • 	Representan las características o datos del objeto.
### • 	Describen cómo es en un momento dado.
### • 	Ejemplo: en un objeto Coche, los atributos pueden ser color, velocidad, marca.
### 2. Métodos (comportamiento)
### • 	Son las acciones que el objeto puede realizar o las operaciones que se pueden ejecutar sobre él.
### • 	Definen cómo se comporta y cómo interactúa con otros objetos.
### • 	Ejemplo: acelerar(), frenar(), encender().
### 3. Identidad
### • 	Es lo que permite distinguir un objeto de otro, incluso si tienen los mismos atributos.
### • 	Cada objeto ocupa un lugar único en memoria o tiene un identificador propio.
### • 	Ejemplo: dos coches idénticos en color y marca siguen siendo objetos distintos.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Clase
### - Es un molde, plantilla o definición que describe:
### - atributos (datos)
### - métodos (comportamiento)
### Objeto
### - Es una entidad concreta creada a partir de una clase.
### - Si la clase es la receta, el objeto es el pastel.
### Instancia
### - Es simplemente un objeto concreto de una clase.
### - “Instanciar” = crear un objeto.
### ¿Todos los lenguajes OO tienen clases?
### - No.
### - Ejemplos:
### - Java, C#, C++ → sí usan clases.
### - Python, Ruby → sí usan clases, pero permiten más flexibilidad.
### - JavaScript → originalmente era prototype-based (sin clases reales). Las “clases” actuales son azúcar sintáctico sobre prototipos.
### - Go → no tiene clases, pero sí métodos y composición.



## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Depende del lenguaje:
### - Java: objetos en el heap.
### - C++: pueden estar en stack, heap o global.
### - Python y C#: heap.
### La recolección de basura es un sistema automático que libera memoria de objetos que ya no se usan.





## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Un método es una función asociada a una clase.
### La sobrecarga consiste en definir varios métodos con el mismo nombre pero distintos parámetros.



## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### public class Punto {
###   int x;
###   int y;

### double calculaDistanciaAOrigen() {
###   return Math.sqrt(x * x + y * y);
###    }
### }

### Ejemplo de uso:

### public class Main {
###    public static void main(String[] args) {
###        Punto p = new Punto();
###        p.x = 3;
###        p.y = 4;

###        System.out.println(p.calculaDistanciaAOrigen()); // 5.0
###    }
### }

## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### El punto de entrada es:
### public static void main(String[] args)


### static indica que el método pertenece a la clase, no a un objeto.
### Se usa también en variables y otros métodos.
### static final define constantes.




## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Compilar:
### javac Main.java


### Ejecutar:
### java Main


### Java es compilado a bytecode, que ejecuta la JVM (Java Virtual Machine).
### Los .class contienen ese bytecode.



## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### new reserva memoria y llama al constructor.
### Un constructor inicializa el objeto.
### public class Empleado {
###    String dni;
###    String nombre;
###    String apellidos;

###    public Empleado(String dni, String nombre, String apellidos) {
###        this.dni = dni;
###        this.nombre = nombre;
###        this.apellidos = apellidos;
###    }
### }



## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### this es la referencia al objeto actual.
### public class Punto {
###    int x;
###    int y;

###    Punto(int x, int y) {
###        this.x = x;
###        this.y = y;
###    }
### }


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### double distanciaA(Punto otro) {
###    int dx = this.x - otro.x;
###    int dy = this.y - otro.y;
###    return Math.sqrt(dx * dx + dy * dy);
### }



## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### En Java:
### - Los objetos se pasan por valor, pero el valor es una referencia → modificar atributos afecta fuera.
### - Los primitivos (int, double, etc.) se pasan por valor real → no afectan fuera.



## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### toString () devuelve una representación en texto del objeto.
### @Override
### public String toString() {
###    return "(" + x + ", " + y + ")";
### }


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Parecido, pero un struct solo contiene datos.
### Le faltan:
### - métodos
### - encapsulación
### - constructores
### - herencia y polimorfismo

17. Emular Punto en C. ¿Qué pasa con this?
#include <math.h>

typedef struct {
    int x;
    int y;
} Punto;

double distanciaAOrigen(Punto* p) {
    return sqrt(p->x * p->x + p->y * p->y);
}


En C no existe this; se simula pasando un puntero al objeto.

Si quieres, puedo generarte un README.md completo, con índice, secciones y formato profesional para GitHub.



## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### #include <math.h>

### typedef struct {
###    int x;
###    int y;
### } Punto;

### double distanciaAOrigen(Punto* p) {
###    return sqrt(p->x * p->x + p->y * p->y);
### }

### En C no existe this; se simula pasando un puntero al objeto.
