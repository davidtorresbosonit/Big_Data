# Spark

## Introducción a Spark


Proyecto open source creado y mantenido por
la comunidad de desarrolladores

Fue creado en 2009 en la universidad de
Berkley, como respuesta a la ineficiencia de
MapReduce(MR) para procesos iterativos e
interactivos

### Porque Scala con Spark

Spark, su API principal y el Spark
Shell están escritos en Scala, por
lo que SPARK utiliza multitud de
funciones de Scala.

Utilizar Scala con Spark nos
proporciona una forma de
implementar paralelismo sin
necesidad de utilizar las librerías
existentes para ello
(como puede
ser en Java la librería Thread).
Pues el framework SPARK
distribuye automáticamente el
trabajo entre los diferentes nodos (ordenadores) disponibles en el
clúster

Es una extensión del modelo MapReduce cuyo objetivo es
soportar más tipos de computación, específicamente en
streaming, con idea de poder explorar los datos
interactivamente, en lugar de tener que esperar horas.

### Información Spark

Para llevar a cabo toda esta computación utilizaremos Apache Spark, que no es
más que un framework para programación distribuida sobre datos en paralelo.

Para ello, Spark implementa un modelo de datos paralelos distribuidos
llamado RDD: Resilient Distributed Dataset

A partir de ahora, tenemos que pensar en nuestros datos distribuidos como si
fueran una única colección

### Latencia

Es algo de lo que no podemos prescindir. Hemos de tenerlo en mente
cuando programamos.

Orden por velocidad

1. Memoria
2. Disco
3. Red

### ¿Por qué se usa Spark si ya está Hadoop?

#### Excelente para los Data Scientist
◦ Spark es mucho más rápido que Hadoop.
◦ Por lo que se mejora la productividad de los analistas de datos.
◦ Pueden experimentar más veces con los datos en el mismo tiempo.
◦ En Hadoop no es fácil crear un bucle que itere sobre los datos hasta que
se cumpla una condición.
◦ …
#### Es más expresivo y sencillo
◦ Hadoop es mucho más rígido: obliga a ejecutar primero un Map de todo y
luego un reduce, sin dar la posibilidad de combinar funciones de manera
INTELIGENTE.

### Spark tolerancia a fallos

#### La tolerancia a fallos en Hadoop MapReduce tiene un coste

Entre cada map y reduce, para poder recuperarse de fallos potenciales, Hadoop
MapReduce hace una copia de los datos intermedios en disco. Lo conocido como
la fase Shuffle

#### Spark

Sigue siendo tolerante a fallos

Sigue siendo escalable

Pero su estrategia de manejo de latencia cambia un poco, de manera que se ve
reducida.

Esto lo consigue usando la programación funcional

##### Spark almacena los datasets en memoria, mientras que Hadoop lo hace en disco

### Introducción al analisis de datos con Spark

**Spark Core**

Contiene la funcionalidad básica de Spark, como programación de tareas, gestión de memoria,
recuperación ante fallos, interacción con sistemas de almacenamiento y otras cosas.


**Spark SQL**

- Antiguamente llamado Shark
- Es el paquete de Spark orientado a trabajar con datos estructurados a través de SQL o HQL
- Soporta varios tipos de datos como Hive, Parquet o JSON
- Permite intercalar comandos de manipulación de RDDs, lo que permite realizar análisis de
datos muy potentes

**Spark Streaming**

Es un componente de Spark que permite procesar
streams de datos en tiempo real, por ejemplo weblogs o
serverlogs mientras se van generando

#### Capas de almacenamientos aceptadas por Spark

- HDFS
- Cualquier otra soportada por Hadoop como Amazon S3, Cassandra, Hive, HBase, etc.
- Spark no requiere de Hadoop para funcionar. Simplemente aporta un soporte para
almacenamiento implementando la API de Hadoop
- Spark soporta TextFiles, SequenceFiles, Avro, Parket y cualquier otro formato de entrada
soportado por Hadoop


##### Podemos ver los usos de Spark en la imagen de mi repositorio UsosSpark.png

## Trabajando con RDDs

RDD: Resilient Distributed Dataset: es una simple, RESILIENTE e
INMUTABLE colección DISTRIBUIDA de objetos.

- Es RESILIENTE (tolerante a fallos): Podemos recuperar los datos en
memoria si se pierden.
- Es INMUTABLE: no podemos realizar modificaciones sobre un mismo RDD.
Si queremos modificarlo tendremos que crear uno nuevo.
- Es DISTRIBUIDO: cada RDD es dividido en múltiples particiones
automáticamente. El RDD puede ser ejecutado en diferentes nodos del
clúster.
- DATASET: Conjunto de datos. 2 tipos de fuentes: externas, datos en
memoria.

### 2 tipos de operaciones sobre los RDD:

- Transformaciones: operaciones que crean un nuevo RDD

- Acciones: operaciones que devuelven un resultado. Devuelven cualquier tipo de
datos menos un RDD.

El Spark Context es la manera que tenemos de comunicarnos
con el clúster

