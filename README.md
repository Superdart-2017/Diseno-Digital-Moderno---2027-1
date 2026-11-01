# Diseño-Digital-Moderno-2027-1

Repositorio del equipo para la materia Diseño Digital Moderno (Grupo 5), Facultad de Ingeniería, UNAM. Semestre 2027-1.

# Integrantes
---

- Carpizo Garduño Andrés
- Mata Ramírez Ximena
- Solís Fuentes José Enrique

## Tarea 1 — Sistemas numéricos y sumador binario
--- 

Son dos programas en C en donde el primer código llamado "Conversor_Numerico.c" que convierte números desde base 2 hasta base 16, ya sean enteros, fraccionarios y negativos en complemento a2 de 6 bits) y aparte está el código llamado "Sumador_Binario.c" el cual realiza la suma binaria de dos números de 6 bits, mostrando acarreos y el caso límite de desbordamiento. El reporte en formato PDF y los códigos fuentes se encuentran acá, aparte que hay videos demostrativos de su uso.

Para poder probar cada código se debe de usar su respectivo comando de compilación:

Para "Conversor_Numerico.c": `gcc Conversor_Numerico.c -o Conversor_Numerico.exe -lm`

Para "Sumador_Binario.c": `gcc Sumador_Binario.c -o Sumador_Binario.exe`


## Proyecto 1 y 2
Los siguientes proyectos son dos proyectos diferentes en donde cada se enfoca en un aspecto:

---

### Proyecto 1
--- 

Diseño y construcción de un sistema, únicamente con el uso de compuertas básicas, el cual debe contar con dos entradas, y solo cuando ambas entradas sean iguales se deberá encender una luz.

### Proyecto 2
---

El diseño de circuitos lógicos combinacionales constituye un pilar fundamental en la electrónica digital, permitiendo la toma de decisiones basada en combinaciones específicas de señales de entrada mediante el uso de compuertas lógicas como NOT y AND. En múltiples áreas de la ingeniería y la vida cotidiana, la gestión y ordenamiento de prioridades resultan esenciales para garantizar una respuesta ordenada frente a distintas condiciones. Un ejemplo claro se observa en los sistemas de atención hospitalaria en salas de urgencias, donde es imprescindible clasificar y canalizar eficientemente a los pacientes en función de la gravedad de su estado (súper-emergencia, emergencia o chequeo rutinario). En la presente práctica se aborda el diseño, análisis e implementación de un sistema combinacional de control de prioridad para la entrada a una sala de urgencias. A partir de las especificaciones requeridas, se formula la tabla de verdad y se realiza la simplificación de funciones booleanas mediante mapas de Karnaugh. Posteriormente, se lleva a cabo la implementación del circuito lógico haciendo uso de circuitos integrados discretos (74LS04 y 74LS08), verificando su correcto funcionamiento práctico mediante indicadores LED que representan visualmente la prioridad de acceso otorgada.

---

### Proyecto 3 — Muxes and Decoders (Sistema de supervisión de 9 puntos)
---

Diseño e implementación de un sistema de seguridad y supervisión para un edificio de 9 puntos de acceso utilizando circuitos integrados de mediana escala de integración (MSI). El sistema monitorea en tiempo real las intrusiones mediante un codificador de prioridad decimal a BCD (74LS147), un inversor séxtuple (74LS04) para adecuar los niveles lógicos activos en bajo a lógica positiva, y un decodificador BCD a 7 segmentos (74LS47/74LS48) que despliega de forma inmediata en un display de 7 segmentos el número exacto del punto o sector vulnerado.

---

### Proyecto Parcial 1 — Unidad Lógica Combinacional de 2 bits (ALU Discreta)
---

Diseño, implementación y verificación en protoboard de una unidad combinacional aritmético-lógica de 2 bits construida con circuitos integrados de lógica discreta TTL, prescindiendo del uso de microcontroladores. 

El sistema procesa dos números binarios de 2 bits ($A$ y $B$) y permite seleccionar, mediante dos líneas de control ($S_1, S_0$), una de cuatro operaciones fundamentales:
- **SUM:** Suma binaria con acarreo ($A + B$) mediante el sumador 74LS283.
- **XOR:** Operación bit a bit ($A \oplus B$) con compuertas 74LS86.
- **AND:** Operación bit a bit ($A \cdot B$) con compuertas 74LS08.
- **MAX:** Obtención del valor máximo entre $A$ y $B$ mediante comparación de magnitud y lógica de selección (74LS04, 74LS08 y 74LS32).

