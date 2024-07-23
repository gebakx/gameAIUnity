# Wander

|![](figures/wander.png)|
|:--:| 
| *Font: (Millington, 2019)* |


```C#
Vector3 localTarget =  UnityEngine.Random.insideUnitSphere;
localTarget.y = 0f;
localTarget.Normalize();
localTarget *= radius;
localTarget += new Vector3(0, 0, offset);

Vector3 worldTarget = transform.TransformPoint(localTarget);

Seek(worldTarget);
```

### Demo

A l'arxiu [wander](demos/wander.unitypackage) trobareu un exemple d'implementació.
L'agent involucrat es diu *robber* i trobareu els paràmetres.

## Referències

- Ian Millington. *AI for Games* (3rd ed). CRC Press, 2019.

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)
