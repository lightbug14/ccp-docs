# Add logic to your character

The logic of the character is define by the CharacterActorBehaviour. 

This behaviour will always be executed just before the CharacterActor update.

To create your own behaviour just create a class derived from CharacterActorBehaviour, as shown in this example:

```csharp
using UnityEngine;
using Lightbug.CharacterControllerPro.Core;

public class ExampleCharacterActorBehaviour : CharacterActorBehaviour
{
    public override void UpdateBehaviour( float dt )
    {
        // Update the CharacterActor values here...
    }
}

```

{% hint style="info" %}
The advantage of doing this is that all the logic es executed in specific moments \(defined by the _CharacterActor_\). Also most of the relevant components are protected members of the class, so you don't need to get extra references from the outside.
{% endhint %}

{% hint style="info" %}
The CharacterStateController is a CharacterActorBehaviour
{% endhint %}

