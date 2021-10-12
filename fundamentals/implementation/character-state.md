# Character state

A state is a component that defines the gameplay logic associated with the CharacterActor component. 

## State vs Monobehaviour

States work in the same way monobehaviours work:

1. They process some task over and over again in a frame by frame basis (the behaviour).
2. They are updated by a controller of some kind (the state controller).

The big advantage of putting code inside a state, rather than using a monobehaviour,  is:

1. The controller communicates better between other states, allowing you to create transitions between them.
2. Since they are part of a FSM, only one of them will be running at a time.
3. The controller is designed with a few components in mind (other states, animator, actions, character actor, etc.).

## State behaviour

Every state presents its own behaviour, and can be implemented through its abstracts and virtual methods. In order to define the state behaviour you'll need to override some specific methods from the _CharacterState_ component. For instance, if you want to create your own "exit behaviour" (executed when leaving a state) you can do something like this:

```csharp
// YourCustomState.cs
public override void ExitBehaviour(float dt)
{
    // Your code ...
}
```

## Transitions

This is an important concept to understand. A transition is evaluated in two places: the "from state" and the "to state":

|            |                                        |
| ---------- | -------------------------------------- |
| From state | State where the transition originates. |
| To state   | State where the transition ends.       |

These transitions are called Exit transition and Enter transition.

|                  |                                                                                                                      |
| ---------------- | -------------------------------------------------------------------------------------------------------------------- |
| Exit transition  | This is the part of the transition that is evaluated first, when trying to exit the current state (hence its name).  |
| Enter transition | This is the part of the transition that is evaluated secondly, when trying to enter the next state (hence its name). |

#### Why do transitions use this approach? 

Sometimes the information required to accept a transition is shared between two or more states. Since we can't be sure that one state has the total control over one particular transition, dividing the condition across states seems logical.

> ### Example
>
> Let's say you want to implement a transition to a _JetPack_ state.
>
> In the _**Normal**_** state**, to activate the jet pack only a specific button press is needed. This state doesn't have any information about the _JetPack_ state whatsoever (and it shouldn't). For the _JetPack_ state is another story. 
>
> The _**JetPack**_ state must check if everything is ok, before allowing the transition to happen. For instance, if the character jet pack doesn't have any fuel, this should not be active. In the transition code, inside the _JetPack_ state we can make sure of that before accepting the transition.

### Adding candidates to the queue

Inside_ CheckExitTransition_ you would normally select a target state. The thing is, there may be more than one potential state (candidate) at the same time. This is why there is a queue of states.

#### Example:

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

_CheckEnterTransition_ will be evaluated for each possible candidate. It returns a bool variable, basically confirming (yes or no, true or false) if the transition was succesful or not. 

#### Example:

Only the _validState _state will be accepted.

```csharp
public override bool CheckEnterTransition( CharacterState fromState )
{
    if( fromState == validState )
        return true;
    
    return false;
}
    
```

{% hint style="info" %}
Note that the default value (virtual method in the base class) is **true**, that is, the transition is always successful.
{% endhint %}
