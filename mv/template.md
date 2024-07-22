# Esquelet del sistema de moviment

Quan volem realitzar un moviment hem d'integrar el càlcul del moviment desitjat dins d'una plantilla que l'implementi.
A continuació teniu el codi exemple que integra la crida al moviment *Seek*.

Els paràmetres que porta són:
- *maxVelocity*: velocitat màxima de l'agent (nombre real)
- *turnSpeed*: velocitat de rotació
- *maxDistance*: distància de parada en arribar a destinació
- *freqMax*: freqüència de crida al nou càlcul desitjat

```C#
void Start()
{
    Seek();
}

void Update()
{
    // condició de parada
    if (Vector3.Distance(target.transform.position, transform.position) < maxDistance) return;

    // actualització de moviment desitjat
    freq += Time.deltaTime;
    if (freq > freqMax)
    {
        freq -= freqMax;
        Seek(); 
    }

    // actualització efectiu del moviment
    transform.rotation = Quaternion.Slerp(transform.rotation, rotation, 
                                          Time.deltaTime * turnSpeed);
    transform.position += transform.forward.normalized * maxVelocity * Time.deltaTime;
}
```

Una altra alternativa per a la crida al moviment desitjat és l'ús de corutines.
