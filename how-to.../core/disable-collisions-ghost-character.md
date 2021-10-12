# Disable collisions between A and B

Any regular rigidbody A will ignore collisions (visually) with any collider B if:

* A and/or B are kinematic rigidbodies.
* A and/or B colliders are disabled.
* A and B ignore each other (collision matrix).

## Setting the rigidbody to kinematic

```csharp
CharacterActor.IsKinematic = true;

// Or
CharacterActor.RigidbodyComponent.IsKinematic = true;
```

## Disabling the collider component

```csharp
CharacterActor.ColliderComponent.enabled = false;
```

## Configuring the collision matrix

Another way to make a ghost character is to change the collision matrix from the Physics (Physics2D). As mentioned in [this section](../../fundamentals/untitled/character-actor/collision-properties.md#obstacles), thecharacter actor uses the collision matrix provided by the physics engine. 

