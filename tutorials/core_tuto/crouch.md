# Crouch

In order to crouch we need to change the character size. So, let's look at the `SetTargetBodySize` method. This method takes a _Vector2_ argument, that is, width = x and height = y \(we are only interested in the y component\).

{% hint style="info" %}
The size we are going to set is the **target size**. We are not setting the height directly, that job is done by the character actor internally. You can modify the transition speed.
{% endhint %}

First thing we need to do is to save the initial size. The size property is from the _CharacterBody_ component. Although we don't have a reference to that component, but we can get it from the character actor.

```csharp
characterActor.CharacterBody.BodySize;
```

 We can do this in awake:

```csharp
Vector2 initialBodySize = default( Vector2 );

void Awake()
{
    characterActor = GetComponent<CharacterActor>();

    initialBodySize = characterActor.CharacterBody.BodySize;
}
```

Good, we now have the initial size. Now it's time to implement the crouch action. Let's say we are going to reduce the height to the half of the initial height. We want this only if we held the crouch button and the character is grounded.

```csharp
void Crouch()
{
    float targetHeight = 0f;
    
    if( characterActor.IsGrounded )
    {
        // Set the target height
        targetHeight = crouchHeld ? initialBodySize.y / 2f : initialBodySize.y;
    }
    else
    {
        // if is not grounded return to the initialHeight
        targetHeight = initialBodySize.y;
    }
    
    Vector2 targetBodySize = new Vector2(
        initialBodySize.x ,
        targetHeight 
    );
    
    characterActor.SetTargetBodySize( targetBodySize );
}
```

We add this to the update method:

```csharp
void UpdateCharacter()
{
    Crouch();
    Rotate();
    
    VerticalMovement();
    PlanarMovement();    
    
    Vector3 velocity = planarVelocity + verticalVelocity;  // for now
    
    // Set the linear velocity
    characterActor.SetLinearVelocity( velocity );
}
```

{% hint style="success" %}
Now the character should crouch when we press the Crouch button. Notice that the character is not returning to its original height if it doesn't fit in that space.
{% endhint %}



