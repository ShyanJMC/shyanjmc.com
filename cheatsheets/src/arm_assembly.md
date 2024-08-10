# Compilación

```
as [archivo].s -o [salida_object].o
ld [object].o -o [salida_binaria]
```

## Inspección

La inspección tiene por objeto ver todo en ensamblador (-d):

```
aarch64-linux-gnu-objdump -d
```

# Misc

- Los comentarios van con //, como en C puro.
- Mientras que "[r2, #4]" indica 4 movimientos en el registro r2, un "#4" solo indica el número entero 4.

# Estructura

Los archivos en ensamblador van con la extensión ".s" y llevan la siguiente estructura;

1. Sección ".text"

    Indica el código ejecutable del programa.

1. Directiva ".global XXX"

    Indica que la función ó variable "XXX" está expuerta al exterior (como el "pub" de Rust).

1. Directiva ".type XXX, YYY"

    Indica que tipo "YYY" es la función ó variable expuerta, los valores pueden ser;

       - "function"

1. Directiva ".p2align Z"

    Indica que el código debe ir alineado en la memoria usando "Z" bytes.

    "Z" debe ser número entero que coincida con la arquitectura de bits del procesador;
    
       - 4
       - 8
       - 16
       - 32
       - 64
       - 128

1. Función/label "XXX:"

    Indica el comienzo de la función "XXX".

    Se recomienda que todo el código de la función tenga 3 espacios como sangría.

    Siempre debe retornar ("ret") y asegurarse de devolver a su estado original
    los registros usados. El registro x0 es el encargado de funcionar como 
    retorno.
    
    En caso de no tener "ret" una función, hará que se ejecute la siguiente y
    así hasta que se encuentre uno. Esto es lo que se llama; "funciones anidadas".
    
    Por ejemplo, funciones separadas que no se ejecutarán hasta
    ser llamadas específicamente;
    
 ```
 funcion_1:
    mov x3,x0
    ret
 
 funcion_2:
    cmp x3,#1
    b.eq funcion1
    ret
 ```
 
    Por ejemplo, funciones anidadas que al ser ejecutada una continuará
    ejecutando las siguientes;
    
```
 funcion_1:
    mov x3,x0
    ret
 
 funcion_2:
    cmp x3,#1
    b.eq funcion1
    ret
 ```

# Registros y variables

Los registros son las variables del propio chip, ARM tiene los siguientes;

| ARM | Registro | Alias | Uso |
| :---: | :---: | :---: | :---: |
| ARMv8 | W0-W30 | - | Propósito general (32 bits) |
| ARMv8 | X0-X30 | - | Propósito general (64 bits) |
| ARMv8 | WZR | - | Zero register (32 bits) |
| ARMv8 | XZR | - | Zero register (64 bits) |
| ARMv8 | WSP | - | Current stack pointer (32 bits) |
| ARMv8 | SP | - | Current stack pointer (64 bits) |
| ARMv8 | PC | - | Program counter (64 bits) |
| ARMv1-8 | CPSR | – | Current Program Status Register |

- Wn está englobado dentro del Xn; W0 está como 32 bits dentro del X0 de 64 bits.
- El WZR ó XZR .
- Antes de usar un registro se debe cargar el valor en él (ldr ó str).
- El estándar de llamado procedural de ARM64 estipula que los datos a devolver deben estar sí o sí en el registro x0

Los registros pueden almacenar los datos en little endian (derecha a izquierda) ó big endian (izquierda a derecha).

Los registros tienen su propio espacio de memoria interno, ya que los mismos están 
circunscritos en el propio procesador por lo que no necesitan en si de la RAM. 
Por lo que "str" saca de la memoria ese dato y se lo asigna al registro destino, 
mientras que "ldr" hace lo mismo pero sin eliminarlo de la memoria RAM haciendo solamente una copia al registro.


En caso de necesitar más, se puede usar segmentos de la RAM para almacenar.

El registro CPSR es muy importante; ya que en si mismo coniene todos los flags así como los estados
del procesador;

| 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| N | Z | C | V | Underflow | - | Jazelle | - | Greater than/or Equal | - | Endianness | Abort disable | IRQ disable | FIQ disable | Thumb | CPU Mode |

- Negative (N)

   Se habilita si el resultados de la operación es un número negativo.

- Zero (Z)

   Se habilita si el resultado de la operación es un cero.

- Carry (C)

   Se habilita si el número requiere un bit 
   adicional para ser representado completamente. 
   Véase, cuando el número repesentado requiere más
   de 64 bits para ser representado.
   
   No diferencia números positivos de negativos.