El método Parallelize convierte una Scala Collection local en un
RDD

El método textFile lee un fichero de texto desde HDFS o Local y
lo transforma en un RDD de tipo String

##### Podemos ver unas caracteristicas de tranformaciones y acciones en la imagen de mi repositorio TransAccSpark.png

### Transformaciones
Aplican Lazy Evaluation

- val inputRDD = sc.textFile("log.txt")
- val errorsRDD = inputRDD.filter(line => line.contains("error"))


En este ejemplo, filter no cambia el contenido de inputRDD, simplemente crea
punteros a un nuevo RDD, de manera que puede volver a ser reutilizado.

- errorsRDD = inputRDD.filter(line => line.contains("error"))
- warningsRDD = inputRDD.filter(line => line.contains(“warning")))
- badLinesRDD = errorsRDD.union(warningsRDD)


Esta forma de trabajar hace que, en caso de pérdida de datos, se pueda volver a
procesar todo de nuevo, de manera que no se pierda nada.

##### Las transformaciones más usadas son map(), flatMap() y filter()

### Acciones

La acción más típica es
reduce() -- los tipos de entrada y salida son iguales

- Opera sobre dos elementos del RDD y devuelve un resultado
- El ejemplo más simple es la suma de elementos
- De este modo es sencillo realizar sumas, cuentas o agregaciones
- val sum = rdd.reduce((x, y) => x + y)
- Todos los elementos del RDD deben ser del mismo tipo

##### También cabe recalcar que existe la función collect() para devolver el dataset completo

##### Las acciones más usadas son: count(),take(n),collect(),saveAsTextFile(file)

#### En mi repositorio tenemos distintas imagenes con las lista de transformaciones y acciones

## Pair RDDs

El formato (K,V) es muy útil para acciones
analíticas, que han de aplicarse a un conjunto de elementos pertenecientes a
la misma clave.

En Spark también es posible trabajar con este tipo de datos, y es con éste
como Spark muestra todo su potencial.

Las operaciones sobre objetos del tipo K-V son las más usadas en el mundo
Big Data, y son la clave del diseño de Map Reduce, especialmente para ETL y
análisis de datos.

Son muy útiles para trabajar con estructuras de datos complejos, donde
podemos elegir solo lo que nos interese

En Spark, los pares K-V se llaman Pair RDDs

El uso más importante que tienen es que te permite operar por clave (K) en
paralelo y reagrupar los datos a través de la red en base a ella.

### Transformaciones y Acciones sobre Pair RDDs

Las operaciones definidas sobre Pair RDDs no son válidas sobre RDDs regulares,
pero si podemos ejecutar las acciones vistas hasta ahora (acciones sobre RRD'S
normales) sobre PairRDD's.

### Transformaciones

- groupByKey
- reduceByKey
- mapValues
- keys
- join
- leftOuterJoin/rightOuterJoin

### Acciones

- countByKey

### Transformación con GroupKey

Volviendo a groupByKey, su definición es esta

**def groupByKey():RDD[(K, Iterable[V])]**

Es una agrupación sobre pair RDDs especializada en agrupaciones sobre los
Valores(V) que tienen la misma K. Esto implica que no tenemos que pasar como
argumento la función a aplicar, ni pares RDD.

El resultado de esta agrupación será un Pair RDD K-V con valores agrupados
por cada clave en una estructura iterable.

### Transformación reduceByKey
Es una de las funciones más útiles para trabajar con PairRDD

reduceByKey toma una función y únicamente tiene en cuenta los V del
PairRDD. Esto es así porque se da por hecho que los valores ya están
agrupados por K

### Transformación con mapValues

Se puede interpretar como

**Rdd.map{case (x,y): (x,func(y))}**

Que simplemente aplica una función sobre los valores de un PairRDD

### Transformación sortByKey

Esta función recibe un parámetro que indica si queremos que el orden sea
ascendente o no. Para que sea descendente, debemos colocar “false”

### Accion countByKey

Es importante recalcar que esta función es una acción.

Notar que es una función sin parámetros, siempre hará lo mismo:
contar el número de elementos por cada clave.

Devuelve un MAP(K,V) con K= la clave del MAP sobre el que se aplicó
la función y V= el número de elementos para esa clave.


##### En mi repositorio podemos encontrar imagenes de transformaciones y acciones de Pair RDDs

### Joins

Como para las funciones pasadas, esta función solo es válida para
PairRDDs

El concepto de Join es muy similar que el que tenemos para BBDDs.

Son muy usados en PairRDDs.

Básicamente combinan dos PairRDDs en uno.

Hay dos tipos básicos
- inner joins (join)
- outer joins (leftOuterJoin/rightOuterJoin)

La diferencia entre ambos es lo que ocurre con las claves cuando los dos
PairRdds a unir no tienen las mismas claves.

##### En mi repositorio poder ver un ejemplo de join

## SparkSQL

Es una interfaz pensada para trabajar con datos estructurados (con schema) y
semiestructurados.

Provee tres capacidades básicas:

1. Cargar datos estructurados de diversos tipos: JSON, Hive, Parquet,
etc..

2. Procesa consultas relacionales sobre esos datos desde dentro de
Spark y desde aplicaciones externas que tengan conectores con
Spark a través de (JDBC/ODBC) (Ej: Tableau)

3. Usado desde dentro de un programa Spark, provee integración con
java/python/scala e incluye la habilidad de hacer Joins con RDDs y
tablas entre otras cosas, de forma que facilita la construcción
completa de la aplicación.

### ¿Por qué utilizar SparkSQL?

La idea fundamental es que, al trabajar con datos estructurados, se pueden
optimizar las consultas. Si trabajamos de la manera tradicional, Spark no
conoce la estructura de los datos, por lo que no es posible optimizar

### Tablas

- Compuestas de filas y columnas.
- Típicamente representan una colección de objetos de un
tipo (empleados, productos..)
- Atributo= columna
- Row= fila, registro, tupla
- Relación= tabla

### DataFrame

Un **DataFrame** es una abstracción que representa el equivalente a una tabla

Cada vez que nos referimos a un DataFrame, podemos pensar en tablas

Por lo tanto, los DataFrame son RDDs de registros distribuidos con esquema
conocido


### SparkSession

Para empezar a usar sparkSQL necesitamos un SparkSession, que es
básicamente un SparkContext para SparkSQL

Para ello, necesitamos ejecutar

**import org.apache.spark.sql.SparkSession**


### Creacion de DataFrames

Se pueden crear de dos maneras

- Desde un RDD
  - Infiriendo un esquema
  - Creando un esquema explicito
- Leyendo datos desde un origen específico con esquema propio
  - Típicamente datos semi-estructurados o estructurados como Hive, Json, XML…

Los DataFrames aprovechan la potencia de las operaciones relacionales

Esto ayuda al optimizador de Spark a comprender qué es lo que queremos
hacer y variar un poco el orden en que se ejecutan las partes de la consulta
transparentemente al usuario. Por ejemplo, filtrar antes de un join.

La API de DataFrame tiene métodos similares a los de SQL

- SELECT
- WHERE
- LIMIT
- ORDER BY
- GROUP BY
- JOIN

## Spark Streaming

Spark Streaming no funciona totalmente en tiempo real. Simula el tiempo real
diviendo los datos que llegan en tiempo real en diferentes RDD's. De forma que
mezclamos la programación en lotes que utiliza Spark (BATCH) con la obtención
de datos en tiempo real.

Así como en Spark tenemos los RDDs, en Spark Streaming tenemos los DStreams
(discretized streams). Un DStream se compone de RDDs.

**Un DStream es una secuencia de datos que llegan en un periodo de tiempo**

**Un DSTREAM se compone de RDD's. Cada RDD representa los datos
recibidos durante un determinado periodo de tiempo (Dicho periodo se
especificará en la declaración del DSTREAM**

### Línea de funcionamiento

Primero se crea el StreamingContext, que es como el SparkContext, pero indicándole
la duración de cada proceso (batch)

Después se van creando los DStream a partir del fichero de origen aplicando la
configuración indicada en el StreamingContext

Posteriormente se ejecutan las operaciones sobre el Dstream, que se realizarán sobre
los RDDs agrupados en cada Dstream

Para comenzar el proceso se ejecuta la orden start()

Se espera a que se hayan procesado todos los Dstream con awaitTermination() 

### Operaciones Spark Streaming

Transformations, que generan otro Dstream de uno existente

Output Operations, que escriben datos a sistemas externos. Similares a las
acciones en RDDs

- print(), saveAsTextFiles(), saveAsObjectFiles()
- foreachRDD(function, time) - ejecuta una función en cada RDD del DStream

### Transformaciones Spark Streaming

Hay 2 tipos de transformaciones de RDDs que se pueden usar con
Dstreams:

- Transformaciones sin estado ("stateless"): donde el procesamiento de cada
lote (BATCH) o RDD no depende de los anteriores. Las operaciones que
podemos realizar son las que llevamos usando durante el curso.

- Transformaciones con estado ("stateful"): donde el procesamiento de cada
BATCH o RDD SI depende de los anteriores. Veremos ejemplos de estas
transformaciones a lo largo de esta presentación

### Operaciones salida del DStream

Salida a consola

  - print - imprime los primeros 10 elementos de cada RDD
  
Salida a fichero

  - saveAsTextFiles - guarda los datos como texto
  - saveAsObjectFiles - guarda ficheros con objetos serializados


Otras funciones

  - foreachRDD(function, time) - ejecuta una función en cada RDD del DStream

### CheckPointing

Los puntos de control (Checkpointing) son los mecanismos que tienen que
ser utilizados para conseguir tolerancia a fallos en Spark Streaming.

Permiten a Spark guardar datos, periódicamente, sobre la aplicación en un
sistema de almacenamiento (HDFS, Amazon S3...) para usar en caso de
recuperación



