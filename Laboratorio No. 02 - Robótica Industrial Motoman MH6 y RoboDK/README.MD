<div align="center">
<h3>Curso de Robótica 2026-I</h3>

<h1>Desarrollo Laboratorio No.2 </h1>
<h2> Robótica Industrial - Análisis y Operación del Manipulador Motoman MH6. </h2>

<h3>Profesores: Pedro Fabián Cárdenas Herrera <br> Manuel Felipe Carranza Montenegro</h3>

<h3>Estudiantes: Juan Diego Sáenz Ardila <br> Alejandra Sofia Monroy Socha <br> </h3>

</div>

---

## 1. Cuadro Comparativo: Motoman MH6 vs. ABB IRB 140. 

| Característica Técnica | Motoman MH6 | ABB IRB 140 |
|---|---|---|
| **Carga Máxima (Payload)** | 6 kg | 6 kg |
| **Alcance Horizontal** | 1422 mm | 800 mm |
| **Alcance Vertical** | 2486 mm | 810 mm (altura del brazo) |
| **Grados de Libertad** | 6 ejes ( 8 con las articulaciones extras especificas del trabajado en este laboratorio) | 6 ejes |
| **Repetibilidad** | ±0.08 mm | ±0.03 mm |
| **Velocidad Máxima (Eje 1)** | 220°/s | 200°/s |
| **Velocidad Máxima (Eje 2)** | 200°/s | 200°/s |
| **Velocidad Máxima (Eje 3)** | 220°/s | 260°/s |
| **Velocidad Máxima (Eje 4)** | 410°/s | 360°/s |
| **Velocidad Máxima (Eje 5)** | 410°/s | 360°/s |
| **Velocidad Máxima (Eje 6)** | 610°/s | 450°/s |
| **Masa del Manipulador** | 130 kg | 98 kg |
| **Montaje** | Suelo, pared, techo | Suelo, invertido, pared (cualquier ángulo) |
| **Controlador** | DX100 | IRC5 |
| **Protección Estándar** | No especificado explícitamente | IP67 (toda la unidad) |
| **Aplicaciones Típicas** | Ensamble, soldadura (arco/punto), empaque, corte, manipulación de materiales | Industrias manufactureras, fundición, sala blanca, pegado, soldadura, carga/descarga |

---

## 2. Descripción de las configuraciones home1 y home2 del Motoman MH6. 

### 2.1 Configuración Home 1 (Posición de transporte)

<div align="center">
<img src="Imagenes/home1.png" style="border-radius: 50%; width: 450px;">
</div>


<br>
Esta posición corresponde a una configuración de reposo, transporte o almacenamiento del robot, donde el manipulador permanece contraído para minimizar el espacio ocupado y reducir esfuerzos mecánicos sobre los actuadores. 

Los valores articulares observados en el Teach Pendant son: 

| Eje | Origin | Current |
|---|---|---|
| S | 0 | -1 |
| L | -115290 | -115290 |
| U | -111622 | -111621 |
| R | 1 | 1 |
| B | 42647 | 42646 |
| T | 1392 | 1392 |

### 2.2 Configuración Home 2 (Posición de operación)

<div align="center">
<img src="Imagenes/home2.png" style="border-radius: 50%; width: 450px;">
</div>

<br>
Esta configuración corresponde a la posición de referencia mecánica utilizada para calibración, sincronización y verificación de alineación de los ejes del robot. 

Los valores articulares observados en el Teach Pendant son: 

| Eje | Specified | Current | Difference |
|---|---|---|---|
| S | 0 | 0 | 0 |
| L | 2037 | 2037 | 0 |
| U | 2359 | 2359 | 0 |
| R | 0 | 0 | 0 |
| B | -121 | -121 | 0 |
| T | 1392 | 1392 | 0 |

### ¿Cuál configuración es mejor?

En operación industrial, la configuración Home 1 suele ser la más conveniente como posición de reposo. Al mantener el robot compacto, reduce el espacio ocupado, disminuye el riesgo de colisiones y genera menor esfuerzo sobre los ejes principales mientras el robot está detenido.

Por otro lado, la configuración Home 2 es más útil para calibración y programación, ya que facilita la verificación visual de la alineación de los ejes y la referencia mecánica del manipulador.

