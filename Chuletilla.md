## Hadoop

#### Muestra el contenido del directorio root en HDFS

Hadoop fs -ls /

#### Comando para añadir un archivo en HDFS. EJEMPLO

hadoop fs -put shakespeare /user/cloudera/shakespeare

#### Comando para copiar un archivo de local a HDFS

hadoop fs -get

## Hive

#### Cargar fichero desde HDFS. EJEMPLO

Load data inpath ‘/user/Cloudera/hive/iris_completo.txt’ into table iris;

## Sqoop

#### Comprobar que Sqoop esta conectado con MySQL

sqoop list-databases --connect jdbc:mysql://localhost --username root --password cloudera

#### Ejemplo de import entre hive y MySQL

sqoop import --connect jdbc:mysql://localhost/pruebadb --table tabla_prueba --username root --password cloudera -m 1 --hive-import 
 --hive-overwrite --hive-table prueba_sqoop_hive.tabla_prueba
 

