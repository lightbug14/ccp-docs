# Getting inputs

We want to move around, jump and crouch. So, we need three types of input variables:

|  |  |
| :--- | :--- |
| inputAxes | To move using the Horizontal and Vertical Axis defined in the InputManager |
| jumpPressed | To detect if the jump button is pressed. |
| crouchHeld | To detect if the crouch key is being held |

{% hint style="info" %}
To avoid the classic Update/FixedUpdate syncronization problem for the Down/Up inputs, all the variables need to be "recorded" in Update and reset in FixedUpdate after they were used.

To fix this we are going to use an OR operation for the bools.
{% endhint %}

```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Core;

[RequireComponent( typeof( CharacterActor ) )] 
public class TutorialController : MonoBehaviour
{        
    CharacterActor characterActor = null;    
    
    Vector2 inputAxes = default( Vector2 );
    bool jumpPressed = false;
    bool crouchHeld = false;
    
    void Awake()
    {
        characterActor = GetComponent<CharacterActor>();
    } 
    
    void Update()
    {
        GetInputs();
    }
    
    void FixedUpdate()
    {
        UpdateCharacter();        
        ResetInputs();        
    }
    
    void GetInputs()
    {
        inputAxes = new Vector2( 
            Input.GetAxisRaw("Horizontal") ,
            Input.GetAxisRaw("Vertical")
        );
        
        jumpPressed |= Input.GetButtonDown( "Jump" );
        crouchHeld |= Input.GetButtonDown( "Crouch" );
    }
    
    void UpdateCharacter()
    {        
    }
    
    void ResetInputs()
    {
        inputAxes = Vector2.zero;        
        jumpPressed = false;
        crouchHeld  = false;
    }
    
    
}
```

Finally, now we are ready to use the inputs variables to modify the properties of the actor.

