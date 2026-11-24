# 📡 Proyecto Final: Decodificador de Clave Morse

Este proyecto consiste en el diseño, construcción y verificación de un sistema digital secuencial con estados explícitos capaz de capturar tres símbolos mediante botones independientes (**PUNTO** y **RAYA**), decodificar las 8 combinaciones posibles de tres símbolos en clave Morse (`S`, `U`, `R`, `W`, `D`, `K`, `G`, `O`) y mostrar su equivalente binario en LEDs hasta recibir una señal de reinicio (`RESET`).

---

## 🛠️ Componentes Utilizados

* **Registros de Corrimiento Universal (`74HC194` $\times 2$):** Almacenan de forma secuencial los símbolos capturados (código Morse) y llevan el registro de la longitud de la secuencia ($n$).
* **Flip-Flop Tipo D (`74HC74`):** Implementa la bandera de estado `VALID`, reteniendo la confirmación de la letra una vez que se completan los 3 símbolos.
* **Inversor Disparador Schmitt (`74HC14`):** Acondiciona las señales provenientes de los pulsadores (junto con redes RC) para eliminar el rebote mecánico y evitar lecturas falsas en la zona prohibida ($1.5\text{ V}$ a $3.5\text{ V}$).
* **Compuertas Lógicas (`74HC86` XOR y `74HC08` AND):** Gestionan la habilitación de pulsos (bloqueando pulsaciones simultáneas de PUNTO y RAYA mediante $XOR = 0$) y condicionan las salidas visuales (`código` $\cdot$ `VALID`).
* **Interfaz de Entrada y Salida:** 4 pulsadores (`PUNTO`, `RAYA`, `CONFIRMAR`, `RESET`) y 4 LEDs indicadores (3 para el código binario `LED2`, `LED1`, `LED0` y 1 para la bandera `VALID`).
* **Componentes Pasivos y de Soporte:** Resistencias limitadoras de $330\ \Omega$ (4), resistencias pull-down/pull-up de $10\text{ k}\Omega$ (8), capacitores cerámicos de $100\text{ nF}$ para filtrado antirrebote (4) y desacople de alimentación (6), protoboard y fuente de alimentación regulada a $5\text{ V}$ DC.

---

## ⚙️ ¿Cómo funciona?

1. **Acondicionamiento y Antirrebote:** Cada pulsación en los botones pasa por un filtro RC ($10\text{ k}\Omega$ y $100\text{ nF}$) conectado al disparador Schmitt (`74HC14`), asegurando transiciones limpias y registrando cada evento una sola vez.
2. **Validación y Captura de Símbolos ($n < 3$):** La etapa combinacional (`XOR` + `AND`) verifica que no se presionen `PUNTO` y `RAYA` al mismo tiempo. Si $n < 3$, el pulso desplaza e ingresa el símbolo correspondiente en los registros `74HC194`, avanzando por los estados desde `E0` hasta el Nivel 3.
3. **Bloqueo y Confirmación ($n = 3$):** Al alcanzar los 3 símbolos capturados, el sistema bloquea la entrada de nuevos puntos o rayas. Únicamente al presionar `CONFIRMAR`, el flip-flop `74HC74` activa la bandera `VALID = 1`.
4. **Decodificación y Visualización:** Mientras `VALID = 0`, los LEDs de código permanecen apagados (`000`). Cuando `VALID = 1`, las compuertas `AND` habilitan la salida en los LEDs (`LED2`, `LED1`, `LED0`), mostrando el valor binario del `0` (`000` para `S`) al `7` (`111` para `O`).
5. **Reinicio del Sistema (`RESET`):** La señal `RESET` (activa en bajo) limpia los registros de corrimiento y reinicia la bandera `VALID` desde cualquier estado, regresando la máquina al estado inicial `E0`.
