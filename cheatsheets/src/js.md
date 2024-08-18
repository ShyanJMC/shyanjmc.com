# JavaScript

Es un estándar (ECMAScript), por lo que cada engine puede expandirlo.

- TypeScript

  Creado por Microsoft añade que se tengan que especificar el tipo de dato.

  TypeScript usa la extensión ".ts"

Al estar pensado para scripting, sigue el mismo esquema que BASH; solo
ejecuta funciones si son llamadas directamente, el resto lo procesa todo en tiempo 
de ejecución.

## Instalar Deno Engine

> curl -fsSL https://deno.land/install.sh | sh

## Ejecutar un archivo

> deno run [archivo]

- "--allow-net" para permitir que el archivo use red

## Comentarios

```js
// Esto es un comentario
```

## Importar 

- De otros archivos

```js
import [Struct],[function_N] from "./[archivo].ts";
```

- De la stdlib

[Deno stdlib](https://jsr.io/@std)

```js
import [Function] from "[package_registry]:@std/[module]"
```

Deno soporta tanto NPM como JSR.

**Consideración; la función debe estar dentro de "{}" cuando el módulo
no tiene un "export default function ....."**

Las funciones que no necesitar las "{}" en el import son las que tienen
en su módulo un el default.

## Variables y constantes

- Variable

  Alcance local en una función

```js
var [var_name]: [var_type_if_is_Typescript] = [value]
```

- Constante

  Alcance global cuando son variables declaradas fuera de una función pero con alcance de bloque.
  Funciones incluidas.

  Solo pueden ser declaradas una vez dentro de su alcance.

```js
{
	const [var_name]: [var_type_if_is_Typescript] = [value]
}
```

  Las constantes no pueden actualizarse a futuro (por que hace un shadowing en realidad, que es
  una redeclaración a bajo nivel).

- let

  Al igual que en Rust, sirven para declarar variables. Y al igual que en "const" tiene alcance
  de bloque pero pueden actualizarse a posteriori.

```js
{
	let [var_name]: [var_type_if_is_Typescript] = [value]
}
```

## Structuras

```js
interface [struct_name] {
	[var_name1]: [type];
	[var_name2]: [type];
}

const [instance_name]: [struct_name] = {
	[var_name1]: [value],
	[var_name2]: [value],
}
```

### Tipos

```js
let var1 = 5;
let var2 = 12.1;
let var3 = 'string1';
let var4 = "string2";
let var5 = true;
let var6 = false;
let var7 = 'c';
```

Se puede formatear un retorno de string sin guardar previamente en
una variable;

```js
return 'Hello, ${[var_or_struct]}'; 
```

## Funciones

```js
function [func_name]([var_name]: [type]): [return_type]{
	[operations];
	return [return_value];
} 
```

Si a la función se le añade "export function ...." entonces
se vuelve pública y puede ser llamada desde otros archivos.

Equivalente al "pub" en Rust.

Si a la función le añadis "async" la volves eso; asíncrona, 
luego la variable que va a contener el retorno debe tener un "await"
antes de su llamado.

## Condicionales

- Para booleanos es un triple = para verificar valores
- Para el resto de tipos de datos son dobles = solamente

### If - else if - else

```js
if (var1 > var2) {
	console.log("el valor de var2 es mayor que var1." + '\n' + "Var2;" + var2 + '\n' + "Var1;" + var1);
} else if (var1 > var2) {
	console.log("el valor de var2 es menor que var1." + '\n' + "Var2;" + var2 + '\n' + "Var1;" + var1);
} else if (var1 == 0 || var2 >=12) {
	console.log("var1 es cero ó var2 es mayor o igual a 12" + '\n' + "Var2;" + var2 + '\n' + "Var1;" + var1);
} else if ( var1 != var2 ) {
	console.log("var1 no es igual a var2");
} else {
	console.log("sin valores de coincidencia");
}
```

### Switch

```js
switch (var1) {
	case 0:
	case 1:
		console.log("el valor de var1 es 0 ó 1");
		break;
	case 5:
		console.log("el valor de var1 es 5");
		break;
	default:
		console.log("sin valores de coincidencia");
		break;
}
```

### While

```js
while (var5 === true) {
	console.log("var 5 es verdadero");
}

/// Loop infinito

while (true){
	console.log("loop infinito");
}

/// Loop combinado
let temporal1 = 0;
while (var5 === true && temporal1 <= 5){
	console.log("loop finito");
	temporal1 += 1;
}
```

### For

Es igual que en C: inicio; condicion; modificacion final
Al igual que con los if/else, pueden combinarse unos dentro de otros

```js
for (let i = 0; i <= 15; i++){
	console.log("i = " + i + ".");
}

/// Breaks combinados
/// Cuando en un bucle se usa el break se asegura que el resto no se procesa y que se
/// termina el ciclo

for (let j = 0; j <= 15; j++){
	// Acá el if hace que no se impriman los mayores a 10
	if ( j > 10) {
		break;
	} 
	console.log("j = " + j + ".");
}

/// El continue en cambio, hace que el ciclo se termine y se inicie el nuevo

for (let e = 0; e <= 15; e++){
	// Acá el if hace que solamente se impriman los mayores a 10
	if ( e < 10) {
		continue;
	} 
	console.log("e = " + e + ".");
}
```

## Arrays

El estándar de javascript lo toma como una sucesion finita de chars
con eso se puede hacer uso de cada uno de sus componentes/chars.

Se cuenta desde cero, por que va por posiciones

```
let string1 = "Cadena de texto 1";

/// imprimirá "C"
console.log("caracter cero; " + string1[0]);
/// también se puede contar desde atrás
/// imprimirá "!"
/// el método "length" devuelve el largo de la cadena
console.log("ultimo caracter; " + string1[ string1.length -1 ]);

/// Si se utiliza un array que está en una posición inválida se obtiene un error de tipo
/// "undefined"

console.log("caracter fuera de rango; " + string1[99999]);

/// Así mismo los valores pueden ser asignados a otras variables
/// La primera toma el primer caracter
/// La segunda toma el rango desde cero hasta la posicion numero 5
let varbuffer = string1[0];
let varbuffer2 = string1[0,5];

console.log("Buffer1 es;" + varbuffer + '\n' + "Buffer2 es;" + varbuffer2);
```

## Funciones comunes

- Imprimir en pantalla

> console.log([function_or_variable]) 

```js
// show variable type
console.log("constante1 es del tipo; " + typeof constante1);
```

- Llamado asíncrono

> await [function][func_parameters];

Al ser guardado en una variable, si se imprime en pantalla también necesita un "await").

- Request web (asíncrono)

> fetch("[URL]");

- Tipo de dato

> typeof [var]

- Obtener el largo de una cadena

> [string_variable].length
