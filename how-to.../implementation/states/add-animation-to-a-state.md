# Add animation to a state

A state can have its own animator controller. For more information, please read [this section](../../../fundamentals/implementation/character-state-controller.md#runtime-animator-controller).

## Creating the Animator controller

To add a custom animator controller first create one.

![](<../../../.gitbook/assets/imagen (64).png>)

Then design the animation node based graph as you want, adding all the parameters you need.

![](<../../../.gitbook/assets/imagen (65).png>)

## Assigning the animator controller

When the state is started, this animator controller will be automatically loaded into the Animator component. Assign your animator controller here:

![](<../../../.gitbook/assets/imagen (86).png>)

## Using the Animator component

Any state can access the Animator component by using the "Animator" public property from the state controller.

```csharp
Animator animator = CharacterStateController.Animator;
```

Once you got this reference you can do whatever you want, just like you would expect. 

This is a code snippet from the NormalMovement state (Demo):

```csharp
public override void PostUpdateBehaviour( float dt )
{       
    if( CharacterStateController.Animator == null )
        return;

    if( CharacterStateController.Animator.runtimeAnimatorController == null )
        return;

    if( !CharacterStateController.Animator.gameObject.activeSelf )
        return;
    
    CharacterStateController.Animator.SetBool( groundedParameter , CharacterActor.IsGrounded );
    CharacterStateController.Animator.SetBool( stableParameter , CharacterActor.IsStable );
    CharacterStateController.Animator.SetFloat( verticalSpeedParameter , CharacterActor.LocalVelocity.y );
    CharacterStateController.Animator.SetFloat( planarSpeedParameter , CharacterActor.PlanarVelocity.magnitude );
    CharacterStateController.Animator.SetFloat( horizontalAxisParameter , CharacterActions.movement.value.x );
    CharacterStateController.Animator.SetFloat( verticalAxisParameter , CharacterActions.movement.value.y );	
    CharacterStateController.Animator.SetBool( isCrouchedParameter , isCrouched );        
    
}
```

Personally, I like to set parameters after the main update function (`UpdateBehaviour`). In this case i'm using `PostUpdateBehaviour`.
