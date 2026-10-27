# ⏱️ Proyecto 5: Temporizadores y Contadores Binarios

Este proyecto consiste en el diseño e implementación de un sistema digital secuencial capaz de generar una señal periódica de reloj, contar pulsos de forma ascendente en código binario de 4 bits y visualizar la cuenta numérica decimal (0 a 9) en un display de 7 segmentos con reinicio automático.

---

### 🛠️ Componentes Utilizados

* **Temporizador Analógico (NE555):** Configurado en modo multivibrador astable para generar el tren de pulsos (señal de reloj) que sincroniza todo el circuito. Su frecuencia de oscilación se ajusta mediante un potenciómetro de 10kΩ y capacitores.
* **Contador Binario Síncrono (SN74LS193 / 74HC93):** Recibe los flancos de reloj y realiza el conteo secuencial de 4 bits (QA, QB, QC, QD). Incorpora retroalimentación en su pin de reinicio/clear (CLR) para truncar la cuenta al llegar a 10.
* **Decodificador BCD a 7 Segmentos (SN74LS48 / CD4511):** Transforma la salida binaria BCD del contador en las señales de activación adecuadas para encender los LEDs del display.
* **Display de 7 Segmentos (Cátodo Común):** Dispositivo optoelectrónico donde se visualizan los dígitos numéricos del 0 al 9.
* **Regulador de Voltaje (LM7805):** Reduce y estabiliza la tensión de entrada de una batería de 9V a +5V DC constantes para alimentar de forma segura los buses lógicos.
* **Componentes Pasivos y de Soporte:** Resistencias de limitación (330Ω), potenciómetro de 10kΩ, capacitores de 1μF y 100μF, LED indicador, batería de 9V y protoboard.

---

### ⚙️ ¿Cómo funciona?

1. **Generación del Reloj (Oscilación Astable):** El circuito integrado **NE555** produce una onda cuadrada continua. La velocidad o frecuencia de parpadeo/conteo se controla manualmente variando la resistencia del potenciómetro en la red RC.
2. **Conteo Síncrono de 4 Bits:** Cada pulso emitido por el temporizador entra por el pin de reloj del contador **74LS193**, incrementando la combinación binaria desde 0000_2 (0 decimal) hacia adelante.
3. **Corte y Reinicio de Cuenta (Reset en 10):** Para mantener la cuenta en base decimal (0-9), las salidas QD (peso 8) y QB (peso 2) se conectan lógicamente para generar la condición CLR = QDQB. Al alcanzarse el valor binario 1010_2 (10 decimal), el contador se reinicia de inmediato a cero.
4. **Decodificación y Visualización:** El decodificador (**74LS48 / CD4511**) interpreta el código BCD de 4 bits y polariza los segmentos individuales ($a, b, c, d, e, f, g$) del display de cátodo común a través de resistencias protectoras.

---
---

# 🔄 Proyecto 6: Registros de Corrimiento (Display Desplazable)

Este proyecto consiste en el diseño e implementación de un sistema digital secuencial que despliega dinámicamente un mensaje de texto en movimiento ("LA OLA") a lo largo de un arreglo de cuatro displays de 7 segmentos, haciendo uso de registros de desplazamiento sincronizados, memoria no volátil y generación de estados.

---

### 🛠️ Componentes Utilizados

* **Registros de Corrimiento (Cuatro SN74LS199):** Circuitos secuenciales de 8 bits constituidos internamente por flip-flops tipo D interconectados. Se encargan de transferir y desplazar la información de los caracteres de un display al siguiente al ritmo del reloj.
* **Memoria EPROM ($8\times 8$ registros):** Almacena previamente en celdas de memoria la codificación de mapa de bits de cada carácter del mensaje (letras y espacios vacíos).
* **Contador Binario (SN74LS193):** Genera la secuencia cíclica de direcciones de lectura para barrer las posiciones de la memoria EPROM.
* **Temporizador (NE555):** Genera el tren de pulsos de reloj global para marcar la velocidad del desplazamiento del texto.
* **Displays de 7 Segmentos (4 Unidades - Cátodo Común):** Arreglo de visualizadores donde se proyecta la animación del texto corriendo de derecha a izquierda.
* **Alimentación y Protección:** Regulador de voltaje **7805** (+5V regulados), batería de 9V, potenciómetro para control de velocidad, resistencias de limitación (330Ω) y cable de conexiones calibre 22/24.

---

### ⚙️ ¿Cómo funciona?

1. **Generación de la Base de Tiempo:** El **NE555** genera los pulsos de reloj que marcan la cadencia y suavidad con la que se moverán las letras a través de la pantalla.
2. **Direccionamiento de Memoria:** El contador **74LS193** incrementa periódicamente su estado, funcionando como apuntador secuencial de direcciones sobre la memoria **EPROM**.
3. **Lectura de Caracteres:** En cada dirección seleccionada, la memoria entrega el patrón binario de 8 bits correspondiente a cada letra del texto ("L", "A", espacio, "O", "L", "A").
4. **Carga y Desplazamiento en Cascada:** Los datos salen en paralelo de la memoria y se ingresan a los registros de corrimiento **74LS199**. Con cada flanco de subida del reloj, los datos se desplazan un paso a lo largo de los cuatro registros enlazados.
5. **Despliegue Visual Dinámico:** Las salidas de los registros alimentan los segmentos de los **4 displays** en paralelo a través de sus resistencias de $330\ \Omega$, logrando el efecto visual del mensaje en movimiento fluido.
