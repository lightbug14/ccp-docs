# Transitions

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

## From StateA to StateB

So, in order to allow a transition from state A to state B we need to implement the _CheckExitTransition_ in _State A_ and the _CheckEnterTransition_ methods in _State B_.

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

## Multiple transitions per state

The principle is exactly the same as before. Here is a simple template you can use for your own states:

```csharp

public override CharacterState CheckExitTransition()
{ 
    CharacterState state = null;
    if( conditionStateA_B )
    {
        state = CharacterStateController.GetState( "StateB" );
    }
    else if( conditionStateA_C )
    {
        state = CharacterStateController.GetState( "StateC" );

    }   
    else if( conditionStateA_D )
    {
        state = CharacterStateController.GetState( "StateD" );

    }    
    // etc...     

    return state;
}
```

