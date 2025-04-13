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
<img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/switch-debounce-principle.jpg" width="30%">

### 2.3 Solución por Hardware
<img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/8a7fb498516bd68a6215badee5aff517d8df4a3b.gif" width="30%">

#### 2.3.1 Solución por Hardware RC

 - Circuito adicional en la entrada del pulsador o boton, se le agrega un filtro de reset, se encarga de detener ese reset, que rechaze ese rebote
 - Se agrega un seguidor (Amplificador de ganancia 1)
 - Esto garantiza que el voltaje se entregue totalmente al microcontrolador

#### 2.3.2 Calculo red RC
 - El cálculo se realiza igualando la constante de carga y descarga del condensador
 - Tener en cuenta los tiempos de carga y de descarga del condensador

   |            CARGA            |         DESCARGA        |
   |:---------------------------:|:-----------------------:|
   | Tiempo de carga=((R1+R2)*C) | Tiempo de descarga=R2*C |

 - La elección de los elementos se dan por los tiempos requeridos para el sistema
 - No hay ganancia el Voltaje maximo sera de **5V**

#### 2.3.3 Respuesta del Pulsador
 - Con el filtro detecta el primer pulso y el filtro disminuye la señal rapidamente, cuando se hace el siguiente pulso la señal es tan baja que es un **0 logico** 

### 2.4 Solución por Software

 - Es tratar de asegurar el estado que estamos detectando a traves de la señal que llego, entonces se espera para actuar,el se espera el tiempo de rebote para saber si la señal se mantiene
 - Habran retardos, pero por software se verifica el estado

#### 2.4.1 Pseudocódigo

     If(entrada_pulsador!=valor_pulsador){
     Delay(tiempo de establecimiento);  //Establecido segun la necesidad
     valor_pulsador= entrada_pulsador   //La idea es detectar los dos cambios de alto a bajo y de bajo a alto
     }
     
## 2.5 Teclado Matricial

### 2.5.1 Tipos de Teclado

 - **MEMBRANA (plastico)** : No tienen efecto rebote (Hace retorno)

   <img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/61zXZuDDsNL._AC_UF1000%2C1000_QL80_.jpg" width="20%">
   
 - **MECÁNICOS**
   
   <img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/61MSwM4cmvL.jpg" width="30%">

### 2.5.2 Teclado Matricial

>  🔑 Teclado Matricial: Es una matriz de pulsadores (Se nombra por la cantidad de filas y columnas)

     - Ej: 4 * 3 Significa que tenemos 4 Filas y 3 Columnas, se necesitan 7 pines para identificar la matriz

 - Se disminuye la cantidad de pines
 - Al pulsar envia un caracter y el usuario define dentro de la logica del programa

### 2.5.3 Uso del Teclado Matricial 

<img src="https://github.com/HeisenDiaz/Teclado-Matricial-Perifericos/blob/main/Distribucion_de_Pines_Teclado_Matricial_Membrana_3x4_Auto_Adhesivo_12_Teclas_Teclado_4x3_Ferretronica.webp" width="30%">

### 2.5.4 Pseducódigo

- Activar resistencias de pullup
- Activar interrupciones externas detección estado
- Activar interrupciones globales
- Repetir:
  - “Mover” un 0 lógico por los pines conectados a las columnas del teclado
- Si se presenta interrupción
- Identificar la Tecla pulsada
- Codificar la tecla

**Importante detectar cambio de estado completo, no flanco**

### 2.5.5 Osciladores 
 
 Se controlan a partir de CONFIG1L y CONFIG1H
 - Varia entre familias, no se cambia cuando se esta corriendo el programa, se debe volver a programar el **PIC** si se quiere cambiar

#### 2.5.5.1

**OSCON & OSTUNE**

Tipos hay diferentes; 2 Familias internas y externas

## 3. Conclusiones

- El diseño de hardware es fundamental en aplicaciones con microcontroladores, ya que garantiza una correcta interpretación de señales de entrada (sensores, botones) y un control preciso de las salidas (actuadores, displays)
- El uso de resistencias pull-up o pull-down es indispensable para asegurar un estado lógico definido en los botones o pulsadores, evitando lecturas erróneas por entradas flotantes
- El efecto rebote es una condición inherente al diseño mecánico de pulsadores, y puede generar múltiples lecturas no deseadas en una sola pulsación. Este fenómeno debe ser tratado para asegurar la fiabilidad del sistema
- Existen soluciones tanto por hardware como por software para eliminar el rebote, siendo la elección dependiente de los recursos disponibles y la precisión requerida
- Los osciladores internos o externos del PIC18F4550 determinan la velocidad del sistema, y deben configurarse adecuadamente antes de cargar el programa al microcontrolador
## 4. Autores

  ### Luis Fernando Pulido Salazar - 76257
  ### Heisen Jawer Diaz Ascencio - 137604