- Overflow-Underflow / Saturation (V)

   Se habilita si el resultado de la operación atimética no 
   puede ser representado con el rango de memoria usado.
   
   El rango va desde -2^63 a 2^63 (considerando que un bit,
   el primero, se usa para representar positivo o negativo), 
   cualquier número fuera de ese rango es overflow ó underflow.
   

- Jazelle

   Se utilizaba en versiones viejas de la arquitectura; ARMv5 y v6.

   Permitía que código bytecode de Java se ejecutara sin necesidad de una JVM (Java Virtual Machine) de
   por medio. Desde ARMv7 quedó obsoleo y remplazado por ThumbEE, que a su vez fue eliminado
   en ARMv8.

- Endianness

   Si está marcado en cero (0) se está usando little-endian.
   Si está marcado en uno (1) se está usando big-endian.

   
- Thumb

   Si está marcado, significa que se está usando el modo Thumb y no el ARM.

   El modo Thumb es un modo de 16bits del procesador, y a diferencia
   del modo ARM (que es 32 o 64 bits) no tiene soporte per se para condiciones
   de ejecución. Salvo Thumbv2 que sí tiene algunas condiciones.

- Mode-bis (M)

   Indica el modo de ejecución actual del procesador.
   Puede tomar los siguientes valores:

   - 0b0000: Modo Usuario (User)
   - 0b0001: Modo FIQ (Fast Interrupt Request)
   - 0b0010: Modo IRQ (Interrupt Request)
   - 0b0011: Modo Supervisor
   - 0b0100: Modo Abort
   - 0b0101: Modo Undefined
   - 0b0110: Modo System
   - 0b0111: Modo Monitor

- Abort-disable (A)

   Deshabilita las excepciones de tipo Abort.
   Se utiliza para impedir que determinadas operaciones generen excepciones Abort, lo que puede ser útil para proteger la integridad del sistema o para realizar operaciones críticas sin interrupciones.

- IRQ-disable (I)

   Deshabilita las interrupciones IRQ (Interrupt Request).
   Se utiliza para impedir que el procesador sea interrumpido por eventos externos, lo que puede ser necesario para realizar operaciones sensibles al tiempo o para proteger regiones críticas de código.

- FIQ-disable (F)

   Deshabilita las interrupciones FIQ (Fast Interrupt Request).
   Las interrupciones FIQ tienen mayor prioridad que las IRQ y se suelen utilizar para eventos críticos que requieren atención inmediata. Deshabilitarlas puede ser necesario para garantizar la ejecución ininterrumpida de tareas sensibles.

# Memoria

La primera posición de memoria es la dirección; 0x00000000

Cada registro o variable puede almacenar en la memoria de a estos rangos;

- byte; 8 bits

   Las instrucciones que llevan una "b" al final indica que el tipo de dato
   con el que operan es un "byte".

   Si es "sb" indica que un "signed byte"; puede contener positivos y negativos.
   Si no está aclarado que un "signed byte" solamente puede contener como valores;
   cero y positivos.

- half word; 16 bits (2 bytes)

   Las instrucciones que llevan un "h" ó "sh" al final indican que el tipo de dato
   con el que operan es un "half word".

- word; 32 bits (4 bytes)

   Las instrucciones que operan con words no llevan un indicativo.

- dword; 64 bits (8 bytes)

El primer bit se le llama LSB (Low Significant Bit) y el último MSB (Most Significant Bit), se lee
de derecha a izquierda.

En ARM las operaciones de memoria se consideran las posiciones:

