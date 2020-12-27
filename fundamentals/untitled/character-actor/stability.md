# States

This character controller state can be defined at any time as a mix between two very important properties:

* Ground state \(grounded, not grounded\).
* Stability \(stable, unstable\).

## Ground state

This property indicates if there is ground below the character, simple as that. This property alone does not influence the actor internal logic at all, that's something the stability does.

The main property associated with the ground state is called **IsGrounded**. There are much more properties associated with the current ground \(see the API reference for more info\).

## Stability

The internal logic of the character controller works differently depending on the current stability state. That is, if the character is stable it uses most of the features from the controller \(velocity projection, step up, step down, edge compensation, and so on\). If it is not, then all the features are disabled.

![](../../../.gitbook/assets/imagen%20%2857%29.png)

A character is _**stable**_ when it is grounded and the _**stable slope angle**_ \(see the API reference\) is less than or equal to the _**slope limit**_ value.

```csharp
IsStable = IsGrounded && ( stableSlopeAngle <= slopeLimit ); 
```

The stable slope angle is selected internally by the character actor based on a few conditions. 

Look at the next image, one surface is unstable \(red\) and the other is stable \(green\). The stable normal is chosen as the one coming from the stable surface. This angle should not be confused with the _slope contact angle_, which is obtained directly from the collision test.

![](../../../.gitbook/assets/contactvsstable.png)



## States

Based on what has been said before, the character actor can be:

| CharacterActorState | IsStable | IsGrounded | Description |
| :--- | :--- | :--- | :--- |
| StableGrounded | true | true | There is ground below the character and it is a stable surface. Most of the features are processed. |
| UnstableGrounded | false | true | There is ground below the character, however, it is not a stable surface. Features are bypassed. |
| NotGrounded | false | false | Same as before, however there is no ground below. |

![](../../../.gitbook/assets/imagen%20%2856%29.png)

Getting a particular state is equivalent to get the two properties separately. For example:

```csharp
//-----------------------------------------------------------------------------
// Properties

if( CharacterActor.IsGrounded && !CharacterActor.IsStable)
{
    ProcessUnstableGroundedLogic();
}

// ----------------------------------------------------------------------------
// Character actor state

if( CharacterActor.CurrentState == CharacterActorState.UnstableGrounded )
{
    ProcessUnstableGroundedLogic();
}
```



