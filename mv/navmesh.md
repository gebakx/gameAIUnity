# NavMesh 

|![](figures/NavMesh.svg)|
|:--:| 
| *Font: [Inner Workings of the Navigation System](https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavInnerWorkings.html)* |

## Components del sistema de navegació

**NavMesh Surface**: component per al sistema de polígons que representa tota la superfície "caminable"

**NavMesh Agent**: component per als agents que permet la navegació sobre les *NavMesh Surfaces*

**Off-Mesh Link**: component per a crear dreceres o salts entre *surfaces*

**NavMesh Obstacle**: component que permet etiquetar objectes dinàmics com a obstacles

## NavMesh Surface

**Instal·lació en el projecte**:

Per poder utilitzar aquest component s'ha d'instal·lar previament. Aneu al menú, *Window - Package Manager*, cliqueu al **+** ubicat a la part de dalt a l'esquerra i *Add package by name..*. Introduiu el nom **com.unity.ai.navigation**. Un cop instal·lat, podeu tancar el *Package Manager*.

**Creació de les superfícies**:

Seleccioneu l'objecte que representa el terra de l'escena i afegiu el component *NavMesh Surface*. Assegureu-vos que el camp *Default Area* està a *Walkable*.

Afegiu el component *NavMesh Modifier* a tots els altres objectes de l'escena. Seleccioneu el valor *Add or Modify object* a tots els objectes estàtics que representin obstacles i *Remove* per als agents.

Seleccioneu el terra i cliqueu en el botó *Bake* del component *NavMesh Surface*. Això ens crearà la superfície de polígons.

![](figures/NavMeshSurface.png)

## NavMesh Agent

El *NavMesh Agent* és el responsable de fer un *seek* combinat amb el *path finding* i l'*object avoidance*:

|![](figures/NavMeshLoop.svg)|
|:--:| 
| *Font: [Inner Workings of the Navigation System](https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavInnerWorkings.html)* |

**Component**:

Afegiu el component *NavMesh Agent* a l'objecte que volqueu fer moure.

![](figures/NavMeshAgent.png)

Fixeu-vos que podeu modificar un munt de paràmetres relacionats amb el moviment.

**Script**:

Per fer que l'objecte es mogui haureu de crear un *script* i afegir-lo com a component a l'agent.

```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.AI;

public class Moves : MonoBehaviour
{
    public NavMeshAgent agent;
    public GameObject target;

    void Start()
    {
        Seek();        
    }

    void Seek()
    {
        agent.destination = target.transform.position; 
    }
}
```

Un cop fet això, recordeu afegir, dins l'Inspector, el propi agent a la propietat *agent* i la destinació a *target*. Assignar una posició a la propietat *destination* del *NavMesh Agent* equival a fer un *seek* avançat.

### Demo

A l'arxiu [seekSurface](demos/seekSurface.unitypackage) trobareu un exemple d'implementació.
L'agent involucrat es diu *robber* i trobareu una sèrie de paràmetres:

## Referències

- [Inner Workings of the Navigation System](https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavInnerWorkings.html)

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)


