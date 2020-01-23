# Rotation

If you refer back to the fundamentals of this documentation, section [Character actor](../../fundamentals/untitled/character-actor.md#orientation) says that the character does not rotate. The rotation of the character is indicated by the _forwardDirection_ vector.

So, we are going to modify this vector to "rotate" our character. 

It's really simple to do this, we only need to call the `SetForwardDirection` method from the _CharacterActor_ component:

```csharp
characterActor.SetForwardDirection( forwardDirection );
```

Just as a remainder, to rotate a vector you need to do the following:

```csharp
Vector3 rotatedVector = quaternion * inputVector;
```

|  |  |
| :--- | :--- |
| inputVector | the current _forwardDirection_ vector. |
| quaternion | a quaternion representing the rotation we want \(based on the rotationAxis input\). |
| rotatedVector | the desired _forwardDirection_ vector. |

So, we can write:

```csharp
[SerializeField]
float rotationSpeed = 50f;

void Rotate()
{
    float rotationAngle = rotationAxis * rotationSpeed * Time.deltaTime;
    Quaternion rotation = Quaternion.AngleAxis( rotationAngle , transform.up );

    Vector3 forwardDirection = rotation * characterActor.ForwardDirection;
    characterActor.SetForwardDirection( forwardDirection );

}
```

And finally:

```csharp
void UpdateCharacter()
{
    Rotate();
    
    VerticalMovement();
    PlanarMovement();    
    
    Vector3 velocity = planarVelocity + verticalVelocity;  // for now
    
    // Set the linear velocity
    characterActor.SetLinearVelocity( velocity );
}
```



