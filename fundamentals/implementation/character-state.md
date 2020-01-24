# Character state

## State behaviour

A state is the main piece of code that the state machine executes. Every state presents its own behaviour, and can be implemented through its abstracts and virtual methods. The state controller will call them when they are needed, so don't worry about the execution order.



You need to override the method you want to define a specific behaviour. For instance, if you want to create your own exit behaviour you can do something like this:

```csharp
// YourCustomState.cs
public override void ExitBehaviour(float dt)
{
    // Your code ...
}
```

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

Well, sometimes the information needed to decide if a transition is successful or not is shared between two or more states, but sometimes it doesn't. Since we can't be sure that one state has the total control over one particular transition, dividing the condition test sounds like the right thing to do.

> ### Example
>
> Let's say you want to implement a transition to a _JetPack_ state.
>
> In the _**Normal**_ **state**, to activate the jet pack only a specific button press is needed. This state doesn't have any information about the _JetPack_ state whatsoever \(and it shouldn't\). For the _JetPack_ state is another story. 
>
> The _**JetPack**_ state must check if everything is ok, before allowing the transition to happen. For instance, if the character jet pack doesn't have any fuel, this should not be active. In the transition code, inside the _JetPack_ state we can make sure that the fuel is enough.



The best way to understand transitions is by looking at the _CharacterStateController_ script. Specifically at the _CheckForTransitions_ method:

```csharp
bool CheckForTransitions()
{ 
    CharacterState nextState = currentState.CheckExitTransition();
    if( nextState == null )
        return false;

    bool success = nextState.CheckEnterTransition( currentState );
    if( !success )
        return false;

    previousState = currentState;
    currentState = nextState;

    return true;
}
```

Something to notice about this is that the _CheckExitTransition_ is evaluated in the current state, and the _CheckEnterTransition_ is evaluated in the next state. 

So, in order to allow a transition from a _state A_ to a _state B_ we need to implement the _CheckExitTransition_ in _State A_ and the _CheckEnterTransition_ methods in _State B_.

By default these are the virtual definitions of both states \(_CharacterState.cs_\):

```csharp
public virtual CharacterState CheckExitTransition()
{
    return null;
}
 
public virtual bool CheckEnterTransition( CharacterState fromState )
{
    return true;
}
```

These are virtual methods, this means that if we don't implement them they are going to run in the base class. In other words, nothing is going to happen, no transitions at all. This is something you probably don't want, unless your character needs only one state, which is unlikely.

### Exit transition

_CheckExitTransition_ returns a target state \(_CharacterState_ type\), in this case it would be _State B._ Notice that the default value \(virtual method in the base class\) is null. This basically means that the transition is failed.

In order to get this state we need to use a character state controller method called _GetState_. For example:

```csharp
CharacterState stateB = CharacterStateController.GetState( "StateB" );
```

Now we can override the _CheckExitTransition_ method in _StateA_, for example:

```csharp
// StateA.cs
public override CharacterState CheckExitTransition()
{
    // StateA -> StateB
    if( conditionStateA )
        return CharacterStateController.GetState( "StateB" );
}
```

### Enter transition

_CheckEnterTransition_ returns a bool, this is because the target state needs to approve or not the transition at the end. Notice that the default value \(virtual method in the base class\) is true, that is, the transition is always successful.

By overriding this method we can impose another condition from within _State B_.

```csharp
// StateB.cs
public override bool CheckEnterTransition( CharacterState fromState )
{
    // Was the transition originated in StateA?
    bool fromStateA = string.Compare( fromState.Name , "StateA" );
    
    // If it was, check if the StateB conditions are true.
    if( fromStateA )
        return conditionStateB;
}
```

