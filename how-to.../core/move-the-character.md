# Move the character

The character can be moved in two ways.

1. Changing its _**Position**._
2. Using the _**Teleport**_ function.
3. Changing its _**Velocity**._

```csharp
// Position
CharacterActor.Position = someVector3;

// Teleport
CharacterActor.Teleport( someVector3 );

// Velocity
CharacterActor.Velocity = someVector3;

```

## Position

The first two methods moves the character from point A to B, without considering collision detection. Just like you would expect when changing a Rigidbody position.

The difference between Position and Teleport is that the latter triggers the OnTeleport event, which can be very useful in some cases.

{% hint style="info" %}
Teleport is used in the 3D Scene \(from the Demo\) in order to notify the camera to stop smoothing out the movement, and change the position and rotation from one frame to the next.
{% endhint %}

## Velocity

Nothing complex here, this field is the rigidbody velocity. So, just like a normal rigidbody, the character will move from point A to B based on the velocity applied to it.

Depending on the grounded state \(see the [Character actor](../../fundamentals/untitled/character-actor.md#velocity) section\) this velocity will be maintained o projected onto the ground.

