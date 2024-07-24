# Patrolling

L'*steering* del *patrolling* vol simular un agent fent una patrulla (recorregut tancat).
Aquest moviment s'implementa amb una llista ordenada de punts, anomenats *way points*. L'agent començarà fent un *seek* cap al primer punt, quan estigui suficientment a prop, farà un *seek* cap al següent de la llista, i així successivament.

Una forma d'implementar els *way points* en Unity és mitjançant *Empty GameObjects*.

El codi següent mostra una implementació en Unity:

```C#
public GameObject[] waypoints;

int patrolWP = 0;

void Patrol()
{
    patrolWP = (patrolWP + 1) % waypoints.Length;
    Seek(waypoints[patrolWP].transform.position);
}
```

Una ampliació que se sol utilitzar d'aquest *steering* és la tècnica de suavitzat basat en fantasmes. Aquesta tècnica consisteix en aplicar el patrolling a un objecte invisible i fer que l'agent real vagi seguint al fantasma. D'aquesta forma s'aconsegueix un moviment més realista.

### Demo

A l'arxiu [patrolling](demos/patrolling.unitypackage) trobareu un exemple d'implementació amb la tècnica dels fantasmes. El fantasma està visible per veure el moviment real. En un cas real, desactivariem el component *Material* del fantasma per fer-lo invisible.

## Referències

- [Making an Agent Patrol Between a Set of Points](https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavAgentPatrol.html)

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)
