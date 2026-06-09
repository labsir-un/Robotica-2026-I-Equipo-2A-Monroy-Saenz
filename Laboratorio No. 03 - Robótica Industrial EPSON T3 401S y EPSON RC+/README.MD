<div align="center">
<h3>Curso de Robótica 2026-I</h3>

<h1>Desarrollo Laboratorio No.3 </h1>
<h2> Operación, Análisis del Manipulador EPSON T3-401S </h2>

<h3>Profesores: Pedro Fabián Cárdenas Herrera <br> Manuel Felipe Carranza Montenegro</h3>

<h3>Estudiantes: Juan Diego Sáenz Ardila <br> Alejandra Sofia Monroy Socha <br> </h3>

</div>

## 1. Cuadro Comparativo: Motoman MH6, IRB140 y EPSON T3-401S 

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

## 4. Explicación sobre los niveles de velocidad. 

## 5. Descripción funcionalidades de EPSON RC+ 7.0, 

## 6. Comparación entre EPSON RC+ 7.0, RoboDK y RobotStudio. 

## 7. Diseño técnico del gripper neumático por vacío

## 8. Diagrama de flujo de la rutina de movimiento. 

## 9. Plano de planta montaje. 

## 10. Código desarrollado en EPSON RC+ 7.0. 

## Video de simulación en EPSON RC+ 7.0.

## Gracias 
