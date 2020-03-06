# Moving the character

## 1. Defining the velocity

In order to move the character we need to set the _input velocity_ field \(CharacterActor\). One cool trick I always do is to separate "the" velocity into multiple velocities \(this will give much more control\).

Let's begin with the _planarVelocity_. Basically this velocity will be projected onto the plane formed by the local up direction \(normal\).

So, let's define a speed field and a private velocity vector.

```csharp
[SerializeField]
float speed = 5f;

Vector3 planarVelocity = default( Vector3 );
```

Then we are going to combine this speed field with the input axes to create a velocity vector.

```csharp
void PlanarMovement()
{
    // Create a 3D vector based on the world forward direction.
    Vector3 inputAxes = forwardAxis * Vector3.forward;
    
    // Normalize the vector!
    inputAxes.Normalize();
        
    // Set the velocity
    planarVelocity = speed * inputAxes;    
    
}
```

FInally we need to set the input velocity:

```csharp
void UpdateCharacter()
{        
    PlanarMovement();    
    
    Vector3 velocity = planarVelocity;
    
    characterActor.SetInputVelocity( velocity );
}


```

{% hint style="warning" %}
The linear velocity is global, this means we could transform the coordinates before sending them to the character actor.
{% endhint %}

{% hint style="success" %}
After doing this the character should be able to move forwards and backwards.
{% endhint %}

## 2. Not grounded movement

Still, the character is always "not grounded". This is because internally the grounded state is activated only if the character has a negative vertical velocity \(along the local up axis or `transform.up`\). In this case the velocity is perpendicular to this direction, or in other words, this direction is the normal of the character "movement plane".

In any case, we can't go to the grounded state. In the next section we are going to overcome this by implement gravity.

