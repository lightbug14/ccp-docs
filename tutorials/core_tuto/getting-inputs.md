# Getting inputs

## 1. Defining our inputs

Based on our vision for the character, we can define:

|  |  |
| :--- | :--- |
| Forward direction | WS |
| Right direction | AD |
| Rotate Left/Right | QE |
| Jump | Space |
| Crouch | C |
| Teleport | T |

. So, we need three types of input variables:

|  |  |
| :--- | :--- |
| inputAxes | To move using the Horizontal, Vertical and QE\(q and e keys\) Axis defined in the InputManager. We are going to read "raw" axes. |
| jumpPressed | To detect if the jump button is pressed. |
| crouchHeld | To detect if the crouch key is being held |

{% hint style="info" %}
To avoid the classic Update/FixedUpdate syncronization problem for the Down/Up inputs, all the variables need to be "recorded" in Update and reset in FixedUpdate after they were used.

To fix this we are going to use an OR operation for the bools.
{% endhint %}

```csharp
Vector3 inputAxes = default( Vector3 );
bool jumpPressed = false;
bool crouchHeld = false;
```

## 2. Getting the inputs

```csharp
void GetInputs()
{
    inputAxes = new Vector3( 
        Input.GetAxisRaw("Horizontal") ,
        Input.GetAxisRaw("QE") ,
        Input.GetAxisRaw("Vertical")
    ).normalized;  //<- Normalized!
    
    jumpPressed |= Input.GetButtonDown( "Jump" );
    crouchHeld |= Input.GetButtonDown( "Crouch" );
}  
    
void ResetInputs()
{
    inputAxes = Vector3.zero;        
    jumpPressed = false;
    crouchHeld  = false;
}
```

Finally, now we are ready to use the inputs variables to modify the properties of the actor.

