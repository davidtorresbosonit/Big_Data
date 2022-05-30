# Ejercicios

## Ejercicio 1. ¿Qué pasaría si cancelamos (utilizando Ctrl+C) uno de los
consumidores (quedando 2) y seguimos enviando mensajes por el producer?

Pues seguirán llegando mensajen a los otros dos consumidores.

## Ejercicio 2. ¿Qué pasaría si cancelamos otro de los consumidores (quedando ya
solo 1) y seguimos enviando mensajes por el producer?

Si queda uno, solo le llegarán a ese consumidor

## Ejercicio 3. ¿Qué sucede si lanzamos otro consumidor pero está vez de un grupo
llamado my-second-application leyendo el topic desde el principio (--from-beginning)?

Que muestra todos los mensajes que se habían enviado anteriormente aunque esté en otro grupo

## Ejercicio 4. Cancela el consumidor y ¿Qué sucede si lanzamos de nuevo el
consumidor pero formando parte del grupo my-second-application?¿Aparecen los mensajes desde el principio?

No, no aparecen

## Ejercicio 5. Cancela el consumer, a su vez aprovecha de enviar más mensajes
utilizando el producer y de nuevo lanza el consumidor formando parte del grupo my-second_application ¿Cuál fue el
resultado?

Sigue sin aparecer ningún resultado


# EJERCICIOS FINALES


## Crear topic llamado "topic_app" con 3 particiones y replication-factor = 1.
kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic topic_app --create --partitions 3 --replication-factor 1


## Crear un producir que inserte mensajes en el topic recien creado (topic_app).
kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic topic_app

## Crear 2 consumer que forman parte de un grupo de consumo llamado "my_app".
kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic topic_app --group my_app

## Interactuar con los 3 elementos creando mensajes en el producir y visualizar como estos son consumidos por los consumer

VER IMAGEN BLOQUE1.PNG

## Aplicar los comandos necesarios para listar los topics, grupos de consumo, así como describir cada uno de estos

- Listar topics
    - kafka-topics.sh --zookeeper 127.0.0.1:2181 --list

- Listar groups
    - kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --list

- Describe topics
    - kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic topic_app --describe
    - kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic first_topic --describe
    - kafka-topics.sh --zookeeper 127.0.0.1:2181 --topic new_topic --describe

- Describe groups
    - kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --describe --group my-first-application
    - kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --describe --group my-second-application
    - kafka-consumer-groups.sh --bootstrap-server 127.0.0.1:9092 --describe --group my_app
