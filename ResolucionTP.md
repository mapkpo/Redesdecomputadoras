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
Origen: b4:2e:99:8c:69:ef (Puerto ethernet del PC utilizando wireshark) Destino: b8:66:85:fd:8c:7a (Direccion del gateway/router)

## 2B) 
IP origen: 192.168.0.59 (direccion de la LAN de la PC utilizando wireshak) IP destino: 142.251.150.119 (IP publica del servidor con la pagina web)

## 2C) 
Las direcciones de origen conciden al mismo dispositivo dentro de la red local, ya que tienen una asignacion dhcp relacionandolas. Pero las direcciones de destino no representan el mismo dispositivo, esto se debe a que el ultimo dispositivo accesible en la red local en camino al destino es el router. Por lo tanto la trama ethernet se resuelve ahi. En el camino al destino se generan multiples tramas a menos que el destino sea accessible por Layer 2 estando en la misma subred conectado posiblemente por switches, en cual caso las direcciones ip y mac del destino representaran el mismo dispositivo.

## 2D)
 el ethertype es ipv4 ya que este es el utilizado por defecto en acceder a google.com

# 3 Protocolo de Transporte TCP

## 3A) 
El protocolo tcp resuelve multiples aspectos de la comunicacion:
- Detecta la perdida de paquetes (Ethernet y IP no garantizan que se recibio un paquete)
- Comunica el orden de los paquetes
- Controla la velocidad para no saturar la red o el receptor
- Utiliza multiples "puertos" para representar a que aplicacion entregar el paquete

## 3B)
- Puerto de origen y destino: identifican que aplicaciones participan en la comunicacion
- Numero de secuencia: representa la posicion de los datos dentro del flujo total de la sesion, para ordenarlos en una comunicacion mas larga aunque lleguen desordenados
- Numero de ACKnowledgment: indica el numero de secuencia del proximo paquete, permite detectar paquetes perdidos
- Longitud de cabecera: indica el largo de la cabecera para saber cuando comienzan los datos reales
- CRC: permite detectar si el paquete sufrio corrupcion durante la transmision
- Puntero Urgente: comunica que el contenido del segmento debe saltarse la cola de espera para resolverse antes

## 3C) 

Para explicar los handshakes se utiliza el nombre de iniciador para el dispositivo que manda el primer paquete del handshake y receptor para su contraparte, de la forma
iniciador -> receptor

El 3 way handshake inicia una conexion:
- ->SYN solicita la apertura de una conexion y comunica la numeracion de los bytes que enviara en iniciador
- <-SYN-ACK Confirma que recibio el SYN y abre la conexion en sentido opuesto desde el receptor al iniciador
- ->ACK se confirma la conexion del paso 2(el iniciador confirma la conexion desde el receptor)

Luego de esto ambos quedan como ESTABLISHED y la transmision puede comenzar

El four way handshake cierra la conexion en ambas direcciones:
- ->FIN el iniciador indica que cierra su canal de salida
- <-ACK el receptor acepta que no recibira mas datos pero puede seguir emitiendolos
- <-FIN(receptor) el receptor termino de enviar sus datos pendientes y cierra su propia conexion
- ->ACK(receptor) el iniciador reconoce el cierre

