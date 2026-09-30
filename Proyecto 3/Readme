# 🚨 Proyecto 3: Sistema de Seguridad de 9 Zonas con Display de 7 Segmentos

Este proyecto consiste en el diseño e implementación de un sistema de seguridad digital utilizando circuitos integrados de mediana escala de integración (MSI). El sistema es capaz de monitorear 9 puntos o zonas diferentes y, al detectar una intrusión, muestra inmediatamente el número de la zona vulnerada en un display de 7 segmentos.

## 🛠️ Componentes Utilizados
*   **Codificador de Prioridad (SN74LS147):** Recibe las señales de los sensores. Como es de prioridad, si se activan dos sensores al mismo tiempo, dará preferencia al de mayor valor.
*   **Compuertas NOT (SN74LS04):** Se utiliza para invertir las salidas del codificador (ya que el 74147 entrega un código BCD invertido/negado) y así obtener un BCD positivo.
*   **Decodificador BCD a 7 Segmentos (SN74LS47 o SN74LS48):** Transforma el código binario (BCD) de 4 bits en las señales necesarias para encender los LEDs correctos del display.
*   **Display de 7 Segmentos:** (Ánodo o cátodo común, dependiendo del decodificador usado) para la visualización del número de la zona (1-9).
*   **Sensores y Simuladores:** Par de fototransmisores (infrarrojos) para zonas reales y un Dipswitch para simular el resto de las zonas.

## ⚙️ ¿Cómo funciona?
1.  **Detección (Entrada):** En estado normal, las 9 entradas del sistema se mantienen en un estado lógico ALTO (1). Cuando un intruso interrumpe la señal del sensor infrarrojo o se baja un switch, esa entrada específica cae a un estado lógico BAJO (0).
2.  **Codificación:** El integrado **74147** detecta ese `0` y lo convierte en un número binario de 4 bits. Sin embargo, su salida es activa en bajo, por lo que entrega el número invertido.
3.  **Acoplamiento Lógico:** Las señales pasan por los inversores del **7404**, aplicando una "doble negación" para recuperar el valor binario real (BCD estándar).
4.  **Decodificación y Visualización (Salida):** El código BCD entra al **7447/7448**, el cual enciende los segmentos correspondientes en el **display**, mostrando un número del 1 al 9 que alerta sobre la zona exacta donde ocurrió la intrusión.
