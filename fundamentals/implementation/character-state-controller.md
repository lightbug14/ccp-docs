# Character state controller

The _CharacterStateController_ is the main component of the _Implementation_. This component derives from the _CharacterActorBehaviour_, which means it defines the logic of the character.

As the name implies, this component is responsible for the control all the logic states involved. This type of component can be also referred to as a finite state machine \(or FSM\).

## Finite State Machine

This component implements a "Finite State Machine" \(FSM\). This machine is responsible for managing and executing all the valid states of the character and the transitions between them.

A simple and crude representation of the structure of a state machine is shown in the next image:

![A representation of the state machine.](../../.gitbook/assets/fsm.png)

The main loop cycle of the _CharacterStateController_ component is shown in the next figure:

![Main loop of the state controller.](../../.gitbook/assets/fsm_loop.png)

## Movement direction

The _CharacterStateController_ component include a simple property that can be used by the states to obtain a movement direction vector, based on the current input and a "reference". This direction is called _input movement reference_.

The _input movement reference_ calculation is expressed in the next block diagram:

![Input movement reference calculation.](../../.gitbook/assets/movementrefdiagram.png)

{% hint style="info" %}
This vector is just the result of super basic algebra between input data and a transform component. All the information needed to create it can be obtained from inside the state. So, it's ok if you don't want to use it for your own state logic, just know that it is there.
{% endhint %}

### Input reference

The input reference is a vector created exclusively by input actions \(AI or Human\), in this case by the _input axes_ information. By default the _input axes_ are defined as a _Vector2_ that contains the _Horizontal_ and _Vertical_ axes values.

$$ inputReference = < inputAxes.x , 0 , inputAxes.y > $$

Basically what this does is to map the input data into 3D space.

### Movement reference

A _movement reference_ is defined as a set of orthonormal vectors \(think of the typical _right, up and forward_ vectors set\).

There are three types of references available:

|  |  |
| :--- | :--- |
| World  | The reference uses the world coordinates, this means that the _right_, _up_ and _forward_ directions are equals to `Vector3.right`, `Vector3.up` and `Vector3.forward` respectively. |
| Character  | The reference uses the own character transform \(`transform.right`, `transform.up` and `transform.forward`\) to update its components. |
| External  | The reference uses an external transform to update its components. |

### Input movement reference

By multiplying the **input reference** with the **movement reference** it is possible to create sort of a mix between inputs and movement reference, hence the name. To better clarify this concept see the next example figure:

![](../../.gitbook/assets/movementref.png)

There are three cases: World, Character and external, in which the same input axes vector \(in this case the "right" action\) is applied to each one of them. The figure shows three very different results, depending on the movement reference used.

Once the _InputMovementReference_ vector has been defined, it only remains to multiply it by the speed required.

{% hint style="info" %}
The _InputMovementReference_ vector is updated before the states main loop. All the character states can have access to this vector, and perform its own calculations to determine the velocity.
{% endhint %}

## Animation

### Animator

The _Animator_ is the main animation component. The _CharacterStateController_ will search for this component from the root object \(the character\) to the last child \(recursively\). 

{% hint style="info" %}
**What happens if you decide to ignore the Animator component?**

Nothing, everything \(from the character logic perspective\) is going to work just fine. This means that, if you are not happy with the CCP approach to animation, you are free to do whatever you want.
{% endhint %}

The _Animator_ can be accessed from within the CharacterState at any time. 

```csharp
CharacterStateController.Animator.SetTrigger( myTrigger );
```

This \(in comparison with previous releases of CCP\) will give you a ton of freedom when defining all the gameplay mechanics of your character.

### Animator controller

Mecanim \(the system behind the Animator controller logic\) can be really good and intuitive for some tasks \(especially if you are not a coder\), but sometimes can be a living nightmare 🤬. In any case, it's the default animation system in Unity, so it's expected to be supported by this asset.

Due to a number of technical issues with Mecanim \(related to transitions times\), CCP uses a **multi-AnimatorControllers** approach, especifically one per state. 

This means that every time a new state is loaded into the state controller, the associated _AnimatorController_ asset is assigned \(on the fly\) to the _Animator_ component.

### Animator messages

Some of the features provided for the _Animator_ can be used only from within special Unity's messages, following an specific execution order:

* **OnAnimatorIK** is used to modify the individual **IK**.
* **OnAnimatorMove** is used to extract the **root motion** data.

The main issue here is that, in order to use these functionalities you need to add a component to the object with the _Animator_ component. The state controller takes care of this, by connecting \(via an **AnimatorLink** component\) the _Animator_ messages with the FSM \(thus, implementing those functionalities for you 😉 \).

### IK

As mentioned before, the FSM takes care of the execution order. So, in order to modify an IK in any way, you would only need to implement the UpdateIK method from the CharacterState component.

> Example:
>
>
>
> ```csharp
> public override void UpdateIK( int layerIndex )
> {     
>      // Write your IK code here...
> }
> ```

### Root Motion

Root motion is a huge topic, some love it, some hate it. 

**Wait, you don't know what root motion is?**

[https://docs.unity3d.com/Manual/RootMotion.html](https://docs.unity3d.com/Manual/RootMotion.html)

The truth is, it's just a tool. Many controllers out there are built on top of this concept, CCP on the other hand just give you the option to enable it.

Enabling root motion is super easy \(from within any state\):

```csharp
CharacterStateController.UseRootMotion = true;
```

After that the movement will be controlled by the animation motion data.

{% hint style="info" %}
If you want to see **root motion** in action, i would recommend to check the **LadderClimbing** or **LedgeHanging** states from the **Demo**.
{% endhint %}

