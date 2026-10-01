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
    2.Code (1 byte), que es un subcodigo
    3.Checksum (2 bytes), para verificar que el mensaje no se corrompió
    4.Identifier (2 bytes), Identificador para asociar la solicitud
    5.Sequence Number (2 bytes), Numero secuencial para emparejar cada Echo con su Reply

Despues de eso, sigue el Payload donde se emite informacion adicional.

