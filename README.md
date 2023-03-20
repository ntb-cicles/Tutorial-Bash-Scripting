# Tutorial-Bash-Scripting

Las primera linea que escribiras en un archivo de bash script es llamado `shebang`. Esta linea en cualquier script determina la habilidad del script para ser ejecutado como un ejecutable independiente sin tener que teclear sh, bash, python, php, etcetera en la terminal.

```bash
#!/usr/bin/env bash
```

## 1.1. Variables

Crear variables en bash es similar a otros lenguajes. No existen los tipos de datos. Una variable en bash puede contener un numero, un caracter, una cadena de caracteres (string), etc. No tienes que declarar una variable, solo asignarle un valor creara la variable.

Ejemplo:
```bash
str="hola mundo"
```
La linea anterior crea una variable `str` y asigna "hola mundo" a esta. El valor de la variable es obtenido añadiendo el `$` al inicio de la variable.

Ejemplo:
```bash
echo $str   # hola mundo
```
## 1.2. Arreglos
Como en otros lenguajes, bash tambien tiene arreglos. Un arreglo es una variable que contiene multiples valores. No hay un limite maximo en el tamaño de un arreglo. Los arreglos en bash son base cero. El primer elemento es indexado con elemento 0.Hay varias maneras de crear arreglos en bash las cuales se muestran a continuacion.

Examples:
```bash
array[0]=val
array[1]=val
array[2]=val
array=([2]=val [0]=val [1]=val)
array=(val val val)
```
Para mostrar el valor especifico de un indice se utiliza la siguiente sintaxis:

```bash
${array[i]}     # donde i es el indice
```

Si no se proporciona un indice, se asume el elemento 0. Para encontrar cuandos valores hay en el arreglo utilice la siguiente sintaxis:

```bash
${#array[@]}
```

Bash tambien tiene soporte para condiciones ternarias. Revisa algunos de los siguientes ejemplos.
```bash
${varname:-word}    # if varname exists and isn't null, return its value; otherwise return word
${varname:=word}    # if varname exists and isn't null, return its value; otherwise set it word and then return its value
${varname:+word}    # if varname exists and isn't null, return word; otherwise return null
${varname:offset:length}    # performs substring expansion. It returns the substring of $varname starting at offset and up to length characters
```

## 1.3 Manupulación de cadenas de carácteres (strings)

Revisa algunos ejemplos de sintaxis para como manipular strings

```bash
${variable#pattern}         # si el patron corresponde al inicio del valor la variable, elimina la parte mas corta que corresponda y regresa el resto 
${variable##pattern}        # si el patron corresponde a el inicio del valor de la variable, elimina la parte mas larga y regresa el resto 
${variable%pattern}         # si el patron corresponde a el final del valor de la variable, elimina la parte mas corta y regresa el resto 
${variable%%pattern}        # si el patron corresponde a el final del valor de la variable, elimina la parte mas larga y regresa el resto 
${variable/pattern/string}  # el patron mas largo que corresponda en la variable es reemplazado por string. Solo la primera coincidencia es reemplazada.
${variable//pattern/string} # el patron mas largo que corresponda en la variable es reemplazado por string. Todas las coincidencias son reemplazadas.
${#varname}                 # regresa la longitud del string
```

Se puede concatenar strings de dos formas:

```bash
string1="Hola "
string2 "Mundo!!"

string_a="$string1$string2"

string_b+=string1
string_b+=string2
```
Tanto `string_a` como `string_b` contienen `Hola Mundo!!` 

## 1.4. Operadores para valores numéricos

Operadores para valores numéricos (**operaciones aritméticas**)

```bash
a + b           # Operador de suma 
a - b           # Operador de resta 
a * b           # Operador de multiplicación 
a / b           # Operador de división 
a ** b          # Operador de potenciación 
a % b           # Operador de módulo 


a += b           # Operador de suma y asignación
a -= b           # Operador de resta y asignación
a *= b           # Operador de multiplicación y asignación
a /= b           # Operador de división y asignación
a %= b           # Operador de módulo y asignación


a++             # Operador de incremento. Hace lo mismo que  a+=1
a--             # Operador de decremento. Hace lo mismo que  a-=1
```

