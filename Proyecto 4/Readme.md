# 📡 Proyecto 4: Comunicación Inalámbrica por Radiofrecuencia (RF 433 MHz)

Este proyecto consiste en el diseño e implementación de un sistema de transmisión y recepción inalámbrica de datos digitales unidireccional a una frecuencia de 433 MHz. Emplea codificación y decodificación digital por desplazamiento de amplitud (ASK) para enviar el estado de 4 canales de entrada binarios (botones pulsadores) y visualizarlos en tiempo real mediante un arreglo de 4 LEDs receptores.

---

### 🛠️ Componentes Utilizados

* **Módulo Transmisor de RF (FS1000A / 433 MHz):** Emite la onda portadora de alta frecuencia modulada en amplitud (ASK). Cuenta con terminales de alimentación ($V_{CC}$, GND), entrada de datos seriales (DATA) y conexión para antena de cable de 30 cm.
* **Codificador de RF (HT12E):** Circuito integrado CMOS que recibe 4 bits de datos en paralelo (`AD0` - `AD3`) junto con 8 bits de dirección (`A0` - `A7`), los codifica y los serializa a través de su pin `DOUT`. Emplea una resistencia osciladora externa de $1\,\text{M}\Omega$ entre los pines 15 y 16.
* **Módulo Receptor de RF (XY-MK-5V / 433 MHz):** Demodula la señal de radiofrecuencia captada por su respectiva antena de 30 cm, regenerando el tren de pulsos digital serial ASK para entregarlo al circuito decodificador.
* **Decodificador de RF (HT12D):** Circuito integrado encargado de recibir la trama serial demodulada en su pin `DIN`, verificar la concordancia de la dirección establecida y decodificar los 4 bits de datos a sus terminales de salida paralelas (`D8` - `D11` / $L_1$ a $L_4$). Opera con una resistencia osciladora de $47\,\text{k}\Omega$ entre los pines 15 y 16.
* **Etapa de Control y Visualización:** 4 push buttons configurados con lógica activa en bajo (hacia GND con `TE` habilitado) en el emisor, y 4 LEDs con resistencias limitadoras de corriente de $220\,\Omega$ en el receptor para indicar el estado lógico transmitido.
* **Fuentes de Alimentación:** Batería de $9\,\text{V}$ DC para la etapa de transmisión (óptima para el alcance del módulo transmisor) y fuente regulada de $5\,\text{V}$ DC para la etapa del receptor.

---

### ⚙️ ¿Cómo funciona?

1. **Lectura y Codificación Paralelo-Serie (HT12E):** Al presionar cualquiera de los 4 push buttons conectados a los pines `AD0`-`AD3`, las entradas se llevan a nivel bajo ($0$ lógico). La terminal de transmisión habilitada (`TE`) se conecta a tierra para activar el ciclo continuo de codificación, empaquetando la dirección fija y los 4 bits de datos en una trama digital serial por el pin `DOUT` (pin 17).
2. **Modulación y Transmisión ASK (433 MHz):** El tren serial ingresa al pin `DATA` del transmisor `FS1000A`. Mediante la técnica **ASK** (*Amplitude Shift Keying* / modulación por desplazamiento de amplitud en esquema On-Off Keying), el transmisor enciende la portadora de 433 MHz para representar un bit $1$ lógico y la apaga para un bit $0$ lógico, propagando la onda a través de la antena de 30 cm.
3. **Recepción y Demodulación de Señal:** El receptor capta la señal electromagnética, filtra el ruido circundante y reconstruye la señal digital cuadrada original en su pin `DATA`, transfiriéndola directamente al pin de entrada `DIN` (pin 14) del decodificador `HT12D`.
4. **Validación y Decodificación Serie-Paralelo (HT12D):** El decodificador compara 3 veces consecutivas la dirección recibida con la local (`A0` - `A7`). Al existir coincidencia válida (*Valid Transmission*, pin `VT` en alto), actualiza sus pines de salida (`D8`-`D11`) reflejando el valor binario enviado ($L_1 = B_0$, $L_2 = B_1$, $L_3 = B_2$, $L_4 = B_3$), encendiendo o apagando el arreglo de LEDs correspondiente.# 📡 Proyecto 4: Comunicación Inalámbrica por Radiofrecuencia (RF 433 MHz)

