# Bibliotecas estándar

Cuando quieres realizar una acción es el kernel el que debe proveer las funcionalidades mínimas para que la misma se pueda hacer correctamente;
¿quieres leer un archivo en una ubicación X? El kernel debe poder reconocer en que dispositivo de almacenamiento se encuentra, debe poner
reconocer en su sistema de archivos cuales son los bits necesarios que contienen la información exacta de ese archivo, debe poder reconocer
la codificación en que está ese archivo (¿está en cirílico o en algún idioma latino?), debe poder guardar esa información en un buffer
temporal para luego pasar esa información al programa que lo solicitó de una forma apropiada (no es correcto simplemente escupirle al programa
todos esos bits de una, se debe hacer de una forma específica).

Ese mismo ejemplo es para algo tan "simple" (notese las comillas), pero es mucho más complejo para el resto de cosas. La forma en que el kernel
del sistema operativo y el programa (y por ende; el lenguaje de programación en que fueron desarrollados) hablan está estandarizada mediante la biblioteca estándar.

## Enlazamiento

En todos los sistemas operativos cuando un programa es compilado (ósea; de código fuente humano a código máquina) todas las funcionalidades
que pide realizar al sistema operativo son redirigidas a la biblioteca estándar a fin de proveer tales.

Hay dos formas de hacer lo; ó se enlaza dinámicamente la funcionalidad a un archivo externo (de tal forma que cuando quiere realizar tal acción
entonces esa llamada se redirige al archivo de la biblioteca estándar que provee esa funcionalidad con el kernel) ó se extrae la funcionalidad
de la biblioteca estándar y se inserta internamente en el programa. Al primero se llama; "enlazamiento dinámico" y al segundo "enlazamiento estático".

| **Aspecto**                   | **Enlazamiento Dinámico**                             | **Enlazamiento Estático**                             |
|-------------------------------|------------------------------------------------------|-----------------------------------------------------|
| **Definición**                | Las bibliotecas se cargan en tiempo de ejecución.    | Las bibliotecas se integran directamente en el binario. |
| **Tamaño del binario**        | Más pequeño, ya que no incluye el código de las bibliotecas. | Más grande, ya que incluye el código completo de las bibliotecas. |
| **Rendimiento en ejecución**  | Puede ser ligeramente más lento debido a la carga dinámica. | Rápido, ya que todo está en un solo binario.        |
| **Consumo de memoria**        | Eficiente, ya que las bibliotecas compartidas se cargan solo una vez en memoria para todos los procesos. | Mayor, ya que cada proceso tiene su propia copia de las bibliotecas. |
| **Portabilidad**              | Menos portátil; depende de la disponibilidad de las bibliotecas en el sistema de destino. | Más portátil; el binario incluye todo lo necesario. |
| **Actualizaciones de bibliotecas** | Fácil; se actualizan independientemente del binario. | Requiere recompilar y redistribuir el binario para actualizar las bibliotecas. |
| **Seguridad**                 | Mayor riesgo si una biblioteca compartida tiene vulnerabilidades. | Más seguro, ya que el binario no depende de bibliotecas externas. |
| **Uso típico**                | Programas generales y aplicaciones del sistema.      | Sistemas embebidos, contenedores y entornos minimalistas. |
| **Ejemplos de herramientas**  | Cargador dinámico (`ld-linux.so`).                   | Compiladores (`gcc -static`).                      |
| **Compatibilidad binaria**    | Alta compatibilidad en sistemas con las mismas versiones de bibliotecas. | Baja compatibilidad; el binario funciona como un todo. |
| **Tiempo de carga inicial**   | Puede ser más lento debido a la búsqueda y carga de bibliotecas. | Más rápido, ya que no requiere resolver dependencias en tiempo de ejecución. |
| **Depuración**                | Puede ser más compleja por la separación entre binario y bibliotecas. | Más simple, ya que todo está integrado en un único binario. |
| **Ventajas**     | - Ahorro de memoria. <br /> - Actualización sencilla de bibliotecas. | - Binarios independientes y portables. <br />  - Seguridad mejorada. |
| **Desventajas**  | - Dependencia de bibliotecas externas. <br /> - Mayor riesgo de problemas de compatibilidad. | - Binarios grandes.<br /> - Necesidad de recompilar para actualizaciones. |

## Sistemas operativos Linux

En los Linux tenemos principalmente dos bibliotecas estándar de C (el lenguaje de programación originario en que hizo el kernel Linux); GlibC y MUSL.

### Verificación y versionado

Si no sabemos que librería estándar estamos usando, o queremos saber su versión, con este comando podemos obtener esa información:

