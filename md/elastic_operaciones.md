

# Primeros pasos

- Introducimos un fichero JSON en un índice.
- Este fichero es lo que se llama un **documento**, que se indexa dentro de un índice
- Los **indices** son independiente uno de otros, no se pueden hace ***joins*** entre diferentes índices.
- Para indexar un documento, se hace mediante una api de índice, mediante un `PUT`o un `POST`

- Cuando hacemos la primera ingesta en un indice, elastic define automáticamente 


## Operaciones básicas

- **Creación de un índice con `PUT`**
```php
PUT mi_indice
```

- **Eliminar un índice con `DELETE`**
```yml
DELETE mi_indice
```

- **Creación de un índice con `POST`**
```yml
POST mi_indice/_doc
{
    "Nombre": "Julian",
    "Apellido": "Juli Joli",
    "Edad": 25
}
```
En este caso, se crea el índice exactamente igual que con `PUT` de forma implicita. Con `PUT` podemos especificar la forma del índice y con `POST` elastic decide qué datos se desean introducir.

- **Consulta de los datos de un índice**
```yml
GET mi_indice/_search
```
Obtenemos todos los registros del índice. Posteriormente profundizaremos sobre esta opción que es la más potente de elastic



- **Introducimos un documento con un índice concreto**
```yml
POST mi_indice/_doc/1
{
    "Nombre": "Pedro",
    "Apellido": "Pedrito Pedrete",
    "Edad": 24
}
```
Asignamos un `id` específico a este documento

- **Modificación de un documento por índice**
```yml
POST mi_indice/_doc/1
{
    "Nombre": "Juan",
    "Apellido": "Juanito Juante",
    "Edad": 26
}
```
En este caso, machacamos el registro anterior con esta nuevo.

- **Actualización mediante `_update`**
```yml
POST mi_indice/_update/1
{
  "doc" : 
  {
    "edad": "62"
  }
}
```
Utilizando `_update` podemos actualizar un campo del documento, en este caso referenciado por un `id`

```yml
POST mi_indice/_update/1
{
  "doc" : 
  {
    "Localidad": "Xativa"
  }
}
```
Observar el resultado, añadimos un nuevo campo sobre el documento existente.

- **Eliminar un documento concreto por `id`**
```yml
DELETE mi_indice/_doc/1
```
Eliminamos selectivamente el documento. Observar el `_doc`

## El método `_bulk`

### Ingestión de documentos masiva

Este método nos permite ingestar mas de un documento de una única vez

```yml
POST mi_indice/_bulk
{"index":{"_id":3}}
{"Nombre":"Evaristo","Apellido":"Evarist Evaristate","Edad":16}
{"index":{"_id":4}}
{"Nombre":"Dorotea","Apellido":"Dori Dorita","Edad":19}
{"index":{"_id":5}}
{"Nombre":"Hortensia","Apellido":"Hori Hortensi","Edad":26}
```
Introduce los tres registros simultáneamente. Observar que se especifica el `id` y que se omite el `_doc`

```yml
POST mi_indice/_bulk
{"index":{}}
{"Nombre":"Lola","Apellido":"Lolita Loleira","Edad":20}
{"index":{}}
{"Nombre":"Silvino","Apellido":"Silva Silvando","Edad":21}
{"index":{}}
{"Nombre":"Torcuato","Apellido":"Torcu Torcu","Edad":22}
```
En este caso, se inserta, pero ahora el `id` se genera automáticamente.

y esto que viene a continuación, también funciona:

```yml
POST mi_indice/_bulk
{ "index":{"_id":10} }
{ "name":"john doe","age":25 }
{ "index":{"_id":11} }
{ "name":"mary smith","age":32 }
```
Otros campos, y sin problemas

### y mas cosas: añadir, actualizar y borrar

Veamos el siguiente ejemplo, donde `_bulk` realiza varias operaciones de una única vez:

