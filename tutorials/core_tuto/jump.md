# Jump

The jump algorithm can be super complex depending on the technique used. For the sake of this tutorial we will make an instant velocity change.

Let's define the jump speed:

```csharp
[SerializeField]
float jumpSpeed = 10f;
```

#### So, Do we need to create a jumpVelocity Vector? 

The answer is **NO**. Jump and gravity are bound to each other, in fact they share the vertical velocity vector. 

The jumping code is as follows:

```csharp
void VerticalMovement()
{
    if( characterActor.IsGrounded )
    {
        verticalVelocity = Vector3.zero;
        
        if( jumpPressed )
            verticalVelocity = transform.up * jumpSpeed;
    }
    else
    {
        verticalVelocity += - transform.up * gravity  * Time.deltaTime;
    }
}
```

Great! to the next se~~ction~~ ... Not so fast! If you try to jump by pressing the Jump button nothing is going to happen. The character is not able to abandon the ground at all. 

#### Why is that? 

Once the character has hit the ground it will be impossible for it to move upwards. This is because it has entered the _grounded_ state, and in this state things work differenty \(due to the grounding technique\).

#### What can we do?

We must use the ForceNotGrounded method from the _CharacterActor_ component.

```csharp
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
```

{% hint style="success" %}
By now the character should move around, fall and jump.
{% endhint %}