> ldd -\-version

### Ubicación de archivos

| Característica                 | **MUSL**                                    | **GlibC**                                   |
|--------------------------------|---------------------------------------------|--------------------------------------------|
| **Biblioteca compartida**      | `/lib/libc.so`                              | `/lib/libc.so.[version]` o `/lib64/libc.so.[version]`       |
| **Biblioteca estática**        | `/usr/lib/libc.a`                           | `/usr/lib/libc.a` o `/usr/lib64/libc.a`     |
| **Archivos de cabecera**       | `/usr/include/`                             | `/usr/include/`                             |
| **Cargador dinámico**          | `/lib/ld-musl-[arquitectura].so.[version]`  | `/lib/ld-linux.so.[version]` o `/lib64/ld-linux-[arquitectura].so.[version]` |
| **Configuración del cargador** | No aplica (sin `ld.so.conf`)                | `/etc/ld.so.conf`                           |
| **Archivos adicionales**       | No tiene configuraciones adicionales        | `/etc/ld.so.conf.d/` (archivos de configuración) |
| **Compatibilidad multilib**    | Unificada: `/lib` misma biblioteca para todas las arquitecturas | Diferenciadas: `/lib` para 32 bits y `/lib64` para 64 bits |

### Verificación del enlazamiento en un binario

Si necesitamos verificar si un binario esta enlazado estáticamente o dinámicamente, podemos utilizar la utilidad (comando) "ldd":

![](data:image/png;baase64,)

Como puede ver en la imagen superior, si el binario está enlazado dinámicamente se obtendrá el siguiente resultado:

```
[librería_que_provee_la_funcionalidad] => [ubicación_de_la_librería] ( [lugar_en_la_memoria_cuando_se_ejecuta_el_programa] )
```

Si el binario está enlazado estáticamente el comando retornará eso indicando lo mismo.

### GLibc

**glibc** (GNU C Library) es la implementación de la biblioteca estándar del lenguaje de programación C 
para sistemas GNU/Linux y otros sistemas operativos. Es una pieza fundamental del ecosistema GNU, desarrollada 
y mantenida como parte del Proyecto GNU por la Free Software Foundation (FSF). Proporciona interfaces críticas 
para aplicaciones, herramientas de usuario y componentes del sistema operativo, facilitando la interacción con el kernel Linux y los recursos de hardware.

#### **Propósito y Funcionalidad**

1. **Provisión de APIs estándar**  

   glibc implementa la mayoría de las interfaces definidas por el estándar C (ISO C), así como numerosas extensiones para 
   soportar características específicas de POSIX y GNU. Entre las funciones que ofrece, se incluyen:
   
   - Manejo de entrada y salida (e.g., `printf`, `scanf`, `fopen`, `fwrite`).
   - Gestión de memoria dinámica (e.g., `malloc`, `calloc`, `free`).
   - Manejo de señales (e.g., `signal`, `sigaction`).
   - Funciones matemáticas (e.g., `sqrt`, `sin`, `cos`).
   - Gestión de procesos (e.g., `fork`, `exec`, `waitpid`).
   - Funciones de threading (e.g., `pthread_create`, `pthread_join`).

2. **Soporte multiplataforma**  

   Aunque está optimizada para GNU/Linux, glibc también puede ser utilizada en otros sistemas operativos como Hurd, BSD, 
   y algunas variantes de UNIX, ofreciendo un alto nivel de portabilidad.

3. **Carga dinámica y resolución de dependencias**  

   glibc proporciona un cargador dinámico (`ld-linux.so`) que gestiona la carga de bibliotecas compartidas en 
   tiempo de ejecución y resuelve dependencias entre estas.

4. **Soporte para localización e internacionalización**  

   glibc incluye soporte extensivo para configuraciones regionales, como el manejo de caracteres multibyte, formato 
   de fechas, y configuraciones de idioma mediante `locale`.

5. **Extensiones de GNU**  

   Además de los estándares, glibc incluye varias funcionalidades exclusivas de GNU, como funciones avanzadas de 
   depuración, introspección y optimizaciones específicas para hardware moderno.

#### **Características Técnicas Destacadas**

1. **Compatibilidad ABI y API**  

   glibc se enfoca en mantener compatibilidad hacia atrás en la medida de lo posible, lo que asegura que aplicaciones 
   compiladas para versiones antiguas de la biblioteca continúen funcionando en sistemas con versiones más recientes.

2. **Optimización por Arquitectura**  

   glibc incluye optimizaciones específicas para diversas arquitecturas (x86, ARM, PowerPC, etc.), garantizando un rendimiento eficiente en hardware moderno.

