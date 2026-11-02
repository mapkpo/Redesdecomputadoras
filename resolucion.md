# 1) Averigüen su IP y su máscara (ipconfig / ip addr) y calculen la dirección de broadcast de la red. ¿Cuál es la dirección MAC de broadcast?
Al analizar el archivo de wireshark posteriormente la ip de nuestra pc no esta disponible, pero si podemos ver las siguientes propiedades de la subred analizando los paquetes dhcp:
gateway/servidor dhcp: 192.168.8.1
mascara de subred: 255.255.255.0 o /24

# 3) Analicen la estructura del mensaje. ¿Qué formato tiene? ¿Qué campos contiene y qué creen que representa cada uno? Con lo visto en la sección 1, propongan cómo hay que interpretar los datos.
filtrando a los paquetes cuyo contenido incorpore "SIZE" podemos ver solo los relevantes para la actividad
Paquete 1:
```
5EvU.{"SIZE": "8,7", "PL": "11010001110100111010011100001110011011101001011110101111111100111011111110101111010011101011100010110010101011101100011110111111011010101111111001111010001101111111001011101001110011010111111100010111000111011111001111001011111101010010101110111101000011000010100100011111111001101100101110000111101001110101111001010001010111101111001111010001100001111001011001010100000010000001000000100000", "CHECK": "011111010110111111110110011100101111001100001100110010001"}
```
Paquete 2:
```
5Ei.{"SIZE": "10,6", "PL": "111100011101001110100111000011100110111010010111101011111111001110111111101011110100111010111000101100101010111011000111101111110110101011111110011110100011011111110010111010011101110101111101011110000111101001011010111010001111101011000110001011110001111000110010010111111110011011001011100001111010011101011110010110110101111011110011110100011000011110010110010101000000100000010000001000000100000010000001000000100000", "CHECK": "1000000100101001111100001011110111100110101001011001"}
```
Paquete 3:
```
5E.'{"SIZE": "99,9", "PL": "https://www.youtube.com/watch?v=msX4oAXpvUE", "CHECK": "https://www.youtube.com/shorts/nw7pN6XW9e4"}
```
Paquete 4:
```
5Ez.fwD{"SIZE": "2,23", "PL": "https://www.youtube.com/watch?v=CsGYh8AacgY", "CHECK": "110011001100"}
```

Vemos contenido ascii que sigue formato json con size(alto y ancho de la matriz), payload(datos a transportar) y check(bits de paridad de filas y luego columnas) siguiendo paridad columna-fila
los primeros dos paquetes parecen usar 7 bits por cada casilla de la matriz, representando caracteres ascii
el tercer paquete contiene links en ambos PL y CHECK por lo que no parece seguir el formato de paridad
el cuarto paquete contiene un link valido y un CHECK en binario, que no tiene la cantidad correcta de bits


analizando el pl del paquete 1:
```
        0110111 1111101 1001110 0101111 0011000 0110011 0010001

0       1101000 1110100 1110100 1110000 1110011 0111010 0101111
1       0101111 1111001 1101111 1110101 1110100 1110101 1100010
1       1100101 0101110 1100011 1101111 1101101 0101111 1110011
1       1101000 1101111 1110010 1110100 1110011 0101111 1110001
1       0111000 1110111 1100111 1001011 1111010 1001010 1110111 !Error
1       1010000 1100001 0100100 0111111 1100110 1100101 1100001 !Error
0       1110100 1110101 1110010 1000101 0111101 1110011 1101000 !Error
1       1100001 1110010 1100101 0100000 0100000 0100000 0100000
                  X        X      X
                (col 9) (col 17) (col 23)
```

la unica posibilidad que es un url valido: https://youtube.com/shorts/q8WgKzJwPa4?feature=share

Corrección:
```
        0110111 1111101 1001110 0101111 0011000 0110011 0010001

0       1101000 1110100 1110100 1110000 1110011 0111010 0101111
1       0101111 1111001 1101111 1110101 1110100 1110101 1100010
1       1100101 0101110 1100011 1101111 1101101 0101111 1110011
1       1101000 1101111 1110010 1110100 1110011 0101111 1110001
1       0111000 1010111 1100111 1001011 1111010 1001010 1110111
1       1010000 1100001 0110100 0111111 1100110 1100101 1100001
0       1110100 1110101 1110010 1100101 0111101 1110011 1101000
1       1100001 1110010 1100101 0100000 0100000 0100000 0100000
```


analizando el pl del paquete 2:
```
        1010011 1110000 1011110 1111001 1010100 1011001

1       1111000 1110100 1110100 1110000 1110011 0111010 !Error
0       0101111 0101111 1111001 1101111 1110101 1110100
0       1110101 1100010 1100101 0101110 1100011 1101111
0       1101101 0101111 1110011 1101000 1101111 1110010
0       1110100 1110111 0101111 1010111 1000011 1101001 !Error
0       0110101 1101000 1111101 0110001 1000101 1110001 !Error
0       1110001 1001001 0111111 1100110 1100101 1100001
1       1110100 1110101 1110010 1101101 0111101 1110011 !Error
0       1101000 1100001 1110010 1100101 0100000 0100000
0       0100000 0100000 0100000 0100000 0100000 0100000
        X (col 3)  X (col 12)  X (col 18)  X (col 25)
```
la unica posibilidad que es un url valido: https://youtube.com/shorts/WCi5hu1EqqI?feature=share

