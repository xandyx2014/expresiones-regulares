
## Caracteres literales
-  Caracteres literales
- Metacaracteres
- Comodines para los metacaracteres
- Secuencias de escape
-  Otros caracteres especiales

Los caracteres “literales”, son las expresiones regulares más sencillas.
La letra “a” empata con la letra “a”
```txt
/agua/ empata con “agua”
/agua/ empata con “aguacate”
/agua/ empata con “Nicaragua”
```

Son sensible a mayúsculas y minúsculas o casesensitive por omisión:
/agua/ no encuentra AGUA
Se puede modificar con la letra “i”
/agua/i si encuentra AGUA

Los espacios si cuentan:
/agua/ no encuentra a g u a
Por omisión, las regex no se encuentran en modo “global”
Por omisión, sólo encuentra la primer coincidencia si no existe el modificador
“global”
/agua/g encuentra en “agua pasa por mi casa, aguacate de mi corazón”
En el modo “global”, encuentra todas las coincidencias.

## Metacaracteres

`\ . * + - [] {} ^ $ | ? () : ! =`

Puede haber cambios dependiendo del motor “regex”
Pueden tener más de un uso, depende de su contexto.

```txt

^ Inicio la regex
$ Fin de la regex
{} Repetición
() Agrupamiento
```

- `*` Coincide con el elemento anterior cero o más veces.
- `+` Coincide con el elemento anterior una o más veces.
- `?` Coincide con el elemento anterior cero veces o una vez.

- `.` Un caracter cualquiera, excepto salto de línea
- `\` Escape
- `|` Elementos alternos
- `!` Negación
Se utilizan con otros metacaracteres:
- `-`
- `:`
- `=` 

## metacaracteres comodin

```txt
. (punto) cualquier caracter excepto el salto de línea

/man./ empata con “mana” “mano” “manx”

/9.99/ empata con “9.99”. “9999”, “9x99”, “9 99”

Para validar el salto de línea con el comodín punto usamos el modificador “s”

/9.99/s
/.a.a.a/ banana papaya *a*a*a
```
## secuencias de escape
```txt

\ Con la diagonal invertida (backslash) escapamos a los metacaracteres

```
La diagonal invertida no “escapa” a las literales, sólo metacaracteres.
Las comillas no “escapan” metacaracteres.
```
\.
/9\.99/
/foto.\.jpg/ empata con foto1.jpg foto2.jpg, pero no foto33.jpg

