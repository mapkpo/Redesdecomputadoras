# Preguntas

3.1. ¿En qué se diferencia un medio guiado de un medio no guiado?

3.2. ¿Cuáles son las diferencias entre una señal electromagnética analógica y una digital?

3.3. ¿Cuáles son las tres características más importantes de una señal periódica?

3.4. ¿Cuántos radianes hay en 360o?

3.5. ¿Cuál es la relación entre la longitud de onda y la frecuencia en una onda seno?

3.6. ¿Cuál es la relación entre el espectro de una señal y su ancho de banda?

3.7. ¿Qué es la atenuación?

3.8. Defina la capacidad de un canal.

3.9. ¿Qué factores clave afectan a la capacidad de un canal?

---

3.1 La Principal diferencia es por donde viajan los datos, mientras que el medio guiado utilizan componentes fisicos y tangibles para la transmision, los medios no guiados utilizan el aire para transmitir ondas electromagneticas

3.2 Una señal Analogica es una onda electromagnetica continua, que varia constantemente de valor, mientras que una señal digital se compone de pulsos que toman solo dos valores, 0 y 1.
La señal analoga es mas sensible al ruido y a los errores, mientras que la digital es mas resistente al ruido

3.3 Sus caracteristicas son:

**Periodo** : Cantidad de tiempo transcurrido entre dos repeticiones consecutivas de señal

**Amplitud** : Valor maximo de laseñal en el tiempo

**Frecuencia** : Es el numero de veces que la onda se repite en un segundo

3.4 2π = 360° = 1 Periodo

3.5 La longitud de onda y la frecuencia estan relacionadas por la velocidad de propagacion. Ya que la frequencia se representa en oscilaciones/tiempo y la longitud de onda en distancia/oscilacion. se cumple que la velocidad de propagacion en distancia/tiempo completa la ecuacion para su relacion de la forma: velocidad de propagacion = longitud * frecuencia 

3.6 la relacion entre el espectro de una señal y su ancho de banda se basa en la definicion de ancho de banda. una señal expresada en frecuencia tendra una frecuencia minima y maxima que la representan, el ancho de banda es simplemente la distancia en frecuencia de este minimo y maximo. Teniendo una señal cuyo espectro tiene un componente minimo de 60hz y maximo de 300hz el ancho de banda seria 240hz.

3.7 La atenuacion es el fenomeno de la reduccion en la intensidad de una señal mientras se propaga por el espacio. Es consecuencia de que una señal tiene energia limitada y al propagarse en mas espacio disminuye su intensidad. Aun para señales que se propagan en medios guiados se produce atenuacion por la interaccion de la señal con materia quitandole energia. Por esto cualquier receptor medira con menor intensidad la señal mientras mas se distancie del transmisor.

3.8 La capacidad de un canal es la velocidad de transmision maxima a la que pueden comunicarse el transmisor y receptor por un canal especifico. Esto es claramente una propiedad del canal.

3.9 los factores que la afectan son:
- velocidad de transmision
- ancho de banda
- ruido
- tasa de errores
  
En conjunto los primeros dos factores no pueden incrementarse indefinidamente sin que los factores 3 y 4 reduzcan la tasa de transmision de informacion efectiva y aumente el costo.

---
# Ejercicios

3.1 

A. Trasmite solo uno a la vez, porque comparten el mismo medio fisico de transmision.
Si transmiten al mismo tiempo provocaria una interferencia destructiva, por eso el medio tiene que compartirse temporalmente, solo a la estacion que tenga el turno de emision

>B.

3.2 con una frecuencia fundamental de 1000Hz 1/1000hz = 1ms

3.3
>A. sen(2π F t - π)*2 experiencian interferencia constructiva
>B. difieren en 180° por lo tanto = 0 experimentan interferencia destructiva

3.4  Pensando en frecuencias relativas podemos ver que un salto de 1 octava duplica la frecuencia. Notas mas altas tienen frecuencias mayores mientras que sus longitudes de onda se vuelven menores. Tambien podemos destacar que la longitud de onda del MI es de 1m aproximadamente. Un MI una octava mayor tendra una longitud de onda de 0.5m

3.5 ya que tiene el doble de amplitud y frecuencia. Se puede representar como 2*sen(2π * 2t + π). Tiene un desfasaje de 180° ya que en los alrededores de 0 difieren en signo

3.6 resolvemos con los siguientes pasos:
- cos(100t)+ 0,1 cos(5t)*cos(100t)
- por la expresion de cos(a)*cos(b) -> 0,1 cos(5t) * cos(100t) = 0,05 cos(95t) * 0.05 cos(105t)
- reemplazando obtenemos cos(100t) + 0,05 cos(95t) + 0,05 cos(105t)

3.7. 
- expandiendo obtenemos (10cos(t))*(10cos(t))
- 100 * cos²t, ignoramos la amplitud de 100 ya que no affecta la frecuencia 
- cos(t) tiene un periodo de 2π. cos² se vuelve positivo para la onda positiva y negativa de cos, por lo tanto su frecuencia es el doble y su periodo la mitad, tiene un periodo de π

3.8 La Suma de dos funciones periodicas da como resultado una Funcion con frecuencia fundamental, solo si la frecuencia de la segunda componente es multiplo entero de la frecuencia de la segunda componente.
Si no es asi, no existe relacion tal que la componente resultante no es ninguna frecuencia fundamental comun y se convierte en una señal no periodica

3.9

3.10

3.11 Se lograba cambiar de mayusculas y minusculas mediante un caracter llamado SHIFT que cambiaba el modo de funcionamiento, era remplazado las letras minusculas por sus respectivas letras mayusculas y los digitos por otros caracteres especiales.
El codigo TeleTypesetter (TTS) utilizaba como base el codigo de murray, sumando un bit mas, duplicando las combinaciones binarias directas

Fuente : https://www.smecc.org/teletypes_in_typesetting.htm

3.12 Utilizando la misma relacion 4:3 , calculamos las resoluciones por separado
Resolucion Horizontal :
Calculamos los ciclos por linea
Ciclos = Fmax * Tactivo = 5Mhz * 52,5us = 262,5

Entonces la resolucion horizontal alcanzada por cada ciclo completo : 
2 * 262,5 = 525 lineas

Resolucion Vertical: 
Usando la misma resolucion horizontal 450 y un ancho de banda de 5Mhz, la duracion de una linea es 

Tactivo = (450/2) / 5Mhz = 45us

usando los aproximandamente 11 reservados para el retroceso horizontal

45us + 11,2 = 56,2 us

Entonces, el escaneo dura 1/30 ≈ 33.33, con el tiempo de linea se puede calcular el total de lineas verticales

33.333us / 56,2 ≈ 593 lineas
