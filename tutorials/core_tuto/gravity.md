# Gravity

Let's define a new velocity, the _vertical_ velocity. And also a gravity field.

```csharp
[SerializeField]
float gravity = 9.8f;

Vector3 verticalVelocity = default( Vector3 );
```

To implement gravity we need apply \(or not\) vertical velocity to the character. This can be done by reading the grounded state.

```csharp
if( characterActor.isGrounded )
{
    verticalVelocity = Vector3.zero;
}
else
{
    verticalVelocity += - transform.up * gravity  * Time.deltaTime;
}
```

Also remember to add this new _verticalVelocity_ to the final velocity:

```csharp
void UpdateCharacter()
{        
    VerticalMovement();
    PlanarMovement();    
    
    Vector3 velocity = planarVelocity + verticalVelocity;  // for now
    
    // Set the linear velocity
    characterActor.SetLinearVelocity( velocity );
}

void VerticalMovement()
{
    if( characterActor.isGrounded )
    {
        verticalVelocity = Vector3.zero;
    }
    else
    {
        verticalVelocity += - transform.up * gravity  * Time.deltaTime;
    }
}
```





Something very important to notice is that the character is able to move around freely, until it hits the ground. Once this happens it is impossible for the character to move upwards! This is because it has entered the _grounded_ state \(internally things work differenty, no matter the linear velocity value you are using\).

One cool thing you can do is to completely ignore this _grounded_ state by setting the _alwaysNotGrounded_ toggle in the _CharacterActor_ inspector.

In the next section we are going to overcome this by implement gravity and jump.