3. **Soporte Multihilo**  

   Soporta modelos de programación multihilo basados en POSIX Threads, permitiendo a las aplicaciones aprovechar múltiples núcleos de CPU.

4. **Configuración y Compilación Personalizada**  

   glibc puede ser configurada y compilada para diferentes necesidades, permitiendo optimizaciones específicas como el 
   uso en sistemas embebidos o en entornos de alto rendimiento.

#### **Ventajas de glibc**

1. **Estándar de la industria**  

   glibc es la biblioteca estándar de facto para sistemas GNU/Linux y se utiliza en la mayoría de las distribuciones.

2. **Extensibilidad y Modularidad**  

   Es compatible con extensiones GNU, lo que la hace flexible y adecuada para aplicaciones avanzadas.

3. **Amplio soporte y documentación** 
 
   Al ser parte del Proyecto GNU, glibc tiene una comunidad activa de desarrollo y una documentación extensa.

4. **Rendimiento optimizado**  

   Con optimizaciones específicas para hardware y soporte para múltiples arquitecturas, ofrece un rendimiento excepcional.

#### **Desventajas de glibc**

1. **Complejidad**  

   Debido a su amplia funcionalidad, glibc puede ser demasiado compleja para sistemas minimalistas o embebidos.

2. **Tamaño**  

   glibc tiene un tamaño significativo en comparación con alternativas como musl libc, lo que puede ser una desventaja en sistemas con recursos limitados.

3. **Dependencia del ecosistema GNU**  

   Aunque es altamente portable, su integración más natural ocurre en entornos GNU/Linux.

#### **Aplicaciones y Casos de Uso**

1. **Sistemas Operativos Generales**  

   Todas las principales distribuciones de Linux, incluidas Debian, Ubuntu, Fedora, y CentOS, utilizan glibc como biblioteca estándar C predeterminada.

2. **Aplicaciones Empresariales**  

   glibc se utiliza ampliamente en servidores y entornos empresariales debido a su estabilidad y soporte de estándares.

3. **Desarrollo de Software**  

   Es esencial para desarrolladores que escriben aplicaciones en C/C++ y necesitan acceso a interfaces estándar.

#### **Comparación con Alternativas**

| **Aspecto**             | **glibc**                         | **musl libc**                     | **uClibc**                        |
|-------------------------|-----------------------------------|-----------------------------------|-----------------------------------|
| **Tamaño**              | Grande                           | Pequeño                           | Muy pequeño                       |
| **Rendimiento**         | Optimizado                       | Adecuado para entornos minimalistas | Adecuado para sistemas embebidos |
| **Portabilidad**        | Alta                             | Alta                              | Moderada                          |
| **Complejidad**         | Alta                             | Baja                              | Baja                              |
| **Soporte de estándares** | Completo                        | Parcial                           | Parcial                           |

### MUSL

**musl libc** es una implementación de la biblioteca estándar C diseñada para ser ligera, rápida y compatible 
con los estándares, manteniendo una simplicidad de diseño y enfoque minimalista. Es especialmente popular en 
sistemas embebidos, contenedores y distribuciones Linux minimalistas. Fue creada como una alternativa más eficiente 
a glibc, y su desarrollo está liderado por Rich Felker desde 2011.

A diferencia de GLibC, MUSL solamente es compatible con Linux.

#### **Propósito y Funcionalidad**

1. **Provisión de APIs estándar**

   musl libc implementa las interfaces definidas por los estándares C (ISO C99 y C11), POSIX y algunas extensiones específicas de Linux. Entre sus funcionalidades principales están:
   - Gestión de entrada y salida (e.g., `printf`, `scanf`, `fopen`, `fwrite`).
   - Operaciones matemáticas (e.g., `sqrt`, `log`, `sin`).
   - Gestión de memoria dinámica (e.g., `malloc`, `calloc`, `free`).
   - Manejo de señales (e.g., `signal`, `sigaction`).
   - Funciones de sistema y threading (e.g., `fork`, `exec`, `pthread_create`).

2. **Simplicidad y diseño minimalista**

   musl busca mantener el código simple y legible, priorizando la claridad sobre la complejidad. Esto lo hace más adecuado para sistemas donde los recursos son limitados.

3. **Compatibilidad con entornos minimalistas**

   musl es ideal para sistemas embebidos y contenedores debido a su pequeño tamaño, bajo consumo de recursos y ausencia de dependencias adicionales.

#### **Características Técnicas Destacadas**

1. **Ligereza**

   - musl está diseñado para ser extremadamente compacto, lo que lo hace ideal para sistemas donde el espacio es limitado, como dispositivos IoT o contenedores Docker.

