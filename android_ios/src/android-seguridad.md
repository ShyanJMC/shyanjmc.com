# Android - Seguridad

Todo se debe verificar internamente en el Android desde la shell (adb shell [comando])

## Detectar root

### Por llave

Si la llave está en 'release' entonces no está rooteado

> cat /system/build.prop | grep ro.build.tags

La salida debería ser parecida a;

> ro.build.tags=release-keys

### Por binarios

Si existen estos binarios entonces el dispositivo está rooteado;

1. supersu.apk
1. com.noshufou.android.su
1. com.thirdparty.superuser
1. eu.chainfire.supersu
1. com.koushikdutta.superuser
1. com.zachspong.temprootremovejb
1. com.ramdroid.appquarantine
1. /system/bin/su
1. /system/xbin/su
1. /sbin/su
1. /system/su
1. /system/bin/.ext/.su
1. /system/usr/we-need-root/su-backup
1. /system/xbin/mu
1. \*chainfire\*
1. busybox

### Por permisos de directorios

Si el dispositivo está rooteado entonces estos directorios van a tener los permisos de escritura y ejecución para 'Otros';

1. /data
1. /system
1. /system/bin
1. /system/sbin
1. /system/xbin
1. /vendor/bin
1. /sys
1. /sbin
1. /etc
1. /proc
1. /dev

### Por permiso de usuario

Listar ID del usuario activo

> dumpsys activity | grep -E "mUserLru" | grep -Eo "[0-9]+\]$" | tr -d "]"

Obtener datos del usuario ID

> id [user_ID]

Si aparece 0 (root) ó 998 (wheel) entonces el dispositivo está rooteado.

## Detectar custom ROM

Generalmente ls custom ROMs no tienen los certificados de Google para recibir actualizaciones OTA (Over The Air);

> ls -l /etc/security/otacerts.zip

La salida debería ser parecida a;

> -rw-r--r-- root     root         1733 2008-08-01 07:00 otacerts.zip

## Listar paquetes instalados

Solamente desde un usuario con root;

> pm list packages

## Listar capacidades (actividades) de una aplicación

> adb shell dumpsys package | grep -i " + [enter package name]  + " | grep Activity
