# Backup

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

### Velocity continuity

By only implementing the _UpdateBehaviour_ method we are reading a bunch of custom velocities \(from the _NormalMovement_ state exclusively\) and combining them to obtain a final velocity vector. 

Since the linear velocity is define within the state we can ask ourself:

#### What happens if a previous state had modified the linear velocity value?

Well, it is most probable that the character will change instantly its velocity, resulting in a not so pleasant result 😕. In some cases we must ensure velocity continuity between the states.

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

So, everytime we come from another state to the NormalMovement state, the velocity will be assigned to our own velocities \(controlled, vertical and external\).

## Collision events

We can take advantage of the character events to modify whatever parameter we want. In this case we need to convert the collision response into the _externalVelocity_ vector.

Another thing we need to do is to make zero our vertical velocity when the character hits something with its head \(typical scenario\). We achieve this by "listening" to the _OnHeadHit_ and _OnContactHit_ events, using the _OnHeadHit_ and _OnContactHit_ methods respectively:

```csharp
void OnEnable()
{
    CharacterActor.OnHeadHit += OnHeadHit; 
    CharacterActor.OnContactHit += OnContactHit;
}

void OnDisable()
{
    CharacterActor.OnHeadHit -= OnHeadHit;
    CharacterActor.OnContactHit -= OnContactHit;
}
```

And implementing those methods:

```csharp
void OnHeadHit( CollisionInfo collisionInfo )
{
    verticalVelocity = Vector3.zero;
}

void OnContactHit( Vector3 impulse )
{
    if( !rigidbodyResponseParameters.reactToRigidbodies )
        return;

    externalVelocity = impulse * rigidbodyResponseParameters.impulseMultiplier;
}
```



## 

