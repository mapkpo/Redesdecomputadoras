# Capítulo 3: Transmisión de Datos

---


### Preguntas Teóricas

**3.1.** ¿En qué se diferencia un medio guiado de un medio no guiado?

**3.2.** ¿Cuáles son las diferencias entre una señal electromagnética analógica y una digital?

**3.3.** ¿Cuáles son las tres características más importantes de una señal periódica?

**3.4.** ¿Cuántos radianes hay en 360°?

**3.5.** ¿Cuál es la relación entre la longitud de onda y la frecuencia en una onda seno?

**3.6.** ¿Cuál es la relación entre el espectro de una señal y su ancho de banda?

**3.7.** ¿Qué es la atenuación?

**3.8.** Defina la capacidad de un canal.

**3.9.** ¿Qué factores clave afectan a la capacidad de un canal?

---

### Ejercicios Prácticos

**3.1.**
a) En una configuración multipunto, sólo un dispositivo puede trasmitir cada vez, ¿por qué?  
b) Hay dos posibles aproximaciones que refuerzan la idea de que, en un momento dado, sólo un dispositivo puede transmitir. En un sistema centralizado, una estación es la responsable del control y podrá transmitir o decidir que lo haga cualquier otra. En el método descentralizado, las estaciones cooperan entre sí, estableciéndose una serie de turnos. ¿Qué ventajas y desventajas presentan ambas aproximaciones?

**3.2.**
Una señal tiene una frecuencia fundamental de 1000 Hz. ¿Cuál es su periodo?

**3.3.**
Simplifique las siguientes expresiones:  
a) $\text{sen}(2\pi f t - \pi) + \text{sen}(2\pi f t + \pi)$  
b) $\text{sen}(2\pi f t) + \text{sen}(2\pi f t - \pi)$

**3.4.**
El sonido se puede modelar mediante funciones sinusoidales. Compare la frecuencia relativa y la longitud de onda de las notas musicales. Piense que la velocidad del sonido es igual a 330 m/s y que las frecuencias de una escala musical son:

| Nota | DO | RE | MI | FA | SOL | LA | SI | DO |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| Frecuencia (Hz) | 264 | 297 | 330 | 352 | 396 | 440 | 495 | 528 |

**3.5.**
Si la curva trazada con una línea continua de la Figura 3.17 representa al $\text{sen}(2\pi t)$, ¿qué función corresponde a la línea discontinua? En otras palabras, la línea discontinua se puede expresar como $A\,\text{sen}(2\pi f t + \theta)$; ¿qué son $A$, $f$ y $\theta$?

**3.6.**
Exprese la señal $(1 + 0{,}1 \cos 5t) \cos 100t$ como combinación lineal de funciones sinusoidales; encuentre la amplitud, frecuencia y fase de cada una de las componentes. (Sugerencia: use la expresión del $\cos a \cos b$).

**3.7.**
Encuentre el periodo de la función $f(t) = (10 \cos t)^2$.

**3.8.**
Sean dos funciones periódicas $f_1(t)$ y $f_2(t)$, con periodos $T_1$ y $T_2$ respectivamente. ¿Es periódica la función $f(t) = f_1(t) + f_2(t)$? Si es así, demuéstrelo. Si no, ¿bajo qué condiciones $f(t)$ será periódica?

**3.9.**
La Figura 3.4 muestra el efecto resultante al eliminar las componentes de alta frecuencia de un pulso cuadrado, considerando sólo las componentes de baja frecuencia. ¿Cómo sería la señal resultante en el caso contrario (es decir, quedándose con todos los armónicos de frecuencia alta y eliminando los de bajas frecuencias)?

**3.10.**
La Figura 3.5b muestra la función correspondiente a un pulso rectangular en el dominio de la frecuencia. Este pulso puede corresponder a un 1 digital en un sistema de comunicación. Obsérvese que se necesita un número infinito de frecuencias (con amplitud decreciente cuanto mayor es la frecuencia). ¿Qué implicaciones tiene este hecho en un sistema de transmisión real?

**3.11.**
El IRA es un código de 7 bits que permite la definición de 128 caracteres. En los años setenta, muchos medios de comunicación recibían las noticias a través de un servicio que usaba 6 bits denominado TTS. Este código transmitía caracteres en mayúsculas y minúsculas, así como caracteres especiales y órdenes de control. Generalmente, se utilizan 100 caracteres. ¿Cómo cree que se puede conseguir esto?

