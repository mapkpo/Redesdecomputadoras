# Capítulo 15: Visión General de las Redes de Área Local

---

## Preguntas Teóricas (Enunciados)

**15.1.** ¿Qué diferencias hay entre los requisitos clave para las redes existentes en salas de computadores de aquellos necesarios para redes de área local de computadores personales?

**15.2.** ¿Qué diferencias hay entre una red LAN de respaldo, una red SAN y una red LAN troncal?

**15.3.** ¿Qué es la topología de una red?

**15.4.** Enumere cuatro topologías comunes para redes LAN y describa brevemente su principio de funcionamiento.

**15.5.** ¿Cuál es el propósito del comité IEEE 802?

**15.6.** ¿Por qué existen diferentes normativas para redes LAN?

**15.7.** Enumere y describa brevemente los servicios proporcionados por LLC.

**15.8.** Enumere y describa brevemente los modos de operación proporcionados por el protocolo LLC.

**15.9.** Enumere algunas funciones básicas que se realicen en la capa MAC.

**15.10.** ¿Qué funciones lleva a cabo un puente?

**15.11.** ¿Qué es un árbol de expansión?

**15.12.** ¿Qué diferencias existen entre un concentrador y un conmutador de capa 2?

**15.13.** ¿Cuál es la diferencia entre un conmutador de almacenamiento y envío y uno rápido?

---

## Respuestas Teóricas

15.1 La principal diferencia entre las LAN de computadoras personales y redes en salas de computadores es la velocidad y el precio. El requisito principal de las redes de respaldo es la transferencia elevada de datos entre un número limitado de dispositivos en un área reducida, junto con la alta fiabilidad. en cambio en las redes LAN personales el requisito principal es el bajo coste ("El coste de la conexión a la red debe ser significativamente menor que el del propio dispositivo conectado"). A menor coste tambien signifca que la velocidad de la red puede quedarse liimitada, por eso en redes con dispositivos muy caros conectados es mas que recomendable la inversion en redes mas veloces y de mayor costo.

15.2 La principal diferencia entre una red LAN de respaldo, una SAN y una red LAN troncal es que resuelven distintos problemas.

La red de respaldo interconecta sistemas grandes y caros: mainframes, supercomputadores y dispositivos de almacenamiento masivo, dentro de una sala de computadoras. Su objetivo es la transferencia de datos a muy alta velocidad entre un número reducido de dispositivos con alta fiabilidad.

La red SAN es una evolucion de la red de respaldo,esta es una red de respaldo especializada y reestructurada específicamente para el almacenamiento, que desliga las tareas de almacenamiento de servidores específicos.

por ultimo la red LAN troncal resuelve un problema distinto, no de rendimiento entre dispositivos caros, sino de organizacion de conexiones entre multiples LAN, esta surge porque desplegar una única LAN para todo un edificio tiene tres problemas serios:

Fiabilidad: una caída de esa LAN única afecta a todos los usuarios.
Capacidad: se satura a medida que crece el número de dispositivos conectados.
Coste: una sola tecnología de LAN no es óptima para todos los requisitos de interconexión, y forzar a microcomputadores baratos a usar una red de gran capacidad no tiene sentido economico.

La solucion a esto es usar LAN de menor coste y capacidad por edificio o departamento, e interconectarlas todas mediante una LAN de mayor capacidad, que es justamente la LAN troncal.

15.3 "En el contexto de una red de comunicaciones, el término topología se refiere a la forma según la cual se interconectan entre sí los puntos finales, o estaciones, conectados a la red".

la topologia describe el patron geometrico y logico de interconexion entre las estaciones de la red, se describen 4 topologias LAN principales: Bus, arbol, anillo y estrella.


15.4 Topologia en Bus y en arbol: Ambas se caracterizan por la conexión multipunto. La topologia bus todas las estaciones se encuentran conectadas directamente a traves de taps, su funcionamiento es full-duplex. En cambio la topologia en árbol, es una generalizacion de la topologia en bus, empieza desde un punto conocido conocido como raiz o cabecera, donde uno o mas cables comienzan desde ahi y cada uno puede presentar ramificaciones.
El principal problema de este tipo de conexion es el metodo para elegir a quien pertenece la informacion transmitida, ya que la misma alcanza todas las estaciones, y de que manera regular la comunicación, ya que dos o mas pueden transmitir al mismo tiempo ocasionando distorsion.

Topología en anillo: Consta de un conjunto de repetidores conectados formando un bucle cerrado. El enlace es unidireccional, los datos se transmiten en un solo sentido a través de repetidores donde los datos se transmiten en tramas, donde al llegar al destino, copia la trama y sigue su rumbo hasta llegar de nuevo a su origen.

