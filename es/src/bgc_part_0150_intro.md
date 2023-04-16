<!-- Beej's guide to C

# vim: ts=4:sw=4:nosi:et:tw=72
-->

# ¡Hola, Mundo!

## Qué esperar de C

> *"¿A dónde van estas escaleras?"*
>
> *"Van hacia arriba".*
>
> ---Ray Stantz y Peter Venkman, Ghostbusters

C es un lenguaje de bajo nivel.

No solía serlo. En el pasado, cuando la gente marcaba tarjetas perforadas en piedra, C era una forma increíble de liberarse de la monotonía de los lenguajes de bajo nivel como [flw[lenguaje ensamblador|Assembly_language]].

Pero ahora, en estos tiempos modernos, los lenguajes de la generaciones actuales ofrecen todo tipo de características que no existían en 1972 cuando se inventó C. Esto significa que C es un lenguaje bastante básico sin muchas características. Puede hacer *cualquier cosa* , pero te hará trabajar para ello.

Entonces, ¿por qué lo seguimos usando?

- Como herramienta de aprendizaje:  C no es sólo una pieza venerable de la historia de la computación, sino que está conectado a [flw[bare metal|Bare_machine]] de una manera que los lenguajes actuales no lo están. Cuando aprendes C, aprendes cómo el software interactúa con la memoria de la computadora a un nivel bajo. No hay cinturones de seguridad. Escribirás software que falla, te lo aseguro. ¡Y eso es parte de la diversión!

- Como herramienta útil: C todavía se usa para ciertas aplicaciones, como construir [flw[sistemas operativos|Sistema_operativo]] o en [flw[sistemas integrados|Sistema_empotrado]]. (¡Aunque el lenguaje de programación [flw[Rust|Rust_(programming_language)]] está mirando estos dos campos!)

Si estás familiarizado con otro lenguaje, muchas cosas sobre C serán fáciles. C inspiró a muchos otros lenguajes, y verás partes de él en Go, Rust, Swift, Python, JavaScript, Java y todo tipo de otros lenguajes. Esas partes te resultarán familiares.

Una peculiaridad  de C que enloquece a la gente son los punteros. Prácticamente todo lo demás es familiar, pero los punteros son los extraños. Es probable que ya conozca el concepto detrás de los punteros, pero C te obliga a ser explícito al respecto, utilizando operadores que probablemente nunca antes hayas visto.

Es especialmente insidioso porque una vez que [flw[ *asimilas* |Asimilar]] los punteros, de repente son fáciles. Pero hasta ese momento, son angulas resbaladizas.

Todo lo demás en C es simplemente memorizar otra forma (o incluso,  a veces ¡la misma forma!) de hacer algo que ya sabías hacer. Los punteros son la parte rara. Y, posiblemente, incluso los punteros son variaciones de un tema con el que probablemente ya estés familiarizado.

Así que prepárate para una divertida aventura lo más cerca posible al corazón de la computadora sin usar ensamblador, en el lenguaje informático más influyente de todos los tiempos^[Sé que alguien peleará conmigo por eso, pero tiene que estar al menos entre los tres primeros, ¿verdad?]. ¡Agárrate!

## ¡Hola, Mundo!

[i [Hola, mundo]() ] Este es el ejemplo canónico de un programa en C. Todo el mundo lo usa. (Ten en cuenta que los números a la izquierda son solo para referencia del lector y no son parte del código fuente).

```{.c
/* Programa Hola Mundo */

#include <stdio.h>

int main(void)
{
    printf("¡Hola, Mundo!\n");  // Aquí es donde se lleva a cabo el trabajo del programa
}
```

Vamos a ponernos nuestros super guantes resistentes de manga larga, agarrar un bisturí y disectar esto para ver qué lo hace funcionar. Así que, prepárate, porque allá vamos. Cortando muy suavemente...

[i[Comentarios]&lt;]Salgamos primero de  lo más fácil: cualquier cosa entre los dígrafos /* y */ es un comentario y el compilador lo ignorará por completo. Lo mismo ocurre con cualquier cosa en una línea después de // . Esto te permite dejar mensajes para tí mismo y para otros, de tal manera que cuando regreses y leas tu código en un futuro lejano, sabrás qué demonios estabas tratando de hacer. Créeme, lo olvidarás; sucede.[i[Comentarios]&gt;]

[i[Preprocesador C]&lt;][i[ La directiva `#include` ]&lt;]Ahora, ¿qué es esto `#include` ? ¡BURDO! Bueno, le dice al preprocesador C que extraiga el contenido de otro archivo y lo inserte en el código *allí* mismo.

