---
title: MongoDB
description: Almacenamiento de datos. NoSQL
permalink: /mongodb/
---

<h1>Almacenamiento de datos. NoSQL</h1>

<h3>Tabla de contenidos</h3>

# Introducción

En el mundo del Big Data, donde la cantidad de datos generados y procesados continúa creciendo exponencialmente, la elección de la tecnología adecuada para almacenar, gestionar y analizar estos datos es fundamental. **MongoDB**, una base de datos NoSQL de código abierto y orientada a documentos, ha emergido como una solución poderosa y versátil en este panorama en constante evolución.

En este apartado exploraremos cómo MongoDB se integra perfectamente en los entornos de Big Data, ofreciendo capacidades escalables, flexibles y de alto rendimiento para abordar una variedad de desafíos y escenarios de datos a gran escala. Desde su modelo de datos flexible hasta su capacidad para manejar grandes volúmenes de datos en tiempo real, MongoDB se ha convertido en una herramienta indispensable para empresas y organizaciones que buscan aprovechar al máximo sus datos en el mundo del Big Data.

Ya sea que estés involucrado en el desarrollo de aplicaciones, la gestión de datos o el análisis de datos a gran escala, este curso te proporcionará los conocimientos y las habilidades necesarias para aprovechar el poder de MongoDB en el emocionante y desafiante mundo del Big Data.


# MongoDB 

**MongoDB** es una base de datos NoSQL, de código abierto y orientada a documentos. En lugar de almacenar datos en tablas, como lo hace una base de datos relacional, **MongoDB** almacena datos en documentos similares a JSON con un formato llamado ***BSON*** (*Binary JSON*). BSON extiende el formato JSON para incluir tipos de datos adicionales como fechas y binarios, lo que lo hace más adecuado para representar datos complejos.

