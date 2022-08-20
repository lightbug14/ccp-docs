# Rotate the character

## 3D Characters

### Assigning a Rotation

Same as transform.rotation, you can set the _**Rotation**_ property directly using any Quaternion value you want.

```csharp
CharacterActor.Rotation = SomeQuaternion;
```

### Setting a direction property

Sometimes it is preferred to make a particular direction to point towards another one. In that case, you could modify any of the actor directions (properties):

```csharp
CharacterActor.Forward = LookingDirection;
```

{% hint style="warning" %}
By setting any of the direction properties there is no guarantee that the rotation applied will be the one you want. For instance, multiplying Forward by -1 does not mean a 180° Yaw rotation will be applied.

For more precise control over the rotation process, please use `RotateYaw`, `RotatePitch` and/or `RotateRoll`.
{% endhint %}

### Using the actor public methods

If you want get a more precise result, you can use `RotateYaw`, `RotatePitch` and/or `RotateRoll`. These are all simple implementations based on `Quaternion.AngleAxis`.

<pre class="language-csharp"><code class="lang-csharp"><strong>// Rotate using the "up" direction as the axis until forward = targetVector
</strong><strong>CharacterActor.RotateYaw(targetVector);
</strong><strong>
</strong><strong>// Rotate a given amount (degrees) using the "up" direction as the axis
</strong><strong>CharacterActor.RotateYaw(amount);
</strong><strong>
</strong>// Rotate around a pivot a given amount (degrees) using the "up" direction as the axis
CharacterActor.RotateYaw(amount, pivot);
<strong>
</strong>// Rotate a given amount (degrees) using the "right" direction as the axis
<strong>CharacterActor.RotatePitch(amount);
</strong><strong>
</strong>// Rotate a given amount (degrees) using the "forward" direction as the axis
<strong>CharacterActor.RotateYaw(amount);</strong></code></pre>

## 2D Characters

The 2D world is very different from the 3D world, especially regarding rotations. However, **all of the principles and functions mentioned above apply here as well.**&#x20;

The big difference between 2D and 3D is that `transform.forward` must be either `Vector3.forward` or `Vector3.back`. Otherwise, the collider size will get reduced.

![](<../../.gitbook/assets/imagen (84).png>)

{% hint style="info" %}
The `Forward` direction (actor property) is directly represented by `transform.right`.
{% endhint %}
