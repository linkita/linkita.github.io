---
id: 548
title: Reloj binario con Arduíno.
date: 2012-01-12T11:17:14+00:00
author: Linkita
layout: post
guid: http://linkita.net/?p=548
permalink: /2012/01/reloj-binario-con-arduino/
categories:
  - Bellas Artes
  - Diseño
---
[<img src="http://farm8.staticflickr.com/7019/6662225621_0696812ffb_z.jpg" alt="Binary clock" width="640" height="450" />](http://www.flickr.com/photos/linkita/6662225621/ "Binary clock by Linkita, on Flickr")

Pues hace poco, me propusieron hacer una maqueta para una escultura. Y a mí se me ocurrió hacer un reloj binario. Se me quedó bastante chulo, así que he decidido hacer un mini tutorial por si quereis tener uno en casa je, je.

Lo iré completando si veo que hay cosas que no han quedado muy claras. Para cualquier pregunta, crítica o similar, a los comentarios =)

> **El esquema de este reloj.**

Primera fila, **horas**. Cuatro leds.

Segunda fila, **minutos**. Seis leds.

Tercera fila, **segundos**. Seis leds. (Yo puse la última fila porque quedaba mucho más visual, pero se puede obviar fácilmente)

[<img src="http://farm8.staticflickr.com/7168/6666564073_2d6fb87cb2_z.jpg" alt="Binary clock" width="640" height="425" />](http://www.flickr.com/photos/linkita/6666564073/ "Binary clock by Linkita, on Flickr")

> **Materiales.**

Arduino.

16 leds + resistencias.

2 botones+ resistencias.

cable.

Protoboard.

Pilas.

> **El esquema del circuito.**

[<img src="http://farm8.staticflickr.com/7031/6667126133_db4d5736a9.jpg" alt="Binary Clock" width="500" height="340" />](http://www.flickr.com/photos/linkita/6667126133/ "Binary Clock by Linkita, on Flickr")

Cada extremo de la resistencia se coloca en un pin del arduíno. **R1 a pin1, R2 a pin2, R3 a pin3&#8230;.** etc etc. En mi caso, no tenía problema de salidas digitales, porque usé un MEGA, pero si usas un UNO o similar, en el que sólo tienen 13 salidas digitales, puedes usar las salidas analógicas como salidas digitales.

Y los botones, se usan de la siguiente manera ([más información en la página de Arduino](http://arduino.cc/es/Tutorial/Button "Cómo usar el botón")):

[<img class="alignnone size-full wp-image-550" title="Button Arduino" src="http://linkita.net/wp-content/uploads/2012/01/button.png" alt="Button Arduino" width="729" height="283" />](http://arduino.cc/es/Tutorial/Button)

Si necesitais más información, os dejo los links de un par de relojes binarios hechos con arduíno, con los cuales he resuelto el proyecto rápidamente. Quizás os lo expliquen mucho mejor que yo =P

[DIY: Binary Clock with Arduino por Daniel Andrade [Inglés]](http://www.danielandrade.net/2008/07/15/binary-clock-with-arduino/ "Binary Clock with Arduino, por Daniel Andrade")

[Arduino + LEDs = Binary clock por Instructables [Inglés]](http://www.instructables.com/id/Arduino-LEDs-Binary-clock/ "Arduino + Leds = Binary Clock")

&nbsp;

> **¡Vídeo!**



&nbsp;

> **Galería.**

Os enlazo una [pequeña galería de fotos en flickr](http://www.flickr.com/photos/linkita/sets/72157628793762895/with/6666564073/ "Galería de fotos Flickr") por si queréis echarle un vistazo.

&nbsp;

> **Construcción.**

En cuanto al reloj en sí, la cosa está en pinchar en la protoboard en el orden adecuado según el esquema que queramos utilizar. La caja de la foto está construída en cartón pluma, porque el proyecto era una maqueta. Personalmente, yo usaría otro material. Madera o similar. La parte superior es metracrilato (del que se raya con mirarlo).

Cuidado también con la tierra, porque yo le quité la placa metálica a la protoboard, porque no me cabía en la caja, y ahora tengo ciertos problemas cuando lleva un rato funcionando. Creo que se acumula algún tipo de electricidad estática o algo así.

> **Código.**

Y por último, lo más importante, el código.

Yo he usado la libreria time.h&#8230; sin un RTC (Real Time Clock) por lo cual, hay errores de cálculo y al no poder sincronizarse, el reloj sufre un pequeño retraso cada día.

Básicamente, al arrancar, hace un test de todos los leds para ver si alguno se me ha fundido, y ya empieza a contar la hora a partir de las 12:00h.

Los pines los he puesto de manera que me fuera más cómodo colocar el Arduino en la protoboard pero básicamente es  indiferente, siempre y cuando los enchufeis bien al led que corresponde.

Y los programadores que lean el código&#8230; por favor, que no sean muy críticos u////u

¡Que disfruteis!

`#include <time.h>` 

`int hourLEDs [] = { 23, 25, 27, 29}; // bit menos significativo primero.`

`int minuteLEDs [] = { 31, 33, 35, 37, 38, 41};`

`int secondLEDs [] = { 43, 45, 47, 49, 51, 53};`

`int loopLEDs[] = {23, 25, 27, 29, 31, 33, 35, 37, 38, 41, 43, 45, 47, 49, 51, 53};`

`int switchPin = 17;`

`const int buttonHour = 52; // pin del pulsador de las horas`

`const int buttonMinute = 50; // pin del pulsador de los segundos`

`int buttonStateHour, lastbuttonStateHour = 0; // estado del pulsador de horas.`

`int buttonStateMinute, lastbuttonStateMinute = 0; // estado del pulsador de minutos.`

`time_t t;`

`void setup(){`

`   for (int i = 0; i< 4; i++){`

`        pinMode(hourLEDs[i], OUTPUT);`

`   }`

`   for (int i = 0; i< 6; i++){`

`        pinMode(minuteLEDs[i], OUTPUT);`

 `}`

`   for (int i = 0; i<6; i++) {`

`        pinMode(secondLEDs[i], OUTPUT);`

`   }`

`   t = now();`

`   Serial.begin(9600); //comunicacion serie.`

`   pinMode(13, OUTPUT); //pin 13 para comprobacion de pulsadores.`

`   digitalWrite(13, HIGH);`

`   pinMode(buttonHour, INPUT);`

`   pinMode(buttonMinute, INPUT);`

`   setTime(0);`

`   spin(2); //check de todos los leds.`

`   delay(1);`

`}`

`void loop(){`

`   //comprobamos pulsadores.`

`   buttonStateHour = digitalRead(buttonHour);`

`   buttonStateMinute = digitalRead(buttonMinute);`

`   if (digitalRead(switchPin)){`

`       adjustTime(1);`

`   }`

`   else if (minute() == 0 && second() == 0){`

`     //spin(hour());`

`   }`

`   updateDisplay();`

`   delay(1);`

`   if (buttonStateHour != lastbuttonStateHour){`

`   // comprobamos si el pulsador de las horas esta pulsado.`

`   // si es asi, estara HIGH:`

`       if (buttonStateHour == HIGH) {`

`       // incrementamos una hora. Reseteamos segundos.`

`           setTime(hour(t)+1, minute(),0,01,01,2011);`

`           Serial.print("test - incrementamos hora: ");`

`           Serial.print(hour(t));`

`           digitalWrite(13, HIGH);`

`       }`

`       else {`

`           digitalWrite(13, LOW);`

`           Serial.println("\ntest - horas off.");`

`       }`

`   }`

`   lastbuttonStateHour = buttonStateHour;`

`   if (buttonStateMinute != lastbuttonStateMinute){`

`   // comprobamos si el pulsador de los minutos esta pulsado.`

`   // si es asi, estara HIGH`

`       if (buttonStateMinute == HIGH) {`

`           // inc`

`           setTime(hour(t), minute()+1,0,01,01,2011);`

`           Serial.print("test - incrementamos minutos: ");`

`           Serial.print(minute(t));`

`           digitalWrite(13, HIGH);`

`       }`

`       else {`

`           digitalWrite(13, LOW);`

`           Serial.println("\ntest - minutos off.");`

`       }`

`   }`

`   lastbuttonStateMinute = buttonStateMinute;`

`}`

`void updateDisplay(){`

`   t = now();`

`   setOutput(hourLEDs, 4, hourFormat12(t));`

`   setOutput(minuteLEDs,6, minute(t));`

`   setOutput(secondLEDs,6, second(t));`

`}`

`void setOutput(int *ledArray, int numLEDs, int value){`

`   for (int i= 0; i < numLEDs; i++){`

`       digitalWrite(ledArray[i], bitRead(value, i));`

`   }`

`}`

`void spin(int count){`

`   for (int i = 0; i < count; i++){`

`       for (int j = 0; j {`

`           digitalWrite(loopLEDs[j], HIGH);`

`           delay(100);`

`           digitalWrite(loopLEDs[j],LOW);`

`       }`

`   }`

`}`

Se me olvidaba, tengo que agradecer a **Franki, David y Julio** por echarme una mano con esto cuando lo he necesitado =)