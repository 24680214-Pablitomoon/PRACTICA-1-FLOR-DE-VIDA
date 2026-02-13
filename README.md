# PRACTICA-1-FLOR-DE-VIDA
Documentación en blender de como hacer la flor de vida con python. 
Flor de Vida en Blender con Python
Introducción

La Flor de Vida es una figura geométrica formada por múltiples círculos del mismo radio, distribuidos simétricamente alrededor de un círculo central. Es un patrón basado en la repetición y la simetría radial.
En Blender, esta figura puede generarse mediante código Python utilizando la API bpy, creando círculos como primitivas geométricas y posicionándolos matemáticamente mediante funciones trigonométricas.

El programa:
Trabaja en el plano XY
Mantiene el eje Z = 0
Utiliza cálculos con seno y coseno
Genera múltiples círculos equidistantes
Aplica rotación angular constante

## En este caso se generará una Flor de Vida básica de 7 círculos:
1 círculo central
6 círculos alrededor, separados cada 60°

## Explicación del Código por Bloques
1️⃣ Importación de módulos

Se importan los módulos necesarios:
bpy → Controla Blender
math → Permite usar funciones trigonométricas y conversión de grados a radianes

Código: 
```Python
import bpy      # Permite interactuar con Blender
import math     # Permite usar funciones matemáticas como cos() y sin()
```

2️⃣ Limpieza de la escena
Antes de crear la figura, se eliminan todos los objetos existentes para evitar superposición o duplicados.

Código:
```Python
# Limpiar la escena eliminando todos los objetos
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()
```

3️⃣ Parámetros de la figura

Se definen variables que controlan el tamaño y la distribución:

radio → Tamaño de cada círculo
distancia → Distancia desde el centro
angulo_actual → Ángulo inicial
paso_angular → Incremento de 60° para distribuir 6 círculos

Código:
```Python
# Parámetros principales
radio = 3                 # Radio de cada círculo
distancia = radio         # Distancia desde el centro
angulo_actual = 0         # Ángulo inicial en grados
paso_angular = 60         # Separación angular de 60 grados
```

4️⃣ Creación del círculo central

Se crea el primer círculo en el origen (0,0,0).
vertices=64 se usa para que el círculo sea más suave visualmente.

Código:
```Python
# Crear círculo central en el origen
bpy.ops.mesh.primitive_circle_add(
    radius=radio,
    location=(0, 0, 0),
    vertices=64
)
```

5️⃣ Bucle para crear los círculos externos

Se utiliza un ciclo while para repetir el proceso hasta completar 360°.
Para cada iteración:

Se convierte el ángulo a radianes
Se calcula la nueva posición con:

x = r cos(θ)
y = r sin(θ)

Se crea un nuevo círculo en esa posición
Se incrementa el ángulo

Código:
```Python
# Crear círculos alrededor del central
while angulo_actual < 360:
    
    # Convertir grados a radianes
    x = distancia * math.cos(math.radians(angulo_actual))
    y = distancia * math.sin(math.radians(angulo_actual))
    
    # Crear círculo en la nueva posición
    bpy.ops.mesh.primitive_circle_add(
        radius=radio,
        location=(x, y, 0),
        vertices=64
    )
    
    # Incrementar el ángulo
    angulo_actual += paso_angular
```

## Resultado Final

Después de ejecutar el script en la pestaña Scripting y presionar Run Script, se obtendrá una figura llamada Flor de Vida básica, compuesta por:

1 círculo central
6 círculos distribuidos cada 60°
Todos ubicados en el plano XY

Geometría generada automáticamente mediante cálculos trigonométricos
La figura mostrará un patrón simétrico y armónico.

## 📌 Código Completo Final:
```Python 
import bpy
import math

# Limpiar la escena
bpy.ops.object.select_all(action='SELECT')
bpy.ops.object.delete()

# Parámetros de la figura
radio = 3
distancia = radio
angulo_actual = 0
paso_angular = 60

# Crear círculo central
bpy.ops.mesh.primitive_circle_add(
    radius=radio,
    location=(0, 0, 0),
    vertices=64
)

# Crear círculos alrededor
while angulo_actual < 360:
    
    x = distancia * math.cos(math.radians(angulo_actual))
    y = distancia * math.sin(math.radians(angulo_actual))
    
    bpy.ops.mesh.primitive_circle_add(
        radius=radio,
        location=(x, y, 0),
        vertices=64
    )
    
    angulo_actual += paso_angular
```

## Captura de pantalla de la visualización del código y la flor de vida en blender.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/20f6706c-b2cc-45db-baaf-d673bcead8cb" />

## Captura de pantalla del código en blender.
<img width="1008" height="897" alt="image" src="https://github.com/user-attachments/assets/68207ec6-bf7d-40ff-9522-72dd603836a5" />

## Captura de pantalla de la flor de vida en blender.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/1f1aac48-440d-49c4-9da0-f15a67b77a5a" />

