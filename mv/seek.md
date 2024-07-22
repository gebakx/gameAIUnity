# Seek i Flee

En el moviment *seek* calculem la direcció de l'agent cap a la seva destinació. El *flee* serà el seu moviment contrari.

![](figures/seek.png)

Font: (Reynolds, 1999)

## Moviment cinemàtic

**Entrada**:

- Agent (posició i orientació)

- Target (posició)

- VelocitatMàxima, rotacióMàxima 

**Sortida**:

- Velocitat i angle 

### Procés

**Direcció desitjada**: vector posició target - posició de l'agent 
$$d=(t_x-r_x, 0, t_z-r_z)$$

```C#
// Seek
Vector3 direction = target.transform.position - transform.position;
direction.y = 0f;    // (x, z): position in the floor
// Flee
Vector3 direction = transform.position - target.transform.position;
```

**Velocitat**: vector direcció amb magnitut *maxVelocity*
$$\vert d\vert=\sqrt{d_x^2+d_z^2};v=\frac{d}{\vert d\vert}maxVelocity$$

```C#
Vector3 movement = direction.normalized * maxVelocity;
```

**Rotació desitjada**:

```C#
float angle = Mathf.Rad2Deg * Mathf.Atan2(movement.x, movement.z);
Quaternion rotation = Quaternion.AngleAxis(angle, Vector3.up);  // up = y
```








