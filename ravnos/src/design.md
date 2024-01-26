# Diseño del sistema operativo

El diseño de RavnOS es modular y minimalista.

- El sysinit del sistema, Huginn, se divide en dos instancias; la de sistema (que inicia los servicios escenciales) y el de usuario (que inicia los servicios específicos de cada usuario).
- La shell del sistema, Rune, integra como builtins todos los programas básicos necesarios (show, ls, etc).
- El package manager, Muninn, se encarga de instalar los programas en el home del usuario (~/.local), aislando así a los usuarios entre sí y al mismo del sistema base.
- El gestor de red, Futhark, se encarga de leer las configuraciones de red basándose en el usuario que lo ejecuta, aislando así las redes. 

La finalidad de tal diseño es, en conjunto con el estándar de programación de RavnOS, crear un sistema tan estable como sea posible que pueda actualizarse en tiempo real sin
necesitar reiniciarse (salvo el kernel o el sysinit de sistema).

Muchas de las ideas utilizadas tanto en el diseño de arquitectura del sistema como del estándar
se basan en las cosas buenas que tienen tanto las distribuciones GNU/Linux como los sistemas
BSD (OpenBSD y DragonFlyBSD en específico). Por lo que si presta atención técnica, puede detectar
cosas de ambos sistemas.
