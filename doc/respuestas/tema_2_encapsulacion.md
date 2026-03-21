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

### La encapsulación busca agrupar datos y operaciones relacionadas dentro de una misma unidad lógica: la clase. La ocultación de información, por su parte, pretende restringir el acceso directo a los detalles internos de esa clase, exponiendo únicamente lo necesario para su uso correcto. Ambas ideas trabajan juntas para que el objeto controle cómo se manipulan sus propios datos.
### Entre las ventajas de la ocultación de información se encuentra la posibilidad de evitar estados inconsistentes, ya que solo los métodos autorizados pueden modificar los atributos internos. También facilita el mantenimiento del código, porque los cambios internos no afectan a quienes usan la clase mientras la interfaz pública se mantenga estable. Además, mejora la modularidad y reduce el acoplamiento entre componentes.


## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### La interfaz pública de una clase es el conjunto de métodos y atributos accesibles desde fuera de ella. Representa aquello que otros programadores o clases pueden utilizar para interactuar con el objeto, sin necesidad de conocer cómo está implementado internamente. Es, en esencia, el “contrato” que la clase ofrece al exterior.
### La ocultación de información se apoya precisamente en esta interfaz pública: se decide qué se expone y qué se mantiene privado. Gracias a esta separación, la implementación interna puede cambiar sin afectar a quienes usan la clase, siempre que la interfaz pública permanezca estable. Esto permite un diseño más robusto y flexible.



## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Diseñar la interfaz pública requiere cuidado porque es la parte de la clase que otros componentes del programa utilizarán. Una interfaz mal diseñada puede obligar a exponer detalles innecesarios, dificultar el uso correcto de la clase o permitir modificaciones que rompan sus invariantes internas. Además, una interfaz confusa o demasiado amplia aumenta el riesgo de errores.
### Cambiar la interfaz pública no suele ser sencillo, especialmente en proyectos grandes. Cualquier modificación puede afectar a múltiples módulos que dependan de ella, obligando a revisar y actualizar gran parte del código. Por eso se recomienda mantener una interfaz estable y bien pensada desde el principio.


## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Las invariantes de clase son condiciones que deben cumplirse siempre para que un objeto sea válido. Por ejemplo, en una clase que representa una cuenta bancaria, una invariante podría ser que el saldo nunca sea negativo. Estas condiciones deben mantenerse antes y después de cada operación pública de la clase.
### La ocultación de información ayuda porque impide que código externo modifique directamente los atributos internos, lo que podría violar esas invariantes. Al obligar a que toda modificación pase por métodos controlados, la clase puede verificar y garantizar que sus reglas internas se respetan en todo momento.


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
### La interfaz pública de esta clase está formada por el constructor  y el método . Estos son los elementos accesibles desde fuera de la clase y que permiten crear y utilizar objetos  sin conocer cómo se almacenan internamente las coordenadas.
### La palabra clave  indica que un miembro es accesible desde cualquier otra clase. En cambio,  restringe el acceso únicamente a la propia clase, impidiendo que otras clases manipulen directamente esos atributos. Esto permite proteger la integridad del objeto.

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### En Java, los modificadores  y  pueden aplicarse tanto a clases (aunque solo a clases de nivel superior se les permite ) como a miembros de clase: atributos, métodos y constructores. Estos modificadores determinan el nivel de visibilidad y acceso permitido desde otras clases.
### En el caso de los atributos y métodos,  es el más restrictivo y se utiliza para implementar la ocultación de información.  se usa para definir la interfaz pública de la clase. También pueden aplicarse a constructores para controlar cómo se crean los objetos.


## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Además de  y , muchos lenguajes orientados a objetos incluyen niveles intermedios de visibilidad. En Java existen  y el nivel por defecto (package-private), que permiten distintos grados de acceso según el paquete o la jerarquía de herencia. Esto ofrece un control más fino sobre qué se expone y a quién.
### Otros lenguajes, como C++, incluyen visibilidades similares (, , ) pero con reglas ligeramente distintas. Algunos lenguajes más modernos incorporan incluso niveles adicionales o mecanismos más flexibles para controlar el acceso, adaptándose a diferentes estilos de diseño.


## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Los miembros privados están ocultos para otras clases, pero no para otras instancias de la misma clase. Esto significa que un objeto puede acceder a los atributos privados de otro objeto si ambos pertenecen a la misma clase. Esta característica permite implementar métodos que comparen o combinen información entre objetos sin exponer sus detalles internos.
### Por ejemplo:
### public double calcularDistanciaAPunto(Punto otro) {
###    double dx = this.x - otro.x;  // acceso permitido
###    double dy = this.y - otro.y;
###    return Math.sqrt(dx * dx + dy * dy);
### }
### Aunque  e  son privados, un objeto  puede acceder a los atributos privados de otro . Esto no viola la ocultación de información, ya que sigue siendo la propia clase quien controla el acceso.

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Los métodos "getter" y "setter" son métodos públicos utilizados para acceder y modificar atributos privados de una clase. Un getter devuelve el valor de un atributo, mientras que un setter permite cambiarlo de forma controlada. Su uso permite mantener la ocultación de información sin renunciar a la posibilidad de consultar o actualizar los datos internos.
### Además, los setters pueden incluir validaciones que garanticen que las invariantes de clase no se rompen. Por ejemplo, un setter podría impedir que se asigne un valor negativo a un atributo que debe ser siempre positivo. Esto ofrece un mayor control que exponer directamente los atributos.


## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Cuando se dice que la ocultación de información mejora la “seguridad” del programa, no se refiere a seguridad informática en el sentido de evitar ataques o hackeos. Más bien se refiere a la seguridad del diseño del software, es decir, a evitar usos incorrectos o inconsistentes de los objetos por parte de otras partes del programa.
### La ocultación ayuda a que los objetos mantengan un estado válido y reduce la probabilidad de errores lógicos. Aunque no protege contra ataques externos, sí contribuye a que el código sea más robusto y menos propenso a fallos.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Un miembro de instancia pertenece a cada objeto individual: cada instancia tiene su propia copia del atributo. En cambio, un miembro de clase (marcado con ) pertenece a la clase en sí, por lo que existe una única copia compartida por todas las instancias. Esto permite almacenar información común a todos los objetos.
### Los miembros de clase también pueden ocultarse utilizando . De hecho, es habitual hacerlo cuando se desea controlar el acceso mediante métodos estáticos públicos. La ocultación funciona igual que con los miembros de instancia.


## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Sí, tiene sentido en ciertos patrones de diseño. Un constructor privado impide que se creen objetos directamente desde fuera de la clase. Esto permite controlar completamente cómo se instancian los objetos, obligando a usar métodos factoría o implementando patrones como Singleton.
### Este enfoque puede ser útil cuando se desea validar parámetros, reutilizar instancias existentes o limitar la creación de objetos. Aunque no es lo más habitual, es una herramienta valiosa en situaciones específicas.



## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Los miembros de clase se indican con la palabra clave . Esto hace que el atributo o método pertenezca a la clase en lugar de a cada instancia. Para almacenar los valores máximos de  e  creados hasta el momento, se podría hacer lo siguiente:
### public class Punto {
###    private double x;
###    private double y;

###    private static double maxX = Double.NEGATIVE_INFINITY;
###    private static double maxY = Double.NEGATIVE_INFINITY;

###    public Punto(double x, double y) {
###        this.x = x;
###        this.y = y;
###        if (x > maxX) maxX = x;
###        if (y > maxY) maxY = y;
###    }

###    public static double getMaxX() { return maxX; }
###    public static double getMaxY() { return maxY; }
### }
### Estos atributos estáticos se actualizan cada vez que se crea un nuevo punto.


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### public static Punto crearRedondeado(double x, double y) {
###    return new Punto(Math.round(x), Math.round(y));
### }

### Sí, se utiliza  porque un método factoría pertenece a la clase y no a una instancia concreta. Su función es crear objetos, por lo que no necesita un objeto previo para ser invocado.

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

### La interfaz pública no cambia, ya que el constructor y los métodos siguen siendo los mismos. Solo se ha modificado la representación interna, demostrando la utilidad de la ocultación de información.

## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Aunque un atributo tenga getter y setter, declararlo público elimina la posibilidad de controlar su modificación. Un setter puede validar valores, registrar cambios o mantener invariantes, mientras que un atributo público puede ser modificado sin restricciones. Por eso no se recomienda exponer atributos directamente.
### La convención habitual en Java es declarar todos los atributos como privados y proporcionar getters y setters solo cuando sean necesarios. Esto está directamente relacionado con las invariantes de clase, ya que permite garantizar que los valores internos siempre sean válidos.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Una clase inmutable es aquella cuyo estado no puede cambiar después de ser creada. Todos sus atributos son privados y no existen métodos que los modifiquen. Para “cambiar” un objeto inmutable, se crea uno nuevo con los valores deseados. Un ejemplo clásico es  en Java.
### Un método modificador es cualquier método que cambia el estado interno del objeto. Aunque un setter es un tipo de método modificador, no todos los modificadores son setters; algunos pueden realizar cálculos complejos o actualizar varios atributos a la vez. En una clase inmutable, simplemente no existen métodos modificadores.
### Las clases inmutables tienen ventajas como mayor simplicidad, seguridad frente a errores y facilidad para trabajar en entornos concurrentes. Al no cambiar su estado, son más predecibles y seguras.


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### No es recomendable incluir setters por defecto. Solo deben añadirse cuando realmente se necesite permitir la modificación del atributo. Incluir setters indiscriminadamente puede romper invariantes, exponer detalles internos y dificultar el mantenimiento del código.
### En muchos casos, es preferible que los objetos sean inmutables o que solo permitan modificaciones controladas mediante métodos específicos que mantengan la coherencia interna. La ausencia de setters suele indicar un diseño más robusto.


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### La clase  en Java es inmutable. Cada vez que se concatena una cadena con otra, no se modifica la original, sino que se crea un nuevo objeto  con el resultado. Esto puede ser costoso si se realizan muchas concatenaciones en un bucle.
### Cuando se necesita construir una cadena muy larga mediante múltiples operaciones, se recomienda utilizar  o . Estas clases son mutables y permiten modificar la cadena sin crear objetos intermedios, lo que mejora significativamente el rendimiento.


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### En POO, los objetos pueden compararse por identidad (si son el mismo objeto en memoria) o por contenido (si representan la misma información). En Java, el operador  compara identidad, mientras que el método  compara contenido, siempre que la clase lo haya sobrescrito adecuadamente.
### Por defecto,  en Java se comporta como , es decir, compara referencias. Para comparar cadenas, debe usarse , ya que  sobrescribe este método para comparar el contenido textual. Usar  con cadenas puede dar resultados incorrectos.


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Las clases wrapper son clases que encapsulan tipos primitivos para tratarlos como objetos. En Java existen wrappers como ,  o . Permiten almacenar valores primitivos en colecciones genéricas o utilizar métodos asociados a esos valores. Java realiza conversión automática entre primitivos y wrappers (autoboxing y unboxing).
### Las ventajas incluyen la posibilidad de usar tipos primitivos en contextos donde solo se aceptan objetos y disponer de métodos útiles asociados al valor. No todos los lenguajes necesitan wrappers, ya que algunos no distinguen entre tipos primitivos y objetos, como Python.


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Un tipo enumerado representa un conjunto finito y fijo de valores posibles. En Java, un  es realmente una clase especial que define instancias únicas y predefinidas. Cada valor del enumerado es un objeto de esa clase.
### Los enumerados en Java permiten encapsular atributos y métodos, igual que una clase normal. Esto permite asociar comportamiento y datos a cada valor del enumerado, manteniendo la seguridad y claridad del diseño. Además, evitan errores como usar valores no válidos.



## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### public enum Mes {
###    ENERO(31, 1),
###    FEBRERO(28, 2),
###    MARZO(31, 3),
###    ABRIL(30, 4),
###    MAYO(31, 5),
###    JUNIO(30, 6),
###    JULIO(31, 7),
###    AGOSTO(31, 8),
###    SEPTIEMBRE(30, 9),
###    OCTUBRE(31, 10),
###    NOVIEMBRE(30, 11),
###    DICIEMBRE(31, 12);

###    private int dias;
###    private int numeroMes;

###    private Mes(int dias, int numeroMes) {
###        this.dias = dias;
###        this.numeroMes = numeroMes;
###    }

###    public int getDias() { return dias; }
###    public int getNumeroMes() { return numeroMes; }
### }


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### public boolean esDePrimavera(boolean enHemisferioNorte) {
###    if (enHemisferioNorte)
###        return this == MARZO || this == ABRIL || this == MAYO;
###    else
###        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
### }

### public boolean esDeVerano(boolean enHemisferioNorte) {
###    if (enHemisferioNorte)
###        return this == JUNIO || this == JULIO || this == AGOSTO;
###    else
###        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
### }

### public boolean esDeOtono(boolean enHemisferioNorte) {
###    if (enHemisferioNorte)
###        return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
###    else
###        return this == MARZO || this == ABRIL || this == MAYO;
### }

### public boolean esDeInvierno(boolean enHemisferioNorte) {
###    if (enHemisferioNorte)
###        return this == DICIEMBRE || this == ENERO || this == FEBRERO;
###    else
###        return this == JUNIO || this == JULIO || this == AGOSTO;
### }
