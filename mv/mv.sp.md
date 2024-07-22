# Movimiento

## Introducción

La figura siguiente muestra los componentes usuales de un sistema *Game AI*:

|![Esquema GameAI](figures/esquema.png)|
|:--:| 
| *Font: (Millington, 2019)* |

El movimiento es el componente de más bajo nivel dentro de una IA.

Este se suele descomponer en movimientos atómicos muy simples que pueden ser combinados para conseguir de muy complejos.

Para hacer el movimiento asumiremos:
- caràcter como puntos (centro de masas)
- trabajaremos en $2\frac{1}{2}$ dimensiones para simplificar las fórmulas

Existen 3 niveles en el movimiento:
- Cinemático: la velocidad es constante
- *Steering*: añadimos acceleración
- *Steering* + *NavMesh*: añadimos el sistema de *path finding*

## Individuales

- [Plantilla del movimiento](template.sp.md)

- *[Seek / flee](seek.sp.md)*: movimiento del agente hacia un punto determinado o se aleja

- *[Wander](wander.sp.md)*: movimiento que simula un paseo aleatorio

- [Patrulla](patrolling.sp.md): movimiento en el que el agente va siguiendo un camino predeterminado

- *[NavMesh](navmesh.sp.md)*: sistema integrado de los motores para hacer *path finding*

- [Utilidades matemáticas en Unity para el movimiento](utils.sp.md)

## Grupales

- [Formación](formacio.sp.md): movimiento típico de tropas

- *[Flocking](flocking.md)*: movimiento típico de grupos de animales

## Referencías

- Ian Millington. *AI for Games* (3rd ed). CRC Press, 2019.

- Craig W. Reynolds. [Steering Behaviors For autonomous Characters](http://www.red3d.com/cwr/papers/1999/gdc99steer.pdf). Proceedings of the Game Developers Conference (GDC), 1999.
