# Patrolling

El *steering* del *patrolling* quiere simular a un agente de patrulla (recorrido cerrado).
Este movimiento se implementa con una lista ordenada de puntos, llamados *way points*. El agente empezará haciendo un *seek* hacia el primer punto, cuando este suficientmente cerca, hará un *seek* hacia el siguiente de la lista, y así sucesivamente.

Una forma de implementar los *way points* en Unity es mediante *Empty GameObjects*.

El código siguiente muestra una implementación en Unity:

```C#
public GameObject[] waypoints;

int patrolWP = 0;

void Patrol()
{
    patrolWP = (patrolWP + 1) % waypoints.Length;
    Seek(waypoints[patrolWP].transform.position);
}
```

Una ampliación que se suele utilizar de este *steering* es la técnica de suavizado basado en fantasmas. Esta técnica consiste en aplicar el patrolling a un objeto invisible y hacer que el agente real lo vaya siguiendo. De  este forma se consigue un movimiento más realista.

### Demo

En el archivo [patrolling](demos/patrolling.unitypackage) encontraréis un ejemplo de implementación con la técnica de los fantasmas. El fantasma está visible para ver el movimiento real. En un caso real, desactivaríamos el componente *Material* del fantasma para volverlo invisible.

## Referencias

- [Making an Agent Patrol Between a Set of Points](https://docs.unity3d.com/Packages/com.unity.ai.navigation@1.1/manual/NavAgentPatrol.html)

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)
