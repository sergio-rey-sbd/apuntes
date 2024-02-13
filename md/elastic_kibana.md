---
title: Kibana 
description: Kibana. Framework visual de elastic stack
permalink: /kibana/
---

<h1>Kibana</h1>

<div align="center">
    <img src="../img/ELK/KibanaLogo.png" alt="Logo Kibana" width="15%" />
</div>

<h3>Tabla de contenidos</h3>


# ¿Qué es `kibana`?

`Kibana` es una herramienta de visualización de datos y análisis para Elasticsearch. Forma parte del Elastic (Elasticsearch, Logstash, Kibana) y se utiliza comúnmente para explorar, visualizar y analizar datos almacenados en Elasticsearch.

Algunas características principales de Kibana son:

- **Exploración de Datos:** Kibana permite a los usuarios explorar grandes volúmenes de datos almacenados en Elasticsearch mediante la realización de consultas y filtros de búsqueda avanzados.

- **Visualizaciones Interactivas:** Proporciona una variedad de opciones de visualización, como gráficos de barras, gráficos circulares, mapas, series de tiempo, etc., que pueden ser personalizados y configurados para mostrar datos de manera clara y comprensible.

- **Dashboards Personalizados:** Permite a los usuarios crear dashboards personalizados que combinan múltiples visualizaciones en una sola página para obtener una visión general completa de los datos.

- **Herramientas de Análisis:** Kibana ofrece herramientas de análisis como agregaciones, métricas y filtros que permiten a los usuarios realizar análisis de datos avanzados para descubrir patrones, tendencias y anomalías en los datos.

- **Gestión de Usuarios y Permisos:** Proporciona capacidades de autenticación y autorización para gestionar el acceso de los usuarios a los datos y las funcionalidades de Kibana.

- **Integración con Elasticsearch:** Está estrechamente integrado con Elasticsearch, lo que facilita la visualización y el análisis de los datos almacenados en los índices de Elasticsearch.


<div align="center">
    <img src="../img/ELK/ELK61.png" alt="ELK - Kibana" width="40%" />
</div>

Para nosotros en concretos, Kibana representa el framework visual de elasticsearch que nos permitirá: 
- Dar forma a los datos almacenados en Elasticsearch
- Crear objetos visuales a partir de los índices llamados **indexPattern**
- Crear *Visualizaciones*
- Crear **Dashboards** a partir de las *Visualizaciones*


# Primera visualización de datos en Kibana. `data view` y `discover`

Para visualizar datos en Kibana, en primer lugar debemos habilitar un índice de elasticsearch (en nuestro caso el de *restaurantes*) para poder ser tratado desde kibana. Esto se hace creando un **Data View** (anteriormente *index pattern*)

Un **Data View** en Kibana se refiere al proceso de explorar, visualizar y manipular datos almacenados en Elasticsearch utilizando las herramientas y funcionalidades proporcionadas por la plataforma. Esto incluye la configuración de index patterns, la creación de visualizaciones y dashboards, y la realización de análisis de datos para extraer información significativa de los datos.

Para gestionar los **Data Views**, vamos en la interface de Kibana a buscar la entrada de `Stack Management` dentro de la sección `Management` (parte inferior del menú)

<div align="center">
    <img src="../img/ELK/ELK62.png" alt="ELK - Kibana" width="30%" />
</div>

Desde este punto podemos administrar nuestras instalación de Elastic y Kibana, por ejemplo en la sección de `Data` podemos ver la gestión de todos los índices en `Index Management`

En las sección de `kibana`, tenemos como primera opción `Data Views` donde podemos crear un nuevo *Data View* seleccionando sobre el botón de ***Create Data View*** y aparece una ventana para la creación del *Data View* o ***Index Patern***.

Completamos el nombre del *Data View*, indicamos el índice y si este índice tiene un campo de tipo fecha, lo seleccionamos:

<div align="center">
    <img src="../img/ELK/ELK63.png" alt="ELK - Kibana" width="50%" />
