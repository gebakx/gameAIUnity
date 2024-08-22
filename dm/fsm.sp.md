# Finite State Machines

En este documento mostraremos como funcionan las máquinas de estados en Unity a partir de un ejemplo: un policia irá persiguiendo a un ladrón cuando esté lejos de él y lo irá "mirando/vigilando" cuando esté cerca.

Las máquinas de estado están integradas en el mecanismo del *Visual Scripting*. Pero utilizaremos el *State Machine* como componente para ejecutar les máquinas de estado:

|![](figures/copInspector2.png)|
|:--:| 
| Componente *State Machine* |

Para implementar el código de los estados y las transiciones utilizaremos graphs del *Visual Scripting*. A continuación tenéis la implementación de la máquina de estados:

|![](figures/fsm.png)|
|:--:| 
| Máquina de estados |

Para el estado *pursue* utilizaremos el graph `pursue` del ejemplo de *Visual Scripting*. A continuación tenéis las implementaciones del estado *look* y les dos transiciones:

|![](figures/lookFSM.png)|
|:--:| 
| Estado *look* |

|![](figures/pursue2look.png)|
|:--:| 
| Transición *pursue -> look* |

|![](figures/look2pursue.png)|
|:--:| 
| Transición *look -> pursue* |


## Implementación

- [Máquina de estados](demos/fsm.unitypackage)

## Referencias

- [Visual Scripting y máquinas de estados en Unity](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.9/manual/index.html)

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)
