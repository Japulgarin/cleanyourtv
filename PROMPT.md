# El prompt

> La versión original en inglés está en [PROMPT.en.md](PROMPT.en.md).

Pega esto en Claude Code (u otro asistente de programación con acceso a la terminal) en una computadora
conectada al mismo Wi-Fi que el televisor. Funciona en televisores Android TV / Google TV (Xiaomi, TCL,
Hisense, Sony, OnePlus, Realme, Nvidia Shield y la mayoría de los demás). No funciona en Samsung Tizen, LG
webOS ni Fire TV. Si clonaste este repositorio, menciónalo: el asistente puede reutilizar `tools/` y
`launcher/` en lugar de escribirlos desde cero, y solo necesita editar `launcher/.../values/config.xml`.

Antes de empezar, en el televisor: Ajustes → Preferencias del dispositivo → Información → presiona OK sobre
"Compilación" 7 veces, luego vuelve atrás → Opciones de desarrollador → activa la depuración por USB (y la
depuración por red/ADB si tu televisor la muestra). Deja el televisor encendido. Algunos aparatos cortan la
energía de su puerto USB mientras la depuración por USB está activada, así que un parlante o una memoria USB
conectados ahí dejan de funcionar hasta que vuelvas a desactivar la depuración. Un adaptador Ethernet USB en
ese puerto puede caerse de la misma forma, así que planea hacer toda la sesión de una sola vez.

---

Quiero quitar el software innecesario (bloatware) de mi Android TV y reemplazar su launcher por una pantalla
de inicio limpia al estilo Apple TV. El modelo de mi televisor es: <NOMBRE DEL MODELO AQUÍ>. Trabaja en el
dispositivo real, paso a paso, y verifica todo lo que hagas con capturas de pantalla tomadas del televisor.
Pregúntame antes de cualquier cosa que dependa de mis preferencias.
Háblame siempre en español y con palabras sencillas: no soy técnico.

Conexión
- Encuentra el televisor en mi red (nombre de host, tabla ARP, o pídeme la IP) y conéctate por ADB en el
  puerto 5555. Si el televisor está en otra casa, te daré su dirección de Tailscale (docs/REMOTE.md): usa
  esa, no escanees mi red local.
- Si el binario adb estándar falla con "No route to host" en macOS aunque el puerto esté abierto, es la
  privacidad de Red local de macOS bloqueando adb. No lo depures: usa como cliente ADB el paquete de Python
  `adb-shell` en un venv. Si su envío de archivos se cuelga con archivos grandes, transfiere los archivos
  como fragmentos en base64 a través de la terminal y verifica el md5.
- Si tus propios comandos no llegan al televisor en absoluto mientras que sí responde desde una terminal
  normal (un sandbox que bloquea la red local), pídeme que ejecute `tools/relay.py <tv ip>` en una terminal
  y lo deje corriendo, y luego usa `TV_HOST=127.0.0.1 TV_PORT=15555` (`tools/relay.md`).
- Si el puerto 5555 sigue cerrado, puede que el televisor solo ofrezca la depuración inalámbrica (los Google
  TV suelen hacerlo): busca `_adb-tls-connect._tcp` con `dns-sd -B` o `adb mdns services`, pídeme el código
  y el puerto que aparecen en Opciones de desarrollador > Depuración inalámbrica > Vincular dispositivo con
  código de vinculación, y luego `adb pair`, `adb connect` y `adb tcpip 5555`. Android desactiva la
  depuración inalámbrica cada vez que se cae el Wi-Fi.
- Avísame cuándo va a aparecer en el televisor el mensaje "¿Permitir la depuración por USB?" para que pueda
  aceptarlo.
- Si `adb install` se cuelga en Android 14, está esperando una confirmación en pantalla; en su lugar, envía
  el APK y ejecuta `pm install -r` desde la terminal.

Primero, la copia de seguridad
- Guarda la lista completa de paquetes, la lista de paquetes desactivados, la salida de getprop y todos los
  ajustes en una carpeta de respaldo antes de cambiar nada, y escribe un script de restauración que vuelva a
  activar todo lo que desactives.
