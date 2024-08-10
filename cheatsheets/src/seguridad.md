# Seguridad

## Certificaciones

- Blueteam

1. Level 1: CompTIA Segurity +, CSA, eCDFP, BTL1
2. Level 2: CompTIA CySA+, BTL2, eCTHP, CCD, CDSA, OSDA, GCIH, eCIR
3. Level 3: CompTIA CASP+, GCFA

- Redteam

1. Level 1: PNPT, CBBH, eJPT, CRTP, CEH
2. Level 2: OSCP, OSWP, OSWA, OSEP, CPTS
3. Level 3: OSMR, OSED, CRTO
4. Level 4: OSCE3, OSEE, OSWE

- InfoSec

1. Level 2: CRISC, CISA, CISM
2. Level 3: CGEIT, CISSP

## Cyber seguridad militar

| Capa | Herramienta / Procedimiento |
| :---: | :---: |
| 1: Seguridad Perimetral | ICAM, Sensor de movimiento, App Firewall, Honeypot, analisis de malware, seguridad de mensaje, IDPS (Intrusion Detection Prevention System), seguridad perimetral, seguridad física, zona demilitarizada segura, DLP |
| 2: Seguridad de red | ICAM, Enclave de firewalls, Acceso remoto empresarial, seguridad de mensaje, seguridad móvil, NAC, Network IDPS, Firewall virtual, protección VoIP (Voz en IP), filtrado por proxy web, DLP, bloqueo por DNS/IP de publicidad/trackers/etc |
| 3: Seguridad en endpoint | ICAM, seguridad en contenido, aplicación de seguridad en endpoint, IDPS en el sistema operativo, manejo de parches, firewall personal, cumplimiento de estándares NIST800/CIS/ENISA/PCI, DLP, EPP (Endpoint Protection Platform)|
| 4: Seguridad en aplicación | ICAM, Monitoreo y escaneo de configuración, Control de cambios, gestión de parches, prueba de penetración, WAF (Web Application Firewall), DLP, cifrado de la comunicación entre los pares conectados |
| 5: Seguridad en datos | ICAM, Protección DAR/DIM/DIU, lugar de almacenamiento de datos, cifrado en reposo, cifrado en transporte, prevención de exportación de los datos, sanitización de los datos a guardar/leer, manejo de permisos, ofuscación de datos, monitoreo de integridad |

Capas adyacentes a todas las anteriores;

- Prevención

1. Manejo de configuraciones
2. Pruebas de penetración
3. Entrenamiento continuo
4. Cumplimiento en políticas de seguridad humanas
5. Auditorias de vulnerabilidades
6. Modelado de amenazas
7. Gobernanza de la seguridad IT
8. Inteligencia de amenazas cibernéticas
9. Marco de trabajo para el manejo de riesgos
10. Plan de recuperación ante desastres
11. Marco de trabajo de cero confianza (ZeroTrust)

- Monitoreo y respuesta

1. Operaciones enfocadas a la detección de amenazas
2. CIRT
3. Análisis de comportamiento
4. Soluciones multi dominio
5. Forencia digital
6. Adminitración y manejo de escalamiento de privilegios
7. Respuestas ante amenazas
8. SIEM (Security Information and Event Management)
9. Sistemas de reporteria y alertas
10. ISCM

## Seguridad móvil

1. Autenticación centralizada en el dispositivo
2. On-boarding
3. Detección de conectividad a redes inalámbricas in/seguras
4. Revisión de amenazas basado en OWASP Mobile TOP 10
5. Escaneo de las aplicaciones instaladas y configuraciones
6. Detección de root/jailbreak en el dispositivo
7. Detección de aplicaciones inseguras o que no cumplen con los estándares de seguridad
8. Pruebas de penetración
9. Deshabilitación del IPC para bloquear la compartición de información sensible
10. Aplicación forzada de configuraciones según estándares

## Seguridad de la infraestructura

