# Modify an IK element

The process of modifying an IK element \(left foot, right foot, left hand or rght hand\) is exactly the same as always was. Basically changing the _Animator_ component directly. The problem is not the How but the **when**.

Since the _Animator_ could be anywhere \(within the hierarchy\), you cannot just use the message Unity provides for this \(OnAnimatorIK\), because the script needs to be in the same object. In order to use this message you need to override a special virtual method \(from the CharacterState\) called _**UpdateIK.**_

```csharp
public override void UpdateIK( int layerIndex )
{
    // Set the weight
    CharacterStateController.Animator.SetIKPositionWeight( avatarIKGoal , positionWeight );
    
    // Set the position
    CharacterStateController.Animator.SetIKPosition( avatarIKGoal , position);    

}
```



