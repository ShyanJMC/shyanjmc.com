# Android - Hacking/Pentesting

# Bootloader

Hay que verificar si el dispositivo se encuentra con el bootloader desbloqueado ("UNLOCKED") y si tiene (o no) 

# Ing. Inversa

El proceso de ingeniería inversa es tomar un producto/activo ya terminado y funcional, para luego estudiar su composición interna para detectar, entender y comprender como fue creado, así como su funcionamiento interno.

Objetivos;

1. Entender como funciona la aplicación que estamos analizando
1. Detectar la utilización de algoritmos criptográficos vulnerables (como; SHA1, md5, SSLv3, TLSv1.0, etc).
1. Detectar errores lógicos en la aplicación a nivel de seguridad (como que se compare una llave con otros valores ya internos en la aplicación).
1. Detectar los lugares donde guarda la información, su codificación (si no se usa UTF-8 o ASCII ya vamos mal), sus metadatos que guarda, etc.
1. Detectar falencias en la resiliencia de la seguridad operacional; no verifica datos y tipos antes de leerlos, etc.

En Android los archivos apk son, desde hace bastantes versiones, compiladas en binario (archivos; .dex, .bundle, etc). Por lo que no se puede abrir el apk, descomprimirlo y leerlo en texto plano.

Hay que decompilarlo, véase; convertir de binario a texto UTF-8.

Podemos usar dos herramientas;

   - apktool
      https://github.com/ibotpeaches/apktool/

   - jadx
      https://github.com/skylot/jadx

Ambos requieren como dependencia a java (java-openjdk):

> apktool d [archivo_apk]

En Android una vez devuelto la decompilación hay que revisar los archivos con extensión "smali", el código ahí tiene el byte-code del código Java original. Es el equivalente
 a leer el ensamblador en un programa compilado.

## Secretos
 
Se deben buscar, tanto en los archivos "smali" como en el código claro accesible variables de tipo string y str que tengan nombres como; "key", "passwd", "pass", etc.
Acá limpie un poco la salida para que no incluya cosas internas del SO o de Google (firebase, androidx, etc)
 
> grep -Eirl "key|pass|crypt" * | grep -Eiv "google|firebase|androidx|lib|drawable"
 
Así mismo debemos verificar si la firma del desarrollador fue utilizado para firmar el instalador, de esta manera nos aseguramos si fue correctamente o no creada.
 
Se requiere del programa "apksigner" (viene dentro del programa android-sdk-build-tools en los repositorios de Kali, BlackArch, etc)
 
> apksigner verify [archivo].apk
 
Si no devuelve nada es que no está firmado.

# Ubicación de los archivos

La ubicación de los archivos corresponde a los de la aplicación y sus datos se encuentran separados.

- Sistema; /data/app/[app_name_id]
- Datos; /data/data/[app_name_id]

# Instalación de la aplicación

Solamente con "adb" estamos:

   - Primero nos conectamos al dispositivo (debe estar el debug habilitado por usb)

   > adb connect [IP]:5555

   - Luego instalamos remotamente en el dispositivo el apk

   > adb install [Archivo].apk

   Si tira un error del tipo "Failure [INSTALL_FAILED_NO_MATCHING_ABIS: Failed to extract native libraries, res=-113" quiere decir que la arquitectura que estás 
   usando en el Android (arm64, armehb, x86_64, etc) no es compatible con el de la aplicación.

# Hacking con Frida

Frida es un framework de escucha y respuesta instrumental para sistemas móbiles de Android y Linux

## Dependencias

- Host; 
  - Paquetes; Python, adb, python-setuptools
  - Infraestructura; Android con usb-debug habilitado y conectado (adb connect [IP]:5555)

## Instalación

En el linux, en un usuario NO root; 

> pip install frida-tools

En sistemas como Arch pip está bloqueado a los repositorios oficiales. En ese caso remplazar "pip" por "pipx" (previa instalación de python-pipx).

Descargar el frida-server;

- https://github.com/frida/frida/releases

 Luego ejecutar;

> adb root

> adb push frida-server /data/local/tmp/

> adb shell "chmod 755 /data/local/tmp/frida-server"

> adb shell "/data/local/tmp/frida-server &"

Y comprobar que se esté ejecutando;

> adb shell "ps -A | grep -i frida "

Comprobar su funcionamiento (se obtiene el ID con; adb devices -l)

> frida-ps -D [ID]

## Instrumentación

Frida se basa en interceptar llamadas.

Por lo que se debe primero saber qué se quier hacer; ¿querés evadir las detecciones y medidas de seguridad de antiroot?
Eso es lo que describiré a continuación.

Debes saber que siempre tenés que tener algún archivo javascript, eso es lo que interpreta el engine de Frida para modificar la app en tiempo real.

## Aplicación objetivo

Primero hay que detectar cual es la aplicación objetivo que se quiere vulnerar mediante Frida

> adb shell " cmd package list packages -U -i -f"

El comando anterior mostrará los paquetes con esta sintaxis;

```
package:[ruta_al_archivo_apk]=[app_name_id] installer=[aplicación_que_la_instaló] uid:[uid_numérico_de_la_app]
```

## Ejecución en un dispositivo

Frida puede conectarse por; usb, adb remoto IP, ID dispositivo, etc.

Ergo; recomiendo que sea por USB (en caso de iOS y Android) con "-U", y/o por adb (en caso de Android) con "-D [device_ID]".

En el caso de "-D" se obtiene con "adb devices -l"

> frida -D [device_id] -f '[app_name_id]' -l [archivo_js]

También se puede ejecutar un script directamente desde la web de Frida

> frida -D [device_id] -f '[app_name_id]' --codeshare [usuario]/[código]

## ByPass root

Generalmente las apps o librerías de detección de root como "rootbeer" (entre otros), que funcionan detectando archivos en el filesystem u otras llamadas simples, ergo la forma es interceptar 
tales llamadas e indicarles que todo esta como si nunca se hubiera hecho root.

Uno debe buscar ("frida bypass root detection" en google) que el funcione para la aplicación que está deseando auditar y usar alguna de las dos ejecuciones anteriormente indicadas.

Por ejemplo;

> frida --codeshare dzonerzy/fridantiroot -f [app_name_id] -D [device_id]

## Seguimiento de actividades

Podes hacer un seguimiento a bajo nivel de que está haciendo la aplicación objetivo, y descubrir cosas nuevas sobre ella con;

> frida-trace -D [device_id] -f [app_name_id]

El comando superior no hará mucho, o hará todo (dependiendo como lo veas y lo que necesites). Es mejor filtrar que necesitamos;

> frida-trace -D [device_id] -f [app_name_id] -i "[funciones]"

El filtrar por funciones (' -i "[funciones]" ') es muy útil. Pero teniendo en cuenta que las apps en Android usan ART
