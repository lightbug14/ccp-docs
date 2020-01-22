# Moving the character



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



