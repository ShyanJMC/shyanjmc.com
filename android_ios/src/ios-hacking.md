# iOS - Hacking/Pentesting

Acá es requisito casi indispensable tener jailbreak, ni yo ni vos somos expertos que podemos encontrar zero days en un dispositivo sin eso.

En iOS se utiliza el lenguaje Swift para programar las aplicaciones. Es un lenguaje compilado por lo que no se puede leer así no más.

Para realizar el proceso de ingeniería inversa en iOS se debe utilizar algún desamblador ('disassembler' en inglés) que permita leer el código en ensamblador.
Hay muchos o pocos, dependiendo de tu experiencia y capacidades así como de lo que necesites, pero acá una lista; 

- [Hopper (pago)](https://www.hopperapp.com/)
- [REDasm (open source)](https://github.com/REDasmOrg/REDasm)

Una vez abierto el desamblador, se abre el ipa (o su archivo binario interno si da error) y a ponerse analizar, acá dependes de tus conocimientos en ensamblador.

## Ubicación de los archivos

La ubicación de los archivos corresponde a los de la aplicación y sus datos, en ambas plataformas (Android e iOS) se encuentran separados.

- Datos; /var/mobile/Containers/Data/Application/[app_name_id]
- Sistema; /Applications
- App ID; /var/mobile/Containers/Bundle/Application/[app_name_id]

# Hacking con frida

Frida es un framework de escucha y respuesta instrumental para sistemas móbiles de Linux y BSD (entra iOS ahí).

## Dependencias

- Host; 
  - Paquetes; Python, python-setuptools
  - Infraestructura; 
    1. iOS con jailbreak
    2. El sistema iOS debe tener instalado frida-server de la tienda "pirata" que se esté utilizando.
    3. Se recomienda también que esté openssh-server funcionando.

## Instalación

En el linux, en un usuario NO root; 

> pip install frida-tools

En sistemas como Arch pip está bloqueado a los repositorios oficiales. En ese caso remplazar "pip" por "pipx" (previa instalación de python-pipx).

Toda la conectividad se realiza sí o sí por el cable usb que debe estar conectado al sistema linux.

> frida-ps -U

## Instrumentación

Frida se basa en interceptar llamadas.

Por lo que se debe primero saber qué se quier hacer; ¿querés evadir las detecciones y medidas de seguridad de antiroot?
Eso es lo que describiré a continuación.

Debes saber que siempre tenés que tener algún archivo javascript, eso es lo que interpreta el engine de Frida para modificar la app en tiempo real.

## Aplicación objetivo

Primero hay que detectar cual es la aplicación objetivo que se quiere vulnerar mediante Frida

Recomiendo realizar una verificación de que programas están ejecutandose en el iOS y ahí determinar el nombre del proceso que queremos vulnerar:

> firda-ps -U

## Ejecución en un dispositivo

> frida -U -f '[app_name_id]' -l [archivo_js]

También se puede ejecutar un script directamente desde la web de Frida

> frida -U -f '[app_name_id]' --codeshare [usuario]/[código]

### ByPass root

Generalmente las apps o librerías de detección de root como "rootbeer" (entre otros), que funcionan detectando archivos en el filesystem u otras llamadas simples, ergo la forma es interceptar 
tales llamadas e indicarles que todo esta como si nunca se hubiera hecho root.

Uno debe buscar ("frida bypass root detection" en google) que el funcione para la aplicación que está deseando auditar y usar alguna de las dos ejecuciones anteriormente indicadas.

Por ejemplo;

> frida --codeshare dzonerzy/fridantiroot -f [app_name_id] -U

### Seguimiento de actividades

Podes hacer un seguimiento a bajo nivel de que está haciendo la aplicación objetivo, y descubrir cosas nuevas sobre ella con;

> frida-trace -U -f [app_name_id]
