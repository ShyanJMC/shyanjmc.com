# Estándar de programación para RavnOS

Todo el desarrollo de RavnOS se guia por las siguientes premisas;

1. El flujo del código debe ser simple, no complejo.

   No siempre un código más complejo es de mejor calidad, muchas veces todo lo contrario.

   Un código más simple permite entenderlo mejor y detectar más fácilmente; errores y oportunidades de optimización.

2. No se permiten "unwrap" ó "expect", todo error debe ser manejado manualmente para decidir si se recupera o no.

   El uso de los "unwraps" y "expects" no es inútil; sirven a un propósito. Pero en RavnOS todo Result debe ser evaluado para evaluar
   individualmente si se prosigue o si se realiza otra acción.

   **Actualmente estoy trabajando en un sustituto para poder lidiar con diferentes situaciones que requieran o no una parada de procesamiento.**

3. Uso del stack antes que el del heap

   El uso del heap permite la locación dinámica de memoria pero a su vez dificulta la detección de erorres de bajo nivel y consume mayores ciclos 
   de procesamiento.

   Por supuesto, no siempre se puede saber el tamaño de la entrada de información y para evitar erorres de seguridad (como los buffer overflow) se 
   debe utilizar el heap en tales casos. Pero de ser posible se usará el stack en vez del heap.

4. Auto contención

   No se permiten el uso de librerías externas (los crates), todo el sistema debe estar autocontenido en su propio código.

   Para evitar problemas de derechos de autor se crea todo desde cero.

5. Modularidad y máximo producto viable

   Todo programa debe estar diseñado con la idea del "máximo producto viable"; el programa final va a tener X características y no más.

   Por supuesto, los tiempos cambian y también las necesidades. Para evitar los futuros problemas de código e integraciones, se debe usar 
   una arquitectura modular que permita el rápido y limpio remplazo de sus partes.

6. Compatibilidades y portabilidad

   Todo el userland de RavnOS (véase; todo lo que está por encima del kernel) debe ser portable a otros sistemas operativos que soporten
   la librería estándar de Rust al completo. Esto permite que, al igual que el proyecto GNU, partes del sistema puedan funcionar sobre un kernel
   diferente.

7. Aislamiento

   El sistema base tiene la finalidad de ser inmutable de cara al usuario final.

   Todo lo que el usuario instale/modifique se aplica en su propio "home" como entorno aislado del resto.

8. Seguridad

   Este es el punto más importante y bajo ningún concepto o escenario es negociable; la seguridad del sistema está siempre primero
   sobre cualquier otra característica.