1. Seguridad en las zonas DNS
1. Seguridad en los servidores de correo y sus configuraciones DKIM, etc del DNS
1. AppArmor y SELinux
1. Kernel LandLock
1. Actualizaciones de seguridad
1. Uso de BTRFS ó XFS
1. Verificación de servicios (en systemd) corriendo de fondo y/o habilitados en el inicio de sistema (\-\-state=enabled)
1. Exportación y análisis de los registros para todos los eventos en las aplicaciones y sistemas operativos
1. Aislamientos de los usuarios e imposibilidad de ver archivos ajenos
1. Aplicación forzada de configuraciones según estándares
1. Uso de VPN como; wireguard, openvpn (preferiblemente wireguard por ser más simple, rápida y segura)
1. Bloqueo de nodos conocidos para evitar conectividad hacia Tor, Freenet, I2P, entre otros

## Seguridad en contenedores

1. Imagen base del contenedor y su propietario/publisher
2. Repositorio base de la imagen
3. INIT 1 del contenedor
4. Volumen de datos en el contenedor
5. Dispositivos físicos expuestos en el contenedor
6. Versionado del sistema base (el contenedor y su imagen) como de las aplicaciones instaladas
7. Puertos expuestos en el contenedor y en el host
8. Versión y que engine de contenedor se está usando (Docker, Podman, Containerd, CRI-O, etc)
9. Modelado de amenazas
10. Benchmarks como CIS Docker, etc
11. Hardenización del engine de contenedor
12. Uso de secrets y no de variables de entorno para pasar tokens
13. Shell deshabilitada en el contenedor como interactive/TTY
14. Contenedores sin permisos "privileged"
15. Contenedores no integrados nativamente (cloud cli, etc) a la nube
16. Exportación de logs fuera del contenedor

## Seguridad en Kubernetes

1. Todo lo anterior de contenedores
2. Uso de Ingress y no de NodePorts como servicios
3. Versión de Kubernetes en uso
4. Archivo de administración yaml del clúster 
5. Alta disponibilidad en cantidad para los worker y master
6. Kube-bench de Aquasecurity
7. Auditorias de; Kubernetes CronJob, 
8. Uso de Kubernetes Secrets o servicio de la nube integrado
9. Role Based Access Control (RBAC)
10. Dashboard expuesto; autenticación, etc
11. Exposición de la API de Kubernetes Master hacia fuera del clúster
12. No disponibilidad para saltar de un contenedor a otro (osea; los namespaces del cluster)
13. Uso de los service mesh para segurizar y monitorear la red de los contenedores con Mutual TLS habilitado (Istio por ejemplo)
14. Uso de agentes de políticas (Open Policy Agent por ejemplo)
15. Exportación, anaálisis y procedimientos con los registros del clúster
16. Integraciones del contenedor con terceros
17. Despliegues realizados con Helm
18. Configuraciones de auto escalado horizontal para los servicios (aka; replicas)
19. Configuraciones de auto escalado horizontal para los nodos worker
20. Verificar las identidades en el cluster
21. PODs sin metadatos sensibles


## Seguridad en bases de datos

1. Copias de seguridad automatizadas y cifradas de los datos
2. Aplicación contenerizada para portabilidad
3. Autenticación por defecto deshabilitada en el motor


## Seguridad en BigData

1. Análisis (Inteligencia) de registros multi-dominios para detección de comportamiento, correlaciones y eventos.
2. 

## Seguridad en PHP

Todo es en el archivo de configuración

1. Deshabilitar "remote connections"

```
allow_url_fopen = 0
allow_url_include = 0
```

2. Limitar tiempo máximo para los procesos de entrada y cuanto puede correr un script (todo en segundos)

```
max_input_time = 30
max_execution_time = 30
```

3. Limitar memoria máxima a utilizar

```
memory_limit = 8M
```

4. Deshabilitar que la data solicitada se almacene, por parte de PHP, en una variable global

```
register_globals=off
```

5. Deshabilitar la exposición de información

```
expose_php = 0
```

6. Deshabilitar que pueda ser llamado directamente, solamente a traves de un web server

```
cgi.force_redirect = 1
```

7. Limitar el tamaño máximo de entrada

```
post_max_size = 500K
max_input_vars = 100
```

8. No mostrar mensajes de error

```
display_errors = 0
display_startup_errors = 0
```

