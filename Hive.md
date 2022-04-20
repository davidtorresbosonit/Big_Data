# Hive
- Es una infraestructura para el almacenaje y consulta de datos basada en Hadoop
- Hadoop proporciona escalabilidad masiva y con capacidades de tolerancia a fallos para el procesamiento y almacenamiento de datos
- Hive está diseñado para facilitar la consulta y el análisis de grandes volúmenes de datos
- Hive no es un gestor de bases de datos relacionales
- Es un sistema de procesamiento por lotes (batch). Por tanto, tiene una latencia muy alta
- Para conjuntos de datos pequeños su rendimiento no es comparable al de sistemas tradicionales (Oracle, MySQL, etc.)

## Niveles de granularidad

- **Bases de datos:** espacio de nombres que agrupa tablas y otras unidades de datos
- **Tablas:** unidades de datos homogéneas que comparten un mismo esquema
- **Particiones:** cada tabla puede tener una o más claves de particionado que determinan cómo se almacenan los datos. Optimizan consultas
- **Buckets(o Clusters):** los datos dentro de cada partición pueden, a su vez, dividirse en bucketsbasados en el valor de una función de dispersión sobre alguna columna de la tabla. Optimizan joins.

## N-Grama

- Un n-gramaes una combinación de “n” palabras
- Se suele utilizar para:
  - Sugerir corrección de palabras cuando hacemos búsquedas
  - Encontrarlas palabras más importantes en los textos
  - Identificartrendingtopics

## Ventanas 
- Se utilizan para realizar funciones de agregación a una partición o subconjunto de filas. Ofrecen muchas más posibilidades que las funciones de agregación típicas
- En funciones agregadas normales utilizamos típicamente el GROUP BY

## Cargar fichero desde HDFS. EJEMPLO

Load data inpath ‘/user/Cloudera/hive/iris_completo.txt’ into table iris;
