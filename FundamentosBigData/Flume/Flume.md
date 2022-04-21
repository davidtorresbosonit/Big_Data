# Flume

ApacheFlume es un sistema distribuido,confiable y preparado para recopilar,agregar y mover de forma eficiente grandes cantidades de datos de diversas fuentes a un almacén de datos centralizado.

Posee una arquitectura sencilla y flexible basada en flujos de datos en streaming.

Es robusto y tolerante a fallos con múltiples mecanismos de configuración.

Utiliza la transaccionalidad en la comunicación entre sus componentes.

## Conceptos Básicos

Flume significa “CanalArtificial”

Log se puede traducir,entre otras cosas,como “Tronco”

## Componentes

Flume se compone de los siguientes componentes principales:

- **Event**:Es la unidad de dato que se va propagando a través de la arquitectura 
- **Source:** Es el origen de los datos 
- **Sink:** Es el destino de los datos 
- **Channel:** Es el buffer de almacenamiento intermedio que conecta el source con el sink.

## Setup

Flume funciona como un agente levantado en la máquina desde la que se quiere recoger la información.

La configuración de este agente se realiza en un fichero local.

Este fichero de configuración contiene las propiedades de cada source,channel y sink que vayamos a definir.

## Sources

EvenDriverSource: Son activos.Controlan cómo y cuándo los eventos son añadidos al channel.Responden al comportamiento “push”.El ejemplo más claro es el Avrosource.Cuando recibe una RPC(RemoteProcedureCall)con uno o mas eventos,inmediatamente los añade al channel.
PollableSource:Son pasivos.No hay forma de saber cuándo llega un nuevo dato que sera enviado através del flow,por lo que Flume tiene que “tirar de ellos:pull”cada cierto tiempo.Son fáciles de configurar pero proveen menos control.

Podemos ver sources predefinidos en la imagen de mi repositorio SourcesPredefinidosFlume1.png y SourcesPredefinidosFlume2.png

## Sink

Se encargan de extraer evento de un channely almacenarlos en un sistema externo o enviarlos al siguiente agente del flow.

Podemos ver sink predefinidos en la imagen de mi repositorio SinkPredefinidosFlume.png

## Channels

Podemos ver channels predefinidos en la imagen de mi repositorio ChannelsPredefinidosFlume.png

## Interceptors

Flume permite modificar eventos en caliente mediante interceptores.
Podríamos decir que los interceptores actúan como si fuera una pequeña ETLcon una serie de funciones predefinidas.

Podemos interceptors predefinidos en la imagen de mi repositorio InterceptorPredefinidosFlume.png


