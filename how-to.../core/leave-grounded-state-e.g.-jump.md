# Leave grounded state \(e.g. jump\)

If the character is stable, any vertical velocity applied to it will be eventually ignored by the CharacterActor component. **The only way to leave grounded state is by forcing this state via the CharacterActor API**, this can be done thanks to the **ForceNotGrounded** method.

{% hint style="info" %}
You can do the opposite, that is, go from "not grounded" to "grounded" by calling **ForceGrounded**.
{% endhint %}

## Jump example

If you want your character to jump, then you need to force the "not grounded" state first. Here is a simple example:

```csharp
CharacterActor.ForceNotGrounded();
CharacterActor.VerticalVelocity = CharacterActor.Up * 10f;
```