</div>

Este ***Data View*** o ***Index Partern*** es un mapeo de nuestro índice que lo prepara para poder trabajar con el desde Kibana.

<div align="center">
    <img src="../img/ELK/ELK64.png" alt="ELK - Kibana" width="50%" />
</div>

Llegados a este punto, ya podemos hacer una primera visualización de los datos de nuestro índice, para ello, volvemos sobre el menú principal y pulsamos sobre el ítem `Discover` de la sección de `Analitics`.

<div align="center">
    <img src="../img/ELK/ELK65.png" alt="ELK - Kibana" width="50%" />
</div>

En nuestro caso, como solo tenemos este *Index Pattern* directamente ya nos salen datos del índice. En caso de que no saltan, entonces deberemos cambiar el intervalo de fechas (**4**)en los cuales buscar, puesto que por defecto solo muestra los últimos 15 minutos.

Una vez ya visualizamos datos, podemos crear vistas seleccionando los datos o filtros que aparecen a la izquierda, se puede reordenar estas vistas e incluso guardar.

También podemos exportar los datos del reporte seleccionando `share` y `CSV Reports`, entonces nos generará un fichero *csv* al que podemos acceder desde el menú general, `stack management` y `reporting`


# Visualizaciones en `kibana`

Antes de crear un cuadro de mandos o ***dashboard*** necesitamos crear **visualizadores** que son los elementos que después incrustaremos en los cuadros de mando.

Para acceder a los **visualizadores** debemos ir al menú principal, después `Analytics` y seleccionamos `Visualize library`.

A partir de aquí crear visualizadores.

En la documentación de `kibana` tenemos un tutorial: [Create your first dashboard](https://www.elastic.co/guide/en/kibana/current/create-a-dashboard-of-panels-with-web-server-data.html).

Respecto a nuestro ejemplo de *restaurantes* podemos crear varios visualizadores.

Para crearlo, al pulsar el botón de "Create Visualization" nos aparece una pantalla donde podemos elegir el tipo visualización. Tradicionalmente se ha utilizado la opción de `Aggregation Based`, aunque la última versión a añadido la opción de `Lens`

<div align="center">
    <img src="../img/ELK/ELK66.png" alt="ELK - Kibana" width="50%" />
</div>

Una vez ahí, silenciamos el tipo de visualizador a realizar: 

<div align="center">
    <img src="../img/ELK/ELK70.png" alt="ELK - Kibana" width="50%" />
</div>

Veamos varios ejemplos.

- **Tipo Métrica**, que nos cuenta la cantidad de reseñas (entre las fechas seleccionadas)

<div align="center">
    <img src="../img/ELK/ELK66.png" alt="ELK - Kibana" width="50%" />
</div>


- **Tipo Barra**: Creamos un visualizador que muestra la cantidad de reseñas según el rango de precios. Para ello seleccionamos en ***Buckets*** (divisiones) una agrupación por un termino (***terms***) sobre el campo *PRECIO*

<div align="center">
    <img src="../img/ELK/ELK67.png" alt="ELK - Kibana" width="50%" />
</div>

Cuando guardamos el visualizador, nos pregunta si lo queremos añadir a un *dashboard* existente o lo dejamos en la librería.

<div align="center">
    <img src="../img/ELK/ELK68.png" alt="ELK - Kibana" width="30%" />
</div>

- Gráfico tipo **area**

Seleccionamos el tipo *data histagram* y a partir de ahi jugamos con los elementos que queramos. Nos mostrará una gráfica de las reviews por fecha

<div align="center">
    <img src="../img/ELK/ELK71.png" alt="ELK - Kibana" width="30%" />
</div>

- Horizontal bar afectado por un **Filtro**.

Seleccionamos termino, especialidad y después aplicamos un filtro.

<div align="center">
    <img src="../img/ELK/ELK72.png" alt="ELK - Kibana" width="30%" />
</div>