2. **Rendimiento**

   - Aunque prioriza la simplicidad, musl ofrece un rendimiento competitivo con glibc, especialmente en sistemas con restricciones de hardware.

3. **Enfoque en la portabilidad**

   - Implementa los estándares ISO C y POSIX de manera rigurosa, garantizando compatibilidad con un amplio rango de aplicaciones.

4. **Integración monolítica**

   - Todas las funciones estándar están en una única biblioteca (`libc.so`), eliminando la necesidad de bibliotecas adicionales como `libpthread` o `librt`.

5. **Optimización para sistemas embebidos**

   - Incluye un manejo eficiente de memoria y bajo consumo de recursos, adecuado para dispositivos con hardware limitado.

#### **Ventajas de musl**

1. **Tamaño reducido**

   - musl es significativamente más pequeña que glibc, tanto en términos de espacio en disco como en uso de memoria.

2. **Simplicidad y mantenibilidad**

   - Su diseño claro y limpio facilita la depuración y el mantenimiento del código.

3. **Compatibilidad con contenedores**

   - Es ideal para aplicaciones en contenedores debido a su pequeño tamaño y ausencia de dependencias adicionales.

4. **Cumplimiento estricto de estándares**

   - Proporciona una implementación precisa de ISO C y POSIX, lo que mejora la portabilidad del software.

#### **Desventajas de musl**

1. **Compatibilidad limitada**

   - Aunque cumple con los estándares, algunas aplicaciones pueden requerir glibc debido a dependencias específicas de GNU o extensiones no compatibles.

2. **Falta de optimizaciones específicas**

   - musl no incluye optimizaciones avanzadas para arquitecturas particulares, como lo hace glibc.

3. **Menos herramientas asociadas**

   - A diferencia de glibc, musl no tiene una amplia gama de herramientas y configuraciones para personalización avanzada.

#### **Aplicaciones y Casos de Uso**

1. **Sistemas embebidos**

   - musl es una opción popular en dispositivos de IoT, routers y otros sistemas embebidos debido a su tamaño reducido y simplicidad.

2. **Distribuciones minimalistas**

   - Distribuciones como Alpine Linux usan musl como su biblioteca estándar, priorizando el bajo consumo de recursos y la seguridad.

3. **Contenedores**

   - En entornos Docker, musl es una excelente opción para imágenes ligeras donde cada kilobyte cuenta.

#### **Comparación con glibc**

| **Aspecto**             | **musl libc**                     | **glibc**                         |
|-------------------------|-----------------------------------|-----------------------------------|
| **Tamaño**              | Muy pequeño                      | Grande                           |
| **Rendimiento**         | Adecuado para entornos minimalistas | Optimizado para sistemas complejos |
| **Portabilidad**        | Alta                             | Alta                             |
| **Complejidad**         | Baja                             | Alta                             |
| **Cumplimiento de estándares** | Rigurosamente cumple ISO C y POSIX | Cumple estándares más extensiones GNU |
| **Uso de memoria**      | Bajo                             | Moderado a alto                  |

## Sistemas operativos BSD

Aquí tienes un análisis detallado y técnico de las características de las librerías estándar C en los 
sistemas **FreeBSD**, **OpenBSD**, y **DragonFly BSD**, destacando sus diferencias, similitudes y particularidades.

No tengo tanta experiencia con los sistemas BSD como con Linux, si encuentras errores avisame.

### **FreeBSD libc**

**Características técnicas**

- **Origen** 

  Basada en la implementación original de BSD, pero constantemente actualizada para cumplir con estándares modernos como POSIX y C11.

- **Desempeño**

  Alta optimización para rendimiento en plataformas x86-64 y ARM64.

- **Compatibilidad** 

  - Amplio soporte para APIs POSIX y SUSv3/SUSv4.

  - Funciones específicas para compatibilidad con software Linux a través de la capa de compatibilidad `linuxulator`.

- **Soporte multihilo** 

  - Utiliza `pthread` como base, con implementación robusta de funciones thread-safe (`reentrant`).

- **Seguridad** 

  - Protección frente a desbordamientos de búfer mediante funciones reforzadas como `strlcpy` y `strlcat`.

  - Uso de verificaciones en tiempo de ejecución para evitar vulnerabilidades en funciones como `printf`.

- **Modularidad**

  Diseñada para una integración estrecha con otros componentes del sistema, como `malloc`, que utiliza estrategias de asignación avanzadas para evitar fragmentación.

#### **Particularidades**

- Soporte específico para zonas de memoria (UMA) y optimizaciones dirigidas al kernel y aplicaciones de red.