Espera, ¿qué es el preprocesador C? Buena pregunta. Hay dos etapas^[Bueno, técnicamente hay más de dos, pero bueno, supongamos que hay dos: la ignorancia es una bendición, ¿no?] para la compilación: el preprocesador y el compilador. [i[Octothorpe]&lt;]Cualquier cosa que comience con el signo de numeral, u "octothorpe", ( `#` ) es algo sobre lo que opera el preprocesador[i[Preprocesador]] incluso antes de que el compilador comience. *Las directivas de preprocesador* comunes, como se les llama, son `#include` y `#define` .[i[ Directiva `#define` ]] Más sobre eso más adelante.[i[ Directiva `#include` ]&gt;][i[C Preprocessor]&gt;]

Antes de continuar, ¿por qué debería molestarme en señalar que el signo de numeral se llama octothorpe? La respuesta es simple: creo que la palabra octothorpe es tan excelentemente divertida que tengo que difundir su nombre gratuitamente cada vez que tengo la oportunidad. octhorpe. Octothorpe, octothorpe, octothorpe.[i[Octothorpe]&gt;]

Así que *de todos modos* Una vez que el preprocesador de C ha terminado de preprocesar todo, los resultados están listos para que el compilador los tome y produzca [flw[código ensamblador|Assembly_language]], [flw[código máquina|Código_máquina]], o lo que sea que esté a punto de hacer. El código de máquina es el "lenguaje" que entiende el CPU, y puede entenderlo *muy rápidamente* . Esta es una de las razones por las que los programas en C tienden a ser rápidos.

No se preocupe por los detalles técnicos de la compilación por ahora; sólo hace falta saber que el código fuente se ejecuta a través del preprocesador, luego la salida de eso se ejecuta a través del compilador, luego eso produce un ejecutable para correrlo.

¿Qué pasa con el resto de la línea? [i[archivo de encabezado `stdio.h` ]&lt;]¿Qué es `<stdio.h>` ? Eso es lo que se conoce como *archivo de cabecera* . Es el punto h al final lo que lo delata. De hecho, es el archivo de encabezado "Standard I/O", Entrada/Salida estándar ( `stdio` ) el que llegarás a conocer y amar. Nos da acceso a un montón de funciones de E/S^[Técnicamente, contiene directivas de preprocesador y prototipos de funciones (más sobre esto más adelante) para necesidades comunes de entrada y salida]. Para nuestro programa de demostración, estamos generando la cadena "¡Hola, mundo!", por lo que en particular necesitamos acceso a la función [i[ `printf()` ]&lt;] `printf()` para hacer esto. El archivo `<stdio.h>` nos da este acceso. Básicamente, si intentáramos usar `printf()` sin `#include <stdio.h>` , el compilador se habría quejado con nosotros.

¿Cómo supe que necesitaba `#include <stdio.h>` para usar `printf()` ?[i[ función `printf()` ]&gt;] Respuesta: está en la documentación. Si estás en un sistema *nix, ejecuta `man 3 printf` y te dirá justo en la parte superior de la página del manual qué archivos de encabezado son necesarios. También puedes ver la sección de referencia en este libro. `:-)` [i[archivo de encabezado `stdio.h` ]&gt;]

Cielos. ¡Eso fue todo para cubrir la primera línea! Pero, seamos realistas, ha sido completamente diseccionada. ¡Nada quedará en el misterio!

Así que toma un respiro... revisa el código de ejemplo. Sólo faltan un par de líneas fáciles.

¡Bienvenido de vuelta de tu descanso! Sé que realmente no te tomaste un descanso; Solo te estaba siguiendo la corriente.

[i[ función `main()` ]&lt;]La siguiente línea es `main()` . Esta es la definición de la función `main()` ; todo lo que está entre las llaves ( `{` y `}` ) es parte de la definición de la función.

(¿Cómo se *llama* a otra función disinta, de todos modos? La respuesta se encuentra en la línea `printf()` , pero llegaremos a eso en un minuto).

Ahora, la función main —principal— es especial en muchos sentidos, pero hay una cosa que la distingue por encima del resto: es la función que se llamará automáticamente cuando tu programa comience a ejecutarse. Nada de tu código se llama antes de `main()` . En el caso de nuestro ejemplo, esto funciona bien ya que todo lo que queremos hacer es imprimir una línea y salir.

Oh, también hay otra cosa: una vez que el programa se ejecuta más allá del final de `main()` , allí abajo en la llave de cierre, el programa se cerrará y volverás a la línea de comandos.

Así que ahora sabemos que ese programa trajo un archivo de encabezado, `stdio.h` [i[stdio.h]T], y declaró una función `main()` que se ejecutará cuando se inicie el programa. ¿Cuáles son las ventajas de `main()` [i[ función`main()`]&gt;]?

