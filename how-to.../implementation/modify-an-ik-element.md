# Modify an IK element

The process of modifying an IK element \(left foot, right foot, left hand or rght hand\) is exactly the same as always was. Basically changing the _Animator_ component directly.

Since the _Animator_ could be anywhere \(within the hierarchy\), you cannot just use the message Unity provides for this \(OnAnimatorIK\), **because the state script needs to be in the same object**. In order to use this message you need to override a special virtual method \(from the CharacterState\) called **`UpdateIK`**.

For example:

```csharp
public override void UpdateIK( int layerIndex )
{
    // Set the weight
    CharacterStateController.Animator.SetIKPositionWeight( avatarIKGoal , positionWeight );
    
    // Set the position
    CharacterStateController.Animator.SetIKPosition( avatarIKGoal , position);    

}
```