## 3. Proceso para realizar movimientos manuales.

## 4. Explicación sobre los niveles de velocidad. 

## 5. Descripción funcionalidades RoboDK, comunicación con el manipulador Motoman y procesos de ejecución de movimiento. 

## 6. Comparación entre RoboDK y RobotStudio. 

## 7. Diagrama de flujo de acciones del robot. 
```mermaid
%%{init: {
  "flowchart": {
    "curve": "linear",
    "nodeSpacing": 28,
    "rankSpacing": 34
  },
  "themeVariables": {
    "fontSize": "14px"
  }
}}%%

flowchart TD

%% ===== BLOQUES PRINCIPALES =====
A1["Importación de librerías"] --> A2["Empezar y verificar la<br/>conexión con el robot"]
A2 --> A3["Creación del marco de<br/>referencia y ajuste de este<br/>al robot"]
A3 --> A4["Ajuste de velocidad y<br/>toleracia del robot"]
A4 --> A5["Creación de parametros de<br/>la figura"]
A5 --> A6["Creación de parametros de<br/>acercamiento en z"]
A6 --> A7["Crear y ir a home"]
A7 --> A8["Ir al 0 del marco del objeto"]
A8 --> A9["Vuelta_completa= 2*pi"]
A9 --> A10["Punto=0"]

D1{Punto==Numero<br/>de Puntos+1?}

A10 --> D1

%% ===== RAMA 1: RECORRIDO DE PUNTOS =====
D1 -->|No| B1["theta=Vuelta*Punto/<br/>Numero de Puntos"]
B1 --> B2["r = Amplitud * (1 +<br/>|cos(2*theta + pi/2)|)"]
B2 --> B3["Transformación de r y<br/>theta a x y y"]
B3 --> B4["Con x y y ir al punto<br/>conseguido"]
B4 --> B5["Punto= Punto + 1"]
B5 --> D1

%% ===== RAMA 2: CREACIÓN DE TEXTPATH =====
D1 -->|Yes| C1["Creación de los<br/>TextPath"]
C1 --> C2["Separación de vertices<br/>y el tipo de trayectoria"]
C2 --> C3["Escalar y trasladar los<br/>valores en x y en y"]
C3 --> C4["Vuelta_completa= 2*pi"]
C4 --> C5["Punto=0"]

D2{Punto==Numero<br/>de Vertices?}
C5 --> D2

%% ===== RAMA 3: MOVIMIENTO FINAL =====
D2 -->|Yes| E1["Moverse encima del último<br/>punto"]
E1 --> E2["Ir a home"]

D2 -->|No| D3{"La trayectoria es<br/>un MoveJ?"}

D3 -->|Yes| F1["Moverse encima de Punto<br/>de cualquier forma"]
F1 --> F2["Moverse a punto de<br/>cualquier forma"]
F2 --> P["Process"]

D3 -->|No| G1["Moverse a punto de<br/>cualquier forma"]
G1 --> P

P --> D2

%% ===== ESTILOS =====
classDef box fill:#d6e6ff,stroke:#3d3d3d,stroke-width:1px,color:#000;
classDef decision fill:#ffffff,stroke:#3d3d3d,stroke-width:1px,color:#000;
classDef process fill:#6fa8dc,stroke:#3d3d3d,stroke-width:1px,color:#000;

class A1,A2,A3,A4,A5,A6,A7,A8,A9,A10,B1,B2,B3,B4,B5,C1,C2,C3,C4,C5,E1,E2,F1,F2,G1,P box;
class D1,D2,D3 decision;

%% ===== COLORES DE RAMAS =====
linkStyle 10 stroke:#ff6b6b,stroke-width:2px
linkStyle 11 stroke:#55c95e,stroke-width:2px
linkStyle 20 stroke:#55c95e,stroke-width:2px
linkStyle 21 stroke:#ff6b6b,stroke-width:2px
linkStyle 22 stroke:#ff6b6b,stroke-width:2px

```
## 8. Plano de planta del robot. 

## 9. Código de RoboDK. 

## 10. Video resultado final Laboratorio 2. 

## Gracias 


