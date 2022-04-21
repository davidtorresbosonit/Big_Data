# IMPALA

### Es un motor SQL de elevado performance pensada para operar sobre grandes volúmenes de datos

### Impala corre sobre clusters Hadoop
- Puede ejecutar Queriessobre HDFS o Hbase
- Lee y escribe datos sobre ficheros con tipos de datos típicos de Hadoop

### Originalmente desarrollada por Cloudera

## Carácteristicas

Impala ejecuta las queries directamente sobre el cluster en lugar de ejecutar MapReduce para procesar

Es en torno a unas 5 veces más rápido que Hiveo Pig, aunque  a menudo puede ser hasta 20 veces más rápido.

Está especialmente optimizado para ejecutar Queries.

## Por qué usar Impala

### Es más efectivo que programar MapReduce

### Hay mucha más gente en el mundo capaz de escribir SQL en lugar de Java

### Ofrece interoperabilidad con otros sistemas

## IMPALA Vs HIVE

Hive e Impala son herramientas diferentes, pero ofrecen bastantes similitudes
- Ambas usan variantes de SQL 
- Ambas compartenel mismo metastorey data warehouseen el cluster
- En proyectos grandes se suelen usar juntas

Las queriesen Impala y Hive operan sobre tablas, igual que en RDBMS(Sistema de BD Relacional)

La estructuray localizaciónde las tablas se definen cuando se crean

### Estas son algunas características que Hive puede hacer pero Impala no:
- Ficheros con tipos de datos a medida
- El tipo de datos DATE◦Funciones XML y JSON
- Algunas funciones de agregación como: “covar_pop, covar_samp, corr, percentile, percentile_approx, histogram_numeric, collect_set”
- Sampling(que es el ejecutar queries sobre un subset de una tabla en lugar de sobre toda la tabla)
- Vistas laterales (sobre una columna de una tabla, fila a fila, se le aplica una función (que crea un resultado en forma de vista en ejecución) y sobre ese resultado se aplica otra función, que es lo que se muestra.
- Multilplescláusulas DISTINCT por query
- UDFs(soportadas a partir de impala  1.2)

## IMPALA: Tolerancia a fallos

Impala al contrarío de Hive, no tiene tolerancia a fallos

## IMPALA: Optimización

En Impala es posible optimizar la ejecución de las queries simplemente informando de las características de las tablas involucradas en dicha query.

Esto se hace mediante el comando COMPUTE STATS
Es recomendable ejecutarlo: 
- Justo después de cargar las tablas
- Cuando haya una modificación en una tabla del 20% o más

Podemos ver más info en la imagen del repositorio llamada ComputeStats.png

## Sentencias:

- $ impala-Shell
- CREATE DATABASE IF NOT EXISTS ejemplo;
- SHOW DATABASES;➢USE ejemplo;
- CREATE TABLE IF NOT EXISTS ejemplo.estudiante(name STRING, age INT, contact INT );
- insert into estudiante(name,age,contact)VALUES ('Ramesh', 32, 941587841);
- Select * from estudiante;


Funciona al igual que hive,con sentencias SQL.

## HIVE Vs IMPALA: Aclaración

**Impala:** Consultas ligeras para buscar velocidad, tener en cuenta que si falla tenemos que relanzar la query(diapositiva 18).
**Hive:** Mejor para trabajos pesados de ETL, buscamos la robustez no tanto la velocidad, y tenemos tolerancia a fallos.
