# Using collision events

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