Corrección:
```
        1010011 1110000 1011110 1111001 1010100 1011001

1       1101000 1110100 1110100 1110000 1110011 0111010
0       0101111 0101111 1111001 1101111 1110101 1110100
0       1110101 1100010 1100101 0101110 1100011 1101111
0       1101101 0101111 1110011 1101000 1101111 1110010
0       1110100 1110011 0101111 1010111 1000011 1101001
0       0110101 1101000 1110101 0110001 1000101 1110001
0       1110001 1001001 0111111 1100110 1100101 1100001
1       1110100 1110101 1110010 1100101 0111101 1110011
0       1101000 1100001 1110010 1100101 0100000 0100000
0       0100000 0100000 0100000 0100000 0100000 0100000
```
# Reflexiones e investigacion
## ¿Qué hubiera pasado si el mensaje tenía errores en dos bits de filas y columnas distintas? ¿Y si se dañaba un bit de los de control?
Si el mensaje tenia errores en dos filas y dos columnas esto crea 2 posibles pares de correcciones posibles, en los paquetes analizados habian multiples opciones que debieron listarse y probar links para evaluar cual es valido ya que los otros fallarian
Si se daña un bit de control el codigo reemplazaria un bit correcto resultando en informacion invalida pasando como valida, creando problemas de confiabilidad

## Si el mensaje es texto en castellano, muchas veces un error "se adivina" por contexto (Hola mondo). ¿Sirve eso para una contraseña, un número de cuenta o una dirección web? ¿Qué aporta el código frente a "leer y adivinar"?
Para casos donde se requiere que verifique exactamente un valor, como contraseñas, direcciones, id de cuenta, no puede utilizarse un medio en donde pueden alterarse silenciosamente informacion, ya que esto rapidamente causaria problemas por ejemplo:
- un usuario cambia su contraseña(sin saberlo la informacion se corrompio cambiando un caracter) ahora el usuario no podra iniciar sesion nunca mas
- para un numero de cuenta bancaria podria resultar en transferencias invalidas o una transferencia posible a una cuenta no deseada
- para una direccion web resultaria en requests dns para un dominio diferente al deseado o inexistentes.
Para todos estos casos y muchos mas se requiere certeza absoluta de que la informacion sea correcta sin informacion extra de como se ve la informacion correcta, no hay contexto para reparar la comunicacion.

## ¿Pudieron confirmar que su corrección es correcta? ¿Cómo?
Al ser todos links de youtube sabemos corregir errores en el dominio o protocolo y solo quedan las posibilidades en errores del id del video. Con prueba y error podemos saber por la mera improbabilidad de encontrarlos accidentalmente que los mensajes correctos son los que corresponden a videos de la cuenta del profesor

## Investigar y describir con el mayor detalle posible cómo funciona la técnica de corrección Hamming (7,4) y
por qué es superior a la demostración didáctica que hicimos en este Laboratorio. Luego, aplicar la técnica
sobre la carga útil obtenida en el desafío y elaborar un paquete de datos que podrían transmitir para que, en
caso de corrupción, pueda ser recuperado.

El codigo de correccion de hamming (7,4) utiliza 3 bits de verificacion por cada 4 de payload.
cada bit de verificacion es un bit de paridad para 3 de los bits de datos de la siguiente manera:
p1: paridad de d1, d2 y d4
p2: paridad de d1, d3 y d4
p3: paridad de d2, d3 y d4

con un paquete de la forma p1 p2 d1 p3 d2 d3 d4

estos bits de paridad estan superpuestos en su calculo, por lo que podemos detectar si 1 bit de paridad fue alterado y donde utilizando los otros dos bits de paridad.
esto permite corregir errores de un bit en cualquiera de los 7 utilizados por hamming (7,4) o detectar errores de 1 a 2 bit.

por ejemplo:

- si se altera p2 este va a resultar en un error de paridad con d1, d3 y d4. 
- Pero con p1 sabemos que d1 y d4 son validos 
- con p3 sabemos que d3 y d4 son validos.
- ya que p1 y p3 coinciden con d4 estos son menos probables de ser erroneos, hay una combinacion de 3 bits coherente
entonces ya que asumir errores en d1 y d3 resultarian en que mas bits sean erroneos, lo mas probable es que p2 sea el error

esto es una simplificacion de porque se puede corregir un error de un bit, el calculo real se basa en los tres sindromes:
S1 = P1 XOR D1 XOR D2 XOR D4
S2 = P2 XOR D1 XOR D3 XOR D4
S3 = P3 XOR D2 XOR D3 XOR D4

donde con un error en solo uno de los sindromes se refleja en un error en el bit de paridad correspondiente
si dos de los sindromes son 1 el error estaria en el bit de datos en comun entre los dos
si todos son 1 el error estaria en d4, el comun a todos los sindromes

en el caso de dos errores encontraremos una combinacion de sindromes que pueden indicar un error en un bit de datos, esto no seria correcto corregir. Por esto hamming (7,4) puede corregir errores en 1 bit(fallando con 2) O detectar errores de 1 a 2 bits(sin intentar corregir)

implementando el codigo de hamming podriamos resolver el problema de tener que adivinar cual combinacion de correcciones resulta en el mensaje correcto, mientras que dos errores no ocurran en una misma ventana de 7 bits siempre puede solucionarse sin retransmitir
en el caso de que sepamos que un grupo de 7 bits puede tener 2 errores podemos limitarnos a detectar y solicitar una retransmision del paquete.
