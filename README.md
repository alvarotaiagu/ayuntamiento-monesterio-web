# Ayuntamiento de Monesterio · propuesta de web «Puerta abierta»

Maqueta de la web municipal del **Ayuntamiento de Monesterio** (Badajoz, 4.245 habitantes, INE 2025), hecha con la plantilla «Puerta abierta» (`plantilla-ayuntamiento-puerta-abierta-web`) y con sus datos reales. Se le propone por correo.

- **No es la web oficial.** Lleva en todas las páginas la banda «Propuesta de diseño… no es la web oficial» y `noindex, nofollow`.
- Publicada en <https://alvarotaiagu.github.io/ayuntamiento-monesterio-web/>. Con `?revision` sale el mando de versión y color.
- Las fuentes de cada dato, el inventario de su web actual y sus errores están **fuera de esta carpeta**, en `../ayuntamiento-monesterio-bocetos/`:
  - `DATOS.md`;
  - `INVENTARIO.md`;
  - `ERRORES.md`.

```bash
npm install                     # Playwright y axe-core (solo para los scripts)
node scripts/aplicar.mjs        # genera la web desde municipio.json, marca/, contenido/ y media/
node scripts/servir.mjs         # http://127.0.0.1:4192/  ·  con ?revision, el mando
node scripts/verificar.mjs      # todas las comprobaciones
```

`municipio.json` lo escribe `../ayuntamiento-monesterio-bocetos/_scripts/municipio.mjs` a partir de lo recogido. Los títulos claros del tablón los pone `_scripts/titulos-claros.mjs`.

---

## El concepto

**La puerta del Ayuntamiento, abierta todo el día.** El arco de medio punto encalado es el único motivo dibujado y enmarca la Casa Consistorial en la portada. El panel «Hoy en Monesterio» dice tres cosas:
- si el Ayuntamiento está abierto, calculado con la hora real;
- qué es lo próximo de la agenda;
- cuál es el último aviso.

Por qué le encaja a Monesterio:
- **Ya publica mucho, pero no se ve.** Su web sube 1 o 2 noticias al día, pero como **imagen sin texto**: no las lee un lector de pantalla, no salen en el buscador y no se ven bien en el móvil. Aquí las noticias van en texto. Los avisos de su canal de verdad, **Monesterio Informa** (Bandomóvil), tienen su sitio («Reciba los avisos en el móvil»), y la web no lo sustituye.
- **Su tablón oficial está en la sede de la Diputación**, sin RSS, y su web no lo enlaza desde el menú. Aquí sus anuncios entran solos y en lenguaje claro («15.26. BORRADOR DISOCIADO SESIÓN JGL 17.08.26» → «Acta de la Junta de Gobierno Local del 17 de agosto de 2026»). Lo que lleva datos personales se queda fuera.
- **Lo que el vecino busca, ordenado:**
  - 60 trámites con un buscador en palabras normales («empadronarme», «obra», «negocio»);
  - el listín entero, con las urgencias primero;
  - las instalaciones municipales;
  - los museos;
  - la normativa (187 documentos, que su web tenía repartidos en una docena de páginas).

**Marca: el sinople del escudo.** El escudo es oro (el campo) y gules (la banda, la cruz de Santiago y la torre).
- El oro nunca es marca: no llega a AA como texto.
- El gules es el color de las alertas: la franja urgente y el 112.
- La plata no sirve.
- Queda el sinople de las esmeraldas de la corona, que además es el verde de la dehesa, la seña del pueblo.

Está forzado con `--principal sinople` y con el motivo escrito en `marca/marca.json`. En la reunión, el mando enseña otros dos colores girando el matiz.

**Cortina: «El escudo a su sitio»** (`"cortina": "escudo"` en `marca/marca.json`). Se eligió entre cinco en el tablero `../ayuntamiento-monesterio-bocetos/cortinas/index.html`. Es la única vez que la web se mueve sola:
- solo en la portada y una vez por sesión, con 1,18 s en total;
- el escudo aparece en el centro sobre la cal;
- la cal se abre en un círculo con un anillo de oro;
- el escudo vuela y aterriza encima del de la cabecera.

Se salta con un clic, una tecla o la rueda, no existe con movimiento reducido y, sin GSAP, se quita sola.

**Ojo:** depende del escudo, que está pendiente de confirmar. Si cambia, basta `scripts/escudo.mjs`. Si prefieren no abrir con él, `"cortina": "puerta"` vuelve a la del arco.