Este proyecto consiste en el diseño e implementación de un sistema de transmisión y recepción inalámbrica de datos digitales unidireccional a una frecuencia de 433 MHz. Emplea codificación y decodificación digital por desplazamiento de amplitud (ASK) para enviar el estado de 4 canales de entrada binarios (botones pulsadores) y visualizarlos en tiempo real mediante un arreglo de 4 LEDs receptores.

---

### 🛠️ Componentes Utilizados

* **Módulo Transmisor de RF (FS1000A / 433 MHz):** Emite la onda portadora de alta frecuencia modulada en amplitud (ASK). Cuenta con terminales de alimentación ($V_{CC}$, GND), entrada de datos seriales (DATA) y conexión para antena de cable de 30 cm.
* **Codificador de RF (HT12E):** Circuito integrado CMOS que recibe 4 bits de datos en paralelo (`AD0` - `AD3`) junto con 8 bits de dirección (`A0` - `A7`), los codifica y los serializa a través de su pin `DOUT`. Emplea una resistencia osciladora externa de $1\,\text{M}\Omega$ entre los pines 15 y 16.
* **Módulo Receptor de RF (XY-MK-5V / 433 MHz):** Demodula la señal de radiofrecuencia captada por su respectiva antena de 30 cm, regenerando el tren de pulsos digital serial ASK para entregarlo al circuito decodificador.
* **Decodificador de RF (HT12D):** Circuito integrado encargado de recibir la trama serial demodulada en su pin `DIN`, verificar la concordancia de la dirección establecida y decodificar los 4 bits de datos a sus terminales de salida paralelas (`D8` - `D11` / $L_1$ a $L_4$). Opera con una resistencia osciladora de $47\,\text{k}\Omega$ entre los pines 15 y 16.
* **Etapa de Control y Visualización:** 4 push buttons configurados con lógica activa en bajo (hacia GND con `TE` habilitado) en el emisor, y 4 LEDs con resistencias limitadoras de corriente de $220\,\Omega$ en el receptor para indicar el estado lógico transmitido.
* **Fuentes de Alimentación:** Batería de $9\,\text{V}$ DC para la etapa de transmisión (óptima para el alcance del módulo transmisor) y fuente regulada de $5\,\text{V}$ DC para la etapa del receptor.

---

### ⚙️ ¿Cómo funciona?

1. **Lectura y Codificación Paralelo-Serie (HT12E):** Al presionar cualquiera de los 4 push buttons conectados a los pines `AD0`-`AD3`, las entradas se llevan a nivel bajo ($0$ lógico). La terminal de transmisión habilitada (`TE`) se conecta a tierra para activar el ciclo continuo de codificación, empaquetando la dirección fija y los 4 bits de datos en una trama digital serial por el pin `DOUT` (pin 17).
2. **Modulación y Transmisión ASK (433 MHz):** El tren serial ingresa al pin `DATA` del transmisor `FS1000A`. Mediante la técnica **ASK** (*Amplitude Shift Keying* / modulación por desplazamiento de amplitud en esquema On-Off Keying), el transmisor enciende la portadora de 433 MHz para representar un bit $1$ lógico y la apaga para un bit $0$ lógico, propagando la onda a través de la antena de 30 cm.
3. **Recepción y Demodulación de Señal:** El receptor capta la señal electromagnética, filtra el ruido circundante y reconstruye la señal digital cuadrada original en su pin `DATA`, transfiriéndola directamente al pin de entrada `DIN` (pin 14) del decodificador `HT12D`.
4. **Validación y Decodificación Serie-Paralelo (HT12D):** El decodificador compara 3 veces consecutivas la dirección recibida con la local (`A0` - `A7`). Al existir coincidencia válida (*Valid Transmission*, pin `VT` en alto), actualiza sus pines de salida (`D8`-`D11`) reflejando el valor binario enviado ($L_1 = B_0$, $L_2 = B_1$, $L_3 = B_2$, $L_4 = B_3$), encendiendo o apagando el arreglo de LEDs correspondiente.
