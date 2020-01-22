# Moving the character

## 1. Defining the velocity

In order to move the character we need to set the _linear velocity_ field \(CharacterActor\). First we need to create a speed serialized field.

```csharp
[SerializeField]
float speed = 5f;
```

Then we are going to combine this speed field with the input axes to create a velocity vector.

```csharp
void UpdateCharacter()
{        
    Vector3 velocity = speed * inputAxes;
}
```

## 2. Setting the linear velocity

And finally we set the linear velocity by using the `SetLinearVelocity` method.

```csharp
void UpdateCharacter()
{        
    Vector3 velocity = speed * inputAxes;
    characterActor.SetLinearVelocity( velocity );
}
```

{% hint style="warning" %}
The linear velocity is global, this means we could transform the coordinates before sending them to the character actor.
{% endhint %}

## 3. Not grounded movement

As you can see, we have a character that can move forwards and backwards, left and right, up and down. Something very important to notice is that the character is able to move around freely, until it hits the ground. Once this happens it is impossible for the character to move upwards! This is because it has entered the _grounded_ state \(internally things work differenty, no matter the linear velocity value you are using\).

One cool thing you can do is to completely ignore this _grounded_ state by setting the _alwaysNotGrounded_ toggle in the _CharacterActor_ inspector.

In the next section we are going to overcome this by implement gravity and jump.