> ldr   r0, [r2, #4]

El "#4" es una forma de indicar que la instrucción debe desplazarse 4 posiciones de memoria en el registro "r2". 
Cada posición son 8 bits.

- ARMv7

   Como la memoria está alineada a 32 bits, cada posición de memoria está separada por 32 bits. 

   Ergo; #4 = 4*8 = 32, lo que al moverse 32 bits hace que pase a la siguiente posición de los valores en el registro "r2" (un vector es).

   Por lo tanto, el desplazamiento de 4 posiciones corresponde a la segunda posición de memoria.

- ARMv8

   Como la memoria está alineada a 64 bits, cada posición de memoria está separada por 64 bits. 

   Ergo; #4 = 4*8 = 32, lo que al moverse 32 bits hace que siga estando en la misma posicon de los valores en el registro "r2" (un vector es).
   
   Por lo tanto, el desplazamiento de 4 posiciones corresponde a la misma posición de memoria (la primera) en ARM64.

## Almacenaje

Hay dos formas en que se guarda la información en la RAM; little endian ó big endian.

ARM tiene la capacidad de usar uno u otro, como se vió en el bit del registro CPSR.

La diferencia viene en que; en Big Endian el byte más significativo es el primero en almacenarse,
mientras que en Little Endian es el byte menos significativo.

Dicho en criollo; en big endian se lee y almacenan los bytes leyendo de izquierda a derecha, mientras
que en little endian se lee y almacenan leyendo de derecha a izquierda.

## Organización

La memoria RAM puede organizarse de dos formas diferentes;

- Heap

   El heap es una estrucura que hace un seguimiento de la memoria que usa un programa y es capaz de aumentar o disminuir la memoria asignada 
   al mismo para evitar un sobre uso o una limitación de memoria al programa.

- Stack

   El stack hace uso del LIFO (Last-In, First-Out; Último en entrar, primero en salir.) para almacenar datos.

   En ARM el registro R13, o también SP (Stack Pointer) contiene la posición del tope del stack.

   El stack se usa mucho cuando se necesita guardar datos para luego restaurarlos; ocurre principalmente
   cuando una función "A" utiliza unos determinados registros "X" e "Y" y luego llama a otra función
   "B" que utiliza los mismos registros, para permitir que al finalizar "B", "A" pueda seguir utilizando
   sus registros los mismos se ponen (push) en el stack y luego se sacan (pop) para ser restaurados.

   En ARM el registro R15, o también PC (Program Counter) indica la dirección en RAM (el offset) de la siguiente instrucción a ser ejecutada.
   La modificación del PC y su uso se conoce como "branching" y/o "jumping". El valor que va a tomar el registro R15 depende de las condiciones
   que se seteen (de ahí vienen el if-else) como; si el resultado de la operación fue cero (Zero; Z), negativo (N, en donde el bit más significativo
   está activo; 1), si hay un carry (C) habilitado (que es cuando sobran números por aumento de valor superior al máximo) o si hay un overflow
   dada en alguna operación aritmética (V). Tales condiciones (llamadas; "flags") se almacenan en el registro CPSR (Curent Program Status Register).

# Operaciones

- Copia de un registro/valor/offset origen a un registro destino

> mov [registro_destino],[registro_valor_o_offset_origen]

- Suma

> add [destino],[valor_1],[valor_2]

- Resta (no actualiza NZCV)

> sub [destino],[operando_registro_1],[operando_registro_2]

- Resta (actualiza NZCV)

> subs [destino],[operando_registro_1],[operando_registro_2]

- Multiplicación

> mul [destino],[operando_registro_1],[operando_registro_2]

- División 32 bits, sin contar signo
   
> udiv [cociente],[dividendo],[divisor]

   Si el divisor es cero, el cociente también lo será.

- División 64 bits, contando signo

> sdiv [cociente],[dividendo],[divisor]

   Si el divisor es cero, el cociente también lo será.
   
   Se puede generar un overflow si se hace una división
   de un entero mínimo por "-1", en tal caso se sobre escribirá
   el resultado a cero.

- Retorno a la función que lo llamó (interna ó externa)

> ret

- Cargar el valor de "YYY" en el registro "XX" sacandolo de la RAM

> ldr XX, YYY

   Si es dirección de memoria se usa [YYY]

- Comparar dos valores (lo hace ejecutando la diferencia)

> cmp [valor_variable_1],[valor_variable_2]

   Si son iguales habilita (poner en 1) el flag Z, si no
   son iguales lo deja deshabilitado.
   
   Si el segundo operando es mayor que el primero, entonces se habilita el flag
   N (negativo). Debido a que la diferencia da un número negativo.
   
   Dicho lo anterior, si el primer operando es más grande entonces N queda en
   deshabilitado y N también.

- Saltar a la funcióń/offset "X" si el flag Z (zero) no está habilitado

> b.ne X

   El acrónico "bne" significa "branch if not equal".

- Saltar a la funcióń/offset "X" si dos registros/valores no son iguales

> b.ne [registro_valor_1],[registro_valor_2], X

- Saltar a la función/offset "X" si el flag N (negative) está habilitado

> b.lt X

   b.le = "Branch i Less Than"

# Ejemplos

## Factorial de un número

```
my_function:
   mov x3, x0
loop:
   subs x3, x3, #1
   cmp x3, #0
   b.eq finish
   mul x0, x0, x3
   b loop
finish:
   ret
```

## Energía quinética de un objeto (KE =1/2 * m * v^2)

```
my_function:
   mul x2, x1, x1
   mul x3, x2, x0
   mov x4, #2
   udiv x5, x3, x4
   mov x0, x5
   ret
```

## Cálculo factorial

```
my_function:
   mov x3, x0
loop:
   subs x3, x3, #1
   cmp x3, #0
   b.eq finish
   mul x0, x0, x3
   b loop
finish:
   ret

```
