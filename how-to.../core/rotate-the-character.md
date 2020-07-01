# Rotate the character

The character rotation can be defined in two steps:

1. Assigning a _**Rotation**_ value to the character \(via a Quaternion\).
2. Letting the _**vertical alignment**_ match the character upwards direction with the vertical alignment up direction.

## 3D Character

### 1. Assigning a Rotation

Same as Transform.rotation, you can set the _**Rotation**_ property using any Quaternion value you want.

```csharp
CharacterActor.Rotation = SomeQuaternion;
```

Many times you would want to change a particular known direction. For instance, it's very common to modify only the _forward direction_ of the character \(rather than calculating a quaternion value just for that\). 

The _CharacterActor_ has a _**Forward**_ public property available \(same for _Up_ and _Right_\):

```csharp
CharacterActor.Forward = LookingDirection;
```

### 2. Vertical Alignment

Most games don't actually change the character vertical direction \(upwards\) in runtime at all. Still, if you want to use a different orientation you can by using the _**vertical alignment settings**_.

{% hint style="info" %}
You don't need to actively change these settings frame by frame, the CharacterActor will align the character automatically for you. 

You can change the CharacterActor vertical alignment settings any time \(in code and/or in the inspector\).
{% endhint %}

#### Defining the up direction based on a reference \(e.g. a planet\)

You need to have a reference to your planet \(e.g. a Transform component\)

```csharp
[SerializeField]
Transform planet = null;
```

Then you need to assign that reference \(the planet\) as the _vertical alignment reference_.

```csharp
CharacterActor.VerticalAlignmentReference = planet;
```

{% hint style="info" %}
Once you assign a reference the vertical direction is controlled exclusively by the character actor.
{% endhint %}

#### Defining the up direction yourself

This has the same effect as defining the character Up property yourself. This becomes really useful when the animation changes the up direction in any way, so by defining a global _**vertical direction**_, you can be sure the character will always stay exactly as you want to.

```csharp
CharacterActor.VerticalAlignmentDirection = - gravityDirection;
```

## 2D Character

The 2D world is very different from the 3D world, especially regarding rotations. 

In order to handle rotations **it is important to separate the graphics \(3D mesh or sprite\) from the actual character**. For more information about 2D rotation please see the [Character actor](../../fundamentals/untitled/character-actor.md#rotation) section. 

You need to add a _CharacterGraphics2DRotator_ to the mesh or sprite representing the graphics.

![](../../.gitbook/assets/imagen%20%2848%29.png)

You can choose between two modes:

|  |  |
| :--- | :--- |
| Rotation | This will modify the transform rotation until _transform.forward_ matches the character _Forward_. |
| Scale | This will modify the transform localScale property based on the character _Forward_ direction \(very used with sprites\). |



