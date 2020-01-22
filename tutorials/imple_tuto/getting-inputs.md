# Reading actions

## Requirements

In order to get actions \(from a Human or the AI\) the character needs to have a _CharacterBrain_ component in it. This component was added along with the _CharacterStateController,_ so you don't have to worry about it. 

Since we want to play around with the character we are creating, let's choose a **Human brain**, and then assign the default **input data asset**. It should look like this:

![](../../.gitbook/assets/imagen%20%2814%29.png)



## Reading the character actions

The character actions are updated by the brain component in the Update cycle. 

By default a _CharacterState_ has a _CharacterBrain_ property, which gets the _CharacterBrain_ component asotiated with the character. We can read the actions values anytime we want. For example, we can read if the jump button was pressed down by doing:

```csharp
bool wasPressed = CharacterBrain.CharacterAction.jump.isPressed;
```

 Or we can get the inputAxes value:

```csharp
Vector2 inputAxes = CharacterBrain.CharacterAction.inputAxes.axesValue;
```

{% hint style="info" %}
Notice that these actions are not necessarily Human actions, that is, they are not linked to input devices whatsoever. The AI can produce the same type of actions as the human, so, the state is totally agnostic of the actions source.

For more information please read the [Character brain](../../fundamentals/implementation/character-brain.md) section.
{% endhint %}



