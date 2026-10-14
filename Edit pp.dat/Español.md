# PvZ2 Chino: Guía de Modding - ¿Cómo modificar tu pp.dat?

El archivo pp.dat contiene los progresos del jugador serializados como datos binarios.

> Ten en cuenta que la versión china de PvZ2 cuenta con un sistema antihacking que detecta cambios en los datos y los anula.
Modificar ciertos valores en versiones recientes del juego tiene riesgo de que recibas un baneo permanente en la cuenta (solo se permiten ciertas modificaciones, la guía fue escrita para versiones previas al bannying).

---

En la guía detallo los nodos responsables del Integrity Check para validar que los datos no estén alterados.

Esto aún está en investigación ya que desconozco cómo se generan los hash, puede que sea MD5 con alguna Salt que varía por usuario.

Lograr descubrir cómo funciona los hash de validación implicaría vulnerar el sistema de baneos ya que este se enfoca en la integridad de los datos principalmente.

**NOTA: NO ME HAGO RESPONSABLE DE BLOQUEOS DE CUENTA O PÉRDIDA DE DATOS, EDITA BAJO TU PROPIO RIESGO.**

Una vez dicho esto, sigue estos pasos al pie de la letra.

## Paso #1. Extraer el archivo

Extrae el archivo pp.dat desde: **_/>data>data>com.popcap.pvz2cthdxx>no_backup_** y luego, pásalo a una carpeta donde puedas ubicarlo fácilmente.

`xx = 360, 4399 o cdbk, esto varía según las versiones del juego`

**NOTA: para acceder a dicho directorio es necesario que tu dispositivo esté rooteado.
No olvides además, hacer un backup a tus datos por si algo sale mal.**

## Paso #2. Decodificar el archivo

Los RTONs de la versión china están cifrados, por lo que tendrás que desencriptar el archivo primero y después decodificarlo.

**NOTA: recomiendo usar Sen para eso. Aunque hay otras herramientas, estas vienen con sus limitaciones o están obsoletas.**

Arrastra el archivo al programa y selecciona la **_opción 39 (PopCap RTON Encriptado a JSON)_**

## Paso #3. Descargar el software de edición

A continuación, descarga uno de los siguientes programas:

- Para editar en Windows

```
JSON Editor
Notepad++
```

- Para editar en Android

```
MT Manager
JSON Validator
```

Estos son editores de texto para manejar archivos JSON en diferentes plataformas.

## Paso #4. Modificar valores

Podrás modificar los valores a la cantidad que desees.

Solo procura no excederte de `2,147,483,647` o se volverán negativos debido a un Overflow.

Cabe destacar también que, algunos valores están ofuscados.

Aquí está la descripción de los nodos documentados en el archivo:

### ▶ Cambiar el nombre de usuario

Busca una `n` en el editor, este valor es tu nombre de usuario.

La ventaja de modificarlo es que te permitirá el uso de más caracteres debido a que el juego tiene un límite.

**NOTA: no es recomendable cambiarlo a un nombre exageradamente largo, ya que la UI podría no mostrarlo correctamente.**

### ▶ Editar la cantidad de Monedas

Busca una `c` en el editor.

Este valor está ofuscado con rotaciones de bits.

*__INTEGRITY CHECK: el hash usado para validar el valor es `csign` (en desuso)__*

### ▶ Editar la cantidad de Días completados

Busca `dc` en el editor. Este valor es la cantidad de Días completados en el modo Aventura.

### ▶ Editar los Premios por recarga acumulativa

Busca `urn` en el editor.

Verás una lista de números. Son las IDs asignadas a los premios que has desbloqueado por recargar dinero real.

Antes de la `v1.8.0`, era posible obtener los premios en la Tienda de Joyas según se completaran los objetivos.

La UI de la tienda fue cambiada en versiones recientes, lo que significa que la mayoría de premios no son reclamables. Aún así, algunos valores del nodo siguen funcionando, subrayaré con itálica los IDs que aun funcionan.

