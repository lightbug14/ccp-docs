# Add animation to a state

Every state has a RuntimeAnimatorController field associated. This animator controller will be automatically loaded to the main Animator component everytime the state is entered.

To add a custom animator controller first create one.

![](../../.gitbook/assets/imagen%20%2832%29.png)



Then design the animation node based graph as you want, adding all the parameters you need.

![](../../.gitbook/assets/imagen%20%2829%29.png)

## Getting/Setting parameters

It works just like you would expect, get the Animator component and get/set the parameters you want. 

I like to set parameters after the main update function \(UpdateBehaviour\). So, i used PostUpdateBehaviour just for this. 

This is from the NormalMovement state \(Demo\):

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

Obviously you can do this from anywhere.

