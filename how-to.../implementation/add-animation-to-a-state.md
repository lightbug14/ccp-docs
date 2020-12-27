# Add animation to a state

## Creating the Animator controller

Every state has a RuntimeAnimatorController field associated. This animator controller will be automatically loaded to the main Animator component everytime the state is entered.

To add a custom animator controller first create one.

![](../../.gitbook/assets/imagen%20%2832%29.png)

Then design the animation node based graph as you want, adding all the parameters you need.

![](../../.gitbook/assets/imagen%20%2829%29.png)

## Assigning the animator controller

The state animator controller \(mentioned before in the [Create a state](create-a-state.md) section\) will be automatically loaded to the Animator component, once the state is started. Assign your animator controller there.

![](../../.gitbook/assets/imagen%20%2858%29.png)

## Using the Animator component

Any state can access the Animator component by using the "Animator" public property from the state controller.

```csharp
Animator animator = CharacterStateController.Animator;
```

Once you got this reference you can do whatever you want, just like you would expect. 

This is a code snippet from the NormalMovement state \(Demo\):

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

Personally, I like to set parameters after the main update function \(UpdateBehaviour\). So, i use _PostUpdateBehaviour_ just for this \(most of the time\).

