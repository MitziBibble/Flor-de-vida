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

Imagen de la flor petalo por petalo:
https://github.com/MitziBibble/Flor-de-vida/issues/1#issue-3935010266

# Ciclo para completar la flor

1.
import bpy: Estas importando el modulo que actua como puente entre Pyton y el interior de Blender.
import math: La necesitamos para calcular dónde poner cada círculo usando ángulos.

2.
bpy.ops.object.select_all(action='SELECT'): Selecciona absolutamente todo lo que haya en la pantalla (cubos, luces, cámaras).
bpy.ops.object.delete(): ¡Pum! Borra todo. Así empezamos con una pantalla vacía y limpia.

3.
radio = 3: Decidimos que nuestros círculos tendrán un tamaño de 3 unidades.angulo_actual = 0: Empezamos a contar desde el grado 0 (como si fuera la aguja de un reloj marcando las 3 en punto).
paso_angular = 60:Queremos dar saltos de 60 en 60 grados. Como un círculo completo tiene 360 grados, $360 / 60 = 6$, así que dibujaremos 6 círculos alrededor.

4.
bpy.ops.mesh.primitive_circle_add(...): Esta línea crea el primer círculo.
location=(0, 0, 0): Lo pone justo en el centro del mundo.

5.
En lugar de escribir 6 veces lo mismo, usamos un while (que significa "mientras").

6.
while angulo_actual < 360:: Es una pregunta: "¿El ángulo es menor a 360?". Si la respuesta es sí, el código hace lo siguiente:
math.radians(angulo_actual): Python no entiende los "grados" normales, así que los convierte a un lenguaje que él entiende (radianes).
x = radio * math.cos(...) e y = radio * math.sin(...): Es para saber en qué parte del borde del círculo central debe ir el nuevo pétalo.
bpy.ops.mesh.primitive_circle_add(...): Crea un círculo nuevo en esa posición (x, y) que acabamos de calcular.
angulo_actual += paso_angular: Le sumamos 60 al ángulo. Si no hiciéramos esto, el ángulo siempre sería 0 y el código se quedaría pegado creando círculos en el mismo sitio para siempre (el ordenador se trabaría).

Codigo completo con while:

import bpy
import math

bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

radio = 3
angulo_actual = 0
paso_angular = 60 

bpy.ops.mesh.primitive_circle_add(radius=radio, location=(0, 0, 0), vertices=64)

while angulo_actual < 360:
    # Calcular posición X e Y usando trigonometría
    x = radio * math.cos(math.radians(angulo_actual))
    y = radio * math.sin(math.radians(angulo_actual))

Imagen de la Flor completa:  https://github.com/MitziBibble/Flor-de-vida/issues/2#issue-3935010882   
    
   


















