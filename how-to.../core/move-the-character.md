# Move the character

The character can be moved in three ways.

1. Changing the _**Position**._
2. Using the _**Teleport**_ function.
3. Changing the _**Velocity**._

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

## Teleport

The difference between changing the rigidbody position and using the Teleport method is that the latter triggers the **OnTeleport event**, which can be very useful in some cases \(for example to notify other objects about this action\).

{% hint style="info" %}
Teleport is used in the demo scenes in order to notify the camera to stop lerping out the movement, and change the position and rotation from one frame to the next.
{% endhint %}

## Velocity

Nothing complex here, this field is the rigidbody velocity. So, just like a normal rigidbody, the character will move from point A to B based on the velocity applied to it. If you want to know more about how velocity is handled please read the [Velocity](../../fundamentals/untitled/character-actor/velocity.md) section.

