# 1)

## a) clasificacion de redes segun su alcance

- PAN personal area network, red de dispositivos personales a corta distancia. Conecta por ejemplo un celular, auriculares, reloj y notebook.

- LAN Local area network, red generalmente comprende un edificio/casa/oficina y se comunica generalmente por ethernet o wifi.

- CAN Campus area network, conecta multiples edificios cercanos con sus propias lans dentro de una organizacion mayor.

- MAN Metropolitan Area Network, conecta redes ubicadas dentro de una ciudad o geograficamente cercanas.

- WAN Wide Area Network, conecta redes geograficamente alejadas. Por ejemplo el internet

## b) vLAN y como se clasifican

Una vLAN (virtual local area network) permite dividir una red fisica en multiples redes lan "virtuales". Sirven para restringir accesso entre grupos de dispositivos que estan conectados a una misma red a nivel de layer 2 OSI. Por ejemplo pueden separar los dispositivos conectados a un switch en vlans para iot y dispositivos seguros.

Hay dos tipos de vLAN segun su asignacion, Estatica o Dinamica

- vLANS Estaticas asignan un puerto en un switch a una vLAN determinada. Cualquier dispositivo conectado a ese puerto formara parte de esa vLAN

- vLANS Dinamicas asignan dispositivos a vLANS mediante su direccion MAC. Un adaptador de red con una MAC fija formara parte de la misma vLAN sin importar a que puerto se conecto

## c) IEEE 802.1Q

Este es el estandar que permite marcar tramas ethernet segun su pertenencia a una vLAN. 

Ya que tramas ethernet destinadas a diferentes vLANs pueden coexistir en la misma conexion ethernet se necesita una forma de diferenciar las tramas a nivel de layer 2. Por esto este estandar extiende la trama ethernet con tags que determinan a cual de las 4095 vLANs pertenece la trama. 

El Switch administrado podra separar que tramas pueden propagarse por que conexiones utilizando estas tags como filtro.

## d) Tagging

Esto significa agregar a una trama Ethernet sin etiqueta una etiqueta 802.1Q (para destinarla a una vLAN)

Generalmente es necesario que el switch realize esto al recibir una trama de un dispositivo final, ya que la intencion es que las vLANs no sean visibles para dispositivos finales.

Una trama ethernet antes de llegar a un dispositivo final(un puerto o mac que no esta asignado como "Trunk") perdera la tag 802.1Q antes de llegar al dispositivo final

Conversamente una trama partiendo del dispositivo final no tendra una tag 802.1Q ya que el dispositivo desconoce su existencia, por lo tanto el primer switch capaz de asignar vLANs realizara el Tagging

# 2)

Para la comunicacion entre pcs los puertos f0/1 de ambos switches tuvieron que ser configurados como trunk para transmitir las tramas con sus tags para la vLAN 10

Entre Pcs se muestra la conecitividad:

Desde PC-A
```
C:\>ping 192.168.10.4

Pinging 192.168.10.4 with 32 bytes of data:

Reply from 192.168.10.4: bytes=32 time=7ms TTL=128
Reply from 192.168.10.4: bytes=32 time<1ms TTL=128
Reply from 192.168.10.4: bytes=32 time<1ms TTL=128
Reply from 192.168.10.4: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.10.4:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 7ms, Average = 1ms
```

Desde PC-B
```
C:\>ping 192.168.10.3

Pinging 192.168.10.3 with 32 bytes of data:

Reply from 192.168.10.3: bytes=32 time<1ms TTL=128
Reply from 192.168.10.3: bytes=32 time<1ms TTL=128
Reply from 192.168.10.3: bytes=32 time<1ms TTL=128
Reply from 192.168.10.3: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.10.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
Ambas pcs pueden comunicarse entre ellas, pero no pueden acceder a las ip de los switches directamente

```
SW-1#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                Fa0/7, Fa0/8, Fa0/9, Fa0/10
                                                Fa0/11, Fa0/12, Fa0/13, Fa0/14
                                                Fa0/15, Fa0/16, Fa0/17, Fa0/18
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
10   Laboratorio                      active    Fa0/6
20   Bar                              active    
99   Management                       active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    
SW-1#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual down                  down 
FastEthernet0/3        unassigned      YES manual down                  down 
FastEthernet0/4        unassigned      YES manual down                  down 
FastEthernet0/5        unassigned      YES manual down                  down 
FastEthernet0/6        unassigned      YES manual up                    up 
FastEthernet0/7        unassigned      YES manual down                  down 
FastEthernet0/8        unassigned      YES manual down                  down 
FastEthernet0/9        unassigned      YES manual down                  down 
FastEthernet0/10       unassigned      YES manual down                  down 
FastEthernet0/11       unassigned      YES manual down                  down 
FastEthernet0/12       unassigned      YES manual down                  down 
FastEthernet0/13       unassigned      YES manual down                  down 
FastEthernet0/14       unassigned      YES manual down                  down 
FastEthernet0/15       unassigned      YES manual down                  down 
FastEthernet0/16       unassigned      YES manual down                  down 
FastEthernet0/17       unassigned      YES manual down                  down 
FastEthernet0/18       unassigned      YES manual down                  down 
FastEthernet0/19       unassigned      YES manual down                  down 
FastEthernet0/20       unassigned      YES manual down                  down 
FastEthernet0/21       unassigned      YES manual down                  down 
```

```
SW-2#show vlan brief

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
10   Laboratorio                      active    Fa0/18
20   Bar                              active    
99   Management                       active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    
SW-2#show ip interface brief
Interface              IP-Address      OK? Method Status                Protocol 
FastEthernet0/1        unassigned      YES manual up                    up 
FastEthernet0/2        unassigned      YES manual administratively down down 
FastEthernet0/3        unassigned      YES manual administratively down down 
FastEthernet0/4        unassigned      YES manual administratively down down 
FastEthernet0/5        unassigned      YES manual administratively down down 
FastEthernet0/6        unassigned      YES manual administratively down down 
FastEthernet0/7        unassigned      YES manual administratively down down 
FastEthernet0/8        unassigned      YES manual administratively down down 
FastEthernet0/9        unassigned      YES manual administratively down down 
FastEthernet0/10       unassigned      YES manual administratively down down 
FastEthernet0/11       unassigned      YES manual administratively down down 
FastEthernet0/12       unassigned      YES manual administratively down down 
FastEthernet0/13       unassigned      YES manual administratively down down 
FastEthernet0/14       unassigned      YES manual administratively down down 
FastEthernet0/15       unassigned      YES manual administratively down down 
FastEthernet0/16       unassigned      YES manual administratively down down 
FastEthernet0/17       unassigned      YES manual administratively down down 
FastEthernet0/18       unassigned      YES manual up                    up 
FastEthernet0/19       unassigned      YES manual administratively down down 
FastEthernet0/20       unassigned      YES manual administratively down down 
FastEthernet0/21       unassigned      YES manual administratively down down
```

Los puertos a los que se conectan las pcs fueron asignados a la vlan de laboratorio. Por lo tanto solo pueden acceder sin un gateway a los dispositivos en su misma vlan. La vlan de management es separada y por esto las pc no pueden acceder a las ips ahi.