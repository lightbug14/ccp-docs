# Rotate the character

## 3D Character

### 1. Assigning a Rotation

Same as transform.rotation, you can set the _**Rotation **_property using any Quaternion value you want.

```csharp
CharacterActor.Rotation = SomeQuaternion;
```

Many times you would want to change a particular known direction instead of the whole Quaternion. For instance, it's very common to modify only the _forward direction_ of the character:

```csharp
CharacterActor.Forward = LookingDirection;
```

{% hint style="warning" %}
By default a vertical direction **constraint** is applied to the character in order to modify the up direction every frame. This means that any change to forward, right or up will be modified in orden to follow this constraint.
{% endhint %}

## 2D Character

The 2D world is very different from the 3D world, especially regarding rotations. 

In order to handle rotations **it is important to separate the graphics (3D mesh or sprite) from the actual character**. For more information about 2D rotation please see the  [Rotation](../../fundamentals/untitled/character-actor/rotation.md#2d-vs-3d) section.

CCP includes a _**CharacterGraphics2DRotator**_  component that does the job for you. Add this component to the mesh/sprite object.

![](<../../.gitbook/assets/imagen (69).png>)