## Mapa de páginas

| Página | Qué tiene |
|---|---|
| `index.html` | Hero «Hoy en Monesterio» con la Casa Consistorial en el arco. Trámites con 4 atajos (volante, escribir al Ayuntamiento, licencia de obra y Escuela Infantil). Tablón con filtros. Agenda y listín corto. «¿Quién se ocupa de qué?». «El año en Monesterio» |
| `tramites.html` | Buscador, «Por momentos» («Me vengo a vivir aquí», «Voy a hacer obra», «Voy a abrir un negocio», «Ha pasado algo en mi calle»), 5 temas y «Todos los trámites (60)»: 25 de la sede y 35 impresos en PDF de su web |
| `ayuntamiento.html` | Alcaldía (retrato como hueco diseñado y saluda de ejemplo). El pleno: PSOE 8 y PP 3, con el cambio de agosto de 2026. Concejalías y «quién se ocupa de qué». **Normativa y documentos**: impuestos, tasas, precios públicos, ordenanzas, reglamentos, urbanismo, archivo, plano y actas de pleno de 2008 a 2017 |
| `avisos.html` | «Reciba los avisos en el móvil» (Monesterio Informa). Avisos del Ayuntamiento y el tablón (40 anuncios) |
| `noticias.html` y `noticia-*.html` | 6 noticias recientes, en texto |
| `agenda.html` | Octubre de 2026, lo que pasó en septiembre y las fiestas de fecha fija |
| `telefonos.html` | Listín: 112, Ayuntamiento, Salud, Educación, Cultura y juventud, Empleo y comarca. **Instalaciones municipales**: piscina, estadio, pistas de El Tejar, albergue «Las Moreras» y área de autocaravanas |
| `pueblo.html` | Qué ver, **Para visitar** (Museo del Jamón, Museo Micológico, Centro de los Caminos Jacobeos y Museo del Recuerdo), historia, patrimonio, fiestas, gastronomía, personajes («tierra de pintores»), rutas (con el Camino de Santiago) y **Dónde comer y dormir** |
| `contacto.html` | Dirección, horario, mapa bajo clic, registro de la sede y datos de la entidad |
| Legal y `404.html` | Aviso legal, privacidad, cookies (no usa) y declaración de accesibilidad |

## Qué se añadió a la plantilla para Monesterio

Todo genérico y en commits de la plantilla, nunca como parche para este pueblo:
- **El lector del tablón de las sedes de la Diputación de Badajoz** (`ff107cc`):
  - las sedes de la Diputación no tienen RSS: se lee la vista antigua subsección a subsección, o una copia en HTML o en JSON;
  - `tablon_max`, porque la sede guarda todo desde 2018;
  - patrones nuevos de datos personales: actas sin disociar, mesas de contratación, mesas electorales, vehículos abandonados y relaciones nominales.
- **El patrón de enlaces de la sede «diputacion»**: admite las fichas de trámite y los documentos del tablón. La instancia general puede ser una URL.
- **Sede sin portal de transparencia** (`ba5d648`): Monesterio no tiene, y antes salía un enlace roto.
- **Trámites con solo `opc`**, la prueba del buscador sacada de los datos del municipio (antes llevaba palabras fijas de Ribera) y un correo largo que desbordaba el listín a 320 px.

Las secciones «Para visitar», «Normativa y documentos», «Dónde comer y dormir», «Instalaciones municipales» y el canal de avisos las añadieron a la plantilla, a la vez, las sesiones de Fuente de Cantos, Segura de León y Usagre. Aquí se reutilizan tal cual.

## Pendientes para el Ayuntamiento

- [ ] **Horario de atención** del Ayuntamiento. Su web solo da el del Registro General (de lunes a viernes, de 9:00 a 14:00, resolución de 2009). Sale ese, con la etiqueta «Ejemplo».
- [ ] **El escudo.**
  - Esta propuesta usa el SVG de Wikimedia Commons (Erlenmeyer, CC BY-SA 4.0).
  - No consta su aprobación en el DOE.
  - Sus notas de prensa usan otro dibujo, con cartela roja y la iglesia con nave.
  - Si nos pasan el vectorial del suyo, se cambia en un minuto y los colores salen solos.
- [ ] **Museo del Jamón**: su web da **cuatro horarios distintos** y ningún precio. No se enseña horario, y la ficha dice que se pregunte en la Oficina de Turismo.
- [ ] **Museo Micológico**: confirmar el horario, que solo da una página sin fecha.
- [ ] **Centro de Interpretación de los Caminos Jacobeos**: tras la cesión a la Junta (2026), ¿quién lo abre y cuándo?
- [ ] **Precios** de la piscina (anuncio del 1-7-2026) y del albergue (edicto del 13-3-2026).
- [ ] **Corporación**: quién lleva ahora la portavocía del PP y quién es el titular de la Secretaría-Intervención.
- [ ] **Teléfono 924 516 011**: lo da el formulario de contacto de la sede. ¿Es del Ayuntamiento?
- [ ] **Biblioteca**: la web municipal y el directorio del Ministerio de Cultura no coinciden en dirección, teléfono ni horario. Se usa el de la web.
- [ ] **Perfil del contratante**: el enlace a su perfil en la Plataforma de Contratación (ahora va al de la sede, parado en 2023).
- [ ] **Fotos propias** y su permiso: la iglesia de San Pedro, el Museo del Jamón, la plaza y el Día del Jamón. Ahora todas son de Wikimedia Commons, y hay huecos diseñados.
- [ ] **Listas que no se publican porque no se pueden fechar**: asociaciones (53, la última referencia es de 2016), taxis (dos listas distintas) y la Guía Empresarial (unos 300 negocios).
- [ ] **Facebook**: si la página «Ayuntamiento de Monesterio» es la suya, se enlaza.
- [ ] **Autorización para leer el tablón** de la sede a diario. La sede no tiene `robots.txt`, pero se pide igual. Mientras tanto, el tablón de la maqueta es una copia del 3 de octubre de 2026.

## Erratas de su web, corregidas al usar sus textos

- «Monesteri ocelebra» → «Monesterio celebra»; «entorno al 15» → «en torno al 15» (fiestas).
- «mantanza», «chuchara», «potage», «bacalo», «repálalos» → «matanza», «cuchara», «potaje», «bacalao», «repápalos» (gastronomía).
- «entre en la Historia», «atestigua se denominación», «se había de perdido» → «entra», «su denominación», «se había perdido» (historia).
- «la vista por el Museo», «Paraje ünico», «Naranjom», «superfie», «especio» → «la visita», «Paraje único», «Naranjo», «superficie», «espacio» (museos).
- «2o:30 h» → «20:30 h» (horario de misa).
- «Viilalba» → «Villalba» (pleno); la ficha de la Diputación dice «Dª Manuel Ferrerira» por Manuela Ferreira Delgado.
- «desde las 8:00 h a 3:00 h» → «de 8:00 a 15:00» (Escuela Infantil).
- «Gestión Prespuestaria» → «Presupuestaria» (catálogo de la sede).
- En los títulos de las ordenanzas: «reguladora.delimpuesto» → «reguladora del impuesto», y las tildes que faltaban («aprobación», «concesión», «protección»…).
- La lista de restaurantes pegaba el número de la calle al teléfono de Los Templarios («Templarios, 206630405»).

## Datos que se contradicen

- **Horarios del Museo del Jamón y de la Oficina de Turismo**: cuatro versiones (ver `ERRORES.md` 1.6). No se enseñan.
- **Hectáreas de dehesa**: 16.000 (Información General) frente a 17.643 (Día del Jamón). Se usa «unas 16.000».
- **Altitud**: 755 m (Diputación y web), 765 (Wikipedia) y 751 (OSM). Se usa 755.
- **Población**: 4.245 (INE 2025), frente a «4.500 aproximadamente» de su web y 4.345 de la Diputación (2014). Se usa la del INE.
- **Feria**: «del 8 al 12» (Diputación); en 2026 fue del 8 al 13. Se dice «en torno al 8 de septiembre».
- **Jamón & Blues**: «julio» según el portal turístico; en 2026, a finales de junio. Se usa «finales de junio».
- **Albergue «Las Moreras»**: 679 587 435 (web municipal) frente a 690 304 314 (OpenStreetMap). Se usa el de la web.
- **Nuevo Centro del Conocimiento, La Dehesa de Don Pedro y taxis**: dos teléfonos o dos listas distintas. No se enseñan.

## Fotos