```yml
POST mi_indice/_bulk
{ "index":{"_id":3}}
{ "Apellidos":"Evar Eviris","age":26}
{ "delete":{"_id":4}}
{ "update":{"_id":10}}
{ "doc": {"name":"John Doe","age":26}}
{ "create":{"_id":8}}
{ "Nombre":"Gervasio","Apellidos":"Ger Gervi","age":22}
{ "create":{}}
{ "Nombre":"Tomasa","Apellidos":"Tomi Toma","age":23}
```

Como se puede ver, en una misma ejecución, hemos realizado
- Una actualización del `id` 3
- Un borrado del `id` 4
- Una actualización del `id` 10
- Una inserción del `id` 10
- Una inserción con un `id` automático
Observar que cada uno de estos elementos tiene una respuesta en su ejecución.

### Usando `_bulk` para operaciones masiva

Podemos tener fichero tipo `json` con un listado de operaciones como las anteriores y lanzarlos directamente sobre elastic, de forma que realizará todas las operaciones simultáneamente:

Dado un fichero llamado [vehiculos_aux.json](../files/vehiculos_aux.json), su ingesta se realizaría desde la línea de comandos, ya que no hay forma de hacerlo desde la interface de `kibana`.

El comando para tal efecto sería: 

```bash
curl --cacert http_ca.crt -u elastic:$ELASTIC_PASSWORD https://localhost:9200/_bulk -H "Content-type: application/json" --data-binary @vehiculos_aux.json 
```
<div align="center">
    <img src="../img/ELK/ELK28.png" alt="ELK" width="50%" />
</div>

Volvemos a la interfaz y si tecleamos 

```yml
GET vehiculos_test/_search
```
Obtendremos un resultado similar al siguiente, donde podemos ver que se ha creado un índice con más de 10000 registros, llamado *vehiculos_test", tal y como se especificaba en el fichero

<div align="center">
    <img src="../img/ELK/ELK29.png" alt="ELK" width="30%" />
</div>

Para mas información en [documentación oficial de elastic del API de Bulk](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-bulk.html)

También existen implementaciones en *python*, *perl*, *javascript* y otro lenguajes para pasar un fichero JSON a un fichero preparado para ser tratado con `_bulk`ç

# El método `GET`

El método `GET` en Elasticsearch se utiliza principalmente para realizar operaciones de lectura y recuperación de datos. 

En apartados anteriores hemos visto como la API `GET` también se puede utilizar para obtener información sobre el estado del ***cluster***, ahora veremos cómo recuperar documentos individuales, realizar búsquedas, obtener información sobre los mappings de índice y otros fines de lectura.

A continuación, se presentan algunos ejemplos de cómo se puede utilizar el método GET en Elasticsearch:

- **Recuperar un documento por su ID:**
```yaml
GET mi_indice/_doc/1
```
Esta solicitud recupera un documento específico de un índice por su ID.

- **Obtener información sobre un índice:**
```yaml
GET mi_indice
```
Esta solicitud devuelve información sobre un índice específico, incluidos los mappings, la configuración y la cantidad de documentos.

- **Realizar una búsqueda:**
```yaml
GET mi_indice/_search
```
Esta solicitud realiza una búsqueda en un índice específico y devuelve los documentos que coinciden con los criterios de búsqueda especificados.

Más información sobre el [API `_search` en la documentación oficial de elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-search.html)

Observar el encabezado donde se muestran por ejemplo la cantidad de registro con `value` y la exactitud de este valor mediante `relation`, así un `eq` indica un valor exactos, `gte` más de las indicadas... 

Así, en el ejemplo del apartado anterior, al ejecutar la consulta del índice importado

```yml
GET vehiculos_test/_search
```
el resultado es el siguiente, donde indica que hay más de 10.000 registros, y cómo podemos ver en el resultado si lo ejecutamos, sólo nos muestra unos 10 registros, o sea, no los muestra todos. Esto se hace por cuestiones de optimización.

