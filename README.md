# C

## References
* [C Reference](https://cppreference.com/w/c.html)
* [C Reference Language](https://cppreference.com/w/c/language.html)

## Basic Concepts
### C Program
Un programa en C es una secuencia de archivos de texto, típicamente archivos header y source. Estos programas pasan por una *translation* para convertirse en un programa ejecutable, y este se ejecuta cuando el Sistema Operativo llama a su *main function*, a menos que el programa sea el propio SO o algún otro programa "independiente", en cuyo caso, el punto de entrada está definido en la implementación (implementaion-defined).

Hay palabras en un programa C que tienen un significado y utlidad especial, y son llamadas *keywords*. Otras, pueden ser usadas como especificadores de varios tipos. Cada identificador (aparte de las macros) es válido únicamente dentro de una parte del programa, a esto se le llama *scope* y puede pertenecer a uno de cuatro tipos de *name spaces*.

Las definiciones de funciones incluyen secuencias de *statements* y *declarations*, que a su vez, pueden incluir *expressions* que especifican las operaciones computacionales a realizar por el programa. Por lo que las *declarations* y *expressions* pueden Crear, Destruir, Acceder y Manipular *objects*. Donde cada *object*, *function* y *expression* están asociados con un *type*.

### ASCII Chart
[ASCII Chart](https://cppreference.com/w/c/language/ascii.html)

### Character Sets
[Character Sets and Encodings](https://cppreference.com/w/c/language/charset.html)

### Translation
Un programa en C pasa por un total de ocho fases distintas para poder ser convertido en un programa ejecutable, este proceso es conocido como `translation` o *proceso de traducción*. Sin embargo, cabe aclarar que la implementación real puede combinar estas fases o procesarlas de distintas maneras, pero el resultado es básicamente el mismo siempre.
#### Phase 1
En esta primera fase, los bytes individuales del archivo source, que generalmente están codificados en UTF-8, son mapeados de acuerdo a la forma de implementación definida, a los caracteres del *source character set*. Es decir, el compilador trasforma todos los caracteres del archivo a su forma normal, o a la forma en que el compilador puede entender y trabajar con esos caracteres.

El *source character set* o *conjunto de caracteres básico* es un conjunto de caracteres de múltiples bytes, que contiene un total de 96 caracteres:
* 5 caracteres de espacio en blanco (space, horizontal tab, vertical tab, form feed, new-line)
* 10 carateres de dígitos (0 - 9)
* 52 letras, incluyendo mayúsculas y minúsculas (a - z)
* 29 caracteres especiales o de puntuación (_ { } [ ] # ( ) < > % : ; . ? * + - / ^ & | ~ ! = , \ " ')

#### Phase 2
Esta segunda fase detecta la presencia de backslashes (\) al final de las líneas, pues generalmente son usadas para definir una sola línea en varias líneas físicas. Por lo tanto, el compilador las elimina y une todas esas líneas en una única línea lógica. Si un archivo source que no está vacío no termina con el caracter new-line en esta fase, se dice que el comportamiento es indefinido.

#### Phase 3
En esta tercera fase, el compilador convierte el código en *preprocessing tokens* válidos que puede entender, y por lo tanto identificar qué es cada parte del código, como headers, identifiers, integer constants, float constants, character constants, string literals, operators, etc. Además, los comentarios son reemplazados por un caracter de espacio.

Para la generación de los *preprocessing tokens*, se sigue la regla de *maximal munch*, que básicamente busca tomar la secuecia más larga de caracteres (mayor cantidad de caracteres) que puedan formar un token válido.

#### Phase 4
En la cuarta fase el *proprocessor* es ejecutado, el cual, se encarga de ejecutar todas aquellas partes del código que inician con el caracter `#`, como `#include` o `#define`. Entonces, cada archivo que es introducido al archivo source, pasa por todas las fases anteriores (Phase 1 - 4) recursivamente, lo que asegura que todos los archivos a usar tengan el formato correcto y el compilador puede trabajar con ellos. Al final de esta fase, todo el código ejectutado por el *preprocessor* es eliminado del archivo source, pues es reemplazado por el resultado correspondiente.

#### Phase 5
En esta fase, todos los caracteres de escape se encuentran representados por caracteres del *source character set*, por lo que son convertidos a caracteres de *execution character set*. Es decir, que todos aquellos caracteres de escape como `\n`, son convertidos a caracteres que el compilador realmente puede interpretar por lo que son.

#### Phase 6
Esta fase es sencilla, y básicamente se encarga de contatenar *string literals* para convertir múltiples strings en un solo string.

#### Phase 7
Esta es la fase de compilación, donde los tokens son analizados en cuanto a su sintaxis (¿está bien escrito?), y a su semántica (¿tiene sentido?) como una unidad de traducción o *tranlation unit*. Se revisa que las variables estén declaradas antes de ser usadas, que los tipos de datos existan, se realizan optimizaciones, etc. Todo esto para que el compilador pueda convertir todo el código en código máquina o en código objeto, que la computadora puede entender pero todavía no lo puede ejecutar.

#### Phase 8
En esta última fase, se da el proceso de *linking*, donde las *translation units*, obtenidas de la fase anterior, y las librerías necesitadas son colectadas en una imagen de programa que contiene la información necesitada para su ejecución. Es decir, que se arma el programa ejecutable final que contine toda la información necesaria para que funcione y finalmente la computadora pueda ejecutar dicho programa.

### Punctuation
Hay un total de 47 símbolos de puntuación en C, y algunos pueden tener múltiples funcionalidades:
#### Delimitation and Grouping
* `{}` - Delimitan bloques de código, listas de inicializadores, y definiciones de estructuras, uniones y enumeraciones.
* `[]` - Actúan como operador de subscripción para arrays, forman parte de declaradores de arrays, y se usan para designadores en inicialización.
* `()` - Agrupan expresiones, delimitan llamadas a funciones, encierran operandos, rodean listas de parámetros, y aparecen en estructuras de control.
#### Preprocessing
* `#` - Introduce directivas del preprocesador. También funciona como operador de "stringificación" que convierte argumentos de macro en cadenas de texto.
* `##` - Es el operador de concatenación de tokens del preprocesador, que une elementos adyacentes para formar un solo token.
#### Control and Separation
* `;` - Termina sentencias y declaraciones.
* `:` - Aparece en el operador condicional, en etiquetas, en campos de bits.
* `,` - Funciona como operador secuencial y como separador en listas de declaradores, argumentos de función, inicializadores, y parámetros de macro.
#### Access and Navegation
* `.` - Operador de acceso a miembros de estructuras y uniones, y designadores para miembros específicos en inicialización.
* `->` - Operador de acceso a miembros a través de punteros, equivalente a (*ptr).member.
* `...` - Indica funciones variádicas (que aceptan número variable de argumentos) y macros variádicas.
* `?` - Forma parte del operador condicional ternario.
* `::` - Indica alcance de atributos y parámetros prefijados del preprocesador. 
#### Arithmetic and Logical
* `+`, `-`, `*`, `/`, `%` - Funcionan como operadores aritméticos básicos, donde * también actúa como operador de indirección para punteros y como indicador de puntero en declaraciones.
* `~` - Operador de complemento bit a bit (NOT).
* `!` - Operador de negación lógica (NOT lógico).
#### Bit-to-Bit and Logical
* `^` - Operador XOR bit a bit.
* `&` - Operador AND bit a bit y operador de dirección (para obtener la dirección de una variable).
* `|` - Operador OR bit a bit.
* `&&` - Operador AND lógico.
* `||` - Operador OR lógico.
* `<<`, `>>` - Operadores de desplazamiento de bits a la izquierda y derecha.
#### Assignation
* `=` - Operador de asignación simple, también usado en inicialización y definición de constantes de enumeración.
* `+=`, `-=`, `*=`, `/=`, `%=`, `^=`, `&=`, `|=`, `<<=`, `>>=` combinan una operación aritmética o bit a bit con asignación.
#### Comparation
* `<, >`, `<=`, `>=` - Operadores relacionales para comparaciones numéricas. Los símbolos <, > también delimitan nombres de cabecera en directivas del preprocesador.
* `==`, `!=` - Operadores de igualdad y desigualdad.
#### Increment-Decrement
* `++`, `--` - Operadores de incremento y decremento, que pueden usarse como prefijo o sufijo.

### Identifier
Un *identifier* es una secuencia arbitraria larga de dígitos, guiones bajos, letras, etc. Para que sea válido debe empezar con un caracter que no sea numérico o que no sea Unicode. Además, los identificadores son *case-sensitive*.

Cada identificador, aparte de los usados en macros, tienen un *scope*, pertenecen a un *name space* y pueden tener *linkage*. Incluso, el mismo identificador puede ser usado para denotar diferentes entidades en distintos puntos del programa, o en el mismo punto pero en name spaces distintos.

Cabe mencionar que existen identificadores reservados y no deben ser declarados en el programa, pues de hacerlo surgiría comportamiento inesperado. Los siguientes son los *reserved identifiers*:
* Identificadores que son *keywords*.
* Identificadores externos que empiezan con guion bajo.
* Identificadores que empiezan con guion bajo y son seguidos por una letra mayúscula u otro guion bajo.
* Identificadores definidos por la *standard library* o por el propio lenguaje.

En cuanto a los límites de longitud de un identificador, con la tecnología actual no existe un límite especificado. Sin embargo, los compiladores y linkers iniciales tenían límites bien definidos.

### Scope
Cada identificador que aparece en un programa de C es visible solamente en alguna porción discontigua del código, a lo que se le llama *scope*. Entonces, C tiene cuatro diferentes tipos de *scope*, excluyendo sus combinaciones:
* `Block Scope`: Este es el tipo de scope más común y restrictivo. Cualquier identificador declarado dentro de una sentencia compuesta (entre llaves), incluyendo cuerpos de funciones, o en expresiones dentro de sentencias if, switch, for, while, o do-while, tiene alcance de bloque. Su vida útil comienza exactamente en el punto donde lo declaras y termina cuando se cierra el bloque correspondiente.
* `File Scope`: Este representa el alcance más amplio para variables regulares. El alcance de cualquier identificador declarado fuera de cualquier bloque o lista de parámetros comienza en el punto de declaración y termina al final de la unidad de traducción. También, es conocido como variales globales.
* `Function Scope`: Este es un tipo muy específico que se aplica exclusivamente a las etiquetas (labels) usadas con goto. Una etiqueta declarada dentro de una función está en alcance en todas partes dentro de esa función, en todos los bloques anidados, antes y después de su propia declaración.
* `Function Prototype Scope`: Este es el más limitado de todos los scopes. El alcance de un nombre introducido en la lista de parámetros de una declaración de función que no es una definición termina al final del declarador de función.

### Lifetime
Cada objeto en C existe, tiene una dirección constante, retiene su último valor almacenado (excepto cuando el valor es indeterminado), y para VLA, retiene su tamaño durante una porción de la ejecución del programa conocida como el tiempo de vida de este objeto.

Para la mayoría de objetos, el lifetime está directamente relacionado con su *storage duration*. Para los objetos que se declaran con duración de almacenamiento automática, estática y de hilo, el tiempo de vida es igual a su duración de almacenamiento. Esto significa que:
* `Variables automáticas (locales)`: Viven desde que se declaran hasta que termina su bloque.
* `Variables estáticas`: Viven durante toda la ejecución del programa.
* `Variables de hilo`: Viven durante la vida del hilo que las creó.

Los objetos creados dinámicamente tienen reglas especiales. Para los objetos con duración de almacenamiento asignada, el tiempo de vida comienza cuando la función de asignación retorna (incluyendo el retorno de realloc) y termina cuando se llama a la función realloc o de desasignación. Estos objetos nacen con `malloc()`, `calloc()`, o `realloc()`, y mueren con `free()` o `realloc()`. Su lifetime está completamente bajo control propio, lo que da poder pero también responsabilidad.

C también tiene un concepto más sutil llamado *temporary lifetime* para objetos temporales. Los objetos de struct y union con miembros de array que son designados por expresiones que no son lvalue, tienen tiempo de vida temporal. Entonces, en el siguiente ejemplo, el tiempo de vida temporal comienza cuando se evalúa la expresión que se refiere a tal objeto y termina cuando termina la expresión completa contenedora o el declarador completo.
```C
struct T { double a[4]; };
struct T f(void) { return (struct T){3.15}; }
double g1(double* x) { return *x; }
int main(void)
{
    double d = g1(f().a);  // ¿Es esto seguro?
}
```

### Lookup and Name Spaces
Cuando un identificador es localizado, se realiza una búsqueda o *lookup*, para intentar localizar la declaración que introdujo dicho identificador y que está en el scope correspondiente. Por lo tanto, C permite más de una declaración del mismo identificador en el mism scope siempre y cuando pertenezcan a diferentes categorías llamadas *name spaces*. Los siguientes son los *name spaces* disponibles y siguen la jerarquía:
1. `Label name space`: Todos los identificadores declarados como *labels*.
2. `Tag names`: Todos los identificadores declarados como nombres de *structs*, *unions*, y *enumerated types*.
3. `Member names`: Todos los identificadores declarados como miembros de *struct* o *union*.
4. `Global attribute name space`: *attribute tokens* definidos por el estándar.
5. `Non-standard attribute names`: Nombres de atributos seguidos por prefijos de atributos.
6. `Ordinary identifiers`: Son todos los otros identificadores, como de nombres de funciones, nombres de objetos, nombres de typedefs, constantes de enumeración, etc.

Ejemplo:
```C
void foo (void) { return; } // ordinary name space, file scope
struct foo {      // tag name space, file scope
    int foo;      // member name space for this struct foo, file scope
    enum bar {    // tag name space, file scope
        RED       // ordinary name space, file scope
    } bar;        // member name space for this struct foo, file scope
    struct foo* p; // OK: uses tag/file scope name "foo"
};
enum bar x; // OK: uses tag/file-scope bar
// int foo; // Error: ordinary name space foo already in scope 
//union foo { int a, b; }; // Error: tag name space foo in scope
 
int main(void)
{
    goto foo; // OK uses "foo" from label name space/function scope
}
```

### Types
Los objetos, funciones y expresiones en C tienen una propiedad llamada *type*, que determina cómo se debe interpretar el valor binario almacenado en dicho objeto o evaluado por dicha expresión. El sistema tipos de C consiste en los siguientes *fudamental types*:
#### Void type
* `void`: Representa la ausencia de tipo, utilizado principalmente para funciones que no retornan un valor o para punteros genéricos.
#### Basic type
* `char`: Tipo de caracter básico, y puede ser *signed* o *unsigned* (8 bits).
* `signed char`: Tipo de caracter con signo.
* `short`: Entero corto con signo (16 bits).
* `int`: Entero estándar con signo (32 bits).
* `long`: Entero largo con signo (64 bits).
* `long long`: Entero extra largo con signo (128 bits).
* `_Bool`: Tipo booleano (0/1 o false/true).
* `unsigned char`: Tipo de caracter sin signo.
* `unsigned short`: Entero corto sin signo (16 bits).
* `unsigned int`: Entero estándar sin signo (16-32 bits).
* `unsigned long`: Entero largo sin signo (32-64 bits).
* `unsigned long long`: Entero extra largo sin signo (64 bits).
* `float`: Punto flotante de precisión simple.
* `double`: Punto flotante de precisión doble.
* `long double`: Punto flotante de precisión extendida.
#### Derived type
* `Array`: Arrays o arreglos de elementos de un solo tipo.
* `struct`: Estructura que agrupa diferentes tipos de datos.
* `union`: Uniones que permiten almacenar diferentes tipos en la misma ubicación de memoria.
* `Function`: Tipo que representa una función.
* `Pointer`: Tipo que almacena direcciones de memoria.
* `Atomic`: Tipo usado en la programación concurrente.

Cabe mencionar que para cada uno de estos tipos pueden existir diferentes versiones dependiendo de la palabra reservada que se use o no:
* Si no se usa alguna palabra reservada, su comportamiento es normal.
* Si se usa *const* hace que el objeto sea solo de lectura.
* Si se usa *volatile* indica que el valor puede cambiar de manera impredecible.
* Si se usa *restrict* para optimizar los punteros.

### Objects and Alignment requirement
Los programas en C pueden Crear, Destruir, Acceder y Manipular objetos, donde un *object* es una región de información almacenada en el entorno de ejecución cuyo contenido puede representar el valor o valores del objeto. Todo objeto puede tener las siguientes características básicas:
* `size`: Tamaño del objeto o la cantidad de bytes que ocupa en memoria (sizeof).
* `alignment requirement`: Es un valor entero de tipo `size_t` que representa la restricción de alineación que determina en qué direcciones de memoria puede comenzar un objeto de cierto tipo. Es decir, indica el múltiplo del que debe ser una dirección de memoria para poder iniciar el almacenamiento de un objeto de un tipo específico, con la intención hacer la lectura de memoria más eficiente. Llegando al punto en que el orden de declaración de variables importa.
* `storage duration`: Se refiere al período durante el cual un espacio de memoria está reservado y disponible para un objeto. Determina cuándo el sistema asigna memoria para un objeto y cuándo esa memoria es liberada y puede ser reutilizada por el sistema para otros propósitos. En C existen cuatro categorías: automatic
* `lifetime`: Se refiere al período durante el cual el contenido de un objeto existe y es válido en un espacio de memoria dado. Comienza cuando el objeto se inicializa con un valor y termina cuando el objeto es destruido o cuando su valor deja de ser válido.
* `effective type`: Se refiere al tipo de dato que C considera que está almacenado en un espacio de memoria específico en un momento dado. Esta "etiqueta" invisible determina cómo el compilador puede optimizar el código y qué tipos de accesos a memoria son válidos según las reglas de strict aliasing.
* `value`: Es el valor asignado al objeto y depende del tipo de dicho objeto. Puede ser indeterminado.
* `identifier`: Este es el nombre que denota o identifica al objeto, y es opcional pero muy útil.

### Main Function
Cualquier programa de C hecho para ser ejecutado en un entorno hosteado (con un Sistema Operativo), debe contener la definición de una función llamada `main`, la cual, es designada como el punto de entrada para el programa. Hay dos tipos principales para su implementación:
* Cuando la función no recibe argumentos en su ejecución:
    ```C
    int main(void) { /*body*/ }
    ```
* Cuando la función sí recibe argumentos en su ejecución:
    ```C
    int main(int argc, char *argv[]) { /*body*/ }
    /* Donde:
        - "argc (argument count)" es un valor no negativo que representa el número total de argumentos pasados al programa en su ejecución.
        - "argv (argument vector)" es un puntero al primer elemento de un arreglo de punteros de tamaño argc + 1, donde el primer elemento argv[0] apunta al nombre del programa, los demás elementos apuntan a los strings que repesentan a los argumentos, y el último elemento argv[arc] es null.
    */
    ```
En cuanto al `return` de la función main, si es explícitamente usado, llama implícitamente a `exit()`, y el valor `0` o `EXIT_SUCCESS` indican terminación exitosa, mientras que `1` o `EXIT_FAILURE` indican terminación fallida. Por otro lado, `main` es llamada en el setup del programa, después de que todos los objetos con duración de almacenamiento estática hayan sido inicializados. Además, un prototipo de esta función no puede ser proporcionado por el mismo programa.
* Ejemplo de uso:
    ```C
    int main(int argc, char *argv[])
    {
        printf("argc = %d\n", argc);
        for (int ndx = 0; ndx != argc; ++ndx)
            printf("argv[%d] --> %s\n", ndx, argv[ndx]);
        printf("argv[argc] = %p\n", (void*)argv[argc]);
    }
    ```

### As-if rule (Observable behaviour)
Esta regla permite al compilador hacer "trampa", o realizar cualquier tipo de transformación en el código con la intención de optimizarlo, siempre y cuando no modifique el comportamiento observable del programa. Esta regla se cumple siempre y cuando se protega lo siguiente:
1. Objetos volátiles:
    * Antes C11: En cada "sequence point", los valores de objetos `volatile` deben estar estables.
    * Desde C11: Los accesos a `volatile` ocurren exactamente según la semántica escrita, sin reordenamiento
2. Archivos:
    * Al terminar el programa, los datos escritos a archivos deben ser idénticos a ejecutar el código literalmente.
3. Entrada/aalida interactiva:
    * Los prompts deben mostrarse antes de esperar entrada del usuario.
4. Entorno de punto flotante:
    * Si `#pragma STDC FENV_ACCESS` está `ON`, los cambios al entorno de punto flotante se preservan (excepciones, modos de redondeo).

Esta regla es crucial cuando se trabaja con hardware, sistemas embebidos, o cuando las optimizaciones del compilador interfieren con el comportamiento esperado. 

### Undefined behaviour
El estándar de C precisamente especifica todo el `observable behaviour` (comportamiento definido) de progras hechos en C, sin embargo, dicho estándar no espeficica para las siguientes categorías de comportamiento:
* `undefined behaviour`: En este caso no existen restricciones en el comportamiento del programa, por lo que los compiladores no están obligados a diagnosticar este comportamiento, y el programa resultante tampoco está obligado a hacer algo significativo. Es decir, que no hay un comportamiento definido para todos los casos del programa y no se sabe lo que pasará exactamente.
* `unspecified behaviour`: En este caso dos o más comportamientos son permitidos, y la implementación no está obligada a detallar los efectos de cada comportamiento. Esto significa que el resultado de cada comportamiento no especificado puede ser completamente diferente y variar aunque sea el mismo porgrama.
* `implementation-denifed behaviour`: Este es un caso donde se da comportamiento no especificado pero donde el documento donde se encuentran las declaraciones es el que define las decisiones que se van a tomar, y por lo tanto, el resultado que se va a obtener.
* `locale-specific behaviour`: Este es un caso donde se da un comportamiento definido por la implementación donde el comportamiento depende en el `currently chosen locale` (locale es básicamente la forma de implementar y tomar decisiones).

### Memory model
El modelo de memoria define la semántica (significado) del uso de la memoria de la computadora, como herramienta para la máquina abstracta de C. En este contexto, el almacenamiento de memoria o memoria disponible para un programa de C es una o más secuencias de `bytes` contiguos, donde cada `byte` tiene una dirección de memoria única.

Por otro lado, un `byte` es la unidad de memoria más pequeña que puede tener una dirección, y son lo suficientemente largos para representar cualquier miembro del *basic character set*. C soporta bytes de 8 o más bits.

## C Keywords
[C Keywords](https://cppreference.com/w/c/keyword.html)

## Preprocessor
El preprocesador es ejecutado en la fase 4 del proceso de traducción, por lo que sucede antes de la compilación. El resultado del preprocesador es un **único archivo**, el cual es pasado al compilador.

Las `preprocessor directives` o directivas del preprocesador controlan su comportamiento, y cada directiva ocupa una línea y deben seguir un cierto formato:
* Primero, va el caracter `#`.
* Luego, el instrucción del preprocesador (`define`, `include`, etc.).
* Argumentos de la instrucción.
* Salto de línea.

Por otro lado, el preprocesador tiene las siguientes `capabilities` o capacidades:
* Condicionalmente compilar partes del archivo base.
* Reemplazar macros en texto.
* Incluir otros archivos.
* Arrojar errores o advertencias.

### Conditional directives
El preprocesador soporta compilación condicional de partes del archivo principal. Este comportamiento es controlado por las siguientes directivas:
* `#if`
* `#else`
* `#elif`
* `#ifdef`
* `#ifndef`
* `#elifdef`
* `#elifndef`
* `#endif`

El bloque de preprocesamiento condicional se estructura de la siguiente manera:
1. Inicia con una directiva como: `#if`, `#ifdef`, or `#ifndef`.
2. Luego, incluye cualquier cantidad de directivas adicionales como: `#elif`, `#elifdef`, or `#elifndef`.
3. Después, opcionalmente incluye como máximo una directiva `#else`.
4. Finalmente, el bloque termina con la directiva `#endif`.

Cualquier bloque de preprocesamiento condicional, ya sean bloques internos o no, son procesados individualmente, y las directivas usadas controlan completamente el comportamiento. Funcionan básicamente como los *if* tradicionales pero para el preprocesador.

Además, es importante tener en cuenta que las directivas solo pueden y deben usar `constants` o `identifiers`. En el caso de las constantes no hay problema en cuanto a su declaración, pues son globales, pero para los identificadores, deben ser definidos usando `#define` para que las directivas condicionales las puedan usar.

### Replacement directives
El preprocesador puede realizar reemplazo de macros, ya sea reemplazo por texto simple o reemplazo en forma de función. Las siguientes directivas son usadas para esto:
* `define`
* `undef`

En este contexto, una macro es una definición de texto, básicamente un identificador, que el preprocesador sustituye por algún valor definido o por alguna función también definida. Ejemplos:
* Text macro: El preprocesador reemplaza el identificador por el valor asignado, por lo que no ocupa memoria.
    ```C
    #define PI 3.14159
    #define MAX_SIZE 100
    ```
* Function-like macro: Igualmente, el preprocesador únicamente reemplaza el identificador y sus parámetros por la evaluación que se realiza dentro de la macro. Para este tipo de macros, existen dos operadores muy útiles, `#` para convertir a string y `##` para concatenar.
    ```C
    #define MAX(a, b) ((a) > (b) ? (a) : (b))
    #define FUNCTION(name, a) int func_##name(int x) { return (a) * x; }
    ```

### Inclusion directives
En esta categoría solo existe la directiva `#include`, que básicamente incluye otro archivo con código dentro del archivo donde se está usando dicha directiva. Esta inclusión sucede inmediatamente en la siguiente línea de la directiva.

Existen dos formas de utilizar esta directiva, dependiendo completamente de la sintáxis:
* `""`: Esta sintáxis obliga al preprocesador a buscar los archivos en el directorio actual, y si no los encuentra, los busca en el sistema.
    ```C
    #include "my_header_file.h"
    ```
* `<>`: Esta sintáxis obliga al preprocesador a buscar los archivos en el sistema directamente, por lo que es el segundo paso si la búsqueda con la sintáxis anterior falla.
    ```C
    #include <stdio.h>
    ```

### Implementation-defined directives
El comportamiento definido por la implementación es controlado únicamente por la directiva `#pragma`. Esta directiva controla la implementación específica de un archivo que el compilador debe realizar, como deshabilitar advertencias del compilador, cambiar los requirimientos, etc., y cualquier uso de esta que no sea reconocido es ignorado.

### Informative directives
En esta categoría se tiene la directiva `#line` que sirve para cambiar la línea actual y el nombre del archivo en el preprocesador.

También, existen las directivas `#error` y `#warning`. Estas directivas muestran el error o advertencia, respectivamente, que se especifica y se renderiza el programa ignorando dicha información.

## Statements
Los *statements* o sentencias son fragmentos de cualquier programa de C que son ejecutados secuencialmente, es decir, uno tras otro siguiendo un orden. Existen cinco tipos de sentencias en C:
* `compound statements`: También conocidos como *blocks* o bloques, son secuencias de sentencias y declaraciones entre llaves `{}`, por lo que crean su propio scope y permiten agrupar múltiples sentencias. Ejemplo:
    ```C
    if (expr)
    {
        int n = 1;
        printf("%d\n", n);
    }
    ```
* `expression statements`: Estas sentencias son seguidas por `;`, incluyen asignaciones, declaraciones, definiciones y llamadas a funciones. Ejemplo:
    ```C
    printf("statement");
    ```
* `selection statements`: Las sentencias de selección eligen una única sentencia de varias basándose en el resultado de una expresión. Ejemplo:
    ```C
    if (expression) {
        // Hacer algo
    }
    else {
        // Hacer otro algo
    }
    switch (expression) {
        case 1:
            break;
        default:
            // Hacer algo
    }
    ```
* `iteration statements`: Las sentencias iterativas ejecutan repetidamente una sentencia. Ejemplo:
    ```C
    while (expression) {
        // Hacer algo
    }
    for (expression) {
        // Hacer algo
    }
    do {
        // Hacer algo
    } while (expression);
    ```
* `jump statements`: Las sentencias de salto transfieren el flujo de control incondicionalmente. Ejemplo:
    ```C
    break;
    continue;
    return;
    goto;
    ```

### If
La sentencia `if` ejecuta código condicionalmente, y se usa donde el código necesita ser ejecutado únicamente cuando alguna condición se cumpla. Ejemplo:
```C
int j = 1;
if (j > 2) {
    printf("%d > 2\n", j);
}
else {
    printf("%d < 2\n", j);
}
```

### Switch
La sentencia `switch` ejecuta código de acuerdo al valor de un argumento. Es importante notar que esta sentencia únicamente redirige el flujo de ejecución al `case` donde la expresión se cumple y continúa ejecutando secuencialmente, por lo que es importante tener el cuenta el concepto de `fall-through`. Ejemplo:
```C
int k = 2;
switch (k) {
    case 1:
        printf("Case 1\n");
        break;
    case 2:
        printf("Case 2 and");
    case 3:
        printf(" Case 3\n");
        break;
    default:
        printf("Case 0\n");
}
```

### For
La sentencia `for` ejecuta un bucle, y es un equivalente corto al bucle *while*. Cabe mencionar que se puede combinar con otras palabras clave como `break`, `continue`, `return`, etc. Ejemplo:
```C
for (int i = 0; i < 10; ++i) {
    // La primera parte se ejecuta antes de iniciar el bucle.
    // La segunda parte se ejecuta antes de cualquier iteración.
    // La tercera parte se ejecuta después de cualquier iteración.
}
```

### While
La sentencia `while` ejecuta código repetidamente hasta que el resultado de una expresión ya no secumpla o se convierta en 0, y dicho resultado se checa antes de cualquier iteración. De igual forma, se puede combinar con otras palabras clave. Ejemplo:
```C
int n = 0;
while (n < 10) {
    printf("Iteration: %d\n", n);
    ++n;
}
```

### Do-While
La sentencia `do-while` ejecuta código repetidamente hasta que el resultado de una expresión ya no se cumpla o se convierta en 0, y dicho resultado se checa después de cualquier iteración. Se puede combinar también con otras palabras clave. Ejemplo:
```C
int m = 0;
do {
    printf("Iteration: %d\n", m);
    ++m;
} while (m < 10);
```

### Continue
La sentencia `continue` provoca que el código restante después de dicha sentencia dentro de algún bucle sea ignorado, y por lo tanto, no sea ejecutado. Básicamente ignora lo que resta de una iteración sin terminar por completo el bucle.

### Break
La sentencia `break` hace que la sentencia donde es usado termine completamente, ignorando el código y/o las iteraciones restantes. Esta sentencia puede ser usada dentro de bucles o de switches.

### Goto
La sentencia `goto` transfiere el control incondicionalmente a la ubicación deseada, la cual es especificada por algún `label`. En este contexto, un label es un `identifier` seguido por `:` y tienen el mismo scope que una función. Ejemplo:
```C
int main(void)
{
    for (int x = 0; x < 3; x++) {
        for (int y = 0; y < 3; y++) {
            printf("(%d;%d)\n",x,y);
            if (x + y >= 3) goto endloop;
        }
    }
endloop:; // identifier "endloop" + ":" = "endloop:";
// goto es muy útil para salir de bucles anidados.
}
```

### Return
La sentencia `return` finaliza la función donde se está utilizando y devuelve el valor especificado al lugar u objeto que llamó a dicha función.

## Expressions
Una expresión es una secuencia de operadores y operandos que especifican una tarea computacional. La evaluación de una expresión puede generar un resultado, efectos variados o designar objetos o funciones.

Los operandos de cualquier operador pueden ser otras expresiones o *primary expressions* (constantes y literales, identificadores o palabras clave y *generic selections*). Cualquier expresión que esté dentro de paréntesis también es clasificada como una primary expression, lo que garantiza que tendrá mayor precedencia que cualquier otro operador.

### Value categories
Cualquier expresión en C is caracterizada por dos propiedades independientes: un `type` y una `value category`. Por lo tanto, toda expresión pertenece a una de tres *value categories*:
* **`Lvalue expressions`**: Cualquier expresión donde su tipo de objeto es cualquiera diferente al tipo `void`, en otras palabras, aquellas que designan objetos (ubicaciones de memoria) de cualquier tip. A esta categoría también se le conoce como `left value`, pues refleja el uso de *lvalue expressions*. 
* **`Non-Lvalue expressions`**: También conocidas como `rvalues`, son aquellas expresiones que no designan objetos, es decir, que representan valores que no son almacenados en memoria, por lo que no se puede acceder o utilizar su dirección de memoria. 
* **`Function designator expressions`**: Son aquellas expresiones de tipo función que se refieren a funciones específicas. Este tipo de expresiones siempre son convertidas a punteros de categoría *non-lvalue* que apuntan a una función.

### Evaluation order
El orden de evaluación de los operandos de cualquier operador de C no está especificado (a excepción de ciertos casos). Por lo que el compilador evaluará a las expresiones en cualquier orden, y puede elegir un orden u otro incluso cuando sea la misma expresión. Además, en C no existe en concepto de evaluación *left-to-right* o *right-to-left*.

#### Evaluations
Existen dos tipos de evaluaciones realizadas por el compilador para cada una de las expresiones:
* `value computation`: Es el valor calculado que es regresado por la expresión. Puede ser un lvalue o un non-lvalue.
* `side effect`: Puede ser acceder a un objeto, modificar un objeto o archivo, o llamar a una función que realiza cualquiera de estas operaciones.
Cabe mencionar que, si no se producen efectos por la expresión o el compilador determina que el valor de la expresión no es utilizado, dicha expresión puede no ser evaluada.
#### Ordering
Las evaluaciones de expresiones que están secuenciadas (*sequenced-before*) dentro del mismo hilo, se caracterizan por ser asimétricas, transitivas y en pares. Por lo tanto, cuando se tienen expresiones secuenciadas, se sigue lo siguiente:
* Si existe un *sequence point* (garantiza que los efectos secuandarios son hechos antes) entre expresiones E1 y E2, entonces todo el procesamiento de E1 se da antes de procesar E2.
* Si la evaluación A está secuenciada antes que la evaluación B, la evaluación de A se completará antes de iniciar con la evaluación de B. Y viceversa.
* Si la evaluación A y la evaluación B no están secuenciadas y son independientes, se pueden dar dos casos:
    * La evaluación de A y de B suceden en cualquier orden y se pueden dar al mismo tiempo.
    * La evaluación A y B son secuenciadas en cualquier orden, pero una se evalúa antes que otra siempre.
#### Rules
[14 Rules](https://en.cppreference.com/w/c/language/eval_order.html#Rules)
#### Undefined behaviour
* Si el efecto secundario en un objeto está junto con otro efecto secundario del mismo objeto dentro de la misma expresión, se da un comportamiento indefinido. Ejemplo:
    ```C
    i = ++i + i++;
    i = ++i + 1;
    fnc(++i, ++i);
    ```
* Si el efecto secundario en un objeto está junto con el uso del valor del mismo objeto dentro de la misma expresión, se da un comportamiento indefinido. Ejemplo:
    ```C
    f(i, i++);
    a[i] = i++;
    ```

### Operators
[Expresssion operators](https://cppreference.com/w/c/language/operators.html#Operators)

### Operator precedence
[C Operator Precedence](https://cppreference.com/w/c/language/operator_precedence.html)

### Generic selection
La selección genérica provee una forma de elegir una de múltiples expresiones en tiempo de compilación, y se basa en un tipo de expresiones de control.

Se utiliza la sintáxis **_Generic(*controlling-expression*, *association-list*)**, donde:
* `_Generic()` es simplemente la palabra clave.
* `controlling-expression` es la expresión a controlar.
* `association-list` es la lista de asociaciones separadas por comas.

Ejemplo:
```C
// Possible implementation of the tgmath.h macro cbrt
#define cbrt(X) _Generic((X),     \
              long double: cbrtl, \
                  default: cbrt,  \
                    float: cbrtf  \
              )(X)
```

## Initialization
Una declaración de un objeto puede incluir su valor inicial mediante el proceso de `initialization`, pues el *initializer* o inicializador especifica el valor inicial almacenado en un objeto. Existen tres tipos de inicialización:
* scalar initialization
* array initialization
* struct/union initialization

Cuando un objeto no es explícitamente inicializado, **en algunos casos** se le asigna un valor automáticamente que preresenta en vacío del tipo de ese objeto. Por ejemplo, un objeto de tipo entero es inicializado con un cero unsigned, objetos de tipo flotante son inicializados con un cero positivo, etc.

### Scalar initialization
Se refiere a la inicialización de objetos de tipo escalar, es decir asignar valores iniciales a variables de tipos básicos, como enteros, flotantes, booleanos, caracteres y punteros. Existen tres tipos de sintáxis que se pueden usar:
```C
int x = 5;  // Inicialización directa.
int y = {10};  // Inicialización con llaves.
int z = {};  // Inicialización en 0 (depende del type).
```

Es importante notar que los valor correspondiente al inicializador es convertido al tipo correspondiente al objeto que se está inicializando, siempre y cuando la conversión se pueda dar. Por ejemplo:
```C
int i = 3.14;  // double se convierte en int.
float f = 5;  // int se convierte en float.
char c = 65;  // 65 se convierte en el caracter número 65 (A).
```

### Array initialization
La inicialización de arreglos se puede dar de dos formas: usando cadenas de caracteres, para el caso de un string `char s[]`; o usando listas entre llaves `{}`.

Es importante tener en cuenta que:
* Los elementos no inicializados se les da el valor de 0, dependiendo del tipo del arreglo.
* No se pueden proporcionar más inicializadores que el total de elementos de un arreglo.
* Que el tamaño de los arreglos de tamaño desconocido es determinado por el índice más alto inicializado.
* Y que los arrays estáticos (como cualquier otro valor global o estático) requiren expresiones constantes.

Ejemplos:
```C
int arr[] = {1, 2, 3};  // Tamaño automático.
int arr[5] = {1, 2, 3};  // Tamaño de 5, y los elementos restantes son igual a 0.
int arr[5] = {};  // Tamaño de 5 y todos los elementos son igual a 0.

char str[] = "hello";  // Arreglo de tamaño 5 + 1, donde el último es '\0'.
char str[5] = "hello";  // Arreglo de tamaño 5.

int arr[5] = {[0]=1, [4]=5};  // arr = {1, 0, 0, 0, 5}.

int matrix[3][2] = {
    {1, 2},
    {3, 4},
    {5, 6}
};
int matrix[3][2] = {1, 2, 3, 4, 5, 6};
```

### Struct/Union initialization
La inicialización de structses muy parecida a la inicialización de los arrays, con la diferencia de que el orden de declaración de los miembros de una struct sí influye en el momento de la inicialización. Las mismas consideraciones de los arrays aplican en las structs. Ejemplos:
```C
struct Point {int x, y;};
struct Point p = {10, 20};  // x=10, y=20
struct Point p = {.x=10, .y=20};  // x=10, y=20
struct Point p = {};  // x=0, y=0
```

En cuanto a las unions, solo es posible inicializar un miembro, y por defecto es el primer elemento a menos de que se utilicen designators.

## Declarations
Una declaración es un constructo que introduce uno o más identificadores al programa, y especifica su significado y propiedades. Estas pueden aparecer en cualquier scope, y consisten de dos partes obligatorias:
* `specifiers-and-qualifiers`: Especifican el tipo del declarador, por ejemplo: void, int, struct, enum, typeof etc. Se separan mediante espacios en blanco.
* `declarators-and-initializers`: Indican el nombre del identificador y/o información adicional sobre el tipo del objeto, y pueden ser acompañados por inicializadores. Se separan mediante comas.
* Ejemplo:
    ```C
    int a, *b = NULL;
    /* Donde:
        - "int" es el "type specifier".
        - "a" es el "identifier".
        - "*b" proporciona más información sobre el tipo.
        - "NULL" es el "initializer" para ambos declarators.
    */
    ```

### Definitions
Una definición es una declaración que provee toda la información sobre los identificadores que declara. Por ejemplo, una declaración de una función que incluye en cuerpo de dicha función, es una definición; una declaración de un objeto que aloja memoria, es una definición, similar con structs y unions.
* Ejemplo:
    ```C
    int foo(double x) { return x; } // Function definition
    int n = 10; // Variable definition
    struct X { int m; } // Struct definition
    ```

### Pointer declaration
Un puntero es un tipo de objeto que se refiere a una función o un objeto de otro tipo, incluso, puede referirse a nada mediante el uso de `NULL`. Para declarar un puntero se utilizan tres elementos fundamentales:
* El tipo al que apunta el puntero.
* El símbolo de puntero `*`.
* El identificador o nombre del puntero.

Es importante recalcar el uso del símbolo `*`, pues puede tener diferentes usos. En la declaración de un puntero, sirve para indicar que se está declarando un puntero; pero su uso fuera de una declaración sirve para indicar que se está trabajando con el valor del objeto al que el puntero hace referencia. Además, la sintáxis de la declaración de un puntero es crucial, pues la posición de los elementos influye directamente en el funcionamiento del puntero.

Ejemplos:
```C
/* ------------------------------------------------------------------------------------------------------------- */
void *pv = NULL;  // Puntero que hare referencia a nada.
/* ------------------------------------------------------------------------------------------------------------- */
int n;  // Objeto de tipo int.
int *pn = &n;  // Puntero que hace referencia a un objeto de tipo int.
*pn = 7;  // Trabaja con el valor del objeto al que el puntero hace referencia.
/* ------------------------------------------------------------------------------------------------------------- */
int a[2];  // Array de dos elementos.
int *pa = a;  // Puntero que hace referencia al primer elemento de un arreglo de tipo int.
/* ------------------------------------------------------------------------------------------------------------- */
int v() { return 37; }  // Función de tipo int que no recibe argumentos.
int (*pf1)() = v;  // Puntero que hace referencia a una función de tipo int que no recibe argumentos.
(*pf1)();  // Llamada a la función que hace referencia desreferenciando el puntero.
pf1();  // Llamada a la función que hace referencia directamente desde el propio puntero.
/* ------------------------------------------------------------------------------------------------------------- */
int f(int x) { return (x + 1) * 2; }  // Función de tipo int que recibe un int.
int (*pf2)(int) = f;  // Puntero que hace referencia a una función de tipo int que recibe un argumento de tipo int.
/* ------------------------------------------------------------------------------------------------------------- */
```

### Array declaration
Un array es un tipo de objeto que consiste de espacios de memoria alojados contiguamente que contienen objetos no vacíos de cierto tipo. Es decir, que un array es memoria contigua que almacena elementos de un tipo específico. Además, el tamaño del array nunca cambia en todo su tiempo de vida.

Existen tres tipos de arrays que se diferencían por su tamaño:
* `Arrays of constant known size`: Son aquellos arrays que su tamaño o la expresión que define su tamaño es constante y mayor que 0, y pueden ser inicializados como normalmente. Ejemplo:
    ```C
    int n[10];  // Array de 10 elementos de tipo int.
    int n[3] = {1, 2, 3};  // Array de 3 elementos de tipo int, con inicializadores.
    char s[] = "abc";  // Array de 4 elementos de tipo char, donde el último elemento es '\0'.
    ```
* `Variable-length arrays (VLA)`: Son aquellos arrays cuya expresión que define su tamaño es evaluada únicamente en tiempo de ejecución, por lo que deben tener una duración automática y no pueden ser `static`, `extern` o `global`. Además, no pueden ser usados en `struct` o en `unions` Ejemplo:
    ```C
    int x = 10;
    int a[x];  // El tamaño es determinado en tiempo de ejecución.
    ```
* `Arrays of unknown size`: Son aquellos arrays donde su tamaño o la expresión que define su tamaño es omitida, por lo que su tamaño es definido por otras características o simplemente no es definido. Ejemplo:
    ```C
    extern int x[];  // El tamaño del array es desconocido.
    int a[] = {1, 2, 3};  // Se infiere el tamaño del array por sus elementos (3).
    ```

Es importante saber que los arrays se convierten automáticamente a punteros en la mayoría de contextos (conversión array-a-puntero). En esta conversión, el nombre del array se convierte en un puntero al primer elemento, pero el array en sí mismo no es un puntero, sino un bloque contiguo de memoria.

Más ejemplos:
```C
void func1(int arr[static 10]) {
    // El uso de static garantiza que el array es de al menos 10 elementos pero no limitado a esa cantidad.
}

void func2(int a[restrict], int b[restrict]) {
    // El uso de restrict garantiza que a y b no se superponen, es decir, que no comparten los mismos espacios de memoria.
}

void func3(double a[static restrict 100], double b[static restrict 100]) {
    // El uso de static y restrict garantiza que los arreglos son de al menos 100 elementos y que no se superponen.
}

void func4(int rows, int cols, int matrix[rows][cols]) {
    // Uso de VLA (variable-length arrays) dentro de un function scope.
}

int* func5(int size) {
    int *arr = malloc(size * sizeof(int));
    return arr;  // Retorna un puntero que hace referencia al array creado dinámicamente.
}
```

### Enumerations
Un tipo enumerado es un tipo diferente cuyo valor es un valor de su tipo subyacente, que incluye los valores de constantes explícitamente nombradas, conocidas como **constantes de enumeración**. Son prácticamente parecidas a la directiva del preprocesador `#define`, pero con algunos cambios:
* Si no se especifican los valores de las constantes de enumeración, toman el valor anterior más uno (+1), donde el primer valor de cualquier constante de enumeración no especificado es 0.
* Cada constante de enumeración se convierte en una constante entera de tipo int, es decir, que se convierten en números.
* Un enum es compatible con tipos char, int y uint. Y, como son enteros, pueden usarse en conversiones implícitas y operadores aritméticos.
* Los enums son únicamente visibles en el scope donde son declarados.

Ejemplos:
```C
enum State { IDLE, RUNNING, STOPPED, ERROR };
enum State machine_state = IDLE;  // Equivale a 0.

switch (machine_state) {
    case IDLE: printf("Esperando...\n"); break;
    case RUNNING: printf("Ejecutando...\n"); break;
    case ERROR: printf("Error!\n"); break;
}

struct Machine {
    char version[5];
    enum State state;
}
```

### Storage duration
**Nota: Es importante entender que *storage duration* y *lifetime* son conceptos similares, sin embargo, el primero se refiere al tiempo en que un espacio de memoria se utiliza para cierto objeto; mientras que el segundo se refiere al valor almacenado en ese espacio de memoria reservado para dicho objeto.**


Todo objeto tiene una propiedad llamada *storage duration* o duración de almacenamiento, la cual limita el *lifetime* o tiempo de vida del valor de dicho objeto. Existen cuatro tipos de duración de almacenamiento:
* `automatic storage duration`: Este tipo hace que la duración de almacenamiento de los objetos dependan completamente del bloque donde son declarados, pues son asignados cuando se entra al bloque y desasignados cuando el bloque termina por cualquier razón. Cuando se usa recursividad para entrar a un bloque se hacen nuevas asignaciones que dependen del nuevo nivel de recursividad, y esto aplica para cualquier objeto no estático.
* `static storage duration`: Este tipo hace que la duración de almacenamiento de un objeto sea la duración de ejecución de todo el programa, es decir, que su asignación sucede una vez antes de llamar a la función main y se encuentran en la misma dirección de memoria durante todo el tiempo que el programa es ejecutado.
* `thread storage duration`: Este tipo hace que la duración de almacenamiento de los objetos dependan completamente del tiempo de ejecución del *thread* o hilo donde son usados, y su inicialización se realiza cuando el hilo empieza.
* `allocated storage duration`: Este tipo permite asignar y desasignar memoria a como sea necesario, mediante el uso de las funciones para la asignación de memoria dinámica. Es decir, que este tipo es completamente dependiente de cómo sea usado por el programador.

Ejemplo:
```C
int global_var;              // static storage duration
_Thread_local int tls_var;   // thread storage duration

void func() {
    int local_var;           // automatic storage duration
    static int static_var;   // static storage duration
    int *ptr = malloc(sizeof(int)); // allocated storage duration
}
```

### Linkage
Este concepto se refiere a la capacidad de un identificador para ser utilizado en otros scopes o niveles. En C, se reconocen los siguientes tipos de *linkages*:
* `no linkage`: En este tipo los identificadores pueden ser utilizados únicamente dentro del nivel donde se encuentran, por ejemplo, a nivel de bloque. Todos los identificadores que no especifiquen un comportamiento diferente, incluyendo parámetros de la función utilizan este tipo de linkage.
* `internal linkage`: En este tipo los identificadores pueden ser utilizados desde cualquier nivel que se encuentre en la misma unidad de traducción (archivo). Todas las variables y funciones declaradas a nivel de archivo usando `static` o `constexpr` utilizan este tipo de linkage.
* `external linkage`: En este tipo los identificadores pueden ser utiizados desde cualquier otra unidad de traducción (archivo) que pertenezca al propio programa. Todas las variables y funciones declaradas a nivel de archivo que no usan `static` o `constexpr` utilizan este tipo de linkage.

### Storage-class specifiers
Existen cuatro `storage-class specifiers`:
* `auto`: automatic storage duration.
    * Este especificador solo está permitido para objetos declarados dentro de un *block scope* sin incluir las listas de parámetros de funciones. Indica que *storage duration* es automático y no hay *linkage*.
* `register`: automatic storage duration.
    * Este especificador solo está permitido para objetos declarados dentro de un *block scope* incluyendo las listas de parámetros de funciones. Indica que *storage duration* es automático y no hay *linkage*, además, indica al optimizador que debe guardar el valor del objeto en un registro del CPU cuando sea posible, y por lo tanto, no se puede usar su dirección ni se puede convertir en puntero.
* `static`: static storage duration.
    * Este especificador está permitido para funciones y variables a nivel de bloque o archivo. Indica que *static storage duration* y hay *internal linkage*.
* `extern`: static storage duration.
     * Este especificador está permitido para declaraciones de funciones y objetos a nivel de bloque o archivo. Indica que *static storage duration* y hay *external linkage*.
* Extras:
    * `_Thread_local`: thread storage duration.
    * `malloc()`/`free()`: allocated storage duration.

Estos especificadores aparecen en declaraciones, y solo se puede usar uno de ellos. Usar un especificador determina dos propiedades independendientes del nombre que declaran: *storage duration* y *linkage*.

Por defecto, si no se utiliza alguno de los especificadores, se asignan automáticamente:
* `extern` para todas las funciones.
* `extern` para objetos a nivel de archivo.
* `auto` para objetos a nivel de bloque.

Ejemplo:
```C
// Nivel archivo.
int global_var;           // extern por defecto.
static int file_var;      // static + internal linkage.

// Nivel de bloque.
void func() {
    int local;            // auto por defecto.
    static int s_local;   // static + no linkage.
    register int r_var;   // register + no linkage.
}
```

### Const type qualifier
Los objetos declarados usando `const` pueden ser almacenados en memoria de solo lectura por el compilador, incluso, si la dirección del objeto nunca es usada en el programa es posible que no sea  almacenado.

La idea de un objeto constante es que no pueda ser modificado y mantenga el mismo valor el todo el tiempo de ejecución del programa. Por lo tanto, cualquier intento de modificación resulta en error o comportamiendo indefinido.

Ejemplos:
```C
const int n = 1;  // Objeto de tipo constante.
n = 2;  // Error porque "n" es constante.

int x = 2;
const int *p = &x;  // Puntero de int constante.
*p = 5;  // Error porque el tipo del valor del puntero es constante.

struct {int a; const int b;} s1 = {.b=1}, s2 = {.b=2};
s1 = s2;  // Error porque objetos de tipos constante no son asignables.
```

```C
struct s {int i; const int ci;} s;  // Un struct con un solo valor de tipo constante.
const struct s cs;  // Los miembros del struct "cs" de tipo "s", se convierten ambos en constantes.
```

```C
const int arr[] = {1, 2, 3, 4};  // Un array de elementos int constantes.
```

```C
void f(double x[const], const double y[const]);
// x es puntero constante a double
// y es puntero constante a const double
```

### Volatile type qualifier
Cualquier acceso para lectura o escritura de un objeto declarado con `volatile` es considerado como un efecto secundario observable, y es evaluado estrictamente de acuerdo a las reglas del modelo de ejecución.

Es decir, que el uso de `volatile` evita que el compilador realice optimizaciones que asumen que el valor de un objeto no cambia. Esto es posible pues cada lectura/escritura del objeto se hace directamente en la memoria. Ejemplo:
```C
volatile int sensor_value;  // Indica que al compilador que el valor del objeto puede cambiar en cualquier momento del programa.
// Sin volatile, el compilador aplicaría optimizaciones a este código.
while (sensor_value == 0) {
    // Hacer nada.
}
// Volatile asegura que el valor del objeto siempre se manipule directamente en la memoria.
```

Ejemplos:
```C
volatile int n = 1;
int* p = (int*)&n;  // Cast necesario porque &n es volatile int*.
int val = *p;       // Comportamiento indefinido por acceso no-volatile a objeto volatile.
```

```C
struct s { int i; const int ci; } s;
volatile struct s vs;  // "vs.i" es volatile int, "vs.ci" es const volatile int.
```

```C
void f(volatile double x[], const volatile double y[]);
// La función recibe punteros a datos volátiles/constantes.
```

```C
int* p = 0;
volatile int* vp = p;     // OK: int* → volatile int*.
p = vp;                   // Error: pérdida de volatile.
p = (int*)vp;            // OK: cast explícito.
```

### Restrict type qualifier
El uso de `restrict` solo aplica para los punteros, y se encarga de informar al compilador que si un objeto es modificado mediante un puntero de tipo `restrict`, todos los accesos a ese objeto deben ser realizados utilizando única y restrictivamente el puntero usado inicialmente. Lo que permite al compilador realizar optimizaciones agresivas, pues asume que diferentes punteros no hacen referencia al mismo espacio de memoria, es decir, que asegura los datos no se superponen.

Ejemplos:
```C
void copy_array(int n, int * restrict dest, int * restrict src) {
    for (int i = 0; i < n; i++) {
        dest[i] = src[i];  // El compilador sabe que "dest" y "src" no se solapan.
    }
}
```

```C
int sum_with_restrict(int * restrict a, int * restrict b) {
    *a = 10;
    *b = 20;
    return *a + *b;
    // Optimiza a return 30, porque a y b no se pueden solapan.
}
```

```C
float * restrict global_buffer;
float * restrict temp_buffer;

void init_buffers(int size) {
    float *mem = malloc(2 * size * sizeof(float));
    global_buffer = mem;  // Primera mitad.
    temp_buffer = mem + size;  // Segunda mitad.
    // Compilador sabe que no se solapan
}
```

```C
void undefined_behavior_example() {
    int array[10] = {0};
    // UB: mismo array, regiones solapadas
    copy_array(5, array + 2, array);  // array[2] accesible por ambos punteros.
}

void correct_usage() {
    int src[10] = {1,2,3,4,5,6,7,8,9,10};
    int dest[10];

    copy_array(10, dest, src);         // OK: arrays completamente diferentes.
    copy_array(5, src + 5, src);       // OK: copia elementos 0-4 a posiciones 5-9.
                                       // No hay solapamiento: src[0-4] → src[5-9].
}
```

### Struct
Una `struct` es un tipo que consiste de una secuencia de miembros, cuyo almacenamiento es asignado en una secuencia ordenada y contigua de memoria. La memoria asignada para cada uno de los miembros incrementa en el orden en que los miembros son definidos, por lo que el orden de declaración de los miembros de una struct sí afecta la asignación y orden de memoria.

Además, es importante saber que el compilador puede agregar bytes extras como relleno para cumplir con el `alignment requirement`, por lo que el tamaño de una `struct` puede cambiar y no coincidir exactamente con el tamaño requerido por los miembros.

Incluso, las structs pueden inicializarse usando los nombres de los miembros o simplemente usando su posición. Pero, si una struct es asignada mediante `=`, se realiza una copia exacta y completa de dicha struct.

Ejemplos:
```C
// Struct simple.
struct Point {
    int x;
    int y;
}
// Inicialización de struct simple.
struct Point point = {10, 20};
```

```C
// Struct con diferentes tipos.
struct Student {
    char name[50];
    int age;
    float grade;
    struct Point point;
};
// Inicialización de struct compleja
struct Student student = {
    .name = "Juan",
    .age = 20,
    .grade = 85.5,
    .point = {15, 25}
};
```

```C
// Efecto del orden en padding.
struct BadOrder {
    char a;     // 1 byte.
    int b;      // 4 bytes (pero necesita padding).
    char c;     // 1 byte.
};  // Total: posiblemente 12 bytes por el padding.

struct GoodOrder {
    int b;      // 4 bytes.
    char a;     // 1 byte.
    char c;     // 1 byte.
};  // Total: posiblemente 8 bytes, con menos padding.
```

### Union
Una `union` es un tipo que consiste de una secuencia de miembros cuyo almacenamiento es solapado o superpuesto, es decir, que todos los miembros de la union van a ocupar el mismo espacio y dirección de memoria, pero únicamente un miembro puede almacenar su valor a la vez. Por lo tanto, una union es tan grande como su miembro más grande (puede incluir padding) y los miembros que son más pequeños ocupan la misma dirección de memoria.

También, es importante considerar que escribir en un miembro y leer de otro miembro es considerado por C como comportamiento indefinido, pero es permitido en ciertos casos. Además, debido a la naturaleza de la union solo se puede inicializar su primer miembro o especificar qué miembro se debe inicializar.

Ejemplos:
```C
// Union simple.
union Number {
    int i;
    float f;
    double d;
};
// Inicialización de union simple.
union Number number;
number.f = 3.2;  // Se especifica qué miembro inicializar.
```

```C
// Union con struct para datos variantes.
struct VariantData {
    enum { TYPE_INT, TYPE_FLOAT, TYPE_STRING } type;
    union {
        int i;
        float f;
        char str[20];
    } data;
};  // "data" es la union, que puede tener un int, o un float o un array.
// Inicialización de struct con union.
struct VariantData var1 = {TYPE_INT, .data.i = 100};
```

### Bit-fields
Un `bit-field` declara un miembro con un `width` específico en `bits`. Miembros declarados de esta forma que son adyacentes pueden ser empaquetados en bytes individuales.

Por otro lado, solo pueden ser `bit-fields` los tipos enteros (`int`, `unsigned int`, `signed int`, `char`, `short`, `long` o `_Bool`). Estos son empaquetados en unidades de almacenamiento (bytes o palabras) de izquierda-a-derecha o de derecha-a-izquierda, dependiendo de la implementación.

Además, un bit-field puede ser usado como simple padding o separación manual, puede forzar al siguiente bit-field a comenzar en una nueva unidad de almacenamiento, y no se pueden usar sus direcciones de memoria ni crear arreglos.

Ejemplos:
```C
// Representación de fecha compacta.
struct Date {
    unsigned int day   : 5;    // 1-31 (5 bits suficientes).
    unsigned int month : 4;    // 1-12 (4 bits suficientes).
    unsigned int year  : 12;   // 0-4095 (año desde base).
};
// Uso de Date.
struct Date today = {15, 7, 2025};
```

```C
// Diferentes tipos de bit-fields.
struct MixedBitfields {
    signed int   temperature : 8;   // -128 a 127.
    unsigned int humidity    : 7;   // 0 a 127.
    _Bool        valid       : 1;   // true/false.
    unsigned int             : 0;   // Forzar nueva unidad.
    unsigned int checksum    : 8;   // En nueva unidad.
};
// Uso de MixedBitfields.
struct MixedBitfields sensor = {0};
sensor.temperature = -15;
sensor.humidity = 65;
sensor.valid = 1;
sensor.checksum = 0xAB;
```

```C
// Sistema de permisos tipo Unix.
struct Permissions {
    unsigned int owner_read   : 1;
    unsigned int owner_write  : 1;
    unsigned int owner_exec   : 1;
    unsigned int group_read   : 1;
    unsigned int group_write  : 1;
    unsigned int group_exec   : 1;
    unsigned int other_read   : 1;
    unsigned int other_write  : 1;
    unsigned int other_exec   : 1;
    unsigned int              : 7;  // Padding.
};
// Uso de Permissions.
struct Permissions perms = {0};
perms.owner_read = 1;
perms.owner_write = 1;
perms.owner_exec = 1;
perms.group_read = 1;
perms.other_read = 1;
```

### Alignas
Este es un type specifier `alignas` que permite modificar el `alignment requirement` del objeto que está siendo declarado. Solo puede ser usado cuando se declaran objetos diferentes a `bit-fields` o `registers`, no puede ser usado en los parámetros de funciones ni en `typedef`.
```C
alignas(expression)  // Alignment por número.
alignas(type)  // Alignment basado en tipo.
```

Es posible que multiples usos de `alignas` aparezcan en una sola declaración, por lo que se tomará únicamente el que sea más estricto, es decir, es que declare un mayor número.

Ejemplos:
```C
// Alineación por número
alignas(16) char buffer[64];  // Alineado a 16 bytes.
alignas(32) int numbers[10];  // Alineado a 32 bytes.
```

```C
// Alineación por tipo
alignas(double) char data[100];  // Alineado igual que double.
alignas(long long) int value;  // Alineado igual que long long.
```

```C
// Se toma el alignment más estricto (32 bytes).
alignas(8) alignas(32) alignas(16) char strict_buffer[128];
```

El tamaño de un objeto se puede ver afectado por el uso de `alignas`, pues cambia el `alignment requirement` de un objeto, lo que provoca que el compilador agregue padding y ajuste el tamaño final de dicho objeto para que sea múltiplo del `alignment requirement`, permitiendo un acceso consistente, parejo y exacto del objeto.

### Typedef declaration
La declaración usando `typedef` proporciona una forma de declarar un identificador como un `alias` para ser usado como reemplazo de otros tipos. Su uso no afecta el storage ni el linkage.
```C
typedef int int_t;
typedef char* String;
```

Cada declarador donde se usa typedef define un nuevo identificador que actúa como un alias de un tipo específico, pero es imporante notar que no pueden ser `static` ni `extern`. El uso de esto no introduce un nuevo tipo, sino sinónimos a los tipos existentes, por lo que ambos tipos son compatibles entre sí.

 Ejemplos:
```C
// Aliases para tipos primitivos.
typedef int Age;
typedef double Temperature;
typedef char* String;

// Uso de los aliases.
Age person_age = 25;
Temperature room_temp = 22.5;
String message = "Hello";
```

```C
// Con typedef.
typedef struct Point {
    int x, y;
} Point;
Point p1 = {30, 40};  // No necesita "struct".

// Typedef anónimo (más común).
typedef struct {
    int x, y;
} Point;
Point p2 = {30, 40};  // No necesita "struct".
```

Este especificador únicamente puede establecer sinónimos para diferentes tipos de datos, es decir, otros identificadores o nombres. Por lo tanto, no puede usar `storage-class specifiers` porque no crea objetos nuevos, únicamente identificadores que son reemplazados por el tipo real.

### Static assertion
La función `static_assert()` sirve para evaluar condiciones en tiempo de compilación, por lo que si la condición es false, el programa no compila y devuelve el mensajes especificado.

Sin embargo, solo puede usar expresiones constantes, es decir, valores que son conocidos en el momento de la compilación, y detiene la compilación únicamente si la condición es `false` o `0`.

Ejemplos:
```C
// Verificar tamaños de tipos.
static_assert(sizeof(int) == 4, "int debe ser de 4 bytes");
static_assert(sizeof(char) == 1, "char debe ser de 1 byte");
```

```C
// Asegurar que el sistema es compatible.
static_assert(sizeof(void*) == 8, "Solo sistemas de 64 bits soportados");
static_assert(CHAR_BIT == 8, "Se requieren 8 bits por byte");
```

### Atomic types
El concepto de tipos atómicos se refiere a tipos cuyas operaciones se realizan atómicamente, es decir, que se realizan todas las operaciones que se tengan que hacer ininterrumpidamente o ninguna se hace, lo que garantiza que nunca habrá errores de carrera (race conditions).

Por lo tanto, en C, los objetos de tipo `_Atomic` son los únicos objetos que pueden estar completamente libres de `data races` o errores de carrera. Cada objeto de este tipo tiene asociado su propio `modification order`, que se refiere al orden total de modificaciones realizadas a ese objeto.

```C
#include <stdatomic.h>

// Forma 1: Usando _Atomic.
_Atomic int counter = 0;
_Atomic bool ready = false;

// Forma 2: Usando tipos predefinidos (equivalente).
atomic_int counter2 = 0;
atomic_bool ready2 = false;
```

#### Modification order
Si la modificación `A` en el objeto `M` pasa antes que la modificación `B` en el mismo objeto `M`, en el orden de modificación de `M` es: `A` sucede antes que `B`. Además, cada objeto atómico tiene un único orden total, pero múltiples hilos pueden observar modificaciones a un objeto atómico en distino orden, es decir, desde diferentes puntos en el tiempo dentro de ese orden único.

#### Coherence guarantees
Hay cuatro tipos de coherencia garantizados para todas las operaciones atómicas (en pares):
* `write-write coherence`: Si una operación A que modifica al objeto M sucede antes de una operación B que modifica al objeto M, entonces A aparece antes que B en el modification order.
* `read-read coherence`: Si una operación de lectura A del objeto M sucede antes de una operación de lectura B del objeto M, y A toma el valor de una escritura X, entonces el valor usado por B es tomado de X o de otra escritura Y, donde Y aparece después de X en el modification order.
* `read-write coherence`: Si una operación de lectura A del objeto M sucede antes de una operación B que modifica al objeto M, entonces A toma el valor de una escritura X, donde X aparece antes que B en el modification order.
* `write-read coherence`: Si una operación A que modifica al objeto M sucede antes de una operación de lectura B, entonces B toma el valor de la operación A o de alguna otra escritura X que aparezca después de A en el modification order.

#### Main atomic functions
* `atomic_store()`: Escritura atómica.
    ```C
    atomic_store(&var, 42)
    ```
* `atomic_load()`: Lectura atómica.
    ```C
    int x = atomic_load(&var)
    ```
* `atomic_fetch_add()`: Suma atómica.
    ```C
    atomic_fetch_add(&var, 1)
    ```
* `atomic_fetch_sub()`: Resta atómica.
    ```C
    atomic_fetch_sub(&var, 1)
    ```
* `atomic_compare_exchange_strong()`: Comparar y cambiar (swap).

### Memory ordering
Las operaciones atómicas no establecen un orden de ejecución, pues su ejecución es secuencial y artitrario, por lo que simplemente aseguran que las operacinoes relacionadas con un objeto de tipo atómico ocurran antes de pasar a la siguiente operación, además, establecen garantías de qué hacer cuando una operación se da antes que otra.

Por lo tanto, `memory ordering` soluciona este problema al poder indicar el orden de ejecución de operaciones de escritura y lectura:
* `memory_order_relaxed`: Asegura únicamente que la operación se realizará atómicamente, sin importar o establecer un orden de ejecución.
    ```C
    atomic_store_explicit(&var, val, memory_order_relaxed)
    ```
* `memory_order_release`: Asegura que todas las operaciones anteriores se terminen de ejecutarpara poder ejecutar la operación atómica especificada.
    ```C
    atomic_store_explicit(&var, val, memory_order_release)
    ```
* `memory_order_acquire`: Asegura que todas las operaciones posteriores a la operación atómica sean ejecutadas únicamente cuando la operación atómica especificada sea ejecutada.
    ```C
    atomic_load_explicit(&var, memory_order_acquire)
    ```
* `memory_order_seq_cst`: Asegura las máximas garantías y es la opción por default.
    ```C
    atomic_store_explicit(&var, val, memory_order_seq_cst)
    ```

### External and tentative definitions
A alto nivel de una unidad de traducción, todos los programas en C son una secuencia de declaraciones, que declaran funciones y objetos con linkage externo e interno. Este tipo de declaraciones son conocidas como *external declarations* porque aparecen afuera de cualquier función.

Los objetos que son declarados externamente tienen `static storage duration`, por lo que no pueden usar los especificadores `auto` o `register`. Pero los identificadores introducidos por declaraciones externas tienen un alcance a nivel de archivo.

#### External declarations/definitions
Las declaraciones/definiciones externas son aquellas que aparecen fuera de cualquier función y pueden tener linkage externo o linkage interno. Todas se caracterizan por:
* Tener static storage duration (existen durante toda la vida del programa).
* Tienen file scope (visibles desde su declaración hasta el final del archivo).
* Pueden tener linkage externo (accesibles desde otros archivos) o interno (accesibles solo desde el archivo actual).

Ejemplos:
```C
// Archivo: globals.c
// External declaration con linkage externo (definición real).
int global_counter = 0;

// External declaration con linkage interno (static).
static int internal_counter = 100;

// External declaration de función.
void increment_counters(void);
```

```C
// Archivo: main.c
// External declaration que referencia la variable en globals.c.
extern int global_counter;

// Declaración de función externa
extern void increment_counters(void);
```

#### Tentative declarations/definitions
Una `tentative definition` es una declaración externa sin un inicializador, que puede actuar o no como una definición, pues si sí existe una definición real, entonces actúa únicamente como una declaración. Pero, en caso contrario, actúa como una definición con inicialización automática a cero.

Todas estas siguen las siguientes reglas:
* **Sin inicializador**: No usan inicializadores, pues originalmente actúan solo como declaraciones.
* **Comportamiento condicional**: Se convierten en definiciones reales solo si no existen otras definiciones reales.
* **Inicialización automática**: Si se convierten en definiciones, se inicializan automáticamente a cero.
* **Múltiples tentativas**: Se puede tener múltiples declaraciones tentativas del mismo identificador.

Ejemplos:
```C
// Tentative definition (se convierte en definición real inicializada a 0).
int current_users;
```

```C
int problematic = 10;   // Definición real.
int problematic = 20;   // ERROR: Redefinición.
```

### Attributes
C23 introdujo el concepto de atributos definidos por la implementación para tipos, objetos, expresiones, etc. Los atributos proveen una sintáxis estándar unificada para implementaciones definidas.

Un atributo puede ser usador casi en cualquier parte de un programa en C, y puede ser aplicado en casi cualquier cosa: tipos, variables, funciones, nombres, bloques de códigos, archivos enteros, etc. Además, en las declaraciones, los atributos pueden aparecer antes de la declaración o después del identificador introducido, en cuyo caso son simplemente combinados.

Ejemplos:
```C
// Uso de los atributos.
[[attribute-token]]  // Uso de atributo sin argumentos.
[[attribute-token(arguments)]]  // Uso de atributo con argumentos.
[[attribute-token1, attribute-token2]]  // Uso de múltiples argumentos.
```

```C
// Posicionamiento de los atributos.
[[deprecated]] void old_function(void);  // Antes de la declaración.

void old_function [[deprecated]] (void);  // Después del identificador.

void process(int data [[maybe_unused]]);  // En parámetros.

[[maybe_unused]] static int debug_counter = 0;  // En variables.
```

El estándar de C únicamente define los siguientes atributos:
* `[[deprecated]]` o `[[deprecated("reason")]]`: Indica que el uso del nombre o entidad declarada con este atributo está permitido, pero no se recomienda hacerlo.
* `[[fallthrough]]`: Indica que el fall-through de un case es intencional y no debe ser diagnosticado como advertencia.
* `[[nodiscard]]` o `[[nodiscard("reason")]]`: Ayuda al compilador a mostrar una advertencia y el valor retornado no es usado.
* `[[maybe_unused]]`: Elimina advertencias del compilador si hay entidades sin usar.
* `[[noreturn]]`: Indica que la función no retorna un valor (termina el programa o transfiere control permanentemente).
* `[[unsequenced]]`: Indica que una función no tiene estado, no tiene efectos secundarios, es idempotente e independiente.
* `[[reproducible]]`: Indica que una función no tiene efectos secundarios y es idempotente (pero puede depender del estado del programa).

#### Attribute detection
Se pueden hacer chequeos para detectar la presencia de atributos usando `__has_c_attribute()`. Ejemplos:
```C
// Macros condicionales basadas en soporte de atributos.
#if __has_c_attribute(nodiscard)
    #define MUST_USE [[nodiscard]]
#else
    #define MUST_USE  // Sin atributo si no está soportado.
#endif

#if __has_c_attribute(deprecated)
    #define OBSOLETE(msg) [[deprecated(msg)]]
#else
    #define OBSOLETE(msg)  // Sin atributo si no está soportado.
#endif
```

```C
// Uso de las macros.
MUST_USE int critical_calculation(int x, int y) {
    return x * y + (x - y);
}

OBSOLETE("Use safe_copy instead") 
char* unsafe_copy(char* dest, const char* src) {
    return strcpy(dest, src);
}
```

## Functions
Una función en C es un constructo que asocia un conjunto de sentencias (bloque de código) con un identificador (nombre de la función). Todo programa en C inicia con la ejecución de la función `main`, que determina o incova otras funciones definidas por el usuario.

Las funciones pueden ser introducidas mediante declaraciones o definiciones, y pueden aceptar uno o más parámetros. Los cuales son inicializados desde los argumentos de la llamada de dicha función, incluso, puede retornar cualquier valor (no arrays ni funciones) al punto de su llamada.
```C
int main(int argc, char *argv[]) {
    // Código escrito por el usuario.
}
```

### Function declarations
La declaración de una función introduce un identificador que designa una función, y opcionalmente, especifica los tipos de los parámetros de dicha función. A diferencia de la definición de una función, estas pueden aparecer a nivel de bloque y a nivel de archivo.
```C
int foo(int a, int b);  // Introduce el identificador foo.
```

Por otro lado, los parámetros de una declaración de una función se comportan diferente a los de una definición de una función:
* Los identificadores de los parámetros no son obligatorios.
    ```C
    int f(int, double);  // OK.
    int g(int a, double b); // OK.
    ```
* No se permiten `storage-class specifiers` (solo `register`).
    ```C
    int f(static int x);  // Error.
    int f(int int x[static 10])  // OK, static no actúa como storage-class specifier.
    ```
* Cualquier parámetro de tipo array es convertido a su tipo de puntero correspondiente.
    ```C
    int f(int []);  // OK, se convierte a int f(int*).
    int g(const int[10]);  // OK, se convierte a int g(const int*).
    int x(int[*]);  // OK, se convierte a int x(int*).
    ```
* Cualquier parámetro de tipo función es convertido a su tipo de puntero correspondiente.
    ```C
    int f(char g(double));  // OK, se convierte a int f(char (*g)(double)).
    int h(int(void));  // OK, se convierte a  int h(int (*)(void)).
    ```
* La lista de parámetros puede ser o terminar con `...`.
    ```C
    int f(int, ...);  // OK.
    ```
* Los parámetros de tipo `void` no pueden tener identificadores.
    ```C
    int f(void);  // OK.
    int g(void x);  // Error.
    ```
* *Nota: Las declaraciones tipo `f()` y `f(void)` NO son iguales. Pues `f()` declara que una función recibe un número desconocido de parámetros; mientras que `f(void)` declara que una función no recibe ningún parámetro.*

### Function definitions
La definición de una función asocia el cuerpo de la función con el identificador (nombre de la función) y con su lista de parámetros. A diferencia de una declaración, cualquier definición de función es permitida únicamente a nivel de archivo, por lo que no existen las funciones anidadas en C.
```C
int max(int a, int b) {
    return a > b ? a:b;
}
```

De la misma forma que las declaraciones, las definiciones de funciones el valor de retorno debe ser un objeto completo diferente a un array o función. También, los parámetros de tipo array o tipo función, son convertidos a sus tipos de punteros correspondientes, y los parámetros tipo `void` no pueden ser nombrados. Sin embargo, todos los parámetros que van a ser usados dentro de la función deben ser nombrados, pero sí es posible declarar parámetros sin nombres.
```C
int f(int a, int b) { return 7; }  // OK, definición de una función.
int g(int, int) { return 8; }  // OK, permitido desde C23.
int h(void) { return 9; }  // OK, no declara parámetros.
```

### Inline function specifier
Una función inline en C cumple con dos propósitos principales:
* Optimización: Indicar al compilador que debe sustituir las llamadas de dicha función por el cuerpo de la función, con el objetivo de evitar overhead (eliminar el costo de llamada/retorno y uso del stack).
* Linkage especial: Cambiar el comportamiento del linkage para permitir múltiples definiciones idénticas en diferentes archivos sin causar errores.

La intención de usar `inline` es servir como sugerencia al compilador para realizar optimizaciones que requieren que la definición completa de la función sea visible en el punto de llamada. Importante: `inline` es una sugerencia, no una orden, el compilador puede ignorarla si considera que no es beneficiosa.
```C
inline int cuadrado(int x) { 
    return x * x; 
}

int main() {
    int resultado = cuadrado(5);  // Puede ser reemplazado por: int resultado = 5 * 5;
    return 0;
}
```

El resultado es similar a las macros de tipo función, pero con importantes diferencias, pues los identificadores y variables en una función inline hacen referencia a las definiciones visibles en el punto de definición de la función, no en el punto de llamada.
```C
#define MACRO_CUADRADO(x) ((x) * (x))
inline int inline_cuadrado(int x) { return x * x; }

int main() {
    int i = 5;
    // La macro evalúa x dos veces (problema con efectos secundarios).
    int resultado1 = MACRO_CUADRADO(++i);  // i se incrementa dos veces.

    i = 5;
    // La función inline evalúa el parámetro una sola vez.
    int resultado2 = inline_cuadrado(++i);  // i se incrementa solo una vez.

    return 0;
}
```

Cuando se usa solo `inline`, el compilador puede hacer inline (sustituir la llamada por el código, no genera función externa) o no hacer inline (Generar una función normal disponible externamente). Pero, cuando se combina con `static`, garantiza que cada archivo tenga su propia versión local.

Por otro lado, el compilador puede ignorar inline cuando:
* La función es muy grande (aumentaría demasiado el tamaño del código).
* La función es recursiva.
* Se toma la dirección de la función (puntero a función).
* El compilador determina que no hay beneficio de rendimiento.

### Variadic arguments
Las funciones variádicas son funciones que pueden ser llamadas con una cantidad diferente de argumentos. Esto es indicado con el parámetro en forma `...`, el cual debe aparecer al final de la lista de parámetros y debe haber al menos un parámetro fijo antes de los `...`.
```C
int printf(const char *format, ...);  // Función variádica estándar.
int suma(int count, ...);             // count indica cuántos números seguirán.
int max(int first, ...);              // Al menos un argumento fijo requerido.
```

Cada argumento que forma parte de la lista de argumentos variables pasa por conversiones implícitas automáticas:
* `char` y `short` -> `int`
* `float` -> `double`
* `array` -> `pointer`
* `function` -> `pointer`

Para acceder a los argumentos variables, se utilizan las siguientes herramientas de `<stdarg.h>`:
* `va_list`: Tipo que contiene la información necesaria para acceder a los argumentos variables.
* `va_start(ap, last_fixed)`: Inicializa `ap` para acceder a los argumentos variables. `last_fixed` es el último parámetro fijo.
* `va_arg(ap, type)`: Obtiene el siguiente argumento de tipo `type` y avanza `ap`.
* `va_copy(dst, src)`: Copia el estado de `src` a `dst` (útil para múltiples pasadas).
* `va_end(ap)`: Limpia y finaliza el uso de `ap`.

Ejemplos:
```C
// Declarar variable para argumentos con va_list.
void ejemplo_va_list(int count, ...) {
    va_list argumentos;  // Esta variable contendrá la info de los argumentos.
    printf("va_list declarado correctamente\n");
}
```

```C
// Inicializar acceso a argumentos con va_start.
void ejemplo_va_start(int count, ...) {
    va_list args;
    va_start(args, count);  // Inicializa args, count es el último parámetro fijo.
    printf("Acceso a argumentos inicializado\n");
    va_end(args);
}
```

```C
// Obtener el siguiente argumento con va_arg.
void ejemplo_va_arg(int count, ...) {
    va_list args;
    va_start(args, count);
    int primer_numero = va_arg(args, int);  // Obtiene el primer argumento como int.
    int segundo_numero = va_arg(args, int);  // Obtiene el segundo argumento como int
    printf("Primer número: %d, Segundo número: %d\n", primer_numero, segundo_numero);
    va_end(args);
}
```

```C
// Copiar argumentos para usar dos veces con va_copy.
void ejemplo_va_copy(int count, ...) {
    va_list args_originales, args_copia;
    va_start(args_originales, count);
    va_copy(args_copia, args_originales);  // Copia los argumentos.
    // Usar los originales.
    int suma = va_arg(args_originales, int) + va_arg(args_originales, int);
    // Usar la copia (empezando desde el principio otra vez).
    int producto = va_arg(args_copia, int) * va_arg(args_copia, int);
    printf("Suma: %d, Producto: %d\n", suma, producto);
    va_end(args_originales);
    va_end(args_copia);
}
```

```C
// Limpiar después de usar argumentos.
void ejemplo_va_end(int count, ...) {
    va_list args;
    va_start(args, count);
    int numero = va_arg(args, int);
    printf("Número obtenido: %d\n", numero);
    va_end(args);  // Limpia y finaliza el uso de argumentos.
    printf("Argumentos limpiados correctamente\n");
}
```

