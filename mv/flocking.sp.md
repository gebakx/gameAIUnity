# Flocking

Es el típico movimiento grupal de animales como aves o peces.

|![](figures/birds.jpg)|
|:--:| 
| *Fuente: [Birds of a Feather Flock](https://blogs.unimelb.edu.au/sciencecommunication/2014/09/06/birdphysics/)* |

## Componentes

Se basa en la suma de tres reglas simples:

**Cohesion**: centro de masas de los vecinos

|![](figures/cohesion.gif)|
|:--:|
| *Fuente: (Reynolds, 1999)* |

**Match velocity/align**: promedio de la velocidad/dirección de los vecinos

|![](figures/alignment.gif)|
|:--:|
| *Fuente: (Reynolds, 1999)* |

**Separation**: separación de los vecinos cercanos

|![](figures/separation.gif)|
|:--:| 
| *Fuente: (Reynolds, 1999)* |

## Implementación

Para esta implementación utilizaremos un objeto *manager* que instanciará (*spawn*) a los miembros del grupo. Le asociaremos el código siguiente: 

```C#
public class FlockManager : MonoBehaviour {
    public GameObject flockPrefab;
    public int numFlocks = 20;
    public float limit = 5f;
    public GameObject[] allFlocks;


    [Header("Flocking Settings")]
    [Range(0.0f, 5.0f)]
    public float minSpeed;
    [Range(0.0f, 5.0f)]
    public float maxSpeed;
    [Range(1.0f, 10.0f)]
    public float neighbourDistance;
    [Range(0.0f, 5.0f)]
    public float rotationSpeed;

    void Start() {
        allFlocks = new GameObject[numFlocks];
        for (int i = 0; i < numFlocks; ++i) {
            Vector3 pos = this.transform.position + new Vector3(Random.Range(-limit, limit),
                                                                Random.Range(-limit, limit),
                                                                Random.Range(-limit, limit));
            Vector3 randomize = new Vector3 (Random.value * 2 - 1, Random.value * 2 - 1, Random.value * 2 - 1);
            allFlocks[i] = (GameObject)Instantiate(flockPrefab, pos, Quaternion.LookRotation(randomize));
            allFlocks[i].GetComponent<Flock>().myManager = this;
        }
    }
}
```

Fijaros que el método *Start* está instanciando a los miembros del grupo en posiciones y rotaciones aleatorias alrededor de el mismo. Así mismo está asignándose a la propiedad *myManager* de cada uno de los miembros para que puedan acceder a los otros miembros y a los parámetros del algoritmo:

![](figures/flockingManager.png)

Fijaros que uno de los parámetros es el *preFab* (modelo gráfico). A este *preFab* le añadiremos el código siguiente (que contiene las reglas del *flocking*):

```C#
public class Flock : MonoBehaviour {
    public FlockManager myManager;
    [HideInInspector]
    public float speed;
    [HideInInspector]
    public Vector3 direction;

    void Start() {
        speed = UnityEngine.Random.Range(myManager.minSpeed, myManager.maxSpeed);
        direction = transform.forward * speed;
        StartCoroutine("Flocking");
    }

    void Update() {
        transform.rotation = Quaternion.Slerp(transform.rotation,
                                              Quaternion.LookRotation(direction),
                                              myManager.rotationSpeed * Time.deltaTime);
        transform.Translate(0.0f, 0.0f, Time.deltaTime * speed);
    }

    IEnumerator Flocking()
    {
        while (true)
        {
            float waitTime = Random.Range(0.3f, 0.5f);
            yield return new WaitForSeconds (waitTime);

            FlockingRules();
        }
    }

    void FlockingRules() {
        Vector3 cohesion = Vector3.zero;
        Vector3 separation = Vector3.zero;
        Vector3 align = Vector3.zero;
        int num = 0;

        foreach (GameObject go in myManager.allFlocks) {
            if (go != this.gameObject) {
                float distance = Vector3.Distance(go.transform.position, transform.position);
                if (distance <= myManager.neighbourDistance) {
                    cohesion += go.transform.position;
                    align += go.GetComponent<Flock>().direction;
                    num++;
                    separation -= (transform.position - go.transform.position) / (distance * distance);
                }
            }
        }

        if (num > 0) {
            align /= num;
            speed = Mathf.Clamp(align.magnitude, myManager.minSpeed, myManager.maxSpeed);
            cohesion = (cohesion / num - transform.position).normalized * speed;

            direction = (cohesion + align + separation).normalized * speed;
        }
    }
}
```

### Demo

En el archivo [flocking](demos/flocking.unitypackage) encontraréis un ejemplo de implementación.

### Variantes

- El *flocking* se comporta mejos si le añadimos mucha componente aleatoria

- El uso de un líder és una variante muy utilizada. Un ejemplo seria el movimiento de grupos de pájaros en el cielo o bancos de peces en un acuario

- Otras ampliaciones pueden ser el controlar las colisiones con objetos (ejemplo: decoraciones de un acuario) o mirar que esten en un entorno controlado (ejemplo: acuario)

- Notar que en el código se está utilizando movimiento cinemático

## Referencias

- Ian Millington. *AI for Games* (3rd ed). CRC Press, 2019.

- Asset [Fantasy Bee](https://assetstore.unity.com/packages/3d/characters/animals/fantasy-bee-135487)


