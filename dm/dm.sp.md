# Decision Making

La figura siguiente muestra los componentes usuales de un sistema *Game AI*:

|![Esquema GameAI](figures/esquema.png)|
|:--:| 
| *Fuente: (Millington, 2019)* |

La toma de decisiones (*decision making*) es el segundo nivel dentro de una IA. 

El problema consiste en decidir cúal es la acción siguiente que tiene que hacer un agente (NPC) dado el entorno.

En un nivel superior de una IA hablaríamos de las acciones de un grupo de agentes. En este caso se aplican las mismas técnicas y hablaremos de táctica o estrategía.

## Método de programación

En los motores de videojuegos encontramos dos formas de programación:

- Lenguaje de programación tradicional: C# en Unity y C++ en Unreal.

- *[Visual Scripting](vs.sp.md)*: (*blueprints* en Unreal): programación visual a base de grafs.

|![](figures/pursue.png)|
|:--:| 
| Visual Scripting Graph |

En este tema profundizaremos en el uso del *visual scripting*. Estas técnicas se suelen utilizar a menudo en equipos mixtos de programadores y diseñadores.

## Algoritmos habituales para *decision making*

A continuación enumeramos los algoritmos más utilizados en la toma de decisiones ordenados por la complejidad de los problemas que pueden resolver.

- *[Máquinas de estado](fsm.sp.md)* (*Finite States Machines*): es el algoritmo más simple. Está basado en estados y transiciones entre estados.

|![](figures/fsm.png)|
|:--:| 
| Máquina de estados |

- [Behavior Trees](bts.sp.md): algoritmo que permite abordar problemas un poco más complejos que las máquinas de estados.

|![](figures/bt.png)|
|:--:| 
| Behavior Tree |

- Planificadores: los sistemas anteriores tienen el inconveniente de que sólo tienen en cuenta una única acción. En juegos de estrategía o *rpgs*, necesitamos decidir una secuencia de acciones a hacer. 

  - Los sistemas más utilizados son los *Goal Oriented Action Planning* (GOAP). El conjunto de las diferentes posibles secuencias a seguir se representan en un árbol. El problema pasa a ser un problema de búsqueda y se suele utilizar el algoritmo de Dijkstra para la búsqueda. La figura siguiente muestra un ejemplo de estos árboles.

  - *[AI Planner](https://docs.unity3d.com/Packages/com.unity.ai.planner@0.3/manual/index.html)*: es una librería Unity que implementa un planificador para *decision making*. Los planificadores quedan fuera del temario de la asignatura.

|![](figures/PlanVisualizer.png)|
|:--:| 
| *fuente*: [AIPlanner documentation](https://docs.unity3d.com/Packages/com.unity.ai.planner@0.3/manual/PlanVisualizer.html) |

- Sistemas basados en reglas: son los sistemas más generales. Se utilizan motores de inferencia, sistemas basados en reglas o programación funcional. También estan fuera del temario de la asignatura. Dos ejemplos de uso son:

  - En programación de videojuegos sin motores, se puede compilar la parte de IA programada en LISP a C++ para integrarla con la parte general del juego. El codi siguiente muestra la función de fibonacci en Clojure (uno de los derivados de LISP). 
```clojure
(defn fibonacci [n]
  (if (< n 2) n (+ (fibonacci (- n 1)) (fibonacci (- n 2)))))
```

  - El proyecto [Arcadia](https://arcadia-unity.github.io/) está portando *Clojure* a Unity.

## Referencias

- [Visual Scripting y máquinas de estados en Unity](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.9/manual/index.html)

- Chris Simpson. [Behavior trees for AI: How they work](https://www.gamedeveloper.com/programming/behavior-trees-for-ai-how-they-work). Game Developer, 2014.

- [Muse Behavior](https://docs.unity3d.com/Packages/com.unity.muse.behavior@0.10/manual/index.html)

- [Muse AI](https://unity.com/products/muse)

- [AI Planner](https://docs.unity3d.com/Packages/com.unity.ai.planner@0.3/manual/index.html)

- [Proyecto Arcadia-clojure](https://arcadia-unity.github.io/)

