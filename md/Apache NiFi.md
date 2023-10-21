---
title: Apache NiFi
description: Apache NiFi
permalink: /nifi/
---

<h1>Apache Nifi</h1>

<div align="center">
    <img src="../img/LogoNiFi.jpeg" alt="Logo Apache NiFi" width="15%" />
</div>

<h3>Tabla de contenidos</h3>

- [1. Instalación `Apache Nifi`](#1-instalación-apache-nifi)
- [2. Terminologia NiFi](#2-terminologia-nifi)
	- [2.1. DataFlow](#21-dataflow)
	- [2.2. FlowFile](#22-flowfile)
	- [2.3. Processors](#23-processors)
	- [2.4. Conexiones](#24-conexiones)
	- [2.5. Process Groups](#25-process-groups)


# 1. Instalación `Apache Nifi`

Para la instalación de NiFi, descargamos la última versión desde la web; archivo binario.

Lo descomprimimos y dejamos en la ubicación adecuada y ya podemos ejecutarlo.

El usuario se puede crear vía comandos por cmd, o se puede coger el que genera automaticamente en el log NiFi, algo asi (fichero nifi-app.log):

```bash 
$ cat logs/nifi-app.log | grep Generated
Generated Username [80e91118-b222-4b47-8dab-63a8deb7905d]
Generated Password [zavwbGlRcYeky51Bxc0zbVN8hj2bE61u]
```

Y para establecer un usuario y contraseña, lo podemos hacer con el siguiente comando: 

```bash
./bin/nifi.sh set-single-user-credentials sergio sergiosergio  #usr y contraseña (de 12 caracteres mínimo)
```

Una vez establecida la contraseña, arrancamos: tenemos los comandos;

```bash
./nifi.sh start   # ejecución en segundo plano
./nifi.sh run     # ejecución en primer plano
./nifi.sh status
./nifi.sh stop
```

Tarda un poco en ponerse en marcha, hasta 5 minutos.

Luego accedemos en `https://localhost:8443/nifi`

> Nota: Para su funcionamiento **es necesaria una máquina Java**. En ocasiones hay problemas con *java* y es necesario establecer la ubicación de Java, esto se hace en el fichero `./bin/nifi-env.sh` añadiendo antes de la definición de variable como la de NIFI_HOME

```bash
export JAVA_HOME=/lib/jvm/java-1.11.0-openjdk-amd64/
```

Más información en la [web de apache nifi](https://nifi.apache.org/docs/nifi-docs/html/getting-started.html#downloading-and-installing-nifi)


# 2. Terminologia NiFi

`Nifi` esta basado en FBP (Flow Based Programming), que es un paradigma de programación que define aplicación como cajas negras (procesos), los cuales intercambian datos entre conexiones predefinidas.
Estas cajas negras (procesos) pueden ser combinados en dataflows. 

## 2.1. DataFlow

- `Dataflow` o `flujo de dato` son los pasos de los datos desde el origen al destino, con o sin transformación en medio.

Los datos pueden ser de diversos formatos, csv, json, videos, audios, .... 

`Apache Nifi` esta diseñado para automatizar el movimiento de datos.

No es recomendable para hacer transformaciones grandes o de tipo batch, en ese caso tenemos ***spark***

Esta basada en la **programación basada en flujo**, basada en unos procesadores que se unen mediante conexiones.

Estos procesadores son como cajas negras, y los conectores cogen los datos de un procesador y lo entregan a otro, de forma que a los procesadores no les interesa la salida, solo el proceso

## 2.2. FlowFile

Los ficheros que se generan entre diferentes procesadores se llaman `flowfiles`, con paquetes de datos (como ficheros) compuesto por contenido y atributos o metadatos. Los atributos contienen información del contenido; fecha de creación, nombre, o información que añadamos.

Contiene datos. Abstracción de los datos en NiFi -->  CSV,JSON,XML,SQL,Binary,etc

Tiene dos componentes:
- Content:  contiene los datos actuales.
- Attributes: representa los metadatos del fichero
	
Son ficheros persistentes en disco

## 2.3. Processors

- `Processor`: un Processor puede generar un nuevo "FlowFile" para procesar o ingestar un existente FlowFile desde cualquier origen. Todos los processors pueden ser conectados con otros. Estos, son enlazados vía conexiones con links. Cada conexión tendrá una cola "Queue for FlowFiles".

Puede añadir, actualizar y borrar atributos de un FlowFile
Puede cambiar el contenido a un FlowFile.
		

- Input/Output: entrada y salida són utilizados para mover datos entre "Process Group".

- Controller Service: servicio compartido que puede usado por un Processor. Este servicio puede mantener
conexiones con bases de datos. Por ejemplo, CSV Reader, JSON Writer, etc.

Los procesadores son los encargados de realizar las transformaciones o acciones sobre los datos. Se pueden configurar para que se ejecuten según una temporización, tipo cron. Proporcionan una interface para acceder a los flowfiles. Hay procesadores ya creados y publicados o podemos crear nuevos, utilizando java.

Apache Nifi ofrece diferentes tipos de **procesadores**, y los más utilizados o importantes son: 

**Ingesta de datos**

	GenerateFlowFiles
	GetFile
	GetFTP
	GetSFTP
	GetJMSQueue
	GetJMSTopic
	GetHTTP
	ListenHTTP
	ListenUDP
	getHDFS
	GetKafka
	QueryDatabaseTable
	GetMongo
	GetTwitter
	ListHDFS / FetchHDFS


**Transformación del datos**. Permiten transformar datos antes de almacenar en destino

	ConvertRecord
	UpdateRecord
	ConvertJSONToSQL
	ReplaceText
	CompressContent
	ConvertCharacterSet
	EncryptContent
	TransformXml
	JoltTransformJSON
	
**Envío de datos**. Ayudan a enviar los datos a un destino

	PutEmail
	PutFile
	PutFTP
	PutSFTP
	PutJMS
	PutSQL
	PutKafka
	PutMongo
	PutHDFS

**Control y revisión**. Enrutan el dato por el flujo adecuado

	ControlRatte
	DetectDuplicate
	DistributeLoad
	RouteOnAttribute
	RouteOnAttribute
	RouteOnContent
	ScanAttribute
	ScanContent
	ValidateXml
	ValidateCSV
	
**Acceso a base de datos**

	ConvertJSONToSQL
	ExecuteSQL
	PutSQL
	SelectHiveQL
	PutHiveQL
	ListDatabaseTables
	
**Extracción de atributos**. Añade o extrae atributos de los FlowFiles
	
	EvaluateJsonPath
	EvaluateXPath
	EvaluateXQuery
	ExtractText
	HashAttribute
	HashContent
	IdentifyMimeType
	UpdateAttribute
	LogAttribute

**Sistema**

	ExecuteProcess
	ExecuteStreamCommand
	
**Agregaciones y Splits**
	
  SplitText
	SplitJson
	SplitXml
	SplitRecord
	SplitContent
	UnpackContent
	SegmentContent
	MergeContent
	QueryRecord

**Http y udp**

	GetHTTP
	ListenHTTP
	InvokeHTTP
	PostHTTP
	HandleHttpRequest
	HandleHttpRespone
	ListenUDP
	PutUDP
	ListenUDPRecord
	
**AWS**

	FetchS3Object
	PutS3Object
	PutSNS
	GetSQS
	PutSQS
	DeleteSQS
	GetDynamoDB
	PutDynamoDB
	PutLambda

## 2.4. Conexiones

Las **Conexiones** permiten transmitir flowFiles entre procesadores. Se encargan de controlar colas y su caducidad, por ejemplo ante procesadores que van a diferentes velocidades, o encola o deciden que datos tienen más prioridad o que datos ya han quedado obsoletos.

## 2.5. Process Groups

Los **Process Groups** es la unión de varios procesadores que tiene una tarea de forma agrupada.

Son conjuntos de componentes Processor combinados. Ayudan a mantener un gran y complejo dataflow.