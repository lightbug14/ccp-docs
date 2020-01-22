# Creating a Character Controller

We are going to create a simple script where we are going to put all our code. This script is usually called a controller. What is that this script control? Movement? Rotation? well, as a general term, this controls some.

First of all let's create our script, we are going to call it "TutorialController":

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TutorialController : MonoBehaviour
{    
}
```

We need to include some of the CCP basic stuff in there.

1. The namespace
2. It would be nice to add a RequireComponent attribute, since we need a CharacterActor component to work with.
3. Add a CharacterActor field
4. Get the CharacterActor component in Awake

```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Core;

[RequireComponent( typeof( CharacterActor ) )] 
public class TutorialController : MonoBehaviour
{       
    CharacterActor characterActor = null;
     
    void Awake()
    {
        characterActor = GetComponent<CharacterActor>();
    }
    
}
```







```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Core;

[RequireComponent( typeof( CharacterActor ) )] 
public class TutorialController : MonoBehaviour
{
    [SerializeField]
    float speed = 5f;
    
    CharacterActor characterActor = null;
    
    void Awake()
    {
        characterActor = GetComponent<CharacterActor>();
    } 
    
    void FixedUpdate()
    {
        // Build an input vector
        Vector3 input = new Vector3( 
            Input.GetAxisRaw( "Horizontal" ) , 
            Input.GetAxisRaw( "QE" ) , 
            Input.GetAxisRaw( "Vertical" ) 
        );
    
        // Normalize it!
        input.Normalize();
    
        // Create a velocity based on the input and the speed
        Vector3 velocity = speed * input;
    
        characterActor.SetLinearVelocity( velocity );
    }
    
    
}
```









