# Handle animation

## Creating the Animator controller

To add a custom animator controller first create one.

![](<../../../.gitbook/assets/imagen (64).png>)

Next, design the animation node based graph as you want.

![](<../../../.gitbook/assets/imagen (65).png>)

## Assigning a runtime controller

There are three possible approaches:

1. You can assign one big runtime controller to the Animator component directly and ignore individual controllers (states).&#x20;
2. You can use individual runtime controllers from each state. For more information please read [this](../../../fundamentals/implementation/character-state-controller.md#animation).
3. You can use a mix between 1 and 2.

## Using the Animator component

Any state can access the Animator component by using the "Animator" public property from CharacterActor.

```csharp
Animator animator = CharacterActor.Animator;
```

Once you got this reference you can do whatever you want. Here is a code snippet taken from the NormalMovement state (Demo):

```csharp
public override void PostUpdateBehaviour(float dt)
{       
    if (!CharacterActor.IsAnimatorValid())
        return;
    
    CharacterActor.Animator.SetBool(groundedParameter , CharacterActor.IsGrounded);
    CharacterActor.Animator.SetBool(stableParameter , CharacterActor.IsStable);
    CharacterActor.Animator.SetFloat(verticalSpeedParameter , CharacterActor.LocalVelocity.y);
    CharacterActor.Animator.SetFloat(planarSpeedParameter , CharacterActor.PlanarVelocity.magnitude);
    CharacterActor.Animator.SetFloat(horizontalAxisParameter , CharacterActions.movement.value.x);
    CharacterActor.Animator.SetFloat(verticalAxisParameter , CharacterActions.movement.value.y);	
    CharacterActor.Animator.SetBool(isCrouchedParameter , isCrouched);        
    
}
```

{% hint style="info" %}
It is recommended to set certain parameters during the `PreCharacterSimulation` and/or `PostCharacterSimulation` methods.

The reason for this is because the actor might modify the body velocity along the way, so the values won't be updated by the time the frame is rendered.
{% endhint %}

