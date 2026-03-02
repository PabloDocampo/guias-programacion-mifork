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

### La encapsulación busca agrupar en una misma unidad (la clase) tanto los datos como las operaciones que actúan sobre ellos. La idea es que el objeto controle ###su propio estado y que el exterior solo pueda interactuar con él mediante un conjunto limitado de operaciones. Esto permite que el estado interno esté ###protegido frente a usos incorrectos o inconsistentes.
### La ocultación de información complementa esta idea restringiendo el acceso directo a los atributos internos. De este modo, se evita que otras partes del   ###programa modifiquen el estado de un objeto de forma arbitraria. Entre sus ventajas destacan la reducción de errores, la posibilidad de cambiar la ###implementación interna sin afectar al resto del programa y la garantía de que el objeto mantiene sus invariantes internas.



## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### La interfaz pública de una clase es el conjunto de métodos accesibles desde fuera de ella. Representa la “cara visible” del objeto y define cómo puede interactuarse con él. 
### En Java, esta interfaz se expresa mediante los métodos declarados como public.
### La relación con la ocultación de información es directa: la interfaz pública actúa como filtro. El usuario de la clase solo puede acceder a lo que la interfaz permite, mientras que los detalles internos permanecen ocultos. Esto permite controlar qué operaciones son seguras y cómo debe manipularse el estado del objeto.



## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### La interfaz pública debe diseñarse con cuidado porque constituye un contrato con el resto del programa. Una vez que otras clases dependen de ella, cualquier cambio puede provocar errores o requerir modificaciones en múltiples partes del código. Por ello, una interfaz mal diseñada puede generar rigidez y dificultar la evolución del software.
### Cambiar la interfaz pública no suele ser fácil. Aunque técnicamente pueda modificarse, el impacto en el resto del sistema puede ser grande. Por eso se recomienda mantener la interfaz lo más estable posible y ocultar todo lo que no sea estrictamente necesario.



## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Las invariantes de clase son condiciones que deben cumplirse siempre para que el estado de un objeto sea válido. Por ejemplo, que un punto no tenga coordenadas inválidas o que un intervalo tenga siempre el extremo inferior menor que el superior. Estas condiciones deben mantenerse antes y después de cada operación pública.
### La ocultación de información ayuda porque impide que el estado interno sea modificado desde fuera sin control. Si solo los métodos de la clase pueden alterar los atributos, es posible garantizar que todas las modificaciones pasen por comprobaciones que mantengan las invariantes.



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

### La interfaz pública de esta clase está formada por el constructor y el método calcularDistanciaAOrigen. Los atributos x e y no forman parte de la interfaz pública porque están declarados como private. El modificador public indica que un elemento es accesible desde cualquier otra clase, mientras que private restringe el acceso exclusivamente a la propia clase.


## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### En Java, los modificadores public y private pueden aplicarse a clases (aunque solo a clases de nivel superior public o sin modificador) y a los miembros de una clase: atributos, métodos y constructores. Esto permite controlar la visibilidad tanto de la clase como de sus componentes internos.



## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Además de public y private, Java ofrece protected y el nivel por defecto (package-private). protected permite el acceso desde clases del mismo paquete y desde subclases, incluso si están en paquetes distintos. El nivel por defecto permite acceso solo dentro del mismo paquete.
### Otros lenguajes pueden tener sistemas de visibilidad distintos. Por ejemplo, C++ incluye public, private y protected, pero su semántica difiere ligeramente. Algunos lenguajes más dinámicos incluso carecen de mecanismos estrictos de ocultación.



## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Los miembros privados están ocultos para otras clases, pero no para otras instancias de la misma clase. Esto significa que un objeto puede acceder a los atributos privados de otro objeto si ambos son de la misma clase. Esta característica permite implementar métodos que comparan o combinan objetos del mismo tipo.

### public double calcularDistanciaAPunto(Punto otro) {
###    double dx = this.x - otro.x;
###    double dy = this.y - otro.y;
###    return Math.sqrt(dx * dx + dy * dy);
### }

### En este ejemplo, aunque x e y son privados, el método puede acceder a otro.x y otro.y porque ambos objetos pertenecen a la misma clase.

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Los métodos getter permiten obtener el valor de un atributo privado, mientras que los setter permiten modificarlo. Son una forma controlada de exponer el estado interno sin renunciar a la ocultación de información. Suelen seguir la convención getAtributo() y setAtributo(valor).

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### No. La “seguridad” en este contexto se refiere a la integridad del estado interno del objeto. La ocultación evita que el programa modifique atributos de forma incorrecta o inconsistente. No tiene relación con la seguridad informática o la protección frente a ataques externos.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Un miembro de instancia pertenece a cada objeto individual, mientras que un miembro de clase pertenece a la clase en sí y es compartido por todas las instancias. En Java, los miembros de clase se declaran con static.
### Ambos tipos de miembros pueden ocultarse mediante modificadores de visibilidad. Un atributo static private es accesible solo desde la propia clase.



## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta


## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta


## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta


## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta


## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta


## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta
