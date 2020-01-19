# Character state

## State behaviour

A state is the main piece of code that the state machine executes. Every state presents its own behaviour, and can be implemented through its abstracts and virtual methods. The state controller will call them when they are needed, so don't worry about the execution order \(see the API reference to know what methods are available\).

You need to override the method you want to define a specific behaviour. For instance, if you want to create your own exit behaviour you can do something like this:

```csharp
// YourCustomState.cs
public override void ExitBehaviour(float dt)
{
    // Your code ...
}
```

## State creation

If you want to create your own states you can do so manually by creating your own class. It's mandatory that it derives from the \textit{CharacterState} class.

Another way is by simply right clicking on the project view \(choose the path of your choice\), then go to \textit{\`\`Create/Character Controller Pro/Implementation/Character State''}. This will create a template with the basics already included.

### Transitions

This is an important concept to understand. A transition is evaluated in two places, in the "from state" and the "to state":

|  |  |
| :--- | :--- |
| From state | State where the transition originates. |
| To state | State where the transition ends. |

These transitions are called Exit transition and Enter transition.

|  |  |
| :--- | :--- |
| Exit transition | This is the part of the transition that is evaluated first, when trying to exit the current state \(hence its name\). |
| Enter transition | This is the part of the transition that is evaluated secondly, when trying to enter the next state \(hence its name\). |

#### Why do transitions using this approach? 

Well, sometimes the information needed to decide if a transition is successful or not is shared between two or more states, but sometimes it doesn't. Since we can't be sure that one state has the total control over one particular transition, dividing the condition test sounds like the right thing to do.

> ### Example
>
> Let's say you want to implement a transition to a _JetPack_ state.
>
> In the _**Normal**_ **state**, to activate the jet pack only a specific button press is needed. This state doesn't have any information about the _JetPack_ state whatsoever \(and it shouldn't\). For the _JetPack_ state is another story. 
>
> The _**JetPack**_ state must check if everything is ok, before allowing the transition to happen. For instance, if the character jet pack doesn't have any fuel, this should not be active. In the transition code, inside the _JetPack_ state we can make sure that the fuel is enough.











