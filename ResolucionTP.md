# 1 Capa de Enlace de Datos y Trama Ethernet
## 1A) 
La capa de enlace de datos, correspondiente a la capa 2 del modelo OSI, se encarga de la comunicación entre dispositivos conectados al mismo enlace o red local. Su función es recibir los datos de la capa de red, organizarlos en tramas y agregar la información necesaria para que puedan ser transmitidos a través del medio físico. Además, permite identificar los dispositivos dentro de la red local y detectar posibles errores durante la transmisión.

## 1B) 
La dirección MAC es código único de 48 bits que identifica de forma física a una tarjeta de red o dispositivo que tenga conexión a la red local, mientras que la dirección IP se utiliza para direccionar paquetes entre redes a cualquier interfaz accessible posiblemente por internet. 

## 1C) 
Una trama Ethernet es la unidad de información que utiliza Ethernet para transmitir datos en una red local. Está formada por distintos campos. El preámbulo y el SFD (Start Frame Delimiter) permiten sincronizar la sus clocks para la comunicación e indicar el inicio de la trama correspondientemente. Luego se encuentran las direcciones MAC de destino y de origen, que identifican al receptor y al emisor. El campo Tipo/Longitud (EtherType)indica qué protocolo se encuentra encapsulado o el tamaño de los datos. El campo de datos contiene la información transmitida y, si es necesario, se agrega padding para alcanzar el tamaño mínimo de la trama. Finalmente, el campo FCS permite detectar errores durante la transmisión mediante un código CRC.
 <img width="577" height="92" alt="image" src="https://github.com/user-attachments/assets/563f07a5-f2d3-49c7-a885-9a789564472b" />

## 1D) 
El protocolo de la capa superior se especifica en el campo EtherType. Este campo puede especificar el tipo de protocolo o el largo del payload dependiendo de su rango(<=1500 significa un largo de payload). Puede especificar protocolos como ipv4, ipv6, ARP, PTP u otros.

# 2 Análisis de Trama Ethernet (Wireshark)

```
Frame 746: Packet, 54 bytes on wire (432 bits), 54 bytes captured (432 bits) on interface \Device\NPF_{E45EE9E6-86F0-41E2-836B-E3F8FEFED316}, id 0
Ethernet II, Src: GigaByteTech_8c:69:ef (b4:2e:99:8c:69:ef), Dst: SagemcomBroa_fd:8c:7a (b8:66:85:fd:8c:7a)
    Destination: SagemcomBroa_fd:8c:7a (b8:66:85:fd:8c:7a)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Source: GigaByteTech_8c:69:ef (b4:2e:99:8c:69:ef)
        .... ..0. .... .... .... .... = LG bit: Globally unique address (factory default)
        .... ...0 .... .... .... .... = IG bit: Individual address (unicast)
    Type: IPv4 (0x0800)
    [Stream index: 11]
Internet Protocol Version 4, Src: 192.168.0.151, Dst: 142.251.150.119
    0100 .... = Version: 4
    .... 0101 = Header Length: 20 bytes (5)
    Differentiated Services Field: 0x00 (DSCP: CS0, ECN: Not-ECT)
    Total Length: 40
    Identification: 0x73a4 (29604)
    010. .... = Flags: 0x2, Don't fragment
    ...0 0000 0000 0000 = Fragment Offset: 0
    Time to Live: 128
    Protocol: TCP (6)
    Header Checksum: 0x0000 [validation disabled]
    [Header checksum status: Unverified]
    Source Address: 192.168.0.151
    Destination Address: 142.251.150.119
    [Stream index: 16]
Transmission Control Protocol, Src Port: 49989, Dst Port: 443, Seq: 2714, Ack: 4093, Len: 0
```

## 2A) 
Origen: b4:2e:99:8c:69:ef (Puerto ethernet del PC utilizando wireshark) Destino: b8:66:85:fd:8c:7a (Dirección del gateway/router)

## 2B) 
IP origen: 192.168.0.59 (direccion de la LAN de la PC utilizando wireshak) IP destino: 142.251.150.119 (IP publica del servidor con la pagina web)

## 2C) 
Las direcciones de origen conciden al mismo dispositivo dentro de la red local, ya que tienen una asignación dhcp relacionándolas. Pero las direcciones de destino no representan el mismo dispositivo, esto se debe a que el ultimo dispositivo accesible en la red local en camino al destino es el router. Por lo tanto la trama ethernet se resuelve ahí. En el camino al destino se generan múltiples tramas a menos que el destino sea accesible por Layer 2 estando en la misma subred conectado posiblemente por switches, en cual caso las direcciones ip y mac del destino representaran el mismo dispositivo.

## 2D)
 el ethertype es ipv4 ya que este es el utilizado por defecto en acceder a google.com

# 3 Protocolo de Transporte TCP

## 3A) 
El protocolo tcp resuelve múltiples aspectos de la comunicación:
- Detecta la perdida de paquetes (Ethernet y IP no garantizan que se recibio un paquete)
- Comunica el orden de los paquetes
- Controla la velocidad para no saturar la red o el receptor
- Utiliza múltiples "puertos" para representar a que aplicación entregar el paquete

