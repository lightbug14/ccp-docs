# Implementing the state



Ok, now that we know how to create a state and read the input actions we are ready to do our own stuff inside the update behaviour methods. 

The _CharacterActor_ component has some public properties and methods we will want to modify. The most common is the _linear velocity_. By assigning this field we can say "move "



## Basic state structure

In our vision we want to make the character **move around** and **crouch**, so we need to set its **linear velocity** and **size** properly to fit our needs. This needs to be done in a frame by frame basis, so we proceed to write the update behaviour like this:

```csharp
public override void UpdateBehaviour( float dt ) 
{ 
    HandleSize( dt );
    HandleMovement( dt );
}
```

 _HandleSize_ and _HandleMovement_ will handle the size and movement respectively. The parameter _dt_ is equals to _Time.deltaTime_.

## Input handling

The more elemental thing to do is to read brain actions from the character \(human or AI\). This is accomplished by reading the \textit{CharacterAction} struct directly.

For example to check if the \textit{Jump} action was initiated \(button pressed down\):

```csharp
if( characterBrain.CharacterAction.jumpPressed )
{ 
    // Define the jump velocity vector ... 
}
```



## Size handling

Regarding the size, the only dimension that matters \(in this case\) is the height, so we define the _targetHeight_ and implement the _HandleSize_ method. Inside this method a targetSize is defined and passed to the _SetTargetBodySize_ method.



```csharp
void HandleSize( float dt ) 
{
    // Define the targetHeight...
    Vector3 targetSize = new Vector2( 
        CharacterActor.DefaultBodySize.x , 
        targetHeight 
    );

    CharacterActor.SetTargetBodySize( targetSize );
}
```

By doing this the character actor will check if the size is valid. If so, the character size will change. If not,  nothing is going to happen, the character size will remain the same.

## Movement handling

The most important properties to set is the _linear velocity._ So, calling the _CharacterActor_ `SetLinearVelocity` method would be a good place to start.

```csharp
void HandleMovement( float dt ) 
{ 
    Vector3 velocity = default( Vector3 ); // < -- ???
    CharacterActor.SetLinearVelocity( velocity );
}
```

Now, we have reached an interesting point. What velocity scheme we are going to use for this purpose. In the NormalMovement state, t**he final velocity is the sum of three separated velocities**. These are:

|  |  |
| :--- | :--- |
| Controlled velocity | Used for handling 100% controlled movement, such as walk, run and not grounded controlled movement. |
| Vertical velocity | Used for gravity-based movement such as jumping and gravity.  |
| External velocity | Used for handling external movement caused by rigidbodies impacts. |

So, by doing this we gain much more control. The disadvantage is that we need to implement the behaviour of all three velocities separately.

Now we need to implement the HandleMovement method:

```csharp
void HandleMovement( float dt ) 
{ 
    // Set the values for all the velocities
    Vector3 velocity = controlledVelocity + verticalVelocity + externalVelocity;
    CharacterActor.SetLinearVelocity( velocity );
}
```

{% hint style="info" %}
If you need to dig into the code please check the _NormalMovement.cs_ script.
{% endhint %}

## Entering the state

By only implementing the _UpdateBehaviour_ method we are reading a bunch of custom velocities \(from the _NormalMovement_ state exclusively\) and combining them to obtain a final velocity vector. 

Since the linear velocity is define within the state we can ask ourself: **What happens if a previous state had modified its value?**. If suddenly we are leaving another state and entering the _NormalMovement_ state the result will be inconsistent.

To fix this we can override the _EnterBehaviour_ method, use it to read the current linear velocity vector and update our custom velocities properly.

```csharp
public override void EnterBehaviour(float dt)
{
    verticalVelocity = Vector3.Project( CharacterActor.LinearVelocity , transform.up ); 
    controlledVelocity = Vector3.ProjectOnPlane( 
        CharacterActor.LinearVelocity , transform.up );
    externalVelocity = Vector3.zero;
}
```

So, everytime we came

## 