**3.12.**
¿Cuál es el incremento posible en la resolución horizontal para una señal de vídeo de ancho de banda 5 MHz? ¿Y para la resolución vertical? Responda ambas cuestiones por separado; es decir, utilice el incremento de ancho de banda para aumentar la resolución horizontal o la vertical, pero no ambas.

**3.13.**
a) Suponga que se transmite una imagen digitalizada de TV de $480 \times 500$ puntos, en la que cada punto puede tomar uno de entre 32 posibles valores de intensidad. Supóngase que se envían 30 imágenes por segundo (esta fuente digital es aproximadamente igual que los estándares adoptados para la difusión de TV). Determine la velocidad de transmisión $R$ de la fuente en bps.  
b) Suponga que la fuente anterior se transmite por un canal de 4,5 MHz de ancho de banda con una relación señal-ruido de 35 dB. Encuentre la capacidad del canal en bps.  
c) ¿Cómo se deberían modificar los parámetros del apartado (a) para permitir la transmisión de la señal de TV en color sin incrementar el valor de $R$?

**3.14.**
Dado un amplificador con una temperatura efectiva de ruido de 10.000 °K y con un ancho de banda de 10 MHz, ¿cuánto será el nivel de ruido térmico a la salida?

**3.15.**
¿Cuál es la capacidad para un canal de un «teletipo» de 300 Hz de ancho de banda con una relación señal-ruido de 3 dB?

**3.16.**
Para operar a 9.600 bps se usa un sistema de señalización digital:  
a) Si cada elemento de señal codifica una palabra de 4 bits, ¿cuál es el ancho de banda mínimo necesario?  
b) ¿Y para palabras de 8 bits?

**3.17.**
¿Cuál es el nivel de ruido térmico para un canal de ancho de banda de 10 kHz y 1000 W de potencia operando a 50 °C?

**3.18.**
Considérense los trabajos de Shannon y Nyquist sobre la capacidad del canal. Cada uno de ellos estableció un límite superior para la razón de bits del canal basándose en dos aproximaciones diferentes. ¿Cómo se pueden relacionar ambas aproximaciones?

**3.19.**
Sea un canal con una capacidad de 20 Mbps. El ancho de banda de dicho canal es 3 MHz. ¿Cuál es la relación señal-ruido admisible para conseguir la mencionada capacidad?

**3.20.**
La onda cuadrada de la Figura 3.7c, con $T = 1\text{ ms}$, se transmite a través de un filtro paso bajo ideal de ganancia unidad con frecuencia de corte a 8 kHz.  
a) Determine la potencia de la señal de salida.  
b) Suponiendo que a la entrada del filtro hay un ruido térmico con $N_0 = 0{,}1\ \mu\text{W/Hz}$, encuentre la relación señal-ruido en dB a la salida.

---

## Respuestas

### Respuestas Teóricas

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

3.7 La atenuación es el fenómeno de la reducción en la intensidad de una señal mientras se propaga por el espacio. Es consecuencia de que una señal tiene energía limitada y al propagarse en mas espacio disminuye su intensidad. Aun para señales que se propagan en medios guiados se produce atenuación por la interacción de la señal con materia quitándole energía. Por esto cualquier receptor medirá con menor intensidad la señal mientras mas se distancie del transmisor.

3.8 La capacidad de un canal es la velocidad de transmisión máxima a la que pueden comunicarse el transmisor y receptor por un canal especifico. Esto es claramente una propiedad del canal.

3.9 los factores que la afectan son:
- velocidad de transmisión
- ancho de banda
- ruido
- tasa de errores
  
En conjunto los primeros dos factores no pueden incrementarse indefinidamente sin que los factores 3 y 4 reduzcan la tasa de transmisión de información efectiva y aumente el costo.

---

### Respuestas Prácticas

3.1 

A. Trasmite solo uno a la vez, porque comparten el mismo medio físico de transmisión.
Si transmiten al mismo tiempo provocaría una interferencia destructiva, por eso el medio tiene que compartirse temporalmente, solo a la estación que tenga el turno de emisión

>B.

3.2 con una frecuencia fundamental de 1000Hz 1/1000hz = 1ms

3.3
>A. sen(2π F t - π)*2 experiencian interferencia constructiva
>B. difieren en 180° por lo tanto = 0 experimentan interferencia destructiva