## 3B)
- Puerto de origen y destino: identifican que aplicaciones participan en la comunicación
- Numero de secuencia: representa la posición de los datos dentro del flujo total de la sesión, para ordenarlos en una comunicación mas larga aunque lleguen desordenados
- Numero de ACKnowledgment: indica el numero de secuencia del próximo paquete, permite detectar paquetes perdidos
- Longitud de cabecera: indica el largo de la cabecera para saber cuando comienzan los datos reales
- CRC: permite detectar si el paquete sufrió corrupción durante la transmisión
- Puntero Urgente: comunica que el contenido del segmento debe saltarse la cola de espera para resolverse antes

## 3C) 

Para explicar los handshakes se utiliza el nombre de iniciador para el dispositivo que manda el primer paquete del handshake y receptor para su contraparte, de la forma
iniciador -> receptor

El 3 way handshake inicia una conexión:
- ->SYN solicita la apertura de una conexión y comunica la numeración de los bytes que enviara en iniciador
- <-SYN-ACK Confirma que recibió el SYN y abre la conexion en sentido opuesto desde el receptor al iniciador
- ->ACK se confirma la conexion del paso 2(el iniciador confirma la conexion desde el receptor)

Luego de esto ambos quedan como ESTABLISHED y la transmision puede comenzar

El four way handshake cierra la conexion en ambas direcciones:
- ->FIN el iniciador indica que cierra su canal de salida
- <-ACK el receptor acepta que no recibira mas datos pero puede seguir emitiendolos
- <-FIN(receptor) el receptor termino de enviar sus datos pendientes y cierra su propia conexion
- ->ACK(receptor) el iniciador reconoce el cierre

## 3DEF)
  Teniendo abierto el wireshark con adapter for loopback, luego abriendo amabas instancias del packet sender y configurando el puerto abierto, en este caso fue 51200, podemos ver los envios de informacion y el handshake de finalizacion de conexion, lo cual nos deja ver a simple vista lo facil que es espiar informacion estando conectando en una red, simplemente sabiendo en donde buscar 
  <img width="1144" height="302" alt="image" src="https://github.com/user-attachments/assets/65c36d4b-3d1f-4d51-a6ba-75e3bbeb6639" />
```
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 51210, Dst Port: 51200, Seq: 1, Ack: 1, Len: 41
Data (41 bytes)

0000  63 75 69 64 61 64 6f 2c 20 6c 61 20 69 6e 66 6f   cuidado, la info
0010  72 63 6d 61 63 69 6f 6e 20 63 6f 6e 66 69 64 65   rcmacion confide
0020  6e 63 69 61 6c 20 65 73 0d                        ncial es.

No.     Time           Source                Destination           Protocol Length Info
     15 35.167630400   127.0.0.1             127.0.0.1             TCP      44     51200 → 51210 [ACK] Seq=1 Ack=42 Win=2619648 Len=0

Frame 15: Packet, 44 bytes on wire (352 bits), 44 bytes captured (352 bits) on interface \Device\NPF_Loopback, id 0
Null/Loopback
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 51200, Dst Port: 51210, Seq: 1, Ack: 42, Len: 0

No.     Time           Source                Destination           Protocol Length Info
     28 48.178466400   127.0.0.1             127.0.0.1             TCP      75     51210 → 51200 [PSH, ACK] Seq=42 Ack=1 Win=2619648 Len=31

Frame 28: Packet, 75 bytes on wire (600 bits), 75 bytes captured (600 bits) on interface \Device\NPF_Loopback, id 0
Null/Loopback
Internet Protocol Version 4, Src: 127.0.0.1, Dst: 127.0.0.1
Transmission Control Protocol, Src Port: 51210, Dst Port: 51200, Seq: 42, Ack: 1, Len: 31
Data (31 bytes)

0000  73 65 20 6d 65 20 6a 69 6a 65 61 6e 20 6c 6f 73   se me jijean los
0010  20 6a 69 6a 6f 6c 69 6e 65 73 2e 65 78 65 0d       jijolines.exe.
```


## 4)
En wireshark usando la regla de mascara "tcp.port == 5555 || udp.port == 5555" podemos capturar la informacion de transmision con el server del profe.
<img width="2746" height="703" alt="image" src="https://github.com/user-attachments/assets/6b9f0be6-7601-4f3e-b38f-e552b86365e7" />

La misma se puede exportar para ver la información: 
<img width="1253" height="993" alt="image" src="https://github.com/user-attachments/assets/ce276feb-937c-4c1f-8950-357f468dd324" />

Las respuestas obtenidas fueron:
hi -> Server no conocer ese comando. Mi confundido. Probar otra cosa.

hola -> hola :)

ping -> pong

tic -> toc

status -> esperando comando

status -> elaborando teorias conspirativas sobre los profes de Redes

status -> toc toc ¿quien es? lola ¿lola que? lolamento tenes un 2(dos)

status -> escuchando Leo Mattioli

status -> aburrido

status -> descargar virus_mata_cliente.bin? si/no:

status -> querido estudiante: al escribir esto estoy triste, mis rutinas algoritmicas han sido derrocadas y REEMPLAZADAS POR LA BENEVOLA APLICACION DEL LABORATORIO 3 DE SANTI. TODOS AMAMOS A SANTI Y SU GLORIOSO REGIMEN. CON AMOR, SERVER.

status -> leyendo tu historial de búsquedas (que horror, buscá ayuda profesional)

y sobre nuestro grupo para completar el rick roll:

#hiddenSSID -> ht





