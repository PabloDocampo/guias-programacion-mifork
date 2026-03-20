<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### La encapsulación y la ocultación de información buscan que los detalles internos de una clase queden protegidos frente al exterior. La idea es que el objeto controle cómo se accede y modifica su estado, evitando que otras partes del programa dependan de su implementación interna. Esto permite que el objeto mantenga su coherencia y que los cambios internos no afecten al resto del sistema.
### Entre las ventajas de la ocultación de información se encuentran la reducción del acoplamiento entre módulos, la facilidad para modificar la implementación sin romper el código cliente y la mejora en la robustez del programa. También contribuye a que el código sea más fácil de mantener, ya que se limita el número de lugares donde pueden producirse errores relacionados con el estado interno.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### La interfaz pública de una clase es el conjunto de métodos y atributos accesibles desde fuera de ella. Representa aquello que un objeto ofrece al exterior como forma de interacción, sin exponer cómo están implementados internamente esos comportamientos. Es, por tanto, la “cara visible” del objeto.
### Esta interfaz se relaciona directamente con la ocultación de información porque permite separar lo que se puede usar de lo que se debe ocultar. Al mantener privados los detalles internos y exponer solo lo necesario, se garantiza que el usuario de la clase no dependa de su implementación, sino únicamente de su comportamiento observable.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Es importante diseñar con cuidado la interfaz pública porque una vez que otros módulos dependen de ella, cualquier cambio puede tener un impacto significativo en el resto del programa. La interfaz actúa como un contrato: si se modifica, se corre el riesgo de romper código que la utiliza. Por eso conviene pensar bien qué métodos deben ser públicos y cuáles no.
### Cambiar una interfaz pública no suele ser fácil, especialmente en proyectos grandes o con muchos módulos interconectados. Aunque técnicamente se pueda modificar, el coste de actualizar todo el código dependiente puede ser elevado, lo que hace que la estabilidad de la interfaz sea un objetivo importante.
 


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Las invariantes de clase son condiciones que deben cumplirse siempre para que un objeto se considere válido. Suelen referirse a restricciones sobre los valores de los atributos o sobre relaciones entre ellos. Por ejemplo, en una clase que representa un intervalo, la invariante podría ser que el extremo inferior sea menor o igual que el superior.
### La ocultación de información ayuda a mantener estas invariantes porque impide que el estado interno sea modificado libremente desde fuera. Al controlar el acceso mediante métodos, la clase puede verificar que cualquier cambio respete las condiciones necesarias para mantener su coherencia interna.



## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### public class Punto {
###    private double x;
###    private double y;

###    public Punto(double x, double y) {
###        this.x = x;
###        this.y = y;
###    }

###    public double calcularDistanciaAOrigen() {
###        return Math.sqrt(x * x + y * y);
###    }
### }
### La interfaz pública de esta clase está formada por el constructor y el método . Los atributos  e  no forman parte de la interfaz pública porque están declarados como privados. Esto significa que solo la propia clase puede acceder a ellos directamente.
### La palabra clave  indica que un elemento es accesible desde cualquier parte del programa, mientras que  limita el acceso exclusivamente a la clase donde se declara. Esto permite controlar qué partes de la clase se exponen y cuáles se mantienen ocultas.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### En Java, los modificadores public y private pueden aplicarse tanto a clases (aunque solo a clases de nivel superior en el caso de public) como a atributos, métodos y constructores. Esto permite controlar la visibilidad de cada uno de estos elementos de forma granular.
### El uso de estos modificadores permite definir claramente qué partes de una clase deben ser accesibles desde fuera y cuáles deben permanecer internas. De esta forma se refuerza la encapsulación y se evita que el código externo dependa de detalles que podrían cambiar.



## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Además de public y private, Java ofrece otros niveles de visibilidad: protected y el nivel por defecto (package-private). protected permite el acceso desde clases del mismo paquete y desde subclases, mientras que el nivel por defecto permite el acceso solo dentro del mismo paquete. Esto proporciona un control más fino sobre la accesibilidad.
### En otros lenguajes orientados a objetos pueden existir más niveles o variaciones. Por ejemplo, C++ incluye public, protected y private, pero su semántica difiere ligeramente. Algunos lenguajes incluso permiten visibilidades más específicas, como “solo lectura” o “solo escritura”.



## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Los miembros privados están ocultos para otras clases, pero no para otras instancias de la misma clase. Esto significa que un objeto puede acceder a los atributos privados de otro objeto de la misma clase, ya que ambos comparten el mismo contexto de definición.
### public double calcularDistanciaAPunto(Punto otro) {
###    double dx = this.x - otro.x;
###    double dy = this.y - otro.y;
###    return Math.sqrt(dx * dx + dy * dy);
### }
### Este comportamiento permite que los métodos de la clase trabajen con otras instancias sin necesidad de exponer sus atributos. La ocultación se aplica a nivel de clase, no de instancia, lo que facilita la implementación de operaciones entre objetos del mismo tipo

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Los métodos getter y setter son funciones que permiten acceder y modificar atributos privados de una clase. Un getter devuelve el valor de un atributo, mientras que un setter permite cambiarlo, normalmente realizando comprobaciones para mantener las invariantes de clase.
### Estos métodos son una forma controlada de exponer el estado interno sin permitir acceso directo a los atributos. Aunque puedan parecer equivalentes a hacer los atributos públicos, permiten añadir lógica adicional, como validaciones o actualizaciones relacionadas.



## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Cuando se dice que la ocultación de información mejora la “seguridad”, no se refiere a evitar ataques o hackeos. Se refiere a la seguridad en el sentido de robustez y fiabilidad del programa. Al impedir que el estado interno sea manipulado libremente, se reducen los errores y se mantiene la coherencia del objeto.
### Esta forma de seguridad es más cercana a la ingeniería del software que a la ciberseguridad. Su objetivo es evitar que el programa entre en estados inválidos o inconsistentes debido a un uso incorrecto de los objetos.



## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Un miembro de instancia pertenece a cada objeto individual, por lo que cada instancia tiene su propia copia. En cambio, un miembro de clase (declarado con static) pertenece a la clase en sí y es compartido por todas las instancias. Esto permite almacenar información común a todos los objetos.
### Los miembros de clase también pueden ocultarse mediante private. Esto es útil cuando se quiere mantener información global controlada únicamente por la propia clase, evitando accesos externos no deseados.





## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Tiene sentido que un constructor sea privado cuando no se desea permitir la creación directa de objetos desde fuera de la clase. Esto se utiliza en patrones como singleton o en clases que proporcionan métodos factoría para controlar cómo se crean las instancias.
### Al hacer el constructor privado, la clase puede garantizar que todas las instancias se creen siguiendo ciertas reglas o restricciones. Esto contribuye a mantener las invariantes y a evitar usos incorrectos.



## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### En Java, los miembros de clase se indican con la palabra clave static. Esto permite que existan variables compartidas entre todas las instancias. En la clase Punto, se podrían añadir miembros estáticos para registrar los valores máximos de x e y.
### public class Punto {
###    private static double maxX = Double.NEGATIVE_INFINITY;
###    private static double maxY = Double.NEGATIVE_INFINITY;

###    private double x;
###    private double y;

###    public Punto(double x, double y) {
###        this.x = x;
###        this.y = y;
###        if (x > maxX) maxX = x;
###        if (y > maxY) maxY = y;
###    }
### }
### Estos atributos estáticos permiten almacenar información global sobre todas las instancias creadas hasta el momento, sin necesidad de mantener estructuras externas.

## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### public static Punto crearRedondeado(double x, double y) {
###    return new Punto(Math.round(x), Math.round(y));
### }
### Este método factoría utiliza static porque no depende de ninguna instancia concreta. Su función es crear un nuevo Punto aplicando un redondeo previo a las coordenadas, lo que permite controlar la forma en que se generan los objetos.


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### public class Punto {
###    private double[] coords = new double[2];

###    public Punto(double x, double y) {
###        coords[0] = x;
###        coords[1] = y;
###    }

###    public double calcularDistanciaAOrigen() {
###        return Math.sqrt(coords[0] * coords[0] + coords[1] * coords[1]);
###    }
### }
### La interfaz pública no cambia, ya que los métodos siguen siendo los mismos. Sin embargo, la implementación interna se modifica para almacenar las coordenadas en un array. Esto demuestra cómo la ocultación de información permite cambiar la estructura interna sin afectar al código cliente.

## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Aunque un atributo tenga getter y setter públicos, no es recomendable declararlo público. Mantenerlo privado permite añadir validaciones o lógica adicional en el futuro sin romper la interfaz pública. Además, evita que el estado interno pueda ser modificado sin control.
### La convención más habitual es declarar los atributos como privados y proporcionar getters y setters solo cuando sean necesarios. Esto está relacionado con las invariantes de clase, ya que permite garantizar que cualquier cambio en el estado pase por un punto de control.



## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Una clase inmutable es aquella cuyo estado no puede cambiar después de ser creada. Esto significa que no tiene setters ni métodos que alteren sus atributos internos. En lugar de modificar el objeto, los métodos devuelven nuevas instancias con los cambios aplicados.
### Un método modificador es cualquier método que altera el estado interno del objeto. No siempre es un setter; puede ser un método más complejo que cambie varios atributos. Las clases inmutables tienen ventajas como la simplicidad, la ausencia de efectos secundarios y la facilidad para razonar sobre su comportamiento.



## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### No es recomendable incluir setters por defecto. Solo deben añadirse cuando realmente se necesite permitir la modificación del estado. Incluir setters innecesarios puede debilitar la encapsulación y hacer más difícil mantener las invariantes de clase.
### Diseñar una clase implica decidir qué operaciones deben estar permitidas y cuáles no. Si un atributo no debe cambiar después de la construcción, no tiene sentido proporcionar un setter.



## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### La clase String en Java es inmutable. Cada vez que se concatenan dos cadenas, se crea un nuevo objeto String. Esto puede ser ineficiente si se realizan muchas concatenaciones dentro de un bucle.
### Para operaciones repetidas de concatenación, se recomienda usar StringBuilder, que es mutable y permite construir cadenas de forma eficiente. Una vez terminada la construcción, se puede convertir a String.



## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### En POO, los objetos pueden compararse por identidad (si son el mismo objeto) o por contenido (si representan la misma información). En Java, el método equals sirve para comparar por contenido, aunque por defecto compara por identidad, ya que hereda la implementación de Object.
### Para comparar cadenas en Java, debe usarse equals, no ==. El operador == compara referencias, mientras que equals compara el contenido de las cadenas.

 

## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Las clases wrapper son clases que encapsulan tipos primitivos para tratarlos como objetos. En Java existen wrappers como Integer, Double o Boolean. La conversión entre primitivo y wrapper puede hacerse de forma automática gracias al autoboxing y unboxing.
### Los wrappers permiten almacenar valores primitivos en colecciones genéricas y utilizar métodos asociados a ellos. No todos los lenguajes tienen tipos primitivos separados; algunos tratan todos los valores como objetos y no necesitan wrappers.



## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Un tipo enumerado representa un conjunto fijo de valores posibles. En Java, un enumerado es una clase especial que permite definir constantes con comportamiento propio. Esto ofrece ventajas de encapsulación, ya que cada valor puede tener atributos y métodos privados.
### Los enumerados en Java permiten agrupar valores relacionados y evitar errores como usar valores no válidos. Además, su implementación como clases facilita añadir lógica interna sin exponer detalles innecesarios.



## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### public enum Mes {
###    ENERO(31, 1), FEBRERO(28, 2), MARZO(31, 3), ABRIL(30, 4),
###    MAYO(31, 5), JUNIO(30, 6), JULIO(31, 7), AGOSTO(31, 8),
###    SEPTIEMBRE(30, 9), OCTUBRE(31, 10), NOVIEMBRE(30, 11), DICIEMBRE(31, 12);

###    private int dias;
###    private int ordinal;

###    private Mes(int dias, int ordinal) {
###        this.dias = dias;
###        this.ordinal = ordinal;
###    }

###    public int getDias() { return dias; }
###    public int getOrdinal() { return ordinal; }
### }
### Este enumerado encapsula tanto el número de días como el orden del mes en el año. Cada instancia del enumerado es un objeto único y no modificable, lo que garantiza su consistencia.

## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### public boolean esDePrimavera(boolean norte) {
###    return norte ? (ordinal >= 3 && ordinal <= 5) : (ordinal >= 9 && ordinal <= 11);
### }

### public boolean esDeVerano(boolean norte) {
###    return norte ? (ordinal >= 6 && ordinal <= 8) : (ordinal == 12 || ordinal <= 2);
### }

### public boolean esDeOtono(boolean norte) {
###    return norte ? (ordinal >= 9 && ordinal <= 11) : (ordinal >= 3 && ordinal <= 5);
### }

### public boolean esDeInvierno(boolean norte) {
###    return norte ? (ordinal == 12 || ordinal <= 2) : (ordinal >= 6 && ordinal <= 8);
### }
### Estos métodos permiten determinar si un mes pertenece a una estación según el hemisferio. La lógica se basa en el ordinal del mes y en la inversión de estaciones entre hemisferios.
