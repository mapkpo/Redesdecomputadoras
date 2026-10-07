# 1)

## ICMP y su primer contacto con Wireshark

A)  ICMP es un protocolo que se utiliza dentro de la red para diagnosticar problemas con la transmisión de datos.
A diferencia de TCP o UDP, este no transporta informacion generada por aplicaciones de usuario, toda su carga util es unicamente informacion de diagnostico

B)  ICMP viaja dentro de IP, son encapsulados directamente en el payload de un paquete IP.
Se identifica segun el encabezado, en IPv4 existe un campo Protocol que si su valor es "1", la carga util es ICMP.

C)  Ping comprueba si la IP destino esta activa y es alcanzable, mide el tiempo de ida y vuelta (RTT) y el porcentaje de paquetes perdidos.
Echo Request es una solicitud del emisor pidiendole al destino que responda con los mismos datos.
Echo Reply es la respuesta  del destino, confirmando la solicitud.
Se diferencian por el campo Type, en Echo Request el campo Type es 8, mientras que en Echo Reply el campo Type es 0.

D)  El encabezado mínimo mide 8 bytes, compuesto de:

1.Type (1 byte), que es el tipo de mensaje

2.Code (1 byte), que es un 
subcodigo

3.Checksum (2 bytes), para verificar que el mensaje no se corrompió

4.Identifier (2 bytes), Identificador para asociar la solicitud

5.Sequence Number (2 bytes), Numero secuencial para emparejar cada Echo con su Reply

Después de eso, sigue el Payload donde se emite información adicional.

Configuración de red del equipo
- **Interfaz:** wlp0s20f3
- **Dirección IPv4:** 192.168.1.22
- **Máscara:** 255.255.255.0 (/24)
- **Gateway por defecto:** 192.168.1.1
- **Dirección MAC de la interfaz:** a0:85:27:5b:f4:c8

---


| Capa (como la nombra Wireshark) | Dirección/identificador origen | Dirección/identificador destino | ¿Qué campo indica qué protocolo viene "adentro"? |
| :--- | :--- | :--- | :--- |
| **Ethernet II** |a0:85:27:5b:f4:c8|98:42:65:72:f7:77 |IPv4 |
| **Internet Protocol Version 4** |192.168.1.22 |8.8.8.8 |ICMP |
| **Internet Control Message Protocol** |0x82db |0x82db|Type: 8 |
| **Datos / payload** |Data (40 bytes)|Data(40 bytes) | -|


A2)  <img width="1016" height="282" alt="A2" src="https://github.com/user-attachments/assets/4f8bbf5f-a879-4abe-8184-e598066400bd" />

La MAC es del router,la misma que se uso para el ping.
El alcance de la MAC es localmente, mientras que la IP tiene un alcance global

B2)  <img width="1105" height="312" alt="B2" src="https://github.com/user-attachments/assets/2e65f51b-6a2b-4f2f-9136-ceac1271b437" />


Campos que cambian:
MAC origen y MAC destino (se invierten),
IP origen e IP destino (se invierten),
TTL (Time to Live),
IP Identification,
Checksum de IP,
ICMP Type (pasa de 8 a 0),
Checksum de ICMP


Campos que NO cambian:
Ethernet Type (0x0800),
Versión de IP (IPv4),
IP Protocol (1 = ICMP),
Tamaño total del paquete,
ICMP Identifier,
ICMP Sequence Number,
ICMP Data (Payload)

Para el ping, las direcciones se tienen que invertir, el Type cambia para que sea una respuesta.

El identifier y Sequence Number se mantienen para emparejar cada respuesta con su solicitud y medir su tiempo de respuesta.


C2)  <img width="1043" height="501" alt="C2" src="https://github.com/user-attachments/assets/6dfc3f0b-7e4c-4d92-9d47-a15a914b7f57" />

Linux payload, PONER CAP PAYLOAD EN WINDOWS

D2)  <img width="1465" height="159" alt="D2" src="https://github.com/user-attachments/assets/7f007c5d-7bfd-413e-8439-d4cfc103ef5b" />

El TTL (Time to Live) mide cantidad de saltos en routers, Linux usa un TTL inicial de 64.
La salida desde Google es de 128 y el TTL que llego fue de 117, asi que paso a través de 11 routers 

E2)  <img width="1403" height="992" alt="E12" src="https://github.com/user-attachments/assets/072ab54b-635d-4463-87ef-e13a298d81b1" />
<img width="827" height="896" alt="E2" src="https://github.com/user-attachments/assets/7df6f5ff-0f33-4a36-a77d-a06f40ed09ad" />