Lista de premios:

* *__2 = Duplicador de Monedas__*
* 6 = Boletos diarios para Lotería
* *__10 = Planta aleatoria__*
* *__20 = Botón turbo__*
* 30 = Petacereza

### ▶ Modificar cantidad de yuanes recargados

Busca `newrcc` en el editor.

Este valor está ofuscado con rotaciones de bits.

### ▶ Editar los Premios por Nueva recarga

Busca `ntrrs` en el editor.

Verás una lista de números. Son las IDs asignadas a los premios que has desbloqueado por recargar dinero real (en la nueva interfaz).

**NOTA: cada premio tiene su propia ID, esta coincide con el hito a alcanzar para desbloquear el premio.**

### ▶ Editar la cantidad de Joyas

Busca una `g` en el editor.

Este valor está ofuscado con rotaciones de bits.

Luego le sigue este otro valor: `gg`

No se haya ofuscado y parece ser una especie de validación para saber cuántas Joyas has comprado.

**NOTA: procura no excederte de `100,000` o tus Joyas se revertirán a 0 y tus plantas pasarán a ser de Nivel 1.
Esto se hizo así en algunas versiones del juego como medida para evitar el uso de hacks.**

*__INTEGRITY CHECK: el hash usado para validar el valor es `gs`__*

### ▶ Editar la cantidad de Estrellas

Busca una `s` en el editor.

Este valor está ofuscado con rotaciones de bits.

### ▶ Editar el último nivel jugado

Busca una `l` en el editor. Este string es el nombre del último nivel que jugaste.

**NOTA: cada nivel tiene su propio ID**

### ▶ Editar los Mundos completados

Busca `wmed` en el editor.

Verás una lista de objetos. Son los Mundos que has completado.

La estructura de cada objeto es la siguiente:

◼ `w`: ID del mundo

◼ `e`: objeto con los datos del mundo, se divide en:

- `i`: ID del nivel o evento

- `h`: determina si el Modo dificil se ha completado o no `(1 = completado, 0 = incompleto)`

◼ `r`: determina si el jugador ha recibido llaves para desbloquear el nivel (siempre en `false`, valor en desuso)

*__INTEGRITY CHECK: el hash usado para validar el valor es `wes`__*

**NOTA: cada mundo y evento tiene su propio ID**

### ▶ Editar qué Plantas tienes

Busca una `p` en el editor.

Verás una lista de números. Son las IDs asignadas a las plantas que has desbloqueado.

**NOTA: cada planta tiene su propio ID**

*__INTEGRITY CHECK: el hash usado para validar los datos es `ups`__*

### ▶ Editar la cantidad de Sobres rojos

Busca `rp` en el editor.

Este valor está ofuscado con rotaciones de bits.

*__INTEGRITY CHECK: el hash usado para validar el valor es `rpsign`__*

### ▶ Editar cuáles Mejoras tienes

Busca `gf` en el editor.

Verás una lista de números. Son las IDs asignadas a las mejoras que has desbloqueado.

**NOTA: cada mejora tiene su propio ID**

*__INTEGRITY CHECK: el hash usado para validar los datos es `ugfs` (en desuso)__*

### ▶ Editar qué Narrativas has visto

Busca `ne` en el editor.

Verás una lista de números. Son las IDs asignadas a las narativas que has visto en el Mapa.

**NOTA: cada narrativa tiene su propio ID**

### ▶ Editar que Zombis has avistado

Busca `kz` en el editor.

Verás una lista de números. Son las IDs asignadas a los Zombis que hayas derrotado.

**NOTA: cada zombi tiene su propio ID**

### ▶ Editar la cantidad de Potenciadores

Busca `pr` en el editor.

Verás una lista de objetos. Son los Potenciadores que has desbloqueado.

La estructura de cada objeto es la siguiente:

