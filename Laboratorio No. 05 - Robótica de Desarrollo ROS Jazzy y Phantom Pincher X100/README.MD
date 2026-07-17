<div align="center">
<h3>Curso de Robótica 2026-I</h3>

<h1>Desarrollo Laboratorio No.5 </h1>
<h2> Phantom X Pincher X100 – ROS 2 Jazzy – RViz - Turtlesim </h2>

<h3>Profesores: Pedro Fabián Cárdenas Herrera <br> Manuel Felipe Carranza Montenegro</h3>

<h3>Estudiantes: Juan Diego Sáenz Ardila <br> Alejandra Sofia Monroy Socha <br> </h3>

</div>

# Actividad 2. Identificación de motores y articulaciones

En esta actividad se identificaron las cinco articulaciones del robot Phantom X Pincher X100, junto con el identificador DYNAMIXEL asignado a cada servomotor, la referencia del actuador, el sentido positivo de movimiento y la función que desempeña cada una dentro del manipulador. Esta información constituye la base para la implementación de los algoritmos de control desarrollados en las actividades posteriores.

## Identificación de las articulaciones

| Articulación | ID | Referencia | Sentido positivo | Función |
|:------------:|:--:|:----------:|:----------------:|----------|
| Base | 1 | AX-12A | Antihorario | Rotación de la base del robot. |
| Hombro | 2 | AX-12A | Elevación | Permite elevar y descender el brazo principal. |
| Codo | 3 | AX-12A | Flexión | Modifica la apertura del brazo mediante la flexión del antebrazo. |
| Muñeca | 4 | AX-12A | Rotación | Orienta el efector final antes de la pinza. |
| Pinza | 5 | AX-12A | Apertura | Permite la apertura y el cierre de la pinza para sujetar objetos. |

# Actividad 4. Movimiento individual de articulaciones

Para esta actividad se implementó el nodo `individual_joint_move.py`, cuyo propósito es controlar de manera independiente cada una de las articulaciones del robot Phantom X Pincher X100. El programa publica comandos sobre el tópico `/pincher/command` utilizando mensajes del tipo `sensor_msgs/JointState`, enviando únicamente la articulación que se desea mover mientras las demás permanecen en su posición actual.

El funcionamiento del programa corresponde al modo demostración, en el cual cada articulación ejecuta automáticamente tres posiciones angulares predefinidas dentro de sus límites seguros y posteriormente retorna a la posición de referencia. De esta manera se verifica el movimiento individual de la base, hombro, codo, muñeca y pinza, tal como lo solicita la guía del laboratorio.

## Posiciones de demostración

Se definieron tres posiciones de prueba para cada articulación. Estas posiciones se encuentran dentro de los límites seguros del manipulador y permiten comprobar el correcto funcionamiento de cada eje.

```python
DEMO_POSITIONS_DEG = {
    "waist": [-40.0, 0.0, 40.0],
    "shoulder": [-30.0, 20.0, -10.0],
    "elbow": [30.0, -30.0, 10.0],
    "wrist": [-40.0, 40.0, 0.0],
    "gripper": [-60.0, 60.0, 0.0],
}
```

Cada conjunto de posiciones es recorrido automáticamente antes de regresar la articulación a la posición inicial.

## Creación del nodo ROS 2

Se implementó la clase `IndividualJointMover`, encargada de crear el nodo y el publicador que envía los comandos al robot mediante el tópico `/pincher/command`.

```python
class IndividualJointMover(Node):

    def __init__(self):

        super().__init__("individual_joint_move")

        self.publisher = self.create_publisher(
            JointState,
            "/pincher/command",
            10
        )

        time.sleep(0.3)
```

Una vez inicializado el nodo, este queda preparado para publicar los mensajes de control hacia el manipulador.

## Envío de movimientos

Cada movimiento es validado antes de ser enviado para garantizar que el ángulo solicitado se encuentre dentro del rango seguro de operación. Posteriormente se construye un mensaje `JointState` con el nombre de la articulación y la posición angular correspondiente.

```python
def send(self, joint: str, angle_deg: float) -> None:

    angle_deg = check_safe(joint, angle_deg)

    msg = JointState()

    msg.header.stamp = self.get_clock().now().to_msg()

    msg.name = [joint]

    msg.position = [math.radians(angle_deg)]

    self.publisher.publish(msg)
```

La función `check_safe()` impide el envío de posiciones que excedan los límites definidos para el robot.

## Ejecución automática de la demostración

El modo demostración recorre automáticamente todas las articulaciones del robot. Para cada una se ejecutan tres posiciones angulares y finalmente se retorna a la posición de referencia.

```python
def run_demo(node, settle_s=2.0):

    for joint in JOINT_ORDER:

        for angle in DEMO_POSITIONS_DEG[joint]:

            node.send(joint, angle)

            time.sleep(settle_s)

        node.go_home(joint)
```

Este procedimiento permite comprobar el funcionamiento independiente de cada articulación antes de continuar con las demás.

## Ejecución del programa

La demostración automática se ejecuta mediante el siguiente comando:

```bash
ros2 run pincher_control individual_joint_move --demo
```

## Código fuente completo

El código completo desarrollado para esta actividad se encuentra en el archivo:

```text
pincher_control/individual_joint_move.py
```
