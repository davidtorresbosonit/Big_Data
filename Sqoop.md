# Sqoop

Sqoopes una herramienta Open Sourcecreada originalmente por Cloudera.

Es una herramienta para transferir datos entre RDBMsy Hadoop

Es posible acceder a los datos de una BBDD como si fuera un origen más especificándolo en nuestro Mapper

Su objetivo fundamental es transferir datos entre RDBMS y Hadoop(HDFS). 

Hay varias opciones:◦Transferir solo una tabla
- Transferir todas las tablas en una BBDD
- Transferir partes de una tabla. Sqoopsoporta la cláusula WHERE de SQL

Para importardatos utiliza MapReduce

Los datos son importados a HDFS como textfiles delimitados o SequenceFiles

Es posible usarlo para importaciones de datos incrementales
- El primer importimporta todas las filas en una tabla
- El resto de importssolo las filas creadas desde la última importación (argumentos)

## Conectores

### Conectores Genéricos

Se utilizan para configurar los parámetros básicos de sqoop

### Conectores a medida

Existen conectores específicos para diferentes BBDD
- Su objetivo es proveer de una interfaz más rápida de importación
- Habitualmente no son opensourcepero si son gratis

## Compatibilidad con BDD

El modo direct permite conectar a la base de datos sin utilizar JDBC, lo cual permite mayor rapidez.
Como hemos comentado, existen otros conectores no OpenSourcepero sí gratuitos. 

Podemos una tabla con información en mi repositorio llamada CompatibilidadSqoop.png

## Sintaxis Básica

La sintaxis básica corresponde a lo siguiente:
- sqooptool-name[tool-options]


Ejemplos de tool-name:
- import
- import-all-tables
- list-tables


Ejemplos de tool-options:
- --connect
- --username
- --password

## Hive

Es posible importar datos directamente a Hive en lugar de hacerlo a HDFS
Para ello se utiliza el comando --hive-import