9. Habilitar logueo

```
log_errors = 1
error_log = [path_absoluto]/error_log
```

10. Incluir, leer y ejecutar archivos solamente de este lugar

```
open_basedir = "[path_absoluto]:[path_absoluto2]"
```

11. Deshabilitar la carga de archivos desde el usuario al PHP

```
file_uploads = 0
```

12. Carpeta temporal donde se suben los archivos

```
upload_tmp_dir = [path_absoluto]
```

13. Limitar tamaño máximo de subida

```
file_uploads = 1
upload_max_filesize = 2M
```

14. Usar una nueva ID de sesión sin reutilizar anteriores

```
session.use_strict_mode = 1
```

15. La cookie solo es accesible desde HTTP, no desde JS

```
session.cookie_httponly = 1
```

16. Guarda el ID de la sesion en la cookie, mas no en el parámetro de URL

```
session.use_cookies = 1
session.use_only_cookies = 1
session.use_trans_sid = 0
```

17. Actualizar en la cookie el ID de sesión cada vez que cambia

```
session.name = custom_session_id
```

18. La cookie solamente puede usarse desde HTTPS

```
session.cookie_secure = 1
```

19. Permitir solamente un dominio determinado como fuente de los datos para acceder a la sesión

```
session.referer_check = shyanjmc.com
```

20. Directorio a donde guardar los archivos de sesión por usuario

```
session.save_path = "[path_absoluto]"
```

21. Hash criptográfico a utilizar (PHP 5.3+)

```
session.hash_function = sha512
```

22. Deshabilitar las variables de sesión globales

```
session.bug_compat_42 = 0
session.bug_compat_warn = 0
```

23. Deshabilitar funciones inseguras del propio PHP

```
disable_functions = ini_set,php_uname,getmyuid,getmypid,passthru,leak,listen,diskfreespace,tmpfile,link,ignore_user_abord,shell_exec,dl,set_time_limit,exec,system,highlight_file,source,show_source,fpaththru,virtual,posix_ctermid,posix_getcwd,posix_getegid,posix_geteuid,posix_getgid,posix_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid,posix,_getppid,posix_getpwnam,posix_getpwuid,posix_getrlimit,posix_getsid,posix_getuid,posix_isatty,posix_kill,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid,posix_setpgid,posix_setsid,posix_setuid,posix_times,posix_ttyname,posix_uname,proc_open,proc_close,proc_get_status,proc_nice,proc_terminate,phpinfo,popen,curl_exec,curl_multi_exec,parse_ini_file,allow_url_fopen,allow_url_include,pcntl_exec,chgrp,chmod,chown,lchgrp,lchown,putenv
```

24. Directorio no default para almacenar cache SOAP

```
soap.wsdl_cache_dir = [path_absoluto]
```

## Seguridad en API (Application Programming Interface)

- Autorización a nivel de objeto - OWASP - A1

1. Verificar que se implementen las verificaciones de autorización con las políticas de usuario y la jerarquía
2. Verificar que la implementación de la API no dependa de las identificaciones enviadas desde el cliente, en su lugar, la API debe verificar las identificaciones de los objetos almacenados en la sesión.
3. Verificar que la configuración del servidor esté reforzada según la recomendación del servidor de aplicaciones y el marco en uso.
4. Verificar que la implementación de la API verifique la autorización cada vez que haya una solicitud de acceso a la base de datos por parte del cliente.
5. Verificar que la API no esté usando identificaciones aleatorias que se puedan adivinar (UUID) 

- Autenticación interrumpida - OWASP - A2

1. Verificar todas las formas posibles de autenticar todas las API 
2. Verificar que las API de restablecimiento de contraseña y los enlaces de un solo uso también permitan que los usuarios se autentiquen y que deban estar estrictamente protegidos.
3. Verificar que la API implemente estándares de autenticación, generación de tokens, almacenamiento de contraseñas y autenticación multifactor.
4. Verificar que la API use un token de acceso de corta duración.
5. Verificar que la API utilice una limitación de velocidad más estricta para la autenticación, implementar políticas de bloqueo y verificaciones de contraseñas débiles.

