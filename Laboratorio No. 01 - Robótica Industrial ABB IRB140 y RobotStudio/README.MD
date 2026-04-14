<div align="center">
<h3>Curso de Robótica 2026-I</h3>

<h1>Desarrollo Laboratorio No.1 </h1>
<h2> Robótica Industrial: Trayectorias, entradas y salidas digitales. </h2>

<h3>Profesores: Pedro Fabián Cárdenas Herrera <br> Manuel Felipe Carranza Montenegro</h3>

<h3>Estudiantes: Juan Diego Sáenz Ardila <br> Alejandra Sofia Monroy Socha <br> </h3>

</div>

---

## Introducción al problema y descripción de la solución planteada 

### Planteamiento del problema

En este laboratorio se aborda el desarrollo de un sistema automatizado con el manipulador ABB IRB 140 para la decoración de una torta mediante un robot industrial, con el propósito de sustituir un proceso manual por uno programado que garantice mayor precisión, repetibilidad y control. El problema consiste en lograr que el robot ejecute trayectorias sobre una superficie plana que representa una torta virtual, en la cual se deben escribir los nombres de los integrantes del equipo y realizar una figura decorativa adicional.

Adicionalmente, el sistema debe integrar el control de una banda transportadora a través del uso de entradas y salidas digitales, y el diseño de una herramienta adecuada para realizar la decoración, de manera que todos los componentes funcionen de forma coordinada.

El desarrollo de la solución está sujeto a las siguientes especificaciones y restricciones:

- La torta está dimensionada para aproximadamente 20 personas, lo que define el área de trabajo.
- Los nombres de los integrantes deben ser legibles y estar separados dentro de la superficie.
- La decoración debe incluir al menos una figura adicional.
- Las trayectorias deben ejecutarse dentro de un rango de velocidades entre 100 y 1000.
- Se debe cumplir una tolerancia máxima de error en la posición de z10 mm.
- El movimiento debe realizarse como un trazo continuo.
- El proceso debe iniciar y finalizar en la misma posición *home*.

### Solución del problema

La solución se desarrolló de manera progresiva, teniendo como primer acercamiento el entorno virtual y luego el físico. Los pasos con los que se dió solución al problema y su respectiva descripción se muestran a continuación.

#### 1. Definición de la herramienta
Inicialmente, se consultó el datasheet del robot con el fin de identificar las especificaciones del flange (dimensiones y forma de ajuste), para luego realizar el modelado CAD de la herramienta en Autodesk Inventor. Este diseño incorporó consideraciones de orientadas a su fabricación mediante manufactura aditiva.
> El diseño detallado de la herramienta se presenta en una sección posterior.

#### 2. Caracterización del entorno de trabajo
Con el fin de definir un sistema coherente entre el entorno real y la simulación se realizaron las siguientes mediciones en el laboratorio:
- Posición y dimensiones de la banda transportadora.
- Distancia entre el robot y la zona de trabajo.

#### 3. Modelado del objeto de trabajo.
Con la zona de trabajo definida se modeló el pastel considerando: 
- La distribución espacial de los nombres.
- La creación de la figura decorativa.
El resultado final es: 
%IMAGEN PASTEL
> Este modelado se utilizó como guía para la generación de trayectorias del robot.

#### 4. Simulación y configuración en RobotStudio
En el entorno de sumulación se realizó el siguiente procedimiento: 
- Carga del robot y la herramienta diseñada.
- Definición del TCP (Tool Center Point).
- Creación de workobject virtual.

Finalmente, se programaron las trayectorias necesarias para: 
- Inicio de la rutina en *home*.
- Escritura de los nombres de los integrantes.
- Ejecución de la figura decorativa (corazón).
- Retorno a la posición *home*.

#### 5. Integración del sistema

Se integraron los distintos componentes del sistema, buscando la coordinación entre el robot y la banda transportadora mediante el uso de señales digitales.

Para el control de la banda, se implementó una lógica basada en entradas y salidas digitales (DI/DO), las cuales fueron previamente definidas tanto en el controlador como en el entorno de simulación de RobotStudio. Esto permitió disponer de una consola de simulación desde la cual se podían activar y monitorear las señales, facilitando la validación del comportamiento del sistema antes de su ejecución física.

Dado que no se contaba con un perfil caracterizado de velocidades de la banda transportadora, la sincronización del sistema no se realizó en función de velocidad, sino mediante parámetros temporales. Se definieron:

- Tiempos de activación de la banda (encendido/apagado).
- Tiempos de espera entre la llegada de un pastel y el siguiente.
- Tiempos de espera asociados a la ejecución del robot.

Adicionalmente, se implementó la lógica de ejecución del sistema mediante condiciones sobre las entradas digitales, así como una rutina de posición de mantenimiento, permitiendo llevar el robot a una configuración dónde el cambio de herramienta se dé fácilmente. Las entradas digitales se daban al sistema físico en forma de botones y las salidas eran el encendido y apagado de luces. 

#### 6. Implementación y pruebas en laboratorio

Una vez validado el sistema en el entorno de simulación, se procedió a su implementación en el laboratorio, con el objetivo de verificar la correspondencia entre el modelo virtual y el comportamiento físico del sistema.

En esta etapa se realizó la calibración experimental del TCP utilizando la herramienta física. Sin embargo, esta calibración presentó un error aproximado de **6 mm**, atribuible a imprecisiones en el proceso de medición y alineación. Debido a esto, para la ejecución final se optó por utilizar el TCP virtual, el cual presentaba error nulo con un modelado casi exacto de la herramienta real.

Por otro lado, se definió también workobject en el entorno real. A diferencia del TCP, en este caso se decidió trabajar con el workobject real ya que la banda transportadora en el laboratorio no coincidía exactamente con la representada en el simulador.

Durante las pruebas experimentales se ajustaron parámetros como:

- Tiempos de activación de la banda transportadora.
- Tiempos de espera entre ciclos.
- Sistemas coordenados del objeto de trabajo y la mejor ubicación según el tipo de acercamiento del robot. 

>  El resultado final del sistema se presenta en la sección de videos más adelante.

## Diagrama de flujo de acciones del robot

<div align="center">
<img src="imagenes/Diagrama_flujo.png" style="border-radius: 50%; width: 480px;">
</div>
