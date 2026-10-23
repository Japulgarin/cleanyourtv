# Solución de problemas

Cosas que nos complicaron a nosotros o a quienes contribuyen, para que no te pasen a ti. Los comandos usan `tools/tv.py`; consulta el
[README](../README.md#hacerlo-a-mano) para configurarlo.

## Conexión

- **macOS: `adb connect` dice "No route to host"** aunque el puerto está abierto. Las versiones recientes de macOS tratan
  el `adb` firmado por Google como una app propia dentro de la privacidad de Red local y lo bloquean en silencio.
  `tools/tv.py` evita por completo ese binario.
- **No hay opción de "depuración inalámbrica"** en algunas TV, entre ellas las Xiaomi. La depuración USB por sí sola abre
  ADB por red en el puerto 5555.
- **La depuración USB aparece en gris y tampoco hay una entrada de Depuración inalámbrica**, visto en un decodificador de operador
  ([Airtel Xstream, Android 11](https://github.com/Gathin23/cleanyourtv/issues/227)). Algunos firmwares de proveedores de internet
  eliminan ambos interruptores, y entonces no se puede llegar a ningún shell: `tools/tv.py` falla,
  `adb connect <ip>:5555` agota el tiempo de espera, y lo mismo pasa con una prueba de puerto. Ese tiempo agotado es culpa del firmware, no
  del Wi-Fi, el router o el cable, así que no te pongas a rehacer la red por eso. Que esté en gris en lugar de
  ausente apunta a una política de propietario del dispositivo o a un bloqueo de aprovisionamiento; el interruptor vuelve tras una
  actualización de firmware del proveedor, o no vuelve nunca. Sin uno de los dos interruptores este repositorio no tiene con qué
  comunicarse.
- **Las Opciones de desarrollador están ocultas, o el Número de compilación pide una contraseña**, visto en un decodificador de proveedor de internet (FPT Play
  650, Android TV 14): tocar Compilación siete veces abre una solicitud de contraseña en lugar de desbloquear el menú.
  A menudo solo está bloqueada la forma de entrar, no la pantalla en sí: TvSettings todavía tiene
  `com.android.tv.settings/.system.development.DevelopmentActivity`, y cualquier app puede abrirla por su
  nombre o con la acción `android.settings.APPLICATION_DEVELOPMENT_SETTINGS`. Instala desde Play Store una app que
  abra actividades por nombre (Activity Launcher), abre esa pantalla y activa allí la
  depuración USB. Si ninguna app puede abrirla tampoco, consulta el punto anterior sobre los decodificadores de operador.
- **La depuración USB nunca abre el puerto 5555** en algunos televisores Google TV (entre ellos un Philips fabricado por Skyworth).
  Vincula una vez mediante Depuración inalámbrica con el `adb` estándar (`adb pair <ip>:<port> <code>`,
  luego `adb connect`), ejecuta `adb tcpip 5555`, y a partir de ahí `tools/tv.py` funciona. `dns-sd -B
  _adb-tls-pairing._tcp` (o `adb mdns services`) muestra el puerto de vinculación mientras el código está en pantalla.
  Android desactiva la Depuración inalámbrica cada vez que se cae el Wi-Fi; vuelve a activarla y `adb` se reconecta
  sin un código nuevo. El puerto 5555 de `adb tcpip` normalmente dura solo hasta el siguiente reinicio. Cuando
  termines, desactiva la Depuración inalámbrica por separado: en un Chromecast con Google TV 4K (`sabrina`),
  desactivar la depuración USB dejó el puerto de Depuración inalámbrica aceptando conexiones, y
  `tools/adb-closed.py` solo revisa el 5555. `adb mdns services` muestra ese puerto mientras está abierto.
- **Los dispositivos USB dejan de funcionar mientras la depuración USB está activada**, visto en el Xiaomi Mi Box S y el Xiaomi TV
  Box S 3.ª gen. ([MiTV-AFMU0, Google TV 14](https://github.com/Gathin23/cleanyourtv/issues/737)):
  su firmware cambia el puerto USB al modo dispositivo ADB, lo que corta la alimentación a una bocina o
  unidad USB. Un **adaptador Ethernet USB usa ese mismo puerto**, así que la red se va con él y el equipo
  vuelve al Wi-Fi sin avisar. `dumpsys usb | grep host_connected` imprime `false`;
  `dumpsys connectivity | grep -o 'Transports: [A-Z]*'` imprime `WIFI` en un equipo que el dueño cree cableado.
  Un `eth0` solo, atascado en `NO-CARRIER`, es la MAC sin conector propia de estas placas, no el adaptador: en la
  TCL 65C735 el adaptador apareció como `eth1`. Cuánto sobrevive el puerto a la depuración depende del firmware:
  los dos equipos Xiaomi lo pierden en cuanto se activa la depuración, mientras que la 65C735 conservó el adaptador hasta que un
  reinicio con la depuración aún activa puso el puerto en modo gadget (`sys.usb.config=adb`, `Mstar-udc`) y
  nunca volvió ([el encabezado de esa lista](../examples/tcl-65c735/debloat.txt)). En cualquier caso no hay
  forma de revertirlo desde el shell en un equipo sin Depuración inalámbrica, y desactivar la depuración USB
  también detiene `adbd`, así que planéalo en una sola sesión en lugar de dos: desactiva la depuración al final, vuelve a conectar el
  adaptador y confirma que hay Ethernet antes de devolver la TV. El launcher nunca necesita la depuración.
- **Cierra el puerto 5555 cuando termines**: va en texto plano, y es un shell para cualquiera en la LAN cuando `ro.adb.secure=0`. Los pasos están en las preguntas frecuentes del README.
- **La TV está en una VLAN o red IoT separada** y `tools/tv.py` agota el tiempo de espera aunque la depuración
  esté activada: el router impide que la computadora llegue a ella. Agrega una regla de firewall temporal desde tu
  computadora hacia la TV solo en tcp/5555, y quítala de nuevo cuando cierres ADB. Abrir todo el
  segmento, o pasar la TV a la red principal de forma permanente, anula la razón por la que estaba separada.
- **Windows PowerShell 5.1 agrega una marca de orden de bytes (BOM)** al texto que se pasa por tubería a un programa, lo que convirtió el
  primer comando del lote en un galimatías. `tv.py` ahora la elimina, y los scripts `.ps1` envían UTF-8 limpio.
- **"¿Permitir la depuración USB?" vuelve a aparecer** aunque `adb devices` ya funciona: `tv.py` usaba su propia
  clave además de la que había registrado platform-tools. Ahora reutiliza `~/.android/adbkey` cuando
  existe. Cada intento con una clave no aceptada pone en cola un aviso más en la TV, así que ciérralos todos
  (Atrás) antes de hacer pruebas con pulsaciones de teclas.
- **Git Bash reescribe rutas** como `/data/local/tmp` a rutas de Windows. Los scripts configuran
  `MSYS_NO_PATHCONV=1` por ti. Define `JAVA_HOME` y `ANDROID_HOME` antes de compilar ahí.

## Trabajando en la TV

- **Los comandos `pm` encadenados** (`pm disable a; pm disable b`) pueden detenerse en silencio después del primero. Ejecuta
  uno por cada llamada al shell; `--batch` hace exactamente eso.
- **Las transferencias grandes se cuelgan** con el cliente de Python. Usa `tools/b64push.py` para los APK.
- **`tools/tv.py reboot` nunca regresa.** `reboot` es un comando de shell, y adbd se detiene antes de
  enviar el último `CLSE` del shell, así que el cliente espera una respuesta que no puede llegar: dos minutos,
  y luego un error, en una TCL 65C935 (`G05_4K_GB`, Google TV 11, AR2101,
  [#995](https://github.com/Gathin23/cleanyourtv/issues/995)). Una cadena que reinicia y luego revisa
  algo se queda trabada ahí. Usa `tools/tv.py --reboot`: envía el reinicio mediante el propio servicio de ADB
  y regresa en cuanto se acepta la solicitud. En ese momento la TV todavía se está reiniciando, así que espera a que
  vuelva a responder (`tools/tv.py --probe`) antes del siguiente comando.
- **Un `logcat` sin la línea que esperabas no prueba que no haya pasado nada.** En una TCL 55C728
  (`G05_4K_GB`, Google TV 11) el búfer principal es de 1 MiB (`persist.logd.size.main`), y el propio registro de
  HDMI, ARC y multimedia de la TV lo llena en mucho menos de un minuto; alrededor del encendido conservaba unos 30
  segundos. Un evento de activación o arranque leído un minuto después ya no está. Amplía el búfer para la
  sesión con `tools/tv.py 'logcat -G 16M'` (`logcat -g` muestra el tamaño; un reinicio restablece el del
  firmware), o deja `logcat` corriendo desde antes del evento. Para el sonido, `dumpsys audio` guarda un
  historial de eventos del reproductor que dura más que el registro.
- **Se rechaza cualquier forma de desactivar un paquete**, no solo una. En un Fire TV Box 2015 (`sloane`,
  Fire OS 5 / Android 5.1) `pm disable-user --user 0` devuelve `SecurityException`,
  `pm uninstall --user 0` devuelve `DELETE_FAILED_INTERNAL_ERROR`, y `pm hide` reporta éxito
  mientras `pm list packages -d` sigue vacío ([#577](https://github.com/Gathin23/cleanyourtv/issues/577)).
  Lee `pm list packages -d` después de cada intento en lugar del código de salida: `pm hide` es el que
  miente. Cuando los tres se rechazan, este firmware no acepta ninguna lista de limpieza: no hay ninguna ruta
  por shell para evitarlo, las filas patrocinadas se quedan en la pantalla de inicio, y el único trabajo útil que queda son los
  propios ajustes de privacidad de la TV más el bloqueo por DNS (Pi-hole con una lista de anuncios para smart TV; el reporte usó
  la lista `AmazonFireTV` de Perflyst). Fire OS 6 es el caso opuesto: `pm disable-user` funciona y unos
  diez paquetes de Amazon están protegidos, que
  [`examples/amazon-fire-tv-stick-4k-2018/debloat.txt`](../examples/amazon-fire-tv-stick-4k-2018/debloat.txt)
  enumera, con el mismo respaldo por DNS para sus endpoints.
- **El botón Input y CEC dejan de funcionar después de abrir el menú de fábrica oculto**, visto en un equipo Haier/CVTE
  (Durabrand `DURAT32ISDB`, `dupont`, Android TV 11 compilación `RTM6.230109.232`,
  [#470](https://github.com/Gathin23/cleanyourtv/issues/470)). `com.cvte.tv.hkcfac` es la
  app de producción del fabricante: `dumpsys package` la muestra como un componente de fábrica, y tiene una
  actividad que se puede iniciar, así que "a ver qué hace este paquete" basta para activarla. Abrirla
  establece `customer_factory_mode=true` en `/vendor/tvcertificate/fdata.ini` y
  `vendor.mtk.factory.disable.input=1`. Entonces el botón Input no hace nada y HDMI-CEC queda desactivado, y
  en el siguiente arranque `com.at.factory.factorymanager` desactiva Play services, Netflix,
  `com.google.android.katniss` y `com.google.android.apps.mediashell`; `pm enable` desde el shell
  se rechaza para esos, así que la transmisión (Cast) y la tienda siguen sin funcionar hasta que se borre el modo. Lee el
  paquete en lugar de iniciarlo. Si ya se abrió, inícialo, envía dos veces el código de tecla de salida del modo de fábrica
  **con la app en primer plano**, reinicia y luego vuelve a activar CEC:
  ```sh
  tools/tv.py 'am start -n com.cvte.tv.hkcfac/.MainActivity'
  tools/tv.py 'input keyevent 218; input keyevent 218'
  tools/tv.py --reboot             # returns once ADB accepts it; wait for the TV to come back
  tools/tv.py 'settings put global hdmi_control_enabled 1'
  ```
  Después presiona el botón Input real y comprueba que los paquetes volvieron:
  `tools/tv.py 'pm list packages -e | grep -E "gms|netflix|mediashell|katniss"'`. Hay más sobre el equipo en
  las [notas del dispositivo](devices/durabrand-durat32isdb.md).
- **Stremio parece tener su servidor caído después de la limpieza**, visto en una Xiaomi MiTV-MZTU0 (`river`,
  Google TV 14, [lista](../examples/xiaomi-tv-a-pro-2026/debloat.txt)). La app abre, los complementos
  cargan, y nada se reproduce nunca, lo que parece una falla del servidor local. No lo es: con
  `com.google.android.apps.mediashell` desactivado, el propio `stremio_server_process` de Stremio sigue
  corriendo, sigue escuchando en 11470/12470, sigue manteniendo conexiones ESTABLISHED con `api.strem.io`,
  y `logcat -b crash` está limpio. La versión de Stremio para Android TV reproduce a través de mediashell, así que el servidor
  está sano y lo que desapareció es la ruta de reproducción. `pm enable --user 0 com.google.android.apps.mediashell`
  lo arregló en ese equipo sin reiniciar y sin reinstalar. Revisa esto antes de culpar a tus complementos o
  a la red:
  ```sh
  tools/tv.py 'pm list packages -d | grep mediashell'     # output here = this is the cause
  tools/tv.py 'pm enable --user 0 com.google.android.apps.mediashell'
  ```
  Deja el paquete fuera de tu lista si usas Stremio en la TV, o transmite desde un teléfono.
- **Elegir HDMI 1 en el menú de Entradas abrió una app sin relación**, visto en una RCA Android TV 9
  (firmware Toptech/Zeasn `RTK2851P`, Realtek RTD2851P,
  [#805](https://github.com/Gathin23/cleanyourtv/issues/805)). El launcher cambia a una entrada de paso
  con un `ACTION_VIEW` *implícito* sobre el URI de canal de la entrada
  (`vnd.android.cursor.item/channel`), y solo envía el `input_action` del tema cuando nada reclama
  ese intent. "Nada lo reclama" es la trampa: ese firmware no tiene una app de Live TV para el URI,
  y ES File Explorer (`com.estrongs.android.pop/.app.transferstation.FileTransferStationActivity`)
  declara un filtro `VIEW` para el mismo tipo MIME, así que HDMI 1 abrió el administrador de archivos y
  nunca se llegó a `input_action`. Un equipo sin ningún controlador al menos muestra "Not available on this TV";
  un equipo con un controlador equivocado abre esa app. Pregunta qué app tomaría una fila antes de culpar al
  launcher:
  ```sh
  tools/tv.py 'cmd package query-activities --brief -a android.intent.action.VIEW -t vnd.android.cursor.item/channel'
  ```
  `live_tv_package` no ayuda: se aplica como `setPackage` solo en la fila de Live TV, y las filas
  HDMI y AV no llevan paquete. Hasta que el launcher compruebe que el controlador es una app de entrada de TV,
  oculta las filas: un tema con `source_panel_service` definido y `live_tv_package` vacío hace que
  la píldora de Entradas abra el propio panel de fuentes de la TV (lo que hizo quien lo reportó), o desactiva la app que
  responde. Reporta cualquier otro caso en lugar de tomarlo como una rareza del firmware: el caso del controlador equivocado necesita
  un cambio en el código fuente, no un ajuste.
- **`adb exec-out screencap -p` da un PNG roto** en algunos equipos MediaTek (Xiaomi, y los propios
  televisores Fire TV de Amazon): el binario imprime primero `Init wrapper sys mutex successful` en stdout.
  Guárdalo en la TV y descarga el archivo en su lugar: `screencap -p /data/local/tmp/s.png`, o recorta
  todo lo anterior al encabezado `\x89PNG`. `tools/tv.py --screenshot shots/home.png` hace el guardado,
  la descarga y la limpieza en un solo comando, y avisa cuando la captura pesa 0 bytes.
- **Play Protect bloqueó el launcher** ("app no segura bloqueada, creada para una versión anterior de Android")
  y `pm install` se colgó, y luego falló con `INSTALL_FAILED_VERIFICATION_FAILURE`, cuando apuntaba al
  SDK 29. Ahora apunta al 34; si compilaste una copia antigua, vuelve a compilar.
- **`pm install` falla con `INSTALL_FAILED_OLDER_SDK`** en un equipo más antiguo que el launcher: el
  `minSdk` del APK es un mínimo fijado al compilar, así que una TV con Android 7.0/7.1 (SDK 24/25) no puede aceptar la
  versión publicada en absoluto ([#576](https://github.com/Gathin23/cleanyourtv/issues/576)). Lee ambos números antes de
  cambiar nada: `tools/tv.py 'getprop ro.build.version.sdk'` y
  `grep minSdk launcher/app/build.gradle` (26, es decir, Android 8.0, al momento de escribir esto).
  `launcher/build-and-install.sh` ahora pregunta primero a la TV y se detiene mostrando ambos números, así que no se
  compila ni se envía nada a un equipo que lo va a rechazar; `build-and-install.ps1` solo lo reporta después de
  `pm install`, que falla de forma segura dejando intacto el launcher original. Bajar `minSdk` es un cambio en el código
  fuente, no un ajuste, y significa mantener tu propia copia: el launcher usa AndroidX y
  llamadas del framework más nuevas que la API 25, así que espera errores de compilación o un launcher que arranca y luego
  se cierra. Un APK producido recompilando el proyecto en otro lugar (un asistente, un compilador en línea, un
  zip "recompilado para API 25" de un foro) no es algo que este repositorio pueda verificar, y los scripts de instalación
  solo envían el APK que ellos mismos compilaron: una compilación firmada con otra clave no se
  instala sobre esta (`INSTALL_FAILED_UPDATE_INCOMPATIBLE`), así que desinstala primero la anterior si
  vas por ese camino, y mantén activado el launcher original hasta que el nuevo realmente arranque. En un equipo por debajo de
  `minSdk` la mitad de limpieza y privacidad sigue aplicando, desde la propia pantalla de inicio de la TV: lo que
  no se puede instalar es el launcher, no las listas. Si la línea `Failure [...]` menciona
  `INSTALL_FAILED_VERIFICATION_FAILURE` en su lugar, es el punto anterior: el verificador del instalador del firmware,
  no el nivel de API.
- **Las capturas de pantalla salen vacías** mientras Live TV, una entrada HDMI o Netflix están en pantalla, visto en TCL
  y en una [Sony KDL-49W800G](https://github.com/Gathin23/cleanyourtv/issues/92). Presiona Home antes de
  `screencap`. Una captura vacía no dice nada sobre la conexión ADB ni sobre la reproducción; revísalas
  por separado.
- **Las capturas de pantalla salen idénticas en lugar de vacías**, visto en un Amazon Fire TV Stick 4K 2.ª gen.
  (AFTKRT, karat, Fire OS 8) justo después de un reinicio: `screencap -p` seguía devolviendo el mismo PNG no vacío,
  byte por byte (mismo MD5), con actividades reanudadas completamente distintas y con minutos de diferencia. Parecía
  una captura real (negra) y costó tiempo real de depuración antes de que comparar el `md5` de dos descargas
  lo delatara. En ese momento `dumpsys SurfaceFlinger --display-id` mostraba `no identification data` para Display 0.
  Aquí no confíes en una descarga de `screencap` por sí sola: compárala con otra descarga, o
  revisa en su lugar `dumpsys activity activities | grep mResumedActivity` y eventos de teclas reales
  (`adb shell getevent -lt`).
- **Toda la interfaz se ve enorme y recortada, y no es el launcher**, visto en una Sony K-85XR70
  (`BRAVIA 4K AE2`, Android 14, firmware de China,
  [#590](https://github.com/Gathin23/cleanyourtv/issues/590)). Su interfaz funciona a 1920×1080 en un panel 4K
  por diseño ([#29](https://github.com/Gathin23/cleanyourtv/issues/29)), y dos arranques confirmados
  iniciaron con una densidad forzada de 640 cuando 320 funcionaba: todo duplica su tamaño, los mosaicos se recortan, y
  parece un error de la cuadrícula. Lee los valores forzados antes de tocar el diseño:
  ```sh
  tools/tv.py 'wm size'          # Physical size vs Override size
  tools/tv.py 'wm density'       # Physical density vs Override density
  tools/tv.py 'settings --user 0 get secure display_density_forced'
  ```
  Un `Override size` que quedó de un experimento antiguo de resolución es lo primero que hay que explicar, y una
  densidad guardada vacía es un valor predeterminado normal de Android, no un daño. `wm density reset` arregla la
  sesión; en este firmware volvió a 640 en el siguiente arranque, y `wm density 320` por sí solo no se
  mantuvo porque dejaba vacío el ajuste guardado. Agrega `settings --user 0 put secure
  display_density_forced 320` después, reinicia, y vuelve a leer las tres líneas antes de darlo por bueno.
  No copies el número a otra TV: anota primero los tres valores, y deshazlo con `wm density reset`
  más `settings delete secure display_density_forced`. Nota del dispositivo:
  [Sony K-85XR70](devices/sony-k85xr70-ae2.md).
- **Desactiva el launcher original solo después de instalar el nuevo**, o el botón Home termina en
  una app de pruebas de fábrica. Inicia primero el reemplazo a mano. `set-home-activity` puede reportar
  `Success` mientras HOME sigue resolviéndose al launcher original (prioridad 2) hasta que ese se desactive.
  Y revisa qué paquetes manejan realmente HOME antes de desactivar nada por nombre: en la Sony
  de arriba, `com.google.android.leanbacklauncher` tiene un receptor de arranque pero ninguna actividad HOME.
  `tools/disable.sh` ahora hace esa revisión por sí mismo: cuando la lista contiene la app dueña de Home y
  nada más en la TV responde a HOME, omite esa entrada y lo avisa (`FORCE_HOME=1` lo anula),
  así que aplicar una lista antes del traspaso ya no deja la TV sin launcher. Aplica la lista
  de nuevo después de que el script de instalación haya hecho del nuevo launcher el Home, para desactivar el anterior. Una app de pruebas
  de fábrica no cuenta como otra cosa: en una Xiaomi Mi TV 4A
  `com.duokan.factorytest/.FactoryLauncher` responde a HOME, así que la protección la deja fuera, junto con cualquier
  paquete llamado `*factorytest*`, `*factory_test*` o `*factorymode*`.
- **La TV ya no arranca después de una lista que desactivó los paquetes centrales de Android** (Mi TV
  Stick original, [#884](https://github.com/Gathin23/cleanyourtv/issues/884)). La lista de un agente incluyó
  `com.google.android.permissioncontroller`, `com.google.android.packageinstaller`,
  `com.google.android.ext.services`, `com.google.android.ext.shared`,
  `com.google.android.modulemetadata` y las superposiciones `com.google.android.overlay.modules.*`, además de
  el launcher original y setupwraith, y el stick nunca volvió. Esos son parte del propio Android,
  no bloatware. `tools/disable.sh`, `disable.ps1` y `check.py --fix` ahora rechazan cualquier lista que
  los mencione (o `com.android.providers.*` que no sean calendario, contactos, diccionario del usuario y
  números bloqueados, `com.android.systemui`, `com.android.shell`, `com.android.phone`,
  `com.android.settings`, `com.android.tv.settings` o `android`), sin ningún interruptor para anularlo.
  Si un equipo ya está atascado y todavía responde por ADB, ejecuta `pm enable` en cada uno de esos paquetes y reinicia;
  si ADB tampoco responde, un restablecimiento de fábrica desde el menú de recuperación suele ser la única forma de volver.
- **La TV se queda en el logo de arranque después de una lista, y desactivar la única app de Home basta para
  provocarlo**, visto en un equipo de la época de KitKat ([COOP COTV-0001](https://github.com/Gathin23/cleanyourtv/issues/795):
  Realtek `rtd298x`, Android 4.4.2, SDK 19). Se desactivaron 17 paquetes por ADB sobre Ethernet, cada uno
  respondió `new state: disabled-user` y `pm list packages -d` devolvió los 17; el launcher de fábrica
  `com.haiersoft.launcherproject2995hk` estaba entre ellos sin reemplazo, porque el
  launcher de aquí necesita Android 8.0. Después de apagar y encender, el equipo se quedó en el robot verde y
  `INICIALIZANDO` durante más de 20 minutos, a pesar de un corte de corriente y otro apagado/encendido con el control. Quien lo
  reportó lo aisló después: desactivar ese único paquete reproduce el bloqueo y volver a activarlo hace que
  el equipo arranque, así que ni el tamaño del lote ni el corte de corriente fueron la causa. Dos lecciones. Primero,
  que la pantalla esté atascada no significa que el equipo esté perdido: este todavía respondía por ADB en Ethernet mientras
  decía `INICIALIZANDO`, y `pm enable` en cada paquete del respaldo previo al cambio más un reinicio
  lo recuperaron (los pasos de recuperación están en las [notas del dispositivo](devices/coop-cotv-0001.md)). Segundo, un
  paquete del fabricante que parece no tener relación puede ser aquello sobre lo que corre el launcher: aquí desactivar `com.tsb.tv`
  detuvo el launcher con "Se ha detenido la aplicación lancherProject" en lugar de romper el
  arranque. Por eso una lista se aplica por lotes, con un reinicio y una revisión de la pantalla entre ellos,
  sobre todo en un equipo que no puede aceptar el launcher: deja en paz el launcher original y mantén ADB por
  Ethernet (KitKat no tiene opción de depuración por red, y en este el Wi-Fi cerró el 5555).
  `tools/disable.sh` omite al dueño de Home cuando puede identificarlo; desde
  [#795](https://github.com/Gathin23/cleanyourtv/issues/795) pregunta a `dumpsys activity` cuando falta `cmd
  package` (Android 6 y anteriores, donde ese comando no existe) y avisa cuando ninguno de los dos
  responde. Ese aviso significa que la protección no se ejecutó, no que la lista sea segura. Sin ADB y
  sin una imagen de recuperación del fabricante, un equipo atascado así sigue fuera de alcance.
- **Las Xiaomi del mercado chino rechazan un Home predeterminado aunque `set-home-activity` reporte éxito**,
  verificado en MiTV-AETP0 (dofus), Android 9, firmware 22.9.2.851: el framework filtra los candidatos HOME de terceros
  con una lista de nombres de paquete permitidos. Desactivar el launcher original selecciona entonces
  `FallbackHome`. Una compilación opcional con otro ID de aplicación funcionó con el launcher original aún activado;
  consulta las [notas del dispositivo y los pasos para revertir](devices/xiaomi-mitv-aetp0-dofus.md). Esto es distinto
  de que falte el selector de Home predeterminado o de un control que emite ALL_APPS.
- **El nuevo launcher sigue sin ser dueño de Home** después de desactivar el original, visto en Google TV
  (Xiaomi MiTV-MOOR2). Otra app del sistema responde a HOME: `com.google.android.tungsten.setupwraith`,
  con `.MainActivity` en prioridad 4 del filtro de intents y `.RecoveryActivity` en prioridad 1. No
  puedes superarla, y las soluciones obvias no ayudan: Android ignora `android:priority` en
  los filtros HOME de apps que no están en la imagen del sistema, `cmd package set-home-activity` imprime
  `Success` sin cambiar nada (ni siquiera después de reiniciar), y `pm disable-user` sobre uno de los
  componentes de setupwraith se rechaza con una SecurityException. Desactivar todo el paquete
  `com.google.android.tungsten.setupwraith` es lo que libera el lugar. Es el asistente de configuración
  inicial, así que el uso diario no se ve afectado, pero vuelve a activarlo antes de un restablecimiento de fábrica: inclúyelo en
  tu `debloat.txt` y `tools/restore.sh` lo hará por ti. Medido de nuevo en un Google TV
  Streamer (`kirkwood`, `UTTK.260317.003`): un launcher compilado con `android:priority="3"` en su filtro
  HOME (`aapt2 dump xmltree` lo encuentra en el APK instalado) sigue sin tener una línea `mPriority` en
  `dumpsys package`, y `cmd role get-role-holders android.app.role.HOME` nombra al nuevo launcher
  mientras la tecla HOME termina de todos modos en `setupwraith/.RecoveryActivity`. `cmd package resolve-activity`
  y `query-activities` responden con el ganador de la tabla del resolvedor, que no es necesariamente la
  actividad que toma el foco: `dumpsys activity activities | grep mFocusedApp` es la referencia real,
  y es lo que hay que revisar antes de decir que el reemplazo funcionó.
- **La TV se desconecta del Wi-Fi para siempre en cuanto se desactiva setupwraith**, visto en Google TV 14 (Sony
  BRAVIA 9 II, Philips R8G, Skyworth SWTV-24NA-4K NF, Xiaomi TV Box S 3.ª gen. MiTV-AFMU0) y en una TCL
  G07 con Google TV 11 (compilación AR17; en AR20 la red pertenecía a `android.uid.system`). Una red Wi-Fi
  guardada durante el asistente inicial pertenece a setupwraith, y Android borra las redes guardadas de una app
  cuando la app se desactiva. La TV está bien pero sin conexión, así que ADB y el control remoto del teléfono dejan de
  funcionar, y reiniciar no recupera la red. Revisa antes de desactivarlo: `tools/tv.py "dumpsys wifi" | grep -o 'cname=[^ ]*'`.
  Si nombra a setupwraith, olvida la red y vuelve a conectarte en Configuración > Red e Internet (entonces
  pertenece a `android.uid.system`), o usa Ethernet. `tools/disable.sh` omite setupwraith mientras sea
  dueño de la red (`FORCE_SETUPWRAITH=1` lo anula). ¿Ya está sin conexión? Vuelve a conectarte desde la TV con su propio
  control o un teclado USB, y luego vuelve a activar la Depuración inalámbrica si la estabas usando. Reconectar no
  basta; primero olvida la red (Xiaomi MiTV-MOSR4, donde esto también desactivó la depuración USB).
- **Un reinicio en la pantalla de recuperación de setupwraith restableció la TV de fábrica** (Xiaomi MiTV-MOSR4). Desactiva
  setupwraith antes que launcherx. Si `mFocusedApp` muestra `.RecoveryActivity`, vuelve a activar launcherx
  primero y no reinicies. [Notas](devices/xiaomi-mitv-mosr4.md).
- **Pantalla negra en cada arranque después del cambio de launcher, LED encendido, control sin respuesta** (Vision
  2024VISION43STV, CVTE, Android 13: [su lista](../examples/vision-2024vision43stv/debloat.txt) tiene los
  detalles). Con cifrado basado en archivos (`getprop ro.crypto.type` dice `file`) Android inicia Home antes
  del primer desbloqueo, y en ese momento solo puede iniciarse una actividad compatible con el arranque directo (direct boot). La mayoría de los firmwares tienen un
  `FallbackHome` que la sustituye hasta el desbloqueo; algunos, como esta placa CVTE, no, y entonces el arranque
  nunca termina. El launcher de este repositorio es compatible con el arranque directo; la mayoría de los otros launchers no. Revisa ambas cosas
  antes de desactivar el launcher original:
  ```sh
  tools/tv.py 'cmd package query-activities --brief -a android.intent.action.MAIN -c android.intent.category.HOME'
  tools/tv.py 'dumpsys package <new.launcher.package> | grep -o "[A-Z_]*DIRECT_BOOT_AWARE"'
  ```
  Si no hay `FallbackHome` en el primero y nada sale del segundo: mantén activado el launcher original y define
  Home solo con `cmd package set-home-activity`. Esa línea no prueba que el traspaso haya ocurrido: en un equipo
  cuyo launcher original declara una prioridad HOME puede imprimir `Success` y no cambiar nada, con el rol de Home
  ya nombrando al nuevo launcher mientras Home sigue abriendo el original, así que lee el resolvedor en su lugar
  (`tools/tv.py 'cmd package resolve-activity --brief -a android.intent.action.MAIN -c android.intent.category.HOME'`).
  Si sigue nombrando al launcher original, el equipo solo admite la limpieza hasta que alguien ejecute estas dos revisiones en
  esa placa exacta (Thomson 40FG2S14W, Expressluck `nagata`, Android TV 14 `UKNV.260317.001`,
  [notas](devices/thomson-40fg2s14w.md)).
- **Atascada en la animación de arranque después del cambio de launcher, sin ADB** (JVC LT-43N7115, CVTE
  `TP.SK706S.PC822`, Android 11, [#741](https://github.com/Gathin23/cleanyourtv/discussions/741)): se desactivó el
  launcher original `com.cvte.tv.launcher.space` y se activó un servicio auxiliar de teclas del control antes de un mismo reinicio.
  No se desinstaló nada, así que prueba en este orden: espera diez minutos una vez; arranca en modo seguro (en muchos equipos, mantén presionado Encendido en
  el control durante la animación), que desactiva las apps agregadas, y luego vuelve a activar el launcher
  original en Configuración > Apps > mostrar apps del sistema; sigue intentando `adb connect <ip>:5555` durante un par de
  minutos justo después de encender y ejecuta `pm enable com.cvte.tv.launcher.space` y
  `settings put secure enabled_accessibility_services ""` si responde (un punto de acceso del teléfono con el nombre y la contraseña
  de la red anterior sustituye a un router que falte); borra la partición de caché desde el menú de
  recuperación. Un restablecimiento de fábrica también funciona pero borra todo, así que va al final. El prompt ahora mantiene activado el
  launcher original en placas CVTE sin una lista probada.
- **Cuentas y perfiles aparece vacío después de desactivar el launcher original** (TCL 75C845X2, `G08_4K_GB`,
  Google TV 14, [#304](https://github.com/Gathin23/cleanyourtv/discussions/304)). Las cuentas siguen
  ahí (`dumpsys account` las muestra); la página vive en `com.google.android.apps.tv.launcherx`, y mientras
  launcherx esté activado recupera Home (`set-home-activity` imprime `Success` y no cambia nada, y
  su actividad de inicio no se puede desactivar desde el shell). Para cambiar de perfil: `pm enable --user 0
  com.google.android.apps.tv.launcherx`, cambia en Configuración, luego desactívalo de nuevo y define Home al final.
- **La búsqueda por voz de una canción o un video dice "Google Assistant is having trouble processing your request"**
  una vez que launcherx está desactivado, mientras que los comandos de apps ("abre YouTube") siguen funcionando. Visto en un onn 4K Streaming
  Box (`YOC`, Google TV 14, `URO4.260304.011.B1.15051976`). Google TV muestra esos resultados en su propia pantalla
  de inicio: el Asistente envía `VIEW https://tv.google.com/...` a launcherx
  (`.gateway.LauncherDeepLink`, luego `.home.HomeActivity` muestra los resultados, y elegir uno abre YouTube
  por paquete). Con launcherx desactivado no hay nada que abrir, y logcat muestra `Failed to execute
  provider.OPEN with status: UNKNOWN_ERROR` en menos de 100 ms. Dos cosas hacen que parezca otra cosa:
  justo después de que launcherx se haya ejecutado, el Asistente sigue mostrando resultados durante un rato aunque se haya desactivado
  de nuevo, y la falla vuelve solo después de un reinicio; y nada de la lista de limpieza importa: con todos los
  demás paquetes reactivados falla igual. El modo Solo apps (Configuración > Cuentas y acceso) no es una
  salida: desactiva el Asistente. Lo que funciona: dejar launcherx activado (entonces es Home, consulta el punto
  anterior) y abrir este launcher desde su fila de apps, donde la búsqueda por voz funciona normalmente porque la pantalla de
  resultados aparece encima; o buscar dentro de YouTube con su micrófono en pantalla. La comunidad de Projectivy llegó a
  lo mismo (los resultados de voz "necesitan la página de resultados de búsqueda del launcher X").
- **El botón del micrófono del control no hace nada, o abre el Asistente y este nunca te escucha**, visto en un
  Xiaomi TV Box S 3.ª gen. (`MiTV-AFMU0`, `twilight`, Google TV 14, `V816.0.7.0.UZFAABX`). Dos
  paquetes tienen que seguir activados, y reactivar solo uno de ellos es lo que hace difícil
  diagnosticarlo: `com.google.android.katniss` es el Asistente en sí, y
  `com.google.android.tv.remote.service` es el puente de Google TV para el control físico, que
  transporta el micrófono Bluetooth del control. Con ambos desactivados el botón no hace nada. Con solo
  `katniss` de vuelta el Asistente abre, toma `AudioRecord` (`inputSource 6`, VOICE_RECOGNITION) y
  graba silencio, porque el audio nunca sale del control. `pm enable` en ambos restaura el
  botón sin reiniciar (ejecuta `pm enable` una vez por paquete). Para distinguir las dos fallas: `dumpsys package
  com.google.android.katniss | grep enabled` y lo mismo para `tv.remote.service` (`enabled=3` es
  desactivado), luego `logcat -d | grep AudioRecord` justo después de presionar el botón: una sesión que
  se abre y se cierra sin reconocimiento es el puente que falta, no un Asistente roto. La lista de la AFMU0
  ahora conserva ambos; las listas que todavía desactivan `com.google.android.tv.remote.service` son
  `rca-ai-pont`, `sharp-aquos-tve21f`, `sony-bravia-4k-gb-us`, `sony-xbr-65x900f`,
  `sony-xbr-x900e`, `tcl-32s5k`, `tcl-40s5400a`, `tcl-55s470g`, `tcl-beyondtv2-android-11`,
  `tcl-g09-google-tv`, `tcl-g10-google-tv`, `xgimi-horizon-s-pro`, `xgimi-mogo-3-pro` y
  `xiaomi-mi-box-s`. Esas TV no se han probado para esto, pero cualquiera de ellas cuyo control tenga
  micrófono puede mostrar el mismo síntoma.
- **Transmitir desde un teléfono falla con "Untrusted device" después de desactivar setupwraith**, visto en
  Chromecast con Google TV HD (`boreal`) con Google TV 14 compilación UTTC.250917.004, la compilación sobre la que se hizo la lista
  `examples/google-chromecast-gtv-4k/`. YouTube en el teléfono dice "Untrusted device.
  ... couldn't be verified", y logcat repite `cast_ClientAuthCredsProvisioning: Loading factory
  credentials for 1P device`, `Failed to find provider info for ...CastInfoProvider` y
  `cast_shell: No private key, hence empty signature`. El receptor de Cast
  (`com.google.android.apps.mediashell`) carga sus credenciales de fábrica del dispositivo desde un proveedor de contenido
  dentro de setupwraith (`...tv.setupwraith.libs.castinfo.CastInfoProvider`), así que desactivar el asistente
  se lleva las credenciales con él. Vuelve a activarlo y en menos de un minuto el registro muestra
  `SetupWraith|CastInfoProvider: querying cast infos` y `Created singleton instance of
  ClientAuthSigner`, y la transmisión funciona. No puedes conservar el proveedor y renunciar solo a Home:
  `pm disable-user` sobre `setupwraith/.RecoveryActivity` se rechaza con `SecurityException: Shell
  cannot change component state`. Así que o haces la limpieza sin tocar setupwraith y launcherx, o vuelves a activar
  setupwraith después de cada arranque, esperas a `ClientAuthSigner` y luego lo desactivas de nuevo: el receptor guarda
  las credenciales en memoria, así que la transmisión sobrevive hasta el siguiente reinicio, y solo en ese proceso.
  `am force-stop com.google.android.apps.mediashell` seguido del regreso del receptor imprime
  `Retry loading factory credentials` y `No private key, hence empty signature` otra vez, así que cualquier cosa
  que lo reinicie (un cierre inesperado, un force-stop, una actualización) necesita la misma secuencia. Reactivar el
  asistente no siempre basta después de un reinicio: en un Chromecast con Google TV 4K (`sabrina`,
  UTTC.250917.004) no apareció ninguna línea `ClientAuthSigner` en 3 minutos y los teléfonos ni siquiera mostraban el
  dispositivo. En su lugar, reinicia el receptor mientras setupwraith está activado: `am force-stop
  com.google.android.apps.mediashell`, luego `am start-foreground-service -n
  com.google.android.apps.mediashell/.CastReceiverService` (después de un force-stop nada lo vuelve a
  iniciar), y la línea del firmante y `MdnsAppFilter: Done announcing.` aparecen en segundos. Reportado en el
  propio hardware Chromecast de Google (`boreal`) y, con las mismas líneas de registro, en un Google TV Streamer
  (`kirkwood`, `UTTK.260317.003`), donde el `CastInfoProvider` también vive dentro del APK de
  setupwraith; la lista del Xiaomi Mi Box S 2.ª gen. dice que ahí transmitir desde un Pixel sigue funcionando con
  setupwraith desactivado.
- **La transmisión desaparece aunque el receptor de Cast sigue corriendo**, visto en una TCL 75QM751G (QM7,
  Google TV 14) después de aplicar su lista, y la misma conclusión de "vivo no significa visible" en una TCL
  BeyondTV2 (Android TV 9, R851T02 V660) en el mismo hilo. Los teléfonos y una PC dejan de ver la TV,
  `com.google.android.apps.mediashell` está activo y escuchando en 8008/8009, y no hay ninguna línea
  `No private key` ni `CastInfoProvider`, así que no es el caso de setupwraith de arriba, y
  reactivar setupwraith no ayuda. Revisa el descubrimiento en lugar del proceso:
  `tools/tv.py "logcat -d -s cast_shell | grep -E 'Done announcing|responses sent'"` y
  `tools/tv.py "dumpsys activity service com.google.android.apps.mediashell | grep WargService"`.
  Un receptor que se está anunciando registra `MdnsAppFilter: Done announcing.`,
  `responses sent in 60 seconds: N` y `Gcm.Register.Success=2`, con `WargService` activo. Si esas faltan
  mientras el proceso sigue vivo, el receptor está colgado: el reporte de la QM7 vio sus conexiones detenidas
  en `CLOSE_WAIT` en el 8009 con datos sin leer. `tools/tv.py "am force-stop
  com.google.android.apps.mediashell"` lo reinicia (la TV lo vuelve a iniciar cuando hace falta), y
  el anuncio volvió en segundos, sin reiniciar. Notas del dispositivo:
  [TCL 75QM751G](devices/tcl-75qm751g-qm7.md).
- **La TV se desconecta del Wi-Fi cada minuto justo después de la instalación**, visto en Google TV 14 (Xiaomi
  MiTV-MZTU0): el mismo `.RecoveryActivity` de setupwraith tomó Home y system_server entró en un ciclo de cierres
  por su causa. El script de instalación ahora inicia el nuevo launcher antes de desactivar el original, define la
  preferencia de Home al final (Android la descarta cada vez que cambia el conjunto de apps HOME), luego revisa adónde
  se resuelve Home y reactiva el launcher original si no es el nuevo. Desactiva setupwraith como se explica
  arriba. Para confirmar que es este error: `logcat -b crash` muestra `FATAL EXCEPTION IN SYSTEM PROCESS:
  android.display`, y el registro principal muestra `setupwraith/.RecoveryActivity` iniciándose cada
  200 ms más o menos. En un Google TV Streamer (`kirkwood`, `UTTK.260317.003`) el mismo ciclo vino con su
  propia firma, `IllegalArgumentException: positionChildAt: container=Task=... is not a child of
  container=Task=1 current parent=null` en `WindowContainer.positionChildAt` /
  `Task.moveToBack` / `TransitionController.tryStartCollectFromQueue`, y se repetía aproximadamente cada
  47 s, y en cada ciclo también caían setupwraith y SystemUI con `DeadSystemException`. Si ya
  estás en el ciclo:
  `tools/tv.py 'pm enable --user 0 com.google.android.apps.tv.launcherx'`.
- **`theme.sh` falla con "couldn't create file: Permission denied"**, visto en TCL G07 (Android 11): el
  shell no está en el grupo que puede escribir en `Android/data`. `theme.sh` prepara los archivos en
  `/data/local/tmp` y los escribe a través del `ThemeProvider` del launcher, que los crea como el
  launcher; `cp` es solo el respaldo para un launcher instalado antes de que existiera ese proveedor: ejecuta
  `launcher/build-and-install.sh` una vez, y luego vuelve a enviar el tema.
- **Un envío de tema imprime "is on the TV" y nada cambia**, visto en Android 14: ahí el shell *sí puede* escribir en
  `Android/data`, así que `cp` funcionó, pero el archivo que creó pertenecía al shell (`ls -ln` muestra
  `2000 1078` en lugar del uid del launcher) y el launcher registró `W TvHome.Config: ignoring
  .../config.json: open failed: EACCES (Permission denied)`. Sobrescribir un archivo que el propio launcher escribió
  conserva su dueño, así que esto solo afectó a archivos que todavía no existían: se veía bien en un equipo al que ya se le había
  aplicado un tema antes y no hacía nada en una instalación nueva o justo después de reinstalar. `theme.sh` ahora elimina la
  copia del shell y escribe primero a través del `ThemeProvider` (el proveedor no puede truncar un archivo cuyo dueño es el
  shell); en una copia antigua, volver a enviar el tema después de que `launcher/build-and-install.sh` haya escrito
  los archivos una vez también corrige el dueño.
- **Google TV vuelve después de unas cuantas pulsaciones del control**, visto en XGIMI (MoGo 3 Pro, Google TV 14). Los
  botones de apps del control (YouTube, Netflix, Prime Video), el botón programable, el botón de perfil y el de encendido
  envían teclas F que el sistema entrega a `com.xgimi.xrmservice/.XgimiGlobalKeyBroadcast` como teclas globales
  (`tools/tv.py 'dumpsys window' | grep -A40 mKeyMapping` las muestra). Ese receptor ejecuta
  `pm enable com.google.android.apps.tv.launcherx` con cada una de ellas, así que el launcher original recupera Home.
  Las teclas listadas en `app_keys` las toman los servicios de teclas antes del despacho de teclas globales, así que el receptor de XGIMI nunca
  las ve: `examples/xgimi-mogo-3-pro` incluye los botones de apps. El de encendido (F11) no se puede tomar, porque su
  manejo de suspensión y del menú de encendido necesita permisos del sistema. Para ese, ejecuta con `HOME_KEY_SERVICE=1` y define
  `stock_home_redirect` como `com.google.android.apps.tv.launcherx`: si vuelve, su pantalla de inicio se redirige
  directamente aquí, y `tools/disable.sh` con la lista lo desactiva de nuevo.
- **No hay teclado en pantalla** después de cambiar de launcher, visto en Xiaomi: el método de entrada predeterminado
  apuntaba a un teclado de Baidu que no está instalado. Solución:
  `tools/tv.py 'ime set com.google.android.inputmethod.latin/com.android.inputmethod.latin.LatinIME'`
- **Los launchers de terceros** a menudo cobran por cosas básicas como un fondo de pantalla personalizado. Por eso este repositorio
  tiene el suyo propio.
- **Zona horaria incorrecta, reloj desfasado 30 o 60 minutos**, visto en Xiaomi en Irán: la TV eligió una
  zona vecina, y los firmwares antiguos traen datos de zona horaria de antes de que Irán abandonara el horario
  de verano en 2022 (en Android 10 y posteriores, compruébalo con
  `tools/tv.py 'cat /apex/com.android.tzdata/etc/tz/tz_version'`). Define la zona tú mismo:
  `tools/tv.py 'settings put global auto_time_zone 0; cmd alarm set-timezone Asia/Tehran'`.
  Si después el reloj se adelanta una hora en primavera, un desfase fijo lo mantiene correcto:
  `tools/tv.py 'cmd alarm set-timezone GMT+03:30'`. Lo mismo aplica a cualquier país cuyas reglas
  cambiaron después de que se compiló el firmware.
- **La píldora de red dice "Wi-Fi" en lugar del nombre de la red** después de `pm clear com.gathin.tvhome`
  o de una reinstalación desde cero: borrar los datos del launcher también quita el permiso de ubicación que
  Android 10 necesita para leer el SSID. `pm grant com.gathin.tvhome android.permission.ACCESS_FINE_LOCATION`
  (el script de instalación lo hace).
- **Home muestra "Seleccionar una app de inicio"** después de `tools/restore.sh` seguido de volver a aplicar una lista: desactivar un
  paquete que también reclama HOME (PatchWall en Xiaomi) hace que Android descarte el predeterminado. El script de instalación
  ahora elige por sí mismo el launcher original conocido entre los candidatos; si no, elige uno en
  la TV o pasa `STOCK_LAUNCHER=<package>`.
- **Stremio falla en cada stream con `ConnectException: Failed to connect to /127.0.0.1:11470`**,
  y solo Forzar detención lo recupera hasta el siguiente reinicio. No es la limpieza. Es una regresión de Stremio
  en la 1.11 ([stremio-bugs#2866](https://github.com/Stremio/stremio-bugs/issues/2866)):
  `startServer()` solo se ejecuta una vez que el ciclo de vida está al menos en STARTED, así que un proceso que Android despertó en
  segundo plano nunca inicia el servidor local, y abrir la app reutiliza ese proceso. En una TV quien lo
  despierta es el propio `BootReceiver` de Stremio al actualizar los canales de la pantalla de inicio, así que pasa en cada
  arranque. Salir de la app y volver a abrirla no ayuda (mismo pid); cualquier proceso nuevo sí, incluido
  `am kill`. Evitar que el proceso despertado en el arranque se quede corriendo lo arregla para siempre:
  `tools/tv.py 'cmd appops set com.stremio.one RUN_ANY_IN_BACKGROUND ignore; cmd appops write-settings'`.
  El segundo comando no es opcional: los app-ops se escriben en disco de forma diferida, y en un equipo Vestel shandao
  la operación había vuelto a `allow` después del siguiente reinicio sin él, lo que parece exactamente que la
  solución no funciona. Una app iniciada en primer plano no se ve afectada, y el efecto secundario, que
  los canales de la pantalla de inicio solo se actualizan mientras Stremio está abierto, no cuesta nada si las filas de
  recomendaciones ya están desactivadas de todos modos.
- **Una actualización de firmware deshace la limpieza sin avisar.** La actualización se instala sobre el sistema ya limpio, así que
  todos los paquetes de la lista vuelven a activarse, Home regresa al launcher original y aparecen nuevas apps preinstaladas
  que ninguna lista menciona. `tools/venv/bin/python -I tools/check.py <list>` reporta las dos primeras cosas
  y sale con 1; `--fix` vuelve a desactivarlos y pone de nuevo el launcher en Home. Las nuevas apps preinstaladas no
  las puede conocer, así que después de una actualización grande compara `tools/tv.py 'pm list packages'` con la lista
  una vez a mano. En una TV cuya lista desactiva el actualizador, esto solo pasa cuando instalas una
  actualización a propósito: activa el actualizador, actualiza, ejecuta `check.py --fix` y desactívalo de nuevo.

## Servicio auxiliar de accesibilidad activado, pero el botón del control no hace nada

Los servicios opcionales `HomeKeyService` e `InputKeyService` solo filtran las teclas del control una vez que Android se ha vinculado a
ellos. El mensaje `enabled` del instalador significa que se escribió el ajuste, no que el servicio esté vinculado.
Lee el estado sin cambiar nada:

```sh
tools/tv.py 'am get-current-user'
tools/tv.py 'settings --user current get secure enabled_accessibility_services'
tools/tv.py 'dumpsys accessibility'
```

| Servicio auxiliar | Componente en la lista de servicios activados | Tecla que filtra |
| --- | --- | --- |
| Botón Home | `com.gathin.tvhome/.HomeKeyService` | `KEYCODE_ALL_APPS` (no un `KEYCODE_HOME` común) |
| Botón Input | `com.gathin.tvhome/.InputKeyService` | `KEYCODE_TV`, `KEYCODE_TV_INPUT`, además de los códigos de tecla en `input_key_keycodes` y `app_keys` (`config.xml` o un tema) |

Forzar la detención del launcher (Configuración > Apps, una app de limpieza, `am force-stop`) saca a ambos servicios auxiliares de
esa lista. Con `restore_key_services` activado (`config.xml` o un tema) y `WRITE_SECURE_SETTINGS` concedido
(`RESTORE_KEY_SERVICES=1` al instalar, `-RestoreKeyServices` en Windows), Home vuelve a poner en la lista los servicios auxiliares que estaban
corriendo la próxima vez que inicia; un servicio auxiliar desactivado en Configuración sigue desactivado.

- **Activado** significa que el componente está en la lista separada por dos puntos de ese usuario (la clase puede estar escrita
  completa, `com.gathin.tvhome/com.gathin.tvhome.HomeKeyService`). Compara el componente completo.
- **Vinculado** significa que aparece en la sección `Bound services` de ese usuario en el volcado (`services` en compilaciones
  más antiguas). Dale unos segundos después de activarlo y vuelve a leer. Las etiquetas del volcado pueden estar traducidas o
  compartidas con otros servicios; una línea que contiene "Home" no es prueba.
- **Funcionando** significa que el botón físico hace lo correcto desde dentro de otra app. Una tecla inyectada
  por ADB prueba la navegación, no que el control envíe el código que este servicio auxiliar filtra. Ni siquiera
  llega al servicio auxiliar: `input keyevent` se salta el filtrado de teclas de accesibilidad, así que un `KEYCODE_TV` inyectado no hace
  nada aunque el botón Input real funcione.
- **Qué código de tecla** envía un botón que no responde: `dumpsys window policy` muestra las "teclas globales" que Android dirige
  a una app (en Google TV varias van a launcherx, que está desactivado), y el firmware de Xiaomi registra cada
  pulsación como `handleAction<keycode>` en `logcat`. Ponlo en `input_key_keycodes` (abre Entradas) o en
  `app_keys` (`keycode:package`, o `hold:keycode:package` para una pulsación larga), reinstala con
  `INPUT_KEY_SERVICE=1` y presiona el botón real.
  Una pulsación que `logcat` reporta como `KEY_UNKNOWN` o `KEY_PROGRAM` no se puede identificar por código de tecla en absoluto,
  porque todos los botones sin asignar comparten esos códigos: usa el scancode de Linux de
  `tools/tv.py 'getevent -lt'` en `settings_key_scancodes` e instala con `HOME_KEY_SERVICE=1`
  (un control RC-36 envía así su engrane en el scancode 240 y su botón de notificaciones en el 362; consulta
  [la nota de la FPD CG50-C3](devices/fpd-cg50-c3.md)).
  Sin embargo, no todos los equipos responden a esas dos rutas ([#853](https://github.com/Gathin23/cleanyourtv/issues/853),
  una PEAQ "AI PONT DE", `DVB99PQ` / Changhong `changi`, Google TV 14, `UKNV.260504.001`): un uso HID
  de control de consumo imprime un `MSC_SCAN` de evdev que no es necesariamente el `KeyEvent.getScanCode()`
  que reporta el framework, así que un valor leído con `getevent -lt` puede no coincidir con nada en
  `settings_key_scancodes` (el engrane de ese equipo imprimió `MSC_SCAN 000c009f`, y ni 159 ni 786591, las
  dos formas de escribirlo, hicieron nada), y `logcat -v time -s InputReader:D`, el filtro que sugiere `config.xml`,
  no imprimió ninguna línea de tecla ahí, para ningún botón, solo `Reconfiguring input devices`. Lo que
  Android entrega realmente se obtiene con un `Log.d` temporal al inicio del `onKeyEvent` del servicio auxiliar que imprima
  `getKeyCode()`, `getScanCode()` y `getDeviceId()`, recompilado con `HOME_KEY_SERVICE=1` y leído con
  `tools/tv.py "logcat -s TvHomeKeys:D"` mientras se presiona el botón real: ese equipo reportó
  `action=0 keyCode=83 scanCode=240 deviceId=9`, y `settings_key_keycodes = [83]` abrió la Configuración
  de la TV de inmediato. Así que un código de `getevent` que no coincide con nada no prueba que la pulsación no haya llegado, y
  consumir la tecla en el servicio auxiliar también evita que llegue al receptor del fabricante
  `com.homwee.factory/.FactoryKeyReciver`, al que `dumpsys window policy` dirige `KEYCODE_NOTIFICATION`
  una vez que el launcher original ya no está.
- **Todos los botones del fabricante dejan de funcionar a la vez** y `logcat` dice `GLOBAL_BUTTON ... process is bad`: el
  receptor de teclas globales se cierra por el launcherx desactivado y Android deja de iniciarlo. Asigna cada uno de esos
  códigos de tecla en los servicios auxiliares, también para apps desactivadas. Consulta [la nota de la MOSR4](devices/xiaomi-mitv-mosr4.md).
- **La lista todavía nombra al servicio auxiliar pero `accessibility_enabled` es `0`**, así que no hay nada vinculado y el
  botón no hace nada (no es el caso de forzar la detención de más abajo): en una TCL C6K Pro (`G08`, Android 14,
  [#1047](https://github.com/Gathin23/cleanyourtv/issues/1047)) un reinicio dejó
  `enabled_accessibility_services` nombrando a `com.gathin.tvhome/com.gathin.tvhome.HomeKeyService` mientras
  `accessibility_enabled` marcaba `0`, `dumpsys accessibility` mostraba `Bound services:{}` y el botón Home
  abría Google TV. `restore_key_services` no repara este estado: `ServiceRepair` escribe
  `accessibility_enabled 1` solo en la ruta que también vuelve a poner en la lista un servicio auxiliar que falta, y aquí
  la lista estaba completa. Vuelve a escribir la marca y luego lee el volcado otra vez; desactivar y activar el servicio
  en Accesibilidad, que es lo que hizo el dueño, recuperó la redirección para esa sesión. No se volvió a probar en ese equipo
  si la marca sobrevive al siguiente reinicio, y no está establecido qué la borró:

  ```sh
  tools/tv.py 'settings get secure accessibility_enabled'
  tools/tv.py 'settings put secure accessibility_enabled 1'
  tools/tv.py 'dumpsys accessibility'
  ```

Forzar la detención desactiva los servicios auxiliares para siempre: después de `am force-stop com.gathin.tvhome` (o Forzar detención en
Configuración > Apps) Android quita los servicios del launcher de la lista de activados, y no vuelven
cuando el launcher inicia de nuevo (visto en una TCL 55C715, Android TV 9). Actívalos otra vez de la misma forma que lo hiciste
la primera vez, y evita forzar la detención del launcher mientras haces pruebas.

Activado pero nunca vinculado apunta a una restricción del firmware sobre el inicio automático de servicios instalados manualmente (algunas compilaciones de TCL
registran denegaciones de `OP_AUTO_START`). Busca en `logcat` el fallo de vinculación antes de cambiar ajustes,
y no reescribas la lista de servicios activados ni concedas app-ops como solución general. En una TCL 55S470G (Google
TV 12) la línea es `[TclAppBoot] ... calleeComponent = 'com.gathin.tvhome/.HomeKeyService', bootType =
'bind_service', isAllow = 'false', reason = 'callee_does't_have_OP_AUTO_START_permission.'`, y
`appops get com.gathin.tvhome` muestra `APP_AUTO_START: ignore`. Permitir esa única operación solo para el launcher
y guardarla (`appops set com.gathin.tvhome APP_AUTO_START allow; appops write-settings`) hizo que el servicio
se vinculara por sí solo después de un reinicio; desactivar y activar el servicio en Accesibilidad funciona hasta el siguiente
reinicio. Los app-ops llegan al disco de forma diferida: sin `write-settings`, un reinicio poco después del `set` descarta el
cambio y la denegación vuelve. Visto en una TCL C89B (Google TV 14, `G08`, `UTT2.250416.001 AU02`), cuyo registro
dice `[TclAppBoot]:forbid bind service ComponentInfo{com.gathin.tvhome/com.gathin.tvhome.HomeKeyService}`
y cuyo `appops get` llama a la operación `AUTO_START`: usa el nombre que imprime `appops get`. Al reportar, indica el
modelo, la compilación, el usuario actual y las líneas relevantes sin datos sensibles, no el volcado completo.

## La app SHIELD TV del teléfono se conecta, pero ninguna tecla hace nada

En una NVIDIA SHIELD, la app SHIELD TV del teléfono encuentra el equipo y se conecta, pero el D-pad, OK, Atrás y
los botones de encendido de la app no hacen nada. Reiniciar el servidor remoto los recupera hasta el siguiente
reinicio. Los servicios auxiliares de teclas no son la causa: pasa también con ellos desactivados.

Las teclas de la app pasan por `com.nvidia.shield.remote.server`, que las inyecta mediante su propio
`virtualinput.InputService`, un `TvRemoteProvider` al que el servicio de control remoto de TV de Android se vincula al arrancar.
Lee el estado sin cambiar nada:

```sh
tools/tv.py "logcat -d | grep -E 'Key injection failed|Beyonder_VIS'"
tools/tv.py "dumpsys activity services com.nvidia.shield.remote.server | awk '/\* ServiceRecord/{inb=/virtualinput.InputService/} inb' | grep -c IntentBindRecord"
```

`Key injection failed` con `Beyonder_VIS ... mProvider ... isInitialized=false`, y un conteo de `0`, es
esta falla: el servicio corre pero Android nunca se vinculó a él. `1` es un servicio vinculado que funciona.

Causa: `com.google.android.tvrecommendations` desactivado. Con él desactivado, el proveedor no se vincula después
del arranque. Aislado con un reinicio por paso en una SHIELD 2017 (`darcy`) y confirmado en una 2015/2017
(`foster_e`), ambas con SHIELD Experience sobre Android 11: cada reinicio con él desactivado dejó el conteo en `0`,
cada reinicio con él activado dio `1`. Solución:

```sh
tools/tv.py "pm enable com.google.android.tvrecommendations"
```

Espera unos 20 segundos antes de reiniciar: Android escribe el estado de los paquetes en disco con retraso, y un reinicio
inmediatamente después de `pm enable` puede perder el cambio. `am force-stop com.nvidia.shield.remote.server` hace que
Android vincule el proveedor de inmediato, pero solo hasta el siguiente arranque. Las listas de SHIELD en `examples/` mantienen
`tvrecommendations` activado por esta razón.

## Fire TV (Fire OS): la limpieza funciona, el launcher no puede tomar Home

Por qué Google TV es distinto: en Google TV una app de terceros puede tomar el rol HOME, así que el launcher, el
predeterminado de `set-home-activity` y la desactivación del launcher original funcionan. Fire OS reserva Home para el
launcher propio de Amazon, y las mismas herramientas fallan ahí. Comprobado en un Amazon Fire TV, modelo AFTDEC012E (nombre en clave ginza),
Android 11 (SDK 30), compilación RS8185.3885N:

- `cmd package query-activities` para HOME: `com.amazon.tv.launcher/.ui.HomeActivity_vNext` con prioridad 950,
  `com.amazon.firehomestarter` con 1. Un launcher de terceros instalado con `android:priority="1000"` en su
  filtro HOME sigue en 0. Fire OS ignora la prioridad de una app que no es del sistema.
- `cmd package set-home-activity com.gathin.tvhome/.MainActivity` imprime `Success`, y HOME sigue resolviéndose
  al launcher de Amazon.
- `pm disable-user --user 0` sobre `com.amazon.tv.launcher`, sobre su componente `HomeActivity_vNext`, y sobre los
  otros paquetes de inicio de Fire OS se rechaza: `Cannot disable a protected package`.
- Interceptar la tecla Home con un AccessibilityService no funcionó: `onKeyEvent` no recibió nada para
  teclas inyectadas (`input keyevent KEYCODE_HOME`) ni durante una ventana de 40 segundos de pulsaciones del control.

Limpieza: `tools/disable.sh examples/amazon-fire-tv-aftdec012e/debloat.txt` desactiva paquetes de telemetría, ACR, compras y
tutoriales. Deshazlo con `tools/restore.sh examples/amazon-fire-tv-aftdec012e/debloat.txt com.amazon.tv.launcher`.

## Reasignar los botones de apps del control sin un servicio auxiliar de teclas

Un proceso propio puede tomar los botones para los que existen los servicios auxiliares sin vincular un servicio de accesibilidad,
y se conserva la repetición automática de teclas que un servicio auxiliar cuesta: un servicio que filtra teclas hace pasar cada tecla por una
ruta de filtrado que descarta las repeticiones, mientras que leer el dispositivo de entrada del control deja en paz la entrada de Android.
Tiene que correr como el usuario `shell`, porque una app normal no puede abrir `/dev/input/event*`, así que esto no es
algo en lo que el launcher pueda convertirse: es un script y un supervisor en la TV. En un Google TV Streamer
(`kirkwood`, Google TV 14, `UTTK.260317.003`) esa fue la única forma de tener ambas cosas: `HomeKeyService` solo,
`InputKeyService` solo y ambos juntos detenían cada uno la rampa después de unos seis pasos, y volvía
en el momento en que el servicio se desvinculaba ([#796](https://github.com/Gathin23/cleanyourtv/issues/796)).

El control del Streamer aparece como `Google TV Remote Keyboard`, y estos son los botones que envía:

| Botón | Uso HID | Código de tecla de Android |
| --- | --- | --- |
| YouTube | `0x000c0077` | `BUTTON_3` (190) |
| Estrella | `0x000c0186` | `MACRO_1` (313) |
| Netflix | `0x000c0078` | `BUTTON_4` |

Busca el nodo por nombre, no por número: `tools/tv.py 'getevent -pl'` muestra cada dispositivo de entrada con su nombre
y los códigos de tecla que declara, y el `/dev/input/event<N>` en el que cae un control no es estable entre arranques,
así que un observador fijado a `event5` deja de funcionar después del siguiente reinicio y vuelve a parecer un botón muerto.

Un lector no puede consumir la pulsación. `getevent` observa los eventos y Android los sigue entregando a
lo que sea que los responda hoy, así que la acción original de un botón reasignado también se ejecuta: asigna el botón de Netflix y
Netflix también se inicia, y luego queda en la pila de actividades. Un servicio auxiliar consume la tecla que asigna (por eso
el receptor del fabricante del punto "Qué código de tecla" de arriba nunca la ve), así que los botones que tienes que
suprimir, en lugar de duplicar, siguen necesitando un servicio auxiliar con su sacrificio de la repetición.

Lo que lo vuelve a ejecutar después de un reinicio es la parte que no sale gratis. El usuario `shell` lee
`/dev/input/eventX` en este equipo sin root y un script guardado en `/data/local/tmp/` se ejecuta, pero nada
ahí se inicia solo: sin root, Android no le da al usuario `shell` ni cron ni gancho de init, así que el observador
desaparece después de cada reinicio y hay que iniciarlo de nuevo desde una sesión de depuración que cierras después. Dos
cosas fallan en silencio cuando lo haces: el script debe desvincularse de la sesión de `adb shell` o muere con
ella, y un supervisor no debe iniciar una segunda copia. No resuelvas el reinicio dejando ADB por TCP activado para que
algo local pueda reiniciarlo: el puerto 5555 accesible desde la LAN es un shell en la TV para cualquier cosa en la
red, y por eso el paso de cierre del [README](../README.md#preguntas-frecuentes) lo desactiva.

## Hay un servicio auxiliar de teclas vinculado y un botón del control mantenido presionado dejó de repetir

Mantén presionado subir o bajar volumen y el volumen avanza un paso por pulsación en lugar de subir o bajar de forma continua. Puede que el control
esté bien, y la limpieza también: la rampa vuelve en el momento en que no hay ningún servicio de accesibilidad que filtre teclas vinculado,
y `getevent -lt` muestra si la repetición sigue llegando desde el control mientras se mantiene el botón. En una
TCL 55P71B Pro (`G09`, Google TV 12, `STT2.230203.001.AS23`) fue todo o nada: `HomeKeyService`
solo, `InputKeyService` solo y ambos juntos la rompían, y `settings put secure
enabled_accessibility_services ''` más `accessibility_enabled 0` la restauraban. Los volcados muestran
`capabilities=8` (`CAPABILITY_CAN_FILTER_KEY_EVENTS`), así que la plataforma hace pasar cada tecla por una ruta de filtrado
que descarta las repeticiones antes de que una app las vea; los propios servicios auxiliares del launcher devuelven `false` para las teclas
que no asignan, así que no están consumiendo la tecla de volumen. Se reportó lo mismo en una Xiaomi MiTV-MOSR4
(`irobot`, Android 11, `RTM5.220609.003.1265`) con los propios servicios auxiliares del launcher, ambos e `InputKeyService`
solo (#944), donde no se probó la lista vacía porque también desconecta los botones para los que se
instalaron los servicios auxiliares. Un onn 4K Streaming Box (`YOC`, Google TV 14, `URO4.260304.011.B1.15051976`) hace lo mismo con
`HomeKeyService` solo; ahí `key_filter` en false (config.xml o un tema) recuperó la repetición con el servicio auxiliar
aún vinculado, así que un servicio auxiliar que se conserva por algo distinto de las teclas no tiene por qué costarla. Revisa primero el estado, no
lo reescribas a ciegas:

```sh
tools/tv.py 'settings get secure enabled_accessibility_services'
tools/tv.py 'settings get secure accessibility_enabled'
tools/tv.py 'dumpsys accessibility'
```

Esto es un intercambio, no un defecto que corregir: los botones para los que existen los servicios auxiliares (un botón de engrane que envía
`KEYCODE_NOTIFICATION` 83, botones de apps que envían códigos de tecla del fabricante como 4062) los respondía el inicio
original, así que en un equipo cuya lista desactivó launcherx solo un servicio auxiliar puede responderlos. O conservas la repetición e
instalas sin `INPUT_KEY_SERVICE=1`/`HOME_KEY_SERVICE=1`, o conservas los botones y aceptas un paso por
pulsación, o dejas launcherx activado y no vinculas nada, o mantienes los servicios vinculados y haces que dejen de filtrar:
`"key_filter": false` en el `config.json` de un tema (el mismo booleano en `config.xml` para una recompilación) hace que
abandonen `FLAG_REQUEST_FILTER_KEY_EVENTS` en tiempo de ejecución, así que la rampa vuelve y los botones que
manejaban dejan de funcionar: el mismo intercambio sin escribir en `settings`. Vuelve a escribir exactamente la cadena que imprimió la primera
lectura; la lista vacía también desvincula TalkBack. Aislamiento, códigos de tecla y límites:
[la nota de la G09](devices/tcl-55p71b-g09-key-repeat.md).

## Una app se niega a reproducir mientras el resto de la TV está en línea

Un DNS privado que bloquea anuncios es un agregado común, y que el resolvedor responda no prueba que la reproducción
no se vea afectada. Un reproductor también llama a dominios de medición y analítica, y un bloqueo ahí vuelve como
el error propio de la app mientras la TV sigue en línea. En una Master-G MGA3200 (`ATV R1`, `R1`, SCBC, Realtek,
Android TV 9, `PTT1.201001.001`) con `dns.adguard-dns.com` en modo de nombre de host, Max (`com.wbd.stream`)
registró `ERR_CONNECTION_REFUSED` para sus endpoints de Braze y Conviva y se quedó detenida, mientras todas las demás apps
reproducían y la propia comprobación de conectividad de Android pasaba (#1060). Bloquear `pixel.spotify.com` deja a Spotify
fuera del Freebox Player POP (`examples/freebox-player-pop`) de la misma manera. Así que cuando una app falla y el
resto reproduce, vuelve a poner el modo anterior antes de depurar la app, y luego prueba el mismo título una vez más: en la
MGA3200 eso eliminó los errores:

```sh
tools/tv.py 'settings put global private_dns_mode opportunistic'
```

El otro modo de falla se ve distinto: cuando la propia TV dice "Sin internet", el resolvedor está caído
o es inalcanzable, y el mismo comando lo restaura. Qué hace el resolvedor opcional, y lo que cuesta,
está en la pregunta "¿También puede bloquear la publicidad dentro de las aplicaciones?" del README.