- Excesiva exposición de datos - OWASP - A3

1. Verificar que la API no dependa del cliente para filtrar los datos.
2. Verificar las respuestas de la API y adaptar la respuesta a lo que los consumidores de la API realmente necesitan.
3. Verificar que la especificación de la API defina los esquemas de todas las solicitudes y respuestas.
4. Verificar que las respuestas de la API de error estén claramente definidas.
5. Verificar que toda la información confidencial o PII se utilice con una justificación clara.
6. Verificar que las API apliquen verificaciones de respuesta para evitar fugas accidentales de datos y excepciones.

- Falta de recursos y limitación de velocidad - OWASP - A4

1. Verificar que la limitación de velocidad esté configurada teniendo en cuenta el método, el cliente y las direcciones de la API.2. Verificar que el límite de carga útil esté configurado.
3. Verificar la relación de compresión al implementar la limitación de velocidad.
4. Verificar la limitación de velocidad en el contexto de los recursos informáticos/de contenedor

- Autorización de nivel funcional interrumpida - OWASP - A5

1. Verificar que, de forma predeterminada, se denieguen todos los accesos
2. Verificar que, la API no dependa de la aplicación para imponer el acceso de administrador
3. Verificar que todas las funciones innecesarias estén deshabilitadas.
4. Verificar la limitación de velocidad en el contenido de los recursos informáticos/de contenedor
5. Asegurarse de que los roles se otorguen solo en función de un rol específico.
6. Verificar que la autorización se implemente correctamente en la API.

- Asignación masiva - OWASP - A6

1. Verificar que la API no vincule automáticamente los datos entrantes y los objetos internos.
2. Verificar que la API no defina explícitamente todos los parámetros y la carga útil que espera.
3. Verificar que, para los esquemas de objetos, utilice readOnly establecido en verdadero para todas las propiedades que se pueden recuperar a través de las API pero que nunca se deben modificar.
4. Verifique que las API definan con precisión en el momento del diseño los esquemas, tipos y patrones que aceptará en las solicitudes y los aplique en el tiempo de ejecución.

- Configuración incorrecta de seguridad - OWASP - A7

1. Verifique que la implementación de las API sea repetible y que las actividades de fortalecimiento y parcheo estén incorporadas en el proceso de desarrollo
2. Verifique que el ecosistema de API tenga un proceso automatizado para localizar fallas de configuración.
3. Verifique que la plataforma haya deshabilitado funciones innecesarias en cualquier API.
4. Verifique que la plataforma restrinja el acceso administrativo.
5. Asegúrese de definir y aplicar todas las salidas, incluidos los errores.
6. Verifique que la autorización se implemente correctamente en la API.

- Inyección OWASP - A8

1. Verifique que las API no confíen en sus consumidores de API, incluso si son internos. 
2. Verifique que las API definan estrictamente todos los datos de entrada: esquemas, tipos, patrones de cadena, y los apliquen en el tiempo de ejecución.
3. Verifique que las API validen, filtren y desinfecten todos los datos entrantes.
4. Verificar que las API estén definidas, limitar y hacer cumplir las salidas de API para evitar fugas de datos.

- Gestión inadecuada de activos - OWASP - A9

1. Verificar la capacidad de la plataforma documentar/inventar todos los hosts de API.
2. Verificar que la plataforma limite el acceso a todo lo que no deba ser público.
3. Verificar que la plataforma limite el acceso a los datos de producción. Acceso agregado a datos de producción y no producción.
4. Verificar que la arquitectura implemente controles externos adicionales como un firewall de API.
5. Verificar que se considere un proceso para retirar correctamente las versiones antiguas o reportar correcciones de seguridad
6. Verificar que la arquitectura implemente autenticación estricta, redirecciones, COR, etc.

- Registro y monitoreo insuficientes OWASP - A10

1. Verificar que la API registre intentos fallidos, acceso denegado, falla de validación de entrada y cualquier falla en las verificaciones de políticas de seguridad.
2. Verificar que la plataforma se asegure de que los registros estén formateados para que puedan ser consumidos por otras herramientas.
3. Verificar que la plataforma proteja los registros como altamente confidenciales.
4. Verificar que la plataforma incluya suficientes detalles para identificar a los atacantes.
5. Verificar que la plataforma se integre con SIEM y otros paneles de control, herramientas de alerta de monitoreo.

## SSL/TLS
SSL 3.0 es vulnerable a;

- POODLE (Padding Oracle On Downgraded Legacy Encryption) - CVE-2014-3566.
- BEAST (Browser Exploit Against SSL/TLS) si está el cipher; cipher block-chaining (CBC) - CVE-2011-3389.
- Raccoon si se tiene habilitado el cipher Diffie-Hellman (DH), DHE o con OpenSSL en versiones anteriores a 1.0.2w - CVE-2020-1968
- CRIME (Compression Ratio Info-leak Made Easy) si está habilitada la compresión. - CVE-2012-4929
- SHAttered si tiene habilitado SHA-1 - CVE-2005-4900

TLSv1.0 es vulnerable a;

- BEAST (Browser Exploit Against SSL/TLS) si está el cipher; cipher block-chaining (CBC) - CVE-2011-3389.
- POODLE (Padding Oracle On Downgraded Legacy Encryption) si está el cipher; cipher block-chaining (CBC) ó RC4.
- CRIME (Compression Ratio Info-leak Made Easy) si está habilitada la compresión. - CVE-2012-4929
- Raccoon si se tiene habilitado el cipher Diffie-Hellman (DH), DHE o con OpenSSL en versiones anteriores a 1.0.2w - CVE-2020-1968
- SHAttered si tiene habilitado SHA-1 - CVE-2005-4900

TLSv1.1 es vulnerable a;

- CRIME (Compression Ratio Info-leak Made Easy) si está habilitada la compresión. - CVE-2012-4929
- Raccoon si se tiene habilitado el cipher Diffie-Hellman (DH), DHE o con OpenSSL en versiones anteriores a 1.0.2w - CVE-2020-1968
- SHAttered si tiene habilitado SHA-1 - CVE-2005-4900

TLSv1.2 es vulnerable a;

- CRIME (Compression Ratio Info-leak Made Easy) si está habilitada la compresión. - CVE-2012-4929
- SLOTH (Security Losses from Obsolete and Truncated Transcript Hashes) si se encuentran habilitados los protocolos y ciphers; SHA1+MD5, MD5 y/o SHA1 - CVE-2015-7575
- Raccoon si se tiene habilitado el cipher Diffie-Hellman (DH), DHE o con OpenSSL en versiones anteriores a 1.0.2w - CVE-2020-1968
- SHAttered si tiene habilitado SHA-1 - CVE-2005-4900

Todos son vulnerables a;

- BREACH (Browser Reconnaissance and Exfiltration via Adaptive Compression of Hypertext ) si está habilitada la compresión HTTP. - CVE-2013-3587
- HeartBleed si el servidor remoto está usando OpenSSL en versiones anteriores a 1.0.1g
- Diversos tipos de ataques si tienen los ciphers; RC4, DSA, MD5, WEAK ELLIPTIC CURVES, RSA KEY EXCHANGE, DHE (RSa+DHE = Tripple Handshake), STATIC DIFFIE-HELLMAN (DH, ECDH)
- Sweet32 si está habilitado el cipher; cipher block-chaining (CBC) - CVE-2016-2183

