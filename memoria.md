# Memoria del Trabajo de Fin de Máster ([MPVD](https://mpvd.es/))

Autor: [Juan Luis Monterroso Aranda](https://www.linkedin.com/in/jlmonterroso/)

## Agradecimientos

### Tutores

- Adolfo Antón: Por sus correcciones y aportaciones en todo el proyecto.

- Yolanda García: Por su ayuda con los notebooks de Python y los gráficos.

- Jesús David Navarro "Jesusda": Por sus anotaciones y propuestas con las tablas.

- Julián Perez: Por su ayuda con la web y los elementos de la misma.

- Alejandro Zappala: Por sus propuestas y correcciones de los mapas.

### Resto de profesores del máster

Agradecido a todos los profesores del MPVD por aportarnos sus conocimientos y estar dispuestos a resolver dudas en clase y en tutorías.

### Profesionales que participaron en el máster

Gracias a aquellos profesionales que han compartido sus conocimientos y proyectos en las diferentes charlas y talleres del MPVD. Sus experiencias han servido para darnos ideas de cara a este TFM.

### Compañeros del MPVD

Agradecido con mis compañeros de máster por la ayuda que me han ofrecido durante todo este curso. Hemos hecho un gran grupo, compartiendo nuestras dudas y resolviéndolas entre todos.

### Familia y amigos

Gracias por motivarme a realizar esta formación, por interesarse en el proceso y por ayudarme de la manera que han podido.

## Girona, una ciudad en transformación

Con el título quería reflejar lo que es Girona: una ciudad que ha cambiado en los últimos años y que aún tiene margen de mejora.

## Resumen del proyecto

Entre los Pirineos y la Costa Brava se encuentra una de las localidades con mayor patrimonio histórico de España: Girona. La ciudad catalana ha sabido convertirse en los últimos años en una ciudad atractiva para el turismo y las inversiones económicas por su clima mediterráneo, por la presencia de monumentos como la Catedral de Girona y por su oferta cultural, gastronómica, deportiva y educativa. La estación de tren de alta velocidad, los accesos por autopista y el aeropuerto hacen de Girona una ciudad accesible y deseada por muchos para instalarse definitivamente.

Este proyecto de periodismo de datos pretende explicar las causas y consecuencias de este crecimiento.

## Introducción

### Motivación

Una de las partes más difíciles del trabajo de fin de máster fue la elección del tema. Varias propuestas sobre la mesa pero al final me decidí por hacer un proyecto local.

Vi que mi ciudad tenía un portal de datos abiertos, [Girona Open Data](https://www.girona.cat/opendata/dataset) donde podemos encontrar mapas de la ciudad y sus barrios, presupuestos del ayuntamiento, licencias de obras, padrón, etc. En este portal me pareció interesate una base de datos con todos los establecimientos comerciales de la ciudad desde el año 2013. Echando un vistazo al documento del último año se podía ver cómo las viviendas de uso turístico eran las más numerosas, por encima de bares, tiendas y otras actividades.

Eso me llevó a pensar que la ciudad había cambiado en los últimos años y se estaba apostando fuertemente por el turismo y todo lo relacionado con el sector servicios. Ahí decidí que podía haber un tema potente sobre el que desarrollar mi trabajo de fin de máster.

### Objetivos

El objetivo principal es mostrar con datos cómo la ciudad de Girona ha experimentado un fuerte cambio en los últimos 50 años. No pretende ser un proyecto sesgado que parta desde una idea preconcebida: quiero que los datos me de indiquen una tendencia (si la hay), no que mi reportaje se base en los datos que sustentan mi teoría.

### Metodología

A la hora de hacer el trabajo se ha seguido el siguiente orden:

#### Elección del tema

Como he comentado anteriormente, me decidí por este tema  al ver en una base de datos sobre actividades económicas en Girona que la mayoría de ellas están relacionadas con las viviendas de uso turístico.

#### Documentación

Esta es una parte muy importante del proyecto, ya que he tenido que informarme mucho sobre el tema para conocer cuáles han sido las políticas que se han llevado en los últimos años en la ciudad. En el apartado *Bibliografía*, al final de este proyecto, se muestra la bibliografía consultada.

#### Descarga de datasets

Una vez consultados todos los datasets que tenía a mi alcance, procedí a su descarga. Para ello usé *Cygwin* y su paquete *wget*. Con ```mkdir``` creé los directorios y con ```wget --no-check-certificate url-archivo``` descargué uno a uno los archivos. Si los archivos venían en formato .zip los descomprimía de la siguiente manera: ```unzip nombre-archivo -d nombre-carpeta-nueva```. También combiné ambas funciones como en el siguiente ejemplo:
```
wget --no-check-certificate https://terra.girona.cat/opendata/storage/f/2021-06-28T10%3A49%3A46.540Z/seccions.zip && unzip seccions.zip -d secciones
```

A la hora de elegir el formato de los archivos (cuando tenía la posibilidad de elegir entre varios formatos) he priorizado aquellos que tenían formato .csv. 

#### Limpieza de datos

A la hora de tratar los datos me he apoyado en dos herramientas: la librería Pandas de Python y el software *OpenRefine*.

Con *Jupyter Notebook*, creaba documentos .ipynb que soportasen Python. Seguidamente importaba (y descargaba si era necesario) la librería Pandas con la que daba un primer vistazo al archivo.

*OpenRefine* me sirvió de gran ayuda cuando usé la función *Cluster and edit*, que permite encontrar palabras similares en una misma celda y agruparlas en una misma categoría. Por poner un ejemplo, en el archivo *activitats2022.csv*, que contenía el censo de establecimientos dedicados a actividades económicas registradas en el Ayuntamiento de Girona, las viviendas de uso turístico aparecían escritas de varias maneras: habitatge d'ús turístic, habitatge d'us turístic, habitatge d'ús turistic, etc. Con la función *Cluster and edit* pude englobarlas todas bajo el nombre correcto.

#### Gráficos con Plotly (Python)

Una vez tratados los datos procedí a visualizarlos. En los notebooks siempre intenté dibujar los gráficos con Matplotlib y Plotly. La razón es que a la hora de subirlos a la web no tenía claro cuál era la mejor opción, si un gráfico estático en formato .svg o un gráfico interactivo en formato .html.

Creo que los gráficos interactivos dan un valor añadido al proyecto y los gráficos estáticos se ajustan mejor a la web y tienen menos problemas de responsividad. Al final subí todos los gráficos en formato .html interactivo consiguiendo que se vean bien tanto en ordenador como en otros dispositivos como tablet o móvil.

#### Mapas en QGIS

El único mapa del proyecto, *comparativa-vut-2013-2022.png*, lo dibujé con QGIS. Para llegar al resultado final, tuve que seguir los siguientes pasos:

1. Descarga del mapa de fondo (*barris.shp*) y los datos necesarios para representarlos (*vut13.csv* y *vut22.csv*). El archivo *barris.shp* lo obtuve de [Girona Open Data]((https://www.girona.cat/opendata/dataset) y corresponde a la delimitación de los barrios de Girona. Los archivos .csv corresponden a las viviendas de uso turístico que había tratado y exportado en los notebook de Python. Los barrios tienen un color de relleno ```#eff6ff```.

2. Descarga del paquete Catastro Inspire para disponer de los edificios de la ciudad. Es importante filtrar por fecha ya que no habían los mismos edificios en 2013 que en 2022. A la hora de añadir los edificios al proyecto, los personalicé quitando la plumilla y coloreándolos de ```#666666```.

3. Añadir las capas vectoriales, raster o texto delimitado. Hay que procurar que todas estén en el mismo Sistema de Referencia de Coordenadas, en este caso ETRS89.

4. Creación del mapa de puntos de las viviendas turísticas de cada año de la comparativa representándolos como simbolo único. Indicarle el color ```#f4a460```, que ha sido el color usado en todos los gráficos y estilos del proyecto, con un tamaño de 3mm.

5. Cluster de puntos en el mapa de 2022, ya que se acumulaban muchos puntos en un mismo espacio y no se visualizaba correctamente. Para ello, modifiqué la simbología, indiqué la opción *Grupo de puntos* y personalicé los parámetros a mi gusto: símbolo, color, distancia de agrupamiento, etc.

6. Por último, creé una nueva composición de impresión para crear la infografía. Allí personalicé todo el mapa añadiendo la escala, el norte, el nombre de los barrios, etc. Exporté el archivo en formato .png ya que, los mapas con tanta información, suelen dar más problemas de visualización si se exportan en formato .svg.

#### Edición de imágenes de alcaldes

En la parte inicial del proyecto aparecen unas imágenes de los diferentes alcaldes y alcaldesas que han gobernado en Girona en la etapa democrática. Todas tienen licencia Creative Commons de Reconocimiento y Compartir Igual, que permite compartir (copiar y distribuir) y adaptar (remezclar, transformar y construir a partir del material), incluso para fines comerciales. Todas tienen formato png y corresponden a:

- Joaquim Nadal, autor Jordi Bedmar.

- Marta Madrenas, autor Aleix Clarió.

- Carles Puigdemont, autor Chatham House.

- Lluc Salellas, autor Guanyem Girona.

- Anna Pagans, autor ACN.

- Albert Ballesta, autor Ajuntament de Girona.

A la hora de hacer los logos de los alcaldes, recorté el contorno con la herramienta de selección libre de *Gimp*, pasé la imagen a *Inkscape* y le apliqué una máscara. Acabé de retocar los colores correspondientes y exporté la imagen en formato .svg.

Para hacer las imagen de fondo de *scrollama*, importé los logos que había creado previamente, los ordené y les apliqué el filtro *Fundir a negro o blanco* para oscurecer las imagenes que no quería resaltar. Repetí el proceso 6 veces, una vez por cada alcalde. Finalmente exporté las imágenes en formato .png.


#### Creación de tablas

Las tablas que aparecen en el proyecto las realicé de la siguiente manera:

1. Dibujé la tabla con la herramienta propia de *LibreOffice Writer*.

2. La copié y la pegué en *LibreOffice Draw*.

3. Seguidamente, pegué la tabla en Inkscape en formato vectorial.

4. Modifiqué la tabla y le  añadí título, créditos, etc.

5. Exporté el documento en formato .svg. Este formato me dio problemas a la hora de subirlo a la web ya que los textos se salían de las cajas cuando se visualizaba desde un teléfono móvil. Asi que decidí exportar las tablas en formato .png para que no hubiera ese problema aunque perdiese algo de calidad.

## CREACIÓN PÁGINA WEB

1. Selección plantilla HTML5UP(https://html5up.net/) y descarga (https://html5up.net/spectral) en la carpeta que será el repositorio del tfm.

2. Vincular carpeta con github mpvdes desde la terminal.

3. Git init > git remote add juanlu1519 https://github.com/mpvdtfm-juanlu1519.git > git remote - v > git add . > git commit -m "descripcion" > git push --set-upstream juanlu1519 master

4. En github pages, indicamos la rama *master* ya que es dónde hemos subido nuestra web. Ahí mismo nos aparece el enlace de nuestra página.

### PÁGINA WEB

Foto Girona, Licencia Creative Commons de Reconocimiento y Compartir Igual, que permite compartir (copiar y distribuir) y adaptar (remezclar, transformar y construir a partir del material), incluso para fines comerciales. Autor: Vitaliy Krylov.


### Edición CSS

- Descarga fuente Calibri y vincularla al CSS.

- Personalización.

### SCROLLAMA

- Clonar repositorio


# IDEAS

- Aumento coste vivienda en la ciudad a raiz del turismo o nuevos vecinos.

- Los ciudadanos se benefician de este crecimiento económico? Distribución oferta turística. Quejas vecinos?

- Crecimiento servicios (transporte urbano, centros de salud, equipamientos deportivos, etc.) acorde al crecimiento de la ciudad?

- Nuevos puestos de trabajo de calidad?

- Causas aumento turismo (juego de tronos, ciclismo, futbol, baloncesto, clima)

- Planificación municipal o descontrolada?

- Voronoi centros salud

- Mejora indicadores economicos (PIB capita)

## BIBLIOGRAFÍA

## Pla estratègic turisme Girona (https://web.girona.cat/documents/20147/154626/Pla-Estrategic-Turisme-Analisi-i-Diagnosi.pdf)

### Context històric

- A	mitjans	del segle	XX,	s’inicia	un	nou	model	turístic,	conegut	en	la	història	del	turisme	com	a	model	
fordista,	 un	 model	 caracteritzat	 per	 l’homogeneïtzació	 de	 l’oferta	 i	 la	 demanda.	 Durant	 aquest	
període	es	popularitza	el	turisme	de	sol	i	platja,	i	això	provoca	que	la	ciutat	de	Girona	quedi	eclipsada	
pel	gran	pol	d’atracció	de	la	Costa	Brava.	En	conseqüència,	aquesta	pèrdua	de	centralitat	afecta	el	
turisme,	 però	 també	 a	 altres	 sectors	 econòmics.	 La	 ciutat	 de	Girona,	 acaba	 sent	 coneguda	 com	 la	
Girona	Gris,	una	ciutat	decadent,	amb	misèria	i	pobresa.	No	és	fins	a	la	dècada	dels	80,	que	Girona	
comença	 a	 recuperar	 la	 capitalitat	 administrativa,	 passant	 de	 la	 Gran	 Gerona a	 l’àrea	 urbana	 de	
Girona	(Oliver,	2000).	

- Pla	 Especial	 del	 Barri	 Vell	 (PERI). Aquest	pla	té	com	a	objectiu	recuperar	l’espai	emblemàtic	del	centre	històric	de	Girona	per	als	seus	
ciutadans.	Galí	 (2005)	descriu	el	Pla	Especial	del	Barri	Vell	com	la	plasmació	d’una	utopia	urbana,	i	
apunta	 les	 accions	 del	 pla	 que	 van	 tenir	 una	 major	 repercussió	 en	 el	 procés	 turístic	 posterior:	 la	
creació	 d’un	 espai	 viu,	 la	 rehabilitació	 de	 les	 cases	 de	 l’Onyar,	 el	 Passeig	 de	 les	 Muralles,	 la	
rehabilitació	 monumental	 i	 la	 dinamització	 comercial.	 El Pla	 Especial	 del	 Barri	 Vell,	 s’emmiralla	 en	
ciutats europees	que	havien	realitzat	una	rehabilitació	dels	seus	centres	històrics.	El	Pla	incentiva	una	
intervenció	estructural	al	barri,	començant	per	les	entranyes,	és	a	dir,	els	subterranis,	el	sistema	de	
clavegueres,	el	cablejat,	per	tal	de	solucionar	problemes	com	la	humitat,	i	seguidament	es	rehabiliten	
els	edificis	i	carrers.	Per	tant	s’intervé	en	el	conjunt	del	centre	històric,	millorant	l’espai	públic	per	tal	
que	 els	 particulars	 s’involucrin	 en	 la	 vida del	 barri.	 Aquesta	 millora	 dóna	 lloc	 a	 inversions	
d’immobiliàries,	ja	que	els	edificis	rehabilitats	del	barri	es	perceben	com un	nínxol	de	negocis	amb	un	
gran	potencial	(Nadal,	2003).

- 1985, Les Àligues i Sant Domènec passa a ser de l'Udg i es converteixen en facultats. Als pisos del barri arriben estudiants. (Nadal, 2003) diu que no suposa gentrificació perquè eren edificis buïts.

- Un	altre	espai,	que	en	aquell	moment	estava	tancat,	era	l’antic	hospital	militar,	que	es	reconverteix	
en	 l’actual	 Centre	 Cultural	 de	 la	Mercè.	 A partir	 de	 la	 rehabilitació	 d’aquest	espai,	es	 desenvolupa	
també	la	rehabilitació	del	passeig	de	la	muralla,	com	a	element	complementari	i	contingent	del	Pla	
Especial.	El	passeig	de	la	muralla,	permet	veure	la	ciutat	des	de	dalt	cap	a	baix,	oferint	un	mirador	
panoràmic	a	la	ciutat,	en	forma	de	camí	de	ronda.
Així	doncs,	el	Pla,	sense	ser un	pla	pròpiament	turístic,	acaba	afectant	decisivament	aquest	àmbit.	De	
manera	que	un	pla	pensat	per	la	rehabilitació	del	Barri	Vell, per	als	seus	ciutadans, acaba	creant	una	
ciutat	atractiva	pel	turisme.

- En	aquell	moment,	es	van	prendre	també	decisions	respecte	a	alguns	esdeveniments	de	la	ciutat.	Per	
exemple	 el	 manteniment	 de	 la	 Processó	 de	 Setmana	 Santa	 subvencionant	 una	 part	 de	 l’acte	
organitzat	per	la	Confraria	i	els	Manaies. O	bé,	la	 reconversió	de	Temps	de	Flors,	que	va	passar	de	
celebrar-se	en un	sol	espai	de	la	ciutat,	Sant	Pere	de	Galligants,	a	obrir-se	a	tot	el	barri,	obrint	espais	
com	patis	i	jardins	de	particulars.	Així	com	el	suport	a	la	creació	del	festival	Temporada	Alta,	festival	
d’arts	escèniques	que	ha	assolit	un	gran	reconeixement	en	els	darrers	anys,	fins	a	convertir-se	en	un	
festival	de	referència	de	la	ciutat.

- 1994, Pla Ciutat de Girona. Integra turisme en les estratègies que es proposen. la	ciutat	esdevingui	un	centre	de	 turisme	urbà	de	referència	europea, incentivant	 la	 creació	 d’una	 ciutat	 per	 a	 la	 ciutadania,	 un	 lloc	 per	 viure-hi,	 i	 conseqüentment	 una	
ciutat	 atractiva	 també	 pels	 seus	 visitants.  El	 Pla	 de	 Ciutat	 es	 caracteritza	 per	 la	 participació	 i	
implicació	de	la	ciutadania.	El	model	turístic	derivat	del	model	de	ciutat	que	es	defineix	en	el	Pla,	es	
caracteritza	 per	 la	 voluntat	 d’esdevenir	 una	 ciutat	 amb	 turistes,	 i	 no	 una	 ciutat	 pels turistes	
(Salamaña,	2017).

- Altres plans especifics (no turisme): Pla	 d’urbanisme	 (2010),	 Pla	estratègic	 de	 cultura	 (2010),	 Pla	 de	mobilitat	
(2014),	 Pla	 de	 promoció	econòmica	 (2015), Pla	Estratègic	 de	l’esport	 (2017),	entre	 d’altres.	A	més,	
actualment	 des	 de	 l’Àrea	 de	 Cultura	 de l’Ajuntament	 s’està	 treballant	 en	 l’elaboració	 del	 Mapa	
Cultural	de	la	ciutat.

- Finals anys 90: ’arribada	de	la	companyia	
de	 vols	 de	 baix	 cost	 Ryanair a	 l’Aeroport	 de	 Girona.	 La	 Diputació	 de	 Girona,	 va	 realitzar	 una	
important	inversió	a	l’Aeroport,	com	a	oportunitat	de	creixement	turístic	i	comunicació	per	la	Costa	
Brava.	 A	 partir	 d’aquest	 moment,	 comença un	 període	 d’esplendor	 per	 l’Aeroport	 de	 Girona,	
posicionat	amb	 viatges	 de	 curta	estada,	 i	 com	a	 Aeroport	 del	 nord	 de	 Barcelona	 i	 de	 baix	 cost.	Es	
constata	que, tot	i	que	la	majoria	de	passatgers	que	arribaven	a	Girona tenien	com	a	destinació	final	
la	ciutat	de Barcelona,	una	part	d’aquests	aprofitava	per	visitar	també	la	ciutat	de	Girona.	Uns	anys	
després,	Ryanair comença	a	operar	a	l’Aeroport	de	Barcelona,	suposant	aquest	fet	una	gran	pèrdua	
de	passatgers	a	l’Aeroport	Girona	– Costa	Brava.	

- 2006: Palau Congressos Girona. Actractiu per empreses.

- 2007-2010 : Pla	de	Foment	Girona	- Gironès	de	l’any	2007,	que	pretenia	diversificar	l’oferta	 turística	de	la	ciutat,	actuant	en	4	
àmbits:	 cultura,	 gastronomia,	 noves	 tecnologies	 i	 senyalització.

- El	 següent	 pas	 important	 va	 ser	 el	 pla	 de promoció	 de	 la	 ciutat	 iniciat	 el	 2012	 per	 fer	 de	
Girona	 una	 ciutat	 pels	 seus	 residents, i	 que,	 conseqüentment, esdevingués	 atractiva	 pels	
visitants.	

- Destinació Turisme Esportiu (DTE)

- Es	constaten	algunes	mancances	en	matèria	de	 gestió	integrada	i	planificada	del	turisme a	la	
destinació,	 així	 com	 de	 la	 manca	 de	 prou	 dades	 que	 permetin	 una	 adequada	 presa	 de	
decisions	turístiques	estratègiques	per	a	la	ciutat.

### Turisme

- Arrel	 d’aquesta	 idea,	 o	 canvi	 de	paradigma,	 han sorgit	nous	productes	o	models	d’oferta,	com	els	apartaments	turístics,	que	per	una	banda	satisfan	la	necessitat	 del	 turista	 de	 sentir-se	 com	 un	 local,	 però	 per	 altra	 banda,	 en	 algunes	 destinacions	 ha generat	 o	 comença	a	generar	 problemàtiques	 de	 convivència,	augment	 de	 preus	 dels	 habitatges,	 i	competència	deslleial	amb	altres	tipus	d’allotjaments	turístics.

- Un	altre	factor	rellevant	en	el	turisme	urbà,	és	el	desenvolupament	del	turisme	cultural	com	a	factor	
clau	per	la	conservació	i valorització	del	patrimoni	històric	i	cultural,	i	 també	el	 turisme	cultural	ha	
passat	a	entendre’s	de	manera	més	àmplia,	incorporant	altres	elements	de	l’oferta	cultural	com	la	
cultura	popular	o	els	esdeveniments,	que	 fan	que	aquest	tipologia	turística	esdevingui	dinàmica.	La	
gestió	passa	per	integrar	al	turista	a	la	cultura	local,	i	l’activitat	turística	a	la	planificació	urbana	de	la	
ciutat de	manera	sostenible.

- Creixement empreses relacionades amb el sector turístic, també les no turístiques. ((49,33%>35,80%)). En	el	marc	de	les	empreses	turístiques	de	la	ciutat,	el	sector	de	l’allotjament	és	el	que	té	un	
pes	 més	 important	 sobre	 el	 total	 de	 la	 facturació,	 representant	 el	 42,32%	 dels	 ingressos	
totals,	 seguidament	 de	 la	 restauració	 (23,77%),	 el	 transport	 (19,40%),	 les	 activitats	 d’oci	 i	
cultura	(8,19%)	i	les	agències	de	viatge	(6,31%).

### Demografia

- Tal com	s’indica	en	el	Pla	Estratègic	de	Promoció	Econòmica	de	Girona	(2015),	
el	creixement	 poblacional	 de	la	ciutat	 de	Girona	en	els	 darrers	anys	 ha	estat	 del	 32%,	 una	 taxa	 de	
creixement	superior	a	la	de	Catalunya	i	Espanya	durant	el	mateix	període	(2001-2014),	que	va	ser	del	
18,2%	i	el	13,7%	respectivament. Aquest	 creixement,	 no	es	 deu	exclusivament	a	la	
població	 natural,	 sinó també	 als	 moviments	 migratoris,	 població	 estudiantil,	 centralitat	 del	 sector	
econòmic	i	llocs	de	treball,	i	la	capacitat	d’atracció	de	la	ciutat	a	les	persones	de	la	resta	de	municipis. Dades IDESCAT 2016.

### Mobilitat

- l’autopista	 AP-7,	 i	 l’autovia	 A-2,	 però	 també	 compta	 amb	 altres	 vies	 supracomarcals	 com	 l’eix	
transversal	C-25	que	comunica	amb	la	Catalunya	central	i	Lleida,	la	C-65	i	la	C-35	que	comunica	cap	al	
sector	meridional	i	la	Costa	Brava	sud,	i	la	C-66,	amb	accés	cap	a Banyoles	i	Costa	Brava	centre.

- AVE i aeroport

- Mobilitat estudiants udg, 83% fora Girona (Taula 7 Estudi)

### Habitatges

- Molts habitants sense empadronar (26.000), suposarien prop de 126.000 habitants totals estimats.

- Cada cop menys habitatges buits.

- 28% habitatges de lloguer, inmigració i estudiants.(2011). El 2021, 30,9, 2n major de l'Estat després de BCN. (https://www.ine.es/prensa/censo_2021_jun.pdf)


# Memoria 2022 Ajuntament Gi

- L’Ajuntament de Girona va aprovar el novembre de 2021 una suspensió, d’un any, de les tramitacions
de comunicació d’habitatges d’ús turístic (HUTs) al Barri Vell i a una part del Mercadal, zona on hi ha
més concentració d’habitatges d’ús turístic. L’objectiu era estudiar un nou plantejament urbanístic que
reguli la implantació d’aquest tipus d’immobles.
Transcorregut l’any de suspensió, l’Ajuntament de Girona ha proposat limitar a un 15% el nombre
màxim d’habitatges turístics que hi pot haver a cada sector de la ciutat. La mesura s’ha fet a través
d’una modificació puntual del Pla General d’Ordenació Urbana (PGOU).
Amb aquesta limitació, a l’àmbit del Pla Especial del Barri Vell (zona que comprèn el Barri Vell i part del
Mercadal) ja no es podran admetre comunicats per a pisos turístics, atès que el sector ja supera el
llindar marcat. La proposta inclou l’àmbit del Pla Especial, que abasta més enllà del Barri Vell i també
comprèn les zones del Mercadal més pròximes, per evitar que augmenti la pressió de sol·licituds de
pisos turístics en els carrers adjacents al nucli antic com a efecte del topall establert.
Aquest topall del 15% tindrà una excepció en què sí que s’admetran comunicats tot i sobrepassar el
límit, en els casos en què hi hagi una gran rehabilitació d’un edifici sencer on el bloc es destini a
habitatge i l’obra incorpori criteris d’accessibilitat afegits, com la instal·lació d’un ascensor. En aquests,
es permetrà destinar la primera planta del bloc a habitatge d’ús turístic. L’objectiu és facilitar la
rehabilitació d’edificis sencers d’habitatges que d’altra manera difícilment serien objecte d’actuacions
de renovació d’aquesta envergadura.
La mesura ha estat implementada un cop s’ha disposat de l’estudi sobre l’impacte dels habitatges d’ús
turístic en el mercat de lloguer encarregat per l’Àrea de Promoció Econòmica l’any 2020. 

