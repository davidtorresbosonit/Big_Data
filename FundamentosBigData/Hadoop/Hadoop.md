# Hadoop

Hadoop(10 años) es un frameworkopensourcepara almacenar datos y ejecutar aplicaciones en clustersde hardware básicos. (En disco, Sparken memoria).

 ##### Lo más importante en Hadoop es:
 - Llevar el procesamiento a los datos 
 
 ##### Hadoop es 
  - Escalable horizontalmente y con coste reducido
  - +Datos
  - +Potencia
  - Tolerante a fallos
  - Que un servidor falle es inevitable
  - Pero los sistemas deben seguir funcionando
  - De manera transparente al usuario◦Sin perder datos
  - Debe recuperarse sin intervención del usuario
  
  
  ##### Hadoop está programado en Java
  - Originalmente se interactúa con él, programando en Java
  - Aunque existe la posibilidad de hacerlo con otros lenguajes de programación o herramientas
  - El programador solo se preocupa de codificar el código que resuelve el caso de uso, no se encarga de gestionar la coordinación, sincronización o los posibles   fallos   del sistema
  
  ##### Tipos de datos en Hadoop:
   - Estructurados
   - Semi-estructurados
   - No estructurados
   
   ##### Hadoop se compone de 
   - HDFS 
   - Almacena datos en el cluster
   - MapReduce◦Procesa datos en el cluster
   
   ## Cluster
   Un cluster se compone de un conjunto de servidores (nodos) que trabajan juntos para conseguir un objetivo común
   
   ## HDFS
   HDFS es un sistema de archivos nativo de Google escrito en Java
   
   HDFS es óptimo cuando trabaja con un cantidad moderada de archivos de gran tamaño
   
   HDFS está pensado para escribir una vez y leer muchas
   
   ## MapReduce
   Conceptos fundamentales
   - El programador solo tiene que definir:
    - El Mapper
    - El Reducer
    - El Driver
   ### Mapper
   - Actúa sobre cada registro de entrada◦Cada tarea, Task, opera sobre un único bloque en HDFS, siempre que sea posible
   - Cada Taskopera en el nodo donde el bloque está almacenado
   - La salida del Mapes un par (Clave/Valor)
   ### Suffle&Sort
   -Ordena por clave y agrupa todos los datos intermedios de todos los Mappersde una misma clave en el formato (K, [V1...Vn])
   -Ocurre justo después de que todos los Mappershayan terminado y justo antes de que la fase Reduce comience
  ### Reducer
  - Recibe la salida del S&S y realiza operaciones sobre ella
  - Produce la salida final
 
 ## Terminología
 - Un Jobes un programa entero, una ejecución completa de Mapsy Reduces sobre un dataset
 - Una Taskes la ejecución de un solo Mapo Reduce sobre una porción de datos, habitualmente un Bloque.
 - Un intento de Taskse refiere a una ejecución concreta de una Tasksobre un bloque de datos

## Comandos

#### Muestra el contenido del directorio root en HDFS

Hadoop fs -ls /

#### Comando para añadir un archivo en HDFS. EJEMPLO

hadoop fs -put shakespeare /user/cloudera/shakespeare

#### Comando para copiar un archivo de local a HDFS

hadoop fs -get
 

