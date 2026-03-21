<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### En C, al no existir excepciones, es habitual indicar errores mediante valores especiales de retorno. Por ejemplo, si se implementa una función  que solo admite números positivos, se puede devolver un valor imposible (como ) para señalar el error. El código llamador debe comprobar explícitamente ese valor antes de usar el resultado, lo que obliga a una disciplina estricta por parte del programador.
### double raiz(double x) {
###    if (x < 0) return -1.0;  // señal de error
###    return sqrt(x);
### }
### Otra opción consiste en usar un parámetro adicional por referencia para indicar si ha ocurrido un error. De esta forma, el valor devuelto puede ser el resultado real, mientras que el parámetro extra informa del estado de la operación. Este enfoque separa el resultado del indicador de error, pero sigue requiriendo que el llamador recuerde comprobarlo
### double raiz(double x, int* error) {
###    if (x < 0) {
###        *error = 1;
###        return 0.0;
###    }
###    *error = 0;
###    return sqrt(x);
### }

## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Una excepción es un mecanismo que permite interrumpir el flujo normal de ejecución cuando ocurre una situación anómala o inesperada. En lugar de devolver códigos de error, una función puede “lanzar” una excepción que será gestionada por un bloque especializado. Esto permite separar el código que realiza la operación del código que maneja los errores.
### El objetivo principal es mejorar la claridad y robustez del programa. Las excepciones permiten que los errores se propaguen automáticamente hasta un punto donde puedan ser tratados adecuadamente, evitando comprobaciones constantes en cada llamada. Además, facilitan la escritura de código más limpio y centrado en la lógica principal.


## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### public class Calculadora {
###    public static double raiz(double x) {
###        if (x < 0) {
###            throw new IllegalArgumentException("No se puede calcular la raíz de un número negativo");
###        }
###        return Math.sqrt(x);
###    }

###    public static void main(String[] args) {
###        try {
###            double r = Calculadora.raiz(-4);
###            System.out.println("Resultado: " + r);
###        } catch (IllegalArgumentException e) {
###            System.out.println("Error: " + e.getMessage());
###        }
###    }
### }
### En este ejemplo, la función  lanza una excepción cuando recibe un valor negativo. El método  contiene un bloque  que captura la excepción y muestra un mensaje adecuado. De esta forma, el control del error se realiza desde fuera de la función, igual que en el ejemplo en C, pero con un mecanismo más estructurado.

## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Lanzar una excepción significa interrumpir la ejecución normal de un método mediante la instrucción . Capturar o controlar una excepción consiste en interceptarla mediante un bloque  y ejecutar un código alternativo. Si una excepción no se captura en un método, se propaga hacia arriba en la pila de llamadas, buscando un manejador adecuado.
### Durante la propagación, cada función que no captura la excepción se abandona inmediatamente, sin reanudarse después. Esto implica que el flujo normal no continúa desde el punto donde ocurrió el error. En el ejemplo de la raíz, si  lanza una excepción y  no la capturara, la excepción seguiría subiendo hasta terminar el programa.


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### La propagación natural de excepciones evita la necesidad de comprobar manualmente códigos de error en cada llamada, como ocurre en C. Esto reduce la cantidad de código repetitivo y disminuye la probabilidad de que el programador olvide verificar un error. Además, permite que los errores se manejen en un punto centralizado, mejorando la claridad del programa.
### Otra ventaja es que la pila se desenrolla automáticamente, liberando recursos y abandonando funciones de forma ordenada. En C, este proceso debe gestionarse manualmente, lo que puede resultar complejo y propenso a errores. Las excepciones proporcionan un mecanismo más seguro y estructurado para manejar situaciones anómalas.



## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### En orientación a objetos, las excepciones suelen representarse como objetos. Esto permite encapsular información relevante sobre el error, como un mensaje descriptivo, la causa original o datos adicionales. Al tratarse de objetos, pueden heredarse y especializarse, creando jerarquías de excepciones adaptadas a distintos tipos de problemas.
### La encapsulación permite que el código llamador reciba información detallada sin necesidad de conocer cómo se generó el error. Además, se pueden crear excepciones personalizadas que representen situaciones específicas de una aplicación, mejorando la claridad y expresividad del código.


## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Un objeto excepción suele incluir un mensaje descriptivo que explica la causa del error. También puede contener la pila de llamadas en el momento en que ocurrió la excepción, lo que facilita enormemente la depuración. Esta información es muy valiosa cuando se llega al manejador, ya que permite comprender el contexto exacto del fallo.
### Comparado con C, donde solo se dispone de códigos de error o valores especiales, las excepciones en Java proporcionan un nivel de detalle mucho mayor. Esto permite diagnosticar problemas de forma más rápida y precisa, especialmente en programas complejos.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### En Java, un bloque  puede ir seguido de varios bloques , cada uno destinado a capturar un tipo específico de excepción. Esto permite manejar de forma diferenciada distintos tipos de errores que puedan ocurrir dentro del mismo bloque . El orden de los  es importante, ya que se evalúan de arriba abajo.
### Solo se ejecuta un bloque : el primero cuyo tipo coincida con la excepción lanzada. Una vez ejecutado ese bloque, los demás se ignoran. Esto permite un control preciso y estructurado de los errores.


## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### El bloque  se utiliza para garantizar que cierto código se ejecute siempre, independientemente de si ocurre o no una excepción. Esto es especialmente útil para liberar recursos como ficheros, conexiones o memoria. Incluso si se lanza una excepción y se propaga, el bloque  se ejecutará antes de continuar.
### try {
###    abrirFichero();
### } catch (IOException e) {
###    System.out.println("Error al abrir el fichero");
### } finally {
###    cerrarFichero();
### }
### También puede usarse sin bloque , cuando no interesa capturar la excepción pero sí asegurar la liberación de recursos:
### try {
###    abrirFichero();
### } finally {
###    cerrarFichero();
### }

## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta


## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta

