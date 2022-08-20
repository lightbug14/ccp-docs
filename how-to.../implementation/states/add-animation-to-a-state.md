# Handle animation

## Creating the Animator controller

To add a custom animator controller first create one.

![](<../../../.gitbook/assets/imagen (64).png>)

Next, design the animation node based graph as you want.

![](<../../../.gitbook/assets/imagen (65).png>)

## Overriding the current animator controller

Any state has the ability to override the current runtime controller (Animator).&#x20;

When the FSM transitions to a particular, if the runtime animator controller field is not null, the FSM will load this controller as THE Animator runtime controller.&#x20;

![](<../../../.gitbook/assets/imagen (86).png>)

## Using the Animator component

Any state can access the Animator component by using the "Animator" public property from CharacterActor.

```csharp
Animator animator = CharacterActor.Animator;
```

Once you got this reference you can do whatever you want. Here is a code snippet taken from the NormalMovement state (Demo):

```csharp
public override void PostUpdateBehaviour( float dt )
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
It is recommended to set certain parameters during the PreCharacterSimulation and/or PostCharacterSimulation methods.

The reason for this is because the actor might modify the body velocity along the way, so the values won't be updated by the time the frame is rendered.
{% endhint %}

