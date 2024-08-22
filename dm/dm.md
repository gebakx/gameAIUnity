# Decision Making

La figura següent mostra els components usuals d'un sistema *Game AI*:

|![Esquema GameAI](figures/esquema.png)|
|:--:| 
| *Font: (Millington, 2019)* |

El presa de decisions (*decision making*) és el segon nivell dins d'una IA. 

El problema consisteix en decidir quina és l'acció següent que ha d'emprendre un agent (NPC) donat l'entorn.

En un nivell superior d'una IA parlaríem de les accions d'un grup d'agents. En aquest cas s'apliquen les mateixes tècniques i parlem de tàctica o estrategia.

## Mètode de programació

En els motors de videojocs trobem dues formes de programació:

- Llenguatge de programació tradicional: C# en Unity i C++ en Unreal.

- *[Visual Scripting](vs.md)*: (*blueprints* en Unreal): programació visual a base de grafs.

|![](figures/pursue.png)|
|:--:| 
| Visual Scripting Graph |

En aquest tema aprofundirem en l'ús del *visual scripting*. Aquestes tècniques es solen utilitzar sovint en equips mixtes de programadors i disenyadors.

## Algorismes habituals per *decision making*

A continuació enumerem els algorismes més utilitzats en el presa de decisions ordenats per la complexitat dels problemes que poden resoldre.

- *[Màquines d'estat](fsm.md)* (*Finite States Machines*): és l'algorime més simple. Algorisme basat en estats i transicions entre estats.

|![](figures/fsm.png)|
|:--:| 
| Màquina d'estat |

- [Behavior Trees](bts.md): algorisme que permet abordar problemes una mica més complexes que les màquines d'estat.

|![](figures/bt.png)|
|:--:| 
| Behavior Tree |

- Planificadors: els sistemes anteriors tenen l'inconvenient de que només tenen en compte una única acció. En jocs d'estrategia, construcció/simulació o *rpg*, necessitem decidir una seqüència d'accions a prendre. 

  - Els sistemes més utilitzats són el *Goal Oriented Action Planning* (GOAP). El conjunt de les diferents possibles seqüències a prendre es representen en un arbre. El problema passa a ser un problema de cerca i es sol utilitzar l'algorisme de Dijkstra per la cerca. La figura següent mostra un exemple d'aquests arbres.

  - *[AI Planner](https://docs.unity3d.com/Packages/com.unity.ai.planner@0.3/manual/index.html)*: és una llibreria Unity que implementa un planificador per *decision making*. Els planificadors queden fora del temari de l'assignatura.

|![](figures/PlanVisualizer.png)|
|:--:| 
| *font*: [AIPlanner documentation](https://docs.unity3d.com/Packages/com.unity.ai.planner@0.3/manual/PlanVisualizer.html) |

- Sistemes basats en regles: són els sistemes més generals. Es fan servir motors d'inferència, sistemes basats en regles o programació funcional. També estan fora del temari de l'assignatura. Dos exemples d'ús són:

  - En programació de videojocs sense motors, es pot compilar la part IA programada en LISP a C++ per integrar-ho amb la part general del joc. El codi següent mostra la funció de fibonacci en Clojure (un dels derivats de LISP). 
```clojure
(defn fibonacci [n]
  (if (< n 2) n (+ (fibonacci (- n 1)) (fibonacci (- n 2)))))
```

  - El projecte [Arcadia](https://arcadia-unity.github.io/) està portant *Clojure* a Unity.

## Referències

- [Visual Scripting i màquines d'estat en Unity](https://docs.unity3d.com/Packages/com.unity.visualscripting@1.9/manual/index.html)

- Chris Simpson. [Behavior trees for AI: How they work](https://www.gamedeveloper.com/programming/behavior-trees-for-ai-how-they-work). Game Developer, 2014.

- [Muse Behavior](https://docs.unity3d.com/Packages/com.unity.muse.behavior@0.10/manual/index.html)

- [Muse AI](https://unity.com/products/muse)

- [AI Planner](https://docs.unity3d.com/Packages/com.unity.ai.planner@0.3/manual/index.html)

- [Projecte Arcadia-clojure](https://arcadia-unity.github.io/)

