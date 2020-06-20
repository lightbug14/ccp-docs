# Disable collisions \(Ghost character\)

Any normal rigidbody will ignore collisions \(visually\) by:

1. Making the rigidbody kinematic.
2. Disabling its collider.

The CharacterActor has these properties availables. This will make the character a "ghost" 👻 .

{% hint style="info" %}
The LadderClimbing and LedgeHanging states \(from the Demo\) use a kinematic character to prevent the body shape to collide with the geometry.
{% endhint %}

## Enabling Kinematic body

```csharp
CharacterActor.IsKinematic = true;
```

## Disabling Collider component

```csharp
CharacterActor.ColliderComponent.enabled = false;
```



