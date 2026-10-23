# Ayudar a alguien que está en otra casa

Todo en este repositorio da por hecho que tu computadora y el televisor están en el mismo Wi-Fi. Cuando el
televisor está en casa de tus padres o de un amigo, crea un enlace privado de
[Tailscale](https://tailscale.com) entre tu computadora y su casa. Así el televisor se comporta exactamente
como si estuviera en tu red: el prompt, `tools/tv.py`, las capturas de pantalla y la instalación del
launcher funcionan sin cambios, con una dirección `100.x.y.z` en lugar de la local. El plan personal de
Tailscale es gratuito.

**Nunca abras el puerto 5555 de su router hacia internet.** ADB da control total del televisor, y hay bots
que escanean internet activamente en busca de puertos ADB abiertos.

## Lo que necesitas

- Tailscale en tu computadora, con la sesión iniciada. Las aplicaciones de Mac y Windows toman las rutas de
  subred por sí solas; en Linux ejecuta también `sudo tailscale set --accept-routes`. Tu computadora no debe
  ser un dispositivo [etiquetado](https://tailscale.com/kb/1068/tags) (tagged), ya que las máquinas
  etiquetadas no pueden llegar a las compartidas.
- Alguien junto al televisor con el control remoto, al teléfono contigo durante unos veinte minutos.
- Una de las dos configuraciones de abajo.

## Opción A: Tailscale en el televisor

La configuración más sencilla cuando el televisor puede ejecutarlo:

- **Android TV y Google TV:** Tailscale desde la Play Store.
- **Fire TV:** Tailscale desde la Amazon Appstore, en la mayoría de los dispositivos de 2018 en adelante.
  No en el Fire TV Stick 4K Select, que usa Vega OS (y a ese de todos modos no se le puede quitar el
  bloatware por ADB).

Al abrir la aplicación aparece un código QR. Luego, una de dos:

1. **Lo mantienen en su propia tailnet y comparten el televisor contigo** (recomendado para la familia).
   Escanean el código con su teléfono e inician sesión con su propia cuenta gratuita. Después, en la consola
   de administración (Machines → el televisor → **Share**), te envían una invitación y tú la aceptas. Ves ese
   único televisor y nada más de su casa, y pueden revocar el acceso cuando quieran.
2. **Se une a tu tailnet.** Escanean el código y tú inicias sesión en su teléfono con tu cuenta. Es más
   rápido, pero el televisor pasa a ser uno de tus dispositivos hasta que lo quites.

La dirección `100.x.y.z` del televisor aparece en la aplicación de Tailscale del televisor y en tu lista de
máquinas.

## Opción B: un dispositivo auxiliar como enrutador de subred

Usa esta opción cuando Tailscale no se puede instalar en el televisor, o prefieren no tenerlo ahí. Otro
dispositivo de su casa reenvía tu conexión a la dirección local normal del televisor:

- una Mac, una PC con Windows o una máquina Linux que se quede encendida durante la sesión, o una Raspberry
  Pi para una configuración permanente;
- un Apple TV, mediante la opción Subnet Router de su aplicación de Tailscale;
- un NAS Synology, con Tailscale desde el Centro de paquetes. Su página de Tailscale (DSM, o el puerto 5252)
  tiene una sección Subnet router, pero es de solo lectura cuando la abres desde un dispositivo etiquetado.
  Sin SSH, una tarea única del Programador de tareas (Panel de control → Programador de tareas → Crear →
  Tarea activada → Script definido por el usuario, usuario root, luego Ejecutar y eliminarla) ejecuta
  `/var/packages/Tailscale/target/bin/tailscale set --advertise-routes=192.168.1.0/24`; el ajuste se
  conserva;
- no un teléfono: las aplicaciones de Android e iOS no pueden enrutar su red doméstica.

El dispositivo auxiliar tiene que estar en **tu** tailnet, porque las máquinas compartidas no llevan sus
rutas de subred a otras tailnets. (Si ellos ya tienen una tailnet, en una oficina por ejemplo, también
funciona al revés: te agregan como usuario, tú agregas su tailnet como segunda cuenta en tu aplicación de
Tailscale y cambias a ella durante la sesión.) Instala Tailscale en él y envíate el enlace de inicio de
sesión que muestra; ábrelo con la sesión iniciada en tu cuenta. Luego anuncia su red doméstica (los
primeros tres números de la dirección del televisor, que aparecen en los ajustes de red del televisor):

```bash
# Mac (aplicación independiente sin la CLI: /Applications/Tailscale.app/Contents/MacOS/Tailscale set ...)
sudo tailscale set --advertise-routes=192.168.1.0/24
# Windows, PowerShell como administrador, después de activar el reenvío de IP
tailscale set --advertise-routes=192.168.1.0/24
# Linux, después de activar el reenvío de IP (https://tailscale.com/kb/1019/subnets)
sudo tailscale set --advertise-routes=192.168.1.0/24
```

Aprueba la ruta en tu consola de administración: Machines → el dispositivo auxiliar → Subnets → Edit.
Entonces llegas al televisor en su dirección local, por ejemplo `TV_HOST=192.168.1.40`.

**Las dos redes no deben superponerse.** Si su casa usa el mismo rango que la tuya (ambas `192.168.1.x`,
por ejemplo), tu computadora no puede distinguir su televisor de un dispositivo de tu casa. Usa la opción
A, o conéctate desde otra red.

## Conectarse

Pídeles que activen la depuración exactamente como en el [Inicio rápido](../README.md#quick-start), y
luego:

```bash
TV_HOST=100.x.y.z tools/tv.py --probe
```

Aceptan "¿Permitir la depuración por USB?" en el televisor mientras estás al teléfono. El resto del prompt
se ejecuta como siempre; dile a tu asistente que el televisor es remoto y dale esta dirección, para que no
lo busque escaneando tu propia red.

**Televisores que solo ofrecen depuración inalámbrica** (algunos Google TV): el descubrimiento por mDNS no
atraviesa el túnel, así que te leen tres datos de Opciones de desarrollador > Depuración inalámbrica: la
dirección IP y el puerto de esa pantalla y, en Vincular dispositivo con código de vinculación, el puerto de
vinculación y el código. Con el `adb` estándar:

```bash
adb pair 100.x.y.z:<pairing port> <code>
adb connect 100.x.y.z:<connect port>
adb -s 100.x.y.z:<connect port> tcpip 5555
TV_HOST=100.x.y.z tools/tv.py --probe
```

(`<pairing port>` es el puerto de vinculación, `<code>` el código y `<connect port>` el puerto de conexión.)

Con la opción B, usa la dirección local del televisor en lugar de `100.x.y.z`.

## Lo que importa más cuando no estás ahí

- **El Wi-Fi es tu única vía de entrada.** Cualquier cosa que deje al televisor sin Wi-Fi te deja fuera a
  ti también, y solo alguien junto al televisor puede arreglarlo. En Google TV, revisa a quién pertenece la
  red guardada antes de desactivar el asistente de configuración (`dumpsys wifi | grep -o 'cname=[^ ]*'`,
  ver [TROUBLESHOOTING.md](TROUBLESHOOTING.md)). Si dice setupwraith, pídeles primero que olviden la red y
  vuelvan a conectarse a ella en Ajustes.
- **Pregunta, no adivines.** Las preguntas de lista de casillas del prompt (qué aplicaciones, el dock, la
  transmisión, la voz, las actualizaciones) les toca responderlas a ellos, igual que qué está conectado a
  los puertos USB.
- **Déjales el script de restauración**, o al menos guárdalo donde puedas ejecutarlo la próxima vez que te
  conectes.

## Después

1. Desactivan la depuración por USB y la depuración inalámbrica en Opciones de desarrollador. El launcher
   sigue funcionando.
2. Quita el acceso: ellos revocan el uso compartido, o tú quitas el televisor o el dispositivo auxiliar de
   tu tailnet (o desactivas sus rutas) en la consola de administración. Desinstala Tailscale del televisor a
   menos que lo usen.

¿Hiciste esto en un televisor donde algo funcionó distinto? Agrega una línea aquí en un pull request.
