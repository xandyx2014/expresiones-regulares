
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

La diagonal invertida no “escapa” a las literales, sólo metacaracteres.
Las comillas no “escapan” metacaracteres.
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
Caracteres ASCII o ANSI:
0xA9 = \xA9
/a g u a/ empata con “a g u a” pero no con “a_g_u_a” ni “a*g*u*a”
```
