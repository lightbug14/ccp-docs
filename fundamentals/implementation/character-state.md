# Character state

## State behaviour

A state is a component that defines the gameplay logic. Every state presents its own behaviour, and can be implemented through its abstracts and virtual methods. The state controller will call them when they are needed, so don't worry about the execution order.

In order to define the state behaviour you'll need to override some specific methods from the _CharacterState_ component. For instance, if you want to create your own exit behaviour \(run when leaving a state\) you can do something like this:

```csharp
// YourCustomState.cs
public override void ExitBehaviour(float dt)
{
    // Your code ...
}
```

## Validation

The state machine will find all the states 



## Transitions

This is an important concept to understand. A transition is evaluated in two places: the "from state" and the "to state":

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

Sometimes the information needed to decide if a transition is successful or not is shared between two or more states, but sometimes it doesn't. Since we can't be sure that one state has the total control over one particular transition, dividing the condition test sounds like the right thing to do.

> ### Example
>
> Let's say you want to implement a transition to a _JetPack_ state.
>
> In the _**Normal**_ **state**, to activate the jet pack only a specific button press is needed. This state doesn't have any information about the _JetPack_ state whatsoever \(and it shouldn't\). For the _JetPack_ state is another story. 
>
> The _**JetPack**_ state must check if everything is ok, before allowing the transition to happen. For instance, if the character jet pack doesn't have any fuel, this should not be active. In the transition code, inside the _JetPack_ state we can make sure that the fuel is enough.

So, in order to allow a transition from a _**state A**_ **to a** _**state B**_  you'll need to implement the _**CheckExitTransition**_ **method in** _**State A**_ ****and the _**CheckEnterTransition**_ **method in** _**State B**_.

### Adding candidates to the queue

Inside _CheckExitTransition_ you would normally select a target state. The thing is, there may be more than one potential state \(candidate\) at the same time. This is why there is a queue of states.

For instance, if conditionA is valid, then the StateA is added as a candidate. If conditionB is valid, then both StateB and StateC are added as candidates.

```csharp
public override void CheckExitTransition()
{
    if( conditionA )
    {
        CharacterStateController.EnqueueTransition<StateA>();
    }
    else if( conditionB )
    {
         CharacterStateController.EnqueueTransition<StateB>();
         CharacterStateController.EnqueueTransition<StateC>();       
    }
}
    
```

### Enter transition

_CheckEnterTransition_ will be evaluated for each possible candidate. It returns a bool, basically confirming \(yes or no, true or false\) if the transition is succesful or not. 

{% hint style="info" %}
Note that the default value \(virtual method in the base class\) is **true**, that is, the transition is always successful.
{% endhint %}

