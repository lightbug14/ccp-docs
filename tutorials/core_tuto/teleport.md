# Teleport

Finally, we need to implement our teleport functionality by calling the Teleport method. 

This method can use:

1. Transform reference... or 
2. Position and rotation. 

We are going to go with the second option. 

We need to teleport the character ten meters up \(10m = 10 units\), so we write:

```csharp
void Teleport()
{
    if( !characterActor.IsGrounded )
        return;
    
    if( teleportPressed )
    {
        characterActor.Teleport( 
            transform.position + transform.up * 10f , 
            transform.rotation //keep the current rotation
        );
    }
}
```

We add this to the update method:

```csharp
void UpdateCharacter()
{
    Teleport();
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