Todas de **Wikimedia Commons**, con su licencia. Su web no se ha tocado: su `robots.txt` prohíbe `/imagenes/`. Tienen gradación común (`scripts/fotos.py`).

| Foto | Autor | Licencia |
|---|---|---|
| Casa Consistorial (portada) | Vanbasten 23 | CC BY-SA 3.0 |
| Calle con la torre de San Pedro (foto antigua) | Fernando Garrorena Arcas (1901-1945) | Dominio público |
| Pilar de la Reverencia | Marbregal | CC BY-SA 3.0 |
| Antiguo silo, hoy Museo Micológico | Vanbasten 23 | CC BY-SA 3.0 |
| Paseo de Extremadura | Feranza | CC BY-SA 3.0 |
| Monasterio de Tentudía (término de Calera de León) | 80kmh | CC BY 4.0 |
| Escudo | Erlenmeyer | CC BY-SA 4.0 |

Cada una enlaza a su ficha en la página «El pueblo» y en `media/creditos.json`.

## Antes de entregar

La receta es la de [RESKIN.md](RESKIN.md) §9:
1. fijar la versión y el color que elijan;
2. `python scripts/quitar_mandos.py --comprobar` y después `python scripts/quitar_mandos.py`;
3. `"propuesta": false` e `"indexar": true` solo cuando sea la web oficial en su dominio;
4. `node scripts/aplicar.mjs && node scripts/verificar.mjs`.

## v3 (rama `v3`, 2026-10-05)

Pasada a la v3 de la plantilla (v3 + v3b + v3c) sin tocar sus datos: código superpuesto, `municipio.json`, `marca/`, `media/` y `contenido/` de Monesterio conservados. `master` sigue en la v1.

Añadido para Monesterio:
- `cifras` (INE 4.245, 322,4 km², 755 m, 1248) con su fuente; `ine`, `incidencias` («Avisar de un problema», al correo del Ayuntamiento), «Escríbanos» (sale solo), `transparencia` (sin portal: apartados con sus huecos «Pendiente»), `farmacias.oficial` y los `pasos` de Monesterio Informa.
- `propuesta_web` (`propuesta.html`, sin enlazar): 5 problemas comprobables de ERRORES.md, captura real de su portada del 5-10-2026 (`assets/web-actual.jpg`) y mi contacto. **Falta el `[PRECIO]`** (solo se ve con `?revision`).
- `contenido/facil.json` (lectura fácil): volante, escribir al Ayuntamiento, licencia de obra, Escuela Infantil e incidencias. Pendiente de validar con personas usuarias.
- `contenido/pueblo.en.json` y `pueblo.pt.json`: «El pueblo» en inglés y portugués.
- Plazo del IAE (16-11) con cuenta atrás; arco de portada con 3 fotos (Casa Consistorial, silo, Tentudía); cabecera de «El pueblo» con la calle de San Pedro; fotos igualadas (`media/originales/`).
- Plano del pie (`marca/plano.*`, desde el elemento de OSM way/549797280, el Ayuntamiento) y mapa del término (`marca/termino.*`, relación 342331): solo 4 de 13 lugares están en OSM con nombre reconocible (Iglesia, Pilar, Ermita de Tentudía, Castillo de las Torres). Los demás se pueden fijar con `node scripts/termino.mjs --lugar "Nombre=node/ID"`.

`municipio.json` **ya no se regenera** con `../ayuntamiento-monesterio-bocetos/_scripts/municipio.mjs` (pisaría lo de la v3); el script que añadió los campos de la v3 está en `../ayuntamiento-monesterio-bocetos/_scripts/v3-datos.py`.

Pendiente de la v3:
- [ ] **Perfil del pueblo en el pie**: sale el genérico. Para dibujar el de Monesterio hace falta una foto actual de la iglesia de San Pedro (la que hay es de hace un siglo).
- [ ] Confirmar el correo de incidencias y «Escríbanos» (`ayuntamiento@monesterio.es`).
- [ ] Fecha de los plenos: no hay pleno próximo en los datos (el último fue el 3-9-2026); el tablón ocupa todo el ancho.
- [ ] Autorización para leer el tablón (`tablon_autorizado`), y con ella la tarea diaria de `.github/workflows/actualizar.yml`.
- [ ] Crear la hoja y los formularios (`plantillas-hoja/crear-hoja.gs`, `PUBLICAR.md`) y rellenar `hoja.id`.