- `n`: tipo de Potenciador.
- `i`: cantidad de usos.

*__INTEGRITY CHECK: el hash usado para validar los datos es `prs`__*

### ▶ Editar las Piezas para plantas

Busca `ppr` en el editor.

Verás una lista de objetos. Son las plantas y sus respectivos números de Piezas. 

La estructura de cada objeto es la siguiente:

- `pi`: ID de la plantas
- `pc`: cantidad de Piezas

*__INTEGRITY CHECK: el hash usado para validar los datos es `pprs`__*

### ▶ Editar las Piezas para colgantes

Busca `asp` en el editor.

Verás una lista de objetos. Son los Colgantes y sus respectivos números de Piezas.

La estructura de cada objeto es la siguiente:

- `acpt`: nombre del colgante
- `acpc`: cantidad de Piezas

*__INTEGRITY CHECK: el hash usado para validar los datos es `asps`__*

### ▶ Editar los cañones y escudos de Ciudad Aérea

Busca `rcstl` en el editor.

Verás una lista de objetos. Son los cañones y escudos de la Ciudad Aérea.

La estructura de cada objeto es la siguiente:

- `rslwn`: nombre del mundo (siempre será `"skycity"` por default, editarlo no tiene efecto alguno).

- `rslcl`: tipo de cañón `(1 = Básico, 2 = Laser, 3 = Lanzacohetes)`

- `rslbl`: tipo de escudo `(1 = Básico, 2 = Metal, 3 = Oro)`

**NOTA: esta lista tiene un único elemento, agregar más es inecesario, puesto que el único mundo donde funcionan las mejoras es en ese.**

### ▶ Editar la Nivelación de tus plantas

Busca `psla` en el editor.

Verás una lista de objetos. Son las plantas desbloqueadas y su respectiva nivelación.

La estructura de cada objeto es la siguiente:

- `icpi`: ID de la planta
- `icl`: nivel actual

#### 🔶 **CURIOSIDADES:**

1. Algunas plantas no tienen estadísticas para ciertos Niveles por lo que se revertirán sus atributos al Nvl. 1 (ej. Girasol al Nvl. 5 en versiones antiguas)*

2. En versiones anteriores a la `2.0.0`, intentar colocar una planta de Nivel 5 en una partida hacía que el juego se cerrara inesperadamente (debido a que faltaban ciertas propiedades, aunque sí existían gráficos).

3. En versiones recientes, existen gráficos para el Nvl. 6 a 10, intentar consultar una planta en la sección Mejoras crashea porque no hay propiedades.

---

**NOTA: edítalo con precaución.**

*__INTEGRITY CHECK: el hash usado para validar el valor es `psls`__*

### ▶ Editar la Nivelación de los zombis derrotados

Busca `zsla` en el editor.

Verás una lista de objetos. Son los zombis derrotados y su respectiva nivelación.

La estructura de cada objeto es la siguiente:

- `icpi`: ID del zombi
- `icl`: nivel actual

#### 🔶 **CURIOSIDADES:**

1. Los indicadores de nivel actual solo tienen íconos del 1 al 5, si el valor difiere tanto el fondo del zombi como la carta no mostrará la nivelación apropiadamente en el Almanaque.

2. Si el valor se establece en 5, la carta mostrará 4 en su lugar

---

**NOTA: edítalo con precaución.**

### ▶ Editar datos de los Retos diarios

Busca `ainfo` en el editor. Verás un objeto con la siguiente estructura:

- `rAt`: última fecha en la que se accedió al evento `(tipo: UnixTimestamp)`
- `ytl`: cantidad de boletos para el evento Locuras de yeti
- `tcylc`: cantidad de boletos para el evento Dios de las Riquezas
- `tgclc`: cantidad de boletos para el evento Crisis Zombistein
- `tdilc`: cantidad de boletos para el evento Invasión explosiva
- `yetiCountPerDayVersion`: versión del objeto (siempre 0, con bits rotation)
- `yetiCountPerDay`: cantidad de yetis a spawmear en el evento
- `acl`: record con el mejor tiempo (no estoy seguro)
- `tyeti`: determina si Locuras de yeti está activado o no
- `sptlc`: record con la puntuación más alta (no estoy seguro)

