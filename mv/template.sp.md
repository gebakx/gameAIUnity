# Esqueleto del sistema de movimiento

Cuando queremos realizar un movimiento tenemos que integrar el cálculo del movimiento deseado dentre de una plantilla que lo implemente. A continuación tenéis el código ejemplo que integra la llamada al movimiento *Seek*.

Los parámetros que utiliza son:
- *maxVelocity*: velocidad máxima del agente (número real)
- *turnSpeed*: velocidad de rotación
- *maxDistance*: distancia de parada al llegar a destino
- *freqMax*: frecuencia de llamada al nuevo cálculo deseado

```C#
void Start()
{
    Seek();
}

void Update()
{
    // condición de parada
    if (Vector3.Distance(target.transform.position, transform.position) < maxDistance) return;

    // actualización de movimiento deseado
    freq += Time.deltaTime;
    if (freq > freqMax)
    {
        freq -= freqMax;
        Seek(); 
    }

    // actualización efectivo del movimiento
    transform.rotation = Quaternion.Slerp(transform.rotation, rotation, 
                                          Time.deltaTime * turnSpeed);
    transform.position += transform.forward.normalized * maxVelocity * Time.deltaTime;
}
```

Otra alternariva para la llamada al movimiento deseado es el uso de corutinas.

