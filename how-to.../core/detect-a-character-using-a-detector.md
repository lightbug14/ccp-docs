# Detect a character using a "detector"

## What's this?

A CharacterDetector is a component that's responsible for detecting characters \(CharacterActor components\). **This component uses the OnTriggerXXX callbacks**, meaning that any character can be detected in either two ways:

1. Trigger vs Character's capsule collider
2. Non-Trigger vs Character's ground trigger \(you'll need to enable it in the inspector\)

## Why use this?

A CharacterDetector object:

* Registers all the current characters inside a dictionary, avoiding multiple GetComponent calls.
* Does its job only once, so you don't need to keep track of each individual colliders involved.
* Works automatically with 2D and 3D physics.

## Custom behaviour

It is possible to implement your own behaviour by implementing the `CharacterDetector` class. For example, the `JumpPad` and `PositionAndRotationModifier` components are essentially detectors.

There are three important methods that you can override in order to define the behaviour you want:

```csharp
protected virtual void ProcessEnterAction( CharacterActor characterActor ){}
protected virtual void ProcessStayAction( CharacterActor characterActor ){}
protected virtual void ProcessExitAction( CharacterActor characterActor ){}
```

### Example: Jump pad

```csharp
public class JumpPad : CharacterDetector
{
    public float jumpPadVelocity = 10f;

    protected override void ProcessEnterAction( CharacterActor characterActor )
    {
        if( characterActor.GroundObject != gameObject )
            return;
        
        characterActor.ForceNotGrounded();
        characterActor.Velocity += transform.up * jumpPadVelocity;
    }

    protected override void ProcessStayAction( CharacterActor characterActor )
    {
        ProcessEnterAction( characterActor );
    }
    
}
```