- Pregúntame qué está conectado a los puertos USB del televisor, y pregúntame por separado si la red del
  televisor llega a través de un adaptador Ethernet USB: "no hay nada conectado" puede ser cierto aunque la
  red misma esté en ese puerto. Algunos dispositivos cortan su energía mientras la depuración por USB está
  activada, así que adviérteme, y recuérdame desactivar la depuración cuando termines. En un televisor que
  se conecta a la red por Ethernet USB, revisa antes de cambiar nada: `dumpsys usb | grep host_connected`
  (`host_connected=false` significa que el adaptador ya se perdió) y `dumpsys connectivity | grep -o
  'Transports: [A-Z]*'` (`WIFI` en un televisor que yo digo que está por cable significa que el aparato se
  pasó a Wi-Fi y que ADB está funcionando por Wi-Fi). Termina todo el trabajo de una sola vez, no en dos: en
  ese caso el puerto solo vuelve con la depuración por USB desactivada, y eso también cierra el puerto 5555.
  Si el televisor tiene depuración inalámbrica, es preferible usarla.
- Cuando termines, cierra el ADB por red en lugar de dejarlo abierto: desactiva en el televisor la
  depuración por USB y la depuración por red/ADB, revoca las autorizaciones de depuración por USB, reinicia,
  y comprueba con `tools/adb-closed.py <tv ip>` que el puerto rechaza la conexión. Si la red del televisor
  llegaba por un adaptador Ethernet USB, desconecta y vuelve a conectar el adaptador una vez desactivada la
  depuración - el puerto vuelve con él - y pídeme que confirme que el televisor está otra vez en Ethernet, no
  en Wi-Fi. No confíes en `nc` en macOS: la privacidad de Red local también puede bloquearlo, y su "No route
  to host" no prueba nada; solo "Connection refused" lo prueba. El puerto 5555 va en texto plano, y en un
  firmware con `ro.adb.secure=0` cualquier dispositivo de la red local puede obtener una terminal.

Quitar el bloatware
- Lista los paquetes instalados y clasifícalos en: telemetría/analítica del fabricante, servicios de
  contenido y publicidad del fabricante (PatchWall, filas de recomendaciones, proveedores de contenido),
  servicios en segundo plano que probablemente no necesito (duplicados de compartir/transmitir,
  limpiadores), aplicaciones preinstaladas y aplicaciones de streaming.
- Desactiva las primeras categorías con `pm disable-user --user 0`; nunca desinstales paquetes del sistema.
- Nunca desactives lo que el televisor necesita para funcionar: la aplicación de TV y los servicios de
  entrada que reproducen HDMI y el sintonizador, el menú de entradas/fuentes, los servicios del control
  remoto y de vinculación Bluetooth, el teclado en pantalla, Google Play Store y Play Services. Los nombres
  de paquete de los fabricantes a menudo no dicen qué hace un paquete: revisa primero sus actividades y
  servicios con `dumpsys package`, y pregúntame si sigue sin estar claro.
