# Flor de vida

Crearemos una flor sencilla a partir de círculos en Blender.

Explicaremos las limeas de este codigo(al final estara el codigo completo)

1.
import bpy y import math: Son los libros de instrucciones. Uno le enseña al código cómo hablar con Blender (bpy) y el otro cómo hacer cuentas matemáticas (math).
select_all y delete: Es como tirar todo lo que hay en la mesa a la basura para empezar con un lienzo en blanco.

2.
Aquí defines cómo será tu dibujo antes de empezar:radio = 3: Es el tamaño de los círculos.paso_angular = 60: Es "cuánto giras la mano" para dibujar el siguiente círculo. Como un círculo completo tiene 360 grados, si saltas de 60 en 60, acabarás dibujando 6 pétalos exactos alrededor del centro ($360 / 60 = 6$).

3.
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)
Este es el círculo que va justo en medio de la pantalla, en las coordenadas $(0, 0, 0)$. Es el corazón de la flor.

5.
Para poner un círculo alrededor del centro:

Gira: Cambia el ángulo (angulo_actual += paso_angular).
Calcula: Usa matemáticas (coseno y seno) para saber dónde aterrizar el lápiz. Es como decir: "Avanza 3 pasos en la dirección en la que estás mirando".
Dibuja: Pone el círculo en esa nueva posición (x, y).

Codigo completo:

import bpy
import math

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

radio = 3
angulo_actual = 0
paso_angular = 60 # Cada 60 grados para obtener 6 círculos alrededor

bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

x1 = radio * math.cos(math.radians(angulo_actual))
y1 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x1, y1, 0), vertices=64)

angulo_actual += paso_angular
x2 = radio * math.cos(math.radians(angulo_actual))
y2 = radio * math.sin(math.radians(angulo_actual))
bpy.ops.mesh.primitive_circle_add(radius=radio, location=(x2, y2, 0), vertices=64)


# Ciclo para completar la flor