|Ciphers                                |Nivel de entropía - bits|Soportado en TLSv1.1|Soportado en TLSv1.2|Soportado en TLSv1.3|Recomendado; Si/No|
|---------------------------------------|------------------------|--------------------|--------------------|--------------------|------------------|
|TLS_ECDHE_RSA_WITH_NULL_SHA            |0                       |-                   |Si                  |-                   |No                |
|TLS_ECDHE_ECDSA_WITH_3DES_EDE_CBC_SHA  |168                     |-                   |Si                  |-                   |No                |
|TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA    |168                     |-                   |Si                  |-                   |No                |
|SSL_RSA_WITH_3DES_EDE_CBC_SHA          |168                     |Si                  |Si                  |-                   |No                |
|TLS_ECDHE_ECDSA_WITH_RC4_128_SHA       |128                     |-                   |Si                  |-                   |No                |
|TLS_ECDHE_RSA_WITH_RC4_128_SHA         |128                     |-                   |Si                  |-                   |No                |
|SSL_RSA_WITH_RC4_128_SHA               |128                     |Si                  |Si                  |-                   |No                |
|SSL_RSA_WITH_RC4_128_MD5               |128                     |Si                  |-                   |-                   |No                |
|SSL_RSA_WITH_DES_CBC_SHA               |56                      |Si                  |-                   |-                   |No                |
|SSL_RSA_EXPORT_WITH_RC4_40_MD5         |40                      |-                   |-                   |-                   |No                |
|SSL_RSA_EXPORT_WITH_RC2_CBC_40_MD5     |40                      |-                   |-                   |-                   |No                |
|TLS_RSA_EXPORT1024_WITH_DES_CBC_SHA    |56                      |-                   |-                   |-                   |No                |
|TLS_RSA_EXPORT1024_WITH_RC4_56_SHA     |56                      |-                   |-                   |-                   |No                |
|SSL_RSA_WITH_NULL_SHA                  |0                       |Si                  |Si                  |-                   |No                |
|SSL_RSA_WITH_NULL_MD5                  |0                       |Si                  |-                   |-                   |No                |
|TLS_RSA_WITH_NULL_SHA256               |0                       |Si                  |Si                  |-                   |No                |
|SSL_NULL_WITH_NULL_NULL                |0                       |Si                  |Si                  |-                   |No                |
|SSL_DES_192_EDE3_CBC_WITH_MD5          |168                     |-                   |-                   |-                   |No                |
|SSL_RC4_128_WITH_MD5                   |128                     |-                   |-                   |-                   |No                |
|SSL_RC2_CBC_128_CBC_WITH_MD5           |128                     |-                   |-                   |-                   |No                |
|SSL_DES_64_CBC_WITH_MD5                |56                      |-                   |-                   |-                   |No                |
|SSL_RC2_CBC_128_CBC_EXPORT40_WITH_MD5  |40                      |-                   |-                   |-                   |No                |
|SSL_RC4_128_EXPORT40_WITH_MD5          |40                      |-                   |-                   |-                   |No                |
|SSL_RSA_FIPS_WITH_DES_CBC_SHA          |56                      |-                   |-                   |-                   |No                |
|SSL_RSA_FIPS_WITH_3DES_EDE_CBC_SHA     |168                     |-                   |-                   |-                   |No                |
|TLS_AES_128_GCM_SHA256                 |128                     |-                   |-                   |Si                  |Si                |
|TLS_AES_256_GCM_SHA384                 |256                     |-                   |-                   |Si                  |Si                |
|TLS_CHACHA20_POLY1305_SHA256           |256                     |-                   |-                   |Si                  |Si                |
|TLS_AES_128_CCM_SHA256                 |128                     |-                   |-                   |Si                  |Si                |
|TLS_AES_128_CCM_8_SHA256               |128                     |-                   |-                   |Si                  |Si                |
|TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384  |256                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256  |128                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384  |256                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256  |128                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA     |256                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA     |128                     |-                   |Si                  |-                   |Si                |
|TLS_RSA_WITH_AES_256_GCM_SHA384        |256                     |-                   |Si                  |-                   |Si                |
|TLS_RSA_WITH_AES_128_GCM_SHA256        |128                     |-                   |Si                  |-                   |Si                |
|TLS_RSA_WITH_AES_256_CBC_SHA256        |256                     |-                   |Si                  |-                   |Si                |
|TLS_RSA_WITH_AES_128_CBC_SHA256        |128                     |-                   |Si                  |-                   |Si                |
|TLS_RSA_WITH_AES_256_CBC_SHA           |256                     |Si                  |Si                  |-                   |Si                |
|TLS_RSA_WITH_AES_128_CBC_SHA           |128                     |Si                  |Si                  |-                   |No                |
|TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA   |128                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA   |256                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256|128                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384|256                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384|256                     |-                   |Si                  |-                   |Si                |
|TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256|128                     |-                   |Si                  |-                   |Si                |


