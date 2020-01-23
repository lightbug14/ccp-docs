# Rotation

If you refer back to the fundamentals of this documentation, section [Character actor](../../fundamentals/untitled/character-actor.md#orientation) says that the character does not rotate. The rotation of the character is indicated by the _forwardDirection_ vector.

So, we are going to modify this vector to "rotate" our character. 

It's really simple to do this, we only need to call the `SetForwardDirection` method from the _CharacterActor_ component:

```csharp
characterActor.SetForwardDirection( forwardDirection );
```

Just as a remainder, to rotate a vector you need to do the following:

```csharp
Vector3 rotatedVector = rotation * inputVector;
```

|  |  |
| :--- | :--- |
| inputVector | the current _forwardDirection_ vector |
| rotation |  |
|  |  |

