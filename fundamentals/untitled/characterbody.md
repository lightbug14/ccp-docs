# Character body

## Properties

### Foot position \(pivot\)

The foot position is considered as the origin, a point of reference for everything \(pivot\). As is normally for character controllers, the origin is assumed to be the bottom most point of the character body. In this case is the bottom point of the capsule.

### Orientation

The character is modeled as an upright capsule.

![](../../.gitbook/assets/capsuleupright.png)

### Size

Since this is a capsule-based character we need only to define the radius and the height to fully describe the size of the character. The _CharacterActor_ will consider the character dimensions as:



$$
Width = 2 \times Collider.Radius
$$

$$
Height = Collider.Height
$$



The Width and Height values are represented with the _body size_ \(a _Vector2_\).

![](../../.gitbook/assets/capsulebodydimensions.png)

{% hint style="info" %}
In play mode the collider bottom offset will be automatically adjusted, depending on the current state \(state vs unstable\).
{% endhint %}

### Scale

Even though the collider will be scaled just fine, the internal "physics size'' \(responsible for physics queries\) will not. So, **it is NOT recommend to scale the character using the** _**Transform**_ **component**.

{% hint style="warning" %}
The character _localScale_ should always be $$< 1, 1 , 1 >$$.
{% endhint %}

#### What if i want to scale my character?

Well, in that case you should scale the graphics object, not the character itself \(root object\). After that, the body size should be modified to fit the graphics.

