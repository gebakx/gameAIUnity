# Pursue / Evade

El *steering* del *pursue* (perseguir) simula la persecución de otro agente en movimiento. El *evade* seria el movimiento opuesto.

|![](figures/pursuit.gif)|
|:--:| 
| *Fuente: (Reynolds, 1999)* |

La figura anterior muestra gráficamente en que consiste y el código siguiente una implementación en Unity. Consiste en estimar (*lookAhead*) hacia donde irá el agente perseguido y hacer un *seek* hacia la posición estimada.

```C#
Vector3 targetDir = target.transform.position - transform.position;
float lookAhead = targetDir.magnitude / agent.speed;
Seek(target.transform.position + target.transform.forward * lookAhead);
// Flee for evasion
```

### Demo

En el archivo [pursue](demos/pursue.unitypackage) encontraréis un ejemplo de implementación.

## Referències

- Craig W. Reynolds. [Steering Behaviors For autonomous Characters](http://www.red3d.com/cwr/papers/1999/gdc99steer.pdf). Proceedings of the Game Developers Conference (GDC), 1999.

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)
