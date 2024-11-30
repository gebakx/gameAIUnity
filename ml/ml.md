# Aprenentatge per reforç amb ML-Agents

En aquest apartat veurem com entrenar agents amb aprenentatge per reforç amb [ML-Agents](https://github.com/Unity-Technologies/ml-agents).

## Guia d'instal·lació

Per instal·lar el ML-Agents hem de seguir una sèrie de pasos que estan descrits a la (documentació oficial](https://github.com/Unity-Technologies/ml-agents/blob/develop/docs/Installation.md) del paquet.

Les probes les hem realitzat amb una màquina Linux.

**Requeriments**:

- Unity versió 2023.2 o superior.

- Python entre 3.10.1 i 2.10.12.

**Instal·lació en una màquina**:

El primer pas es obrir un terminal i instal·lar la llibreria **pytorch** (xarxes neuronals):

```
pip install torch
```

A continuació hem de clonar el component de *github*:

```
git clone --branch release_22 https://github.com/Unity-Technologies/ml-agents.git
```

A continuació instal·lem els dos paquets que connecten el *Python* amb el *ML-Agents* i *Unity*:

```
cd ml-agents/
python3 -m pip install ./ml-agents-envs
python3 -m pip install ./ml-agents
```

En aquest punt us hauria de funcionar el següent:

```
mlagents-learn
```

![captura](mlagents-learn.png)


**Instal·lació en el projecte Unity**:

Per a cada projecte Unity que utilitzi el ML-Agents heu d'afegir un parell d'assets del component que heu clonat de *github*. Heu de mostrar el *package manager* mitjançant el menú, opció *Window* subopció *Package Manager*:

![captura](package-manager.png)

Cliqueu en el botó *+* que hi ha a la part de dalt a l'esquerra i *Add package from disk...*. En aquest punt haureu de seleccionar l'arxiu *package.json* que trobareu a la carpeta *com.unity.ml-agents*.

Repetiu el procés amb la carpeta *com.unity.ml-agents.extensions*. 

En aquest punt us haurien de sortir els paquets *ML Agents* i *ML Agents Extensions* tal i com mostra la figura de dalt.

**Nota**: per instal·lar-lo en una màquina Windows recomanen utilitzar l'Anaconda. A l'arxiu [mlAgentsGuide.txt](mlAgentsGuide.txt) teniu una petita que heu d'adaptar amb el que hi ha més amunt.


## Introducció

- components: recompenses, observacions, actuadors (continu vs discret), raycasting, arxiu yml

- Tutorial (Roller ball)
  - Demo: funcionant

## Consells per a l'entrenament

- Raycasting

- Curriculum learning

- Enllaç al TFG de Haonan

- Complexitat: mida xarxa, epochs, curiosity, sac vs ??

## Referències

- [Unity ML-Agents Toolkit](https://github.com/Unity-Technologies/ml-agents)