El espacio no es caracter especial.
Un espacio debe coincidir con otro espacio.
Para representar un tabulador utilizamos \t
Retornos de línea \r, \n, \r\n+
escape \e
cambio de página \f
tabulador vertical \v
```
Caracteres ASCII o ANSI:
```
0xA9 = \xA9
/a g u a/ empata con “a g u a” pero no con “a_g_u_a” ni “a*g*u*a”
```
## Conjunto de caracteres
Definir un conjunto de caracteres
- Rango de caracteres
- Conjunto negativo de caracteres
- Metacaracteres dentro de los conjuntos de caracteres
- Abreviaciones conjunto de caracteres
- Expresiones de corchetes POSIX
### definir un conjunto de caracteres
```txt
Podemos definir un conjunto de caracteres por medio de los “corchetes”
(Square Brackets) 
[ ]
/[aeiou]/
/[áéíóú]/
```
Sólo evalúa caracteres, no palabras.
El orden de los caracteres no importa.
```
/m[aeiu]sa/ 
empata con “masa”, “mesa”, “misa” y “musa” no con “mosa” porque la o no esta incluida
```
## Rango de caracteres

Por medio del renglón medio” (-) podemos abreviar los rangos de caracteres, por
ejemplo:
`[A-Z]`
Representan todos los caracteres entre ambos.
Debes escribirse en orden. No es válido
`[Z-A]`

Sólo utilizamos caracteres, no conjunto de caracteres:
`[40-45]`
No representa de 40 a 45, sino 4, de 0 a 4 y 5.
Podemos escribir diferentes grupos de caracteres:
`[A-Za-z0-9]`
> No incluye vocales acentuadas, eñes, etc., sólo las letras del abecedario inglés.
```
Prueba [á-ü]
[50-60] mal !!
[A-Z] ola
[0-9][0-9]-[0-9][0-9]-[0-9][0-9]-[0-9][0-9]-[0-9][0-9]
[0-9][0-9][0-9][0-9][0-9]
```
## Conjunto negativo de caracteres
El caracter `^` (circunflejo) dentro de los corchetes es una negación de uno de los
conjuntos de caracteres.
“Ninguno de los caracteres marcados”
Se escribe al inicio, dentro del conjunto de caracteres:
```
[^aeiou]
[^"#$%&/()=*]
```
## Metacaracteres dentro de los conjuntos de caracteres
Los metaracteres dentro de los conjuntos de caracteres ya están “escapadas”.
No hay necesidad de “escaparlos” nuevamente.
```
m[ao.xcv]lo malo, m.lo, pero no mulo
Los siguientes metacaracteres si hay que “escaparlos”
] - ^ \
Si queremos usar :
var[[(][0-9][\])] por ejemplo var(9) var[9]
var[ [ ( ] [0-9] [ \] \) ]
```
El puntoo ya esta escapado si esta dentro de un ranngo
## abreviaciones condjunto de caracteres
```
Abreviaciones conjunto de caracteres
\d Dígitos [0-9]
\w Caracteres [a-zA-Z0-9_] (no incluye el punto)
\s Espacios en blanco [ \t\r\n]
\D No dígito [^0-9]
\W No caracteres [^a-zA-Z0-9_]
\S No espacios en blanco [^ \t\r\n]
```
```
[\d\s]
[^\d\s] Diferente a...
[\D\S] Diferente a...
Soportado por PERL
No soportado por Unix
```
## Expresiones de repeticion
Metacaracteres de repetición
- Cuantificadores de repetición
- Expresiones “codiciosas” (Greedy)
- Expresiones “flojas” (Lazy)
- Utilizar las repeticiones en forma eficiente

`*` cero o más veces del elemento precedente
`+` una o más veces del elemento precedente
`?` cero o una vez (opcional) del elemento precedente
```
/aguas*/ empata aguassss, aguas, agua
/aguas+/ aguas, aguasssssss, no agua
/aguas?/ aguas, agua, no aguassssss
/\d\d\d\d*/ tres dígitos o más
/\d\d\d+/ tres dígitos o más
/Jes+ica/ Jesica, Jessica
/\w+s/ palabras que terminen en ese
```
## Cuantificadores de repeticion
`{}` lo que está antes de las llaves debe aparecer exactamente esa cantidad
de veces
`{min,max}` --> lo que está antes tiene que aparecer entre esas cantidades
(ambas inclusive)
`{min,}` definimos un mínimo, no un máximo, tiene que aparecer desde esa
cantidad de veces.

- min y max deben ser positivos
- min siempre es incluido y puede ser cero
- max es opcional
```
\d{4,8}
\d{4}
\d{4,}
\d{3}-\d[3}-\d{2}
\d{0,} es igual a \d*
\d{1,} es igual a \d+
A{1,3} empata con A, AA, AAA pero no AAAA
```
## Expresiones codiciosas
Las expresiones regulares son “codiciosas” (greedy) porque siempre van a
seleccionar la cadena más grande.
```
<p>(.*)<\/p>
<p>en el agua clara, que brota en la fuente</p> <p> un lindo pescado, sale de
repente</p>
Codicioso Perezoso
(.*)      (.*?)
(.+)      (.+?)
(?)       (??)
```
## Expresiones perezosas
Para hacer a las expresiones regulares ya no sean “codiciosas”, las podemos
hacer perezosas:
```
Codicioso Perezoso
(.*)     (.*?)
(.+)     (.+?)
(?)      (??)
{min.max} {min,max}?
```


## utiliza las repeticiones en forma eficiente

```
/\w+s/
El metacaracter “+” es más eficiente que “*”
Las llaves {} son más eficientes que “+” y “*”
Delimitar las búsquedas con delimitadores (^$) es más eficiente
```
## Agrupay y alternar expresiones
Metacaracteres para agrupar expresiones
- Metacaracteres para alternar
- Escribir alteraciones en forma eficientes y lógicas
- Repeticiones y anidaciones de alteraciones
## Metacaracteres para agrupar expresiones
Por medio de los paréntesis `( )` podemos agrupar expresiones.
Por medio de los paréntesis podemos:
- Aplicar operadores de repetición a grupos.
- Hacer las expresiones más legibles.
- “Capturar” un grupo para empatar o reemplazar.
- No podemos agrupar dentro de un conjunto de caracteres `[()]`
```
(in)?dependiente
color(es)?
```
## MEtacaracteres para alternar
Por medio del metacaracter `|` (pipe o línea vertical) podemos alternar
expresiones.
- Empata expresiones de izquierda a derecha.
- Tiene precedencia las expresiones de la izquierda.
- Por lo general alternamos expresiones dentro de paréntesis.
- En este caso son expresiones, no caracteres.
```
o(bs|s)curo
(pera|manzana)s
```
## Escribir alteraciones en forma eficientes y lógicas
```
Las expresiones regulares son “codiciosas” (greddy)
También son “ansiosas” (eager):
(agua|aguacate)
Es mejor escribir:
agua(cate)?
```
## Repeticiones y anidaciones de alternativas
```
Repeticiones:
([A-Z]|[a-z]|[0-9]){3}
Valido
AAA
aaa
333
Anidaciones:
(jugo (manzana|pera)|agua (naranja|fresa|sandia)|agua(cate)?)
Valido:
jugo manza
jugo pera
agua naranja
agua fresa
INvalido:
agua horchata.
```
## Delimintadores de expresiones
- Iniciar y terminar las expresiones regulares
- Salto de líneas y modo multilíneas
- Delimilatores de palabras
## Iniciar y terminar las expresiones regulares
Los metacaracteres con los cuales podemos delimitar una expresión
regular son:
- `^` Inicio de la expresión
- `$` Fin de la expresión
- `\A` Inicio de la expresión, nunca fin de la línea
- `\Z` Fin de la expresión, nunca fin de la línea

- Refieren una posición, no un caracter:
- `^` y `$` es soportado por todos los motores
- `\A` y `\Z` sólo es soportado por Java, .NET, Perl, Python, PHP y Ruby
- `\A` y `\Z` no es soportado por JavaScript y algunas herramientas de UNIX
```
/agua/g
```
## Salto de lineas y modo multilineas
El modo de línea sencilla está activo por omisión.
- Puede activar el modo de línea múltiple por medio del modificador “m”.
- `^`y `$` no empatan con el fin de línea.
- Muchas herramientas UNIX solo manejan el modo de línea sencilla.
- `\A` y `\Z` no funcionan en JavaScript.

En modo multilínea `^`y `$` empata con el inicio y final de línea (no de la expresión).
En modo multilínea `\A` y `\Z` NO empata con el inicio y final de línea.
Algunos lenguajes de programación aceptan el modo multilíneas:
- JavaScript: `/^regex$/m`
## Delimitadores de palabras

- `\b` Límites de las palabras (inicio y fin de la palabra)
- `\B` No es el fin ni el inicio de la palabra
- Versiones antiguas de UNIX no soportan estos metacaracteres
- `\b\w+\b`

El espacio en blanco no es un delimitador de palabra.
Los delimitadores hacen referencia a una posición, no a un caracter (tienen
longitud cero).
```
\w+
peras\b y\b manzanas
peras y manzanas
\b\w+\b
```
## Capturar grupos y hacer referencias
- Referenciar grupos
- Referenciar expresiones opcionales
- Utilizar referencias en la acción “Buscar y reemplazar”
- Expresiones de grupo de no-captura
## Referenciar grupos
- Las expresiones agrupadas (entre paréntesis) son “capturadas”.
- `/a(c{2}io)n/`
- Recuerda el contenido y podemos “referenciarlo”.
- No recuerda la expresión.
- Hacemos una “referencia” iniciando como `\1` al `\9`
- Podemos utilizar la referencia dentro de la expresión o después de ella.
- No se pueden utilizar dentro de las clases de caracteres, corchetes `[ ]`.
```txt
La mayoría de motores regex soportan \1 al \9
Ejemplo:
(golpe) a \1, (verso) a \2
explicacion:
- el `\1` hace referencia a (golpe)
- el `\2` hace referencia a (verso)
<(div|p)>.+?</\1>
```
## Referenciar expresiones opcionales
Hay que tener cuidado en hacer referencia a expresiones “opcionales”.
```
Aquí hacemos un grupo y dentro viene un elemento opcional (?).
(A?)B\1C
Aquí hacemos un grupo que es opcional:
(A)?B\1C
```
> En JavaScript funciona igual, pero en algunos regex puede aceptar espacios vacíos.
## Expresiones de grupo de “no-captura”
Para especificar que no se capture un grupo en una expresión regular se utiliza:
`?:`
Puede servir para optimizar las búsquedas.
Para guardar referencias cuando estas son limitadas
```
(rojo) es (verde) no \1
(rojo) es (verde) no \2
(?:rojo) es (verde) no \1
Correpto 
rojo es verde no verde
Explicacion:
El ?: hace que no se referencia y se haga referencia al verde
```
## Aserciones "look around (mirar alrededor)"
- Aserciones positivas “lookaround”
- Aserciones negativas “lookaround”
- Aserciones “lookbehind” mirar atrás
## Aserciones positivas “lookaround”
Las aserciones son “pruebas” para encontrar cadenas, pero que no se
consideran dentro de la selección.
- Tienen “longitud-cero”.
- Aserciones básicas son los metacaracteres `^` y `$` que son “longitud-cero”.
- Como secuencias de escape podemos definir otras aserciones simples:
  - `\b` y `\B` delimitador de palabra y su negativo
  - `\a` y `\A` inicio de palabra y su negativo
  - `\z` y `\Z` final de la palabra y su negativo

- Podemos hacer expresiones más complicadas por medio de aserciones de
tipo “mirar alrededor” o lookaround:
- Aserciones “mirar después” o lookahead: indican ciertos caracteres que
deben de existir después de la expresión y se marcan con (?=).
- La aserción negativa se marca con (?!).
- Aserciones “mirar antes” o lookbehind: Indica los caracteres que deben
existir antes de la expresión y se marcan con (?<=).
- La aserción negativa se marca con (?<!).

Si se usan dentro de paréntesis, deben de ir al inicio.
- Si no se ubica la cadena delante de la expresión, la búsqueda falla.
- Podemos utilizar cualquier expresión válida como aserción delante.
- Por lo general, las herramientas tradicionales de UNIX no soportan las
aserciones.
```
/(?=regex)/
/aguacate(?=;)/
Explicacion:
Busca aquel que tenga "aguacate," si tiene  la "," este es seleccionado
y solamente la palabra aguacate estara selecionada
/aguacate (?= molido)/
correcto:
aguacate molido
resultado:
aguacate

/\b[A-Za-z]+\b/
/\b[A-Za-z]+\b,/
/\b[A-Za-z]+\b(?=,)/
```
## Aserciones negativas “lookaround”
Por medio de una aserción negativa indicamos “que no termine en...”
- `/(?!regex)/`
- `/aguacate(?!,)/`
- `/video(?! curso)/`
- `/video(?!.*curso)/`
- `/\bcaballo\b(?! negro)/`
- `/\bcaballo\b(?= negro)/`
## Aserciones “lookbehind” mirar atrás NO SOPORTADO JAVASCRIPT
Podemos seleccionar cadenas que contengan “antes” alguna subcadena, o en
su defecto, que no la tengan como condición:
- /(?<=regex)/ aserción positiva
- /(?<!regex)/ aserción negativa