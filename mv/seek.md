# Seek i Flee

En el moviment *seek* calculem la direcció de l'agent cap a la seva destinació. El *flee* serà el seu moviment contrari.

|![](figures/seek.png)|
|:--:| 
| *Font: (Reynolds, 1999)* |

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

### Demo

A l'arxiu [seekKin](demos/seekKin.unitypackage) trobareu un exemple d'implementació.
L'agent involucrat es diu *robber* i trobareu una sèrie de paràmetres:

![](figures/robberKin.png)

El paràmetre *vehicle* serveix per indicar si volem que faci el gir i el moviment d'avançar a la vegada. En cas contrari, primer gira i després avança.

## Moviments d'*Steering*

Els moviments cinemàtics tenen l'inconvenient de que no són gaire realistes. Els moviments d'*steering* afegeixen acceleració als anteriors per solucionar-ho.

A continuació teniu el codi que necessitem:

```C#
turnSpeed += turnAcceleration * Time.deltaTime;
turnSpeed = Mathf.Min(turnSpeed, maxTurnSpeed);
movSpeed += acceleration * Time.deltaTime;
movSpeed = Mathf.Min(movSpeed, maxSpeed);
```

### Arriving

Hem d'evitar que un agent en moviment arribi a la seva destinació. En cas contrari, pot començar a realitzar moviments cíclics al voltant de la destinació. Dos comportaments de parada són:

- **Stopping distance**: l'agent s'atura en arribar a una certa distància de l'objectiu

- **Steering Arrive**: l'agent comença frenar en arribar a una distància de parada

$$speed=\frac{maxSpeed\times distance}{slowRadius}$$

### Demo

A l'arxiu [seekSteering](demos/seekSteering.unitypackage) trobareu un exemple d'implementació.
L'agent involucrat es diu *robber* i trobareu una sèrie de paràmetres:

![](figures/robberSteering.png)

## Referències

- Craig W. Reynolds. [Steering Behaviors For autonomous Characters](http://www.red3d.com/cwr/papers/1999/gdc99steer.pdf). Proceedings of the Game Developers Conference (GDC), 1999.

- Asset [Easy Primitive People](https://assetstore.unity.com/packages/3d/characters/easy-primitive-people-161846)

- Asset [Five Seamless Tileable Ground Textures](https://assetstore.unity.com/packages/2d/textures-materials/floors/five-seamless-tileable-ground-textures-57060)

- Asset [LowPoly Trees and Rocks](https://assetstore.unity.com/packages/3d/vegetation/lowpoly-trees-and-rocks-88376)



