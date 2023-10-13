# Notas sobre Apache nifi

Para su funcionamiento es necesaria una máquina Java y establecer la ubicación de Java, esto se hace en el fichero `./bin/nfif-env.sh` añadiendo antes de la definición de variable como la de NIFI_HOME

```bash
export JAVA_HOME=/lib/jvm/java-1.11.0-openjdk-amd64/
```

Después debemos establecer un usuario y contraseña, por ejemplo con la función: 

```bash
./run/nifi.sh set-single-user-credentials sergio sergiosergio  #usr y contraseña
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

Más información en la [web de apache nifi](https://nifi.apache.org/docs/nifi-docs/html/getting-started.html#downloading-and-installing-nifi)


# Flujo de datos

Dataflow o flujo de dato son los pasos de los datos desde el origen al destino, con o sin transformación en medio.

Los datos pueden ser de diversos formatos, csv, json, videos, audios, .... 

Apache Nifi esta diseñado para automatizar el movimiento de datos.

No es recomendable para hacer transformaciones grandes o de tipo batch, en ese caso tenemos ***spark***

Esta basada en la **programación basada en flujo**, basada en unos procesadores que se unen mediante conexiones.

Estos procesadores son como cajas negras, y los conectores cogen los datos de un procesador y lo entregan a otro, de forma que a los procesadores no les interesa la salida, solo el proceso

Los ficheros que se generan entre diferentes procesadores se llaman `flowfiles`, con paquetes de datos (como ficheros) compuesto por contenido y atributos o metadatos. Los atributos contienen información del contenido; fecha de creación, nombre, o información que añadamos.

Los procesadores son los encargados de realizar las transformaciones o acciones sobre los datos. Se pueden configurar para que se ejecuten según una temporización, tipo cron. Proporcionan una interface para acceder a los flowfiles. Hay procesadores ya creados y publicados o podemos crear nuevos, utilizando java.

Apache Nifi ofrece diferentes tipos de **procesadores**:
- Ingesta  de datos
  - Ejemlos: GetFile, GetFTP, GenerateFlowFiles, GetHTTP, GetMongo, GetKafka, GetTwiter, ... 
- Transformación de datos
  - Permiten transformar datos antes de almacenar en destino
  - Ejemplo: ConvertRecor, UpdateRecord
- Salida de datos
  - Ayudan a enviar los datos a un destino
  - PutEmail, PutFile, PutSFTP, PutMongodb
- Enriamiento y Mediación
  - Enrutan el dato por el flujo adecuado
  - RuteOnAttribute, ControlRate
- Acceso a base de datos
  - ConvertJSONtoSQL, ExecuteSQL
- Extración de atributos
  - Añade o extrae atrubutos de los FlowFiles
  - EvaluateJsonPAth... 
- Interacción con el sistemas
  - ExecuteProcess
- División y agregación
- HTTP y UDP
- AWS


Las **Conexiones** permiten transmitir flowFiles entre procesadores. Se encargan de controlar colas y su caducidad, por ejemplo ante procesadores que van a diferentes velocidades, o encola o deciden que datos tienen más prioridad o que datos ya han quedado obsoletos.

los **Process Groups** es la unión de varios procesadores que tiene una tarea de forma agrupada.