## 1.4.1 Operando con valores numéricos (IMPORTANTE!)

Bash, por defecto, cuando se opera entre dos variables interpreta siempre que la variables son strings.

Por ejemplo, cuándo realizamos la siguiente operación:

```bash
valor=5
valor += 2
echo $valor
```    
El echo imprime `52`, ya que interpreta que las variables son string, y por lo tanto, concatena los dos string.

Si queremos que el resultado sea `7`, debemos envolver la **operación aritmética** con dos paréntesis delante y dos detrás, como en el ejemplo siguiente:

```bash
valor=5
((valor += 2))
echo $valor
```    
En este caso, echo imprime `7`, ya que se le ha indicado con `(( OPERACION_ARITMETICA ))` que debe realizar una operación aritmética en vez de una operación con strings.

Si queremos imprimir el resultado de una operación aritmética pero no guardarla, debe hacerse de la forma siguiente:

```bash
valor=60
echo Suma de dos valores sin guardar resultado:  $((valor + 15))
``` 
En este caso, echo imprime `Suma de dos valores sin guardar resultado: 75`,

## 1.5. Funciones

Como en casi todos los lenguajes de programacion, se pueden utilizar funciones para agrupar piezas de codigo de una manera mas logica o para practicar el divino arte de la recursion. Declarar una funcion solo consiste en escribir function mi_funcion { mi_codigo }. Llamar a la funcion es como llamar a cualquier otro programa, solo hay que escribir su nombre.

```bash
function nombre() {
    comandos de shell
}
```

Ejemplo:
```bash
#!/bin/bash
function hola {
   echo mundo!
}
hola

function say {
    echo $1
}
say "hola mundo!"
```

Cuando ejecutas el ejemplo anterior la funcion `hola` enviara como salida "mundo!". En cambio, la funcion `say` imprime el primer argumento que recibe. Argumentos dentro las funciones son tratados en la misma manera que los argumentos dinamicos que se dan al script.

## 1.5. Condicionales

Las instrucciones condicionales en bash son similares a otros lenguajes de programacion. Las condiciones tienen muchas formas, como por ejemplo la forma mas basica es `if` expresion `then` instrucciones, donde instrucciones solo se ejecutan si la expresion es verdadera.

```bash
if [ expresion ]; then
    se ejecutara solo si la expresion es verdadera    
else
    se ejecutara solo si la expresion es falsa
fi
```
En ocasiones, si las condiciones se vuelven confusas, se pueden escribir las mismas utilizando `case statements`.

```bash
case expression in
    pattern1 )
        statements ;;
    pattern2 )
        statements ;;
    ...
esac
```

Expresiones lógicas para bloques de expresiones condicionales (statements):

```bash
statement1 && statement2  # ambas condiciones son verdaderas
statement1 || statement2  # por lo menos una de las condiciones son verdaderas
```

Expresiones de comparación para Strings:

```bash
str1 = str2       # str1 es igual a str2
str1 != str2      # str1 no es igual a str2
str1 < str2       # str1 es menor que str2
str1 > str2       # str1 es mayor que str2
-n str1         # str1 no es nulo (tiene una longitud mayor que 0)
-z str1         # str1 es nulo (tiene una longitud de 0)
```
Expresiones de comparación para valores numéricos

```bash
-lt     # menor que
-le     # menor o igual que
-eq     # igual
-ge     # mayor o igual que
-gt     # mayor que
-ne     # no es igual
```
Expresiones para ficheros:

```bash
-a file         # el archivo existe
-d file         # el archivo existe y es un directorio
-e file         # el archivo existe, mismo funcionamiento que -a
-f file         # el archivo existe y es un archivo normal (por ejemplo, no es un directorio o un tipo de archivo especial) 
-r file         # se tiene permiso de lectura
-s file         # el archivo existe y NO esta vacio
-w file         # se tiene permiso de escritura
-x file         # se tiene permisos para ejecutar el archivo o de busqueda si es un directorio
-N file         # el archivo fue modificado desde la ultima lectura
-O file         # eres el dueño del archivo
-G file         # el ID del grupo del archivo es igual que el de tu usuario (o en alguno de tus grupos si tienes varios)
file1 -nt file2     # file1 es mas nuevo que file2
file1 -ot file2     # file1 es mas viejo que file2
```

## 1.6. Bucles
Hay tres tipos de bucles en bash. `for`, `while` y `until`.
Diferentes sintaxis de `for` :
```bash
for x := 1 to 10 do
begin
  statements
end

for name [in list]
do
  statements that can use $name
done

for (( initialisation ; ending condition ; update ))
do
  statements...
done
```
Sintaxis de `while` :
```bash
while condition; do
  statements
done
```
Sintaxis de `until` :
```bash
until condition; do
  statements
done
```
# 2. Trucos
## Establecer un alias
Ejecutar `nano ~/.bash_profile` y agregar la siguiente linea:
```bash
alias dockerlogin='ssh www-data@adnan.local -p2222'  # agregar tu alias en .bash_profile
```
## Para rapidamente movers a un directorio especifico
Ejecutar `nano ~/.bashrc` y agregar la siguiente linea:
```bash
export hotellogs="/workspace/hotel-api/storage/logs"
```
Ahora puedes utilizar el path guardado:
```bash
source ~/.bashrc
cd $hotellogs
```
## Re-ejecutar el comando anterior
Esto se remonta a los dias cuando no se podia confiar en que los teclados tengan una tecla de flecha "hacia arriba", pero puede aun ser util
Para ejecutar el ultimo comando en su historia.
```bash
!!
```
Un error comun es el olvidar utilizar `sudo` como prefijo de un comando que requiere privilegios parar su ejecucion. En lugarr de teclear todo el comando de nuevo, puedes usar:
```bash
sudo !!
```
Esto cambiara  `mkdir somedir` en `sudo mkdir somedir`.
## Trampas de salida
Haga sus scrips de bash mas robustos ejecutando de manera regular limpieza.
```bash
function finish {
  # your cleanup here. e.g. kill any forked processes
  jobs -p | xargs kill
}
trap finish EXIT
```
## Guardar variables de ambiente
Cuando se ejecuta `export FOO = BAR`, la variable de ambiente solo se exporta en la shell actual y todos sus hijos, para persistirla en el futuro se puede simplemente agregar en el archivo `~/.bash_profile` el comando para exportar la variable
```bash
echo export FOO=BAR >> ~/.bash_profile
```
## Acceder a tus scripts
Puedes facilmente  utilizar tus scripts creando un folder bin en tu directorio home utilizando `mkdir ~/bin`, de esta manera todos los scripts que se guarden en este directorio pueden ser utilizados desde cualquier directorio.
Si esto no funciona, prueba agregando el siguiente codto en tu archivo `~/.bash_profile` y despues ejecuta `source ~/.bash_profile`.
```bash
# Configurar PATH para que incluya el directorio privado bin del usuario si existe
if [ -d "$HOME/bin" ] ; then
    PATH="$HOME/bin:$PATH"
fi
```
# 3. Depuracion (debugging)
Puedes facilmente depurar scrips de bash enviando diferentes opciones a el comando `bash`. Por ejemplo `-n` no ejecutara el comando y solo revisara errores de sintaxis. `-v` realiza un echo del comando antes de ejecutarlo. `-x` realiza un echo del comando despues de procesarlo. 
ß
```bash
bash -n nombredelscript
bash -v nombredelscript
bash -x nombredelscript
```