[**MongoDB**](http://www.mongodb.com) es una de las bases de datos NoSQL más conocidas. Sigue un modelo de datos documental,

<div align="center">
    <img src="../img/MongoDB/MongoDBLogo.png" alt="MongoDB" width="30%" />
</div>

> Como curiosidad, su nombre viene de la palabra inglesa humongous, que significa gigantesco/enorme.

MongoDB destaca porque:

- Soporta esquemas dinámicos: diferentes documentos de una misma colección pueden tener atributos diferentes.
- Aunque inicialmente tenía un soporte limitado de joins, desde la versión 5.2 se pueden realizar incluso entre colecciones particionadas.
- Soporte de transacciones sólo a nivel de aplicación. Lo que en un RDMS puede suponer múltiples operaciones, con MongoDB se puede hacer en una sola operación al insertar/actualizar todo un documento de una sola vez, pero si queremos crear una transacción entre dos documentos, la gestión la debe realizar el driver.

MongoDB se utiliza ampliamente en una variedad de aplicaciones, incluidas aquellas con grandes volúmenes de datos, cargas de trabajo de alta velocidad y requisitos de flexibilidad de esquema. Es especialmente popular en aplicaciones web y móviles, así como en entornos de Big Data y análisis en tiempo real.


## Características de MongoDB

Si tuviéramos que resumir a una la principal característica a destacar de MongoDB, sin duda esta sería la velocidad, que alcanza un balance perfecto entre rendimiento y funcionalidad gracias a su sistema de consulta de contenidos. Pero sus características principales no se limitan solo a esto, MongoDB cuenta, además, con otras que lo posicionan como el preferido de muchos desarrolladores.

Características principales:

- **Consultas ad hoc**. Con MongoDb podemos realizar todo tipo de consultas. Podemos hacer búsqueda por campos, consultas de rangos y expresiones regulares. Además, estas consultas pueden devolver un campo específico del documento, pero también puede ser una función JavaScript definida por el usuario.
- **Indexación**. El concepto de índices en MongoDB es similar al empleado en bases de datos relacionales, con la diferencia de que cualquier campo documentado puede ser indexado y añadir múltiples índices secundarios.
- **Replicación**. Del mismo modo, la replicación es un proceso básico en la gestión de bases de datos. MongoDB soporta el tipo de replicación primario-secundario. De este modo, mientras podemos realizar consultas con el primario, el secundario actúa como réplica de datos en solo lectura a modo copia de seguridad con la particularidad de que los nodos secundarios tienen la habilidad de poder elegir un nuevo primario en caso de que el primario actual deje de responder.
- **Balanceo de carga**. Resulta muy interesante cómo MongoDB puede escalar la carga de trabajo. MongoDB tiene la capacidad de ejecutarse de manera simultánea en múltiples servidores, ofreciendo un balanceo de carga o servicio de replicación de datos, de modo que podemos mantener el sistema funcionando en caso de un fallo del hardware.
- **Almacenamiento de archivos**. Aprovechando la capacidad de MongoDB para el balanceo de carga y la replicación de datos, Mongo puede ser utilizado también como un sistema de archivos. Esta funcionalidad, llamada GridFS e incluida en la distribución oficial, permite manipular archivos y contenido.
- **Ejecución de JavaScript del lado del servido**r. MongoDB tiene la capacidad de realizar consultas utilizando JavaScript, haciendo que estas sean enviadas directamente a la base de datos para ser ejecutadas.



## Conceptos básicos

Hay una serie de conceptos que conviene conocer antes de entrar en detalle:

- MongoDB tienen el mismo concepto de base de datos que un RDMS. Dentro de una instancia de MongoDB podemos tener 0 o más bases de datos, actuando cada una como un contenedor de alto nivel.
- Una base de datos tendrá 0 o más colecciones. Una colección es muy similar a lo que entendemos como tabla dentro de un RDMS. MongoDB ofrece diferentes tipos de colecciones, desde las normales cuyo tamaño crece conforme lo hace el número de documentos, como las colecciones capped, las cuales tienen un tamaño predefinido y que pueden contener una cierta cantidad de información que se sustituirá por nueva cuando se llene.
- Las colecciones contienen 0 o más documentos, por lo que es similar a una fila o registro de un RDMS.
- Cada documento contiene 0 o más atributos, compuestos de parejas clave/valor. Cada uno de estos documentos no sigue ningún esquema, por lo que dos documentos de una misma colección pueden contener todos los atributos diferentes entre sí.

<div align="center">
    <img src="../img/MongoDB/MongoDB01.png" alt="MongoDB" width="50%" />
</div>

Así pues, tenemos que una base de datos va a contener varias colecciones, donde cada colección contendrá un conjunto de documentos. Podemos hacer una correspondencia rápida entre bases de datos Relacionales y NoSQL:

<div align="center">
    <img src="../img/MongoDB/MongoDB02.png" alt="MongoDB" width="31%" />
    <img src="../img/MongoDB/MongoDB17.png" alt="MongoDB" width="60%" />
</div>

Además, MongoDB soporta índices, igual que cualquier RDMS, para acelerar la búsqueda de datos. Al realizar cualquier consulta, se devuelve un cursor, con el cual podemos hacer cosas tales como contar, ordenar, limitar o saltar documentos.


## BSON

MongoDB almacena los documentos mediante BSON (Binary JSON).

Repasemos el concepto de **JSON**: *JavaScript Object Notation*
- Formato de texto sencillo para el intercambio de datos.
- Subconjunto de la notación literal de objetos de JavaScript.
- Alternativa a XML como lenguaje de intercambio de datos. Mucho más sencillo de leer y escribir.
- Uso extendido en bases de datos noSQL, entre ellas MongoDBJSON: JavaScript Object Notation
- Ampliamente soportado por multitud de lenguajes de programación.
- Un objeto JSON está formado por uno o varios pares string: value (cadena:valor).
- Soporta diferentes tipos de datos como cadenas de texto, números, fecha, hora, valores nulos y booleanos.

<div align="center">
    <img src="../img/MongoDB/MongoDB03.png" alt="MongoDB" width="70%" />
</div>

Mediante JavaScript podemos crear objetos que se representan con JSON. Internamente, MongoDB almacena los documentos mediante BSON (Binary JSON). Podemos consultar la especificación en http://BSONSpec.org

**BSON** representa un superset de JSON ya que:

- Permite almacenar datos en binario
- Incluye un conjunto de tipos de datos no incluidos en JSON, como pueden ser ObjectId, Date o BinData.

Podemos consultar todos los tipos que soporta un objeto BSON en http://docs.mongodb.org/manual/reference/bson-types/

Un ejemplo de un objeto BSON podría ser:

```json
var yo = {
  nombre: "Aitor",
  apellidos: "Medrano",
  fnac: new Date("Oct 3, 1977"),
  hobbies: ["programación", "videojuegos", "baloncesto"],
  casado: true,
  hijos: 2,
  contacto: {
    twitter: "@aitormedrano",
    email: "a.medrano@edu.gva.es"
  },
  fechaCreacion: new Timestamp()
}
```

Los documentos **BSON** tienen las siguientes restricciones:

- No pueden tener un tamaño superior a 16 MB.
- El atributo _id queda reservado para la clave primaria.
- Desde MongoDB 5.0 los nombres de los campos pueden empezar por $ y/o contener el ., aunque en la medida de lo posible, es recomendable evitar su uso.

Además MongoDB:

- No asegura que el orden de los campos se respete.
- Es sensible a los tipos de los datos
- Es sensible a las mayúsculas.

Por lo que estos documentos son distintos:

```json
{"edad": "18"}
{"edad": 18}
{"Edad": 18}
```

Si queremos validar si un documento JSON es válido, podemos usar http://jsonlint.com/. Hemos de tener en cuenta que sólo valida JSON y no BSON, por tanto nos dará errores en los tipos de datos propios de BSON.

## Bases de datos Relacionales vs MongoDB

Aquí tenemos un esquema de los elementos de una base de datos representada tanto por un sistema relacional tradicional, frente a la misma estructura con una base de datos en MongoDB

Primero la base de datos relacional

<div align="center">
    <img src="../img/MongoDB/MongoDB18.png" alt="MongoDB" width="70%" />
</div>

y ahora la misma representación en MongoDB

<div align="center">
    <img src="../img/MongoDB/MongoDB19.png" alt="MongoDB" width="70%" />
</div>

# Instalación

En la actualidad, MongoDB se como base de datos en tres productos diferentes más un conglomerado de servicios y herramientas que complementas a la base de datos.

<div align="center">
    <img src="../img/MongoDB/MongoDB04.png" alt="MongoDB" width="50%" />
</div>

1. **Mongo Atlas**, como plataforma cloud, con una opción gratuita mediante un cluster de 512MB.
2. **MongoDB Enterprise Advanced**, versión de pago con soporte, herramientas avanzadas de monitorización y seguridad, y administración automatizada.
3. **MongoDB Community Edition**, versión gratuita para trabajar on-premise, con versiones para Windows, MacOS y Linux. *Nosotros de momento trabajaremos con esta versión*

Para la instalación de **MongoDB Community Edition** en un sistema Ubuntu vamos a proceder tal y como se espedifica en la propia web de **mongodb**. [Install MongoDB Community Edition](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/#install-mongodb-community-edition) 

Realizaremos los siguientes pasos:

```bash
# Requisitos previos
sudo apt-get install gnupg curl                   # Requisitos previos

# Importar claves públicas GPG de MongoDB
curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor

# añadir las fuentes
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list

# recargar paquetes
sudo apt-get update

# e instalar
sudo apt-get install -y mongodb-org
```

Con esto ya tenemos MongoDB instalado en nuestro sistema.

Ahora nos falta ponerlo en marcha, para ello habilitamos e iniciamos el servicio

```bash
# recargamos los nuevos servicios
sudo systemctl daemon-reload

# Habilitamos el servicios (esto es opcional, solo si queremos que se inicie al arrancar el equipo)
sudo systemctl enable mongod

# Iniciamos el servicio
sudo systemctl start mongod

# Comprobamos que el servicio se ha iniciado correctamente
sudo systemctl status mongod
```
<div align="center">
    <img src="../img/MongoDB/MongoDB08.png" alt="MongoDB" width="50%" />
</div>

Mediante el siguiente comando también verificamos que esta activa y su versión. 

```bash
mongod --version                                  # Comprobamos la versión
```

<div align="center">
    <img src="../img/MongoDB/MongoDB09.png" alt="MongoDB" width="50%" />
</div>



> **Nota**: MongoDB también lo podemos instalar descargando el paquete .deb desde la web de MongoDB, pero suele dar mas problemas que con la instalación presentada

Independientemente de nuestro sistema operativo, por defecto, el demonio se lanza sobre el puerto 27017. Una vez instalado, si accedemos a http://localhost:27017 podremos ver que nos indica cómo estamos intentando acceder mediante HTTP a MongoDB mediante el puerto reservado al driver nativo.

<div align="center">
    <img src="../img/MongoDB/MongoDB06.png" alt="MongoDB" width="50%" />
</div>

En vez de instalarlo como un servicio en nuestra máquina, a día de hoy, es mucho más cómodo hacer uso de contenedores Docker o utilizar una solución cloud, aunque nosotros por simplicidad, de momento, realizaremos una instalación tradicional.

Al versión de **Mongo Atlas** nos ofrece de manera gratuita un cluster compartido de servidores con 3 nodos y 512 MB para datos. Si queremos una solución serverless o un servidor dedicado, ya tendremos que pasar por caja.

Password de mi cuenta: 3xC9L1Lkr9GxPm5c

# Primeros pasos con MongoDB

Una vez instalada la base de datos, vamos a interactuar desde su propia consola.

## Trabajando con MongoDB desde la consola

Para acceder a la consola de MongoDB escribimos:

```bash
mongosh
```
<div align="center">
    <img src="../img/MongoDB/MongoDB10.png" alt="MongoDB" width="50%" />
</div>

Algunas de las operaciones básicas que podemos realizar son : 

- Salir de la consola (quit() o pulsando Ctrl+C)
- Limpiar la consola (Ctrl+L)
- Listar las bases de datos (show dbs)
- Cambiarse de base de datos (use <dbname>)
- Listar las colecciones de una base de datos (show collections / show tables)

<div align="center">
    <img src="../img/MongoDB/MongoDB11.png" alt="MongoDB" width="50%" />
</div>

- Mostrar el nombre de la base de datos (db.getName() o db)
- Listar metadata sobre una base de datos (db.stats())
- Solicitar ayuda sobre comandos (db.help())
- Mostrar información sobre el servidor (db.hostInfo())
- Mostrar fecha y hora del sistema (Date())
- Dar formato JSON (db.<collectionName>.find().pretty())

<div align="center">
    <img src="../img/MongoDB/MongoDB12.png" alt="MongoDB" width="50%" />
</div>

Observar que al poner `.pretty()` al final, hace que la salida tenga un formato fácilmente reconocible, aunque hay ocasiones que la salida por defecto ya viene con esta método.

<div align="center">
    <img src="../img/MongoDB/MongoDB13.png" alt="MongoDB" width="50%" />
</div>

Observa también que hay un diferencia entre invocar la función con los paréntesis `()`:

<div align="center">
    <img src="../img/MongoDB/MongoDB14.png" alt="MongoDB" width="50%" />
</div>

## Creación y gestión de Bases de Datos

### Creacion : `use`

El comando para crear una base de datos es el mismo que visto anteriormente para cambiar de base de datos: `use`

Así pues si intentamos entrar en una base de datos que no existe, directamente la prueba

Hasta que no insertes al menos un documento en una de sus colecciones, no estará disponible. Esto lo podemos hacer en el siguiente ejemplo:

<div align="center">
    <img src="../img/MongoDB/MongoDB15.png" alt="MongoDB" width="50%" />
</div>

Todo esto es debido a que MongoDB planifica la existencia de una base de datos, pero hasta que no tenga su primer datos, no va a designar ningún tipo de recursos a la misma. En la captura anterior, se ve que ya le ha asignado 8 KiB a nuestra primera base de datos porque ya tiene algún dato.

Por otra parte, para la creación de una colección e inclusión de un documento en concreto, observar que simplemente al insertar el documento, si la colección no existe, la crea directamente, de la misma forma que ha hecho con la base de datos.

Más adelante ya veremos con más detenimiento las diferentes forma de insertar registro en un tabla (colección), de momento hemos usando el comando:

```
db.primeraColeccion.insertOne({ id: 1, nombre: 'sergio' })
```

## Eliminación de base de datos: db.dropDatabase()

Para eliminar una base de datos, en primer lugar debemos estar ubicados dentro de la propia base de datos a eliminar y ahí ejecutamos el comando 

```
db.dropDatabase()
```

Podemos hacer uso de los comandos `use` y `db` para pasar ubicarnos en una base de datos y comprobar que efectivamente lo estamos, aunque en el prompt de la propia shell de MongoDB directamente ya nos dice que estamos ahí.

<div align="center">
    <img src="../img/MongoDB/MongoDB16.png" alt="MongoDB" width="50%" />
</div>


## Tipos de datos 

Aquí tienes una lista de algunos tipos de datos comunes en MongoDB, junto con ejemplos de cómo se representan en formato de tabla:

| Tipo de Datos  | Descripción                             | Ejemplo                                |
|----------------|-----------------------------------------|----------------------------------------|
| String         | Cadena de texto                         | "Hello World"                          |
| Number         | Número                                  | 42                                     |
| Boolean        | Valor booleano (true/false)             | true                                   |
| Date           | Fecha y hora                            | ISODate("2024-03-01T12:00:00.000Z")   |
| Array          | Arreglo de valores                      | [1, 2, 3]                              |
| Object         | Objeto o documento anidado              | {"nombre": "Juan", "edad": 30}        |
| ObjectId       | Identificador único de documento        | ObjectId("61e4c3055b17967d02a9c3d7")  |
| Null           | Valor nulo                              | null                                   |
| BinData             | Datos binarios                              | BinData(0, "ABC123==")                     |
| Regular Expressions | Expresiones regulares                       | /pattern/g                                 |

Recuerda que MongoDB es una base de datos NoSQL orientada a documentos, por lo que no tiene una estructura de tabla como las bases de datos relacionales. En MongoDB, los datos se almacenan en documentos BSON (Binary JSON), que pueden contener campos con diferentes tipos de datos, incluidos los mencionados anteriormente.

Es importante destacar que en MongoDB, los datos binarios y las expresiones regulares se representan de manera especial. Los datos binarios se representan mediante el tipo `BinData`, que incluye un tipo y una cadena de datos codificados en base64. Las expresiones regulares se representan utilizando el formato `/pattern/flags`, donde `pattern` es el patrón de la expresión regular y `flags` son los modificadores de la expresión regular, como `i` para ignorar mayúsculas y minúsculas o `g` para realizar una búsqueda global.


Aquí tienes un ejemplo de cómo se podría representar un documento en MongoDB utilizando algunos de estos tipos de datos:

```json
{
  "_id": ObjectId("61e4c3055b17967d02a9c3d7"),
  "nombre": "Juan",
  "edad": 30,
  "activo": true,
  "intereses": ["programación", "música", "viajes"],
  "ubicacion": {
    "ciudad": "Barcelona",
    "pais": "España"
  },
  "fechaRegistro": ISODate("2024-03-01T12:00:00.000Z"),
  "comentarios": [
    {
      "usuario": "Ana",
      "texto": "¡Hola Juan!"
    },
    {
      "usuario": "Carlos",
      "texto": "Saludos desde Xàtiva."
    }
  ]
}
```

<div align="center">
    <img src="../img/MongoDB/MongoDB03.png" alt="MongoDB" width="70%" />
</div>


En este ejemplo, que ya hemos visto previamente para ilustrar qué es un BSON, el documento representa un usuario con campos como nombre, edad, activo, intereses, ubicación, fecha de registro y comentarios. Cada campo tiene un tipo de datos diferente, como string, number, boolean, array, object, date, etc.

Más información sobre tipos de datos en [tutorialspoint MongoDB - Datatypes](https://www.tutorialspoint.com/mongodb/mongodb_datatype.htm)

## Ejercicios propuestos

1. Partiendo del escritorio de tu ordenador, ejecuta los pasos necesarios para poder usar la consola de `mongodb` (abrir un terminal o consola, iniciar/parar servicios, ejecutar la shell de `mongodb`)
2. Crea una base de datos llamada concesionario. Recuerda insertar al menos un documento en una colección que se llame coches. Como propiedades del documento json, puedes usar matrícula, marca, modelo, versiones (sport, confort), kms y fecha de matriculación. (Aunque veremos cómo insertar documentos JSON en próximas clases, puedes usar el comando db.insertOne(aqui va tu documento json))
3. Visualiza el listado de todas las bases de datos disponibles.
4. Elimina la base de datos creada y comprueba que ya no existe al pedir el listado.

# Operaciones con datos CRUD

En MongoDB, las operaciones **CRUD** (*Crear*, *Leer*, *Actualizar*, *Eliminar*) se realizan utilizando métodos específicos. Aquí te muestro cómo realizar cada una de estas operaciones.

Antes de comenzar a trabajar, debemos entrar en una de las bases de datos con `use` y en todo momento podemos ver las colecciones que tenemos en esta base de datos con `use collections` 

## Insertar :

Para insertar documentos en una colección, se utiliza el método `insertOne()` o `insertMany()`.

- `db.collectionName.insertOne(<json>);`: Inserta un solo documentos


Ejemplos

```javascript
// Insertar un solo documento en la colección "usuarios"
db.usuarios.insertOne({
    nombre: "Juan",
    edad: 30,
    ciudad: "Barcelona"
});

// En un única línea, y con comillas dobles, también... 
db.usuarios.insertOne({ nombre: "Toni", edad: 15, ciudad: "Valencia"});

// Insertar un solo documento en la colección "usuarios"
db.usuarios.insertOne({
    nombre: "Juan",
    edad: 30,
    ciudad: "Barcelona",
    intereses: ["fútbol", "música"],
    direccion: { calle: "Calle Mayor", numero: 123 },
    fechaRegistro: new Date(),
    activo: true
});


// Insertar un documento con la fecha actual. Ojo con el último campo
db.usuarios.insertOne({
    nombre: "Dorotea",
    fecha: new Date(),
    lugar: "Xàtiva"
});

// Insertar un documento con una fecha específica 
// con campos que antes no estaban 
// poniendo los campos entre comillas, que es totalmente indiferente
// pero si ponemos los número entre comillas se convierten en texto
db.usuarios.insertOne({
    "nombre": "Filiberto",
    "edad" : "33",
    "fechaNacimiento": new Date("2004-03-15"),
    "ciudad": "Alacant"
});
```

Cuando hacemos una inserción, nos devuelve el resultado del tipo

```js
{
  acknowledged: true,
  insertedId: ObjectId('65e818360ad094ed2ab24245')
}
```


- `db.collectionName.insertMany(<json>);`. Inserción de varios elementos.
Como se trata de una inserción de un conjunto de documentos, lo que hacemos en pasar un **array** y esto se hace mediante el uso de ***corchetes*** : `[]`.

Ejemplos: 

```javascript
// Insertar varios documentos en la colección "usuarios"
db.usuarios.insertMany([
    { nombre: "Ana", edad: 25, ciudad: "Madrid" },
    { nombre: "Carlos", edad: 35, ciudad: "Valencia" }
]);

// Insertar varios documentos en la colección "usuarios"
db.usuarios.insertMany([
    { nombre: "Ana", edad: 25, ciudad: "Madrid", intereses: ["viajes"], fechaRegistro: new Date(), activo: false },
    { nombre: "Carlos", edad: 35, ciudad: "Valencia", intereses: ["lectura"], fechaRegistro: new Date(), activo: true }
]);
```
Observar cómo trabajar con fechas

## Leer:

Uno de los aspectos más interesantes de las bases de datos es la capacidad para realizar consultas, por lo que ahora vamos a ver de forma muy breve como leer datos, pero más adelante profundizaremos en la realización de consultas más elaboradas.

Para leer datos de una colección, se utiliza el método `find()`.

```javascript
// Leer todos los documentos de la colección "usuarios"
db.usuarios.find();

// Leer todos los documentos de la colección "usuarios" y formatear la salida json
db.usuarios.find().pretty();

// Leer documentos que coincidan con un criterio específico
db.usuarios.find({ ciudad: "Barcelona" });

// Leer documentos que coincidan con un criterio específico (por ejemplo, ciudad igual a "Barcelona" y activo igual a true)
db.usuarios.find({ ciudad: "Barcelona", activo: true });

// Leer documentos con proyección (seleccionar campos específicos)
db.usuarios.find({}, { nombre: 1, edad: 1 });

// Leer documentos con proyección (seleccionar campos específicos)
db.usuarios.find({}, { nombre: 1, edad: 1, _id: 0 });

// Leer todos los eventos que ocurrieron después de una fecha específica
db.eventos.find({ fecha: { $gt: new Date("2024-01-01") } });

// Leer eventos que ocurrieron en un rango de fechas
db.eventos.find({ fecha: { $gte: new Date("2024-01-01"), $lte: new Date("2024-12-31") } });
```

## Actualizar:

Para actualizar documentos en una colección, se utiliza el método `updateOne()` o `updateMany()`.

- `db.collection.updateOne(<filter>, <update>)`

El método `updateOne()` se utiliza para actualizar un solo documento que coincida con un criterio específico. Si hay varios documentos que coinciden con el criterio, solo se actualizará el primero que se encuentre.

En la clausula de actualización tenemos el comando `$set`. Además debemos tener en cuenta que tanto el `<filter>` como la `<update>` son json por lo que deben estar comprendidos entre corchetes:

```js
db.collection.updateOne({}, {});
db.collection.updateOne({}, {$set:{}});
```

Veamos algunos ejemplos

```javascript
// Ejemplo de updateOne()
db.usuarios.updateOne(
    { nombre: "Juan" },
    { $set: { edad: 31 } }
);

// Cambiamos más de un valor
db.usuarios.updateOne(
    { nombre: "Juan" },
    { $set: { edad: 31, ciudad: 'Albacete' } }
);

// Actualizar la fecha de un evento específico
db.usuarios.updateOne(
    { nombre: "Alberto" },
    { $set: { fechaRegistro: new Date("2024-03-20") } }
);
```
En el primer ejemplo, se actualizará el primer documento de la colección "usuarios" que tenga el campo `nombre` igual a "Juan". Si hay varios documentos con ese nombre, solo se actualizará uno.

Una vez realizada la actualización, MongoDB avisa: 

```js
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

- `db.collection.updateMany(<filter>, <update)`

Por otro lado, el método `updateMany()` se utiliza para actualizar múltiples documentos que coincidan con un criterio específico. Todos los documentos que cumplan el criterio serán actualizados.

```javascript
// Ejemplo de updateMany()
db.usuarios.updateMany(
    { ciudad: "Játiva" },
    { $set: { ciudad: "Xàtiva" } }
);
```

En este ejemplo, se actualizarán todos los documentos de la colección "usuarios" que tengan el campo `ciudad` igual a "Játiva", estableciendo su valor a "Xàtiva".

O sea, `updateOne()` es útil cuando solo quieres actualizar un único documento, mientras que `updateMany()` es útil cuando necesitas actualizar múltiples documentos que cumplan un criterio específico.


- `db.collection.replaceOne(<filter>, <update>)`

Reemplazo completo de un documento. En este caso, al reemplazar el documento que encontramos por una nuevo, no necesitamos el comando `$set`

Ejemplos

```js
db.usuarios.replaceOne(
    { nombre: "Alberto" },
    {     
        nombre: "Alberto D.",
        edad: 18,
        ciudad: "Xàtiva",
        intereses: ["Baloncesto", "Informática"],
        fechaRegistro: new Date(),
        activo: true 
    }
);
```

En este caso, vamos a ver su ejecución, donde veremos incluso que al cambiar el nombre, este campo también cambia aunque se el utilizado para hacer la búsqueda:

<div align="center">
    <img src="../img/MongoDB/MongoDB20.png" alt="MongoDB" width="50%" />
</div>

## Eliminar:

Para eliminar documentos de una colección, se utiliza el método `deleteOne()` o `deleteMany()`.

En MongoDB, tanto `deleteOne()` como `deleteMany()` son métodos utilizados para eliminar documentos de una colección. Aquí tienes las diferencias entre ellos:

- `deleteOne()`

El método `deleteOne()` se utiliza para eliminar un solo documento que coincida con un criterio específico. **Si hay varios documentos** que coinciden con el criterio, **solo se eliminará el primero** que se encuentre.

```javascript
// Ejemplo de deleteOne()
db.usuarios.deleteOne({ nombre: "Juan" });
```

En este ejemplo, se eliminará el primer documento de la colección "usuarios" que tenga el campo `nombre` igual a "Juan". Si hay varios documentos con ese nombre, solo se eliminará uno.

`deleteMany()`

Por otro lado, el método `deleteMany()` se utiliza para eliminar varios documentos que coincidan con un criterio específico. Todos los documentos que cumplan el criterio serán eliminados.

```javascript
// Ejemplo de deleteMany()
db.usuarios.deleteMany({ activo: false });
```
En este ejemplo, se eliminarán todos los documentos de la colección "usuarios" que tengan el campo `activo` igual a false.

Otros ejemplos

```javascript
// Eliminar varios documentos que cumplan el criterio especificado
db.usuarios.deleteMany({ ciudad: "Xàtiva" });

// Eliminar eventos que ocurrieron antes de una fecha específica
db.eventos.deleteMany({ fecha: { $lt: new Date("2024-03-01") } });

```

**Cuidado**. Como siempre debemos tener cuidad a la hora de borrar, de echo si hacemos 

```js
db.usuarios.deleteMany({});
```
Nos borrará **todos** los documentos de la colección.

> **Nota**: Siempre se debe pasar un json dentro de la condición, o sea, dentro de los paréntesis deben haber llaves:
> ```js
> db.usuarios.deleteMany();     //error
> db.usuarios.deleteMany({});   //correcto: json vacío
> ```

# Diseño de modelado de bases de datos. `schemaless`

## Concepto de `schemaless`

El término `schemaless` (sin esquema) se refiere a la capacidad de una base de datos para manejar datos sin una estructura fija predefinida. En el contexto de *MongoDB*, esto significa que no estás obligado a definir un esquema estricto para tus datos antes de comenzar a almacenarlos. En lugar de eso, los datos se almacenan en documentos BSON (Binary JSON), y estos documentos pueden tener una estructura flexible y pueden variar de un documento a otro dentro de la misma colección.

A continuación, profundicemos en algunos aspectos clave del concepto de schemaless en MongoDB:

- **Flexibilidad de estructura**: Los documentos en MongoDB pueden contener diferentes campos y tipos de datos. No es necesario que todos los documentos en una colección tengan la misma estructura. Esto permite adaptarse fácilmente a cambios en los requisitos de la aplicación sin tener que modificar un esquema centralizado.

-  **Adición dinámica de campos**: En MongoDB, puedes agregar campos a un documento en cualquier momento sin afectar a otros documentos en la misma colección. Esto significa que puedes manejar datos evolutivos donde la estructura de los documentos puede cambiar con el tiempo.

-  **Consulta sin restricciones**: Dado que no hay un esquema fijo que imponga restricciones sobre la estructura de los datos, las consultas en MongoDB pueden ser más flexibles. Puedes realizar consultas sobre cualquier campo en cualquier documento, incluso si esos campos no están presentes en todos los documentos de la colección.

-  **Evita la migración de esquemas**: En las bases de datos tradicionales con esquemas fijos, los cambios en el esquema requieren migraciones de datos costosas. Con MongoDB, puedes evitar este problema ya que no hay un esquema centralizado que necesite ser modificado.

-  **Agilidad en el desarrollo**: La falta de un esquema fijo permite una mayor agilidad en el desarrollo de aplicaciones, ya que puedes iterar rápidamente y ajustar el modelo de datos según sea necesario sin tener que preocuparte por actualizar un esquema centralizado.

-  **Rendimiento**: La flexibilidad del modelo de datos schemaless puede traducirse en un mejor rendimiento en ciertos casos, ya que elimina la necesidad de realizar un join de datos dispersos en múltiples tablas, como suele ocurrir en bases de datos relacionales.

A pesar de las ventajas de un modelo de datos schemaless, es importante tener en cuenta que esto también puede presentar **desafíos**, especialmente en términos de **mantener la coherencia y la integridad de los datos**. Por lo tanto, es crucial diseñar cuidadosamente la base de datos y utilizar prácticas como la validación de datos y la indexación adecuada para garantizar un rendimiento óptimo y la integridad de los datos en aplicaciones MongoDB.

Observar la diferencia que tenemos en el diseño de la bases de datos relacionales con las NoSQL como lo vimos anteriormente

## Documentos embebidos

El concepto de embebido hace referencia a guardar una *‘cosa’* dentro de otra *‘cosa’*. En este caso, guardar un documento JSON dentro de
otro como valor de una de sus propiedades.

Por ejemplo, supongamos que tenemos una colección que guarda datos sobre cursos que se están impartiendo, en una base de datos relacional serían dos tablas, pero en MongoDB lo hacemos en una única colección:

```js
{
    id: 1,
    referencia: 'C0001',
    nombre: 'Curso de especialización de Inteligencia Artificial y Big Data',
    fechaInicio: new Date("2023-10-01"),
    activo: true,
    asignaturas: [
        {
            codAsig: 101,
            nombre: 'Sistemas de Big Data',
            horasSemana: 3,
            profesores: [
                {
                    codProf: 302,
                    nombre: 'Sergio Rey',
                    rol: 'Profesor'
                },
                {
                    codProf: 901,
                    nombre: 'Jorge Soro',
                    rol: 'Especialista'
                }
            ]
        },
        {
            codAsig: 102,
            nombre: 'Big Data aplicado',
            horasSemana: 3,
            profesores: [
                {
                    codProf: 301,
                    nombre: 'Nacho Pachés',
                    rol: 'Profesor'
                },
                {
                    codProf: 901,
                    nombre: 'Jorge Soro',
                    rol: 'Especialista'
                }
            ]
        }
    ],
    alumnos: []
}
```


## Documentos referenciados

El concepto ***referenciado***  a diferencia de los documentos embebidos, en un documento JSON se guarda solo el valor de una o varias propiedades, en lugar del documento completo.

Normalmente, se guarda el valor de una propiedad que identifica unívocamente, al documento referenciado: por ejemplo en el caso anterior podríamos tener: 

```js
{
    id: 1,
    referencia: 'C0001',
    nombre: 'Curso de especialización de Inteligencia Artificial y Big Data',
    fechaInicio: new Date("2023-10-01"),
    activo: true,
    asignaturas: [ 101, 102],
    alumnos: []
}
```

En este caso, las asignaturas se referéncian mediante el código de identificación, en lugar de guardar en el JSON todos los datos. De esta forma es similar al adoptado por las bases de datos relacionales.


Esto plantea varias ventajas y desventajas:

Así pues en los **documentos embebidos** tenemos:
- Ventajas
  - Al recuperar un curso, podemos traernos toda la información relacionada en otras colecciones (p.e. asignaturas)
- Desventajas:
  - Al hacer consultas sobre la colección externa (cursos), si uno de los criterios afecta a la información de los documentos embebidos, el tiempo para realizar dicha consulta se verá incrementando.
  - Las actualizaciones serán más costosas si alguna de las propiedades a actualizar pertenece al documento embebido.

Mientras que en los **documentos referenciados**
- Ventajas
  - Las consultas sobre la colección principal y las relacionadas se ejecutará más rápido.
  - Al actualizar información relacionada, se hace directamente en sus documentos sin tener que revisar la colección externa.
- Desventajas:
  - Al recuperar un curso, habrá que consultar los identificadores que relacionan a los documentos en otras colecciones y hacer consultas adicionales para obtener la información relacionada.


Entonces **¿Qué diseño elegir?**

Dependerá de:
- Cómo se quiere almacenar la información.
- la naturaleza y el contexto de las aplicaciones que vayan a consumir la información.
- Las preferencias de roles como arquitectos de software y de bases de datos teniendo en cuenta factores futuros como la escalabilidad en cuanto a volumen de datos, usuarios / aplicaciones y sus formas de acceder a la información, etc.



# Herramientas visuales para interactuar con MongoDB 

Hemos visto cómo interactuar con MongoDB desde la consola que nos ofrece la base de datos, pero para interactuar de una forma más flexible e intuitiva existen herramientas visuales que nos facilitan el trabajo diario con MongoDB

## MongoDB Compass

Una de ellas es MongoDB Compass, que facilita la exploración y manipulación de los datos. De una manera flexible e intuitiva, Compass ofrece visualizaciones detalladas de los esquemas, métricas de rendimiento en tiempo real así como herramientas para la creación de consultas.

Existen tres versiones de Compass, una completa con todas las características, una de sólo lectura sin posibilidad de insertar, modificar o eliminar datos (perfecta para analítica de datos) y una última versión isolated que solo permite la conexión a una instancia local.

Enlace a la documentación oficial de MongoDB Compass: [What is MongoDB Compass?](https://www.mongodb.com/docs/compass/current/)

### Instalación

Siguiendo los pasos ofrecidos por la propia web de MongoDB, para la instalación de MongoDB Compass en Ubuntu seguimos los siguientes pasos:

```bash
# Download MongoDB Compass
wget https://downloads.mongodb.com/compass/mongodb-compass_1.40.4_amd64.deb

# Install MongoDB Compass
sudo dpkg -i mongodb-compass_1.40.4_amd64.deb

# Start MongoDB Compass
mongodb-compass
```

Si hacemos caso a lo que nos dicen en la guía, directamente instalamos la última versión estable.

<div align="center">
    <img src="../img/MongoDB/MongoDB21.png" alt="MongoDB" width="50%" />
</div>

## Tabajando con MongoDB Compass

Al iniciar la aplicación, la primera vez nos ofrece conectarnos a la base de datos local. También nos podemos conectar a una base de datos remota e incluso a [Mongo Atlas](https://www.mongodb.com/es/atlas), que como se comentó es la base de datos que ofrece MongoDB en la nube.

Una vez conectados a la base de datos, vemos todas las bases de datos exitentes. En la parte inferior tenemos una consola donde podemos actuar de la misma forma que lo hicimos anteriormente.

<div align="center">
    <img src="../img/MongoDB/MongoDB22.png" alt="MongoDB" width="60%" />
</div>

Dentro de una base de datos, podemos acceder a las colecciones, listar los documentos, y realizar todo tipo de operaciones sobre los mismos:

<div align="center">
    <img src="../img/MongoDB/MongoDB23.png" alt="MongoDB" width="60%" />
</div>

Así como operaciones específicas sobre documentos en concreto. Si nos colocamos con el ratón sobre un documento aparecen cuatro opciones, para *editar*, *copiar,*, *duplicar* y *borrar* el documento. Haciendo doble click, también lo editamos.

Tenemos varias opciones sobre la base de datos, incluso podemos hacer consultas.

<div align="center">
    <img src="../img/MongoDB/MongoDB24.png" alt="MongoDB" width="60%" />
</div>

En la imagen:
1. Dentro de una colección, seleccionamos la pestaña de `schema`
2. Introducimos el filtro a buscar
3. Obtenemos el detalle de los datos de los documentos obtenidos
4. Tenemos un histórico de todas las búsquedas realizadas


## MongoDB for VSCode

También podemos utilizar la extensión que lleva VSCode para trabajar con MongoDB.

Para su **instalación**

Si no disponemos de VSCode:
- podemos instalarlo siguiendo los pasos de la propia web de Microsoft: [Visual Studio Code on Linux](https://code.visualstudio.com/docs/setup/linux#_debian-and-ubuntu-based-distributions)
- si tenemos la versión completa de Ubuntu, la podemos instalar desde el gestor de aplicaciones:

<div align="center">
    <img src="../img/MongoDB/MongoDB25.png" alt="MongoDB" width="20%" />
    <img src="../img/MongoDB/MongoDB26.png" alt="MongoDB" width="50%" />
</div>

Una vez instalado VSCode, instalamos la extensión de MongoDB for VS Code, aqui seguimos los pasos de la web oficial donde tenemos cómo instalar y configurar la conexión: [VSCode: Working with MongoDB](https://code.visualstudio.com/docs/azure/mongodb). Para la conexión, pulsamos sobre el botón de *Advanced* y la conexión es sencilla

<div align="center">
    <img src="../img/MongoDB/MongoDB27.png" alt="MongoDB" width="40%" />    
    <img src="../img/MongoDB/MongoDB28.png" alt="MongoDB" width="40%" />
</div>

Una vez conectados, podremos recorrer las colecciones con los datos así como utilizar un *playground* para interactuar de manera similar al shell:

<div align="center">
    <img src="../img/MongoDB/MongoDB27.png" alt="MongoDB" width="40%" />    
    <img src="../img/MongoDB/MongoDB28.png" alt="MongoDB" width="40%" />
</div>

Realmente, esta extensión este pensada para trabajar con opciones avanzadas, como crear índices, generar código en lenguajes como *javascript*, *python* o cualquier otro para realizar todo tipo de operaciones en MongoDB, o crear variables con datos y estos utilizarlos en nuestras operaciones. Para más información en la web de la extension: [MongoDB for VS Code. MongoDB Without Leaving Your IDE](https://www.mongodb.com/products/tools/vs-code)














# Operaciones con datos: Consultas

Vamos a profundizar sobre las operaciones de consultas que ya hemos visto brevemente con anterioridad.

El comando básico es `.find()`

```js
db.collection.find()            // devuelve todos los documentos
db.collection.find(<filter>)    // devuelve los documentos que cumplen el filtro
```

