1B Considerando que la longitud del periodo son 60mm según el gráfico, usando la formula de longitud de onda c (velocidad de la luz) = lambda * frecuencia, nos da como resultado una frecuencia 5 Ghz.

1C En la clasificación del espectro electromagnetico, nuestra onda de 60mm seria del rango de microondas. 

Según la clasificación de la ITU, dividida en 15 bandas, nuestra onda caería en la banda número 10 (SHF, super high frecuency), según la tabla, la cual contempla frecuencias de rango 3 a 30 GHz, llamada "Ondas centrimetricas".
<img width="1172" height="659" alt="image" src="https://github.com/user-attachments/assets/2e5a1768-c0f9-486f-91f7-06466519a9b3" />

fuentes: 

https://www.itu.int/dms_pubrec/itu-r/rec/v/r-rec-v.431-8-201508-i!!pdf-e.pdf

https://es.wikipedia.org/wiki/Espectro_electromagn%C3%A9tico

1D El uso mas común que podemos encontrar para esta banda es el wifi de 5GHz, el cual permite velocidades mas rápidas que la 2.4Ghz y es necesaria en entornos como edificios y departamentos debido a la alta saturación del espectro de 2.4 y las bajas velocidades de transmisión que ocurren debido a esto. 

1E La linea roja punteada quiere representar el fenómeno presentado en el cap3 del Stallings como atenuación, el cual se define como "decaimiento de la energía en la transmisión debido a la distancia."

1F Si, le afecta. Se nota claramente que al alejarnos del router y tener peor conexión vamos perdiendo velocidad, en este caso como ejemplo podemos poner a reproducir un video en youtube a 4k en el teléfono con calidad automática y ver que al caminar y alejarnos la calidad irá disminuyendo debido a la menor velocidad de internet. 

1G Si, en los 3 casos mencionados se sufre atenuación. El mas evidente es el primero, ya que las señales electromagnéticas se ven atenuadas y bloqueadas por el medio, por ejemplo arboles, paredes, metal, si estamos en un vehiculo o una edificación de puro hierro notaremos como la señal del teléfono disminuye. En el caso del cable la atenuación será debido a la resistencia intrínseca del cable, mientras mayor sea la longitud del mismo mayor será la caída de la señal.
Y en la fibra óptica la atenuación seria no por perdida de luz del cable pero debido a las terminales y en partes donde haya empalmes estos no serán perfectos.









2A Segun el modelo de comunicacion presentado podemos suponer que se trata que tiene caracteristicas temporales congruentes con la comunicacion sincronica y de direccion unidireccional.
Tambien podriamos llegar a pensar que se trata de una comunicacion en serie porque solo tenemos una linea de datos

2B Al pensar el sistema como un sistema de comunicacion unidireccional no seria posible enviar informacion en ambas dirrecciones pero si lo analizamos como si fuese bidireccional ahi la cosa cambia.
Suponiendo esto deberiamos considerar si estamos en una comunicacion halfduplex o fullduplex, teniendo en cuenta que podriamos estar en la primera, no seria lo ideal pues esta no permite la transmicion 
de datos en ambas dirreciones simultaneamente, para esto podriamos considerar como la mejor la fullduplex la cual deberiamos anadir otra linea de datos para que se puedan comunicar de forma simultanea.
Ahora en cuanto a las caracteristicas temporales si consideramos a la comunicacion sincronica como la mejor opcion pues esta a funciona con flancos de clock a diferencia de la asincronica que deberiamos mandar
un bit de inicio y uno de stop.
Tambien si lo que buscamos es mayor velocidad podriamos llegar a considerar una transmicion en paralelo, ya que en la transmision en serie presentada solo podemos mandar un dato a la vez, en cambio en una transmision
en paralelo nos permite enviarlos de forma concurrente a los datos pero tiene limitaciones fisicas en cuanto a la frecuencia que puede alcanzar y un alto coste.
En conclusion la mejor alternativa seria una comunicacion fullduplex, sincronica y serie
