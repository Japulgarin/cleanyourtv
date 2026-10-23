<p align="center">
  <a href="https://cleanyour.tv"><img src="https://raw.githubusercontent.com/Gathin23/cleanyourtv/main/docs/banner.png" alt="CleanYourTV. Tu televisor, sin la publicidad. Quita las aplicaciones de relleno de cualquier Android TV o Google TV por Wi-Fi y cambia la pantalla de inicio llena de anuncios por un inicio limpio que se parece al de un Apple TV. Sin root, sin cable, sin desinstalar nada, y se deshace con una sola línea." width="800"></a>
</p>

<p align="center">
  <a href="https://github.com/Gathin23/cleanyourtv/stargazers"><img src="https://img.shields.io/github/stars/Gathin23/cleanyourtv?style=flat&cacheSeconds=1800&color=cfffcf&labelColor=15181e" alt="Estrellas"></a>
  <a href="https://github.com/Gathin23/cleanyourtv/pulls?q=is%3Amerged"><img src="https://img.shields.io/github/issues-search?query=repo%3AGathin23%2Fcleanyourtv%20is%3Apr%20is%3Amerged&style=flat&cacheSeconds=1800&label=merged%20PRs&color=cfffcf&labelColor=15181e" alt="PR aceptados"></a>
  <a href="https://github.com/Gathin23/cleanyourtv/network/members"><img src="https://img.shields.io/github/forks/Gathin23/cleanyourtv?style=flat&cacheSeconds=1800&color=cfffcf&labelColor=15181e" alt="Forks"></a>
  <a href="https://github.com/Gathin23/cleanyourtv/graphs/contributors"><img src="https://img.shields.io/github/contributors/Gathin23/cleanyourtv?style=flat&cacheSeconds=1800&color=cfffcf&labelColor=15181e" alt="Colaboradores"></a>
  <a href="README.en.md"><img src="https://img.shields.io/badge/README-English-cfffcf?style=flat&labelColor=15181e" alt="English"></a>
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/README-%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87-cfffcf?style=flat&labelColor=15181e" alt="简体中文"></a>
  <a href="README.vi.md"><img src="https://img.shields.io/badge/README-Ti%E1%BA%BFng%20Vi%E1%BB%87t-cfffcf?style=flat&labelColor=15181e" alt="Tiếng Việt"></a>
  <a href="README.ja.md"><img src="https://img.shields.io/badge/README-%E6%97%A5%E6%9C%AC%E8%AA%9E-cfffcf?style=flat&labelColor=15181e" alt="日本語"></a>
  <a href="https://buymeacoffee.com/gathint"><img src="https://img.shields.io/badge/support-%E2%9D%A4-ff5e8a?style=flat&labelColor=15181e" alt="Apoya el proyecto, invítame un café"></a>
  <a href="https://www.producthunt.com/products/cleanyourtv"><img src="https://img.shields.io/badge/Product%20Hunt-upvote%20%E2%96%B2-da552f?style=flat&logo=producthunt&logoColor=white&labelColor=15181e" alt="CleanYourTV en Product Hunt"></a>
</p>

<p align="center">
  <a href="https://trendshift.io/repositories/310225"><img src="docs/trending-badge.png" alt="Repositorio n.º 1 en tendencias de la semana, según trendshift.io" width="360"></a>
</p>

<p align="center">
  <a href="docs/PRESS.md"><img src="docs/card.jpg" alt="246 modelos de TV · 71 marcas · 25 idiomas · inicio de 474 KB. Aparecimos en TechCrunch, TechRadar, Tom's Guide, Mashable, Android Authority, XDA, FlatpanelsHD, It's FOSS, Phandroid, GIGAZINE, Xataka, WinFuture, Frandroid, Macitynet, Techaeris, TechPP y 171 más: 187 artículos de 31 países. Antes: la pantalla de inicio original de Google TV con un anuncio patrocinado. Después: el inicio de Clean Your TV." width="800"></a>
</p>

**La publicación que se hizo viral:** [x.com/gathint/status/2111379569030939102](https://x.com/gathint/status/2111379569030939102)

El 17 de octubre de 2026 publiqué un antes y después del televisor de mis padres, limpiado por Claude Code a través del Wi-Fi.
Llegó a 7,4 millones de vistas, la gente empezó a hacer lo mismo con sus propios televisores, y sus respuestas se convirtieron en
las listas que hay aquí: más de 170 modelos de TV aportados por más de 200 personas en cuatro días. El repositorio se llamaba tv-vibehack
hasta el día 19; los enlaces viejos siguen funcionando.

**Temas, opciones y complementos:** [cleanyour.tv/addons](https://cleanyour.tv/addons)

**Enlaces oficiales:** el sitio web es [cleanyour.tv](https://cleanyour.tv) y el código, el inicio y las
herramientas están solamente en este repositorio. Otros dominios que usan el nombre, como cleanyourtv.com, no son de
este proyecto ([#1004](https://github.com/Gathin23/cleanyourtv/issues/1004)).

## Cómo funciona

Los televisores Android tienen la misma "puerta de depuración" que los teléfonos Android. Se activa la depuración por USB en las
opciones de desarrollador del televisor, se le da permiso a tu computadora una sola vez, y lo demás son las herramientas normales de Android:

| Paso | Qué pasa |
|---|---|
| **Copia&nbsp;de&nbsp;seguridad** | Se guarda la lista de aplicaciones instaladas y los ajustes. |
| **Desactivar** | Se apagan el rastreo del fabricante, los servicios de publicidad, las filas de contenido y las aplicaciones de relleno que venían instaladas, con `pm disable-user`. No se desinstala nada, así que un programa de restauración puede deshacer cada paso. |
| **Instalar** | Se instala un inicio pequeño y liviano, y se deja como pantalla de inicio principal. |

**Sin root, sin cable, sin desinstalar nada, y con una sola línea se vuelve todo atrás si cambias de opinión.**

Las aplicaciones de relleno cambian según la marca, así que las instrucciones le piden a tu asistente de programación que las encuentre en tu televisor y que te pregunte
antes de tocar cualquier cosa que puedas usar.

## Primeros pasos

| Si tienes | Haz esto |
|---|---|
| **Una computadora** | Usa las instrucciones con un asistente de programación: los tres pasos de abajo. |
| **Solo un teléfono Android** | Usa la [aplicación Clean Your TV](https://cleanyour.tv/app), hecha por la comunidad, de [@udhaykumarbala](https://github.com/udhaykumarbala): conectar, analizar, limpiar, en unos cinco minutos. Sin computadora portátil y sin asistente de programación. |

Con una computadora, necesitas que esté conectada al mismo Wi-Fi que el televisor y un asistente de programación que pueda usar la terminal.

Cualquiera de estos sirve: Claude Code (en [0G Private Computer](https://pc.0g.ai) o con un [plan de Anthropic](https://claude.com/pricing)), [Codex](https://github.com/openai/codex) o [Gemini CLI](https://github.com/google-gemini/gemini-cli).

| Dónde | Qué hacer |
|---|---|
| **1. En el televisor** | Configuración → Preferencias del dispositivo → Información → presiona OK sobre **Compilación** siete veces → vuelve atrás → Opciones de desarrollador → activa **Depuración por USB**. Si ves un interruptor de depuración por red o depuración ADB, actívalo también. Deja el televisor encendido. |
| **2. En tu computadora** | Pega [`PROMPT.md`](PROMPT.md) en tu asistente y escribe el modelo de tu televisor. |
| **3. Sigue los pasos** | Acepta "¿Permitir la depuración por USB?" en el televisor y luego responde la lista de preguntas: qué aplicaciones usas, el tamaño de la barra inferior y el orden de las aplicaciones, y si quieres conservar el asistente de voz, Chromecast y las actualizaciones. |

El asistente hace la copia de seguridad, quita lo que sobra, prepara e instala el inicio, y revisa cada paso con
capturas de pantalla tomadas del televisor. Con este repositorio como guía tarda unos quince minutos.

## Qué obtienes

Una pantalla de inicio que se parece a la de un Apple TV y no estorba:

| Parte | Cómo se ve |
|---|---|
| **Un inicio negro total** | Una barra con tus cuatro aplicaciones favoritas en una franja redondeada, donde la pone Apple TV. |
| **Una franja superior** | Muestra con letras grandes el nombre de la aplicación seleccionada, con un brillo de fondo del color de su imagen. |
| **El resto de tus aplicaciones en una cuadrícula** | Aparece desde abajo cuando presionas Abajo. |
| **Un solo resaltado de vidrio** | Salta de un recuadro a otro. El recuadro seleccionado se levanta y muestra su nombre. |
| **Tres botones esmerilados** | Entradas (los puertos HDMI con los nombres que les pusiste en la configuración del televisor, AV, TV en vivo), Wi-Fi o cable de red con el nombre de la red, y Configuración. |
| **Un saludo, un reloj fino y la fecha** | En la letra [Outfit](https://fonts.google.com/specimen/Outfit), y un protector de pantalla de reloj que combina. Activa `show_stats` en la configuración o en un tema para ver una línea debajo del reloj: uso del procesador, memoria libre y espacio libre. Viene apagado a menos que lo actives, y solo se actualiza mientras el Inicio está en pantalla. |
| **Temas y tarjetas de módulo** | Los temas cambian los colores, el fondo de pantalla, la barra y las columnas sin tener que volver a armar el inicio, y las tarjetas de módulo permiten que otras aplicaciones agreguen un recuadro, solo si tú lo autorizas. |

Y un televisor que deja de trabajar en tu contra: sin filas patrocinadas, sin avisos de "Descubrir", sin datos
enviados a terceros, sin aplicaciones que nunca pediste.

| | |
|---|---|
| ![La franja superior muestra el nombre de la aplicación seleccionada sobre un brillo de su color](docs/focus-2-up-netflix.png) | ![La ventana de Entradas: los puertos HDMI con lo que está conectado, AV y TV en vivo](docs/inputs-menu.jpg) |
| *Franja superior y brillo de fondo* | *Entradas: HDMI con su estado de conexión, AV, TV en vivo* |
| ![La cuadrícula con el resaltado de vidrio sobre un recuadro y su nombre debajo](docs/focus-1-fancode.png) | ![El protector de pantalla de reloj: un reloj fino que se desplaza sobre el brillo](docs/clock-screensaver.png) |
| *La cuadrícula, un resaltado de vidrio, el nombre del recuadro* | *Protector de pantalla de reloj; se mueve para que nada quede marcado en la pantalla* |
| ![El tema aurora: un fondo de pantalla y botones con color, aplicado sin volver a armar el inicio](themes/aurora/screenshot.jpg) | ![Seis columnas y una barra de seis aplicaciones, desde el config.json de un tema](themes/six-columns/screenshot.jpg) |
| *Tema Aurora, aplicado con `tools/theme.sh`* | *Seis columnas y una barra de seis aplicaciones, con el mismo inicio* |
| ![Mover un recuadro: se mantuvo OK, se eligió Mover, el recuadro queda levantado y los demás se oscurecen](docs/tile-move.jpg) | ![La biblioteca de aplicaciones: las aplicaciones instaladas; con un botón se vuelve a poner una aplicación en el Inicio](docs/app-library.jpg) |
| *Con `tile_menu`, mantén OK sobre un recuadro y elige Mover: las flechas lo llevan, Atrás lo suelta* | *Biblioteca de aplicaciones: con un botón vuelve al Inicio una aplicación que habías quitado* |

## Televisores compatibles

Cualquiera que funcione con **Android TV** o **Google TV**.

| Plataforma | Qué funciona |
|---|---|
| **Android TV, Google TV** | La limpieza y el inicio nuevo. |
| **Fire TV** | Solo la parte de limpieza, porque Fire OS no deja que otro inicio ocupe la pantalla principal. Y en el Fire TV Box de 2015 (Fire OS 5) ni siquiera esa parte funciona: rechaza todas las formas de usar `pm`. |
| **Algunos televisores TCL para el mercado chino** | No permiten instalar ningún inicio; sus listas lo dicen en el encabezado. |
| **Samsung (Tizen), LG (webOS)** | Son sistemas distintos. Mira [SHOWCASE.md](SHOWCASE.md#other-platforms-fire-tv-and-lg-webos) para tres adaptaciones a webOS, y [docs/devices/samsung-tizen.md](docs/devices/samsung-tizen.md) para ver qué responde por Wi-Fi un televisor Samsung de 2021 (sin ADB, así que sin `pm disable-user`) si estás pensando en adaptarlo a Tizen. |

Listas probadas por colaboradores, una carpeta por modelo en [`examples/`](examples/):

**TCL** 57 · **Sony** 31 · **Xiaomi** 28 · **Philips** 12 · **Hisense** 9 · **Skyworth** 9 · **Amazon Fire TV** 7 ·
**Thomson** 4 · **BenQ** 3 · **Google** 3 · **OnePlus** 3 · **Panasonic** 3 · **CHiQ** 2 · **FFalcon** 2 · **Haier** 2 ·
**Hitachi** 2 · **Kalley** 2 · **Motorola** 2 · **Nokia** 2 · **NVIDIA Shield** 2 · **onn** 2 · **Redmi** 2 ·
**Toshiba** 2 · **Vu** 2 ·
AiPro2K · AIWA · Artel · Caxium · Cecotec · Challenger · Compac · Dialog · EKO · Freebox · Grundig · Insignia Fire TV ·
JVC · Karbonn · Kogan · Lumio · MTC · Noblex · OK. · PEAQ · Polytron · PRISM+ · RCA · RockTek · Sankey · SANYO · SHARP ·
Super General · Tele System · TiVo · Tornado · Turkcell · Verizon · Vidda · Vision ·
proyectores Anker Nebula, BYINTEK, Epson, Formovie, Gadnic, JMGO, Portronics, Stellamore, Wanbo y XGIMI

<details>
<summary><strong>La lista completa</strong></summary>

| TV | OS |
|---|---|
| AiPro2K (Expressluck, dongnae; Changhong AI PONT family) | Android TV 14 |
| AIWA AI PONT SA (Changhong, osaka, ISDB86AW) | Google TV 14 |
| Amazon Fire TV, AFTDEC012E (ginza), Android 11 | Fire OS / Android 11 |
| Amazon Fire TV smart TV (AFTEU014, greta, MediaTek m7322), Germany | Fire OS 7.6.8.5 / Android 9 |
| Amazon Fire TV 50" 4K smart TV (AFTTIFF43, brandenburg) | Fire OS 7.7.1.7 / Android 9 |
| Amazon Fire TV Stick 4K Max, 1st gen 2021 (AFTKA, kara), Colombia | Fire OS 7.7.1.3 / Android 9 |
| Amazon Fire TV Stick 4K, 1st gen 2018 (AFTMM, mantis) | Fire OS 6.7.1.1 / Android 7.1 |
| Amazon Fire TV Stick 4K, 2nd gen 2023 (AFTKM, karat), Brazil | Fire OS 8.1.8.5 / Android 11 |
| Amazon Fire TV Stick Lite, 1st gen 2020 (AFTSS, sheldon) | Fire OS 7.7.1.7 / Android 9 |
| Anker Nebula Cosmos projector D2140 (D2140-Cosmos, SDMC/Amlogic, 2 GB), Vietnam | Android TV 9 |
| Anker Nebula projector D2426 (D2426_CapsuleIIIPro, baekdu, SDMC/MediaTek m7632, 1.7 GB), Brazil | Android TV 14 |
| Artel smart TV (CVTE TP.MT5510S.PB782, cvt_mt5863_eu, SMART_TV), Uzbekistan | Android 7.0 |
| BenQ E55-735 (Changhong AI PONT, DVB96BQ) | Google TV 14 |
| BenQ E55-750 (Changhong AI PONT, DVB96BQ) | Google TV (Android 11) |
| BenQ GV32 portable projector (SDMC, BenQ_GV01, himalaya, MediaTek m7332) | Google TV 14 |
| BYINTEK Love U4 projector, 1080P (Skyworth RG_HS352, HiSilicon Hi3751V350, 1 GB), Brazil | Android 9 |
| BYINTEK T5 Max projector (built-in Google TV stick: SkyworthDigital YYT, Amlogic), Brazil | Google TV 14 |
| Caxium 58" 147 cm UHD Smart TV (Realtek RTD285O, RTK2851P, TopTech + Zeasn), Colombia | Android TV 9 |
| Cecotec VQU10065S 65" QLED (Vestel-built, shandao, MediaTek), Spain | Android TV 14 |
| Challenger 32T22 BT (cvt_mt5863_col, board TP.MT5510.PB781, MediaTek MT5659, 1 GB RAM), Colombia | Android 7.0 |
| CHiQ AI PONT (Changhong GTVU65, dangni, MediaTek mt5867) | Google TV 14 |
| CHiQ AI PONT (DVB93CQ) | Android TV 11 |
| Chromecast with Google TV 4K (sabrina) | Google TV 14 |
| Chromecast with Google TV HD (boreal) | Google TV 14 |
| Compac ATV R2 (SCBC R2, Realtek RTD285O) | Android TV 9 |
| Dialog ViU (SEI Robotics SEI103DL, Amlogic, NES middleware), Sri Lanka | Android TV 9 |
| EKO 2K Google TV (MTC-built, tennoji, MediaTek mt5867 / T56) | Google TV 14 |
| Epson LS800 laser projector (Askey HA90 module, sti6202d101, Amlogic) | Android TV 14 |
| FFalcon (雷鸟) 鹤6 PRO 65S585C Pro (China, tcl_mt5879_cn, MediaTek MT9653) | Android TV 11 |
| FFalcon (雷鸟) r34a0, China (V8-A920T01-LF1V147, Amlogic T920), 1 GB | Android 5.1.1 |
| Formovie Laser 4K projector (hanlla, MediaTek T31 / m7632, 1.8 GB) | Android TV 14 |
| Freebox Player POP (Free, fbx8am, Amlogic), IPTV/DVB-T box | Android TV 10 |
| Formovie / Fengmi projector MiProjM05 (eva, Amlogic) | Android TV 9 |
| Gadnic PROJ100W projector (built-in Google TV stick: SkyworthDigital YYT, Amlogic HP46B), Argentina | Google TV 14 |
| Google TV Streamer 4K (kirkwood, GZRNL) | Google TV 14 |
| Grundig Android UHD TV (Arçelik, GxGrNM, kunyang, MediaTek), Turkey | Android TV 14 |
| Haier Android TV DVB2K (broadway, HaierATVT56DVB) | Android TV 11 |
| Haier H32S80EFX (MatrixTV CE, HRT56EU, deto, MediaTek), Thailand | Google TV 14 |
| Hisense E5Q Pro (VIDAA_TV, MediaTek MT9653), China | Android TV 11 |
| Hisense Fire TV (AFTCIBFBD1, coyote, MediaTek), US | Fire OS 8.0 / Android 11 |
| Hisense HG9 (HiSmart 4K A4FFM) | Android TV 9 |
| Hisense HiSmartTV A4 (xiaoyushan, MStar m7322), Android 11 firmware RTT2.221108.001 | Android TV 11 |
| Hisense HiSmartTV A4 (xiaoyushan, MStar m7322), India | Android TV 9 |
| Hisense SmartTV 4K FFM (songshan, MediaTek m7632) | Android 11 (SDK 30) |
| Hisense SmartTV 4K FFM (huangshan, MediaTek), Latin America; also the US Hisense U9DG | Android TV 10 |
| Hisense SmartTV 4K FFM (lushan, MediaTek MT9676), Mongolia | Google TV 12 |
| Hisense U75 (hengshan, MediaTek), Latin America | Google TV 12 |
| Hitachi 65QLEDSM20 (MTC, bangbae, MediaTek m7322), Australia | Android TV 11 |
| Hitachi CDH-LE32SMART21 (TCL-built C06, C06_2K_GB, MediaTek MT9221, 1 GB), Argentina | Android TV 11 |
| INCLO Google TV 4K (KTC, Realtek, khardi, KTC_INCLO_4K_EU_23GV1), Taiwan | Google TV 11 |
| Insignia 55" F30 4K Fire TV (NS-55F301NA25, AFTDCT31, duckie) | Fire OS 7 / Android 9 |
| JMGO N1S projector (K80A, holan, MediaTek m7332), Australia | Google TV 14 |
| JVC Android TV (Vestel-built, BARTU_Jvc, menlo, MediaTek mt5867), Spain | Android TV 11 |
| Kalley 43G200 (device R3_GTV, MOKA, Realtek RTD2841A), Latin America | Google TV 14 |
| Kalley R10G (device R10G, product ACER_FFM, MOKA, Realtek RTD2875P), Latin America | Google TV 14 |
| Karbonn SWTV-20AE (Skyworth OEM, SW4H, MediaTek), India | Android TV 10 |
| Kogan Google TV (Changhong CHiQ AI PONT, GTVU65KG, dangni, MediaTek mt5867), Australia | Google TV 14 |
| KTC 4K Smart TV (device hongkong, MediaTek), Taiwan | Google TV 14 |
| Lumio Vision 7 55" (KTC ODM, Realtek, khardi, KTC_LUMIO_4K_EU_23GV1), India | Google TV 14 |
| Motorola MT4310 (Newsan; Hisense board, hayward, MediaTek), Argentina | Android TV 11 |
| Motorola SWTV-24AE-FHD (Skyworth OEM, beomil, MediaTek), India/Global | Google TV 14 |
| MTC UK 2K Android TV (tabata, MediaTek m5621; JVC-family firmware, `android.autoinstalls.config.JVC` present), UK | Android TV 11 |
| Noblex NoblexTV (Skyworth-built, shinjuku, MediaTek m5621), Argentina | Android TV 11 |
| Nokia Streaming Box 8000 (Sagemcom/NES, SEI600NK4, HND, Amlogic) | Android TV 14 |
| Nokia Streaming Box 8010 (Sagemcom/NES, SEI804NK, YYJ, Amlogic) | Android TV 14 |
| NVIDIA SHIELD TV 2019 tube (P3430, sif) | Android TV 11 |
| NVIDIA SHIELD TV Pro 2019 (P2897, mdarcy) | Android TV 11 |
| OK. AI PONT (Changhong, ikebukuro, MediaTek), Italy | Android TV 11 |
| OnePlus TV (C00, Cebu, MediaTek m7632), India | Android TV 10 |
| OnePlus TV (D00, Dubai) | Google TV 14 |
| OnePlus Y1 43" (Y Series, shibuya) | Android TV 11 |
| onn 4K Streaming Box (2023, Walmart; YOC, Amlogic), US | Google TV 14 |
| onn. 4K Plus Streaming (2025, Walmart; coffey, Amlogic S905X5M), US | Google TV 14 |
| Panasonic 4KTV-0SU (Skyworth-built SW4H, MediaTek m7332), Gulf region | Android TV 10 |
| Panasonic 4KTV-JUP (Jupiter_PA, MediaTek) | Android TV 11 |
| Panasonic TH-40HS550K (Skyworth-built, GS655 shibuya, MediaTek) | Android TV 11 |
| Philips 50PUD7406/43 (TPV, PH0M_EA_T32, MStar/MediaTek), Chile | Android TV 11 |
| PEAQ PTV 43AQU-5023C (Changhong, reports OK. AI PONT, dundas, MediaTek m7332) | Android TV 11 |
| Philips 50PUS8517/12 (TP Vision, PH1M_EA_9970A, MediaTek MT5895), Europe | Android TV 11 |
| Philips 55OLED707/12 (TP Vision, PH1M_EA_9970A, MediaTek MT5895), UK | Android TV 11 |
| Philips 55OLED708/12 (TPV, PH1M_WW_9972, MediaTek), Poland | Google TV 12 |
| Philips 55PUS7503/12 (TP Vision TPM171E, PH7M_EU_5596, MediaTek MT5891), Europe | Android TV 8.0 |
| Philips 65PUS8102/12 (TP Vision TPM171E, PH7M_EU_5596, MediaTek MT5891), Europe | Android TV 8.0 |
| Philips 65PUS9435/12 (TP Vision TPM191E, PH9M_EA_5599, MediaTek MT5887), Germany | Android TV 12 |
| Philips 75PUS8505/12 (TP Vision TPM191E, PH9M_EA_5599, MediaTek MT5887), Europe | Android TV 12 |
| Philips Google TV TA7 (TPV, PH3M_AL_T32, MediaTek), Brazil | Google TV 14 |
| Philips R8G Google TV (MOKA, whitefield, Realtek RTD2851F), US | Google TV 14 |
| Philips Smart 4K TV (Skyworth, eleonas, MediaTek), India | Google TV 14 |
| Philips TPM191E (TP Vision, PH9M_EA_5599, MediaTek mt5887), Europe | Android TV 12 |
| Polytron 2K (WLTV POLYTRON2K, hayward; Hisense/CVTE board, MediaTek mt5867), Indonesia | Android TV 11 |
| Portronics Beem 470 Smart LED Projector (Allwinner H713, 1 GB), India | Android 11 |
| PRISM+ Q65 Ultra 2026 QLED 4K AI Google TV (R10G, PRISMPLUS_FFM, MOKA, Realtek RTD2875 SoC, RTD6748 platform) | Google TV 14 |
| RCA AI PONT SA (Changhong, redwood, ISDB92RC; also sold as realme 40-inch and AIWA AW32B4SMG) | Android 14 |
| Redmi TV (MiTV-ANTL0, starwars) | Android 5.1.1 (not Android TV) |
| Redmi TV (MiTV-MFTP0, alita), China firmware 23.2.10.6129 | Android TV 9 (CN build) |
| RockTek GB1 | Google TV 14 |
| SANYO ATV R2 (SCBC, Realtek RTD285O) | Android TV 9 |
| Sankey SMART2KTVSE (Whale OS, SiliconPlayer am30bm) | Android TV 13 |
| SHARP AQUOS TVE21F (AQUOS-TVE21F, banqiao, CVTE/MediaTek), UK | Android TV 14 |
| Skyworth / Coocaa 8R40_K5C (Realtek rtd285x, 1 GB, 32-bit), China domestic firmware | Android 8.0 (not Google TV) |
| Skyworth 65A3F (7T641_A3F, MediaTek MT9633), China | Android 13 (CCOS 10.01.250328) |
| Skyworth Coocaa K3 Pro 90P3D Max (8R145_P3DM, Realtek RTD2885N), China market | Android 11 (Coocaa OS) |
| Skyworth 7S60_A5 (sky8S34, 1.9 GB), China market | Coocaa OS / Android 8 |
| Skyworth SW-22SA (SW6H, MediaTek), ~1.9 GB | Android TV 14 (Google TV home) |
| Skyworth SWTV-21AE (sunnyvale, MediaTek) | Android TV 14 |
| Skyworth SWTV-22AE-FHD (umeda, MediaTek), Vietnam/Global | Google TV 14 |
| Skyworth SWTV-24AE-4K NF (eleonas, MediaTek mt5896), South Africa/Global | Google TV 14 |
| Skyworth SWTV-24NA-4K NF (eleonas, MediaTek mt5896), US | Google TV 14 |
| Sony BRAVIA 4K AE1 (BRAVIA_AE_M6L, MediaTek MT5897), EU | Google TV 12 |
| Sony BRAVIA 4K AE2 (BRAVIA_AE2, MediaTek MT5897), North America | Google TV 14 |
| Sony BRAVIA 4K GB (BRAVIA_ATV2_EU, BRAVIA_ATV2) | Android TV 9 |
| Sony BRAVIA 4K GB (BRAVIA_ATV2_UC, MediaTek mt5891) | Android TV 9 |
| Sony BRAVIA 4K UR2 (BRAVIA_UR2_4K, MediaTek) | Android TV 10 |
| Sony BRAVIA 4K VH1 (KD-55XH9096, BRAVIA_VH1, MediaTek MT5895), EU | Google TV 12 |
| Sony BRAVIA 4K UR3 (BRAVIA_UR3, MediaTek mt5893), EU | Android TV 10 |
| Sony BRAVIA 4K VH2 (KD-55X80J, BRAVIA_VH2, MediaTek), EU | Google TV 12 |
| Sony BRAVIA 4K VH21 (KD-65X85K, 2022, BRAVIA_VH21, MediaTek MT5895), Australia | Google TV 12 |
| Sony BRAVIA 4K VH21 (XR-55A80K, 2022, BRAVIA_VH21, MediaTek mt5895), EU | Google TV 12 |
| Sony BRAVIA 9 II (K-65XR90M2, BRAVIA_AE3, MediaTek MT5838) | Google TV 14 |
| Sony BRAVIA BF1 (BRAVIA 2 II class, BRAVIA_BF1_4K_A, MediaTek) | Google TV 12 |
| Sony BRAVIA KD-49X8307C (2015, "BRAVIA 4K 2015", SVP-DTV15, MediaTek), EU firmware | Android TV 7.0 |
| Sony BRAVIA KD-55X8509C (2015, "BRAVIA 4K 2015", SVP-DTV15, MediaTek), EU firmware | Android TV 7.0 |
| Sony BRAVIA KD-55X85J (2021, BRAVIA_VH2, MediaTek MT5895), South America | Google TV 12 |
| Sony BRAVIA KD-55XF8096 (2018, "BRAVIA 4K GB ATV3", BRAVIA_ATV3_4K_EU, MediaTek MT5891), Spain | Android TV 9 |
| Sony BRAVIA KD-55XE8596 (2017, "BRAVIA 4K GB", BRAVIA_ATV2_EU, MediaTek MT5891), UK | Android TV 9 |
| Sony BRAVIA KD-55XF7596 (2018, "BRAVIA 4K GB ATV3", BRAVIA_ATV3_4K_EU, MediaTek MT5891), EU | Android TV 9 |
| Sony BRAVIA KD-65X80J (2021, BRAVIA_VH2, MediaTek), India | Google TV 10 |
| Sony BRAVIA KD-43X80L (2023, BRAVIA_VH22, MediaTek MT5895), EU | Google TV 12 |
| Sony BRAVIA KD-65X82L (2023, BRAVIA_VH22, MediaTek), India | Google TV 12 |
| Sony BRAVIA KD-65X9300D (2016, SVP-DTV15, MediaTek), Asia-Pacific | Android TV 8.0 |
| Sony BRAVIA TL2 (OD0M_EA_T32, TPV-built, MediaTek), Europe | Android TV 11 |
| Sony BRAVIA VU31 4K (BRAVIA_VU31_4K, Realtek), India | Google TV 14 |
| Sony BRAVIA X9000H (2020, BRAVIA_VH1_CN, MediaTek MT5895), China | Android TV 12 |
| Sony BRAVIA XBR-55X850D (Android model "BRAVIA 4K 2015"), firmware 6.827 | Android TV 8.0.0 |
| Sony BRAVIA XBR-55X850C (2015, "BRAVIA 4K 2015", SVP-DTV15, MediaTek), US firmware | Android TV 8.0 |
| Sony BRAVIA XBR-65X900E (2017, BRAVIA_ATV2) | Android TV 9 |
| Sony BRAVIA XBR-65X900F (2018, BRAVIA_ATV3_4K, MediaTek MT5891), US/Canada | Android TV 9 |
| Sony XR-65A80J (65-inch OLED, 2021, BRAVIA_VH2), EU | Google TV 12 |
| Sony XR-65X90J (2021, BRAVIA_VH2, MediaTek MT5895), China | Android TV 10 |
| Stellamore T950S projector (Droidlogic be30a3, Amlogic txhd2) | Android 13 |
| Super General 55" 4K (CVTE TP.SK708D.PC821, Amlogic T972, x30a4, 1 GB), Saudi Arabia | Android 9 |
| TCL / FFalcon China (tcl9655_cn, MediaTek MT9655 "merak", UTT2.250416.001 AU01) | Android 14 |
| TCL 32L5A (C06, model "Smart TV", 1 GB) | Android TV 11 |
| TCL 32S5400A (C06, C06_2K_GB, MediaTek MT9221, 1 GB), 2023 | Android TV 11 |
| TCL 32S5K (C06, C06_2K_GB, MediaTek MT9221, 918 MB), EU | Android TV 11 |
| TCL 40S5400A (C06, C06_2K_GB, MediaTek MT9221, 1 GB) | Android TV 11 |
| TCL 43P615 (Europe, BeyondTV, Realtek RTD2851, AR06) | Android TV 11 |
| TCL 43S450F-CA (S4 Fire TV Edition, AFTDEC012E, ginza, MediaTek), Canada | Fire OS 8.1.8.5 / Android 11 |
| TCL 43S5400A (C06, C06_2K_GB, MediaTek MT9221, 1 GB) | Android TV 11 |
| TCL 43C645 (Smart TV Pro, Realtek RTD2851 / R51MT05, V8-R51MT05-LF1V652); also TCL 60C635 (G03_4K_GB, Realtek rtd288o), Spain | Google TV launcher on Android TV 11 |
| TCL 43EP660 (Europe, BeyondTV, Realtek rtd285o, V8-R851T02-LF1V378) | Android TV 9 |
| TCL 43S5K (G13, G13_2K_GB, MediaTek MT9221, 1 GB), India | Google TV 14 |
| TCL 50C725K (Smart TV Pro, BeyondTV4/BeyondTV6, RTD2851M, Realtek rtd288o, 2 GB), AR10 build | Android TV 11 |
| TCL 50P735 (BeyondTV4, Smart TV Pro) | Google TV 11 |
| TCL 50DP660 (Europe, "Percee TV", MediaTek MT5658 / board mt5891, V8-T658T01-LF1V602) | Android TV 8.0 |
| TCL 50EP680 (Europe, BeyondTV, Realtek rtd285o) | Android TV 11 |
| TCL 50P615 (Greece, BeyondTV, Realtek RTD2851 / rtd285o, AR05) | Android TV 11 |
| TCL 55" 4K Google TV, 2023 (G10, G10_4K_US_NF); also TCL 55P6K, Spain (G10_4K_GB_NF_32BIT) | Google TV 12 |
| TCL 55C715 QLED (Europe, BeyondTV2, Realtek RTD2851, V8-R851T02-LF1V606) | Android TV 9 |
| TCL 55C725 (Smart TV Pro, BeyondTV4, G03_4K_GB, Realtek R51MT05, V8-R51MT05-LF1V620), Italy | Google TV launcher on Android TV 11 |
| TCL 55C745, 2023 (G08, G08_4K_GB, MediaTek tcl9618) | Google TV 14 |
| TCL 55C815 (2020, Europe/Denmark, BeyondTV2, Realtek rtd285o) | Android TV 11 |
| TCL 55EP640 (Greece, BeyondTV, Realtek RTD2851 / rtd285o, AR04) | Android TV 11 |
| TCL 55P638 (Smart TV, BeyondTV4) | Android TV 11 |
| TCL 55P7K, Middle East (G10, G10_4K_GB, Realtek RTD2875P) | Google TV 12 |
| TCL 55P8LS QD-Mini LED, Vietnam (G10, G10_4K_GB_32BIT, Realtek rtd6748) | Google TV 12 |
| TCL 55Q10G Pro (China, tcl_mt5879_cn, MediaTek MT9952) | Android TV 11 |
| TCL 55S470G (G10, G10_4K_US_NF, Realtek), US | Google TV 12 |
| TCL 55S546 (5-Series, G03_4K_US, BeyondTV4, GTV93), US | Google TV 11 |
| TCL 58S571F (TCL Fire TV, AFTDEC012E, ginza, MediaTek mt5896), US | Fire OS 8 / Android 11 |
| TCL 65C725 (Smart TV Pro, BeyondTV4) | Android TV 11 |
| TCL 65C735 (Smart TV Pro, G05, MediaTek), France; also TCL 55C728, Turkey, and TCL 65C935, France | Google TV 11 |
| TCL 65C7L (Smart TV Pro, G08, G08_4K_GB, MediaTek tcl9618), 2025, Australia | Google TV 14 |
| TCL 65C7K (Smart TV Pro, G08, G08_4K_GB, MediaTek mt5896), Brazil | Google TV 14 |
| TCL 65Q550G (TCL Smart TV, Google TV 11, V8-R51MT08-LF1V095.021344) | Google TV |
| TCL 65Q650G (US Q6 2023, BeyondTV4, Realtek RTD2851 / R51MT08, V8-R51MT08-LF1V095, 2 GB) | Google TV 11 |
| TCL 85RM7L (G08, G08_4K_GB, MediaTek tcl9618) | Google TV 14 |
| TCL 75T7 (Smart TV Pro, G08, G08_4K_US, MediaTek tcl9618), US firmware | Google TV 14 |
| TCL Q7C (Smart TV Pro, G08, G08_4K_GB, MediaTek tcl9618), European firmware | Google TV 14 |
| TCL ak30a5 (China, Amlogic) | Android TV 9 |
| TCL BeyondTV (India) | Android TV 9 |
| TCL BeyondTV, Poland (Realtek RTD2851, AP03, 2 GB) | Android TV 9 |
| TCL BeyondTV, EU/Nordic (Realtek RTD2851, V8-R851T02-LF1V606) | Android TV 9 |
| TCL BeyondTV2 (Latin America / Brazil, Realtek RTD2851) | Android TV 9 |
| TCL BeyondTV2, Android 11 build (AR05, Realtek rtd285o) | Android TV 11 |
| TCL C755 QD-Mini LED, 2024, Australia (G08, MediaTek tcl9618) | Google TV 14 |
| TCL 55C7K QD-Mini LED, 2025, UK (G08, MediaTek tcl9618) | Google TV 14 |
| TCL C89B 85", 2024, a local variant of the C855 (G08, G08_4K_GB, MediaTek tcl9618) | Google TV 14 |
| TCL 75C845X2, UK/Europe (G08_4K_GB, MediaTek tcl9618) | Google TV 14 |
| TCL L40S66E (C06, C06_2K_GB, MediaTek MT9221, 1 GB), Argentina | Android TV 11 |
| TCL QM6K Pro, 2025 (G08, MediaTek tcl9618) | Google TV 14 |
| TCL Smart TV (G07, G07_4K_GB_NF, Realtek RTD2851A, 2 GB) | Google TV 11 |
| TCL Smart TV Pro (G03, G03_4K_GB, BeyondTV4, Realtek R51MT05, V8-R51MT05-LF1V620), Middle East firmware | Google TV 11 |
| TCL Smart TV Pro (G05, G05_4K_US, MediaTek MT5889); also TCL 55Q750G | Google TV 11 |
| TCL Smart TV Pro (G08, G08_4K_GB, MediaTek), Australian firmware | Google TV 12 |
| TCL Smart TV Pro (G08, G08_4K_GB, MediaTek), Europe/UK firmware | Android TV 12 |
| TCL Smart TV Pro (G09, G09_4K_GB, Amlogic T5M, 2 GB), UK firmware, Brazil | Google TV 12 |
| TCL UnionTV, Latin America (TCL-built like Thomson 32HE5800, Realtek RT2841) | Android TV 9 |
| Tele System TS ON T2/HD (ONT2HD, SDMC, Amlogic), Italy | Android TV 11 |
| Thomson 32HE5800 (TCL-built UnionTV, Realtek RT2841), Spain | Android TV 9 |
| Thomson 43RT1055 FA Series (SPPL-built, sauve, Realtek RTD2841A), India | Android TV 14 |
| Thomson SPPL 4K Google TV (Skyworth SW6H, MediaTek, same board as `skyworth-sw-22sa/`), India, ~1.9 GB | Android TV 14 (Google TV home) |
| Thomson T32RTL6000 (SCBC, Realtek; Android reports model `ATV R1`) | Android TV 9 |
| TiVo Stream 4K (SEI Robotics IPA1104HDW, SEI400TV, Amlogic S905Y2, NES) | Android TV 12 |
| Tornado 65UA1400E (El Araby, Skyworth-built SW4H, MediaTek m7332), Egypt | Android TV 11 |
| Toshiba (Vestel Cosmos170, yeoksam, MediaTek), Spain | Android TV 11 |
| Toshiba Fire TV (AFTHA004, hazel) | Fire OS 7 / Android 9 |
| Turkcell TV+ 4K Box (SDMC DV6069Y, Amlogic), Turkey, operator streaming box | Android TV 10 |
| Verizon Stream TV, 1st gen (WNC JS8V, Amlogic), US | Android 12 |
| Vidda VIDAA_TV (Hisense sub-brand; device MT9653, board mt5879), China JuUI | Android TV 11 |
| Vision 2024VISION43STV (CVTE TP.T950D4T.PB751, Amlogic T950D4, 1 GB), Europe | Android 13 |
| Vu 4K (HVCL, lushan, MediaTek), India | Google TV 12 |
| Vu Premium FHD 43-inch (Smart 2K ATV4, hamamatsucho), India | Android TV 9 |
| Wanbo X5 Pro projector (built-in Google TV stick: SkyworthDigital YYT, Amlogic), Australia | Google TV 14 |
| XGIMI Horizon S Pro projector (XK03H, xgimigalileo, MediaTek) | Android TV 11 |
| XGIMI MoGo 2 projector (MoGo, xgimiapollo, pokemon) | Android TV 11 |
| XGIMI MoGo 3 Pro projector (G0035, altai, MediaTek) | Google TV 14 |
| Xiaomi Mi Box 3 (MIBOX3, once), streaming box | Android TV 9 |
| Xiaomi Mi Box S (MIBOX4, oneday), streaming box | Android TV 9 |
| Xiaomi Mi Box S 2nd gen (MiTV-AFKR0, jaws), streaming box | Google TV 11 |
| Xiaomi Mi TV (MiTV-MOOQ0, croods) | Android TV 10 |
| Xiaomi Mi TV 4A (MiTV-MOOQ1) | Android TV 10 |
| Xiaomi Mi TV P1 43" (MiTV-MOOQ2, croods) | Android TV 11 |
| Xiaomi MiTV-AESP0 stick (aquaman, 1 GB) | Android TV 9 |
| Xiaomi MiTV-ANSP0 (小米电视5 Pro 65", jobs, Amlogic), China firmware 23.6.5.3226, 4 GB RAM | Android TV 9 (CN build) |
| Xiaomi MiTV-ASTP0 (mulan, sold as L55M7-EA), China firmware 22.12.2.1630, 1.5 GB RAM | Android TV 9 (CN build) |
| Xiaomi MiTV-ASTP1 (maverick), China firmware 2.40.641.0514.cn, 1 GB RAM, 720p | Android TV 9 (CN build) |
| Xiaomi MiTV-MSSP2 (volver, MediaTek), firmware PI.4621, low-RAM | Android TV 9 |
| Xiaomi TV EA Pro 55" (MiTV-MTEQ0, baymax, MediaTek), China firmware 23.6.26.4028 | Android TV 10 (CN build) |
| Xiaomi MiTV-AXFR1 (rango, Amlogic, 1 GB), India | Android TV 11 |
| Xiaomi MiTV-AXSO0 (dangal; Mi TV 4C Pro 2019 / 4A Pro) | Android TV 9 |
| Xiaomi MiTV-AXSO2 (dangalUHD, India, 2 GB) | Android TV 9 |
| Xiaomi TV S Mini LED 75 2025 (MiTV-MOEU0, ladybird, MediaTek) | Google TV 14 |
| Xiaomi MiTV-MOOR2 / MOOR4 (venom, MediaTek) | Google TV 11 |
| Xiaomi MiTV-MOSR4 (irobot, MediaTek) | Google TV 11 |
| Xiaomi MiTV-MSSP0 / Xiaomi Mi TV 4A 32 (amelie), firmware PI.5926 | Android TV 9 |
| Xiaomi MiTV-MSSP1 (nino), firmware PI.5925 | Android TV 9 |
| Xiaomi MiTV-MSSP3 (machuca, MediaTek) | Android TV 11 |
| Xiaomi MiTV-MSSP3 (machuca, MediaTek), Android 9 firmware PI.7524 | Android TV 9 |
| Xiaomi TV A Pro 75" 2026 (MiTV-MZTU0, river, MediaTek) | Google TV 14 |
| Xiaomi TV Box S 3rd gen (MiTV-AFMU0, twilight, Amlogic), streaming box | Google TV 14 |
| Xiaomi TV Stick 4K 2nd gen (MiTV-AFMU1, twilight, adastra, Amlogic), streaming stick | Google TV 14 |
| Xiaomi TV Stick 4K (MiTV-AYFR0, soul, Amlogic), streaming stick | Android TV 14 |
| Xiaomi TV S Pro 100 Mini LED 2025 (小米电视 S Pro 100, L100MB-SP, MiTV-MFFU0, finch, MediaTek), China firmware OS3.0.115.0.UFFMATV, 4 GB RAM | Android 14 (HyperOS 3, CN build) |
| Xiaomi Redmi Smart TV A Pro 55" 2025 Energy-saving (MiTV-ASTR0, blueplanet, Amlogic), China firmware OS3.0.106.0.USTAATV, 3 GB RAM | Android 14 (HyperOS 3, CN build) |
| Xiaomi MiTV-MFTR0 (freeguy, MediaTek mt9653), China firmware OS2.0.23.0.RFTMATV (HyperOS TV 2) | Android 11 (HyperOS TV 2, CN build) |

</details>

¿Tu televisor no está aquí? Las instrucciones encuentran solas lo que sobra. Después agrega tu lista y la próxima
persona con tu modelo se ahorra ese paso: [CONTRIBUTING.md](CONTRIBUTING.md).

## Hacerlo a mano

Todo lo que hace el asistente lo puedes hacer tú mismo. Las herramientas solo necesitan Python 3.

```bash
python3 -m venv tools/venv && tools/venv/bin/pip install -r tools/requirements.txt
export TV_HOST=192.168.1.50                                   # your TV's IP address

tools/venv/bin/python -I tools/tv.py --probe                 # model, Android version, firmware
tools/venv/bin/python -I tools/tv.py 'pm list packages'      # one shell command on the TV
tools/disable.sh examples/xiaomi-mi-tv-4a/debloat.txt        # apply a debloat list
tools/restore.sh examples/xiaomi-mi-tv-4a/debloat.txt        # undo it, stock launcher back
tools/venv/bin/python -I tools/check.py examples/xiaomi-mi-tv-4a/debloat.txt   # what a firmware update undid
TV_HOST=192.168.1.50 launcher/build-and-install.sh           # build the launcher and make it Home
tools/theme.sh themes/aurora                                 # push a theme; --reset removes it
```

| Herramienta | Qué hace |
|---|---|
| [`tools/tv.py`](tools/tv.py) | Un cliente ADB escrito solo en Python: ejecuta comandos, varios a la vez, envía y trae archivos, reinicia y toma capturas de pantalla, con la opción de presionar antes botones del control remoto. Funciona donde el programa `adb` normal está bloqueado. |
| [`tools/b64push.py`](tools/b64push.py) | Sube archivos grandes, como los APK, en partes codificadas en base64 y comprueba que lleguen completos. |
| [`tools/relay.py`](tools/relay.py) | Redirige un puerto de tu computadora al puerto ADB del televisor, para asistentes cuyo entorno aislado no llega a tu red. Solo escucha en esta computadora. [Guía](tools/relay.md). |
| [`tools/disable.sh`](tools/disable.sh), [`restore.sh`](tools/restore.sh) | Aplican o deshacen una lista de limpieza; para deshacer usan el estado que se guardó antes del cambio. |
| [`tools/recovery.py`](tools/recovery.py) | Escribe el registro que `disable.sh` necesita para deshacerse, y muestra los comandos de restauración. |
| [`tools/check.py`](tools/check.py) | Compara el televisor con la lista que se aplicó, para ver qué deshizo una actualización del firmware; `--fix` lo vuelve a dejar como estaba. |
| [`tools/adb-closed.py`](tools/adb-closed.py) | Comprueba que el puerto ADB de red del televisor quedó cerrado después de apagar la depuración: termina con 0 cuando nada responde, con 1 si sigue abierto y con 2 cuando no pudo hacer la comprobación. No hace falta `nc`. |
| [`tools/privacy.py`](tools/privacy.py) | Revisa el televisor buscando posibles servicios de voz, de reconocimiento de contenido (ACR) y de rastreo, y muestra las pruebas de cada uno; `--write` convierte lo encontrado en una lista que `disable.sh` y `restore.sh` ya entienden. |
| [`tools/theme.sh`](tools/theme.sh) | Envía una carpeta de [`themes/`](themes/) al inicio y reinicia el Inicio. |
| [`tools/bench.py`](tools/bench.py) | Mide el inicio que responde al botón HOME: demora de los botones, cuánto se movió la selección, cuadros entrecortados, arranque en frío, regreso al Inicio, y cuánto procesador y memoria consume en reposo. No cambia nada en el televisor y guarda los números detallados de cada botón en un archivo JSON; no hay que instalar nada extra. |
| [`tools/trace.py`](tools/trace.py), [`trace_report.py`](tools/trace_report.py) | Graba registros de Perfetto del inicio (regreso al Inicio, arranque en frío, flechas del control) e informa en qué se le va el tiempo, en cada prueba y comparando antes con después. Opcional: necesita [`requirements-perf.txt`](tools/requirements-perf.txt). [Guía](tools/trace.md). |
| [`tools/flamechart.py`](tools/flamechart.py) | Dibuja un gráfico de llamas de antes y después a partir de esos registros, para una solicitud de cambios (pull request): una franja por hilo en una misma escala de tiempo, y el trabajo que busca mejorar un cambio en color magenta con su total. Opcional, como las herramientas de registro. [Guía](tools/flamechart.md). |
| [`tools/screendiff.py`](tools/screendiff.py) | Compara una captura de antes y una de después punto por punto, sin contar el reloj ni nada que tú tapes, y guarda las dos con el nombre de tu Wi-Fi borroso. Opcional, como las herramientas de registro. [Guía](tools/screendiff.md). |
| [`tools/race_calendar.py`](tools/race_calendar.py) | Escribe el calendario de Fórmula 1 de esta temporada en un tema para el modo de fin de semana de carrera, usando la API gratuita de Jolpica. |
| [`launcher/build-and-install.sh`](launcher/build-and-install.sh) | Arma una versión final reducida (unos 474 KB), la instala, la pone como Inicio, y vuelve atrás si el Inicio no queda en ella. |

Los programas nunca dejan el televisor sin una aplicación de Inicio: solo desactivan un inicio original que reconocen,
y se saltan la aplicación de Inicio de una lista hasta que otro inicio responda al botón HOME. Más detalles abajo.

<details>
<summary><b>Windows (PowerShell)</b></summary>

Cada programa tiene una versión gemela para PowerShell al lado. En Windows, con Android Studio instalado, no hace falta
nada más:

```powershell
python -m venv tools\venv; tools\venv\Scripts\python.exe -m pip install -r tools\requirements.txt
powershell -ExecutionPolicy Bypass -File launcher\build-and-install.ps1 -TvHost 192.168.1.50
powershell -ExecutionPolicy Bypass -File tools\disable.ps1 -TvHost 192.168.1.50 examples\xiaomi-mi-tv-4a\debloat.txt
```

</details>

<details>
<summary><b>Cómo protegen el Inicio los programas</b></summary>

Los programas de instalación le preguntan al televisor qué inicio ocupa la pantalla principal y solo desactivan uno que reconocen, los cuatro
de `KNOWN_STOCK_LAUNCHERS`: `com.google.android.tvlauncher`, `com.google.android.apps.tv.launcherx`,
`com.google.android.leanbacklauncher` y el de Xiaomi, `com.mitv.tvhome` (PatchWall). Usa
`STOCK_LAUNCHER=<package>` (`-StockLauncher`) para indicar otro, o `none` para no tocarlo.

`tools/disable.sh` (`disable.ps1`) aplica la misma regla antes de desactivar cualquier cosa: si la lista
incluye la aplicación que ocupa el Inicio y ninguna otra aplicación del televisor responde al botón HOME, se salta esa línea, explica
por qué, y desactiva el resto de la lista. El asistente de configuración inicial, las aplicaciones de ajustes, un `FallbackHome` del fabricante
y las aplicaciones de prueba de fábrica (como `com.duokan.factorytest` de Xiaomi) también responden a HOME, pero no cuentan. Así, una lista aplicada antes del cambio de inicio no puede dejar
al televisor sin nada que abrir. Vuelve a aplicar la misma lista cuando `launcher/build-and-install.sh` haya puesto
el inicio nuevo como Inicio, y esa línea se aplicará; `FORCE_HOME=1` (`$env:FORCE_HOME`) la desactiva de todos modos.

</details>

<details>
<summary><b>Dónde pueden estar tus listas</b></summary>

Las rutas de las listas de limpieza que se le pasan a `disable.sh` y `restore.sh` se toman a partir de la carpeta desde donde
los ejecutas, así que tus propias listas pueden estar fuera del repositorio. Las rutas completas también funcionan.

</details>
## El micrófono, y lo que se puede decir sobre él

"¿Cuál de estas aplicaciones está escuchando?" no tiene una respuesta honesta en una línea, y revisar los permisos lo empeora:
en muchos televisores la mayoría de las aplicaciones funcionan como `android.uid.system`, así que cincuenta de ellas muestran
`RECORD_AUDIO: granted=true` y ninguna graba nada. En otros, el micrófono está en el
control remoto, no en el televisor, y una aplicación sin ningún permiso de audio igual ve todo lo que hay en la pantalla
— los programas de reconocimiento de contenido (ACR), como `tv.inscape.tvclient.inscapeacr`, identifican lo que estás viendo a partir de la imagen y solo necesitan
`INTERNET`.

`tools/privacy.py` informa lo que el televisor realmente dice, en vez de adivinar:
`TV_HOST=192.168.1.50 tools/venv/bin/python -I tools/privacy.py` muestra los posibles servicios de voz, ACR y rastreo
en tres grupos, cada uno con su prueba — señalado por el propio
`voice_interaction_service` del firmware, un componente conocido de [`examples/`](examples/), o solo un
nombre que coincide — y además si la aplicación declara `RECORD_AUDIO`, si comparte la identidad del sistema,
y si el historial de AppOps que devuelve muestra uso del micrófono. Un modo configurado o un intento rechazado
por sí solos no prueban que haya habido acceso.

`--write privacy.txt` convierte lo identificado en una lista de limpieza normal, así que aplicarla y
deshacerla se hace con los mismos comandos que ya usas (`tools/disable.sh`, `tools/restore.sh`). Las aplicaciones que
solo coincidieron por el nombre quedan fuera, a menos que uses `--include-low`; son las que conviene revisar antes con
`dumpsys package <name>`.

Lo que la revisión no puede hacer es probar intenciones. `appops` muestra que se usó una función, no qué pasó con el
sonido después, y ninguna revisión de nombres de aplicaciones prueba que un televisor esté o no esté grabando. Desactivar un
asistente es un intercambio en el que pierdes algo concreto (el botón del micrófono del control, la búsqueda por voz dentro
de las aplicaciones), y por eso el informe nombra esa pérdida para cada aplicación en vez de presentarlo como una ganancia.

## El inicio

Una pantalla de inicio pequeña y liviana para Android TV: **unos 474 KB**, escrita en Java simple, pensada para televisores con 1 GB de memoria RAM.
Sin efectos de desenfoque, sin video, sin permiso de red, sin servicios funcionando en segundo plano.

El **televisor** necesita Android 8.0 (API 26) o más nuevo: `minSdk` es un mínimo que se fija al armar el programa en
[`launcher/app/build.gradle`](launcher/app/build.gradle), y el programa de instalación le pregunta al televisor su
`ro.build.version.sdk` antes de armarlo, así que a un televisor más viejo se le muestran los dos números en vez de fallar en
`pm install` (mira [Solución de problemas](docs/TROUBLESHOOTING.md) para saber qué se puede hacer en esos televisores).

| Qué | Cómo funciona |
|---|---|
| **Configurar** | Orden de la barra, aplicaciones ocultas, aplicación de TV en vivo, de 4 a 7 recuadros por fila, menos movimiento. Todo en [`config.xml`](launcher/app/src/main/res/values/config.xml) |
| **Ajustes en el televisor** | Mantén OK sobre Configuración para abrir los ajustes del inicio. La opción `launcher_settings_button` hace que un clic normal los abra directamente; los ajustes del televisor siguen en la página de ajustes y en su recuadro de aplicación. |
| **Temas** | Fondo, fondo de pantalla y diseño desde un `config.json` enviado por Wi-Fi, sin volver a armar el inicio. Vienen siete en [`themes/`](themes/), incluido el `default/` que trae de fábrica |
| **25 idiomas** | Usa el idioma del televisor, con un diseño completamente en espejo, de derecha a izquierda, para el hebreo |
| **Biblioteca de aplicaciones** | Opcional: recorre todas las aplicaciones instaladas y agrega o quita accesos directos del Inicio. Mira [la guía de la biblioteca de aplicaciones](docs/app-library.md) |
| **Menú del recuadro** | Opcional (`tile_menu`): mantén OK sobre un recuadro para Mover, Quitar del Inicio e Información de la aplicación. Si está apagado, mantener OK abre la Información de la aplicación |
| **Tarjetas de módulo** | Cualquier aplicación del televisor puede ofrecer su propio recuadro; tú apruebas cada una una sola vez. Mira [`docs/modules.md`](docs/modules.md) |
| **Complementos** | Aplicaciones opcionales que se conectan como tarjetas de módulo, guardadas en [`addons/`](addons/) y nunca incluidas dentro del inicio |
| **Protector de pantalla de reloj** | Un reloj que se desplaza sobre el brillo, para que nada quede marcado en la pantalla |
| **Botones del control remoto** | Mantiene funcionando los botones de Entrada, YouTube y el engranaje después de quitar el inicio original |

<details>
<summary><b>Armarlo tú mismo</b></summary>

Necesita JDK 17 y la plataforma 34 del SDK de Android. En macOS: `brew install openjdk@17 android-commandlinetools`
y `sdkmanager "platforms;android-34" "build-tools;34.0.0"`. En Linux, el programa de instalación encuentra
`~/Android/Sdk` y el `java` que esté en tu PATH.

</details>

<details>
<summary><b>Configurar</b></summary>

[`config.xml`](launcher/app/src/main/res/values/config.xml) define el orden de la barra, las aplicaciones ocultas, la aplicación de
TV en vivo, las columnas (los recuadros se achican a partir de 5), las filas debajo de la barra, una aplicación de VPN opcional para el botón de red,
y `reduced_motion` para televisores cuyo procesador gráfico no da abasto. Los temas definen las mismas opciones, más un color de fondo
y un fondo de pantalla.

</details>

<details>
<summary><b>Ajustes del inicio y el inicio predeterminado</b></summary>

- Haz clic en **Configuración** para abrir los ajustes propios del televisor. Mantén OK sobre ese botón y elige **Ajustes del inicio**, o ábrelos
  con un clic directo si usas `launcher_settings_button`. La página propia del inicio tiene estas filas, de arriba hacia abajo:
  - **Reordenar aplicaciones**, solo con `launcher_settings_button`: OK levanta una aplicación, las flechas la mueven, Atrás
    la suelta, y Atrás otra vez termina.
  - **Aplicaciones por fila** 4, 5, 6 o 7; **Filas debajo de la barra** de 0 a 3, cuántas filas de recuadros se ven debajo de la
    franja de la barra; **Opacidad de la franja de la barra** 100%, 70%, 50% o 30%. Las dos últimas solo hacen algo mientras la barra
    está en su propia fila (`dock_row`, activado de forma predeterminada).
  - **Fondo de pantalla**: una imagen de la colección del tema (o su `wallpaper.jpg`), **Ninguno**, o **Predeterminado del
    tema**. Al elegir una, esa imagen se queda fija y deja de rotar hasta que elijas Predeterminado del tema, presiones
    Seguir el tema, o vuelvas a enviar el tema.
  - **Animaciones** activadas o desactivadas, y **Efectos avanzados** (recuadros que se levantan, íconos que se agrandan y cambios suaves del
    color de fondo; pueden usar más memoria) cuando las animaciones están activadas.
  - **Seguir el tema (borrar lo elegido en el televisor)**, que borra todas las elecciones de arriba. Enviar o restablecer un tema
    también las borra.
  - **Elegir inicio predeterminado** abre el selector de inicio de Android, y **Ajustes del sistema del televisor** abre la página de ajustes propia
    del televisor.
- **Cambiar el inicio predeterminado:** los Ajustes del inicio y el recuadro opcional de Inicio predeterminado
  (`show_home_settings_shortcut`) abren el selector de inicio de Android. Elige el inicio original para dejar de usar
  CleanYourTV como Inicio, o CleanYourTV para volver a él. El inicio original tiene que estar activado; si el programa de instalación
  lo desactivó, primero ejecuta el programa de restauración que aparece más abajo. Algunos televisores no tienen selector de inicio.

</details>

<details>
<summary><b>Idiomas</b></summary>

Inglés, alemán, español, catalán, francés, ruso, serbio (alfabeto latino), polaco, checo, italiano, portugués,
turco, árabe, hebreo, chino simplificado, chino tradicional (Taiwán), tailandés, finlandés, vietnamita,
bengalí, indonesio, noruego bokmål, neerlandés, uzbeko (alfabeto latino) y ucraniano. El inicio usa el idioma del televisor. Android 13 o más nuevo permite elegirlo
solo para el inicio: `tools/tv.py 'cmd locale set-app-locales com.gathin.tvhome --locales ca'`.

En hebreo el diseño se pone en espejo: los botones del menú a la izquierda, la fecha y el reloj a la derecha con el saludo arriba,
la barra y las filas de aplicaciones empiezan por la derecha y el control remoto se mueve igual, los íconos y nombres del selector de entradas
quedan a la derecha, y las fechas llevan el prefijo de mes ב (por ejemplo, 19 באוקטובר). El protector de pantalla de reloj
alinea a la derecha su fecha y su hora. El ruso cubre todas las pantallas, incluidos los fines de semana de carrera, los saludos de fiestas y la fecha del calendario persa (Shamsi). Los demás
idiomas mantienen su diseño original.

</details>

<details>
<summary><b>Tarjetas de módulo</b></summary>

Cualquier aplicación del televisor puede declarar su propio recuadro (nombre, texto, brillo). El inicio te pregunta una vez por cada aplicación, lo deja
oculto de forma predeterminada, y recuerda tu respuesta según la firma de esa aplicación y el nombre de la tarjeta. Mantén OK sobre Configuración
y elige Tarjetas de módulo si cambias de opinión. Cómo hacer una: [`docs/modules.md`](docs/modules.md); las
reglas técnicas: [`docs/specs/card.md`](docs/specs/card.md).

</details>

<details>
<summary><b>Protector de pantalla de reloj</b></summary>

Elige "Reloj" en los ajustes del protector de pantalla del televisor, o hazlo por ADB:

```bash
tools/tv.py 'settings put secure screensaver_components com.gathin.tvhome/.ClockDream; settings put secure screensaver_enabled 1'
```

</details>

<details>
<summary><b>Botones del control remoto</b></summary>

- Un servicio de accesibilidad opcional mantiene funcionando el botón **Entrada** del control en Google TV
  (`INPUT_KEY_SERVICE=1` al instalar).
- Puede recuperar otros botones que solo atendía el inicio original, como el botón de **YouTube**
  (`app_keys` y `input_key_keycodes`, en config.xml o en un tema; `HOME_KEY_SERVICE=1` también lee `app_keys`).
- El prefijo `hold:` en una línea de `app_keys` le da a ese botón una segunda aplicación: una pulsación normal abre la
  aplicación sin prefijo, y mantenerlo presionado medio segundo abre la otra (por código de tecla o `hold:scan:...`).
- `HOME_KEY_SERVICE=1` también arregla los dispositivos tipo "stick" cuyo botón de Inicio envía ALL_APPS, y abre Configuración desde el botón del
  **engranaje** del control, incluso uno que Android no reconoce (códigos de tecla en config.xml).
- Con `settings_key_panel`, el engranaje abre un [pequeño panel de ajustes rápidos](docs/quick-settings-panel.jpg)
  encima del Inicio o de cualquier aplicación: ajustes del televisor, Pantalla, Red, Aplicaciones y Ajustes del inicio.

</details>

<details>
<summary><b>Navegación e imágenes</b></summary>

Arriba y Abajo mueven una fila. Los botones de arriba nunca saltan a los recuadros, y Abajo desde ellos vuelve al
recuadro de la barra desde el que llegaste. Se recuerda la última aplicación seleccionada, y al instalar o quitar una aplicación se actualizan
los recuadros mientras el Inicio está abierto. Las imágenes de las aplicaciones se cargan en alta resolución (xhdpi o más), para que los televisores de baja resolución no las
achiquen antes del acercamiento al seleccionarlas.

</details>

## Restaurar tu televisor

Guarda la lista que aplicaste. Con una sola línea el televisor vuelve a quedar como estaba:

```bash
TV_HOST=192.168.1.50 tools/restore.sh examples/<your tv>/debloat.txt                                    # Android TV
TV_HOST=192.168.1.50 tools/restore.sh examples/<your tv>/debloat.txt com.google.android.apps.tv.launcherx  # Google TV
```

| Qué | Cómo |
|---|---|
| **Primero se guarda un registro** | Antes de que `tools/disable.sh` cambie algo, anota cómo estaba el televisor, en `~/.cleanyourtv/`. |
| **La restauración lo repite al revés** | Una aplicación que tú mismo habías desactivado sigue desactivada, y el Inicio vuelve a quien lo ocupaba antes. |
| **El inicio nuevo queda instalado** | Quítalo desde Configuración → Aplicaciones del televisor si ya no lo quieres. |
| **¿No tienes computadora?** | Si no puedes conectarte al televisor, su propia página de Configuración → Aplicaciones también permite volver a activar aplicaciones. |

<details>
<summary><b>Qué guarda el registro, y qué pasa si no hay uno</b></summary>

Antes de que `tools/disable.sh` cambie algo, anota cómo estaba el televisor: para cada aplicación
de la lista, si estaba activada, ya desactivada o no instalada; qué componente ocupaba el Inicio;
y las tres escalas de animación. Ese registro se guarda en `~/.cleanyourtv/`, un archivo por televisor y por lista, y
si se vuelve a aplicar la misma lista se conserva el primer registro en vez de guardar encima el estado ya limpio.
Si desde entonces agregaste aplicaciones a la lista, esa vez se suman al registro antes de desactivarlas.

Guarda la lista que aplicaste. El programa de restauración repite el registro, así que una aplicación que tú mismo habías desactivado
sigue desactivada y el Inicio vuelve al componente que lo ocupaba:

El argumento `stock launcher` es solo un plan de respaldo: si hay registro, el inicio que realmente ocupaba el Inicio
es el que lo recupera, y el argumento solo se usa cuando nada respondía al botón HOME en ese momento
o cuando lo ocupaba el inicio de este proyecto. El inicio original se vuelve a activar de todas formas, salvo que ya
estuviera desactivado cuando se guardó el registro.
Sin registro (de una versión anterior, o porque lo borraste) el programa lo avisa y vuelve a lo que hacía antes:
activar toda la lista y poner las escalas en `1.0`.

Deja instalado el inicio nuevo (quítalo desde Configuración → Aplicaciones del televisor si ya no lo quieres)
y no sabe nada de las aplicaciones que desactivaste fuera de la lista. Para volver a cambiar más adelante, ejecuta otra vez el
programa de instalación; descubre qué inicio desactivar incluso cuando el Inicio quedó en el
selector de Android. Si no puedes conectarte al televisor, su propia
página de Configuración → Aplicaciones también permite volver a activar aplicaciones.

</details>

## Después de una actualización del firmware

Una actualización se instala encima del sistema ya limpio: las aplicaciones de la lista vuelven, el Inicio pasa al
inicio original, y aparecen nuevas aplicaciones preinstaladas que ninguna lista menciona. Nada más aquí se da cuenta, así que
compara el televisor con la lista que aplicaste:

```bash
TV_HOST=192.168.1.50 tools/venv/bin/python -I tools/check.py examples/<your tv>/debloat.txt
```

Muestra lo que cambió y termina con 1 cuando algo cambió, así que basta una tarea semanal en un servidor de casa o en una Raspberry Pi
para enterarte:

```bash
0 9 * * 1 cd ~/cleanyourtv && TV_HOST=192.168.1.50 tools/venv/bin/python -I tools/check.py examples/<your tv>/debloat.txt
```

`--fix` vuelve a aplicar la lista a lo que cambió: pone como Inicio el inicio que la lista no
desactiva (indica una aplicación como segundo argumento si usas una versión modificada), luego desactiva las aplicaciones de la lista
que volvieron, y revisa el televisor para confirmar las dos cosas. No escribe un registro de recuperación, porque el
registro ya tiene el estado de antes de la primera vez: `tools/restore.sh` igual devuelve el televisor a como venía
de fábrica después. Primero se arregla el Inicio; si no queda ningún inicio que pueda ocuparlo, `--fix` no cambia nada
y lo avisa.

Hace las mismas comprobaciones de seguridad que `tools/disable.sh` antes de desactivar cualquier cosa, porque una actualización es
justo el momento en que vuelven a importar: deja activado setupwraith mientras la red Wi-Fi guardada le pertenezca
(`FORCE_SETUPWRAITH=1` si usas cable de red), deja activadas las aplicaciones de las entradas HDMI/AV
(`TVINPUT_ALLOW=1` si de verdad quieres apagarlas), y nunca pone como Inicio un `FallbackHome` del fabricante ni
una aplicación de prueba de fábrica.
Cada aplicación que deja activada viene con su motivo y termina con 1, porque el televisor no vuelve a estar como dice la lista
hasta que resuelvas eso a mano.

Las listas que también desactivan el actualizador no reciben ninguna actualización. Para instalar una, vuelve a activar el actualizador en
el televisor, deja que se actualice, ejecuta `check.py --fix`, y desactiva el actualizador otra vez.

En Windows el mismo comando es `tools\venv\Scripts\python.exe -I tools\check.py <list>`.

## Cuando algo sale mal

La lista completa de problemas que nos encontramos está en [docs/TROUBLESHOOTING.md](docs/TROUBLESHOOTING.md). Los
tres más importantes:

- 🍎 **macOS bloquea `adb connect`** ("No route to host") por la privacidad de Red local. `tools/tv.py` evita ese programa.
- ⚠️ **Desactiva el inicio original solo después de que el nuevo esté instalado y funcionando**, o el Inicio termina en una aplicación de prueba de fábrica. El programa de instalación lo hace en ese orden por ti.
- 🔁 **En Google TV, el asistente de configuración inicial** (`com.google.android.tungsten.setupwraith`) puede ocupar el Inicio y hacer que el sistema se cuelgue una y otra vez después de desactivar el inicio original. Desactívalo también, y agrégalo a tu `debloat.txt` para que la restauración lo traiga de vuelta. Pero antes revisa `dumpsys wifi | grep -o 'cname=[^ ]*'`: si la red Wi-Fi se guardó durante la configuración inicial, le pertenece a setupwraith, y desactivarlo borra la red (primero vuelve a conectarte a ella desde Configuración; `tools/disable.sh` se salta setupwraith hasta que lo hagas). En el propio Chromecast de Google y en el Google TV Streamer también pierdes la opción de transmitir desde el teléfono; mira [Solución de problemas](docs/TROUBLESHOOTING.md). ¿Ya te quedaste atascado? `tools/tv.py 'pm enable --user 0 com.google.android.apps.tv.launcherx'`.

## Preguntas frecuentes

<details>
<summary><b>No sé programar y no tengo computadora portátil. ¿Igual puedo hacerlo?</b></summary>

Sí. [@udhaykumarbala](https://github.com/udhaykumarbala) creó una [aplicación para el teléfono](https://cleanyour.tv/app) gratuita y de código abierto
para Android que hace la misma limpieza por Wi-Fi: se conecta al televisor, primero te muestra un plan, guarda un punto de
restauración, y solo apaga aplicaciones, así que todo se puede volver a poner. Está hecha por la comunidad.

</details>

<details>
<summary><b>¿Es seguro? ¿Puede dejar el televisor inservible?</b></summary>

No se reinstala el sistema, no se hace root ni se borra nada; las aplicaciones se desactivan
en el perfil del usuario. El riesgo es desactivar algo que el televisor necesita, y por eso las listas se
aplican en grupos pequeños con un programa de restauración listo. La propia página de Configuración → Aplicaciones del televisor puede
volver a activar aplicaciones incluso sin las herramientas.

</details>

<details>
<summary><b>¿Y las actualizaciones del firmware?</b></summary>

En la mayoría de las listas el actualizador queda activado, así que las actualizaciones del firmware llegan como siempre. Algunas listas desactivan el
actualizador propio del televisor, y en esos casos una actualización solo llega cuando lo vuelves a activar. Cuando llega una,
se instala encima del sistema ya limpio, así que alguna aplicación vuelve y tienes que ejecutar el programa otra vez: mira
[Después de una actualización del firmware](#después-de-una-actualización-del-firmware).

</details>

<details>
<summary><b>¿No se van a romper las aplicaciones?</b></summary>

Las aplicaciones de streaming se siguen actualizando por la Play Store, que no se toca.
El inicio solo muestra lo que está instalado y lo abre con métodos de Android que no han cambiado en una década.

</details>

<details>
<summary><b>¿Puedo hacerlo para alguien que vive en otra casa?</b></summary>

Sí, por una conexión privada de [Tailscale](https://tailscale.com)
en vez de estar en el mismo Wi-Fi: ya sea con Tailscale en su televisor, compartido contigo, o con una computadora o un Apple
TV en su casa que te dé acceso a él. Nunca abriendo el puerto ADB en su router. El paso a paso está en
[docs/REMOTE.md](docs/REMOTE.md).

</details>

<details>
<summary><b>¿El acceso ADB no es un agujero de seguridad?</b></summary>

Es un único toque explícito de "permitir esta computadora" en el televisor, lo
mismo que cuando se desarrolla una aplicación para Android. El ADB por red viaja sin cifrar por el puerto 5555, y en los firmwares con
`ro.adb.secure=0` cualquier aparato de tu red local puede entrar, así que ciérralo cuando termines:

1. En el televisor: Opciones de desarrollador → desactiva **Depuración por USB** y **Depuración por red/ADB**, y
   revoca las autorizaciones de depuración por USB.
2. Reinicia el televisor y luego confirma desde tu computadora que el puerto ya no está:
   `python3 tools/adb-closed.py <tv ip>` tiene que decir que el puerto está cerrado. Con `nc -vz <tv ip> 5555`,
   solo cuenta "Connection refused": en macOS, la privacidad de Red local puede bloquear `nc` y hacerlo
   fallar con "No route to host" aunque el puerto siga abierto.

El inicio sigue funcionando sin la depuración.

</details>

<details>
<summary><b>¿También puede bloquear la publicidad dentro de las aplicaciones?</b></summary>

En parte, con el DNS privado de Android (Android 9 o más nuevo). Apúntalo
a un servidor que bloquee anuncios, como [AdGuard DNS](https://adguard-dns.io), y las direcciones de anuncios y
rastreo de todas las aplicaciones dejan de funcionar, en todo el sistema, y se mantiene después de reiniciar. La contra: ese servidor
ve todas las consultas DNS que hace el televisor.

```bash
tools/tv.py 'settings put global private_dns_specifier dns.adguard-dns.com'
tools/tv.py 'settings put global private_dns_mode hostname'
```

No quita los anuncios de YouTube, que vienen de los mismos servidores que los videos. Cuando el televisor dice
"Sin conexión a internet", el servidor está caído o no se puede alcanzar, y volver atrás lo arregla todo:
`tools/tv.py 'settings put global private_dns_mode opportunistic'`. Un servidor que sí responde igual puede
hacer fallar una aplicación en particular, así que si una sola aplicación falla mientras las demás funcionan, mira
[una aplicación no reproduce](docs/TROUBLESHOOTING.md#una-app-se-niega-a-reproducir-mientras-el-resto-de-la-tv-está-en-línea)
antes de buscar el problema en la aplicación.

</details>

<details>
<summary><b>¿AirPlay?</b></summary>

No desde este repositorio. Chromecast integrado se mantiene para los teléfonos Android. Para iPhone,
[jqssun/android-airplay-server](https://github.com/jqssun/android-airplay-server) funciona; un programa de instalación
para eso está en el [PR #84](https://github.com/Gathin23/cleanyourtv/pull/84).

</details>

<details>
<summary><b>¿Puedo simplemente descargar el APK?</b></summary>

Ármalo con el programa de una sola línea; tarda un minuto y tú
controlas lo que se instala en tu televisor. No hay programas ya armados para descargar.

</details>

## Cómo colaborar

La colaboración más útil es la lista de limpieza de tu televisor, para que la próxima persona con ese modelo no
tenga que descubrirla de nuevo. [CONTRIBUTING.md](CONTRIBUTING.md) explica el formato y las pruebas que pedimos.
¿Colaboras a través de un asistente de programación? [AGENTS.md](AGENTS.md) le da las mismas reglas.

| Cómo ayudar | Qué significa |
|---|---|
| **La lista de limpieza de tu televisor** | La más útil: la próxima persona con ese modelo se ahorra buscar qué desactivar. |
| **Inicio e instrucciones** | También son bienvenidas las mejoras al inicio y una redacción más clara de las instrucciones. |
| **¿Creaste algo a partir de esto?** | Un inicio, una adaptación, un tema: agrégalo a [SHOWCASE.md](SHOWCASE.md), donde ya hay setenta proyectos, ordenados en pantallas de inicio, versiones derivadas, complementos, herramientas y otras plataformas, con un índice por marca de televisor. |

Las personas cuyo trabajo está en este repositorio:

<a href="https://github.com/Gathin23/cleanyourtv/graphs/contributors"><img src="https://contrib.rocks/image?repo=Gathin23/cleanyourtv&columns=16&max=400" alt="Colaboradores"></a>

<details>
<summary><strong>Historial de estrellas</strong></summary>

<a href="https://star-history.com/#Gathin23/cleanyourtv&Date"><img src="https://api.star-history.com/svg?repos=Gathin23/cleanyourtv&type=Date" alt="Gráfico del historial de estrellas" width="640"></a>

</details>

## Contacto

| Para | Dónde |
|---|---|
| **Preguntas sobre tu televisor** | [GitHub Discussions](https://github.com/Gathin23/cleanyourtv/discussions) |
| **Prensa y alianzas** | [hello@itsgathin.com](mailto:hello@itsgathin.com) |
| **Problemas de seguridad** | Repórtalos en privado desde la [pestaña Security](https://github.com/Gathin23/cleanyourtv/security); mira [`SECURITY.md`](SECURITY.md) |

## Aviso legal

- CleanYourTV es un proyecto independiente de código abierto. No está asociado, respaldado ni patrocinado
  por ningún fabricante de televisores ni plataforma. Los nombres de marcas y modelos se usan solo para decir en qué televisor se probó una lista,
  y siguen siendo marcas registradas de sus dueños.
- Funciona solo a través de opciones que el propio televisor le ofrece a su dueño: las Opciones de desarrollador, la depuración ADB y
  el propio `pm disable-user` de Android, el mismo interruptor que Configuración > Aplicaciones > Desactivar. No hace root al televisor,
  no reinstala el firmware ni salta ningún bloqueo, DRM o protección anticopia, y el repositorio no contiene programas,
  firmware ni APK de ningún fabricante.
- No se desinstala nada, y `tools/restore.sh` vuelve a poner todo como estaba. Lo usas en un televisor que es tuyo, bajo tu
  propia responsabilidad, y cambiar los programas de un televisor puede afectar su garantía o el soporte técnico.
- Todo lo que hay aquí se ofrece tal como está, sin garantía de ningún tipo, bajo la licencia MIT que aparece abajo.

## Licencia

MIT, mira [`LICENSE`](LICENSE). La letra Outfit está bajo la SIL Open Font License; mira
`launcher/FONT-LICENSE-OFL.txt`.
