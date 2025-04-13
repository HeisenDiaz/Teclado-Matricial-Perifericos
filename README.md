# Teclado-Matricial-Perifericos

## 1. HARDWARE

 - En una aplicación de microcontroladores el hardware se refiere a los 
dispositivos que podrián estar conectados en entrada y salida.

|    Entradas    |   Salidas  |
|:--------------:|:----------:|
| Sensores       | Leds       |
| Potenciometros | Display    |
| Pulsadores     | Motores    |
| Botones        | Actuadores |

### 1.1 Pulsadores/Botones

>  🔑 Pulsador: Cambia y mantiene el estado solamente si se mantiene pulsado, puede ser **NO** o **NC**

>  🔑 Boton: Cambia y mantiene el estado solamente pulsando una vez, para recuperar el estado de reposo


### 1.2 Circuito Pulsadores/Botones

 - No deben quedar al aire sin un estado definido
 - Asegurar su estado depende de la resistencia, si tenemos 1 o 0
<img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/resistencia-pull-up-down-e1435659241597.png" width="30%">
                   R=V/I

                   P= V1*VCC = I^2R1*R1

                   - Potencia en Watts para escoger el voltaje de la resistencia


## 2. EFECTO REBOTE

### 2.1 Características Mecánicas

 - Los pulsadores y botones (incluyendo las teclas) son normalmente, dispositivos mecánicos que cierran un circuito poniendo en contacto dos laminas metalicas, los problemas mas comunes presentados son:
   - Ruido
   - Vibraciones
   - Cambios de voltaje 
 - No se presentan este tipo de fenómenos en teclados de tipo capacitivo o resistivo

### 2.2 Efecto Rebote

 - Vibración o ruido se conoce como efecto rebote
 - Cambios de estado que hubo en una pulsación
 - Durante un cierto tiempo el pulsador (ó el botón) oscila entre cerrado y abierto.
<img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/resistencia-pull-up-down-e1435659241597.png" width="30%">

### 2.3 Solución por Hardware RC

 - Circuito adicional en la entrada del pulsador o boton, se le agrega un filtro de reset, se encarga de detener ese reset, que rechaze ese rebote
 - Se agrega un seguidor (Amplificador de ganancia 1)
 - Esto garantiza que el voltaje se entregue totalmente al microcontrolador
