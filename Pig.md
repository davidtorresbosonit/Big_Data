# PIG

## Conceptos Básicos

- Las Bases de Datos Relacionales tienen tablas, filas, columnas y campos
- Un fieldes un elemento en sí mismo.
- Una collection de valores es llamado tuple.
- Una collection de tupleses llamado bag.
- Una relación es simplemente una bagcon un nombre asignado (alias)

## Sintaxis Básica

### KeyWords

Las palabras clave son palabras reservadas por PIG. No es posible utilizar dichas palabras para nombrar cosas. Ejemplo: **LOAD, AS, FILTER, BY, STORE, INTO...**

### Identificadores

Los identificadoresson los nombres asignados a campos u otras estructuras

### Comentarios

PigLatin soporta dos tipos de comentarios
- Línea sencilla comentada comenzando por --
- Múltiples líneas comentando comenzando por /* y finalizando por */

### Operaciones Comunes

Muchos operadores son similares a los utilizados en SQL
- PigLatinusa == y != para las comparaciones

## Carga y Almacenamiento de datos

La función por defecto para la carga de datos se denomina PigStorage
- El nombre de la función está implícito en la instrucción LOAD
- PigStorage asume el formato de texto separando las columnas por tabulador

### Almacenamiento de datos

El comando usado para obtener la salida nos indicará el formato de la misma

- DUMP: Muestra la salida por pantalla
- STORE: Envía los resultados al disco (HDFS)

Con el comando LOAD, el uso del ‘PigStorage’ está implicito
- El delimitador de los campos es el de por defecto (tab)
- Es posible indicar un delimitador propio por ejemplo: `STORE bigsales INTO 'myreport' USING PigStorage(,);`

## Tipos de datos simples

- Pigsoporta muchos tipos de datos básicos
  - Similar a muchas bases de datos o lenguajes de programación
 - Pigtrata a los “fields” no identificados como arrayde bytes
  - Llamado bytearrayen Pig

Podemos una tabla con tipos de datos simples en la imagen de mi repositorio DatosSimplesPig.png

### Datos Inválidos

Cuando nos encontramos con datos inválidos, Pig los sustituye por NULL

## Filtrado y Ordenación de datos

### Filtrado de registros

El comando FILTER nos permitirá extraer las tuplas que cumplan un determinado requisito

Es posible combinar diferentes requisitos con AND y OR

### Comparación de campos

El operador == es soportado por cualquier tipo de dato

PigLatin soporta la utilización de patrones a través de expresiones regulares de Java

### Selección y comparación de campos

Es posible realizar la extracción de columnas gracias a los operadores FOREACH y GENERATE

Con los operadores FOREACH y GENERATEpodemos generar nuevos campos

El comando DISTINCT elimina los registros duplicados de una “bag”

El comando ORDER....BY permite ordenar todos los registros de una “bag” en orden ascendente

## Funciones básicas

En PIG podemos utilizar diferente funciones predefinidas.

Podemos ver un ejemplo en la imagen FuncionesPredifinidasPig.png de mi repositorio



