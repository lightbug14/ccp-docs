# Collision properties

## Obstacles

Obstacles are those objects that can generate a collision contact with the character. The controller does not expose any layermask to the user, meaning that **these obstacles will be represented by the collision matrix \(layer-based collision\)**. For more information, please visit [this link \(manual\)](https://docs.unity3d.com/Manual/LayerBasedCollision.html).

{% hint style="warning" %}
In previous versions of CCP there was a **"tags and layers"** profile. This asset was used by the character actor in order to determine which objects are valid as static obstacles, dynamic obstacles, etc.

From 1.2.0 onwards **this profile is not required anymore**, the controller uses the current collision matrix.
{% endhint %}

## Collision information

A very import aspect of every character controller is the information it provides to the user. This information is really important when defining the behaviour of a character.

CCP offers this information in form of public properties. In order to access them you need a reference to the _CharacterActor_ component.

For more information about the collision information see the API reference.

## Collision events

A collision event is just a C\# delegate event that is called whenever a particular situation happened \(in this case related exclusively to collisions\). When a specific condition is met, the related event will be called by the _CharacterActor_, therefore calling any method subscribed to it.

The package include a number of collision events, if you want to look at them please refer to the API reference. All the events names start with the word "On" \(normal convention\).

{% hint style="info" %}
If you want to see all these events in action, or simply see a code example please check the `CharacterDebug.cs`script. It contains a few methods subscribed to all of the available events. You will notice that every delegate event has its own signature, this is because they are passing information along when the event is called.
{% endhint %}