3.4  Pensando en frecuencias relativas podemos ver que un salto de 1 octava duplica la frecuencia. Notas mas altas tienen frecuencias mayores mientras que sus longitudes de onda se vuelven menores. Tambien podemos destacar que la longitud de onda del MI es de 1m aproximadamente. Un MI una octava mayor tendrá una longitud de onda de 0.5m

3.5 ya que tiene el doble de amplitud y frecuencia. Se puede representar como 2*sen(2π * 2t + π). Tiene un desfase de 180° ya que en los alrededores de 0 difieren en signo

3.6 resolvemos con los siguientes pasos:
- cos(100t)+ 0,1 cos(5t)*cos(100t)
- por la expresion de cos(a)*cos(b) -> 0,1 cos(5t) * cos(100t) = 0,05 cos(95t) * 0.05 cos(105t)
- reemplazando obtenemos cos(100t) + 0,05 cos(95t) + 0,05 cos(105t)

3.7. 
- expandiendo obtenemos (10cos(t))*(10cos(t))
- 100 * cos²t, ignoramos la amplitud de 100 ya que no affecta la frecuencia 
- cos(t) tiene un periodo de 2π. cos² se vuelve positivo para la onda positiva y negativa de cos, por lo tanto su frecuencia es el doble y su periodo la mitad, tiene un periodo de π

3.8 La Suma de dos funciones periodicas da como resultado una Funcion con frecuencia fundamental, solo si la frecuencia de la segunda componente es múltiplo entero de la frecuencia de la segunda componente.
Si no es asi, no existe relacion tal que la componente resultante no es ninguna frecuencia fundamental común y se convierte en una señal no periódica

3.9.
La señal resultante se convertiría en una serie de picos agudos o impulsos periódicos que marcan los instantes exactos de las transiciones de voltaje, perdiendo sus tramos planos al carecer de la energía que aportan las bajas frecuencias, esto podria
interpretarse como una mini curva de descarga de un pequeño capacitor con una carga instantánea.

<img width="683" height="446" alt="imagen" src="https://github.com/user-attachments/assets/dce5752d-5e06-47b0-8081-fb7c8cbdd4f3" />

3.10
Esto tiene varias implicancias, la mayor de ellas siendo que al requerir un ancho de banda infinito cualquier sistema real limitaría estas frecuencias, lo que introduce distorsiones en la señal lo que dificulta su interpretación y agrega errores.   

3.11 Se lograba cambiar de mayusculas y minusculas mediante un caracter llamado SHIFT que cambiaba el modo de funcionamiento, era remplazado las letras minúsculas por sus respectivas letras mayúsculas y los digitos por otros caracteres especiales.
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

3.13  
A) Para determinar la cantidad de bits debemos hacer la siguiente cuenta: bits*pixeles*fps
los bits en este caso serian 5, ya que 2^5=32 colores que necesitamos
osea resolviendo 480*500*5*30 = 36000000 bps == 36 megabits

B)  Para saber el ancho maximo del canal usamos la formula de shanon, con una snr de 35db, resolviendo obtenemos que
c = 4,5 × 10^6 log2​(1 + snr (3162,3))
c = 52,3 megabits

C)  Se pueden reemplazar los 32 niveles de intensidad por 3 colores con 10 niveles de intensidad cada uno, obteniendo 3x10 = 30 posibles estados por píxel.
Como 30 estados todavía pueden codificarse con 5 bits, la velocidad permanece igual

3.14 
N = 10log k + 10log T + 10log b 

K : constante de boltzmann T : Temperarura absoluta en grados kelvin b : Ancho de banda
Reemplazando :
N = -228,4dBW + 10log(10000) + 10log(1000000) = -228,4 + 40 + 70 = -118,6 dBW

3.15  Usando la formula de shanon, buscamos la SNR y obtenemos
c = 475 bps

3.16
Usando la formula de Nyquist (Pag 84)

C = 2B log2 M

Para 4 bits (M = 2⁴ = 16)
9600 = 2 * B * log2(16)
9600 = 2 * B * 4
9600 = 8 * B
B = 9600 / 8 = 1200 Hz (1.2 kHz)

Para 8 bits (M = 2^8 = 256)
9600 = 2 * B * log2(256)
9600 = 2 * B * 8
9600 = 16 * B
B = 9600 / 16 = 600 Hz (0.6 kHz)

