<div align="center">
<h3>Curso de Robótica 2026-I</h3>

<h1>Desarrollo Laboratorio No.3 </h1>
<h2> Operación, Análisis del Manipulador EPSON T3-401S </h2>

<h3>Profesores: Pedro Fabián Cárdenas Herrera <br> Manuel Felipe Carranza Montenegro</h3>

<h3>Estudiantes: Juan Diego Sáenz Ardila <br> Alejandra Sofia Monroy Socha <br> </h3>

</div>

## 1. Cuadro Comparativo: Motoman MH6, IRB140 y EPSON T3-401S 
| Característica Técnica | Motoman MH6 | ABB IRB 140 | Epson T3-401S |
|------------------------|-------------|-------------|---------------|
| Carga Máxima (Payload) | 6 kg | 6 kg | 3 kg |
| Alcance Horizontal | 1422 mm | 800 mm | 400 mm |
| Alcance Vertical | 2486 mm | 810 mm | 150 mm (eje Z) |
| Grados de Libertad | 6 ejes (8 con articulaciones extras del laboratorio) | 6 ejes | 4 ejes|
| Repetibilidad | ±0.08 mm | ±0.03 mm | ±0.02 mm(J1-J2-J3) , ±0.02° (J4) |
| Velocidad Máxima (Eje 1) | 220°/s | 200°/s | 3700 mm/s |
| Velocidad Máxima (Eje 2) | 200°/s | 200°/s | 3700 mm/s|
| Velocidad Máxima (Eje 3) | 220°/s | 260°/s | 1000 mm/s |
| Velocidad Máxima (Eje 4) | 410°/s | 360°/s | 2600°/s |
| Velocidad Máxima (Eje 5) | 410°/s | 360°/s | No aplica |
| Velocidad Máxima (Eje 6) | 610°/s | 450°/s | No aplica |
| Masa del Manipulador | 130 kg | 98 kg | 16 kg |
| Montaje | Suelo, pared, techo | Suelo, invertido, pared (cualquier ángulo) | Mesa (Tabletop) |
| Controlador | DX100 | IRC5 | RC90B |
| Protección Estándar | No especificado explícitamente | IP67 (toda la unidad) | CE Mark, EMC directive, Machinery directive, RoHS directive , ANSI/RIA R15.06-2021, NFPA 79 (Edición 2007) |
| Aplicaciones Típicas | Ensamble, soldadura (arco/punto), empaque, corte, manipulación de materiales | Manufactura, fundición, sala blanca, pegado, soldadura, carga/descarga | Ensamble, pick-and-place, manipulación de materiales, empaque, palletizado, inspección y pruebas |
## 2. Descripción de las configuraciones Home del EPSON T3-401S. 

Durante la práctica de laboratorio con el robot SCARA EPSON T3-401S se identificaron dos configuraciones Home diferentes:

### 2.1. Home 1 (predeterminado)

<div align="center">
<img src="Imágenes/Home 1.jpeg" style="border-radius: 50%; width: 380px;">
</div>

En la configuración predeterminada del fabricante, las articulaciones se encuentran en la siguiente posición:

<div align="center">

| Articulación | Valor | Pulsos |
| ------------ | ----- | ------ |
| J1           | 0°    | 0      |
| J2           | 0°    | 0      |
| J3           | 0 mm  | 0      |
| J4           | 0°    | 0      |

</div>

En esta condición, el primer eje rotacional (J1) orienta el robot hacia la dirección correspondiente al eje X del sistema de referencia utilizado por el fabricante.


### 2.2. Home 2 (Laboratorio)

<div align="center">
<img src="Imágenes/Home 2.jpeg" style="border-radius: 50%; width: 340px;">
</div>

Durante las prácticas de laboratorio se utiliza una configuración alternativa en la cual la articulación J1 se encuentra desplazada 90° respecto a la configuración original.

Los valores observados son:

<div align="center">

| Articulación | Valor | Pulsos |
| ------------ | ----- | ------ |
| J1           | 90°   | 204800 |
| J2           | 0°    | 0      |
| J3           | 0 mm  | 0      |
| J4           | 0°    | 0      |

</div>

Esta modificación orienta el robot hacia la dirección correspondiente al eje Y del sistema de trabajo.
La principal razón para utilizar una configuración Home con J1 = 90° es la adaptación del robot al entorno físico donde opera.

En la celda de trabajo del laboratorio, la orientación hacia el eje Y permite que el volumen de trabajo útil quede mejor alineado con la disposición de la mesa y de los elementos de manipulación. De esta manera, el robot inicia su operación apuntando directamente hacia la zona donde se realizan la mayoría de las tareas. Es importante destacar que la modificación del Home 2 no altera los límites mecánicos reales del robot. El robot conserva la misma capacidad física de movimiento, ya que únicamente se modifica el punto de referencia desde el cual se miden las posiciones articulares.

## 3. Proceso para realizar movimientos manuales.

### 3.1 Cambio al modo de enseñanza

<div align="center">
<img src="Imágenes/teach_pendant.jpeg" style="border-radius: 50%; width: 380px;">
</div>

1. Colocar el selector del Teach Pendant TP3 en modo `TEACH/T1`.
2. Acceder a la ventana `Jog & Teach`.
3. Verificar que el robot se encuentre habilitado para realizar movimientos manuales.

### 3.2 Selección del modo de operación

Dentro de la ventana `Jog & Teach`, en la opción `Mode`, seleccionar el sistema de coordenadas deseado:

| Modo | Descripción |
|--------|-------------|
| Joint | Movimiento individual de las articulaciones J1, J2, J3 y J4. |
| World | Movimiento cartesiano respecto al sistema de coordenadas global. |
| Tool | Movimiento cartesiano respecto al sistema de coordenadas de la herramienta. |
| Local | Movimiento cartesiano respecto al sistema de coordenadas local. |
| ECP | Movimiento respecto al punto central efectivo de la herramienta. |

### 3.3 Configuración de la distancia de desplazamiento

<div align="center">
<img src="Imágenes/Modos.png" style="border-radius: 50%; width: 400px;">
</div> 
En la sección `Jog Distance` se puede seleccionar:

| Opción | Descripción |
|---------|-------------|
| Continuous | El robot se mueve mientras se mantenga presionado el botón de desplazamiento. |
| Long | Movimiento incremental grande. |
| Medium | Movimiento incremental medio. |
| Short | Movimiento incremental pequeño. |

Cuando los robots no estan en modo "Continuous", las articulaciones se mueven de a pasos ( indicado en donde dice jog Distance). La diferencia entre short, medium y long, es que la distancia entre pasos puede ser mayor según el modo.

### 3.4 Movimiento en modo articulaciones (Joint)

Cuando se selecciona el modo `Joint`, cada control de desplazamiento actúa sobre una articulación específica:

| Control | Articulación |
|----------|-------------|
| J1 | Primera articulación |
| J2 | Segunda articulación |
| J3 | Eje vertical |
| J4 | Rotación final |

Procedimiento:

1. Mantener presionado el interruptor de habilitación (Enable Switch).
2. Pulsar la tecla correspondiente a la articulación que se desea mover.
3. Observar el desplazamiento y detener el movimiento soltando la tecla.

### 3.5 Movimiento en modo cartesiano

Cuando se selecciona cualquiera de los modos cartesianos (World, Tool, Local o ECP), los controles permiten desplazamientos sobre los ejes cartesianos.

Para robots SCARA de 4 grados de libertad como el T3-401S:

| Control | Movimiento |
|----------|------------|
| J1 | Traslación en X |
| J2 | Traslación en Y |
| J3 | Traslación en Z |
| J4 | Rotación alrededor del eje Z |

Procedimiento:

1. Seleccionar uno de los modos cartesianos.
2. Mantener presionado el interruptor de habilitación.
3. Utilizar las teclas de desplazamiento para mover el robot en la dirección requerida.
4. Verificar visualmente la trayectoria antes de continuar.

### 3.6 Registro de posiciones

Para almacenar una posición enseñada:

1. Situar el robot en la posición deseada.
2. En la ventana `Jog & Teach`, seleccionar el archivo de puntos (`Point File`).
3. Seleccionar el número de punto (`Point`).
4. Pulsar `Teach`.
5. Guardar los cambios mediante la opción `Save`.


## 4. Explicación sobre los niveles de velocidad. 

## 5. Descripción funcionalidades de EPSON RC+ 7.0, 

## 6. Comparación entre EPSON RC+ 7.0, RoboDK y RobotStudio. 

## 7. Diseño técnico del gripper neumático por vacío

## 8. Diagrama de flujo de la rutina de movimiento. 

## 9. Plano de planta montaje. 

## 10. Código desarrollado en EPSON RC+ 7.0. 

Con el fin de implementar la aplicación de pick and place con el robot, se desarrolló una rutina de paletizado para manipular dos huevos ubicados inicialmente en posiciones opuestas de una cubeta de 30 cavidades (6×5), trasladándolos de forma alternada a través de todas las posiciones disponibles. Como restricción del problema, cada desplazamiento debía realizarse siguiendo exclusivamente el patrón de movimiento de un caballo en un tablero de ajedrez. 
El código completo se presenta [aquí](./Código EPSON RC+ 7.0.MD) y consta de las siguientes secciones: 

### 10.1 Inicialización del sistema

El programa principal habilita los servomotores del robot y configura las condiciones de movimiento.

```python
Motor On
Power High
Accel 100, 100
Speed 100
```

Luego, el robot ejecuta de forma continua una secuencia en la que va a la posición Home, hace la ejecución de la rutina de paletizado y regresa nuevamente a Home.

```python
Do
    Home
    Call Palletized
    Home
Loop
```

### 10.2 Función de paletizado

La distribución de posiciones dentro de la cubeta de huevos se definió mediante la instrucción:

```python
Pallet 1, Origin, PointX, PointY, 6, 5
```

Esta función genera automáticamente una matriz de paletizado de 6 columnas y 5 filas, equivalente a las 30 posiciones disponibles en la cubeta.

Para definir dicha matriz se utilizaron tres puntos enseñados previamente al robot:

* **Origin:** posición correspondiente a una de las esquinas de referencia de la cubeta.
* **PointX:** punto utilizado para definir el límite y dirección de la cubeta en el eje X.
* **PointY:** punto utilizado para definir el límite y dirección de la cubeta en el eje Y.

A partir de estos tres puntos, el controlador calcula automáticamente las posiciones intermedias de la matriz, generando las 30 ubicaciones donde posteriormente se desplazan los huevos durante la simulación.

### 10.3 Definición de las secuencias de recorrido

El programa utiliza dos arreglos denominados **Verde** y **Rosa**.

```python
Integer Verde(30)
Integer Rosa(30)
```

Estos nombres fueron asignados debido a que durante el planteamiento del laboratorio los huevos fueron identificados por colores diferentes: un huevo verde y un huevo rosa.

Cada arreglo contiene una secuencia específica de posiciones dentro de la matriz de paletizado. Estas secuencias determinan el orden en que cada huevo debe visitar las distintas ubicaciones de la cubeta. A diferencia de un recorrido secuencial convencional, las posiciones fueron organizadas siguiendo el patrón inspirado en el movimiento de un caballo sobre un tablero de ajedrez.

De esta manera, ambos huevos recorren progresivamente las diferentes ubicaciones de la cubeta siguiendo trayectorias previamente definidas.

### 10.4 Alternancia entre los huevos

La rutina principal se ejecuta mediante un ciclo que recorre las posiciones almacenadas en ambos arreglos.

```python
For i = 1 To 29
```

Durante cada iteración, el robot realiza movimientos asociados al huevo verde y posteriormente movimientos asociados al huevo rosa.

```python
Jump Pallet(1, Verde(i))
Off DO_09

Jump Pallet(1, Verde(i + 1))
On DO_09

Jump Pallet(1, Rosa(i))
Off DO_09

Jump Pallet(1, Rosa(i + 1))
On DO_09
```

La instrucción **Jump** permite al robot desplazarse rápidamente entre las posiciones calculadas por la matriz de paletizado.

La salida digital **DO_09** se emplea para controlar la herramienta de manipulación del robot, la cual consiste en una ventosa utilizada para sujetar los huevos. Esta herramienta opera con lógica negada, por lo que el estado de la salida se interpreta de manera inversa al funcionamiento convencional. En consecuencia, las instrucciones `On DO_09` y `Off DO_09` permiten activar o desactivar el vacío necesario para tomar o liberar los huevos durante el recorrido programado.

La alternancia entre las secuencias Verde y Rosa permite observar simultáneamente el comportamiento de ambos huevos dentro de la cubeta, verificando que cada uno siga la trayectoria definida y visite las posiciones correspondientes.

## Video de simulación en EPSON RC+ 7.0.
A continuación se presenta el link del video de youtube donde se encuentra el video: [Video resultado final Laboratorio 3](https://youtu.be/6_o-GGpcaL4)
## Gracias 