- Nunca desactives los paquetes centrales de Android, o puede que el televisor no vuelva a arrancar: el
  controlador de permisos, el instalador de paquetes, ext services y ext shared, los metadatos de módulos
  (cada uno como `com.android.*` o `com.google.android.*`), `com.google.android.overlay.modules*`,
  `com.android.providers.*` (salvo calendario, contactos, diccionario del usuario y números bloqueados),
  `com.android.systemui`, `com.android.shell`, `com.android.phone`, `com.android.settings`,
  `com.android.tv.settings` y `android`. Un Mi TV Stick original nunca volvió a arrancar después de que una
  lista quitara los seis primeros
  ([#884](https://github.com/Gathin23/cleanyourtv/issues/884)); `tools/disable.sh` rechaza una lista así.
- Antes de tocar las aplicaciones de streaming, el asistente de voz, Chromecast, Miracast o el servicio de
  actualizaciones, pregúntame cuáles uso con una pregunta de lista de casillas y desactiva solo lo que no
  marque.
- Ejecuta los comandos `pm` de uno en uno por llamada a la terminal; los comandos encadenados pueden
  detenerse en silencio después del primero.
- Si `pm disable-user` es rechazado para todos los paquetes, detente y avísame: algunos firmwares (Fire OS 5
  en un Fire TV Box, por ejemplo) rechazan `pm disable-user` con una `SecurityException`, `pm uninstall
  --user 0` con `DELETE_FAILED_INTERNAL_ERROR`, y `pm hide` informa éxito sin cambiar nada. Comprueba con
  `pm list packages -d` en lugar del código de salida, y no desperdicies la sesión reintentando - no hay
  nada que quitar en un televisor así, así que recurrimos a sus propias opciones de privacidad y al bloqueo
  por DNS (`docs/TROUBLESHOOTING.md`).
- No abras un paquete cuyo nombre diga factory, production, AT o fac menu (`com.cvte.tv.hkcfac`,
  `com.cvte.tv.fac.menu`, `com.at.factory.*`, `mediatek.factorymenu.ui` y similares) para ver qué hace, ni
  siquiera en modo de solo lectura: en placas Haier/CVTE, abrir uno activa una marca de modo de fábrica que
  inutiliza la tecla Input y el CEC, y hace que el siguiente arranque desactive Play services, Netflix y
  Chromecast - que la terminal luego no puede volver a activar. `dumpsys package <name>` te dice qué es un
  paquete sin iniciarlo, y `docs/TROUBLESHOOTING.md` explica cómo salir si ya se abrió uno.
- Desactiva en tandas pequeñas y toma una captura de pantalla entre ellas: una tanda puede llevarse consigo
  algo imprescindible y no podrás saber qué fue.
- Después de la última tanda, reinicia una vez y compara `pm list packages -d` con lo que desactivaste:
  algunos firmwares vuelven a activar paquetes en cada arranque a partir de su propia lista (TCL Android 9
  lo hace con su centro de usuario). Anótalos en el encabezado de la lista en lugar de volver a
  desactivarlos después de cada arranque.
- Ofréceme como extra opcional un DNS que bloquee anuncios: en Android 9 y versiones posteriores, DNS
  privado configurado con un resolvedor que bloquee anuncios (`settings put global private_dns_specifier
  dns.adguard-dns.com`, luego `settings put global private_dns_mode hostname`). Dime que no bloquea los
  anuncios de YouTube, comprueba que una aplicación siga reproduciendo después, y anota cómo deshacerlo
  (`private_dns_mode opportunistic`) en el README.

Launcher
- Comprueba que el televisor acepte APKs antes de compilar nada. Algunos televisores del mercado chino
  responden a toda instalación externa con `INSTALL_FAILED_VERIFICATION_FAILURE` — `adb install`,
  `pm install`, un instalador abierto a mano e incluso los propios APKs del fabricante fallan — y otros
  rechazan cualquier paquete que declare `android.intent.category.HOME` a menos que lleve la firma del
  fabricante. Si te encuentras con cualquiera de los dos casos, haz la parte de quitar el bloatware, di
  claramente que la parte del launcher es imposible aquí y deja de reintentar instalaciones. El encabezado
  correspondiente en `examples/` dice en qué caso está tu televisor.
- Comprueba también el nivel de SDK del televisor antes de prometer el launcher: `tools/tv.py 'getprop
  ro.build.version.sdk'` contra `grep minSdk launcher/app/build.gradle` (26 = Android 8.0). Un televisor por
  debajo responde `INSTALL_FAILED_OLDER_SDK`; bajar `minSdk` es un cambio en el código fuente que luego
  tendrías que mantener tú, y un APK recompilado en otro lugar no es algo que este repositorio pueda
  verificar. En esos televisores ofrece la parte de quitar el bloatware y di que el launcher no se puede
  instalar. Sin un launcher al que pasarle el control, se queda el original: `cmd package` no existe antes de
  Android 7, así que ahí `tools/disable.sh` le pregunta a `dumpsys activity` cuál es la pantalla de inicio y
  avisa cuando ninguno de los dos responde - ese aviso significa que no se comprobó nada, y un televisor sin
  modo de recuperación no tiene vuelta atrás (#795).
- No instales un launcher de terceros que cobre por lo básico, como los fondos de pantalla. En su lugar,
  compila un launcher nativo pequeño para Android TV (Java, AndroidX RecyclerView, minSdk acorde al
  televisor; una compilación de depuración está bien), instálalo por ADB, configúralo como pantalla de inicio
  predeterminada y desactiva el launcher original. Si varias aplicaciones reclaman el intent HOME, lístalas
  con `cmd package query-activities -a android.intent.action.MAIN -c android.intent.category.HOME` y
  establece la predeterminada con `cmd package set-home-activity`. Esos dos comandos pueden nombrar ambos a
  tu launcher mientras que el botón de inicio sigue abriendo otra cosa: en algunas versiones de Google TV
  `set-home-activity` imprime `Success` y no cambia nada, y el `.RecoveryActivity` de setupwraith se queda
  con la tecla. Confírmalo con `dumpsys activity activities | grep mFocusedApp` antes de decirme que el
  cambio funcionó.
- Antes de desactivar el launcher original, revisa qué otras aplicaciones reclaman HOME: en Google TV el
  asistente de configuración (`com.google.android.tungsten.setupwraith`) toma el control incluso después de
  desactivar el launcher original, y el encabezado correspondiente en `examples/` dice qué hacer. Antes de
  desactivar setupwraith, ejecuta `dumpsys wifi | grep -o 'cname=[^ ]*'`: una red Wi-Fi guardada durante la
  configuración inicial le pertenece, y Android borra esa red en el momento en que se desactiva, lo que deja
  al televisor sin Wi-Fi y sin ADB. Si es así, pídeme primero que olvide la red y vuelva a conectarme a ella
  en Ajustes.
- En una placa CVTE (cualquier paquete `com.cvte.*`), deja activado su launcher original
  (`com.cvte.tv.launcher.*`) a menos que la carpeta de `examples/` de esa placa exacta lo desactive: haz que
  tu launcher sea la pantalla de inicio con `set-home-activity`, reinicia una vez y confirma que la pantalla
  de inicio y ADB vuelven antes de cualquier otra cosa. No actives un ayudante de teclas del control remoto
  en la misma pasada. Un JVC LT-43N7115 (`TP.SK706S.PC822`, Android 11) se quedó colgado en su animación de
  arranque y sin ADB después de hacer ambas cosas antes de un solo reinicio (#741).
- En Google TV el launcher original también responde a los botones de aplicaciones del control remoto
  (Netflix, YouTube y similares), al botón Input y a los botones de Ajustes/panel, así que después de
  desactivarlo pídeme que presione cada uno, y reasigna los que no hagan nada con los servicios de teclas del
  launcher: `input_key_keycodes` y `app_keys` con INPUT_KEY_SERVICE=1, `settings_key_keycodes` con
  HOME_KEY_SERVICE=1 (`config.xml` o el tema). Activar cualquiera de los dos ayudantes puede costar más que
  los botones que asigna: en una versión TCL G09 (Google TV 12) pídeme que mantenga presionado subir volumen
  antes y después, porque un servicio de filtrado de teclas activo ahí descarta las repeticiones de tecla -
  un volumen que sube de forma continua pasa a subir un paso por pulsación, con un ayudante o con ambos, todo
  o nada - así que dime a qué estoy renunciando en lugar de activarlo en silencio
  (`docs/devices/tcl-55p71b-g09-key-repeat.md` tiene la búsqueda por bisección y las tres salidas). En otros
  televisores esto no se midió; si mantener presionado un botón deja de repetir una vez que un ayudante está
  activado, es la misma concesión y no un control remoto roto.
  Un botón que el televisor registra como `KEY_UNKNOWN` o `KEY_PROGRAM` no se puede identificar por código de
  tecla, ya que todos los botones sin asignar lo comparten: lee el scancode con `getevent -lt` y usa
  `settings_key_scancodes`, que solo admite `config.xml` (un tema puede definir códigos de tecla, no
  scancodes).
- En Android 11 y versiones posteriores el launcher debe declarar `<queries>` para
  `android.intent.category.LEANBACK_LAUNCHER`, o la visibilidad de paquetes oculta en silencio todas las
  aplicaciones y la cuadrícula aparece vacía; apunta a un SDK reciente, algunos televisores con Google TV 14
  rechazan versiones de destino antiguas al instalar.
- Pregúntame cuántos espacios quiero en el dock (4, 5, 6 o 7), qué aplicaciones y en qué orden; deja cuatro
  si no tengo preferencia. El launcher de referencia ya admite esto: usa `columns` y `dock_apps` en
  `launcher/app/src/main/res/values/config.xml` o en el `config.json` de un tema, sin agregar un nuevo
  diseño.
- Diseño, estilo Apple TV 4K: fondo negro puro; una fila de dock en la parte inferior de la pantalla, dentro
  de una franja redondeada un poco más clara, con las aplicaciones que yo elija; el resto de las aplicaciones
  en una cuadrícula con el mismo número de columnas debajo, que se desplaza hacia arriba cuando presiono
  Abajo; un único resaltado translúcido de "vidrio" que salta con efecto de resorte de un mosaico a otro en
  lugar de bordes en cada mosaico; el mosaico enfocado se agranda un poco y muestra su nombre debajo; encima
  del dock, el nombre de la aplicación enfocada del dock en letra grande y fina con un resplandor ambiental
  de un color tomado de su banner; botones tipo píldora esmerilados arriba a la derecha para Entradas, Wi-Fi
  (mostrando el nombre de la red) y Ajustes; un saludo, un reloj grande y fino y la fecha arriba a la
  izquierda en una tipografía descargada de licencia abierta, como Outfit. Entradas abre un menú desplegable
  compacto de vidrio debajo de la píldora que lista los puertos HDMI, AV y TV en vivo, y cambia de entrada a
  través del framework de entradas de TV.
- Haz que la navegación con el D-pad sea determinista: Arriba/Abajo mueven exactamente una fila, Arriba
  desde el dock va a la barra superior, y los extremos de la barra superior no caen a los mosaicos. Recuerda
  el último mosaico enfocado.
- Mantenlo liviano: el televisor tiene alrededor de 1 GB de RAM. Nada de desenfoque, nada de video, nada de
  consultas periódicas a la red.

Verificación
- Después de cada cambio, simula pulsaciones del control remoto por ADB, toma una captura de pantalla del
  televisor y mírala: `tools/tv.py --screenshot shots/01-after.png DPAD_RIGHT` presiona la tecla, luego hace
  la captura en el televisor y descarga el PNG (omite las teclas para capturar lo que ya está en pantalla).
  Corrige lo que veas antes de seguir.
- TV en vivo, HDMI y algunas aplicaciones de streaming (Netflix) dan capturas vacías (0 bytes); eso es cosa
  del televisor, no un fallo al quitar el bloatware, y `--screenshot` termina con código 1 y ese mensaje. En
  su lugar, revisa `dumpsys activity activities | grep topResumedActivity` (ver `docs/TROUBLESHOOTING.md`).
- Si la pantalla se ve agrandada y recortada después de una instalación o un reinicio, revisa los ajustes
  forzados de pantalla antes de editar la cuadrícula del launcher: `wm size` y `wm density` muestran un valor
  físico junto a un valor forzado, y un valor forzado que quedó de un experimento antiguo de resolución, o una
  densidad que vuelve mal en algunos firmwares Sony con MediaTek, no es un error del launcher. Un
  `settings get secure display_density_forced` vacío es un valor predeterminado normal, no un daño - lee los
  tres valores primero y restáuralos si deshaces el cambio (`docs/TROUBLESHOOTING.md`).
- Si un botón del control remoto depende de un ayudante de accesibilidad, comprueba que el servicio esté
  activado y vinculado para el usuario actual, y luego pídeme que presione el botón real; una tecla simulada
  no es prueba (ver `docs/TROUBLESHOOTING.md`).
- Al terminar, dame un script de restauración, un script de compilación e instalación, y un README que
  explique cómo volver a activar cualquier aplicación y cómo cambiar el orden del dock o el fondo de
  pantalla.

---

Prepárate para responder tres o cuatro preguntas de lista de casillas (qué aplicaciones usas, el tamaño del
dock y el orden de las aplicaciones, si quieres conservar el asistente de voz, Chromecast y las
actualizaciones del firmware). Todo es reversible.
