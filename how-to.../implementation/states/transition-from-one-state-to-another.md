# Transition from one state to another

## One state

Let's say you want to go from _**StateA **_to _**StateB **_if _**someCondition **_is valid. For this you need to implement the CheckExitTransition in StateA (since you want to leave this state):

```csharp
// StateA.cs --------------------------        
public override bool CheckExitTransition()
{
     if( someCondition )
     {
        // Add StateB to the queue
        CharacterStateController.EnqueueTransition<StateB>(); 
     }     
}
```

If someCondition is true, then StateB will have to handle the transition. To control the result you'll need to implement the _**CheckEnterTransition **_in StateB. By default the _CheckEnterTransition _will accept the transition (returning true).

Let's say StateB can be entered only from StateA:

```csharp
// StateB.cs --------------------------        
public override bool CheckEnterTransition( CharacterState fromState )
{
     // True if fromState is StateA. False otherwise
     if( fromState == CharacterStateController.GetState<StateA>() )
          return true;
     
     return false; 
}
```

## Multiple states

Let's say you have two or more states that can be triggered by the same initial condition (_someCondition _from the previous example). Both uses the same condition, but the target state has some extra conditions as well (_CheckEnterTransition_). If you need to evaluate multiple states you can enqueue them, one after another.

```csharp
// StateA.cs --------------------------        
public override bool CheckExitTransition()
{
     if( someCondition )
     {        
        CharacterStateController.EnqueueTransition<StateB>(); 
        CharacterStateController.EnqueueTransition<StateC>();
     }
     
}
```

