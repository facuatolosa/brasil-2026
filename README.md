# ✈️ Río + Búzios 2026 — Guía de viaje interactiva

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-vanilla-F7DF1E?logo=javascript&logoColor=black)
![PWA](https://img.shields.io/badge/PWA-instalable-5A0FC8?logo=pwa&logoColor=white)
![Leaflet](https://img.shields.io/badge/Leaflet-1.9.4-199900?logo=leaflet&logoColor=white)
![Versión](https://img.shields.io/badge/versi%C3%B3n-12.1.3-0B2E42)

Guía de viaje **personalizada** para un viaje a **Río de Janeiro y Búzios (Brasil) del 10 al 18 de noviembre de 2026**, desarrollada como una *Single Page Application* en **un único archivo HTML** (HTML + CSS + JavaScript vanilla), sin frameworks ni proceso de compilación.

🔗 **Sitio publicado:** <https://brasil-2026.facuatolosa.workers.dev/>

---

## Tabla de contenidos

1. [Descripción general](#1-descripción-general)
2. [Contexto del viaje](#2-contexto-del-viaje)
3. [Funcionalidades](#3-funcionalidades)
4. [Historial de versiones](#4-historial-de-versiones)
5. [Arquitectura y consideraciones técnicas](#5-arquitectura-y-consideraciones-técnicas)
6. [Problemas conocidos y deuda técnica](#6-problemas-conocidos-y-deuda-técnica)
7. [Ejecución local y despliegue](#7-ejecución-local-y-despliegue)
8. [Ideas a futuro](#8-ideas-a-futuro)
9. [Autoría y licencia](#9-autoría-y-licencia)

---

## 1. Descripción general

El proyecto reúne en una sola aplicación web todo lo necesario para **preparar, vivir y organizar** el viaje: dónde se alojan, qué clima esperar y qué ropa llevar, una lista de verificación editable, presupuesto y control de gastos, cotizaciones del real por PIX en tiempo real, recomendaciones turísticas con mapas, frases útiles en portugués con pronunciación, y un repositorio de documentos del viaje (PDF y enlaces). Desde la v12 suma un **itinerario día por día** con horarios, costos y un **mapa numerado del recorrido**.

Objetivos de diseño:

- **Un solo archivo, cero dependencias de build.** Se abre con doble clic o se publica en cualquier hosting estático.
- **Funciona en el celular** (diseño responsivo, instalable como PWA) y también offline para lo ya cargado.
- **Los datos del usuario no salen del dispositivo**: checklist, gastos, enlaces y PDF se guardan en el navegador (`localStorage` / `IndexedDB`).
- **Identidad visual propia**: paleta tropical (azul océano, coral, verde, arena) con tipografías *Fraunces*, *Manrope* y *Space Mono*, y una onda inspirada en el calçadão de Copacabana como motivo recurrente.

La aplicación es de uso personal, pero está pensada para poder reutilizarse como plantilla de otros viajes cambiando los textos, fechas y coordenadas.

## 2. Contexto del viaje

Datos que contiene la guía (visibles en la propia página):

| Concepto | Detalle |
|---|---|
| Fechas | Salida el **10/11/2026 a las 03:20 hs** · regreso con llegada el **19/11/2026 a las 02:20 hs** |
| Vuelo | Directo desde Córdoba con Gol |
| Equipaje | Solo cabina: carry-on de 10 kg + mochila |
| Alojamiento | **3 noches** en Río de Janeiro (Rede Andrade Hotel Canadá, Copacabana) + **5 noches** en Búzios (Pousada Brisas de Búzios, zona Tartaruga) |
| Incluye | Traslados, desayuno y asistencia médica |

---

## 3. Funcionalidades

La aplicación se organiza en **10 pestañas** con barra de navegación fija (*sticky*), más un encabezado con cuenta regresiva y un pie de página personal.

### 3.1 Encabezado (hero) y navegación

- **Cuenta regresiva** en vivo (días, horas, minutos y segundos) hasta la salida del vuelo, calculada con la hora local del dispositivo. Tras la salida muestra *«¡Ya estás de viaje!»* y, pasada la llegada de regreso, un mensaje de fin de viaje.
- **Barra de pestañas fija** con desplazamiento horizontal: arrastre con el mouse en escritorio, gesto táctil en celulares y barra visible en PC.
- **Cambio de pestaña sin saltar al inicio de la página**: si ya se bajó más allá del encabezado, la nueva sección arranca justo debajo de la barra de pestañas; la pestaña activa se centra automáticamente en la barra.
- **Barra de copia de seguridad** (Guardar / Restaurar copia), visible solo en *Checklist* y *Documentos*.

### 3.2 🏨 Alojamiento

- Ficha de cada alojamiento: dirección, noches, valoración, **puntos a favor / a tener en cuenta** según reseñas y un consejo práctico.
- **Mapa de Google Maps embebido** para cada hotel (ubicación exacta del alojamiento).

### 3.3 🌤️ Clima y ropa

- Promedios de noviembre para Río y Búzios (temperaturas, humedad, probabilidad de lluvia, agua de mar).
- **Clima en tiempo real** (OpenWeatherMap): temperatura actual, mínima/máxima del día, humedad y descripción con emoji, para Copacabana y Tartaruga. Se consulta una sola vez, al entrar a la pestaña.
- Recomendaciones de ropa por situación (playa, lluvia/sol, noche) y consejos para armar una valija de cabina.

### 3.4 ✅ Checklist

- **7 categorías y 32 ítems** por defecto: documentación, equipaje de cabina, ropa y calzado, salud y botiquín, dinero y pagos, tecnología y antes de salir de casa.
- Barra de **progreso** (ítems tildados / total) y botón para destildar todo.
- **Modo edición** (botón arriba a la derecha): agregar, modificar y quitar ítems en cada sección. Los cambios y el progreso se guardan automáticamente.
- Migración automática del progreso de la versión 1 (checklist fija) al formato editable.

### 3.5 💰 Presupuesto

- Tabla de **precios de referencia** (comidas, bebidas, transporte, excursiones) y **tres niveles de gasto diario** (mochilero, gama media, cómodo) con una estimación total para los 8 días, sin contar lo ya incluido en el paquete.
- Guía de **medios de pago para argentinos en Brasil** (billetera con Pix, tarjeta de crédito saldada en dólares, efectivo como respaldo y por qué evitar la tarjeta de débito en pesos).

### 3.6 📊 Gastos

- **Gráfico de dona** (CSS `conic-gradient`) con el total gastado en **R$** y leyenda por categoría con monto y porcentaje.
- Alta de gastos con **fecha** (hoy por defecto), descripción, categoría y monto.
- **Categorías administrables** (por defecto: Comida, Transporte, Excursiones, Supermercado y Otros). Al borrar una categoría, sus gastos se reasignan a «Otros»; siempre queda al menos una.
- **Filtros** por texto y por categoría, listado ordenado por fecha descendente y **edición en línea** (guardar / cancelar) o borrado de cada gasto.
- Todo se guarda en el dispositivo.

### 3.7 🗺️ Turismo

- Lugares a visitar en **Río** y **Búzios**, con etiqueta **Gratis / Pago** y consejos de movilidad (metro, Uber/99, combis, buggy, a pie).
- **Un mapa interactivo por destino** (Leaflet) con los puntos de interés mencionados en la pestaña:
  - **Forma del marcador por ciudad**: círculos en Río, rombos en Búzios.
  - **Color por costo**: 🟢 verde = gratis · 🔴 rojo (con insignia «$») = pago · ⬛ azul oscuro con 🏠 = alojamiento.
  - Cada marcador está numerado y abre una ficha con descripción y enlace a Google Maps.
  - Debajo del mapa, una **lista** de los mismos puntos: al tocar uno se abre su ficha en el mapa; el botón ↗ abre el lugar en Google Maps.
  - En pantallas táctiles el mapa arranca «bloqueado» (para no interferir con el scroll) y se activa tocando un aviso.
  - Los marcadores de **alojamiento (🏠)** tienen un efecto de pulso para destacarlos.
  - Cada mapa incluye una **escala métrica** y se encuadra solo para mostrar todos los puntos.
  - Los marcadores que **quedan fuera de la vista** (al hacer zoom o mover el mapa) se muestran en el **margen del mapa**, con su número, color e ícono, hasta que vuelven a caber; al tocarlos, el mapa se centra en el marcador real y abre su ficha.
  - El **marcador 6 de Río (Cristo Redentor)** usa un ícono propio (`assets/cristo-redentor.png`) con el borde blanco, el fondo rojo y la insignia «$» de los lugares de pago; si la imagen no carga, vuelve a mostrarse el número.
  - La atribución del mapa de fondo se muestra como «© CARTO © OpenStreetMap».
  - Si el mapa de fondo no carga, los puntos y la lista siguen funcionando.

### 3.8 🗓️ Itinerario

- **Plan de 9 días** pensado por cercanía: **Río (10, 11 y 12/11)**, **día de mudanza (13/11)**, **Búzios (14 a 17/11)** y **día de regreso (18/11)**.
- **Vista general** con una tarjeta por día (ciudad en color, fecha, tema y costo estimado); al tocar una se abre el detalle. Si el viaje está en curso, se abre el día de hoy.
- **Línea de tiempo** con horario, tipo de actividad (atracción, comer y beber, traslado, descanso y salida nocturna, cada una con su color), descripción, **costo por persona** en R$, **cómo moverse**, duración y enlace a Google Maps. Los ítems opcionales se marcan como tales.
- **Lugares pensados para jóvenes de 20 a 30 años** en lugar de bares clásicos: por ejemplo, la Rua Arnaldo Quintela y la Cobal do Humaitá en Río, y Celestinnas, Chez Michou, Anexo Bar y el club Privilège en Búzios.
- **Mapa del día** con las paradas **numeradas en orden cronológico** (los mismos números de la línea de tiempo), línea punteada del recorrido y ventana emergente con el detalle de cada parada; un botón abre el recorrido en Google Maps.
- **Plan B si llueve** y **tips** por día, además del ritmo, el alojamiento y el transporte.
- **Totales** por día y del plan completo en R$ y en US$ (≈ R$ 4,9 por dólar), sin vuelo, hotel, desayuno ni traslados del paquete: ≈ R$ 2.295 a 3.861 por persona.
- Sección final **«Cómo moverse y qué reservar»** y avisos de que precios y horarios son de referencia.

### 3.9 🗣️ Frases

- Mini-diccionario de **frases útiles en portugués** (saludo, pedir la cuenta, preguntar el precio, comprar bebida, etc.).
- Cada frase se puede **editar** y reproducir con la **Web Speech API** (síntesis de voz `pt-BR` a velocidad 0,9).

### 3.10 📄 Documentos

- **Adjuntar PDF** (arrastrar y soltar o seleccionar): quedan guardados en el navegador (IndexedDB), con opciones para abrir, descargar y quitar.
- **Agregar enlaces** (por ejemplo, de Google Drive) como alternativa, sin duplicar archivos.
- **Categorías con color**: vuelos e itinerario, comprobantes de pago, alojamiento y traslados, asistencia médica y otros (editables luego de cargar).
- Resumen de cantidad y peso total, y avisos claros cuando el navegador no permite guardar archivos de forma permanente.

### 3.11 💱 Cotizaciones

- **Cotización del real al pagar por PIX** según cada app (Cocos, ARQ, Ripio, Astropay, Wayni, Global66, Personal Pay, Mercado Pago, Fiwind, P2P.me, Caipi, Decrypto, Lemon, Belo, Prex y otras), con datos de **ComparaPix**.
- Ordenadas de la más barata a la más cara, con la mejor resaltada, la **diferencia porcentual** contra ella y etiquetas de **Comisiones**, **USDT** y **Dato viejo**.
- Selector **ARS / USD-USDT** y referencia **fuera de PIX** (tarjeta en pesos y tarjeta con resumen cancelado en dólares).
- **Conversor rápido BRL ⇄ moneda seleccionada** (rediseñado en la v11.3.1) que usa la mejor cotización de la tabla; la etiqueta del campo cambia entre *Pesos (AR$)* y *USD / USDT* según el selector.
- El botón **«Ver en ComparaPix»** queda alineado junto a «Actualizar» en escritorio (en celulares se mantiene arriba a la derecha).
- Actualización automática cada ~60 segundos con la pestaña abierta, botón «Actualizar» y **logos** de cada aplicación.
- **Resiliencia**: si falla la conexión se muestra la última cotización guardada o una cotización de referencia embebida, con el **motivo del error** y una opción para **cargar los datos a mano** (pegando la respuesta de la API).

### 3.12 💾 Copia de seguridad (Checklist y Documentos)

- **Guardar copia**: descarga un HTML nuevo con la checklist editada y los enlaces guardados *dentro* del propio archivo.
- **Restaurar copia**: importa esos datos desde un archivo guardado antes (por ejemplo, para pasarlos a otro dispositivo).
- Al abrir un archivo con copia incorporada, la aplicación decide si usarla comparando fechas y contenido; si la copia es más reciente que los cambios locales, **pregunta** antes de reemplazar.
- Los PDF subidos y los gastos **no** se incluyen en la copia (ver [limitaciones](#6-problemas-conocidos-y-deuda-técnica)).

### 3.13 PWA y pie de página

- **App instalable** (manifest, íconos 192/512 px, `display: standalone`) con **Service Worker** para funcionamiento offline del contenido ya visitado.
- **Pie de página personal** con foto, perfil profesional y enlaces de contacto (mail, LinkedIn y GitHub).

---

## 4. Historial de versiones

El proyecto se desarrolló de forma iterativa entre el **12/10/2026 y el 16/10/2026** (hora de Argentina), con **26 commits** en la rama `main`. Las versiones v1.0.0 a v11.3.0 son del 12/10 (la tabla indica solo la hora); las siguientes indican día y hora. Cada commit corresponde a una versión (`Brasil 2026 (vX.Y.Z)`).

### Resumen

| Versión | Hora | Commit | Cambio principal |
|---|---|---|---|
| **v1.0.0** | 17:27 | `c4671d0` | Primera versión: guía estática de 5 secciones |
| **v2.0.0** | 17:33 | `94d97f2` | Cuenta regresiva, checklist editable y pestaña Documentos |
| **v3.0.0** | 17:34 | `d43aa02` | Enlaces de Drive y copia de seguridad exportable/importable |
| **v4.0.0** | 17:36 | `23f7f75` | Pestaña Cotizaciones (ComparaPix) |
| **v5.0.0** | 17:37 | `506b554` | Diagnóstico y carga manual de cotizaciones; cambio de pestaña sin saltar |
| **v5.1.0** | 17:42 | `4f1c5af` | Proxy CORS propio (Cloudflare Workers) |
| **v6.0.0** | 17:45 | `28e3a40` | Clima en tiempo real (OpenWeatherMap) |
| **v7.0.0** | 17:47 | `1e27f83` | Pestaña Frases con Web Speech API |
| **v7.1.0** | 17:50 | `4736e3c` | Ancho completo en encabezados de sección |
| **v8.0.0** | 17:52 | `a411f4c` | Pestaña Control de gastos diarios |
| **v8.0.1** | 17:56 | `a09d955` | Ajuste de tamaño de letra del total de gastos |
| **v8.1.0** | 17:59 | `e5923a5` | Filtros y edición de gastos |
| **v8.2.0** | 18:01 | `0a7e0d7` | Mapas de Google Maps de los alojamientos |
| **v9.0.0** | 18:04 | `2572087` | Barra de copia visible solo en Checklist y Documentos |
| **v10.0.0** | 18:11 | `4c5aea6` | Deploy como PWA, íconos, logos de apps y ajustes visuales |
| **v11.0.0** | 20:08 | `4a8b4d3` | Mapas de puntos de interés con marcadores personalizados |
| **v11.1.0** | 20:25 | `62a7a41` | Alojamientos incluidos en los mapas |
| **v11.2.0** | 22:06 | `1ca0049` | Conversor de moneda y scroll horizontal de secciones |
| **v11.3.0** | 22:43 | `1e42583` | Pie de página personal con datos de contacto |
| **v11.3.1** | 13/10 · 01:42 | `af472ee` | Ajustes visuales del conversor, etiqueta de moneda, logos faltantes y README |
| **v12.0.0** | 15/10 · 00:16 | `15648b5` | Nueva pestaña Itinerario y botón de ComparaPix alineado |
| **v12.0.1** | 15/10 · 00:44 | `3335a7d` | Correcciones de fuentes y logo de Satoshi Tango |
| **v12.1.0** | 15/10 · 11:31 | `0b790cf` | Itinerario con lugares para jóvenes y mapa del recorrido |
| **v12.1.1** | 15/10 · 22:13 | `8c3e1d0` | Cambios en la visualización de los mapas |
| **v12.1.2** | 16/10 · 22:30 | `7e73351` | README, marcador personalizado del Cristo Redentor y EdgeMarker |
| **v12.1.3** | 16/10 · pendiente | _(sin commit)_ | Corrección de las ubicaciones de Búzios en los mapas |

### Detalle por versión

#### v1.0.0 — Primera versión
- Página HTML estática de **823 líneas** con diseño propio: encabezado con datos del viaje, barra de pestañas y cinco secciones: **Alojamiento, Clima y ropa, Checklist, Presupuesto y Turismo**.
- Checklist con ítems fijos tildables y progreso persistido en `localStorage`.
- Tablas de precios, niveles de gasto, medios de pago y tarjetas de lugares con etiquetas Gratis / Pago.

#### v2.0.0 — Cuenta regresiva, checklist editable y Documentos (+510 / −46 líneas)
- **Cuenta regresiva** al día de salida en el encabezado.
- **Checklist editable**: botón de modo edición para agregar, modificar y quitar ítems; nuevo modelo de datos con identificadores estables y migración del progreso previo.
- **Nueva pestaña Documentos**: carga de PDF por arrastrar y soltar, almacenados en **IndexedDB**; categorías con color; abrir, descargar y quitar.

#### v3.0.0 — Enlaces y copia de seguridad
- Documentos admite **enlaces** además de archivos locales.
- **Guardar / Restaurar copia**: exportación de un HTML con los datos embebidos y validación/normalización de los datos importados.
- Resolución de conflictos entre la copia del archivo y los datos del navegador mediante marca de tiempo.

#### v4.0.0 — Cotizaciones del real por PIX
- Nueva pestaña **Cotizaciones** con tabla ordenada, selector ARS / USD-USDT, referencia fuera de PIX, caché local y *snapshot* embebido de respaldo.

#### v5.0.0 — Robustez de cotizaciones y navegación
- Aviso con el **motivo del error** y caja de **carga manual** de datos.
- Consulta con *timeout* propio (sin `AbortController`).
- Uso de un proxy CORS público (`corsproxy.io`).
- `keepTabsInView`: al cambiar de pestaña ya no se vuelve al inicio de la página.

#### v5.1.0 — Proxy CORS propio
- Se reemplaza el proxy público por un **Cloudflare Worker propio** (`proxy-comparapix…workers.dev`) para consultar la API de ComparaPix.

#### v6.0.0 — Clima en tiempo real
- Integración con **OpenWeatherMap**: temperatura actual, mínima y máxima, humedad y descripción con emoji para Copacabana y Tartaruga; se carga al abrir la pestaña y una sola vez.

#### v7.0.0 — Frases con voz
- Nueva pestaña **Frases** con frases útiles en portugués, editables, y reproducción con **Web Speech API** (`pt-BR`, velocidad 0,9).

#### v7.1.0 — Ancho de secciones
- Los encabezados de sección pasan de `max-width: 640px` a `100%`.

#### v8.0.0 — Control de gastos diarios
- Nueva pestaña **Gastos**: gráfico de dona con `conic-gradient`, total en R$, leyenda por categoría, categorías administrables, alta de gastos y modo edición, con persistencia en `localStorage`.

#### v8.0.1 — Ajuste visual
- El tamaño de la letra del total de gastos baja de `1.4rem` a `1.2rem`.

#### v8.1.0 — Filtros y edición de gastos
- Campo de **fecha** en cada gasto, **filtros** por texto y categoría, orden por fecha descendente y **edición en línea** (guardar / cancelar).

#### v8.2.0 — Mapas de alojamientos
- Mapas de Google Maps incrustados (`iframe`) en las fichas de los dos alojamientos.

#### v9.0.0 — Barra de copia contextual
- La barra de «Guardar / Restaurar copia» solo se muestra en *Checklist* y *Documentos*.

#### v10.0.0 — Deploy como PWA y ajustes visuales
- **PWA**: `manifest.json`, `sw.js`, íconos 192/512, `favicon` y `theme-color`.
- **Logos** de las aplicaciones de la tabla de cotizaciones (carpeta `assets/logos`).
- Ajustes visuales: tablas más compactas, **scroll horizontal** de tablas en celulares, alineación de encabezados con botones.
- Registro del Service Worker al cargar la página.

#### v11.0.0 — Mapas de puntos de interés
- **Un mapa Leaflet por destino** en la pestaña Turismo con marcadores personalizados: **círculos** (Río) y **rombos** (Búzios), **verde** para lugares gratuitos y **rojo con «$»** para los de pago.
- Fichas emergentes, lista de puntos con enlaces a Google Maps, bloqueo táctil del mapa, *fallback* si no carga el mapa de fondo y limpieza de los mapas al exportar la copia.
- **Leaflet 1.9.4 incluido dentro del HTML** (sin dependencia de CDN).
- Se corrige la descripción del *Parque Garota de Ipanema* (queda frente al Arpoador, no junto al hotel).

#### v11.1.0 — Alojamientos en el mapa
- Nuevo tipo de marcador **«Alojamiento»** (🏠, azul oscuro) para el Hotel Canadá y la Pousada Brisas.

#### v11.2.0 — Conversor y scroll de secciones
- **Conversor rápido BRL ⇄ ARS** en Cotizaciones, basado en la mejor cotización de la tabla.
- La barra de pestañas se desplaza **arrastrando** con el mouse y muestra una barra de scroll en PC.
- Ajuste de tamaño del selector ARS / USD-USDT.

#### v11.3.0 — Pie de página personal
- Nuevo *footer* con foto, perfil profesional, enlaces de contacto (mail, LinkedIn, GitHub) y aviso de derechos de autor.

#### v11.3.1 — Ajustes visuales, logos faltantes y README
- **Calculadora de monedas rediseñada**: contenedor en fila con encabezado azul oscuro y área gris, campos con tipografía propia, ícono de intercambio y versión apilada en celulares; el título pasa a «Calculadora».
- La etiqueta del campo de origen **cambia según el selector** de moneda: «AR Pesos (AR$)» con ARS y «USD / USDT» con USD.
- Se suben los **6 logos que faltaban** (Binance, Peanut, Takenos, Vesseo, Wallbit y Yodl Pay).
- Se agrega el `README.md` al repositorio.

#### v12.0.0 — Itinerario y botón de ComparaPix
- Nueva pestaña **🗓️ Itinerario** con el plan de 9 días: vista general por tarjetas, línea de tiempo con horarios, tipos de actividad con color, costos por persona, cómo moverse, plan B si llueve, tips y totales estimados en R$ y US$.
- Sección **«Cómo moverse y qué reservar»** con avisos de precios y horarios de referencia.
- El botón **«Ver en ComparaPix»** se alinea junto a «Actualizar» en escritorio.
- La copia exportada limpia el contenido generado del itinerario.

#### v12.0.1 — Correcciones de fuentes y logos
- Tamaños de fuente más chicos en la zona de carga de PDF, los nombres de documentos y el título del formulario de enlaces.
- La etiqueta del conversor pasa a «Pesos (AR$)».
- Se agrega el logo y el nombre de **Satoshi Tango** (`assets/logos/satoshi-tango.png`).

#### v12.1.0 — Itinerario para jóvenes y mapa del recorrido
- El itinerario se ajusta a un público de **20 a 30 años**: bares y restaurantes clásicos se reemplazan por opciones de ambiente joven, y se suman actividades como el Museu da Chácara do Céu (gratis los miércoles) y una tarde en Geribá.
- **Mapa del día** con Leaflet: paradas **numeradas en orden cronológico**, línea punteada del recorrido, un solo marcador con varios números cuando se vuelve al mismo lugar, ventana emergente por parada y botón para abrir el recorrido en Google Maps (hasta 10 puntos).
- Los números de parada también aparecen en la línea de tiempo; avisos para los días en que el mapa no dibuja un tramo (viaje Río → Búzios, traslado al aeropuerto y Arraial do Cabo).
- Se corrige la ubicación de Azeda y Azedinha en el mapa de Turismo.

#### v12.1.1 — Visualización de mapas
- **Mapas de Turismo**: fondo CARTO Voyager con API key y OpenStreetMap como respaldo, **escala métrica**, **marcadores de alojamiento con efecto de pulso** y encuadre automático más ajustado (`padding` 10 y `maxZoom` 17), con el mismo criterio para Río y Búzios.
- **Mapa del Itinerario**: se reemplaza CARTO (que pasó a exigir clave) por **OpenStreetMap con Esri como respaldo**.
- Se restauran los tamaños de fuente de la zona de carga de PDF, los nombres de documentos y el formulario de enlaces, y el título de la zona de carga se acorta a «Subir PDF».
- Se deja en el código un comentario que apunta a una conversación externa para comparar los tres mapas (ver problemas conocidos).

#### v12.1.2 — README, marcador del Cristo Redentor y EdgeMarker
- Se actualiza el `README.md` con los cambios desde la v11.3.0 hasta la v12.1.1.
- **Leaflet.EdgeMarker** (MIT) incluido dentro del HTML: los marcadores de los mapas de Turismo que no entran en la vista se muestran en el **margen del mapa** hasta que caben; cada uno conserva su número, color, imagen e insignia, y al tocarlo centra el mapa y abre su ficha.
- El **marcador 6 de Río (Cristo Redentor)** pasa a usar la imagen `assets/cristo-redentor.png` dentro del círculo, manteniendo el borde blanco, el fondo rojo y la insignia «$»; también se usa en la lista de puntos y, si la imagen falla, vuelve el número.
- La atribución del mapa de fondo de Turismo cambia de orden: «© CARTO © OpenStreetMap».
- Se agrega el archivo `assets/cristo-redentor.png`.

#### v12.1.3 — Corrección de las ubicaciones de Búzios
- **Pousada Brisas de Búzios** movida unos **720 m al sur** (de `-22.7565, -41.8973` a `-22.7630, -41.8970`): coincide con las coordenadas publicadas por Booking y otros portales y con el pin de Google Maps. Antes quedaba en una zona de monte, lejos del camino.
- **Playa Tartaruga** y **Playa Ferradura** se recalibran (≈ 310 y 440 m) tomando como referencia la captura de Google Maps de la pousada.
- **Rua das Pedras**, **Orla Bardot** (estatua de Brigitte Bardot), **muelle / Praia da Armação**, **O Barco**, **Privilège** y **Porto da Barra** se reubican (≈ 550 a 940 m) con coordenadas publicadas por Waze y por un alojamiento local, además de la posición relativa en Google Maps.
- Los cambios se aplican en los dos mapas que usan estos puntos: **Turismo** e **Itinerario** (que comparten las mismas ubicaciones). Azeda y Azedinha, João Fernandes y Arraial do Cabo se mantienen.

---

## 5. Arquitectura y consideraciones técnicas

### 5.1 Stack

| Capa | Tecnología |
|---|---|
| Estructura | HTML5 semántico (`header`, `nav`, `main`, `section`, `footer`) |
| Estilos | CSS3 con variables personalizadas, Grid, Flexbox, `conic-gradient`, *media queries* |
| Lógica | JavaScript vanilla (ES2017+: `async/await`, módulos por secciones dentro de un mismo `<script>`) |
| Mapas | [Leaflet](https://leafletjs.com/) 1.9.4 (BSD-2-Clause) y [Leaflet.EdgeMarker](https://github.com/ubergesundheit/Leaflet.EdgeMarker) (MIT), incluidos en línea |
| Tipografías | Google Fonts: Fraunces, Manrope y Space Mono |
| PWA | Web App Manifest + Service Worker |
| Hosting | Cloudflare Workers (sitio estático); el repositorio está en GitHub |

No hay *bundler*, gestor de paquetes, pruebas automatizadas ni integración continua.

### 5.2 Estructura del repositorio

```text
brasil-2026/
├── index.html          # Toda la aplicación (HTML + CSS + JS + Leaflet) ≈ 396 KB, ~5.050 líneas
├── manifest.json       # Web App Manifest (nombre, colores, íconos)
├── sw.js               # Service Worker (caché y modo offline)
├── favicon.ico         # Copia PNG de 512 px del ícono
├── README.md           # Esta documentación
└── assets/
    ├── icon-192.png / icon-512.png   # Íconos de la PWA
    ├── MiFoto.png                    # Foto del pie de página
    ├── cristo-redentor.png           # Ícono personalizado del marcador del Cristo Redentor
    ├── logo-brasil-2026.jfif         # Logo (sin referencias en el código)
    ├── logo-brasil-2026-modified.png # Logo (sin referencias en el código)
    └── logos/                        # 22 logos de apps de la tabla de cotizaciones
```

### 5.3 Organización interna de `index.html`

El archivo sigue un orden fijo:

1. **`<head>`**: metadatos, `manifest`, favicon, `theme-color`, Google Fonts, hoja de estilos propia y CSS de Leaflet.
2. **`<body>`**: encabezado con cuenta regresiva → barra de pestañas → `<main>` con **un `<section class="panel">` por pestaña** → barra de copia → pie de página.
3. **Scripts**: Leaflet en línea → bloque JSON `#embeddedData` (copia de seguridad) → script principal → script de registro del Service Worker.

El script principal está dividido en bloques comentados:

| Bloque | Responsabilidad |
|---|---|
| Pestañas | Cambio de panel, `keepTabsInView`, ocultar/mostrar barra de copia |
| Datos compartidos y estado | Claves de almacenamiento, normalización y validación de copias, estado de checklist y enlaces |
| Checklist (editable) | Render, modo edición, progreso |
| Cuenta regresiva | Temporizador por segundo (`setInterval`) |
| Documentos | IndexedDB (PDF), enlaces, categorías |
| Copia: guardar / restaurar | Exportación e importación del HTML |
| Cotizaciones | Consulta, caché, snapshot, tabla, referencia, conversor |
| Clima en tiempo real | OpenWeatherMap |
| Diccionario / Web Speech | Frases y síntesis de voz |
| Control de gastos | CRUD de gastos y categorías, gráfico, filtros |
| Mapas de Turismo | Leaflet, marcadores (con imagen opcional), listas, bloqueo táctil, escala, marcadores de alojamiento y marcadores en el margen (EdgeMarker) |
| Itinerario | Datos de los 9 días (`DAYS`), línea de tiempo, totales, mapa numerado y enlace de recorrido |

### 5.3.1 Diagrama de componentes

```mermaid
flowchart LR
  subgraph Cliente["Navegador (PWA)"]
    UI["index.html<br/>SPA de 10 pestañas"]
    LS[("localStorage")]
    IDB[("IndexedDB<br/>PDF")]
    SW["Service Worker<br/>sw.js"]
  end
  UI --> LS
  UI --> IDB
  UI <--> SW
  UI -->|clima| OWM["OpenWeatherMap"]
  UI -->|cotizaciones| WK["Cloudflare Worker<br/>proxy CORS"] --> CP["api.comparapix.ar"]
  UI -->|mapas| TILES["Tiles CARTO / OSM / Esri"]
  UI -->|iframes| GM["Google Maps (embed y enlaces)"]
```

### 5.4 Navegación (SPA sin enrutador)

- Cada pestaña es un botón con `data-tab="x"` que activa el panel `#panel-x` (clase `.active`); no hay enrutador ni cambios de URL.
- Algunas pestañas cargan datos **de forma diferida** al activarse (clima, cotizaciones, mapas), evitando llamadas innecesarias al iniciar.
- `keepTabsInView` calcula dónde empieza a quedar fija la barra para no devolver al usuario al inicio.

### 5.5 Persistencia de datos

| Dato | Almacenamiento | Clave / nombre |
|---|---|---|
| Checklist (formato actual) | `localStorage` | `rioBuziosChecklist2026_v2` |
| Checklist (formato original, solo lectura para migrar) | `localStorage` | `rioBuziosChecklist2026` |
| Enlaces de documentos | `localStorage` | `rioBuziosLinks2026` |
| Marca de tiempo de la última modificación local | `localStorage` | `rioBuziosMeta2026` |
| Caché de cotizaciones | `localStorage` | `rioBuziosQuotes2026` |
| Gastos y categorías | `localStorage` | `rioBuziosGastos2026` |
| PDF adjuntos | `IndexedDB` | base `rioBuziosDocs2026`, almacén `docs` |
| Recursos offline | Cache Storage | `rio-buzios-cache-v1` |

Todas las escrituras están protegidas con `try/catch`: si el navegador bloquea el almacenamiento, la aplicación sigue funcionando sin persistencia y, en el caso de los PDF, lo informa en pantalla.

### 5.6 Copia de seguridad (exportar / importar)

Un HTML estático no puede reescribirse a sí mismo, por lo que la copia se resuelve así:

1. **Exportar**: se clona el documento (`document.documentElement.cloneNode(true)`), se **limpia** todo lo que el script vuelve a generar (listas, mapas, tablas, estado de pestañas) y se inyecta un JSON con `{ v, savedAt, checklist, links }` en `<script type="application/json" id="embeddedData">` (escapando `<`). El resultado se descarga como `rio-buzios-2026-copia-AAAA-MM-DD.html`.
2. **Abrir un archivo con copia**: `applyEmbedded()` normaliza los datos (límites de tamaño, URLs `http/https`, categorías válidas) y compara el contenido:
   - sin cambios locales → usa la copia en silencio;
   - copia más reciente que lo local → **pregunta** al usuario;
   - cambios locales más nuevos → conserva lo local.
3. **Restaurar**: lee el `#embeddedData` de un archivo elegido por el usuario y reemplaza checklist y enlaces tras confirmar.

### 5.7 Integraciones externas

| Servicio | Uso | Observaciones |
|---|---|---|
| **OpenWeatherMap** (`/data/2.5/weather`) | Clima actual en Copacabana y Tartaruga | Consulta directa desde el navegador con *API key* |
| **ComparaPix** (`api.comparapix.ar/quotes`) | Cotizaciones PIX | Se consulta mediante un **Cloudflare Worker propio** que resuelve CORS |
| **Google Maps** | `iframe` de alojamientos, enlaces de búsqueda por nombre y enlaces de recorrido (`/maps/dir`) | Sin API key (modo *embed* y enlaces) |
| **CARTO** (Voyager) | Mapa de fondo de los mapas de Turismo | Requiere *API key* (incluida en la URL de los tiles); si falla, se usa OpenStreetMap |
| **OpenStreetMap / Esri** | Mapa de fondo del Itinerario (y respaldo en Turismo) | OpenStreetMap primero y, ante errores, Esri World Street Map; sin API key |
| **Web Speech API** | Pronunciación de frases | Depende de las voces `pt-BR` instaladas en el dispositivo |
| **Google Fonts** | Tipografías | Requiere conexión la primera vez |

### 5.8 Cotizaciones: flujo y tolerancia a fallos

```mermaid
flowchart TD
  A[Abrir pestaña Cotizaciones] --> B{Consulta al proxy<br/>timeout 10 s}
  B -- OK --> C[Datos en vivo<br/>y guardado en caché local]
  B -- Error --> D{¿Hay caché local?}
  D -- Sí --> E[Última cotización guardada]
  D -- No --> F[Snapshot embebido en el HTML]
  E --> G[Aviso en rojo + motivo del error<br/>+ carga manual]
  F --> G
```

- La respuesta de la API se **valida** (estructura, números positivos) y se descartan filas inválidas.
- El *timeout* se implementa con `Promise` propio y **sin `AbortController`**: algunas vistas previas reenvían `fetch` con `postMessage` y no pueden clonar la señal de cancelación.
- Los nombres de apps se renderizan con `textContent` (no `innerHTML`), por tratarse de contenido de terceros.
- La tabla usa el campo `buy` (precio *para pagar*) de cada app marcada como PIX (`isPix`), separa USD de USDT y marca datos viejos (`stale`).

### 5.8.1 Mapas de Turismo

- Los puntos viven en una constante `POI` (nombre, coordenadas, costo, descripción, consulta de Google Maps), de donde salen **marcadores, popups y listas**.
- Marcadores creados con `L.divIcon` (HTML/CSS): forma por ciudad, color por costo y número visible; la insignia «$» refuerza el color para accesibilidad.
- Inicialización **diferida** al abrir Turismo (los contenedores ocultos tienen tamaño 0) y `invalidateSize()` posterior.
- Los contenedores usan `isolation: isolate` para que los controles de Leaflet no queden por encima de la barra fija.
- Los alojamientos se marcan con `hotel: true` (marcador 🏠 con animación de pulso) y cada mapa incluye `L.control.scale` en metros.
- El encuadre inicial usa `fitBounds` con `padding` 10 y `maxZoom` 17 para ambos destinos.
- **Marcadores en el margen**: se crea una instancia de `L.edgeMarker` por cada marcador (con `layerGroup` de un solo elemento y `rotateIcons: false`) para que cada uno conserve su propio ícono; se crean **después** de `fitBounds` y su `onClick` se sobrescribe para centrar el mapa y abrir el popup. El plugin está envuelto en un `if (typeof L !== 'undefined')` para no fallar si Leaflet no carga.
- **Marcador con imagen**: un punto del arreglo `POI` puede llevar `img` (por ejemplo `assets/cristo-redentor.png`); `poiIconHtml()` agrega una etiqueta `<img>` dentro del círculo (clase `has-img`, ícono recortado en círculo sobre el fondo rojo) y un listener de `error` en captura la quita y vuelve a mostrar el número si el archivo falta.
- Las coordenadas son **aproximadas**: las ubicaciones de Búzios se corrigieron en la v12.1.3 con coordenadas publicadas (Booking, Waze, OpenStreetMap) y una captura de Google Maps, y los enlaces ↗ abren el lugar por nombre en Google Maps para obtener la ubicación exacta.

### 5.8.2 Itinerario: datos y mapa del recorrido

- Los 9 días viven en la constante `DAYS` (fecha ISO, ciudad, ritmo, alojamiento, transporte, ítems, plan B y tips). Cada ítem define hora, tipo (`sight`, `food`, `move`, `rest`, `night`), título, descripción, costo por persona `[mín, máx]` en R$, si es opcional o está incluido, cómo llegar, duración, consulta de Google Maps (`q`) y, opcionalmente, coordenadas (`ll`).
- Los totales por día y del viaje se calculan en JavaScript: los ítems opcionales suman solo al máximo y la conversión a dólares usa una constante (`RATE`, ≈ R$ 4,9 por US$).
- **Paradas del mapa**: `computeStops()` toma los ítems con coordenadas en orden cronológico y los consecutivos en el mismo punto comparten número. Se dibuja una línea punteada entre paradas (recta y aproximada) y los marcadores se agrupan por ubicación (por ejemplo, «1·5·8» para el hotel).
- **Enlace de recorrido**: `routeUrl()` arma una URL `google.com/maps/dir` con origen, destino y puntos intermedios; como Google admite hasta 10 puntos, se omiten paradas de descanso intermedias cuando hace falta.
- El mapa se crea **una sola vez** y se mueve dentro de la vista del día; su inicialización es diferida (al abrir la pestaña) y usa el mismo bloqueo táctil que los mapas de Turismo.
- Los textos se construyen con `textContent` y los días sin coordenadas en un tramo (viaje entre ciudades, aeropuerto) muestran un aviso en lugar de dibujarlo.

### 5.9 PWA y modo offline

- `manifest.json`: nombre, `short_name`, `start_url: ./index.html`, `display: standalone`, colores de tema y fondo, íconos 192 y 512.
- `sw.js` (`CACHE_NAME = rio-buzios-cache-v1`):
  - **Instalación**: precachea `index.html` y `manifest.json`; usa `skipWaiting`.
  - **Activación**: elimina cachés con otro nombre.
  - **Estrategia por tipo de recurso**: *Cache First* para `/assets/` y *Network First con respaldo en caché* para todo lo demás.
- Los mapas de fondo (tiles) no se precargan, por lo que el mapa requiere conexión; el resto de la guía funciona offline una vez visitada.

### 5.10 Diseño, accesibilidad y responsividad

- Diseño *mobile-first*: grillas que colapsan, tablas con scroll horizontal y tipografías fluidas (`clamp`).
- Paleta definida con **variables CSS** (`--navy`, `--ocean`, `--coral`, `--jungle`, `--sun`, `--poi-free`, `--poi-paid`, etc.).
- Atributos ARIA en componentes clave (`role="timer"`, `role="status"`, `aria-pressed`, `aria-label`), foco visible y soporte de `prefers-reduced-motion`.
- La información crítica no depende solo del color (insignia «$», etiquetas de texto «Gratis» / «Pago»).

### 5.11 Seguridad y privacidad

- **Los datos personales permanecen en el dispositivo**: PDF, gastos, checklist y enlaces no se envían a ningún servidor propio. No hay analítica ni seguimiento.
- Las solicitudes a terceros (clima, mapas, cotizaciones, fuentes) exponen la IP y el navegador a esos servicios, como en cualquier página web.
- La copia exportada **contiene la checklist y los enlaces**: no conviene publicarla en un sitio abierto.
- El HTML contiene **API keys visibles en el cliente** (OpenWeatherMap y, desde la v12.1.1, CARTO); al ser un repositorio público, cualquiera puede leerlas (ver problemas conocidos).
- Se validan y limitan los datos importados (cantidad de secciones, ítems y enlaces; solo URLs `http/https`) y los enlaces externos usan `rel="noopener noreferrer"`.

### 5.12 Rendimiento y peso

- `index.html` pesa ≈ **396 KB**, de los cuales ≈ **172 KB** son Leaflet y Leaflet.EdgeMarker (JS + CSS) incluidos en línea.
- Mayor peso de la carpeta `assets`: `MiFoto.png` (≈ 7,7 MB), `logo-brasil-2026-modified.png` (≈ 2,9 MB) y `logo-brasil-2026.jfif` (≈ 2,2 MB); estos dos últimos no se usan en el código.
- Carga diferida de datos (clima, cotizaciones, mapas) y caché de assets en el Service Worker.

---

## 6. Problemas conocidos y deuda técnica

| # | Tema | Detalle | Sugerencia |
|---|---|---|---|
| 1 | 🔑 **API keys expuestas** | El HTML de este repositorio público contiene una API key de OpenWeatherMap y, desde la v12.1.1, una de CARTO (en la URL de los tiles). | Revocarlas o regenerarlas, restringirlas por dominio si el proveedor lo permite o moverlas a un Worker, y evitar volver a subirlas. |
| 2 | 🧮 **Conversor y símbolo de moneda** | Con USD/USDT la etiqueta cambia a «USD / USDT» y la conversión usa la tasa en dólares, pero el encabezado «Cotización: $…» sigue mostrando el valor con prefijo `$` y 2 decimales (≈ 0,21). | Mostrar prefijo y decimales según la moneda seleccionada. |
| 3 | 🖼️ **Nombres de apps** | Los logos faltantes se resolvieron (v11.3.1 y v12.0.1), pero `satoshitango` quedó fuera de `APP_NAMES` en la v12.1.0 y se muestra como «Satoshitango»; sigue sin haber `onerror` en las imágenes. | Restaurar el nombre y caer a la letra inicial con `onerror`. |
| 4 | 🧩 **Gastos sin escapar** | El módulo de gastos interpola descripción y categoría dentro de `innerHTML` y usa `onclick` en línea; caracteres como `"` o `<` pueden romper la interfaz. Los datos son locales (impacto bajo). | Usar `textContent` / `createElement` y `addEventListener`. |
| 5 | 💾 **Alcance de la copia** | La copia incluye checklist y enlaces, pero no gastos, PDF ni caché de cotizaciones. | Sumar `gastos` al esquema de la copia (versionando `v`). |
| 6 | 🗂️ **Assets pesados / sin uso** | `MiFoto.png` (≈ 7,7 MB) se carga en el pie; dos logos (≈ 5 MB) no se referencian; `favicon.ico` es un PNG renombrado. | Optimizar o redimensionar imágenes y eliminar archivos sin uso. |
| 7 | 🔧 **Service Worker básico** | Nombre de caché fijo (sin versión), no distingue métodos ni orígenes y cachea también respuestas de APIs de terceros. No se modifica desde la v10.0.0. | Versionar el caché, limitar a `GET` del mismo origen y excluir APIs. |
| 8 | ☁️ **Proxy fuera del repo** | El código del Cloudflare Worker de cotizaciones no está versionado en el repositorio. | Incluirlo (por ejemplo en `/worker`) y documentar su despliegue. |
| 9 | 📍 **Coordenadas y recorrido aproximados** | Las ubicaciones de Búzios se corrigieron en la v12.1.3, pero varias siguen siendo estimaciones (Rua das Pedras, Orla Bardot, muelle, O Barco, Privilège, Porto da Barra, Geribá y varios puntos de Río), y la línea del recorrido es recta, no la ruta real. | Copiar las coordenadas exactas de cada punto desde Google Maps (clic derecho sobre el lugar) y, si hace falta, usar un servicio de ruteo. |
| 10 | 🗺️ **Tres implementaciones de mapa** | Alojamiento usa un `iframe` de Google Maps; Turismo usa CARTO con API key y respaldo OpenStreetMap; el Itinerario usa OpenStreetMap con respaldo Esri. El respaldo se activa tras 2 errores de tiles sin ninguna carga previa, por lo que un mapa puede cambiar de proveedor y verse distinto de otro. El código de tiles está duplicado entre `addBaseTiles` y `addTiles`. | Unificar en una sola función de tiles (un único proveedor sin clave) y reutilizarla en ambos mapas. |
| 11 | 🧹 **Comentarios y código muerto** | Hay un comentario con un enlace a una conversación externa de Gemini y un bloque comentado de zoom fijo para Río en `initPoiMap`. | Eliminarlos o pasarlos a la documentación. |
| 12 | 🧪 **Sin pruebas ni CI** | La verificación es manual y el código vive en un único archivo de casi 4.700 líneas. | Separar en módulos y agregar pruebas básicas. |

---

## 7. Ejecución local y despliegue

**Abrir sin servidor** (la mayoría de las funciones andan, salvo el Service Worker y algunas llamadas con restricciones del navegador):

```bash
git clone https://github.com/facuatolosa/brasil-2026.git
cd brasil-2026
# abrir index.html en el navegador
```

**Con servidor local** (recomendado para probar la PWA y el Service Worker, que requieren `localhost` o HTTPS):

```bash
python3 -m http.server 8080
# luego visitar http://localhost:8080
```

**Despliegue**: al ser contenido estático, basta publicar `index.html`, `manifest.json`, `sw.js` y la carpeta `assets/` en cualquier hosting estático (Cloudflare Workers/Pages, GitHub Pages, Netlify, etc.). Para actualizar una versión ya instalada, conviene cambiar `CACHE_NAME` en `sw.js`.

**Adaptar a otro viaje**: editar los textos de las secciones, las fechas de la cuenta regresiva (`new Date(...)` en el bloque *Cuenta regresiva*), las coordenadas del clima, la constante `POI` de los mapas, el array `DAYS` del itinerario y los datos de alojamiento.

---

## 8. Ideas a futuro

- Incorporar los **gastos** a la copia de seguridad y permitir exportarlos a CSV.
- Convertir los gastos de reales a pesos usando la cotización PIX del día.
- Separar el código en archivos (`css/`, `js/`) con un *build* liviano y pruebas.
- Precarga de mapas y mejoras del modo offline.
- Modo oscuro y soporte de varios idiomas.
- Editar el itinerario desde la interfaz y guardarlo en el navegador y en la copia de seguridad.
- Exportar el itinerario a calendario (`.ics`) o PDF.
- Dibujar la ruta real entre paradas con un servicio de ruteo.

---

## 9. Autoría y licencia

Desarrollado por **Facundo Argüello Tolosa**.

- GitHub: [@facuatolosa](https://github.com/facuatolosa)
- LinkedIn: [Facundo Argüello Tolosa](https://www.linkedin.com/in/facundo-arg%c3%bcello-tolosa-153115162/)

El repositorio **no incluye un archivo de licencia**; el pie de la aplicación indica «Todos los derechos reservados». Leaflet se distribuye bajo licencia BSD-2-Clause y conserva su aviso de copyright dentro del archivo. Los datos de cotizaciones pertenecen a [ComparaPix](https://comparapix.ar/) y el mapa base a sus respectivos proveedores (© OpenStreetMap contributors, © CARTO).
