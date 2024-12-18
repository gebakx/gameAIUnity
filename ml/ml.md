# Aprenentatge per reforç amb ML-Agents

En aquest apartat veurem com entrenar agents amb aprenentatge per reforç amb [ML-Agents](https://github.com/Unity-Technologies/ml-agents).

## Guia d'instal·lació

Per instal·lar el ML-Agents hem de seguir una sèrie de pasos que estan descrits a la [documentació oficial](https://github.com/Unity-Technologies/ml-agents/blob/develop/docs/Installation.md) del paquet.

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

**Nota**: per instal·lar-lo en una màquina Windows recomanen utilitzar l'Anaconda. A l'arxiu [mlagentsGuide.txt](mlagentsGuide.txt) teniu una petita que heu d'adaptar amb el que hi ha més amunt.


## Introducció

El ML-Agents té com a component principal l'aprenentatge per reforç (*Reinforcement Learning*):

![esquema](rl.png)
[font: thomassimonini.medium](https://thomassimonini.medium.com/q-learning-lets-create-an-autonomous-taxi-part-2-2-8cbafa19d7f5)

L'aprenentatge per reforç conté dos grans elements: l'*agent* per al que volem fer aprendre un comportament i l'*entorn* en el que es mou. El procés consisteix en un bucle en el que l'entorn dona una descripció del món a l'agent (*observacions*), l'agent decideix una acció a efectuar (mitjançant *actuadors*) i l'entorn li torna una *recompensa* (que pot ser negativa) en funció de com ho hagi fet l'agent.

A continuació veurem com declarar aquests components en un projecte Unity per aprendre el comportament d'un agent. Tot es fa mitjançant un *script* amb una classe de tipus *Agent* que conté tota la lògica de l'agent i un arxiu de configuració *.yaml* que conté els paràmetres de l'aprenentatge.

En afegir l'script amb la classe *Agent*, ens apareixerà automàticament el component *Behavior Parameters* on podrem establir paràmetres com el tipus d'observacions o el model entrenat. Adicionalment, haurem d'afegir-li el component *Decision Requester* a l'agent.

### Observacions

Les definirem mitjantçant un mètode anomenat *CollectObservations*:

```c#
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(transform.position);
        sensor.AddObservation(transform.forward);
    }
```

A l'exemple estem afegint com a observacions la posició i cap a on està mirant l'agent en qüestió. Cadascun d'aquest dos tenen una mida de 3, ja que són vectors. Haurem d'especificar als *Behavior Parameters - Vector Observation - Space Size* una mida de 6.

Uns dels sensors més utilitzats en aquest tipus d'aprenentatge són els "Ray Casts". ML-Agents en proporciona un component per tractar-los automàticament. Només hem d'afegir el component *Ray Cast Sensor 3D* al nostre agent i configurar les seves propietats. Això inclou els *tags* dels objectes que volem detectar. En afegir aquest component, no cal afegir res al mètode *CollectObservation*. Ja ho fa ell tot sol.

### Accions

Hi ha dos tipus d'accions que podem crear: continues (força a aplicar a un objecte) o discretes (girar a l'esquerra).

Si utilitzem les continues tindrem quelcom com:
```c#
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        // Actions, size = 2
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);
    }
```
en que s'està aplicant una força a un objecte per control·lar el seu moviment.

Si utilitzem accions discretes:
```c#
    public override void OnActionReceived(ActionBuffers actions)
    {
        if (actions.DiscreteActions[1] == 1)
        {
            transform.Rotate(transform.up * -turnSpeed * Time.deltaTime);
        } 
        else if (actions.DiscreteActions[1] == 2)
        ...
    }
```
en que es veu el gir cap a l'esquerra com una acció discreta.


### Recompenses

Per afegir recompenses teniu dos mètodes:
```c#
    AddReward(-0.01f);
    SetReward(+1f);
```

El primer afegeix una recompensa (s'utilitza per anar afegint recompenses petites acumulatives) i el segon n'estableix (s'utilitza en recompenses finals en cas d'èxit o fracas).

Aquestes últimes solen venir acompanyades a una crida al mètode *EndEpisode();* que fa acabar l'episodi d'entrenament actual. Disposem així mateix del mètode *OnEpisodeBegin()* per inicialitzar els episodis.

### Paràmetres de l'algorisme d'entrenament

Els paràmetres de l'entrenament s'estableixen en un arxiu *yaml*:

```
behaviors:
  RollerBall:                # nombre del agente            
    trainer_type: ppo        # algoritmo de reinforcement learning: ppo, sac...
    hyperparameters:
        ...
    network_settings:
      normalize: false
      hidden_units: 128      # número de neuronas de la red neuronal
      num_layers: 2          # número de capas de la red neuronal
    reward_signals:
        ...
    max_steps: 500000        # número de iteraciones
    summary_freq: 10000      # frecuencia de report de les recompensas
    ...
```

Els paràmetres mostrats són alguns dels més importants. Mireu la [documentació](https://unity-technologies.github.io/ml-agents/Training-Configuration-File/) per obtenir més informació.

## Consells per a l'entrenament

El disseny de sistemes d'aprenentatge per reforç no és una tasca senzilla. Aquí us oferim una sèrie de consells per orientar-vos en aquesta tasca.

El primer consell és mirar algun exemple semblant al que tracteu de solucionar i partir de la solució que propossen. Un recurs molt interessant és el de la [llista d'exemples del propi ML-Agents](https://unity-technologies.github.io/ml-agents/Learning-Environment-Examples/).

El segon consell és que un cop programat l'agent el probeu amb el mètode *Heuristics* que admet el control manual de l'agent i el probeu a consciència:

```c#
    public override void Heuristic(in ActionBuffers actionsOut)
    {
        ...
        var actions = actionsOut.DiscreteActions;
        actions[0] = v;
        actions[1] = h;
    }
```

La complexitat del problema a tractar requerirà una complexitat equivalent per tal d'aprendre un model útil. Els paràmetres més importants a nivell de complexitat seran:

- el tipus d'algorisme: *ppo*, *sac*, *curiosity*, *curriculum learning*...

- les observacions i recompenses del sistema

- el nombre de capes i neurones de la xarxa neuronal

- el nombre d'iteracions

Si el sistema no és capaç de trobar un model vàlid, reviseu primerament els paràmetres anteriors.


## Referències

- [Unity ML-Agents Toolkit](https://github.com/Unity-Technologies/ml-agents)

- Haonan Jin. [NPC's en Karting Game](https://upcommons.upc.edu/handle/2117/411664), 2024. [Github](https://github.com/YudaLegend/TFG-ML-AGENTS)
