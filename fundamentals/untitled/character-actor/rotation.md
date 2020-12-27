# Rotation

The rotation of the character is handled in a very specific way, depending on the physics involved, and the constraints specified.

## Pivot

As mentioned in the [Character body](../characterbody.md) section, the pivot of the character is the actual rotation pivot.

## 2D vs 3D

For a 3D character, the rotation value can be anything, you are free to set the value you want. The returned value \(a Quaternion\) will represent the character rotation.

On the other hand, for a 2D character, **the forward direction** **needs to be facing towards Vector3.forward or Vector3.back \(= - Vector3.forward\)**. Otherwise, the collider 2D area will be less than the original intended area.

{% hint style="info" %}
You can test this by yourself, create a CapsuleCollider2D and rotate it along the y axis.
{% endhint %}

![](../../../.gitbook/assets/imagen%20%2864%29.png)

This is of course unacceptable ☹. With CCP you don't need to worry about this issue, you can assign the rotation value \(Quaternion\) that you want, and the _CharacterActor_ component will be smart enough to keep track of the rotation value. The result will affect a virtual \(or "fake"\) forward direction that you can access using the property **Forward**.

{% hint style="warning" %}
Now that we can't rotate the character \(the root\) we need to represent somehow that for the graphics. This is where the **CharacterGraphics2DRotator** component comes handy.
{% endhint %}

## Orthonormal directions

A much more intuitive way of working with rotations is not using rotation at all, instead, we can use orthonormal directions \(the Transform component use them as well\). The character has three directions available:

* Forward
* Right
* Up

By modifying one of them the entire rotation structure will be modified as well.

## Constraints

This feature \(if enabled\) allows you to modify the character up direction based on some predefined value.

![](../../../.gitbook/assets/imagen%20%2855%29.png)

Even though the character is freezing its own rotation by default \(rigidbody constraint\), there is still possible to modify the rotation without the user's consent. For instance, a root motion clip might apply some rotation value to the character if the animation is not properly created/configured. By using a constraint we are 100% sure this will never happen.

