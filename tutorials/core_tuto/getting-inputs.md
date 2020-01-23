# Getting inputs

## 1. Defining our inputs

Based on our vision for the character, we can define:

| Action | Keys | Axis Name \(Input Manager\) |
| :--- | :---: | :--- |
| Forward direction | WS | Vertical |
| Rotate Left/Right | AD | Horizontal |
| Jump | Space | Jump |
| Crouch | C | Crouch |
| Teleport | T | Teleport |

The next thing to do will be register all these inputs in the Unity's Input manager \(I will asume you already know how to do that\).

Still, we don't care about a button, what matters is the action that button has triggered. For example a ButtonDown, a ButtonUp, etc.

So let's redefine the inputs again as:

| Actions | Inputs | Axis Name \(Input Manager\) | Input actions |
| :--- | :---: | :--- | :--- |
| Forward direction | WS | Vertical | -1, 0 or 1 \(Axis Raw\) |
| Rotate Left/Right | AD | Horizontal | -1, 0 or 1 \(Axis Raw\) |
| Jump | Space | Jump | Jump when the button is pressed \(GetButtonDown\) |
| Crouch | C | Crouch | Crouch while the button is held down \(GetButton\) |
| Teleport | T | Teleport | Teleport when the button is pressed \(GetButtonDown\) |

{% hint style="info" %}
To avoid the classic Update/FixedUpdate syncronization problem for the Down/Up inputs, all the variables need to be "recorded" in Update and reset in FixedUpdate after they were used.
{% endhint %}

To do this we need to define our inputs as variables:

```csharp
float forwardAxis = 0f;
float rotationAxis = 0f;
bool jumpPressed = false;
bool crouchHeld = false;
bool teleportPressed = false;
```

## 2. Getting the inputs

The boolean fields need to acumule the current state of its asociated input. This can be done by using the OR operation.

```csharp
void GetInputs()
{    
    forwardAxis = Input.GetAxisRaw("Vertical");
    rotationAxis = Input.GetAxisRaw("Horizontal");    
    jumpPressed |= Input.GetButtonDown( "Jump" );
    crouchHeld |= Input.GetButton( "Crouch" );
    teleportPressed |= Input.GetButtonDown( "Teleport" );
}  
    
void ResetInputs()
{   
    forwardAxis = 0f;       
    rotationAxis = 0f;            
    jumpPressed = false;
    crouchHeld  = false;
    teleportPressed = false;
}

void FixedUpdate()
{
    UpdateCharacter();
    ResetInputs();
}
```

Finally, now we are ready to use these inputs variables and implement the _UpdateCharacter_ method.

