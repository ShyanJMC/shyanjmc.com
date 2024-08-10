# Bash

Bash = Bourne Again Shell

- Proyecto; GNU
- URL; https://www.gnu.org/software/bash/

Los comentarios en Bash se ponen con los numerables; # así se puede comentar cosas sin que den error en el script (por que no se procesan básicamente)

## Scripting

No te hagas la cabeza, el scripting de una shell es usar el 95% del tiempo los condicionales y el otro 5% es usar variables
en comandos que uno necesita.

- Extensión de archivo; sh

1. Inicio de archivo - header

```
#!/bin/bash
```

2. Variables

```
[variable_name]=[valor]
```

Las variables creadas luego se referencian en el código con;

```
$[variable_name]
```

3. If / elif / else

El único mandatorio es "if", "elif" es para hacer una segunda verificación.

```
if [ [condición] ]; then
	[acción_si_condición_verdadera]
elif [ [condición_2] ]; then
	[acción_si_condición_verdadera]
else
	[acción_si_ninguno_verdadero]
fi
```

La condición tiene formas según lo que se quiera comparar;

- Si $a y/o $b son numerales, se puede usar;

  1. "-lt" para si $a es menor ("less than") a $b
  1. "-le" para si $a es menor o igual a $b
  1. "-eq" para si $a es igual a $b
  1. "-ne" para si $a NO es igual a $b
  1. "-gt" para si $a es mayor a $b
  1. "-ge" para si $a es mayor o igual a $b

- Si $a y/o $b son strings, se puede usar;

  1. "==" para si $a y $b son iguales
  1. "!=" para si $a y $b son diferentes
  1. "\<" ó "\>" para menor o mayor respectivamente según el orden lexicográfico (no es igual al orden numérico)
  1. "-z" para si $a ó $b es una cadena vacía
  1. "-n" para si $a ó $b NO es una cadena vacía


- Sí $a y/o %b son archivos, se puede usar;

  1. "-e" para sí $a ó $b existe (se recomienda que sean Path absolutos)
  1. "-f" para si $a ó $b es un archivo regular (osea; no es un directorio, dispositivo, etc). Sirve también para saber si el archivo existe.
  1. "-d" para si $a ó $b es un directorio
  1. "-r" para si $a ó $b es un archivo legible (lo saca por permiso)
  1. "-w" para si $a ó $b es un archivo escriturable (lo saca por permiso)
  1. "-x" para si $a ó $b es un archivo ejecutable (lo saca por permiso)
  1. "-s" para si $a ó $b tiene un tamaño mayor que cero

- Por último, se pueden anidar varias condiciones 

  1. "&&" para anidar dos o más condiciones, cada una debe estar en su propio set de "[ [condición] ]"
  2. "||" para hacer un "ó" exclusivo de dos o más condiciones, apenas se encuentre con la primera que sea verdadera la condición procede y deja de verificar las siguientes,  cada una debe estar en su propio set de "[ [condición] ]"
  3. "!" para hacer una negación de la condición de verificación, a diferencia de los dos anteriores este debe ir dentro del set.

- Consideraciones

  Si por esas casualidades llegamos a tener en la condición una cadena (string) no guardada en una variable previamente, entonces
  debemos poner en el set un "[ ]" doble, quedando; "[[ [condición] ]]" ya que si no dará error.
 
4. Retornos de comandos

Como bash almacena en una variable el retorno del comando, lo podemos usar para trabajarlo.

- Guardar la salida (stdout) de un comando en una variable

> [variable]=$( [comando_a_guardar_su_stdout] )

5. Leer la entrada del usuario

> read [variable_a_guardar_la_entrada]

6. Verificar existencia

Archivo

> test -f [path_absoluto_archivo]

> -f [variable_o_path_absoluto]

Directorio

> test -d [path_absoluto_directorio]

> -d [Variable_o_path_absoluto]

7. Ciclo "for"

El ciclo "for" de bash es igual que en Python, Rust y otros; lo que hace es iterar sobre los valores
y en cada iteración ejecuta el código con ese valor correspondiente.

Asi mismo separa los valores por "nuevalínea" de esa manera si la salida de un comando tiene 3 párrafos (aunque sean de pocas palabras), entonces
la salida tiene 3 valores (cada párrafo) y en cada iteración trabajará sobre cada uno de ellos.
 
```bash
variable_1=$(ls /)

for [variable_de_iteración] in $variable_1; do
	[comandos_de_trabajo_en_cada_iteración]
done
```

También bash posee la capacidad de trabajar indicando archivos de un directorio. Al igual que en todos los Unix, tenemos la capacidad
de utilizar el * (llamado wildcard) para indicar todo lo que coincida con algo, en el caso de abajo todo lo que tenga extensión ".md"

```bash
for [variable_de_iteración] in /home/usuario_linux/Documentos/*.md; do
	[comandos_de_trabajo_en_cada_iteración]
done
```


# Ejemplo

```bash
#!/bin/bash

echo "Ingrese el documento a verificar"
read $doc

if [ ! -f $doc ]; then
	echo "El archivo no existe"
	exit
fi

# Extraemos el peso separando por espacios hasta el campo 6 y luego extrae la letra, para dejar el número solamente
len=$(ls -lh | grep document.pdf | cut -d' ' -f6 | tr -dc '0-9')

if [ -r $doc ]; then
	echo "El documento es legible"
else
	echo "El documento no es legible"
fi
###############
if [ $len -ne 0 ]; then
	echo "El archivo no tiene peso vacio"
else
	echo "El archivo tiene peso vacio, saliendo erroneamente"
	return 1
fi

## Lee recursivamente /usr
variable_iterativa=$(ls -R /usr/*)

## Itera en cada nueva linea almacenando en valor en la variable "i" y luego ejecuta
for i in $variable_iterativa; do
	if [ -f $i ]; then
		echo $i es un archivo
	elif [ -d $i ]; then
		echo $i es un directorio
	fi
done

```
