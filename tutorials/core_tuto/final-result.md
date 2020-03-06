# Final result

Finally we are here! this is how the _TutorialController_ script should look \(copy paste the code if you want to test it by yourself\):

```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Core;

[RequireComponent( typeof( CharacterActor ) )] 
public class TutorialController : MonoBehaviour
{        

    [SerializeField]
    float speed = 6f;

    [SerializeField]
    float gravity = 9.8f;
    
    [SerializeField]
    float jumpSpeed = 7f;

    [SerializeField]
    float rotationSpeed = 180f;

    // Components
    CharacterActor characterActor = null;
    CharacterBody characterBody = null;

    //Inputs
    float forwardAxis = 0f;
    float rotationAxis = 0f;
    bool jumpPressed = false;
    bool crouchHeld = false;
    
    // Velocities
    Vector3 planarVelocity = default( Vector3 );
    Vector3 verticalVelocity = default( Vector3 );

    // Size
    Vector2 initialBodySize = default( Vector2 );
    

    void Awake()
    {
        characterActor = GetComponent<CharacterActor>();
        characterBody = GetComponent<CharacterBody>();

        initialBodySize = characterBody.BodySize;
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
        
        forwardAxis = Input.GetAxisRaw("Vertical");
        rotationAxis = Input.GetAxisRaw("Horizontal");
        jumpPressed |= Input.GetButtonDown( "Jump" );
        crouchHeld |= Input.GetButton( "Crouch" );
    }  
    
    void ResetInputs()
    { 
        forwardAxis = 0f;       
        rotationAxis = 0f;            
        jumpPressed = false;
        crouchHeld  = false;
    }
        

    void UpdateCharacter()
    {
        Crouch();
        Rotate();
        
        VerticalMovement();
        PlanarMovement();    
        
        Vector3 velocity = planarVelocity + verticalVelocity;
        
        characterActor.SetInputVelocity( velocity );
    }


    

    void Rotate()
    {
        float rotationAngle = rotationAxis * rotationSpeed * Time.deltaTime;
        Quaternion rotation = Quaternion.AngleAxis( rotationAngle , transform.up );

        Vector3 forwardDirection = rotation * characterActor.ForwardDirection;
        characterActor.SetForwardDirection( forwardDirection );

    }

    void VerticalMovement()
    {
        if( characterActor.IsGrounded )
        {
            verticalVelocity = Vector3.zero;
            
            if( jumpPressed )
            {
                characterActor.ForceNotGrounded();
                verticalVelocity = transform.up * jumpSpeed;
            }
        }
        else
        {
            verticalVelocity += - transform.up * gravity  * Time.deltaTime;
        }
    }

    void PlanarMovement()
    {
        Vector3 inputAxes = forwardAxis * Vector3.forward;
        
        inputAxes.Normalize();        
            
        planarVelocity = speed * inputAxes;   

        Quaternion rotation = Quaternion.FromToRotation( Vector3.forward , characterActor.ForwardDirection );
        planarVelocity = rotation * planarVelocity; 
        
    }

    void Crouch()
    {
        float targetHeight = 0f;
        
        if( characterActor.IsGrounded )
        {
            targetHeight = crouchHeld ? initialBodySize.y / 2f : initialBodySize.y;
        }
        else
        {
            targetHeight = initialBodySize.y;
        }
        
        Vector2 targetBodySize = new Vector2(
            initialBodySize.x ,
            targetHeight 
        );
        
        characterActor.SetTargetBodySize( targetBodySize );
    }
    
    
}
```

There are still a some important things we can do to improve this super basic character:

* smooth planar velocity \(not instant\).
* grounded and not grounded control.
* variable jump height.
* velocity projection.
* slide down from a steep slope \(unstable ground\).
* movement states \(very important as well\).
* etc.

The list goes on and on, the sky is the limit, really. The implementation included in the package does all these tasks and much much more! 😀.