Me dá gusto que hayas preguntado. ¡En serio! Solo tenemos un detallito: una llamada a la función [i[ `printf()` function]&lt;] `printf()` . Existen varias maneras para saber que se trata del <em>llamado</em> a una función y no de la definición de una función, un buen indicador es la falta de llaves inmediatamente después. Además finaliza la llamada a la función con un punto y coma para que el compilador sepa que es el final de la expresión. Pondrás punto y coma después de casi todo, como verás.

Estás pasando un argumento a la función `printf()` [i[ función `printf()` ]&gt;]: una cadena que se imprimirá cuando la llames. Oh, sí --- ¡estamos llamando a una función! ¡Somos lo máximo! Espera, espera --- no te pares el cuello aún. [i[ nueva línea`\n` ]&lt;]¿Qué es esa locura `\n` al final de la cadena? Bueno, la mayoría de los caracteres de la cadena se imprimirán tal como están almacenados. Pero hay ciertos caracteres que no se puede imprimir bien en la pantalla que están incrustados como códigos de barra invertida de dos caracteres(dígrafos de barra invertida). Uno de los más populares es `\n` (léase "barra invertida-N" o simplemente "línea Nueva") que corresponde al carácter de *línea nueva * . Este es el carácter que hace que la impresión continúe al comienzo de la siguiente línea en lugar de la actual. Es como presionar INTRO al final de la línea.[i[ `\n` línea Nueva]&gt;]

Así que copia ese código en un archivo llamado `hola.c` y compílalo. En una plataforma similar a Unix (p. ej., Linux, BSD, Mac o WSL), desde la línea de comandos  se compilará con un comando como este:

[i[compilador `gcc` ]]

```{.zsh}
gcc -o hola hola.c
```

(Esto significa "compilar `hola.c` y generar un ejecutable llamado `hola` ".)

Una vez hecho esto, deberías tener un archivo llamado `hola` que puedes ejecutar con este comando:

```{.default}
./hola
```

(El `./` inicial le dice al shell que "se ejecute desde el directorio actual".)

Ahora veamos lo que pasa:

```{.default}
¡Hola, Mundo!
```

¡Está hecho y probado! ¡Envíalo![i[Hola, mundo]&gt;]

## Detalles de la compilación

[i[Compilación]&lt;]Hablemos un poco más sobre cómo crear programas en C y qué es lo que sucede tras bambalinas.

Como otros lenguajes, C tiene *código fuente* . Pero, según el lenguaje del que provengas, es posible que nunca hayas tenido que *compilar* tu código fuente en un *archivo ejecutable* .

La compilación es el proceso de tomar el código fuente, en este caso en C y convertirlo en un programa que tu sistema operativo pueda ejecutar.

Los desarrolladores de JavaScript y Python no están acostumbrados a un paso de compilación por separado, ¡aunque detrás de escena está sucediendo! Python compila su código fuente en algo llamado *bytecode* que la máquina virtual de Python puede ejecutar. Los desarrolladores de Java están acostumbrados a la compilación, pero eso produce bytecode  para la máquina virtual de Java.

Al compilar C, se genera *código máquina* . Estos son los 1 y 0 que el CPU puede ejecutar directa y rápidamente.

> Los lenguajes que normalmente no se compilan se denominan lenguajes *interpretados* . Pero, como mencionamos con Java y Python, también tienen una etapa de compilación. Y no hay ninguna regla que diga que C no se puede interpretar. (¡Hay intérpretes de C por ahí!) En resumen, hay bastantes áreas grises. La compilación en general es sólo tomar el código fuente y convertirlo en otra forma más fácil de ejecutar.

El compilador de C es el programa que hace la compilación.

Como ya dijimos, `gcc` es un compilador que está instalado en muchos [flw[sistemas operativos similares a Unix|Unix]]. Y normalmente se ejecuta desde la línea de comandos en una terminal, pero no siempre. También puedes ejecutarlo desde una IDE.

Entonces, ¿cómo hacemos compilaciones desde la línea de comandos?

## Compilando con `gcc`

[i[compilador `gcc` ]&lt;]Si tienes un archivo fuente llamado `hola.c` en el directorio actual, puedes compilarlo en un programa llamado `hola` con este comando escrito en la terminal:

```{.zsh}
gcc -o hello hello.c
```

El parámetro `-o` significa "salida (del inglés output) a este archivo"^[Si no le da un nombre de archivo de salida, se exportará a un archivo llamado `a.out` por defecto---este nombre de archivo tiene sus raíces muy profundizadas en la historia de Unix.]. Y al final está `hello.c` , el nombre del archivo que queremos compilar.