### ▶ Editar cuáles Atuendos tienes

Busca `ulokpa` en el editor.

Verás una lista de objetos. Son los Atuendos que has desbloqueado.

La estructura de cada objeto es la siguiente:

- `paipid`: ID del atuendo

- `avt`: tipo de atuendo (`"normal"` por default)

- `vaulok`: array de booleanos. El valor determina si el atuendo se ha desbloqueado o no `(1 para true, 0 para false)`

*__INTEGRITY CHECK: el hash usado para validar los datos es `uas`__*

### ▶ Editar las Piezas para atuendos

Busca `lpapi` en el editor.

Verás una lista de objetos. Son los Atuendos y sus respectivos números de Piezas. 

La estructura de cada objeto es la siguiente:

- `papidid`: ID del atuendo
- `vapc`: cantidad de Piezas

*__INTEGRITY CHECK: el hash usado para validar los datos es `aps`__*

### ▶ Editar índices de Plantas en los Retos diarios

Busca `lfprii` en el editor.

Verás una lista de objetos. Son los records de los Retos diarios.

La estructura de cada objeto es la siguiente:

- `gm`: modo de juego
- `gl`: dificultad
- `npri`: índice aleatorio de premio (planta común)
- `fpri`: índice aleatorio de premio (planta especial)
- `rpri`: índice aleatorio de premio (planta rara)

**NOTA: los índices aleatorios parecen ser las probabilidades de obtener Piezas en el nivel.
Están ofuscados con bit rotation, descifra el valor original con SexyCalculator**

### ▶ Editar cuáles Atuendos secundarios tienes

Busca `lpnai` en el editor.

Verás una lista de objetos. Son los Atuendos secundarios que has desbloqueado. 

La estructura de cada objeto es la siguiente:

- `pnai`: ID de la planta
- `vnaid`: lista de atuendos desbloqueados

### ▶ Editar las Piezas para atuendos secundarios

Busca `pnapi` en el editor.

Verás una lista de objetos. Son los Atuendos secundarios y sus respectivos números de Piezas. 

La estructura de cada objeto es la siguiente:

- `pnapid`: ID del atuendo
- `pnapc`: cantidad de Piezas

### ▶ Editar los atuendos secundarios equipados

Busca `lpaei` en el editor.

Verás una lista de objetos. Son los Atuendos secundarios y las plantas que lo usan. 

La estructura de cada objeto es la siguiente:

- `peapid`: ID de la planta
- `peaaid`: ID del atuendo equipado

Editar esto te permitira forzar a una planta usar un atuendo aun si no lo tienes desbloqueado.

### ▶ Editar los Colgantes equipados

Busca `pasi` en el editor.

Verás una lista de objetos. Son los Colgantes que has equipado a tus plantas. 

La estructura de cada objeto es la siguiente:

- `paci`: ID de la planta que usa el Colgante
- `pact`: nombre del colgante equipado
- `pacid`: id del enlace, por default 0
- `l`: nivel (max 5, solo aplica para Super-Colgantes)

*__INTEGRITY CHECK: el hash usado para validar el valor es `ais`__*

### ▶ Editar las propiedades de Familia de plantas

**NOTA: el siguiente nodo tiene subnodos que poseen nombres idénticos al del objeto raíz, pondre un ´*´ para diferenciar los nodos hijos del padre, NO aparecen así en el JSON**

Busca `pfi` en el editor.

Verás una lista de objetos. Son las familias de plantas y sus respectivos efectos porcentuales. 

La estructura de cada objeto es la siguiente:

◼ `pfi*`: ID de la familia de plantas

