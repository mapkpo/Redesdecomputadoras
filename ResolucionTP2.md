1A) El fenómeno físico representado en la figura es el efecto Doppler, el cual es el cambio de la frecuencia de una onda cuando la fuente que lo emite y el receptor
se mueven el uno respecto al otro. Si la fuente y el receptor se acercan, la frecuencia percibida aumenta. Si se alejan, la frecuencia percibida disminuye.

1B) Las bandas de transmisión vistas en el primer practico son las 15 bandas clasificadas por ITU, de estas, las mas afectadas por el efecto Doppler son las bandas
altas, porque trabajan con frecuencias de portadoras muy grandes y por el contrario las mas resilientes a este efecto son las bandas mas bajas, en estas, este efecto
apenas aparece.

1C) No deberíamos utilizar nuestro teléfono celular sobre un avión ya que sobrecarga la red celular en tierra, dada la velocidad del avión, este intenta conectarse y
desconectarse constantemente a multiples torres o celdas en tierra. Esto también agota la batería del dispositivo mas rápidamente. 
Otra consecuencia es el hecho de poder interferir con los sistemas de radiofrecuencia del avión.

El efecto Doppler se encuentra indirectamente relacionado, ya que el constante intento del celular por conectarse a una red en tierra es debido a la gran velocidad del
avión y el efecto se produce entre el la señal del celular y la torre al alejarse uno de otro. Por esto, lo que siempre se recomienda es activar el modo avión del celular.



2A) El fenómeno físico representado en la figura es el ruido, mas concretamente el ruido impulsivo. El ruido impulsivo es no continuo y está constituido por pulsos 
o picos irregulares de corta duración y de amplitud relativamente grande. Se generan por una gran diversidad de causas, por ejemplo, por perturbaciones
electromagnéticas exteriores producidas por tormentas atmosféricas o por fallos y defectos en los sistemas de comunicación. Este tipo de ruido es bastante perjudicial
para los datos digitales, mientras que las analógicas son las que menos sufren su efecto. En la figura vemos representado el ruido impulsivo siendo generado por un operario 
utilizando un martillo neumático.

2B) Tomando en cuenta las 15 bandas clasificadas por el ITU, las bandas mas afectadas por el fenómeno del ruido son las bandas terrestres bajas y medias, 
usadas en enlaces cercanos al suelo, líneas de cobre o zonas industriales/urbanas, donde conviven con maquinaria, motores, etc. Y sistemas de banda angosta,
ya que el pulso que es de banda ancha ocupa  más energía dentro del canal.

En cambio los mas resilientes son los enlaces en bandas altas dedicados y apantallados, que al ser enlaces punto a punto muy directivos y alejados de fuentes de ruido
mecánico, están menos expuestos a este tipo de interferencia puntual. También los sistemas de banda ancha, porque el pulso impulsivo afecta solo una fracción pequeña del
ancho de banda total utilizado, diluyendo su impacto.

2C) La SNR (Signal-to-Noise Ratio) es el cociente entre la potencia de la señal y la potencia del ruido presente en un punto del sistema, normalmente medida en el receptor.
Una SNR alta significa que la señal predomina claramente sobre el ruido, obteniendo una mejor calidad; una SNR baja indica que el ruido es comparativamente fuerte y puede 
llegar a tapar o distorsionar la información.

El BER (Bit Error Rate) es la medida que indica la proporción de bits erróneos recibidos en comparación con el número total de bits transmitidos en un canal digital. 
Sirve para evaluar la calidad y la fiabilidad de un sistema de telecomunicaciones. 

La SNR y el BER están inversamente relacionados, Cuanto menor es la SNR, mayor es la probabilidad de que el ruido altere un bit (convierta un 1 en 0 o viceversa), 
por lo tanto mayor es el BER. Cuanto mayor es la SNR, el receptor puede distinguir mejor los niveles de señal del ruido de fondo, y el BER disminuye.


3)

4A) Sincronización significa que el receptor sepa cuándo y cómo interpretar los datos que recibe. Ambos deben tener una referencia en común.
Sincronización de bits es cuando usamos un ciclo de reloj coordinado para saber cuando leer la información, esto puede ser una señal paralela o un reloj interno 
el cual a sido prefijado. 
En cambio en la sincronización de trama, se usa un patrón único para delimitar donde empiezan y donde terminan los datos dentro de una secuencia continua.

4B) Un frame podemos decir es un pedazo de información, al cual se le agrega metadata para que sea posible su transmisión de manera segura y sin errores.
El header es la parte primera, la cual contiene la información necesaria para interpretar la trama en sí, dirección/destino, longitud, tipo, etc.
El payload es la información en si que se desea transmitir, la cual ha sido encapsula en la trama.
El trailer es la parte ultima del frame, el cual además de decir que la trama termina puede tener información para detección de errores.
[ HEADER ][      PAYLOAD       ][ TRAILER ]

4C)


5) Nuestro grupo #hiddenSSID, los primeros 5 caracteres serian #hidd lo cual en binario lo encontramos como "23 68 69 64 64". El numero de secuencia seria "01" osea la primera posición,
el length "02" osea 2 bytes de payload que viene luego los cuales eran "68 74" traducidos como "ht". Resultando ser el inicio de la url del youtube short del premio.
   
