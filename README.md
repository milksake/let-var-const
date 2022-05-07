# Let, Var y Const

Para entender las diferencias entre `let`, `var` y `const` es necesario primero entender que es el *scope* y el *hoisting* y cómo afectan ambos al momento de escribir código.

## Scope
El *scope* es básicamente el **ámbito** al que una variable pertenece dentro de un programa, es decir, donde dicha variable **puede ser usada**.

## Declaración de una variable
Una declaración de una variable es cuando se le indica al programa que se va a utilizar sicha variable. Se puede dar de tres maneras:
```javascript
var hola; //usando var
let hola; //usando let
const hola; //usando const
```

## Asignar un valor a una variable
Asignar un valor a una variable es darle un valor para que luego sea usado por el programa:
```javascript
hola = "Hola";
```

## Hoisting
*Hoisting* es una característica propia de JavaScript que causa que la declaración de variables (y funciones) se mueva al principio del código y se ejecute antes que todo lo demás. Esto afecta de manera diferente a los tres tipos de variables.

# Var
## *Scope* de `var`
La característica principal de las variables declaradas con `var` es que su *scope* es **global** a menos que estén dentro de una función, caso en el que se su *scope* es local a ella. Esto quiere decir que si son declaradas fuera de una función, las variables `var` podrán ser accedidas desde cualquier punto del programa. Si en cambio, son declaradas dentro de una función, no podrán ser accedidas fuera de ella.

Por ejemplo, en el siguiente programa:

```javascript
var saludo = "saludo";
    
function miFuncion() {
    var hola = "hola";
}

console.log(saludo);
console.log(hola);
```
En este caso, el *scope* de la variable `saludo`, es global, mientras que el de la variable `hola` está restringido a la función `miFuncion()`. De esta manera, solo `console.log(saludo)` será ejecutado sin problemas, mientras que `console.log(hola)` nos dará error porque `hola` no está declarado en ese *scope*.

## Declaración y asignación de valores

Otra característica de las variables `var` es que, aparte de que se les puede asignar nuevos valores, también pueden ser redeclaradas, incluso en el mismo *scope*. 

Esto quiere decir que se puede hacer cosas como:

```javascript
var saludo = "saludo";
var saludo = "hola";
saludo = "adiós";
```

En la primera línea, la variable `saludo` está siendo **declarada e inicializada**, en la segunda, está siendo **redeclarada** y, por último, en la tercera, se le está **asignando otro valor**. Este código no obtendrá ningún error, a pesar de que se declara `saludo` más de una vez en el mismo *scope*.

## *Hoisting* de variables `var`
Mover la **declaración** una variable `var` al principio, significa que:
```javascript
console.log (saludo);
var saludo = "saludo";
```
es interpretado como si fuera:
```javascript
var saludo;
console.log(saludo); // undefined
saludo = "saludo";
```
En este caso, cuando `console.log(saludo)` es llamado, `saludo` es `undefined`, esto ocurre debido a que las variables `var` se **inicializan** de esta forma.

## Desventajas de usar `var`
El comportamiento de las variables `var` puede resultar confuso en algunos casos, por ejemplo:
```javascript
var i = "Hola";
for (var i = 0; i < 5; i++) {
    console.log(i);
}
console.log(i); // imprime 5
```
Como se puede ver, es muy fácil perder el seguimiento a las variables `var` que han sido usadas y asignarles otro valor por error, lo cuál en algunas circumnstancias puede ser fatal.

# Let
`let` es la manera preferida de declarar variables en JavaScript; esto se debe a que resuelve algunos de los problemas que había al usar `var`.

## *Scope* de `let`
A diferencia de `var`, el *scope* de `let` es el **bloque** en el que fue declarada. Un **bloque** es todo lo que está entre `{}`. Por ejemplo:
```javascript
if (true)
{
    let hola = "hola";
    console.log(hola);
}
console.log(hola);
```
En el ejemplo, todo lo que está entre `{}` es el *scope* de la variable `hola`, por lo que la segunda llamada a `console.log(hola)` dará un error, ya que `hola` no ha sido declarada en ese *scope*.

## Declaración y asignación de valores
Al igual que `var`, las variables `let` pueden ser **asignadas otro valor**; sin embargo, **no** pueden ser **redeclaradas** en el mismo *scope*.
Esto quiere decir que esto es válido:
```javascript
let hola = "hola";
hola = "buenos dias";
```
mientras que esto, **no**:
```javascript
let hola = "hola";
let hola = "buenos dias";
```

Declarar una variable `let` con el mismo nombre en diferentes *scopes* no dará ningún error. Por ejemplo:
```javascript
let hola = "hola";
if (true) {
    let hola = "buenos dias";
    console.log(hola); // imprime "buenos dias"
}
console.log(hola); // "imprime hola"
```
## *Hoisting* de `let`
Al igual que `var`, las declaración de las variables `let` se van al inicio de su **scope**; sin embargo, la gran diferencia es que en vez de ser inicializadas como `undefined`, **no** son inicializadas.

## Ventajas de usar `let`
Como las variables están limitadas al bloque (`{}`) en la que están declaradas, es más fácil hacerles seguimiento y no encontrarse con un comportamiento inesperado en el código.

Usando de ejemplo un código muy similar al que se vió en el segmento de `var`:
```javascript
let i = "Hola";
for (let i = 0; i < 5; i++) {
    console.log(i);
}
console.log(i); // imprime "Hola"
```
Se puede ver claramente la diferencia entre ambos tipos de variables: en este caso, la segunda declaración de `i` esta dentro del **bloque for**, por lo que, una vez acabado, en la llamada a `console.log(i)`, se hace referencia a la primera declaración de `i`, que tiene el valor de `"Hola"`.

# Const
Las variables que son declaradas con `const` son, como su nombre lo indica, **valores constantes**, es decir, no pueden ser cambiados.

## *Scope* de  `const`
Las variables `const` coparten varias características con las variables `let`. Una de ellas es que ambas tienen de *scope* el bloque (`{}`) en el que fueron declaradas.

```javascript
if (true)
{
    const hola = "hola";
    console.log(hola);
}
console.log(hola); //error
```

## Declaración y asignación de valores
Al igual que las variables `let`, las variables `const` no pueden ser redeclaradas; sin embargo, a estas **tampoco** se les puede asignar otro valor. Esto quiere decir que tanto:
```javascript
const hola = "hola";
hola = "buenos dias";
```
como esto:
```javascript
const hola = "hola";
const hola = "buenos dias";
```
son inválidos.

Es importante mencionar que, por este motivo, las variables `const` deben ser inicializadas **al momento de ser declaradas**.

## *Hoisting* de `const`
Otra similitud con las variables `let` es el hecho de que las variables `const` se declaran al inicio de su *scope* pero no se inicializan.

# Resumen de las diferencias

|                          | `var`                           | `let`              | `const`                             |
|--------------------------|---------------------------------|--------------------|-------------------------------------|
| *Scope*                  | Global o en una función         | En bloques         | En bloques                          |
| Declaración y asignación de valores | Se puede redeclarar y asignar otro valor | Se le puede asignar otro valor | No se puede redeclarar ni asignar otro valor |
| *Hoisting*               | Se inicializa con `undefined`   | No se inicializa   | No se inicializa                    |