◼ `pfbv`: objeto con los valores porcentuales, se divide en:

- `pfbvt`: tipo de mejora
- `pfbv*`: valor actual
- `pfbvrt`: tipo de mejora (hueco 2)
- `pfvrb`: valor futuro (hueco 2)
- `pfbm` : TO-DO
- `pfbl` : determina si el segundo hueco está desbloqueado (no estoy seguro)

**NOTA: cada familia de plantas tiene su propio ID**

### ▶ Editar los Trofeos de mundo

Busca `wcif` en el editor.

Verás una lista de objetos. Son los mundos y sus trofeos de progreso. 

La estructura de cada objeto es la siguiente:

- `wcwn`: nombre del mundo
- `wcscu`: trofeo de estrellas `(true para desbloquearlo, false para bloquearlo)`
- `wcbcu`: trofeo del jefe `(true para desbloquearlo, false para bloquearlo)`
- `wcpcu`: trofeo de plantas `(true para desbloquearlo, false para bloquearlo)`

### ▶ Editar el avatar de usuario

Busca `hsid` en el editor. Este valor es el ID del avatar que tienes asignado.

**NOTA: cada avatar de usuario tiene su propio ID

### ▶ Editar cúales avatars tienes

Busca `unlockhs` en el editor.

Verás una lista de números. Son las IDs asignadas a los avatars que has desbloqueado.

**NOTA: cada avatar de usuario tiene su propio ID

### ▶ Editar cantidad de Materiales y Monedas de evento

Busca `mtrl` en el editor.

Verás una lista de objetos. Son los materiales o monedas de evento que has acumulado.

La estructura de cada objeto es la siguiente:

- `id`: ID del material o moneda
- `count`: cantidad (ofuscado con bit rotation)

### ▶ Editar el Artefacto equipado

Busca `catfc` en el editor. Este valor es el ID del artefacto que has equipado.

**NOTA: cada artefacto tiene su propio ID

### ▶ Editar la Nivelación de tus artefactos

Busca `atfcla` en el editor.

Verás una lista de objetos. Son los artefactos y sus respectivas nivelaciones.

La estructura de cada objeto es la siguiente:

- `id`: ID del artefacto
- `rank`: rango de eficacia
- `level`: nivel
- `boostinfos`: array con info sobre las mejoras de cupon
- `uboostinfos`: array con info sobre las mejoras de cupon desbloqueadas

### ▶ Editar el banner de usuario

Busca `cravr` en el editor. Este valor es el ID del banner que tienes asignado.

**NOTA: cada banner de usuario tiene su propio ID

### ▶ Editar cúales banners tienes

Busca `unlockrai` en el editor.

Verás una lista de números. Son las IDs asignadas a los banners que has desbloqueado.

**NOTA: cada banner de usuario tiene su propio ID

### ▶ Editar los Genes de planta desbloqueados

Busca `mpgl` en el editor.

Verás una lista de objetos. Son los genes de plantas y su nivelación

La estructura de cada objeto es la siguiente:

- `id`: ID del gen
- `level`: nivel
- `lockState`: si está bloqueado o no `(0 = desbloqueado, 1 = bloqueado)`

### ▶ Editar cantidad de Material genético

Busca `mpgel` en el editor.

Verás una lista de objetos. Son los diferentes materiales usados en el Refinador de genes.

La estructura de cada objeto es la siguiente:

- `id`: ID del material
- `num`: cantidad

---

Los siguientes valores son exclusivos de versiones antiguas `(v1.0.1 - v1.7.7)`

### ▶ Editar la cantidad de Estamina

Busca `staminaData` en el editor.

Verás un objeto con las siguientes propiedades:

- `lastLocalTime`: última fecha local en la que se agotó la Estamina `(tipo: UnixTimestamp)`

- `startLocalTime`: fecha local en la que la Estamina empezó a recargarse `(tipo: UnixTimestamp)`

