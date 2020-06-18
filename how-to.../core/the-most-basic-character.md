# Create a basic character

**GOAL:** Add a functional character to the scene. This character will not move or do anything , but at least it will be the starting point for you to do anything with it.

{% hint style="warning" %}
I will assume you have already set the project properly. If not, please go to the [setting up the project](../../package/setting-up-the-project.md) section first.
{% endhint %}

## Creating the character

### 1. The character Gameobject

Add a new GameObject in the scene and give it a name. Make sure the local scale \(as mentioned in the fundamentals section\) is$$<1,1,1>$$.

{% hint style="info" %}
There is no need to add a **Collider** and/or **Rigidbody** to the object. The CharacterBody and CharacterActor will do this for you.
{% endhint %}

### 2. Add the CharacterBody

Add a character body component to the character:

![](../../.gitbook/assets/imagen%20%286%29.png)

### 3. Add the CharacterActor

Next, add a CharacterActor component.

{% hint style="info" %}
By adding a _CharacterActor_ component a _CharacterBody_ component will be added automatically if there is not one yet. This is because the _CharacterActor_ requires a _CharacterBody_ component.
{% endhint %}

![](../../.gitbook/assets/imagen%20%283%29.png)

Make sure to add a **TagsAndLayers** profile to the _CharacterActor_. This profile is used by the component to filter collisions and compare tags.

You can find one of these in the Demo.

![](../../.gitbook/assets/imagen%20%2812%29.png)

{% hint style="success" %}
Done! 😃 This is the more boring invisble character you can create, It does absolutely nothing. In order to give it some life you need to implement some logic \(a "behaviour"\).
{% endhint %}

## Using a prefab

Another way is to simply add a prefab to the scene. Use the basic "Blank Character" \(invisible\) or the "Capsule Blank Character" \(using a Capsule 3D Mesh\).

![&quot;Capsule Blank Character&quot; pregab](../../.gitbook/assets/imagen%20%2825%29.png)

## Future

If you are interested in creating your own input system, state controller \(or anything else you want, on top of the Core\) this is where you should stop reading. The character is now a very special Rigidbody with very special rules \(as explained in the [Core](../../fundamentals/untitled/) section\).

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





## 











