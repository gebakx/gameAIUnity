# Behavior Trees

**Comentarios previos**:

El diseño de árboles de comportamiento es una tarea no trivial. Os recomiendo que leais el articulo [Behavior trees for AI: How they work](https://www.gamedeveloper.com/programming/behavior-trees-for-ai-how-they-work) para empezar.

Existen dos módulos llamados *Muse* en Unity:

- *Muse Behavior*: módulo para trabajar con *behavior trees*. Necesita instalación externa. Es el que utilizaremos.

- *Muse AI*: módulo de pago que tiene un componente *behavior* que permite generar los *behavior trees* con técnicas de IA generativa.

**Instalación en el proyecto del Muse Behavior**:

Para poder utilizar este componente se tiene que instalar previamente. Ir al menú, *Window - Package Manager*, clicad en lel **+** ubicado en la parte superior izquierda y *Add package by name..*. Introducir el nombre **com.unity.muse.behavior**. Una vez instalado, podéis cerrar el *Package Manager*.

**Ejemplo**:

En este documento mostraremos como funcionan los *behavior trees* en Unity a partir de un ejemplo: un policia irá (*seek*) hacia un ladrón cuando esté lejos de él y ira "mirándolo/vigilándolo" cuando esté cerca.

Utilizaremos el *Muse Behavior Agent* como componente para ejecutar los *behavior trees*:

|![](figures/copInspector3.png)|
|:--:| 
| Componente *Muse Behavior Agent* |

Tenemos la *Blackboard* como mecanismo de compartición de variables entre los *behavior trees* y el entorno.

A continuación tenéis la implementación de los *behavior trees*:

|![](figures/bt.png)|
|:--:| 
| Behavior Tree |

La *Acción* `Self moves to robber` tiene las propiedades (en el *Node Inspector*):

| propiedad | valor |
|:--|:--| 
| Agent | Self |
| Target | robber |
| Speed | 2 |
| Distance Threshold | 3 |

La condición añadida al nodo *Abort If* está definida por nosotros y tiene el código:

```C#
using System;
using System.Collections.Generic;
using UnityEngine;
using Unity.Muse.Behavior;

[Serializable]
[Condition(name: "farAway", story: "d(cop, robber) > 5", category: "distances", id: "bc032ce09737b7062dca7f01eaba3690")]
public class farAway : Condition
{
    public BlackboardVariable<GameObject> Agent;
    public BlackboardVariable<GameObject> Target;
    public override bool IsTrue()
    {
        return Vector3.Distance(
            Agent.Value.transform.position,
            Target.Value.transform.position) > 5f;
    }
}
```

Las implementaciones de *Behavior Trees* suelen tener los componentes básicos y facilidad para implementar acciones y condiciones. El código anterior os sirve como ejemplo de condición. A continuación tenéis un ejemplo de acción (que no se utiliza en la implementación de este documento) que para el movimiento del agente:

```C#
using System;
using UnityEngine;
using Unity.Muse.Behavior;
using Action = Unity.Muse.Behavior.Action;

[Serializable]
[NodeDescription(name: "Stop", story: "Stops the agent", category: "Action/Move", id: "37d14153df25444624d82be524a73527")]
public class Stop : Action
{
    public BlackboardVariable<GameObject> Agent;
    private UnityEngine.AI.NavMeshAgent m_NavMeshAgent;

    protected override Status OnStart()
    {
        return Status.Running;
    }

    protected override Status OnUpdate()
    {
        m_NavMeshAgent = Agent.Value.GetComponentInChildren<UnityEngine.AI.NavMeshAgent>();
        if (m_NavMeshAgent != null)
        {
            m_NavMeshAgent.isStopped = true;
        }
        return Status.Success;
    }

    protected override void OnEnd()
    {
    }
}


```

## Implementación

- [Behavior Trees](demos/bts.unitypackage)

## Referencias

- [Muse Behavior](https://docs.unity3d.com/Packages/com.unity.muse.behavior@0.10/manual/index.html)

- Chris Simpson. [Behavior trees for AI: How they work](https://www.gamedeveloper.com/programming/behavior-trees-for-ai-how-they-work). Game Developer, 2014.

- [Muse AI](https://unity.com/products/muse)

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)