Topología en estrella: Cada estación esta conectada a un nodo central a través de dos enlaces, uno para transmisíon y otro para recepción.
Su funcionamiento puede ser muy parecido a la topologia en bus, donde una estacion retransmite a traves de todos los enlaces de salida del nodo central.
Otro modo de funcionamiendo es usar el nodo como un dispositivo de conmutación (switch), donde la trama entrante se almacena en el nodo temporalmente y luego se transmite hacia la estacion de destino.


15.5 El proposito del comite es desarrollar estandares de redes LAN y WAN enfocados en aspectos de la capa fisica y enlace de datos para mantener redes interoperables. Son responsables por las principales tecnologias de conexion en redes como Ethernet, WiFi, vLAN, STP, etc.

15.6 Las diferentes normativas para las redes lan existen para acomodar requisitos diferentes en implementacion. Las normativas tratan de mantener interoperabilidad para un estandar pero mantienen estandares diferentes de medios fisicos, velocidades o tecnologia de transmision. Esta versatilidad permite tener dispositivos moviles(los cuales no pueden cablearse comodamente) y dispositivos fijos en una misma red utilizando dispositivos que utilizen dos o mas tecnologias para interoperar en estas normativas.

15.7 La subcapa LLC proporciona 3 tipos de servicios:
- servicio no orientado a conexion sin confirmacion: Este no garantiza la recepcion de datos, dejando esa tarea a capas superiores. Util cuando manterner una conexion es demasiado caro computacionalmente o cuando una capa superior ya implementa deteccion de errores/perdida de paquetes
- servicio en modo conexion: los dos "usuarios" forman una conexion por la cual intercambian datos, en esta existe el control de flujo y deteccion de errores. Util cuando la implementacion de software de las capas superiores es muy simple, LLC reduce la necesidad de implementar los mecanismos que ya provee
- servicio no orientado a conexion con confirmacion: no existe conexion previa pero el receptor confirma recibir los datagramas. Util cuando hay demasiados dispositivos no centrales para mantener conexiones activas pero se requiere confirmacion de recepcion de datagramas

15.8 Los tres tipos de operacion son:
- operacion de tipo 1: presta el servicio no orientado a conexion sin confirmacion utilizando la Pdu de informacion no numerada
- operacion de tipo 2: presta el servicio en modo conexion utilizando el modo de operacion balanceado asincrono de HDLC(unicamente)
- operacion de tipo 3: presta el servicio no orientado a conexion confirmado con dos PDU, una de orden y una de respuesta para confirmar que la anterior fue recibida

15.9 En la capa mac se realizan las siguientes funciones:
- control de accesso al medio
- deteccion de errores mediante CRC
- control de tamaño y formato de tramas
- direccionamiento fisico(mediante direcciones de origen y destino)

15.10 Un puente se encarga de connectar redes LAN similares. Estos realizan dos funciones en ambas direcciones entre dos redes lan:
- Lectura de las tramas transmitidas en red 1 y aceptar tramas dirigidas a la red 2
- retransmitir hacia la red 2 todas las tramas

15.11 Es un algoritmo para encaminamiento entre redes, util para cuando existen caminos redundantes. Se basa en 3 aspectos:
- retransmision de tramas
- aprendizaje de direcciones
- evitar bucles
Es importante el ultimo en caso de que se emita un broadcast y no cree un bucle infinito. STP bloquea uno de los enlaces para cortar bucles y lo rehabilita en caso de que sea necesario

15.12 La principal diferencia entre un concentrador(hub) y un conmutador de capa 2(switch) es que el switch solo emite los paquetes entrantes a el puerto correspondiente al destinatario.
un hub repite las tramas a todos los puertos sin entender quien debe recibirlos. Los dispositivos en un mismo hub no pueden transmitir al  mismo tiempo, ya que los paquetes colisionarian
Ademas el hub distribuye el ancho de banda de la conexion entre los dispositivos conectados, mientras que un switch mantiene la velocidad maxima del link para cada uno.

15.13 La principal diferencia es que el conmutador rapido inicia la transmision de la trama al receptor cuando aun esta recibiendo la trama del remitente, esto es posible ya que cuando recibio el inicio de la trama con la direccion mac de destino sabe a donde debe transmitir. En comparacion un conmutador de almacenamiento y envio acepta la trama y almacena su totalidad antes de retransmitirla a el puerto correspondiente.
El conmutador rapido tiene la desventaja que no puede detectar tramas erroneas antes de retransmitirlas, ya que necesita conocer la trama entera para verificar su crc.
