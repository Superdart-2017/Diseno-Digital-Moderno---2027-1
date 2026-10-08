# Unidad Lógica Combinacional de 2 Bits (ALU Discreta)

## 📌 Descripción del Proyecto
Diseño, implementación y validación experimental de una **unidad combinacional de 2 bits** construida completamente con circuitos integrados TTL de lógica discreta (sin microcontroladores). 

El sistema toma dos operandos binarios de 2 bits ($A$ y $B$), ejecuta una de cuatro operaciones aritmético-lógicas seleccionables mediante control ($S_1, S_0$) y despliega el resultado numérico en un display de 7 segmentos. Incluye una señal global de habilitación (**ENABLE**) y un arreglo de LEDs que indica visualmente la operación activa.

---

## ⚙️ Operaciones Disponibles

| ENABLE | $S_1$ | $S_0$ | Operación | Salida ($Y_2 Y_1 Y_0$) | Indicador Display |
| :---: | :---: | :---: | :--- | :--- | :--- |
| `0` | `X` | `X` | **Sistema Deshabilitado** | `000` | Display apagado |
| `1` | `0` | `0` | **Suma (A + B)** | $C_{out}, S_1, S_0$ | Decimal 0 a 6 |
| `1` | `0` | `1` | **XOR ($A \oplus B$)** | $0, A_1 \oplus B_1, A_0 \oplus B_0$ | Decimal 0 a 3 |
| `1` | `1` | `0` | **AND ($A \cdot B$)** | $0, A_1 \cdot B_1, A_0 \cdot B_0$ | Decimal 0 a 3 |
| `1` | `1` | `1` | **Máximo (MAX)** | $0, \max(A, B)_1, \max(A, B)_0$ | Decimal 0 a 3 |

---

## 🧩 Arquitectura del Sistema
El diseño sigue una arquitectura modular en hardware:

1. **Entradas & Acondicionamiento:** DIP Switches configurados con arreglos de resistencias pull-down ($10\text{ k}\Omega$) para evitar estados flotantes.
2. **Bloque Operativo:**
   * **Suma:** Sumador completo de 4 bits (74LS283).
   * **XOR:** Compuertas XOR (74LS86).
   * **AND:** Compuertas AND (74LS08).
   * **MAX:** Red combinacional con comparador de magnitud ($A \ge B$) y lógica de conmutación (74LS04, 74LS08, 74LS32).
3. **Enrutamiento (Multiplexado):** Multiplexores dobles 4:1 (74LS153) gobernados por las líneas de selección $S_1, S_0$ y la señal `ENABLE`.
4. **Decodificación y Visualización:**
   * **Operación activa:** Decodificador 2 a 4 líneas (74LS139) hacia 4 LEDs de estado.
   * **Resultado numérico:** Decodificador BCD a 7 segmentos (74LS47) conectado a un display de ánodo/cátodo común.

```text
       +-----------------------+
       |     DIP SWITCHES      |
       |  (A[1:0], B[1:0], S)  |
       +-----------+-----------+
                   |
         +---------+---------+
         |                   |
         v                   v
+-----------------+   +---------------+
| Bloque Operador |   | Decodificador |
| (SUM, XOR, etc) |   | 2:4 (74LS139) |
+--------+--------+   +-------+-------+
         |                    |
         v                    v
+-----------------+      [ 4x LEDs ]
| MUX 4:1 74LS153 |
+--------+--------+
         |
         v
+-----------------+
| Driver 74LS47   |
+--------+--------+
         |
         v
  [ Display 7-Seg ]