Si la fuente está dividida en varios archivos, se pueden compilar todos juntos (casi como si fueran un solo archivo, pero las reglas erán en realidad más complejas que eso) colocando todos los archivos `.c` en la línea de comando:

```{.zsh}
gcc -o juegogenial ui.c personajes.c npc.c elementos.c
```

[i[compilador `gcc` ]&gt;]

y todos se compilarán juntos en un solo y gran ejecutable.

Eso es suficiente para comenzar --- más adelante hablaremos sobre los detalles de varios archivos fuente, archivos de objetos y todo tipo de cosas divertidas.[i[Compilación]&gt;]

## Compilando con `clang`

En Mac, el compilador estándar no es `gcc` , es `clang` [i[ compilador `clang` ]]. Pero también hay  un envoltorio para que pueda ejecutar `gcc` y hacerlo funcionar.

También puede instalar el compilador `gcc` [i[ `gcc` compiler]] a través de [fl[Homebrew|https://formulae.brew.sh/formula/gcc]] o por algún otro medio.

## Compilando desde IDEs

[i[Entorno de desarrollo integrado]&lt;]Si está utilizando un *Entorno de desarrollo integrado* (IDE), probablemente no sea necesario compilar desde la línea de comandos.

Con Visual Studio, se compilará con `CTRL-F7` y se ejecutará con `CTRL-F5` .

En VS Code, se puede presionar `F5` para ejecutar a través del depurador. (Es necesario instalar la extensión C/C++).

Con XCode, se puede compilar con `COMMAND-B` y ejecutar con `COMMAND-R` . Para obtener las herramientas de línea de comandos, busca en Google "herramientas de línea de comandos XCode" y encontrarás instrucciones para instalarlas.

Para comenzar, te invito  a que también intentes compilar desde la línea de comando --- ¡es historia! [i [Entorno de desarrollo integrado]&gt;]

## Versiones de C

[i[Versiones de lenguaje]&lt;]C ha recorrido un largo camino a lo largo de los años, y ha tenido varios números de versión con nombre para describir qué dialecto del lenguaje se está usando.

Estos generalmente se refieren al año de la especificación.

Los más famosos son C89, C99, C11 y C2x. Nos centraremos en el último en este libro.

Aquí hay una tabla más completa:

Versión | Descripción
--- | ---
K&amp;R C | 1978, el original. Lleva el nombre de Brian Kernighan y Dennis Ritchie. Ritchie diseñó y codificó el lenguaje, y Kernighan fue coautor del libro sobre el mismo. Rara vez verás el código K&amp;R original hoy. De hacerlo, se verá extraño, como el inglés medieval se ve extraño para los lectores de inglés moderno.
**C89**, ANSI C, C90 | En 1989, el American National Standards Institute (ANSI) produjo una especificación del lenguaje C que marcó la pauta para C, la cual persiste hasta el día de hoy. Un año más tarde, las riendas fueron entregadas a la Organización Internacional de Normalización (ISO) que produjo el idéntico C90.
C95 | Una adición rara vez mencionada a C89 que incluía soporte para caracteres multibyte (caracteres ampliados).
**C99** | La primera revisión mayor con muchas adiciones al lenguaje. Lo que la mayoría de la gente recuerda es la adición de comentarios de estilo `//` . Esta es la versión más popular de C en uso a partir de este escrito.
**C11** | Esta actualización de versión principal incluye compatibilidad con Unicode y procesos multihilo. Es necesario tener en cuenta que si se comienzan a usar estas funciones del lenguaje, es posible que se esté sacrificando la portabilidad con lugares que están atrapados en el espacio de C99. Pero, sinceramente, 1999 está quedando cada día mas en el pasado.
C17, C18 | Actualización de corrección de errores de la versión C11. C17 parece ser el nombre oficial, pero la publicación se retrasó hasta 2018. Por lo que hasta donde sé, estos dos son intercambiables, sin embargo se prefiere C17.
C2x | ¡Lo qué viene después! Se espera que con el tiempo se convierta en C23.

[i[compilador `gcc` ]&lt;]Se puede obligar a GCC a usar uno de estos estándares con el argumento de línea de comandos `-std=` . Si se desea que sea exigente con el estándar, agregue `-pedantic` .

Por ejemplo:

```{.zsh}
gcc -std=c11 -pedantic foo.c
```

Para este libro, compilo los programas para C2x con todas las advertencias configuradas:

```{.zsh}
gcc -Wall -Wextra -std=c2x -pedantic foo.c
```

[i[compilador `gcc` ]&gt;]