- `lastServerTime`: última fecha del servidor en la que se agotó la Estamina `(tipo: UnixTimestamp)`

- `leftSeconds`: segundos restantes para recibir más Estamina `(tipo: int)`

- `totalStamina`: cantidad de Estamina actual, por default 5 `(tipo: int)`

- `isTrust`: si confiar en los datos locales o usar los del servidor `(tipo: boolean)`

### ▶ Editar la cantidad de Llaves de mundo

Busca `wks` en el editor.

Este valor está ofuscado con rotaciones de bits.

*__INTEGRITY CHECK: el hash usado para validar el valor es `wkssign`__*

### ▶ Modificar cantidad de yuanes recargados (antiguo)

Nodo para las versiones antiguas del juego.

Busca `rcc` en el editor.

Luego, busca `ttrc` y modificalo con el mismo valor que asignaste al nodo anterior.

El segundo valor está ofuscado con rotaciones de bits.

### ▶ Editar la cantidad de Frijoles de oro

Busca `ptss` en el editor. Este valor son los Frijoles de oro que tienes.

Está ofuscado con rotaciones de bits.

*__INTEGRITY CHECK: el hash usado para validar el valor es `lsign`__*

### ▶ Editar los Mundos completados (mapa antiguo)

Busca `wm` en el editor.

Verás una lista de objetos. Son los Mundos que has completado.

La estructura de cada objeto es la siguiente:

- `W`: ID del mundo
- `E`: ID del nivel o evento
- `S`: estado de completación del nivel (0 = inexplorado, 1 = bloqueado, 2 = desbloqueado, 3 = completado)
- `C`: estrellas recogidas (0 = ninguna, 1 = ⭐, 3 = ⭐⭐, 7 = ⭐⭐⭐)
- `N`: numero de veces que se completo este nivel
- `P`: numero de veces que se jugo este nivel

*__INTEGRITY CHECK: el hash usado para validar el valor es `wes`__*

### ▶ Editar la cantidad de Piedras

Busca `sc` en el editor. Este valor son las Piedras obtenidas (antiguo evento, La Tienda de Piedra).

Está ofuscado con rotaciones de bits.

*__INTEGRITY CHECK: el hash usado para validar el valor es `ssign` (en desuso)__*

### ▶ Editar datos del evento del Yeti

Usado en las primeras versiones del juego.

Busca `tyi` en el editor. Verás un objeto con la siguiente estructura:

- `wml`: nivel donde el evento se activó `(tipo: string)`
- `lst`: última fecha en la que se avistó el yeti `(tipo: UnixTimestamp)`
- `nst`: próxima fecha del evento `(tipo: UnixTimestamp)`

### ▶  Editar las Zonas de Infinito

Busca `dri` en el editor.

Verás una lista de objetos. Son las Zonas de Infinito, a continuación su estructura:

- `wn`: nombre del Mundo o evento
- `cl`: nivel actual
- `hl`: puntuación más alta.
- `pfco`: Nutrientes almacenados (máx. lógico: 5)
- `l`: cortadoras restantes, cada configuración tiene su propia ID.
- `sb`: lista de plantas, cada una tiene su respectivo ID
- `hr`: determina si este nivel robará una carta o no

### ▶ Editar la cantidad de Llaves estelares

Busca `wsk` en el editor.

Verás una lista de objetos. Son los mundos y sus respectivas Llaves estelares.

La estructura de cada objeto es la siguiente:

- `wn`: nombre del mundo
- `kc`: cantidad de Llaves

*__INTEGRITY CHECK: el hash usado para validar los datos es `ws`__*

### ▶ Editar records de la Zona de Infinito (Festival)

Busca `mlescs` en el editor.

Verás una lista de objetos. Son las Zonas de Infinito del festival y sus records.

La estructura de cada objeto es la siguiente:

- `mark`: record
- `level_name`: nombre de la zona

---

> Hecho con ❤️ por FranZ, ¡disfruta!