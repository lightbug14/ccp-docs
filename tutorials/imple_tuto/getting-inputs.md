# Getting actions

## Requirements

In order to get actions \(from a Human or the AI\) the character needs to have a _CharacterBrain_ component in it. So, make sure to add this component to the character.



By default a _CharacterState_ has a _CharacterBrain_ property, which gets the _CharacterBrain_ component asotiated with the character.

## Reading the character actions

The character actions are updated by the brain component. 

We can read the actions values anytime we want. For example, we can read if the jump button was pressed down by doing:

```csharp
bool wasPressed = CharacterBrain.CharacterAction.jump.isPressed );
```

 Another example, we can read the inputAxes value:

```csharp
Vector2 inputAxes = CharacterBrain.CharacterAction.inputAxes.axesValue;
```

{% hint style="info" %}
Notice that these actions are not necessarily Human actions. The AI will produce the same, the key difference is what is triggering those actions.

For more information please read the [Character brain](../../fundamentals/implementation/character-brain.md) section.
{% endhint %}



