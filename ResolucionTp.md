




# Parte 1 

## 1 Pasos Para Crimpear T568A/B derecho
1) Para crimpear un cable utilizamos la normativa T568B para ambos extremos ya que no es un cable cruzado el que buscamos armar
2) Removemos aproximadamente 5cm de la insulacion exterior
3) Destrenzamos los cables internos y alineamos segun la normativa T568B
4) Cortamos los cables alineados para igualar su largo 2cm fuera de la insulacion
5) Introducimos los conectores en la ficha hasta que lleguen todos al tope
6) Utilizamos la pinza crimpeadora para finalizar el extremo del cable

## 3 Verificacion de cable

<img width="1200" height="1600" alt="WhatsApp Image 2026-10-16 at 10 02 22 AM" src="https://github.com/user-attachments/assets/5fca3b18-c7d8-4058-91c9-683fae777801" />

https://github.com/user-attachments/assets/43baa132-d031-4764-8325-60fe0d4d22ce

El cable resulto tener la insulacion fuera de la ficha, lo cual causa problemas de fiabilidad con tensionar el cable con respecto a la ficha pudiendo causar que uno de los conectores salga y pierda contacto.

Tambien puede causar problemas de fiabilidad a alta velocidad ya que presenta un mayor largo del cable sin trenzar(lo que reduce levemente los beneficios del par trenzado para resistir ruido en modo comun). Por eso este cable no cumpliria las especificaciones cat5e o superiores que especifican un maximo de 13mm sin trenzar por extremo.

Aun asi, los 8 cables presentan continuidad entre las fichas lo que significa que el cable es funcional. Por su largo (Y la calidad de los nic modernos) puede utilizarse con velocidad gigabit entre dispositivos

# Parte 2

## 1 configuracion manual de interfaz de red

Configuramos una notebook con fedora con la siguiente configuracion ipv4:

<img width="1220" height="847" alt="image" src="https://github.com/user-attachments/assets/c2d557f1-0376-47b0-812f-99977ddde451" />

utilizamos la mascara de subred /0 o 0.0.0.0 para que todo paquete se direcione a la ip correspondiente en vez de intentar pasarla a la gateway(ya que no tenemos gateway) esto solo es necesario para garantizar compatibilidad con la ip que elija otro grupo.

La ip para el gateway es arbitraria ya que no existe y no se utiliza, solo se asigna una por requisito de la gui para guardar la configuracion.

Para la actividad solo tiene utilidad asignar una ip para nuestro dispositivo y la mascara de subred que considere la ip del dispositivo de destino como parte de la subred

## 2 verificacion de conectividad por ping:

Despues de resolver problemas con el firewall de windows por la configuracion en defecto como "red publica" que bloquea pings:

<img width="768" height="305" alt="image" src="https://github.com/user-attachments/assets/3912a572-0bdd-42e6-92e6-7bfc0360749a" />


## test ncat
utilizando ncat entre pcs y analizando por wireshark. vemos que ambos utilizan udp para los mensajes y no existe ningun ack entre ellos. si el paquete se perdiera el destinatario nunca vera el mensaje:
´´´
Frame 5: Packet, 53 bytes on wire (424 bits), 53 bytes captured (424 bits) on interface enp0s13f0u3, id 0
Ethernet II, Src: LuxsharePrec_59:64:dc (3c:18:a0:59:64:dc), Dst: GigaByteTech_8c:69:ef (b4:2e:99:8c:69:ef)
Internet Protocol Version 4, Src: 192.168.1.25, Dst: 192.168.1.15
User Datagram Protocol, Src Port: 56552, Dst Port: 5000
Data (11 bytes)
´´´
<img width="1207" height="520" alt="image" src="https://github.com/user-attachments/assets/1edccd77-8537-4796-86c7-18ba8bc87eb7" />
<img width="960" height="76" alt="image" src="https://github.com/user-attachments/assets/79286cca-7fbd-4e6f-b2e1-2f458c2e538f" />


# 5

a) no vemos ningun paquete al iniciar el comando ncat en ambos pcs, y solo vemos un paquete por mensaje

b) no vemos ningun mensaje del destinatario al origen en ninguna direccion, parece no tener ningun ack(aparte de usar udp que no lo provee)

c) si el receptor udp no se ejecuta, un paquete icmp retorna de la ip destino indicando que el puerto esta cerrado indicando a ncat que se denego la coneccion
si el servidor esta abierto pero ningun destinatario se conecta no vemos ningun paquete de salida

d) no, de hecho si en el servidor ncat se ingresan mensajes antes de que el cliente envie el primero estos seran enviados despues figurando fuera de orden. udp no tiene un mecanismo para garantizar el orden y la aplicacion tampoco lo provee

e) aplicaciones como stream de video en vivo, videojuegos, Network Time Protocol. La razon por la que se utilizan es que se prefiere menor latencia para estas aplicaciones, aceptando la posibilidad de paquetes fuera de orden o reenvios. Las aplicaciones pueden utilizar sus propios mecanismos de ack y ordenado mas utiles para su funcionalidad especifica al utilizar udp

# Pequeño servidor

<img width="1851" height="428" alt="image" src="https://github.com/user-attachments/assets/48bf9b59-05b4-47c6-8cc3-56c9202a505d" />

el trafico es de tipo tcp, esto se debe a que si se pierde un tramo de la transferencia el archivo puede volverse inoperable. Se necesita garantizar el orden y presencia de todos los segmentos de los archivos a enviar
