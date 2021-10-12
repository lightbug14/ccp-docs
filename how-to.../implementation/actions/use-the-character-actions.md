# Use the character actions

## Getting the action struct

The CharacterActions struct can be obtained from the CharacterBrain component. 

```csharp
CharacterActions actions = characterBrain.CharacterActions;
```

If you are working from inside a state you can call the CharacterActions property (not the class):

```csharp
CharacterActions actions = CharacterActions;
```

## Reading the actions

Just access the public member you want from the CharacterAction struct.

```csharp
// Bool action ---> E.g. Jump (button)
bool jumpValue = CharacterActions.jump.value;

// Float action ---> E.g. Horizontal (AD keys)
float horizontalValue = CharacterActions.horizontal.value;

// Vector2 action ---> E.g. Movement (WASD keys)
Vector2 movementValue = CharacterActions.movement.value;
```

### Bool actions

Float and Vector2 actions are most of the time related to analog values. Their value is what's important. On the other hand, with bool actions it is often more important the "phase" of the action.

For a button, the phases are started (similar to the classic "GetButtonDown") and canceled ("GetButtonUp").

```csharp
// Bool action ---> E.g. a jump button 
bool wasJumpPressed = CharacterActions.jump.Started;
bool wasJumpReleased = CharacterActions.jump.Canceled;
```

### Vector2 actions

If you are using the old InputManager (the default input system used by the demo scenes) you can create a Vector2 action from the project settings, even though these type of actions are not supported.

The Vector2 action is just a mix between two float actions. 

{% hint style="info" %}
To define a Vector2 action you need to create two input axis:

1. The Name of the action + space + "X"
2. The Name of the action + space + "Y"
{% endhint %}

For instance, the "movement" action is defined like this:

![](<../../../.gitbook/assets/imagen (62).png>)

