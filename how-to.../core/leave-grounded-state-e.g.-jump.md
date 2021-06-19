# Leave grounded state \(e.g. jump\)

If the character is stable, any vertical velocity applied to the character will be eventually ignored by the actor. The only way to leave grounded state is by forcing this state via the CharacterActor API, this is possible thanks to the **ForceNotGrounded** method.

## Jump example

If you want your character to jump, then you need to force the "not grounded" state first. Here is a simple example:

```csharp
CharacterActor.ForceNotGrounded();
CharacterActor.VerticalVelocity = CharacterActor.Up * 10f;
```