-------------------------------------------------------------------------------------------------------------------------------------------------------------------
2) ARP: de una IP a una dirección MAC

a) Resuelve la correspondencia entre direcciones IP y direcciones MAC dentro de una red local. Sin ARP un equipo que conoce la IP de destino no podría construir la trama.

Suele ubicarse en la capa 2 o en una capa intermedia entre la 2 y la 3. Es discutible porque usa direcciones de capa 3 para obtener direcciones de capa 2, y porque viaja directamente sobre Ethernet sin encapsularse en IP, pero existe solo para dar soporte a IP.

b) ARP Request es la pregunta por quien tiene la IP "X" y le deben responder a su direccion MAC. Esta se envía por broadcast, así que lo reciben todos los equipos de la red local.

ARP Reply en cambio, es la respuesta. Se envía por unicast directamente al equipo que hizo la consulta, y solo lo responde el dueño de esa IP.

c) Es una tabla en cada equipo que guarda las asociaciones IP a MAC aprendidas recientemente. Esta existe para evitar hacer un broadcast antes de cada paquete, sin ella, cada envio generaría una consulta, con su tráfico y retardo correspondiente. Las entradas caducan tras un tiempo porque la red cambia, un equipo puede cambiar de IP, de tarjeta o apagarse, y una entrada vieja enviaria tramas a un destino equivocado.

d) Primero tengo que revisar mi cache ARP para ver si ya conozco la MAC de esa IP. Si esta, la uso directamente, si no, mando un ARP Request por broadcast a toda la red preguntando por quien tiene esa IP. La maquina que tiene esa IP me responde diciendome su MAC. Guardo ese dato en la cache y ahora armo la trama Ethernet con esa MAC como destino.





-------------------------------------------------------------------------------------------------------------------------------------------------------------------

3) TCP y UDP "a mano" con ncat

a) Establecer una conexión TCP significa que los dos extremos acuerdan comunicarse y reservan estado el uno para el otro antes de intercambiar datos.
Existe unicamente en los extremos, es decir, en la memoria del sistema operativo de las dos máquinas. No existe en los cables que transportan bits, ni en los routers (que reenvían paquetes IP de forma independiente, sin saber que pertenecen a una conexión TCP; solo miran la IP destino). Por eso se dice que la conexión es una abstracción de extremo a extremo.

b) Un puerto es un número de 16 bits que usan TCP y UDP para distinguir entre las distintas aplicaciones que se ejecutan en un mismo equipo. La IP lleva el paquete hasta la máquina correcta, y el puerto indica a qué proceso dentro de esa máquina debe entregarse.

El par (IP, puerto) se llama socket e identifica un extremo de comunicación: una aplicación concreta en una máquina concreta. A su vez, una conexión TCP queda identificada de forma única por la 4-upla (IP origen, puerto origen, IP destino, puerto destino).

c) Significa que el proceso le pidió al sistema operativo, mediante las llamadas bind() y listen(), que reserve ese puerto y quede a la espera de conexiones entrantes. Cuando llega un SYN dirigido a ese puerto, el sistema operativo sabe a qué proceso corresponde, completa el handshake y le entrega la nueva conexión mediante accept().


-------------------------------------------------------------------------------------------------------------------------------------------------------------------

3.1) Experimento TCP.
<img width="1214" height="179" alt="b1" src="https://github.com/user-attachments/assets/a05802da-a797-4476-a445-39c862bfd00f" />
<img width="1105" height="177" alt="a1" src="https://github.com/user-attachments/assets/63d6aa08-d011-4516-bdc4-59ef47ea54d0" />
<img width="1277" height="276" alt="1" src="https://github.com/user-attachments/assets/33b844ef-577f-4411-8b41-90b0df4404fe" />

Experimento UDP.
<img width="2361" height="283" alt="2" src="https://github.com/user-attachments/assets/548d053d-d53b-4d7d-a97d-4bc08d0799a6" />
<img width="1103" height="238" alt="2w" src="https://github.com/user-attachments/assets/eb59ee87-5b39-4d77-bf12-0b0880044184" />

Experimento sin servidor.
<img width="1207" height="380" alt="3" src="https://github.com/user-attachments/assets/d5d1dce2-2972-4730-a95b-154a1d451cb0" />
<img width="1390" height="316" alt="3w" src="https://github.com/user-attachments/assets/717c61de-eaf2-4e2d-b8db-4d5c02a9855e" />







