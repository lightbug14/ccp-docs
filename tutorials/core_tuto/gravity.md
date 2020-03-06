# Gravity

Let's define a new velocity, the _vertical_ velocity. And also a gravity field.

```csharp
[SerializeField]
float gravity = 9.8f;

Vector3 verticalVelocity = default( Vector3 );
```

To implement gravity we need apply \(or not\) vertical velocity to the character. This can be done by reading the grounded state.

```csharp
void VerticalMovement()
{
    if( characterActor.IsGrounded )
    {
        verticalVelocity = Vector3.zero;
    }
    else
    {
        verticalVelocity += - transform.up * gravity  * Time.deltaTime;
    }
}
```

Also remember to add this new _verticalVelocity_ to the final velocity:

```csharp
void UpdateCharacter()
{        
    VerticalMovement();
    PlanarMovement();    
    
    Vector3 velocity = planarVelocity + verticalVelocity;  // for now
    
    // Set the input velocity
    characterActor.SetInputVelocity( velocity );
}
```

{% hint style="success" %}
You should see how the character falls until it hits the ground, thus entering the grounded state.
{% endhint %}

{% hint style="info" %}
One cool thing you can do is to completely ignore this _grounded_ state by setting the _alwaysNotGrounded_ toggle in the _CharacterActor_ inspector.
{% endhint %}