<div align="center">
    <img src="../img/ELK/ELK30.png" alt="ELK" width="30%" />
</div>

Si dentro de la búsqueda incluimos el siguiente JSON indicando `track_total_hits`, entonces nos indicará exactamente la cantidad de registros. Ahora Elastic se tomará su tiempo, para calcular la cantidad exacta de registros, cosa que antes no ha hecho 

```yml
GET vehiculos_test/_search
{
  "track_total_hits": true
  "size": 5000
}
```

En el caso anterior, hemos añadido que nos muestre 5000 registros.

<div align="center">
    <img src="../img/ELK/ELK32.png" alt="ELK" width="30%" />
</div>

En este caso, se obtienen 5000 registros, pero por contra se han utilizado 25ms para obtener estos datos. Por este motivo, elastic esta preparado para ofrecer como máximo 10.000 documentos. Existe otra [API llamada `scroll`](https://www.elastic.co/guide/en/elasticsearch/reference/current/scroll-api.html) que permite recuperar todos los documentos, pero en bloques limitados, de forma que cada petición nos ofrece una cantidad de todos ellos.


- **Obtener información sobre el cluster:**
```yml
GET /_cluster/state
```
Esta solicitud devuelve información sobre el estado actual del cluster, incluidos los nodos, los shards y la configuración.


- **Obtener información sobre nodos individuales:**
```yml
GET /_nodes
```
Esta solicitud devuelve información sobre todos los nodos en el cluster, incluyendo estadísticas de uso de recursos y configuración.

**Obtener información sobre mappings de índice:**
```yml
GET mi_indice/_mapping
```
Esta solicitud devuelve el mapping de un índice específico, que describe la estructura de los documentos en el índice.

O sea, vemos los campos y la tipificación de datos establecida.

<div align="center">
    <img src="../img/ELK/ELK31.png" alt="ELK" width="30%" />
</div>

Como se puede ver en la captura anterior aparecen todos los campos introducidos en los diferentes documentos de introducidos en el índice, y su tipificación básica.

# Consulta de datos. 

## Un poco de teoría

Elastic hace una búsqueda indexada de los elementos, por lo que a la hora de responde puede devolver respuesta ordenadas de forma más o menos acertada

<div align="center">
    <img src="../img/ELK/ELK33.png" alt="ELK" width="40%" />
</div>


En Elasticsearch, al igual que en otros motores de búsqueda, se utilizan varios conceptos importantes para evaluar y medir el rendimiento de las consultas. Estos conceptos incluyen la relevancia, la precisión y el recall. Aquí tienes una descripción de cada uno de ellos:

1. **Relevancia:**
   - La relevancia se refiere a la medida en que los resultados devueltos por una consulta son pertinentes o adecuados para la intención del usuario.
   - En el contexto de Elasticsearch, la relevancia se determina mediante un algoritmo de puntuación que asigna una puntuación de relevancia a cada documento en función de su similitud con los términos de búsqueda y otros factores como la frecuencia de los términos, la longitud del documento, etc.
   - Elasticsearch utiliza el modelo de puntuación TF-IDF (Term Frequency-Inverse Document Frequency) como uno de los factores para calcular la relevancia de los documentos.

2. **Precisión:**
   - La precisión se refiere a la proporción de documentos relevantes entre todos los documentos devueltos por una consulta.
   - En otras palabras, la precisión mide qué tan útiles son los resultados devueltos por una consulta en relación con la cantidad total de resultados.
   - Una alta precisión significa que la mayoría de los documentos devueltos son relevantes para la consulta, mientras que una baja precisión indica que muchos de los documentos devueltos son irrelevantes.

3. **Recall:**
   - El recall, también conocido como exhaustividad, se refiere a la proporción de documentos relevantes recuperados por una consulta en relación con todos los documentos relevantes en la colección.
   - En otras palabras, el recall mide qué tan bien una consulta recupera todos los documentos relevantes en el conjunto de datos.
   - Un alto recall significa que la mayoría de los documentos relevantes se recuperan en la consulta, mientras que un bajo recall indica que muchos documentos relevantes se pierden.


<div align="center">
    <img src="../img/ELK/ELK34.png" alt="ELK" width="35%" />
</div>

Elasticsearch utiliza una puntuación (***score***) para determinar la clasificación de documentos coincidentes


## Consultas DSL
Vamos a ver cómo podemos lanzar diferentes tipos de Query para obtener los registros que mas relevancia tienen para nosotros, para ello vamos a utilizar el índice que obtendremos de la ingesta del fichero [restaurantes_es.json](../files/restaurantes_es.json) 

```bash
curl --cacert http_ca.crt -u elastic:$ELASTIC_PASSWORD https://localhost:9200/_bulk -H "Content-type: application/json" --data-binary @restaurantes_es.json 
```

Una vez introducidos los datos, verificamos y revisamos su estructura:


```yml
GET restaurantes/_search
```

Las consultas DSL nos permiten realizar consultas con un formato JSON.

### `match`

El primer tipo de consulta que vamos a utilizar es el `match query`

<div align="center">
    <img src="../img/ELK/ELK41.png" alt="ELK" width="70%" />
</div>

Así pues, al ejecutar la siguiente consulta para buscar "*Cocina Tradicional*", obtendremos los siguientes registros:

```yml
GET restaurantes/_search
{
  "size":50,
  "query":{
    "match": {
      "DESCRIPCION": "cocina tradicional"
    }
  }
}
```
Como se puede observar, la consulta ha tenido éxito, ha obtenido un total de 17 registros y podemos observar en los registros del resultado que contiene en la *descripción* el literal buscado.

> **Nota**: se ha especificado un `"size":50` porque como por defecto solo muestra los 10 primeros documentos, para que los muestre todo, en este caso serán 17

<div align="center">
    <img src="../img/ELK/ELK42.png" alt="ELK" width="70%" />
</div>

En los últimos registros podremos ver que exactamente no obtenemos el literal "*Cocina Tradicional*"

Esto es porque realmente ha hecho un ***or lógico*** entre *cocina* y *tradicional*.

Si queremos afinar más la búsqueda y queremos exigir que existan los dos terminos, entonces necesitamos el ***operador lógico and*** de la siguiente manera

```yml
GET restaurantes/_search
{
  "size":50,
  "query":{
    "match": {
      "DESCRIPCION": {
        "query": "cocina tradicional",
        "operator": "and"
    }
  }
}
```

Ahora nos responde 8 registros y veremos que en todos exige las dos palabras, aunque puede que no se encuentren de forma consecutiva.

Otra forma de obligar a la consulta a un mínimo de coincidencia es mediante el operador `minimum_should_match` donde es especifica que como mínimo de todas las palabras a buscar, se deben encontrar una cantidad mínima de ellas. 

Veamos el ejemplo buscando "*cocina tradicional canaria*"

```yml
GET restaurantes/_search
{
  "query":{
    "match": {
      "DESCRIPCION": {
        "query": "cocina tradicional canaria",
        "minimum_should_match": 2
      }
    }
  }
}
```

En este caso, nos devuelve 8 registros. 

Observar que tenemos una puntuación para cada uno de los documentos obtenidos en la búsqueda identificada por el campo `max_score`

<div align="center">
    <img src="../img/ELK/ELK43.png" alt="ELK" width="50%" />
</div>

Así pues, `max_score` es un campo que se devuelve en los resultados de una consulta de búsqueda y que indica la puntuación máxima de relevancia entre todos los documentos recuperados por esa consulta. Este campo se utiliza para proporcionar una medida relativa de la relevancia de los documentos devueltos en comparación con otros documentos en el conjunto de resultados.

El valor de `max_score` es útil para los usuarios y los desarrolladores de aplicaciones para comprender la distribución de relevancia en los resultados de la búsqueda y para determinar la importancia relativa de los documentos devueltos. También puede ser utilizado para normalizar las puntuaciones de relevancia de otros documentos en el conjunto de resultados, si es necesario.

Básicamente depende de 3 factores:

- **Frecuencia del termino**: Cuanto más aparece un termino en un campo, más puntúa.
- **Frecuencia inversa del documento**: Cuanto más documentos contienen el termino, menos importante es.
- **Longitud del campo**: Los campo más cortos son más relevantes que los largos.

### `match_phrase`

Para **buscar frase** y no términos separados utilizamos el operados `match_phrase`

<div align="center">
    <img src="../img/ELK/ELK44.png" alt="ELK" width="70%" />
</div>

Entonces, si buscamos el literal exacto

```yml
GET restaurantes/_search
{
  "query":{
    "match_phrase": {
      "DESCRIPCION": {
        "query": "cocina tradicional"
      }
    }
  }
}
```

En este caso nos devuelve solo 7 registros. Si buscamos la canaria, nos reduce la cantidad de elementos encontrados.

De las misma forma que el `minimum_should_match` nos introducía una variación sobre una búsqueda normal con `match`, ahora tenemos el parámetro de `slop` que nos indica el número de términos que esperamos encontrar mínimo de entre todos los términos indicados. 

O sea, con la siguiente búsqueda:

```yml
GET restaurantes/_search
{
  "query":{
    "match_phrase": {
      "DESCRIPCION": {
        "query": "cocina tradicional",
        "slop": 10
      }
    }
  }
}
```

Permitimos que haya hasta **10 palabras** entre "*cocina*" y "*tradicional*" puesto que el `slot` tiene un valor de 10. Si lo cambiamos a 1 por ejemplo, permitiría encontrar el literal "*cocina canaria tradicional*" pero no el de "*cocina procedente de canarias tradicional*" puesto que tiene más términos entre los dos indicados.

### `range`

Las **consultas de rangos** son adecuadas para hacer consultas numéricas y especialmente de fechas.

Elastic permit el uso de **Date math** que es un lenguage *user fiendly* que nos permite especificar fechas una forma más lógica y sencilla de entender.

Per ejemplo, la siguiente consulta:

```yml

GET restaurantes/_search
{
  "query":{
    "range": {
      "FECHA_MODIFICACION": {
        "gte": "2024-02-11",
        "lte": "2024-08-11"
      }
    }
  }
}
```

es similar a 

```yml
GET restaurantes/_search
{
  "query":{
    "range": {
      "FECHA_MODIFICACION": {
        "gte": "now-6M"
      }
    }
  }
}
```

Ejemplo de uso de **Date math** usando la fecha de hoy:

- **Búsqueda de documentos desde la fecha de hoy hasta hace una semana:**

```yml
{
  "query": {
    "range": {
      "fecha": {
        "gte": "now-1w/d",
        "lte": "now/d"
      }
    }
  }
}
```

Esto buscará documentos con un campo "fecha" dentro del rango de hace una semana hasta la fecha actual.

- **Búsqueda de documentos desde el comienzo del mes actual hasta la fecha de hoy:**

```yml
{
  "query": {
    "range": {
      "fecha": {
        "gte": "now/M",
        "lte": "now/d"
      }
    }
  }
}
```

Esto buscará documentos con un campo "fecha" dentro del rango desde el primer día del mes actual hasta la fecha actual.

- **Búsqueda de documentos desde la fecha de hoy hasta hace tres meses:**

```yml
{
  "query": {
    "range": {
      "fecha": {
        "gte": "now-3M/d",
        "lte": "now/d"
      }
    }
  }
}
```

Esto buscará documentos con un campo "fecha" dentro del rango de hace tres meses hasta la fecha actual.

Si buscamos estrictamente el formato de las fechas en elastic, podemos simplificar en la siguiente imagen:

<div align="center">
    <img src="../img/ELK/ELK45.png" alt="ELK" width="50%" />
</div>

Más información sobre **Date Math** en la documentación de elastic: [Date math expressions](https://www.elastic.co/guide/en/elasticsearch/client/net-api/7.17/date-math-expressions.html)


## Búsquedas combinadas y buenas prácticas

Veamos como podemos operar con todo lo visto anteriormente media su combinación. 

Para ello utilizaremos las **bool query** que están compuestas de varias clausulas como son: 
- **must**, que establece condiciones que son de obligado cumplimiento
- **must_not**, que es lo contrario del anterior. Elementos que no queremos encontrarnos.
- **should**, clausula permisiva que abre la consulta a textos o numeros que pueden estar o no, o incluso que se asemejen auna condición ***or***. En este caso no se excluyen documentos y se pueden aplicar todas las clausulas vistas anteriorment.
- **filter**, donde filtramos y ordenamos los documentos obtenidos. Esta clausula no afecta al `score` y se aplica una vez obtenidos los resultados. Es suele filtrar por fecha, números... 

<div align="center">
    <img src="../img/ELK/ELK46.png" alt="ELK" width="30%" />
</div>

Por ejemplo:

Hacemos una búsqueda donde se encuentre el literal "*cocina*" o "*tradicional*" y además queremos aplicar un filtro para que nos muestre solo los resultados entre unas fechas dadas.

```yml
GET restaurantes/_search
{
  "query":{
    "bool": {
      "must": [
        {
          "match": {
            "DESCRIPCION": "cocina tradicional."
          }
        }
      ],
      "filter": [
        {
          "range": {
            "FECHA_MODIFICACION": {
              "gte": "2024-02-01",
              "lte": "now"
            }
          }
        }
      ]
    }
  }
}
```

Recordad que si cambiamos `match` por `match_phrase`, entonces exigiremos el literal.

En el siguiente ejemplo, buscamos un restaurante de precio *gourmet* donde puede ser que sirvan o **carne** o **pescado** o ninguna de las dos cosas;

```yml
GET restaurantes/_search
{
  "query":{
    "bool": {
      "must": [
        {
          "match": {
            "PRECIO": "gourmet"
          }
        }
      ],
      "should": [
        {
          "match": {
            "DESCRIPCION": "carne"
          }
        },
        {
          "match": {
            "DESCRIPCION": "pescado"
          }
        }
      ]
    }
  }
}
```

Si queremos que se cumpla alguna de las condiciones del parámetro `should`, debemos introducir el `minimun_should_match`, y ahora deberá cumplirse obligatoriamente la cantidad que se especifique.

```yml
GET restaurantes/_search
{
  "query":{
    "bool": {
      "must": [
        {
          "match": {
            "PRECIO": "gourmet"
          }
        }
      ],
      "should": [
        {
          "match": {
            "DESCRIPCION": "carne"
          }
        },
        {
          "match": {
            "DESCRIPCION": "pescado"
          }
        }
      ],
      "minimum_should_match": 1
    }
  }
}
```

En este caso solo se obtiene un resultado, mientras que en el primero obtenemos 7.

Realicemos una nueva búsqueda de un restaurante que abra los lunes, que sea cocina canaria o portuguesa

```yml
GET restaurantes/_search
{
  "query":{
    "bool": {
      "must": [
        {
          "match": {
            "HORARIO": "lunes"
          }
        }
      ],
      "should": [
        {
          "match": {
            "DESCRIPCION": "canaria"
          }
        },
        {
          "match": {
            "DESCRIPCION": "portuguesa"
          }
        }
      ],
      "minimum_should_match": 1
    }
  }
}
```

Al final se trata de ir buscando y revisando los resultado obtenidos, por ejemplo los últimos registros, para en caso de no ser deseados añadir restricciones para que no aparezcan estos documentos.

En general, estas son las búsquedas que podemos realizar. Se podrían optimizar pero esto ya es cuestión de analizar y afinar tal y como hemos comentado.