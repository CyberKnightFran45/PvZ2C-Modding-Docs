# PvZ 2 Chino - Analisis al sistema anticheat

La version china de PvZ2 cuenta con un sistema antihacking que detecta cambios en los datos del juego mediante la comparacion de firmas MD5 alimentadas por un salt diferente para cada usuario.

Esto quiere decir que dos cuentas con misma cantidad de Gemas pueden tener un hash diferente, ya que se usa algo propio del usuario como Salt *(un uid o un random seed posiblemente)* para que las firmas sean unicas por jugador.

**Esquema de los datos validados**

| Descripcion | Nodo      | Tipo     | Firma      |
|------------|:---------:|:--------:|:----------:|
| Monedas  | c |      int    |    csign        |
| Joyas   | g/gg |    int      |      gs      |
| Llaves estrella | wsk |   WorldSpecificKey[]     |      ks      |
| Potenciadores  | pr |   PowerupRecord[]    |      prs      |
| Piezas de plantas  | ppr |   PlantPieceRecord[]     |      pprs      |
| Plantas   | p |    int[]     |      ups     |
| Mejoras  | gf |   int[]     |      ugfs      |
| Mundos completados| wm |   SavedWorldMapEventData[]     |      wes      |
| Compras | rpi |   PurchaseInfo   |      rps      |
| Llaves de mundo | wks |   int     |      wkssign      |
| Piedras   | sc |    int      |      ssign      |
| Nivelacion de plantas | psla |   PlantStarLevel[]     |      psls      |
| Atuendos  | ulokpa |   PlantAvatarInfo[]     |      uas      |
| Piezas de atuendo | lpapi |   PlantAvatarPiecesInfo[]     |      aps     |
| Sobres rojos  | rp |    int      |      rpsign      |
| Piezas de colgantes  | asp |   AccesoryPiece[]     |      asps     |
| Colgantes equipados | pasi |   PlantAccesoryInfo[]     |      ais      |
| Nueva tienda | Varios |   Varios |      lprmd5     |
| Frijoles dorados | ptss |   int   |      lsign      |
| Mundos desbloqueados: aventura de plantas | pawf |   int[]   |      paws      |

---

**Ejemplo**

El siguiente ejemplo muestra el nodo de gemas y su firma. El formato original es RTON, esto es su equivalente JSON obtenido al parsear la data

```
"g" : 618405888,
"gg" : 65500,
"gs" : "7007b0af5f6b668318ac64ee9d7eaaca"
```

**NOTA: todo indica que el sign se trata en realidad de MD5 por la longitud del string (32 caracteres hex, es decir 16 bytes)**

## Anticheat v1.0

El sistema usaba el campo `pcpid` como base (un GUID del jugador cargado desde el archivo `SexyAppActivity.xml`) y comparaba los datos criticos del pp.dat. Si se encontraban anomalias, estas eran revertidas, dejando el archivo local en limpio.

Un dialogo en pantalla aparece con los siguientes mensajes

```
[DIA_FAKE_SAVE_WARNING]
Para supervisar la excepción de datos de archivo,
el sistema ha borrado los datos anormales.

[DIA_FAKE_SAVE_WARNING_301]
Para supervisar la excepción de datos de archivo,
el sistema ha borrado los datos anormales.
<Código de error: 301>

[DIA_FAKE_SAVE_WARNING_302]
Para supervisar la excepción de datos de archivo,
el sistema ha borrado los datos anormales.
<Código de error: 302>
```

Los datos se borran al hacer clic en ACEPTAR.

**Versiones afectadas: 1.0.1 - 1.6.3**

---

## Anticheat v2.0

Mismo principio que el sistema anterior, ahora banea las cuentas si detecta que usan hacks.

El dialogo que aparece en pantalla es el siguiente:

```
[PVZ_LOGIN_CHEAT_ERROR]
Se te ha vetado por hacer trampas con mods o programas de terceros.
Si se trata de un error, ponte en contacto con el servicio al cliente.
Tu UID: {UID}
```

**Versiones afectadas: 2.2.7 - 2.4.81**

## Anticheat v3.0

Version reforzada del sistema anterior, la validacion y carga de progreso parecen hacerse desde el servidor.

Los dialogos que aparecen en pantalla son:

```
[PVZ2_CHEATING_CHECK_TITLE]
DETECTOR DE TRAMPAS

[PVZ2_CHEATING_WARNING_1]
Se detectaron anomalías en modos online.
Si se trata de trampas, tus puntuaciones se eliminarán de la clasificación.

[PVZ2_CHEATING_WARNING_2]
Trampas detectadas en modos online, se te excluirá de la lista de clasif.
Si se repite este comportamiento, tu cuenta será vetada.
¿Se trata de un error? Contáctate al soporte en QQ: 4008932088

[PVZ2_CHEATING_WARNING_3]
Trampas detectadas en modos online, se te excluirá de la lista de clasif.
La proximá vez que hagas trampa, tu cuenta será vetada.
¿Se trata de un error? Contáctate al soporte en QQ: 4008932088

[PVZ2_CHEATING_WARNING_4]
Jugador vetado por hacer trampas. No puedes acceder con esta cuenta.
¿Se trata de un error? Contáctate al soporte en QQ: 4008932088
```

**Versiones afectadas: 2.4.83+**

---

### Detalles del Debug Check

La version con Debug menu (v1.6.3) contiene una funcion interesante:

```Global > Debug Check```

Esta verifica la integridad del perfil actual contra un perfil con hash recalculado, y genera una copia decodificada de ambos. 
Funciona asi:

1. Primero verifica que existan copias de los datos guardadas como json en local, se generan al hacer clic en el boton Save de la interfaz como dos archivos: `PlayerInfo_backup.json` y `PlayerInfo_tmp.json`

2. Compara las versiones del perfil con la version actual (`nodo v`). **El identificador de version es 19 para la 1.6.3**

3. Verifica la lista de plantas desbloqueadas, comparando cualquier ID invalido y verificando que coincidan con la firma. Luego se genera el archivo `Plants_backup.json` conteniendo una lista de plantas desbloqueadas escritas como typename. **El pp.dat las almacena como IDs numericos**

4. Analiza que no haya discrepancias con los datos del jugador `(PlayerInfo)`, recalculando las firmas en `tmp` y comparandolas con el `backup`. **Lanzara una alerta si detecta que hay cambios.**

---

### Sobre las firmas de perfil

Estuve buscando con IDA las funciones encargadas de calcular los nodos hash antes de escribirlos.

`Version de referencia: 1.6.3 (Debug)`

Esto fue lo que encontre.

1. Los datos se concatenan con diferentes formatos dependiendo el tipo de campo antes de hacer el MD5 digest.

2. El primer string usado en las diferentes concatenaciones se obtiene de `sub_262EC0()` Esta funcion carga el nodo `pcpid` (PlayerID) del archivo `SexyAppActivity.xml`

3. El objeto `a1` es una instancia del perfil `(PlayerInfo)`

4. El campo `rs` corresponde al seed del jugador `(RandomSeed)`

5. El campo `snuuid` corresponde a la direccion MAC del servidor (un string con el valor `02:00:00:00:00:00`)

6. Para la mayoria de valores escalar, primero se calcula el entero real (ya que algunos estan protegidos por BitsRotation y se serializan ofuscados en el json mientras que se cargan en memoria como `PropGrid.Hide`, ocultando el valor real).

A continuacion el flujo de como los hash son generados:

#### Sign para Llaves de mundo

- Usado en: `sub_A9B1C8, sub_A9B360, sub_A9B4B4`

- Nodo firma: `wkssign`

- Formato: `off_24EBAE0[0] -> 0x2045798 = "brGwm%siuy%deert%d10%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)	wks
%s (4)	snuuid
```

#### Sign para cantidad de Monedas

- Usado en: `sub_A9B65C, sub_A9B7F4, sub_A9B948`

- Nodo firma: `csign`

- Formato: `off_24EBABC[0] -> 0x20456A8 = "asIen%seos%deosd%d11%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)	c
%s (4)	snuuid
```

#### Sign para cantidad de Piedras

- Usado en: `sub_A9BAF0, sub_A9BC88, sub_A9C698`

- Nodo firma: `ssign`

- Formato: `off_24EBAF0[0] -> 0x20457F8 = "bgXes%sezz%detwd%d11%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)	sc
%s (4)	snuuid
```

#### Sign para cantidad de Joyas

- Usado en: `sub_A9C840, sub_A9C9E4, sub_A9CB44`

- Nodo firma: `gs`

- Formato: `off_24EBAC0[0] -> 0x20456C0 = "Odsn%sasde%dNNsd%d22%s%d"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)	g
%s (4)	snuuid
%d (5)	gg
```

#### Sign para cantidad de Sobres rojos

- Usado en: `sub_A9CD0C, sub_A9CEA4, sub_A9CFF8`

- Nodo firma: `rpsign`

- Formato: `off_24EBAFC[0] -> 0x2045840 = "Yun%s;ej%dlLinzzet%dk1%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)	rp
%s (4)	snuuid
```

#### Sign para Llaves estrella

- Usado en: `sub_A9D1A0, sub_A9D420, sub_A9D66C`

- Nodo firma: `ks`

- Serializacion: cada elemento se serializa con `"%s_%d"` (nombre del mundo y cantidad de llaves). El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBAC4[0] -> 0x20456E0 = "(&^^%sOsP%dlsdfs%s33%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%s (3)	cadena serializada del vector wsk
%s (4)	snuuid
```

#### Sign para Potenciadores

- Usado en: `sub_A9D868, sub_A9DAE8, sub_A9DD34`

- Nodo firma: `prs`

- Serializacion: cada elemento se serializa con `"%s_%d"` (tipo de potenciador y cantidad). El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBAC8[0] -> 0x20456F8 = ")2ld%sPPsd%dDSsf%d44%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)	direccion al buffer con la cadena serializada del vector pr
```

**NOTA: el tercer valor concatenado deberia ser un string (%s) para obtener el contenido y no la direccion al buffer, la cual es dinamica y varia segun el estado de ejecucion del juego. Lo mas probable es que se trate de un error de desarrollo.**

#### Sign para Piezas de plantas

- Usado en: `sub_A9DF30, sub_A9E1A8, sub_A9E3EC`

- Nodos firma: `pprs`

- Serializacion: cada elemento se serializa en par con `"%d_%d"` (donde el primer entero es el ID de la planta y el segundo es la cantidad de Piezas). El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBACC[0] -> 0x2045710 = "Owe%s_(sd%dNNlsd%s55%s"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada del vector ppr
%s (4)	snuuid
```

#### Sign para Piezas de Colgantes

- Usado en: `sub_A9E644, sub_A9E890`

- Nodos firma: `asps`

- Serializacion: cada elemento se serializa con `"%s_%d"` (nombre del colgante y cantidad de piezas). El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBAF4[0] -> 0x2045810 = "iou%s_(sd%dUiowl%s92%s"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada del vector asp
%s (4)	snuuid
```

#### Signs para Colgantes equipados

- Usado en: `sub_A9EAE8, sub_A9ED44`

- Nodo firma: `ais`

- Serializacion: cada elemento se serializa como campo estructurado con `"%d_%s"` (ID de la planta portadora y nombre del colgante equipado). El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBAF8[0] -> 0x2045828 = "woq%s_&zo%doWzqk%s37%s"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada del vector pasi
%s (4)	snuuid
```

#### Sign para Nivelacion de plantas

- Usado en: `sub_A9F024, sub_A9F29C, sub_A9F4E0`

- Nodo firma: `psls`

- Serializacion: cada elemento se serializa en par con `"%d_%d"` (donde el primer entero es el ID de la planta y el segundo es la nivelacion). El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBAEC[0] -> 0x20457E0 = "dja%sDM&%dOc%s-@ow%so2"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada del vector psla
%s (4)	snuuid
```

#### Sign para std::vector<int> (GameFeatures y otros)

- Usado en: `sub_A9F6DC, sub_A9F93C, sub_AA161C, sub_AA1874, sub_AA1A98, sub_AA1C94, sub_AA1F38, sub_AA21A8`

- Nodo firma: `ups, ugfs, wes`

- Serializacion: cada elemento se serializa con `"%d_"` El resultado final es una unica cadena representando todos los elementos.

- Formato: `off_24EBAD0[0] -> 0x2045728 = "23d%sceaa%dmjLsd%s66%s"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada de p, gf o wm
%s (4)	snuuid
```

**Nota: para wm, la serialización interna es "%d_%d_%d" (para los nodos W, E y S respectivamente)**

#### Sign para Atuendos desbloqueados

- Usado en: `sub_A9FFB4, sub_AA0304, sub_AA0620`

- Nodo firma: `uas`

- Serializacion: cada elemento se descompone en `"%d_%d"` (ID del atuendo y estado), y luego `"_%d"` para subelementos (cada byte del tipo de atuendo).

- Formato: `off_24EBAE4[0] -> 0x20457B0 = "oang%s[ea0J%d)Mn%s>z%s"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada de ulokpa
%s (4)	snuuid
```

#### Sign para Piezas de Atuendo

- Usado en: `sub_AA0BDC, sub_AA0F0C, sub_AA1208`

- Nodo firma: `aps`

- Serializacion: se manejan subelementos con múltiples niveles con `"%d"` (ID del atuendo) y luego `"_%d"` (array de un unico entero, con la cantidad de piezas)

- Formato: `off_24EBAE8[0] -> 0x20457C8 = "pqan%sz/qeY%d{qn%s#!%s"`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada de lpapi
%s (4)	snuuid
```

#### Sign para info de compras

- Usado en: `sub_AA23A4, sub_AA255C, sub_AA26E0`

- Nodo firma: `rps`

- Formato: `off_24EBADC[0] -> 0x2045770 = "Odsn%sasde%dNNsd%s3fswe%sfefef%s99%s"`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%s (3)	rpi.rcp
%s (4)	rpi.rcpi
%s (5)	rpi.pdi
%s (6)	snuuid
```

---

A partir de la version `1.7.5`, se agregaron las siguientes firmas:

#### Signs para info de Nueva tienda

Se guardan diferentes firmas como una especie de copia de seguridad para la compra de ciertos recursos.

- Nodo firma: `lprmd5`

- Campos: 

`rcpi` - cantidad de Frijoles dorados (misma firma que `lsign`, descrito a continuacion)

`rcp` - cantidad de Monedas (misma firma que `csign`)

`pdi` - cantidad de Joyas (misma firma que `gs`)

---

#### Sign para cantidad de Frijoles dorados

La cantidad de Frijoles dorados obtenidos al abrir Cofres en versiones antiguas.

El valor se deriva con una rotacion a la izquierda (ROR) y se compara contra un valor recalculado para la nueva cantidad de hojas bajo la siguiente formula: `ptss + (extra * lmz)`

Donde:

- `lmz` es el multiplicador de frijoles, con valor `1.0` por default

- `extra` es la cantidad de frijoles adicionales (puede ser 1 o 10)

Esto aplica unicamente cuando se esta abriendo cofres. La formula se simplifica tomando el valor directo de `ptss`, lo que produce el mismo resultado exacto: `derived = ROR(ptss, ptss & 0x1F) ^ ptss`

- Nodo firma: `lsign`

- Formato: `aaXes%smzz%dbdwd%d12%s`

- Parametros:

```
%s (1)	pcpid
%d (2)	rs
%d (3)  derived
%s (4)	snuuid
```

---

#### Sign para mundos abiertos (Aventuras de plantas)

- Nodo firma: `paws`

- Serializacion: cada elemento se serializa con `"%d_"` El resultado final es una unica cadena representando todos los elementos.

- Formato: `uio%sHuy%dpe%srew-%sl4`

- Parametros:

```
%s (1) pcpid
%d (2) rs
%s (3)	cadena serializada de pawf
%s (4)	snuuid
```

---

#### Signs residuales

Se dejaron los siguientes literales en el codigo, pero no hay funciones que los utilicen

`Owe%s_(sd%dNe2sd%s88%s`

`Odd%s_(sd%dNvbNd%s77%s`

---

A partir de la version `2.0.0`, se hicieron los siguientes cambios:

1. El nodo `lprmd5` paso de ser un objeto a un string vacio (eliminado por redundancia)

2. Se le agrego un nuevo campo a la clase `PurchaseInfo` llamado `oipi` (entero), esto no afecta la generacion de `rps`

3. Con el cambio de los Mundos, se agregó el nodo `wmed`, sin embargo, `wes` sigue generandose de`wm` (ahora vacío)

---

Una vez se hace la concatenacion, se procede a generar el Hash MD5 en `sub_1C38284`, no hay clave HMAC ni nada por el estilo, solo un digest casero con valores cambiantes segun usuario.

### Conclusiones

Busque los mismos literales en la version mas reciente (`4.0.1` a la fecha en la que hago este documento) y aun están presentes, lo cual indica que el sistema usa los mismos principios para validar datos de usuario y determinar si son legitimos o no.

El siguiente paso sera modificar un pp.dat y con un script replicar los hash para probar si los datos persisten despues de ingresar al juego, o si el sistema los borra de igual forma.

**NOTA: intercambiar los datos locales en versiones posteriores a la `2.4.83` no tiene efecto alguno porque los archivos se manejan de lado del servidor, pero si descargas una version anterior (como la `2.2.5`)  y luego actualizas el juego a la más nueva, su sistema migrará los datos a la nube haciendo que los cambios persistan (esto funciona siempre y cuando el anticheat no detecte anomalias)**

> Analisis por FranZ