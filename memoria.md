# Memoria del Trabajo de Fin de Máster ([MPVD](https://mpvd.es/))

Autor: [Juan Luis Monterroso Aranda](https://www.linkedin.com/in/jlmonterroso/)

## Agradecimientos

### Tutores

- Adolfo Antón: Por sus correcciones y aportaciones en todo el proyecto.

- Yolanda García: Por su ayuda con los notebooks de Python y los gráficos.

- Jesús David Navarro "Jesusda": Por sus anotaciones en materia de Software Libre y sus propuestas con las tablas.

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

1. Descarga del mapa de fondo (*barris.shp*) y los datos necesarios para representarlos (*vut13.csv* y *vut22.csv*). El archivo *barris.shp* lo obtuve de [Girona Open Data](https://www.girona.cat/opendata/dataset) y corresponde a la delimitación de los barrios de Girona. Los archivos .csv corresponden a las viviendas de uso turístico que había tratado y exportado en los notebook de Python. Los barrios tienen un color de relleno ```#eff6ff```.

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

4. Modifiqué la tabla y le añadí título, créditos, etc.

5. Exporté el documento en formato .svg. Este formato me dio problemas a la hora de subirlo a la web ya que los textos se salían de las cajas cuando se visualizaba desde un teléfono móvil. Asi que decidí exportar las tablas en formato .png para que no hubiera ese problema aunque perdiese algo de calidad.

#### Creación y publicación de la página web

Viendo ejemplos de trabajos anteriores me pareció buena idea publicar mi proyecto en una página web donde podría poner en práctica todo lo aprendido en HTML, CSS y Javascript.

Desde la creación hasta el producto final se siguieron los siguientes pasos:

1. Seleccioné la plantilla en [HTML5UP](https://html5up.net/) y descargué [la elegida](https://html5up.net/spectral) en la carpeta que sería el repositorio del TFM.

2. Vinculé la carpeta con el Github del [MPVD](https://github.com/mpvdes) desde la terminal:

```
Git init > git remote add juanlu1519 https://github.com/mpvdes/2022-2023-tfm-juanlu1519.git > git remote - v > git add . > git commit -m "descripcion" > git push --set-upstream juanlu1519 master
```

3. En Github Pages, indiqué la rama *master* ya que es dónde subí la web. Ahí mismo nos apareció el [enlace](https://mpvdes.github.io/2022-2023-tfm-juanlu1519/) de la página.

Una vez creada y publicada la web, empecé a modificar el archivo *index.html* para personalizarlo a mi gusto y el archivo *main.css* que proporciona la plantilla. Para añadir otros estilos y no tocar demasiado el archivo .css principal, creé el archivo *custom.css*. La fuente usada en la web es *Calibri*, que no es la predeterminada y hay que [descargarla](https://www.downloadfonts.io/download/calibri-font/?utm_content=cmp-true) e incorporarla al archivo *main.css* en los apartados donde se modifique la fuente de los textos.

La foto que se usa de encabezado tiene Licencia Creative Commons de Reconocimiento y Compartir Igual, que permite compartir (copiar y distribuir) y adaptar (remezclar, transformar y construir a partir del material), incluso para fines comerciales. Su autor es Vitaliy Krylov.

La parte de *Scrollama* se hizo clonando el [repositorio](https://github.com/russellsamora/scrollama) del autor y modificándolo según mis necesidades. También me sirvió de guía el proyecto [*La huella de las armas españolas en el mundo*](https://github.com/ojedadario/tfm-mpvd-armas-espana) del compañero de la anterior de edición del MPVD [Darío Ojeda](https://x.com/DarioOjeda). Asímismo, me fijé en el reportaje[*El dominio histórico de la derecha en Madrid: consigue la mayoría ganando solo en el 30% más rico*](https://www.eldiario.es/madrid/gana-derecha-elecciones-madrid-mayoritaria-30-rico_1_7347696.html) para modificar mis estilos.

## Trabajos relacionados

Los siguientes trabajos me sirvieron de inspiración para realizar mi proyecto:

- [Ciudad desigual](https://jllopc.github.io/ciudad.desigual/): en este trabajo de [Joan Llop](https://x.com/jouerl) se abordan las diferencias socioeconómicas que hay entre dos barrios de Madrid unidos por una línea de metro.

- [Efecto AIRBNB en Pamplona-Iruña](https://lab.montera34.com/airbnb/pamplona/): realizado por [Montera 34](https://x.com/montera34), en este proyecto se estudia el efecto de la presencia de alojamientos turísticos en Pamplona.

- [El caso Rubiales, la gota que ha colmado el vaso](https://www.elnacional.cat/es/sociedad/caso-rubiales-gota-colmar-vaso_1085964_102.html): de este reportaje realizado por [Laura Cercós](https://x.com/cercos_tuset) me llamó mucho la atención el *scrollytelling* y me habría gustado realizar algo similar.

- [*La huella de las armas españolas en el mundo*](https://github.com/ojedadario/tfm-mpvd-armas-espana): como he comentado anteriormente, el TFM del compañero de la anterior de edición del MPVD [Darío Ojeda](https://x.com/DarioOjeda) me inspiró a la hora de hacer la parte de *scrollama* y las diferentes secciones de la web.

- [*Forgotten Pandemics*](https://github.com/arantxaherranz/forgotten-pandemics): el proyecto de la compañera de la edición anterior del MPVD [Arantxa Herranz](https://x.com/aherranz) me sirvió de inspiración para enfocar las diferentes partes de la web y del repositorio de Github. Sobre todo me gustó la idea de añadir gráficos interactivos con Plotly y he intentado replicarlo lo mejor posible.

## Tecnologías y herramientas utilizadas

Todas las herramientas usadas para la elaboración del proyecto son FLOSS, es decir, *Free/Libre Open Source Software*:

- Para la extracción de datos se usó el paquete [Wget](https://www.gnu.org/software/wget/) de [Cygwin](https://www.cygwin.com/). 

- Para la limpieza y análisis de los datos se emplearon las librerías Numpy y Pandas de [Python](https://www.python.org/) y el *software* [OpenRefine](https://openrefine.org/). Los notebooks se realizaron con [Jupyter Notebook](https://jupyter.org/).

- Los gráficos se dibujaron con el paquete Plotly de Python y las tablas, con [LibreOffice](https://es.libreoffice.org/) e [Inkscape](https://inkscape.org/es/). 

- Las imágenes se editaron con [Gimp](http://www.gimp.org.es/) e Inkscape. 

- El mapa se realizó con el programa [QGIS](https://www.qgis.org/es/site/). 

- La redacción del proyecto y de la página web fue con [Emacs](https://www.gnu.org/software/emacs/). Con [Git](https://git-scm.com/) se realizó el control de versiones y la publicación del proyecto en Github.

## Fuentes de datos

Las bases de datos sobre las que se trabaja son oficiales, públicas y abiertas. Estas bases pertenecen a: 

- [Open Data Girona](https://www.girona.cat/opendata/): de esta base de datos obtuve los presupuestos de la ciudad, el archivo en formato .shp de la delimitación de los barrios de Girona y la lista de establecimientos dedicados a actividades comerciales.

- [L'Observatori](https://terra.girona.cat/apps/observatori/): de L'Observatori, observatorio de datos dependiente del ayuntamiento de Girona, obtuve recopilatorios referentes a la movilidad, equipamientos, situación social del municipio y evolución del precio de la vivienda.

- [Instituto Nacional de Estadística](https://ine.es/): del INE obtuve el histórico de empadronados de la ciudad. Sobre su estudio *Censo de Población y Vivienda* creé el archivo *viviendas-vacias.csv*.

- [Catastro](https://www.sedecatastro.gob.es/): con el paquete [Catastro Inspire](https://www.catastro.minhap.es/webinspire/index.html) disponible en QGIS pude recopilar los edificios de Girona en los años que necesitaba.

Asímismo, también consulté las siguientes bases de datos aunque no he incorporado ninguna de ellas al proyecto:

- [Dades obertes](https://governobert.gencat.cat/ca/dades_obertes/inici/): catálogo de datos abiertos de la Generalitat de Catalunya.

- [Idescat](https://www.idescat.cat/emex/?id=170792): en el Institut d'Estadística de Catalunya hay datos referentes a la población, elecciones, medio ambiente y lengua, entre otros.

- [Idealista](https://www.idealista.com/sala-de-prensa/informes-precio-vivienda/alquiler/cataluna/girona-provincia/girona/): me interesaba conocer la evolución del precio de la vivienda en Girona pero, finalmente, encontré una [base de datos](https://terra.girona.cat/apps/observatori/indicadors/urbanisme-i-habitatge/habitatge/renda-mitjana-dels-contractes-de-lloguer/) oficial, pública y abierta que me aportaba un enfoque similar.

- [Epdata](https://www.epdata.es/datos/datos-graficos-estadisticas-municipio/52/girona/3468): este portal del grupo Prensa Ibérica recopila diferentes gráficos sobre la ciudad en materia demográfica, económica, laboral, etc. Si me interesó algún dato, recurrí a la fuente oficial.

## Métodos y técnicas

A la hora de realizar este proyecto me fue muy útil documentar todo el proceso a medida que iba avanzando en él. Al ser un trabajo que se extendió durante varios meses, con sus pausas y sus complicaciones, tener los últimos pasos documentados me ayudó a volver a situarme en todo momento. Además, una buena documentación del proceso sirve para que quien quiera pueda usar los recursos que pongo a su disposición para inspirarse o mejorar el resultado.

El hecho de que todas las herramientas usadas sean *Software Libre* me permitió encontrar mucha información cuando he tenido problemas y dudas sobre su uso. La propia documentación de la herramienta en cuestión o los foros del estilo [Stackoverflow](https://stackoverflow.com/) me han sido de gran utilidad.

## Resultados

Los resultados de este trabajo de fin de máster están recopilados en el siguiente repositorio de Github:

https://github.com/mpvdes/2022-2023-tfm-juanlu1519

En el repositorio encontramos las siguientes carpetas y archivos:

- https://mpvdes.github.io/2022-2023-tfm-juanlu1519/ : enlace a la página web que muestra el TFM con gráficos, mapas, tablas, etc.

- Archivo *readme.md*: archivo dónde se explica todo lo que podemos encontrar en el repositorio del proyecto.

- Archivo *memoria.md*: esta memoria la podemos encontrar en el repositorio Github del TFM.

- Archivo *index.html*: es la página predeterminada de la página web del trabajo.

- Carpeta *assets*: aquí encontraremos, divididos en subcarpetas, los archivos .css y .js necesarios para que funcione la página web.

- Carpeta *images*: todas las imágenes que han resultado de la elaboración de este proyecto las encontraremos en esta carpeta. Podemos encontrar gráficos interactivos en formato .html, mapas en formato .png, imágenes en formato .svg y .jpg y tablas en formato .png y .svg.

- Carpeta *data*: las bases de datos que se han usado para realizar el proyecto se encuentran en esta carpeta.

- Carpeta *notebooks*: aquí encontramos los documentos en formato .ipynb dónde se hace el tratamiento de los datos y se crean los gráficos estáticos e interactivos.

## Conclusiones

Este es un proyecto al que le tuve que dedicar muchas horas en informarme sobre el tema, recopilar datos, tratarlos, visualizarlos y documentar todo el proceso. Fue un gran aprendizaje y estoy orgulloso del resultado. Mejoré mis habilidades en el tratamiento de bases de datos, en la realización de mapas e infografías y en la creación de páginas web.

También me encontré con dificultades a la hora de hacer el trabajo. Me vi obligado a recurrir a foros, documentación y tutoriales para usar diferentes herramientas. También tuve que consultar a diferentes profesores del MPVD para que me ayudasen cuando me encontraba atascado. 

Las bases de datos también me han dado problemas. Algunas no eran tan ricas como yo esperaba (elementos vacíos o nulos) o tenían varios errores de precisión con los datos. Basarme en una ciudad como Girona ha tenido la ventaja de encontrar información que en un municipio pequeño sería prácticamente imposible de encontrar pero, por otro lado, me han faltado ciertas bases de datos que en una ciudad como Barcelona o Madrid me habría sido más fácil de obtener. 

En lo referente al contenido de *Girona, una ciudad en transformación*, realizando el trabajo conocí la historia contemporánea de mi ciudad. A su vez, los datos me mostraron la situación actual de la ciudad, la evolución durante los últimos años y las partidas que se dedican en los presupuestos a diferentes departamentos.

Antes de hacer el trabajo tenía la idea de que en Girona lo único que había cambiado en los últimos años eran las políticas públicas enfocadas en favorecer el turismo. Sin embargo, los datos no me han mostrado solo eso:

- Las partidas presupuestarias dedicadas al turismo han aumentado. Sin embargo, son practicamente irrelevantes comparadas con las dedicadas a movilidad, servicios sociales y cultura.

- La población en la ciudad ha aumentado. Es un hecho evidente pero pude observar las causas y las consecuencias de este crecimiento demográfico.

- La ciudad mejoró en materia de movilidad, adaptándose al crecimiento comentado, pero mantiene prácticamente los mismos equipamientos urbanos.

- Aunque en la ciudad hay menos tasa de paro que en años anteriores, las desigualdades han aumentado y hay más familias pasando apuros.

- Existe un problema con el acceso a la vivienda. Cada vez hay menos vivienda vacía y los pisos turísticos han aumentado, masificando el centro histórico de Girona. Desde el consistorio se está interviniendo pero las plataformas ciudadanas consideran las medidas insuficientes.

## Bibliografía

En este apartado se indican las diferentes fuentes consultadas para la realización de este trabajo. No se recoge la documentación propia de cada herramienta utilizada ni las soluciones encontradas en foros:

[Ciudad desigual](https://jllopc.github.io/ciudad.desigual/)

[Efecto AIRBN en Pamplona-Iruña](https://lab.montera34.com/airbnb/pamplona/)

[*El turismo de bicicleta sacude Girona tras el letargo pandémico* - La Vanguardia](https://www.lavanguardia.com/local/girona/20220606/8318585/turismo-bicicleta-sacude-girona-letargo-pandemico.html)

[*Girona fixa un topall màxim del 15% de pisos turístics a cada barri* - Diari de Girona](https://www.diaridegirona.cat/girona/2022/11/08/girona-fixa-topall-maxim-15-78281951.html)

[Indicadors turístics de la ciutat de Girona](https://web.girona.cat/promocio/observatori/indicadorsturistics)

[*L’Ajuntament de Girona establirà un topall global del 4% d’apartaments i d’habitatges d’ús turístic al municipi* - Ajuntament de Girona](https://web.girona.cat/noticies?id=11675058)

[*Los pisos turísticos pagarán un impuesto extraordinario en Portugal* - El País](https://elpais.com/economia/negocios/2023-07-29/portugal-gravara-los-pisos-turisticos-con-un-impuesto-extraordinario-y-veta-nuevas-licencias.html)

[Pla Estratègic de Turisme de Girona](https://web.girona.cat/promocio/platurisme)

[Pla Local per l'Habitatge de Girona](https://web.girona.cat/omh/plahabitatge)

[Twitter(X) Més Barri Girona](https://twitter.com/MesBarriGirona/status/1702787180182081778)

[*Un estudio revela las razones por las que Girona es un destino de éxito para el ciclismo de carretera* - La Vanguardia](https://www.lavanguardia.com/local/girona/20220922/8539118/estudio-revela-razones-pora-girona-destino-exito-ciclismo-carretera.html)

