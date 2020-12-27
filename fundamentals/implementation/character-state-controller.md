# Character state controller

This component is essentially a "character-oriented" finite state machine \(FSM\) that also includes some other useful functionalities such as animation, actions and movement. It can be considered as a "high level character controller" \(since the user will be referring to this component from now on\).

## Finite State Machine

This component implements a "Finite State Machine" \(FSM\). This machine is responsible for managing and executing all the valid states of the character and the transitions between them.

A simple and crude representation of the structure of a state machine is shown in the next image:

![A representation of the state machine.](../../.gitbook/assets/fsm.png)

The main loop cycle of the _CharacterStateController_ component \(simplified version\) is shown in the next figure:

![Main loop of the state controller \(simplified\).](../../.gitbook/assets/fsm_loop.png)

## Movement direction

Input signals by their own do not translate into gameplay. Often they need to be converted into 3D world space \(a vector\) in order to be processed or sent to another component. For instance, if we move a stick, or use the WASD keys, we want to convert that into a velocity value. This is what the input movement reference does.

The input movement reference is just the combination of two concepts, **input reference** and **movement reference**.

![Input movement reference calculation.](../../.gitbook/assets/movementrefdiagram.png)

{% hint style="info" %}
This vector is just the result of super basic algebra between input data and a transform component. All the information needed to create it can be obtained from inside the state. So, **it's ok if you don't want to use it for your own state logic**, just know that it is there.
{% endhint %}

### Input reference

The input reference is a vector created exclusively by input actions \(AI or Human\), in this case by the _input axes_ information. By default the _input axes_ are defined as a _Vector2_ that contains the _Horizontal_ and _Vertical_ axes values.

$$ inputReference = < inputAxes.x , 0 , inputAxes.y > $$

Basically what this does is to **map the input data into 3D space**.

### Movement reference

A _movement reference_ is defined as a set of orthonormal vectors \(think of the typical _right, up and forward_ vectors set\) that are built based on a given reference. There are three types of references available:

| Reference Type | Description |
| :--- | :--- |
| World  | The reference uses the world coordinates, this means that the _right_, _up_ and _forward_ directions are equals to `Vector3.right`, `Vector3.up` and `Vector3.forward` respectively. |
| Character  | The reference uses the own character transform \(`transform.right`, `transform.up` and `transform.forward`\) to update its components. |
| External  | The reference uses an external transform to update its components. |

### Input movement reference

By multiplying the **input reference** with the **movement reference** it is possible to create sort of a mix between inputs and movement, hence the name. 

To better clarify this concept see the figure. There are three cases: World, Character and external, in which **the same input axes vector \(in this case the "right" action\) is applied to each one of them**. The figure shows three very different results, depending on the movement reference used:

![](../../.gitbook/assets/movementref.png)

## Animation

### Animator

The _CharacterStateController_ automatically searches for the Animator component at the beginning. You can access this component by using a public property. For example:

```csharp
CharacterStateController.Animator.SetTrigger( myTrigger );
```

### Animator controller

Mecanim \(the system behind the Animator controller logic\) can be really good and intuitive for some tasks \(especially if you are not a coder\), but sometimes can be a living nightmare 🤬. In any case, it's the default animation system in Unity, so it's expected to be supported by this asset.

Due to a number of technical issues with Mecanim \(related to transitions times\), CCP was uses a **multi-AnimatorControllers** approach, specifically one per state. This means that every time a new state is loaded into the state controller, the associated _AnimatorController_ asset can be re-assigned \(on the fly\) to the _Animator_ component.

In order to do that the target state must enable the "override animator controller" setting in the inspector.

![](../../.gitbook/assets/imagen%20%2858%29.png)

### Animator messages

Some of the features provided by the _Animator_ can be used only by calling some special Unity's messages. These messages often are:

* **OnAnimatorIK** is used to modify the individual **IK element**.
* **OnAnimatorMove** is used to extract the **root motion** data.

The main issue here is that, in order to use these functionalities you need to add a component to the object with the _Animator_ component. The state controller takes care of this, by connecting \(via an **AnimatorLink** component\) the _Animator_ messages with the FSM \(thus, implementing those functionalities for you 😉 \).

{% hint style="info" %}
There is no need to add this **AnimatorLink**, the CharacterStateController does this for you.
{% endhint %}



