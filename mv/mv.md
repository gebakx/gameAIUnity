# Moviment

## Introducció

La figura següent mostra els components usuals d'un sistema *Game AI*:

|![Esquema GameAI](figures/esquema.png)|
|:--:| 
| *Font: (Millington, 2019)* |

El moviment és el component de més baix nivell dins d'una IA. 

Aquest es sol descomposar en moviments atòmics molt simples que poden ser combinats per assolir-ne de molt complexos.

Per fer el moviment fem dues assumpcions:
- caràcter com a punts (centre de masses)
- treballem amb $2\frac{1}{2}$ dimensions per simplificar les fòrmules

Existeixen 3 nivells en el moviment:
- Cinemàtic: la velocitat és constant
- *Steering*: afegim acceleració
- *Steering* + *NavMesh*: afegim el sistema de *path finding*

## Individuals

- [Plantilla del moviment](template.md)

- *[Seek / flee](seek.md)* (cinemàtic i steering): moviment de l'agent va cap a un punt determinat o se n'allunya

- *[NavMesh](navmesh.md)* (seek): sistema integrat dels motors per fer *path finding*

- *[Wander](wander.md)*: moviment que simula un passeig aleatòri

- [Patrulla](patrolling.md): moviment en el que l'agent va seguint un camí predeterminat

- [Pursue / Evade]: pendent

- [Utilitats matemàtiques en Unity per al moviment](utils.md)

## Grupals

- [Formació](formacio.md): moviment típic de tropes

- *[Flocking](flocking.md)*: moviment típic de grups d'animals

## Referències

- Ian Millington. *AI for Games* (3rd ed). CRC Press, 2019.

- Craig W. Reynolds. [Steering Behaviors For autonomous Characters](http://www.red3d.com/cwr/papers/1999/gdc99steer.pdf). Proceedings of the Game Developers Conference (GDC), 1999.
