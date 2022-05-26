
## YARN y MAP REDUCE
Si da problema con MapReduce con Java, en especifico este error: no se ha encontrado o cargado la clase principal org.apache.hadoop.mapreduce.v2.app.MRAppMaster. Mirar este link:
https://programmerclick.com/article/8992195719/

## HIVE y HUE

### hive-site.xml
- Linea 819 -> Cambiar false por true
- Linea 806 -> Cambiar de true a false
- Linea 4829 -> Cambiar de true a false

## SQOOP
Importante actualizar .bashrc en todos los nodos cuando se hagan cambios en el nodo1 para evitar problemas

## ZOOKEEPER
Utilizar versión del video Zookeeper
Si da fallo al hacer hdfs --daemon start journalcode: Cannot set priority. Como no creaba la carpeta a la que apuntaba en el archivo hdfs-site.xml, la he creado yo,
lo que pasaba es que no tenía suficientes permisos, así que ha bastado un chmod 777 /datos/jn

## SPARK
Tras pasar al módulo de spark, volver poner los archivos xml modificados, core-site y hdfs-site a como estaban.
Instalar python3 si da fallo 
