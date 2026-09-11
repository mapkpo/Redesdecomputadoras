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