3.17
N = 10log k + 10log T + 10log b

Con la temperatura, en kelvin : 50 + 273 = 323 K
Y los 1000w de la señal transmitida, que no afecta al calculo, quedaria como:
N = -228,6 dBW + 10log(323) + 10log(10000) = -228,6 + 25,09 + 40 = -163,51 dBW

3.18 Relacion de Shannon y Nysquit

La aproximacion de Nysquit para un canal sin ruido establece que el límite máximo en la velocidad de transmisión basándose exclusivamente en el ancho de banda disponible B y el numero de senales discretas o niveles de tension es M. Su formulación es C = 2B*log_2 M

Por otro lado la aproximacion de Shannon para un canal con ruido nos dice el límite teórico máximo de transmisión de un canal real considerando la distorsión introducida por el ruido térmico, utilizando la relación señal-ruido (NR). Su formulación es C = B*log_2 (1 + SNR)

Con esto podemos decir que la relacion entre estas aproximaciones es que la fórmula de Shannon se utiliza primero para calcular el límite superior teórico absoluto de la capacidad de un canal dadas sus condiciones de ruido.
Una vez conocido este límite máximo, se utiliza la fórmula de Nyquist para determinar cuántos niveles de señalización diferentes M serían necesarios para alcanzar exactamente esa capacidad teórico, como se vio en el ejemplo 3.3

3.19 Sea un canal con una capacidad (C) de 20 Mbps. El ancho de banda (B) de dicho canal es 3 MHz. ¿Cuál es la relación señal-ruido admisible para conseguir la mencionada capacidad? 
Utilizando la formula de Sharron:

20Mbps = 3 MHz*log_2 (1 + SNR)

20/3 = log_2 (1 + SNR)

2^(20/3) = 1 + SNR

2^(20/3) - 1 = SNR

Resolviendo esto obtenemos una relacion senal ruido (SNR) de 100.59, que explesada en db seria 10*log_10(100.59) = 20.02db

3.20
A) De la señal con frecuencia fundamental de 1Khz y armonicos en 3Khz, 5Khz, 7Khz 9Khz... El filtro deja pasar los armónicos con k impar menores a 8, es decir k = 1, 3, 5, 7 (k = 9 y mayores quedan bloqueados por exceder la frecuencia de corte).
Cada armónico tiene amplitud Ak = (4/π)·(1/k), y su potencia es Pk = Ak²/2 = 8/(π²·k²).
Potencia total de salida:

Po = (8/π²) · (1/1² + 1/3² + 1/5² + 1/7²)
Po ≈ 0,95 W

b) para el SNR de salida, con ruido termico es igual a N0 * ancho de banda(en este caso 8000)
Pnoise= 0,0000001 * 8000 = 0.0008W = 0.8mW
SNR: Po/Pnoise = 0.95w/0.0008W = 1187.5
o en escala logaritmica 30.75dB

# Punto D

caso base del codigo:
```
import numpy as np
import matplotlib.pyplot as plt

A_m = 5
F_m = 4000
A_p = 5
f_p = 40000
ka = 1

fs = 1_000_000
t = np.linspace(0, 0.002, int(fs*0.002))

moduladora = A_m*np.cos(2*np.pi*F_m*t)
portadora = A_p*np.cos(2*np.pi*f_p*t)
modulacion_AM = A_p*(1+ka*np.cos(2*np.pi*F_m*t))*np.cos(2*np.pi*f_p*t)

plt.figure(figsize=(10,8))

plt.subplot(3,1,1)
plt.title("Señal de mensaje o moduladora")
plt.plot(t, moduladora, "g")
plt.ylabel("amplitud")

plt.subplot(3,1,2)
plt.title("Señal portadora")
plt.plot(t, portadora, "r")
plt.ylabel("amplitud")

plt.subplot(3,1,3)
plt.title("Modulación AM")
plt.plot(t, modulacion_AM, "y")
plt.ylabel("amplitud")
plt.xlabel("tiempo (s)")

plt.tight_layout()
plt.show()
```
*Resultado:*

![Image 1](img1.png)

*prueba con frecuencia portadora menor y amplitud portadora mayor:*

![Image 2](img2.png)

*prueba con frecuencia portadora mayor y amplitud moduladora mayor:*

![Image 3](img3.png)
