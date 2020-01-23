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

Notice that the teleport method takes a rotation as well. 

So, what happens if we pass another value.

The answer is: nothing is going to happen. Rotation is determined by the character actor. If we need to change the rotation we need to modify its gravity modes first.



