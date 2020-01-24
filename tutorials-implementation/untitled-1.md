# Improving the Tutorial controller

## Identifying old problems

Before we had a full "controller" in one script. that is, a component responsible for gettings inputs, and updating our character with those inputs.

So, by using the implementation we can:

* Reduce the size of the initial script, since now we are focus only on the behaviour of the character \(the previous`UpdateCharacter` method mostly\)
* Use the a state machine, so we can separate out focus into smaller scripts if needed.
* Use actions rather than inputs from a device.

## Solving those problems

### Getting rid of the unnecessary code

So, we don't need the components references:

```csharp
    // Components
    CharacterActor characterActor = null;
    CharacterBody characterBody = null;
```

Also we don't need all the input infromation \(varaibles and methods\) anymore \(the _CharacterBrain_ is doing that for us\):

```csharp
//Inputs
float forwardAxis = 0f;
float rotationAxis = 0f;
bool jumpPressed = false;
bool crouchHeld = false;

void ResetInputs()
{ 
    forwardAxis = 0f;       
    rotationAxis = 0f;            
    jumpPressed = false;
    crouchHeld  = false;
    teleportPressed = false;
} 
```

### Using the state machine

The update need to be change. Now it is not up to the state to handle the update process. This must override the _UpdateBehaviour_ method in order to update:

```csharp
void FixedUpdate()
{
    UpdateCharacter();
    ResetInputs();
}
```



```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Implementation;

// Now it is a state, not a simple MonoBehaviour
public class TutorialState : CharacterState
{        
    public override string Name
    {
        get
        {
            return "TutorialState ";
        }
    }
    

    [SerializeField]
    float speed = 6f;

    [SerializeField]
    float gravity = 9.8f;
    
    [SerializeField]
    float jumpSpeed = 7f;

    [SerializeField]
    float rotationSpeed = 180f;
    
    // Velocities
    Vector3 planarVelocity = default( Vector3 );
    Vector3 verticalVelocity = default( Vector3 );

    // Size
    Vector2 initialBodySize = default( Vector2 );
    
    // Now we need to override the Awake method.
    protected override void Awake()
    { 
        base.Awake();       
        initialBodySize = characterBody.BodySize;
    }     
    
    public override void UpdateBehaviour( float dt )
    {
        Crouch();
        Rotate();
        
        VerticalMovement();
        PlanarMovement();    
        
        Vector3 velocity = planarVelocity + verticalVelocity;

        characterActor.SetLinearVelocity( velocity );
    } 
    
    
    // The following methods need to be upgraded (inputs).
    void Crouch()
    {
        //...
    }
    
    void Rotate()
    {
        //...
    }

    
    void VerticalMovement()
    {
        //...
    }

    void PlanarMovement()
    {
        //...        
    }

    
    
    
}
```



### Implementing actions

We have to call the _CharacterBrain_ component \(protected\) and get the actions avaialble there. So, we can replace every input read by the corresponding action.

For example, the rotation axis is represented by the x component of the _inputAxes_ action. So, we can do this:

```csharp
float rotationAngle = CharacterActions.inputAxes.axesValue.x * rotationSpeed * Time.deltaTime;
```

## Final script

```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Implementation;

// Now it is a state, not a simple MonoBehaviour
public class TutorialState : CharacterState
{        
    public override string Name
    {
        get
        {
            return "TutorialState ";
        }
    }
    

    [SerializeField]
    float speed = 6f;

    [SerializeField]
    float gravity = 9.8f;
    
    [SerializeField]
    float jumpSpeed = 7f;

    [SerializeField]
    float rotationSpeed = 180f;
    
    // Velocities
    Vector3 planarVelocity = default( Vector3 );
    Vector3 verticalVelocity = default( Vector3 );

    // Size
    Vector2 initialBodySize = default( Vector2 );
    
    // Now we need to override the Awake method.
    protected override void Awake()
    { 
        base.Awake();       
        initialBodySize = CharacterActor.CharacterBody.BodySize;
    }     
    
    public override void UpdateBehaviour( float dt )
    {
        Crouch();
        Rotate();
        
        VerticalMovement();
        PlanarMovement();    
        
        Vector3 velocity = planarVelocity + verticalVelocity;

        CharacterActor.SetLinearVelocity( velocity );
    } 
    
    
    void Crouch()
    {
        float targetHeight = 0f;
        
        if( CharacterActor.IsGrounded )
        {
            targetHeight = CharacterActions.crouch.isHeldDown ? initialBodySize.y / 2f : initialBodySize.y;
        }
        else
        {
            targetHeight = initialBodySize.y;
        }
        
        Vector2 targetBodySize = new Vector2(
            initialBodySize.x ,
            targetHeight 
        );
        
        CharacterActor.SetTargetBodySize( targetBodySize );
    }
    
    void Rotate()
    {
        float rotationAngle = CharacterActions.inputAxes.axesValue.x * rotationSpeed * Time.deltaTime;
        Quaternion rotation = Quaternion.AngleAxis( rotationAngle , transform.up );
    
        Vector3 forwardDirection = rotation * CharacterActor.ForwardDirection;
        CharacterActor.SetForwardDirection( forwardDirection );
    
    }
    
    void VerticalMovement()
    {
        if( CharacterActor.IsGrounded )
        {
            verticalVelocity = Vector3.zero;
            
            if( CharacterActions.jump.isPressed )
            {
                CharacterActor.ForceNotGrounded();
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
        Vector3 inputAxes = CharacterActions.inputAxes.axesValue.y * Vector3.forward;
        
        inputAxes.Normalize();        
            
        planarVelocity = speed * inputAxes;   
    
        Quaternion rotation = Quaternion.FromToRotation( Vector3.forward , CharacterActor.ForwardDirection );
        planarVelocity = rotation * planarVelocity; 
        
    }   
}
```

{% hint style="success" %}
We ended up bringing our old TutorialController from the core world into the the implementation world. 

By making this simple conversion from one world to another you gained some cool features 😀.
{% endhint %}

## 



