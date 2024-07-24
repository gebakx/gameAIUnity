# Wander

L'*steering* del *wander* vol simular un agent passejant tanquil·lament.

|![](figures/wander.png)|
|:--:| 
| *Font: (Millington, 2019)* |

La figura anterior mostra gràficament en que consisteix i el codi següent una implementació en Unity. L'algorisme té dos paràmetres:
- **radi** d'una cercle: es calcula aleatòriament un punt de la circumferència.
- **offset**: se li suma aquesta distància al punt anterior.
El punt resultant del *wander* serà la suma d'aquest vector al *forward* de l'agent (eix Z). Es va cridant al *wander* cada vegada que l'agent s'apropa a l'últim punt i es fa un *seek* cap al nou punt.

```C#
Vector3 localTarget =  UnityEngine.Random.insideUnitSphere;
localTarget.y = 0f;
localTarget.Normalize();
localTarget *= radius;
localTarget += new Vector3(0, 0, offset);

Vector3 worldTarget = transform.TransformPoint(localTarget);

Seek(worldTarget);
```

De cara a implementar el moviment s'han d'ajustar els paràmetres para que la velocitat sigui relativament baixa i control·lar que el punt resultant del *wander* estigui en una posició "caminable".


### Demo

A l'arxiu [wander](demos/wander.unitypackage) trobareu un exemple d'implementació.

## Referències

- Ian Millington. *AI for Games* (3rd ed). CRC Press, 2019.

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)