El enrutamiento de los resultados se realiza a través de multiplexores dobles de 4 a 1 líneas (74LS153) y se despliega en un display de 7 segmentos mediante el decodificador/driver BCD 74LS47. Adicionalmente, el circuito integra una entrada de habilitación global (**ENABLE**) y un decodificador de 2 a 4 líneas (74LS139) acoplado a un arreglo de 4 LEDs para indicar visualmente la operación seleccionada.

---

### 📡 Proyecto 4 — Comunicación Inalámbrica por Radiofrecuencia (RF 433 MHz)
---

Diseño e implementación de un enlace de transmisión y recepción inalámbrica de datos digitales unidireccional a 433 MHz, integrando módulos de radiofrecuencia con circuitos codificadores y decodificadores dedicados para actuar como entradas a un sistema digital.

El enlace se estructura en dos subsistemas principales:
- **Transmisor (FS1000A + HT12E):** El codificador HT12E toma el estado de 4 entradas paralelas controladas por push buttons (`AD0`–`AD3`) polarizadas con lógica activa en bajo y las empaqueta junto con 8 bits de dirección local (`A0`–`A7`), empleando una resistencia osciladora externa de $1\text{ M}\Omega$. Dicha trama digital se serializa por su pin `DOUT` hacia el transmisor FS1000A (alimentado a $9\text{ V}$), modulando en amplitud por desplazamiento (**ASK** / On-Off Keying) la portadora de 433 MHz enviada a través de una antena de $30\text{ cm}$.
- **Receptor (XY-MK-5V + HT12D):** El módulo receptor captura y demodula la señal de radiofrecuencia a $5\text{ V}$, entregando el tren de pulsos serial al pin `DIN` del decodificador HT12D (oscilador con resistencia de $47\text{ k}\Omega$). Tras validar tres veces la concordancia de dirección, el HT12D activa la bandera de recepción válida (`VT`) y proyecta el estado de los 4 canales decodificados ($L_1 = B_0, L_2 = B_1, L_3 = B_2, L_4 = B_3$) directamente sobre un arreglo de 4 LEDs con resistencias limitadoras de $220\ \Omega$.

---

### ⏱️ Proyecto 5 — Temporizadores y Contadores Binarios
---

Diseño y construcción de un tren de pulsos y un contador binario síncrono modular con visualización decimal en display de 7 segmentos cátodo común.

El sistema comprende tres etapas funcionales:
- **Base de Tiempo (Reloj):** Temporizador analógico NE555 configurado en modo multivibrador astable, cuya frecuencia de conmutación se ajusta mediante una red RC formada por un potenciómetro de $10\text{ k}\Omega$ y capacitores de temporización.
- **Conteo Síncrono y Truncamiento:** Contador binario de 4 bits (74LS193 / 74HC93 en simulación) que incrementa su estado con cada flanco de reloj. Implementa un lazo de retroalimentación hacia la entrada de reinicio ($CLR = Q_D \cdot Q_B$) para resetear la cuenta al alcanzar el número binario $1010_2$ (10 decimal), restringiendo el ciclo de cuenta al intervalo $0-9$.
- **Decodificación y Despliegue:** Conversión de código binario BCD a formato de 7 segmentos mediante un circuito decodificador (74LS48 / CD4511), mostrando los dígitos de manera secuencial y continua a través de resistencias limitadoras de $330\ \Omega$.

---

### 🔄 Proyecto 6 — Registros de Corrimiento (Display de Mensaje Dinámico)
---

Diseño e implementación de un sistema digital secuencial sincronizado capaz de proyectar un mensaje en movimiento dinámico ("LA OLA") a través de un arreglo de cuatro displays de 7 segmentos de cátodo común.

La arquitectura integra:
- **Generador de Sincronía:** Temporizador NE555 en modo oscilador para dictar el ritmo de desplazamiento del texto.
- **Direccionamiento y Almacenamiento:** Contador binario 74LS193 que recorre secuencialmente las direcciones de una memoria EPROM ($8\times 8$ registros), la cual almacena los patrones de bits correspondientes a los caracteres alfanuméricos y espacios en blanco del mensaje.
- **Desplazamiento en Cascada:** Arreglo de cuatro registros de corrimiento bidireccionales/universales 74LS199 (flip-flops tipo D interconectados) que reciben las palabras binarias en paralelo y transfieren la información de segmento a segmento en cada flanco de subida de reloj hacia las pantallas de visualización.
