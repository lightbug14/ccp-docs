# Use the character information \(with examples\)

Using the character information is one of those things are mandatory, especially if you want to create your custom gameplay logic. This information is usually exposed via getters \(read only public properties\).

## Grounded state

For example, knowing if the character is grounded or not can be achieve by getting the IsGrounded property.

```csharp
if( CharacterActor.IsGrounded )
{
    // Do grounded logic.
}
```

## Wall collision example

The same can be applied to some other property, for example, if we need to trigger some animation parameter only when the character is touching a wall:

```csharp
if( CharacterActor.WallCollision )
{
    animator.SetTrigger( "Wall" );
}
```

## Slide movement

Let's say our character is standing on top of a steep slope \(unstable state\) and we want to make it slide down. What we can do is getting the unstable state first amd then apply the movement \(downwards movement\).

```csharp
if( !CharacterActor.IsStable )
{
    // Do Slide
}
```

However, unstable means also not grounded, so we need to add one more condition:

```csharp
if( !CharacterActor.IsStable && CharacterActor.IsGrounded )
{
    // Do Slide
}
```

We can simply this condition by using the CurrentState property from the actor \(for more information please read the [States](../../fundamentals/untitled/character-actor/stability.md#states) section\).

```csharp
if( CharacterActor.CurrentState == CharacterActorState.UnstableGrounded )
{
    // Do Slide
}
```

Now, lets add one more condition. We want to execute the slide movement 1 second after making contact with this unstable surface. One way to do this is by using a timer, however, there is no need to implement one since the character actor gives this information via a public property called `GroundedTime` \(you have also `NotGroundedTime`, `StableGroundedTime` and `UnstableGroundedTime`\).

```csharp
if( CharacterActor.CurrentState == CharacterActorState.UnstableGrounded )
{
    if( CharacterActor.GroundedTime >= 1f )
    {
        // Do Slide
    }    
}
```

Making the character slide is very simple. Based on [this](../../fundamentals/untitled/character-actor/stability.md#stability) section, we know that only collide and slide is applied to the character. So, we need to move the character downwards, the collide and slide algorithm will handle that for us \(also, the physics simulation does the same thing\). 

So, this is the final code:

```csharp
if( CharacterActor.CurrentState == CharacterActorState.UnstableGrounded )
{
    if( CharacterActor.GroundedTime >= 1f )
    {
        CharacterActor.Velocity += - CharacterActor.Up * slideAcceleration * Time.deltaTime;
    }    
}
```