- Extensiones BSD propias como `arc4random`, `realpath`, y `flopen`.

### **OpenBSD libc**

**Características técnicas**

- **Filosofía de diseño:** 

  - Foco en la simplicidad, seguridad y corrección por encima del rendimiento puro.
  
  - Código revisado exhaustivamente para eliminar vulnerabilidades y bugs.
  
- **Compatibilidad** 

  - Conformidad estricta con estándares POSIX y C99, con un enfoque particular en evitar funciones peligrosas (e.g., `gets`).
  
  - Funciones eliminadas o marcadas como inseguras (`strcpy`, `sprintf`) han sido reemplazadas por alternativas seguras.
  
- **Seguridad**

  - Introducción de mecanismos como `FORTIFY_SOURCE` para protección en tiempo de compilación y ejecución **de forma obligatoria en todos los programas al compilarlos**.
  
  - Uso intensivo de funciones reforzadas como `strlcpy`, `strlcat`, y `explicit_bzero` (la última para manejo seguro de memoria sensible).
  
  - Protección frente a "buffer overreads" y otros ataques comunes en C.
  
- **Innovaciones**

  - Implementación del generador de números aleatorios `arc4random`, que sirve como estándar de facto por su simplicidad y seguridad.
  
  - Uso de `pledge` y `unveil` en programas dependientes de la libc para garantizar menor exposición de privilegios.

#### **Particularidades**

- Sacrifica rendimiento en ciertas funciones en favor de la seguridad y claridad del código.

### **DragonFly BSD libc**

**Características técnicas**

- **Origen** 

  Derivada inicialmente de FreeBSD, pero con múltiples mejoras adaptadas a sus necesidades.
  
- **Optimización para multiprocesadores** 

  - Enfocada en sistemas SMP (multiprocesador simétrico), optimizando `pthread` y el manejo de memoria para aplicaciones paralelas.
  
  - Uso de las `kqueue` y otras primitivas para mejorar la eficiencia en I/O.
  
- **Compatibilidad**

  - Compatible con POSIX y extensiones de BSD.
  
  - Mantiene funciones tradicionales de la libc BSD con soporte para nuevas tecnologías.
  
- **Rendimiento**

  - Alto enfoque en optimización de aplicaciones multihilo y de alto rendimiento, como bases de datos y servidores.
  
  - Se integra estrechamente con el subsistema de virtualización de memoria (VM) específico de DragonFly BSD, diseñado para manejar 
  grandes cantidades de datos concurrentemente.

#### **Particularidades**

- Desarrollo estrechamente vinculado a su sistema de archivos HAMMER/HAMMER2, adaptando las funciones libc a sus capacidades avanzadas.

- Incorporación de características modernas para optimizar el rendimiento en clústeres y redes distribuidas.

### **Comparación directa**

| Característica       | FreeBSD libc                     | OpenBSD libc                        | DragonFly BSD libc                 |
|----------------------|----------------------------------|-------------------------------------|------------------------------------|
| **Filosofía**        | Rendimiento y versatilidad       | Seguridad y simplicidad             | Rendimiento en entornos paralelos |
| **Optimización**     | Balanceada (x86-64, ARM64)       | Menos prioritaria                   | Fuerte enfoque en SMP y redes     |
| **Seguridad**        | Moderada (uso de `strl*`)        | Máxima prioridad                    | Basada en prácticas estándar      |
| **Innovaciones**     | Zonas de memoria UMA             | `arc4random`, `pledge`, `unveil`    | Optimización para VM y HAMMER FS  |
| **Compatibilidad**   | Amplia (POSIX, Linux)            | Estricta a estándares               | Adaptada para distribuciones SMP  |

### **Comparación de Ubicaciones y Comandos**

| Sistema Operativo | Librería Principal      | Fuente Principal               | Headers              | Configuración             | Comando de Versión              |
|-------------------|-------------------------|--------------------------------|----------------------|---------------------------|---------------------------------|
| **FreeBSD**       | `/lib/libc.so`          | `/usr/src/lib/libc`            | `/usr/include`       | `/etc/malloc.conf`        | `ldd --version`                 |
| **OpenBSD**       | `/usr/lib/libc.so`      | `/usr/src/lib/libc`            | `/usr/include`       | `/etc/malloc.conf` (versiones viejas) | `ldd /bin/ls`                   |
| **DragonFly BSD** | `/usr/lib/libc.so`      | `/usr/src/lib/libc`            | `/usr/include`       | `/etc/malloc.conf`        | `ldd --version` o `ldd /bin/ls` |
